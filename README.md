## I. GIT
### 1. Utwórz nową gałąź (np. nowa) z bieżącej (najczęściej będzie to main), stwórz w nowej gałęzi nowy plik i zmerguj nową gałąź do bieżącej.
- zaczynamy od utworzenia nowej gałęzi `git checkout -b nowa`
- stworzenie nowy_plik.txt: ` echo "To jest nowy plik" > nowy_plik.txt`
- dodanie pliku do repozytorium: `git add nowy_plik.txt`
- zatwierdzenie zmian `git commit -m "Dodano nowy plik w gałęzi nowa"`
- przejście na gałąź główną main `git checkout main`
- zmergowanie zmiany z nowej gałęzi do głównej gałęzi `git merge nowa`
![1](https://github.com/kleinszmidt/zaliczenieISI/assets/100431820/2ca054ef-eda3-4145-b360-a67cf94404cf)
### 2. Pokaż jak działa pull request na jednym ze swoich repozytoriów.
- Upewnij się, że twoje zmiany znajdują się na osobnej gałęzi:
Przed utworzeniem pull requestu warto upewnić się, że twoje zmiany znajdują się na oddzielnej gałęzi niż główna gałąź, np. main lub master.
- Przejdź do swojego repozytorium na GitHubie:
Zaloguj się na swoje konto na GitHubie i przejdź do repozytorium, w którym chcesz utworzyć pull request.

- Kliknij na przycisk "Pull Request":
Na stronie repozytorium znajdź zakładkę "Pull Request" i kliknij na nią.

- Wybierz gałąź:
Z rozwijanej listy wybierz gałąź, którą chcesz porównać z główną gałęzią (najczęściej będzie to gałąź, na której wprowadziłeś swoje zmiany).

- Przegląd zmian:
GitHub pokaże wszystkie zmiany wprowadzone w wybranej gałęzi. Sprawdź, czy wszystko jest tak, jak powinno być.

- Utwórz Pull Request:
Jeśli jesteś zadowolony ze swoich zmian, kliknij przycisk "Create Pull Request" (Utwórz Pull Request).

- Dodaj opis i tytuł:
Wprowadź tytuł i opis swojego pull requestu. Opis może zawierać informacje o celu zmian, sposobie ich przetestowania itp.

- Utwórz Pull Request:
Po dodaniu opisu i tytułu, kliknij przycisk "Create Pull Request" (Utwórz Pull Request) lub jego odpowiednik.

- Oczekiwanie na recenzję:
Teraz twój pull request został utworzony i inni współpracownicy mogą go przeglądać, komentować i recenzować. Możesz też być poproszony o wprowadzenie dodatkowych zmian.

- Merge Pull Request:
Po zakończeniu recenzji i ewentualnym wprowadzeniu poprawek, właściciel repozytorium może zmergować twoje zmiany do głównej gałęzi.
