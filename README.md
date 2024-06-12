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
-`git merge`: Tworzy dodatkowy commit scalający, który łączy dwie historie. `git rebase`: Przenosi commity z jednej gałęzi na szczyt innej, tworząc liniową historię.

Obie metody mają swoje zastosowania. merge jest bezpieczniejszy, ponieważ zachowuje pełną historię, natomiast rebase jest użyteczny, gdy chcesz utrzymać czystszą i liniową historię commitów.
Gałąź main: Posiada commity A, B, C, D, E.
Gałąź feature-branch: Rozgałęzia się od commita C i zawiera commity F oraz G.

A---B---C---D---E main \ / \ / F---G feature-branch

Po rebase:

A---B---C---D---E---F'---G' main, feature-branch

-Po operacji, obie gałęzie (main i feature-branch) zawierają linowy ciąg commitów A, B, C, D, E, F', G, operacja rebase została wykonana, ale tym razem feature-branch została przepisana na bazę main, zaczynając od commitu A.
