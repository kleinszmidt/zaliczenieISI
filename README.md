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
`git push origin nowa` wyycham zmiany z lokalnego repozytorium na zdalne
- W repozytorium na GitHubie przechodze do zakładki "Pull requests".
- "New pull request".
- wybieram odpowiednie gałęzie do porównania i utwórz Pull Request.
- opis zmian, przeglądanie zmiany i review.
- wszystko jest w porządku, zatwierdź i scalam zmiany.

### 3. Omów różnicę między git fetch a git pull na przykładzie swojego repozytorium.
- git fetch pobiera dane z zdalnego repozytorium, ale nie aktualizuje automatycznie lokalnych gałęzi. Pozwala to na przeglądanie zmian bez wprowadzania ich do swojego lokalnego repozytorium.
  `git fetch origin`
- git pull pobiera dane z zdalnego repozytorium i automatycznie łączy je z bieżącą gałęzią. Jest to połączenie git fetch i git merge.
`git pull origin main`
