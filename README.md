## I. GIT
### 1. Utwórz nową gałąź (np. nowa) z bieżącej (najczęściej będzie to main), stwórz w nowej gałęzi nowy plik i zmerguj nową gałąź do bieżącej.
-tworze nowe repozytorium 
- clonuje repozytorium z githuba
![git](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/77525f55-74fd-4f2e-b896-7ade15d437a7)

- zaczynamy od utworzenia nowej gałęzi `git checkout -b nowa`
- stworzenie nowy_plik.txt: ` echo "To jest nowy plik" > nowy_plik.txt`
- dodanie pliku do repozytorium: `git add nowy_plik.txt`
- zatwierdzenie zmian `git commit -m "Dodano nowy plik w gałęzi nowa"`
- przejście na gałąź główną main `git checkout main`
- zmergowanie zmiany z nowej gałęzi do głównej gałęzi `git merge nowa`
![nowagalaz](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/a909a5d1-aaf0-4518-938a-62a36e08ca47)


### 2. Pokaż jak działa pull request na jednym ze swoich repozytoriów.
`git push origin nowa` wyycham zmiany z lokalnego repozytorium na zdalne
![gitpush](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/239c7987-6daf-4aea-9c6f-10ca6a1a1357)

- następnie na gitcie naciskam na Compare & pull request Wypełniam szczegóły pull requesta i klikam Create pull request a potem merguje

### 3. Omów różnicę między git fetch a git pull na przykładzie swojego repozytorium.
- git fetch pobiera dane z zdalnego repozytorium, ale nie aktualizuje automatycznie lokalnych gałęzi. Pozwala to na przeglądanie zmian bez wprowadzania ich do swojego lokalnego repozytorium.
  `git fetch`
  `git log origin/main`
  ![gitfetch](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/062bab9e-b9a1-46ea-aa53-b2ec7f095d63)

- git pull pobiera dane z zdalnego repozytorium i automatycznie łączy je z bieżącą gałęzią. Jest to połączenie git fetch i git merge.
`git pull origin main`

### 4. Pokaż działanie git stash.
- `git stash` pozwala na tymczasowe zapisanie zmian w czystym repozytorium. Jest to przydatne, gdy chcesz przełączyć się na inną gałąź bez konieczności commitowania niedokończonej pracy.
- wprowdzam zmiany w repozytorium
`echo "Niezapisane zmiany" > plik.txt
git add plik.txt`
- uzywam `git stash` do tymczasowego zapisania zmian
- `git status`- Sprawdź stan repozytorium (zmiany zostały zapisane i usunięte z bieżącej gałęzi)
- `git stash pop` - przywracam zmiany z stash
![gitstash](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/0d333c45-ae87-4922-86c3-032bd4211586)
### 5. Omów działanie git rebase i wskaż różnice w stosunku do git merge (mile widziany rysunek).
`git merge`: Tworzy dodatkowy commit scalający, który łączy dwie historie. `git rebase`: Przenosi commity z jednej gałęzi na szczyt innej, tworząc liniową historię.

Obie metody mają swoje zastosowania. merge jest bezpieczniejszy, ponieważ zachowuje pełną historię, natomiast rebase jest użyteczny, gdy chcesz utrzymać czystszą i liniową historię commitów.
Gałąź main: Posiada commity A, B, C, D, E.
Gałąź feature-branch: Rozgałęzia się od commita C i zawiera commity F oraz G.

A---B---C---D---E main \ / \ / F---G feature-branch

Po rebase:

A---B---C---D---E---F'---G' main, feature-branch

-Po operacji, obie gałęzie (main i feature-branch) zawierają linowy ciąg commitów A, B, C, D, E, F', G, operacja rebase została wykonana, ale tym razem feature-branch została przepisana na bazę main, zaczynając od commitu A.

## II. Bazy danych
### 1. Za pomocą skryptu w wybranym języku dodaj kolejny rekord do wskazanej bazy danych.
```
import sqlite3

# tworze połączenie z bazą danych (lub nową bazę danych)
conn = sqlite3.connect('przykladowa_baza.db')

# tworze kursor do wykonywania poleceń SQL
cursor = conn.cursor()

try:
    # tutaj przykładowa tabela w bazie danych o nazwie Uzytkownicy z kolumnami id imie nazwisko itp
    cursor.execute('''CREATE TABLE IF NOT EXISTS Uzytkownicy 
                      (id INTEGER PRIMARY KEY, imie TEXT, nazwisko TEXT, wiek INTEGER)''')

    # dodaje nowy rekord do tabeli, i wykonuje polecenie insert zeby dodac nowy rekord do tabeli Uzytkownicy- nowe dane
    nowe_dane = ('Jan', 'Kowalski', 30)
    cursor.execute("INSERT INTO Uzytkownicy (imie, nazwisko, wiek) VALUES (?, ?, ?)", nowe_dane)

    # zatwierdzam zmiany za pomocą commit()
    conn.commit()
    print("Rekord został dodany pomyślnie.")

    # wyswietlenie komunikatu o bledzie jest bedzie zle sie wykonywalo polecenie sql
except sqlite3.Error as e:
    print("Wystąpił błąd przy dodawaniu rekordu:", e)

finally:
    # niezaleznie czy jest blad zamyka sie polaczenie z baza danych
    conn.close()

# kod tworzy nową tabelę w bazie danych SQLite, jeśli nie istnieje, a następnie dodaje nowy rekord do tej tabeli.
```
### 2. Dla wybranej bazy danych pokaż działanie co najmniej trzech różnych typów JOIN'a.
- utworzyłam tabele
```
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS orders (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL,
    product TEXT NOT NULL,
    quantity INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```
- umiesciałm dane do tabeli
```
INSERT INTO users (name, email) VALUES
('John Doe', 'john.doe@example.com'),
('Jane Smith', 'jane.smith@example.com'),
('Alice Johnson', 'alice.johnson@example.com');

INSERT INTO orders (user_id, product, quantity) VALUES
(1, 'Laptop', 1),
(2, 'Smartphone', 2),
(3, 'Tablet', 1),
(1, 'Headphones', 1);
```
- `INNER JOIN` zwraca tylko te wiersze, które mają pasujące wartości w obu tabelach.
```
SELECT users.name, orders.product
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```
- left join LEFT JOIN zwraca wszystkie wiersze z lewej tabeli (users), nawet jeśli nie mają pasujących rekordów w prawej tabeli (orders).
```
SELECT users.name, orders.product
FROM users
LEFT JOIN orders ON users.id = orders.user_id;
```
- right join ale sqlite nieobsługuje right joina więc odwrociłam left joina RIGHT JOIN zwraca wszystkie wiersze z prawej tabeli (orders), nawet jeśli nie mają pasujących rekordów w lewej tabeli (users).
```
SELECT users.name, orders.product
FROM orders
LEFT JOIN users ON users.id = orders.user_id;
```

### 3. Zaloguj się do bazy danych PostgreSQL w kontenerze Dockerowym i wykonaj operację SELECT dla dowolnej tabeli.
- ` docker exec -it baza_postgres psql -U postgres`
  
`CREATE TABLE students( id SERIAL PRIMARY_KEY, student_id INT REFERENCES students2(id), course_name VARCHAR(100));`

`INSERT INTO students2 (name) VALUES ('Jan Kowalski');`

` docker exec -it baza_postgres psql -U postgres -d postgres -c "SELECT * FROM students;"`
![postgres](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/c3223680-678c-4921-8394-9d53eda65ae8)

### 4. Wskaż różnice między SQLite a PostgreSQL na wybranym przez siebie przykładzie.
- PostgreSQL wymaga oddzielnego procesu serwera i konfiguracji, podczas gdy SQLite jest prostszy w użyciu i nie wymaga oddzielnego serwera ani konfiguracji.
- w SQlite nie ma RIGHT JOIN

### 5. Przygotuj zapytania zawierające polecenia WHERE, LIKE, COUNT, GROUP BY, HAVING i bądz gotowy do ich uruchomienia i modyfikacji.
- WHERE:
```
SELECT * 
FROM users
WHERE name = 'John Doe';
```
- LIKE:
```
SELECT * 
FROM users 
WHERE name LIKE 'J%';
```
- COUNT:
```
SELECT users.name, COUNT(orders.id) AS orders_count
FROM users
LEFT JOIN orders ON users.id = orders.user_id
GROUP BY users.id;
```
- GROUP BY
```
SELECT product, COUNT(id) AS orders_count
FROM orders
GROUP BY product;
```
- HAVING:
```
SELECT product, COUNT(id) AS orders_count
FROM orders
GROUP BY product
HAVING COUNT(id) > 0;
```
## III. Aplikacja wg wzorca projektowego MVC (Model-View-Controller)

### 1. Czym jest ORM, zaprezentuj praktycznie na przykładzie własnego projektu.
ORM (Object-Relational Mapping) to technika programowania, która umożliwia mapowanie obiektów w kodzie na rekordy w bazie danych. W praktyce oznacza to, że zamiast korzystać bezpośrednio z języka SQL do operacji na bazie danych, możemy używać obiektów w naszym kodzie, a ORM zajmie się tłumaczeniem tych operacji na odpowiednie zapytania SQL.







## IV. Docker
### 1. Utwórz plik z obrazem Dockerfile, w którym z hosta do kontenera kopiowany będzie folder code (zawiera np. jeden skrypt w języku Python 🐍) i zbuduj go: uruchom ww. skrypt wewnątrz kontenera.
- utworzyłam skrypt w pythonie `script.py`
- utworzyłam plik `Dockerfile`
```
# Użyj obrazu bazowego Pythona
FROM python:3.9

# Utwórz katalog docelowy w kontenerze
WORKDIR /app

# Skopiuj plik script.py z hosta do katalogu /app w kontenerze
COPY script.py /app

# Określ, co ma zostać wykonane po uruchomieniu kontenera
CMD ["python", "/app/script.py"]
```
- `docker build -t my-python-app .`
![myapp](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/d2daef24-7447-4cfc-9152-e03310f4bd73)
-`docker run my-python-app` - uruchomiłam ww. skrypt wewnatrz kontenera
![skrypt](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/09b20976-1a39-46dc-a4cc-601225eb98cb)

### 2. Skopiuj wybrany plik tekstowy z hosta (swojego komputera) do kontenera Dockerowego
- docker run -it --name my_container python - utworzylam nowy kontener
![nowykontener](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/41d39931-5009-48a0-a55b-ae76d410f0d2)
- kopiowanie pliku tekstowego do kontenera
`docker cp C:/Users/klein/PycharmProjects/pythonProject/data/sample.txt my_container:/app`
  ![plikdokontenera](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/5a9aae00-0daa-4083-b786-845ab7d352cf)

### 3. Skopiuj wybrany plik tekstowy z kontenera Dockerowego do hosta (swojego komputera).
- `docker cp my_container:/app C:/Users/klein/PycharmProjects/pythonProject/data/`
![kopiowanieplikupng](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/cffb9e14-a2d4-43c4-975f-da90279b9acf)

### 4. Pokaż użycie komend ENTRYPOINT i CMD.

- utworzyłam nowy projekt pythonProject1 z `app.py`
```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```
- potem utworzylam cmd.Dockerfile
```
FROM python:3.9

WORKDIR /app

COPY . /app

RUN pip install flask

CMD ["python", "app.py"]
```
- `docker build -f cmd.Dockerfile -t cmd .` - zbudowałam go
![cmdDockerfile](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/ec2d6575-fc5f-403b-9902-3a5ca2c58e99)

- teraz gdy chce dodac nowe polecenie do cmd np /dev to reszta polecen sie nie wykonana
![dev](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/46daba84-4d0c-4494-9300-f567e9e4cdd7)
- przy uzyci entrypointa bede mogla dopisac polecenie
```
FROM python:3.9

WORKDIR /app

ADD . /app

RUN pip install flask

ENTRYPOINT ["python", "app.py"]
```
- `docker build -f entrypoint.Dockerfile -t entrypoint .` - buduje go
- i następnie dopisze komende `docker run entrypoint /dev` zostanie ona wykonana na końcu, dopisana.

### 5. Pokaż użycie komend ADD i COPY i WORKDIR w swoim projekcie.
`add` działa jak `copy` Kopiuje pliki i katalogi z lokalnego systemu plików do systemu plików obrazu Docker z tą różnica ze moze kopiować z linku i pliki tar. `workdir` utworzy katalog jesli nie istenije, ustawia katalog roboczy dla wszystkich kolejnych instrukcji tzn. jesli ustawimy katalog /app to wszytskie polecenia np COPY test.txt będą zapisywane w tym katalogu
- tworze plik notepad vol.Dockerfile
```
FROM ubuntu
WORKDIR /app
COPY text.txt .
CMD pwd && ls
```
- `docker build -f vol.Dockerfile -t vol_test .` buduje go
- utworzenie pliku `Dockerfile`
```
FROM ubuntu

# Ustaw katalog roboczy na /app
WORKDIR /app

# Skopiuj plik text.txt do katalogu roboczego
COPY text.txt .

# Dodaj plik tar.gz do katalogu roboczego i rozpakuj go
ADD sample.tar.gz .

# Uruchom polecenie, aby sprawdzić zawartość katalogu roboczego
CMD pwd && ls -la

```
- utworzenie pliku sample.tar.gz, który będzie używay przez komendę `ADD`
'tar -czf sample.tar.gz text.txt' 
- `docker build -t my_project_image .` - Używam poniższego polecenia, aby zbudować obraz Docker na podstawie pliku Dockerfile.
- `docker run --rm my_project_image` - Użyj poniższego polecenia, aby uruchomić kontener na podstawie stworzonego obrazu.

![sampletargz](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/fb28a5f3-c990-4171-966e-23820573be41)

- WORKDIR upraszcza ścieżki do plików i katalogów, ustawiając domyślny katalog roboczy.
- COPY służy do prostego kopiowania plików i katalogów z hosta do obrazu Docker.
- ADD jest bardziej zaawansowane niż COPY, ponieważ może rozpakowywać archiwa tar.

### 6. Pokaż działanie docker compose w swoim projekcie.
- Docker Compose- system do automatyzacji uruchamiania i budowania wielu kontenerów na raz
Docker Compose to narzędzie, które umożliwia definiowanie i zarządzanie wielokontenerowymi aplikacjami Docker. Umożliwia uruchomienie wielu usług kontenerowych zdefiniowanych w jednym pliku YAML. Dzięki Docker Compose możesz łatwo budować, uruchamiać i skalować aplikacje składające się z wielu kontenerów.
- `docker-compose` 
- `notepad docker-compose.yml`
```
version: '3.8'

services:
  web:
    build:
      context: .
      dockerfile: cmd.Dockerfile
    ports:
      - "5000:5000"
```
- `docker-compose up` 
![docker-composeup](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/5de47016-f85b-4419-9598-ef7bf2b6ac05)
- WORKDIR: Ustawia katalog roboczy w kontenerze. W tym przypadku WORKDIR /app ustawia katalog roboczy na /app, co oznacza, że wszystkie polecenia RUN, CMD, ENTRYPOINT, COPY i ADD będą działać w tym katalogu.
- COPY: Kopiuje pliki z systemu plików hosta do systemu plików kontenera. W tym przypadku COPY . /app kopiuje całą zawartość bieżącego katalogu (.) do katalogu /app w kontenerze.
- ADD: Działa podobnie jak COPY, ale może również pobierać pliki z URL i automatycznie rozpakowywać archiwa tar. Jest to bardziej elastyczne polecenie, ale w tym projekcie nie było używane.

### 7. Omów na podstawie swojej aplikacji komendy docker inspect i docker logs.
`docker inspect` zawiera wszytskie informacje o kontenerze, jak nazywa się jego sieć z jakiego portu korzysta, jaki ma obraz, czego uzywa dockerfile (cmd). `docker logs` służy do wyświetlania dzienników kontenera. Pozwala na przeglądanie wszystkich logów wypisywanych przez procesy wewnątrz kontenera.

### 8. Czym są sieci w Dockerze? Zaprezentuj przykład na bazie swojego projektu.
Sieci w Dockerze służą do zarządzania łącznością między kontenerami i hostami. Umożliwiają komunikację między różnymi kontenerami oraz łączność z zasobami sieciowymi na hoście. Docker oferuje kilka rodzajów sieci, takich jak bridge, host, overlay, macvlan itp.
- `docker-compose` z siecia my_network
```
services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "5000:5000"
    networks:
      - my_network

networks:
  my_network:
```
- docker-compose up
![problem](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/cee92f74-6836-4b4a-a2d7-22aa4a04ae6a)

- gdy wystapil jakikolwiek blad uzycie `docker-compose up -d`-która uruchamia kompozycję w trybie tła, co pozwoli ci zobaczyć błędy kontenera bez przerywania działania procesu.
![helloworld](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/dcc0d2f7-aa71-4de0-a30b-6cd10e28f9d4)
