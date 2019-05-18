# Commit messages guide

Przewodnik mający na celu ukazanie, jak ważne są commit messages, oraz jak pisać je lepiej.

Ma pomóc w zrozumieniu co to są commity, dlaczego ważne jest ich dobre opisanie, oraz pokazać dobre praktyki i kilka porad w planowaniu i tworzeniu historii zmian.

## W innych językach

- [angielski](README.md)
- [portugalski](README_pt-BR.md)
- [niemiecki](README_de-DE.md)
- [hiszpański](README_es-AR.md)
- [włoski](README_it-IT.md)

## Co to jest "commit"?

W prostych słowach, commit jest _migawką_ twoich plików lokalnych, zapisanych w twoim lokalnym repozytorium.
Wbrew przekonaniom niektórych, [git nie przechowuje wyłącznie różnic pomiędzy kolejnymi wersjami plików - przechowuje pełną wersję wszystkich plików](https://git-scm.com/book/pl/v2/Pierwsze-kroki-Podstawy-Git).
Dla plików, które nie uległy zmianie między commitami, git używa linku do poprzedniej (identycznej) wersji pliku, którą już przechowuje.

Obrazek poniżej pokazuje, jak git przechowuje dane w czasie, gdzie każda "wersja" jest commit-em:

![](https://i.stack.imgur.com/AQ5TG.png)

## Czemu commit messages są ważne?

- aby przyspieszyć przeglądy kodu
- aby pomóc w zrozumieniu wprowadzonej zmiany
- aby wyjaśnić te kwestie, których nie da się opisać w kodzie
- aby pomóc w utrzymaniu kodu w przyszłości, ukazując czemu i jakich zmian dokonano.

W celu uzyskania lepszych rezultatów, możesz skorzystać z kilku "dobrych praktyk" i wzorów

## Dobre praktyki

Kilka użytecznych wskazówek zebranych z _"my experiences, internet articles, and other guides"_. Jeśli znasz inne, podziel się nimi - zachęcamy do pull requestów.

### Używaj czasu teraźniejszego

Dotyczy to szczególnie historii zmian tworzonej w języku angielskim.

```
# Dobrze
Use InventoryBackendPool to retrieve inventory backend
```

```
# Źle
Used InventoryBackendPool to retrieve inventory backend
```

_Ale czemu czas teraźniejszy?_

Commit message opisuje, co wprowadzana zmiana **robi**, jej efekty, a nie co zostało zrobione (~~czas przeszły~~).

[Ten artykuł Chrisa Beams'a](https://chris.beams.io/posts/git-commit/) podaje prostą frazę, która może być używana by pomóc pisać lepsze commit messages w trybie rozkazującym:
```
If applied, this commit will <commit message>
```

Przykłady:

```
# Dobrze
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Źle
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Zaczynaj wielką literą

```
# Dobrze
Add `use` method to Credit model
```

```
# Źle
add `use` method to Credit model
```

Pierwsza litera powinna być _wielka_, ponieważ jest to zgodne z zasadami gramatyki.

Stosowanie (lub nie) tej reguły może się różnić w zależości od osoby / zespołu / języka.
Ważne jest jednak ustalić jeden standard, którego wszyscy w zespole będą się trzymać.

### Staraj się przekazać, co robi dana zmiana bez potrzeby sięgania do kodu.

```
# Dobrze
Add `use` method to Credit model

```

```
# Źle
Add `use` method
```

```
# Dobrze
Increase left padding between textbox and layout frame
```

```
# Źle
Adjust css
```

Jest to użyteczne w wielu przypadkach (np. wiele commitów, kilkukrotne zmiany i przeróbki) w późniejszym zrozumieniu, co commitujący miał na myśli.

### Używaj rozwinięcia wiadomości aby wyjaśnić "po co", "jak" i "dlaczego"

```
# Dobrze
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Dobrze
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Dobrze
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

Nagłówek oraz rozwinięcie wiadomości są oddzielane pustą linią.
Późniejsze puste linie są traktowane jako część rozwinięcia.

Znaki `-`, `*` oraz \` dodatkowo poprawiają czytelność.

### Unikaj ogólnych wiadomości oraz wiadomości bez żadnego kontekstu

```
# Źle
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### Ogranicz liczbę znaków

[Zaleca się](https://git-scm.com/book/pl/v1/Rozproszony-Git-Wgrywanie-zmian-do-projektu#Wskaz%C3%B3wki-wgrywania-zmian) używać maksymalnie 50 znaków w nagłówku i do 72 w rozwinięciu.


### Trzymaj się konsekwentnie języka

Dla menedżerów projektu: Wybierz język, w którym będą pisane wszystkie commit messages.
Najlepiej, jeśli będzie zgodny z komentarzami w kodzie, domyślnymi ustawieniami regionalnymi (dla lokalnych projektów), itp.

Dla programistów: Pisz własne commit messages używając tego języka, w którym do tej pory jest tworzona historia zmian.

```
# Dobrze
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Dobrze
ababab Dodanie metody `use` do modelu Credit
efefef Użycie InventoryBackendPool aby naprawić backend inwentarza
```

```
# Źle (mieszany polski i angielski)
ababab Dodanie metody `use` do modelu Credit
efefef Use InventoryBackendPool to retrieve inventory backend
cdcdcd Już działa
```

```
# Źle (polski i łacina)
ababab Dodanie metody `use` do modelu Credit
efefef Dlaczego *********** ********* ************
cdcdcd Naprawione
```

### Szablon

Poniżej wzór [napisany pierwotnie przez Tima Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), który pojawił się w [_Pro Git Book_](https://git-scm.com/book/pl/v1/Rozproszony-Git-Wgrywanie-zmian-do-projektu). ([EN](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project))

```

Krótki (50 znaków lub mniej) opis zmiany

Bardziej szczegółowy tekst jeżeli jest taka konieczność. Zawijaj
wiersze po około 72 znakach. Czasami pierwsza linia jest traktowana
jako temat wiadomości email, a reszta komentarza jako treść. Pusta
linia oddzielająca opis od streszczenia jest konieczna (chyba że
ominiesz szczegółowy opis kompletnie); narzędzia takie jak `rebase`
mogą się pogubić jeżeli nie oddzielisz ich.

Wyjaśnij problem, który rozwiązujesz tym commitem. Skup się na tym,
czemu wprowadzasz tą zmianę, a nie jak (wyjaśnia to kod).
Czy ta zmiana wywołuje jakieś efekty uboczne lub inne nieintuicyjne
konsekwencje? Tu jest miejsce na wyjaśnienie.

Kolejne paragrafy przychodzą po pustej linii.

 - wypunktowania też są poprawne

 - zazwyczaj myślnik lub gwiazdka są używane do punktowania,
   poprzedzone pojedynczym znakiem spacji, z pustą linią pomiędzy,
   jednak zwyczaje mogą się tutaj różnić.

Jeśli używasz issue trackera, zamieść odniesienia do niego na dole,
jak te:

Naprawia: #123
Zobacz też: #456, #789
```

## Rebase vs. Merge

This section is a **TL;DR** of Atlassian's excellent tutorial, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Applies your branch commits, one by one, upon the base branch, generating a new tree.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Creates a new commit, called (appropriately) a _merge commit_, with the differences between the two branches.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Why do some people prefer to rebase over merge?

I particularly prefer to rebase over merge. The reasons include:

* It generates a "clean" history, without unnecessary merge commits
* _What you see is what you get_, i.e., in a code review all changes come from a specific and entitled commit, avoiding changes hidden in merge commits
* More merges are resolved by the committer, and every merge change is in a commit with a proper message
    * It's unusual to dig in and review merge commits, so avoiding them ensures all changes have a commit where they belong

### When to squash

"Squashing" is the process of taking a series of commits and condensing them into a single commit.

It's useful in several situations, e.g.:

- Reducing commits with little or no context (typo corrections, formatting, forgotten stuff)
- Joining separate changes that make more sense when applied together
- Rewriting _work in progress_ commits

### When to avoid rebase or squash?

Avoid rebase and squash in public commits or in shared branches where multiple people work on.
Rebase and squash rewrite history and overwrite existing commits, doing it on commits that are on shared branches (i.e., commits pushed to a remote repository or that comes from others branches) can cause confusion and people may lose their changes (both locally and remotely) because of divergent trees and conflicts.

## Useful git commands

### rebase -i

Use it to squash commits, edit messages, rewrite/delete/reorder commits, etc.

```
pick 002a7cc Improve description and update document title
pick 897f66d Add contributing section
pick e9549cf Add a section of Available languages
pick ec003aa Add "What is a commit" section"
pick bbe5361 Add source referencing as a point of help wanted
pick b71115e Add a section explaining the importance of commit messages
pick 669bf2b Add "Dobrze practices" section
pick d8340d7 Add capitalization of first letter practice
pick 925f42b Add a practice to encourage Dobrze descriptions
pick be05171 Add a section showing Dobrze uses of message body
pick d115bb8 Add generic messages and column limit sections
pick 1693840 Add a section about language consistency
pick 80c5f47 Add commit message template
pick 8827962 Fix triple "m" typo
pick 9b81c72 Add "Rebase vs Merge" section

# Rebase 9e6dc75..9b81c72 onto 9e6dc75 (15 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into the previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

#### fixup

Use it to clean up commits easily and without needing a more complex rebase.
[This article](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) has very good examples of how and when to do it.

### cherry-pick

It is very useful to apply that commit you made on the wrong branch, without the need to code it again.

Example:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Let's say we have the following diff:

```diff
diff --git a/README.md b/README.md
index 7b45277..6b1993c 100644
--- a/README.md
+++ b/README.md
@@ -186,10 +186,13 @@ bebebe Corrige nome de método na classe InventoryBackend
 ``
 # Źle (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

We can use `git add -p` to add only the patches we want to, without the need to change the code that is already written.
It's useful to split a big change into smaller commits or to reset/checkout specific changes.

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### hunk 1

```diff
@@ -186,7 +186,6 @@
 ``
 # Źle (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]?
```

#### hunk 2

```diff
@@ -190,6 +189,10 @@
 ``
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
Stage this hunk [y,n,q,a,d,/,K,j,J,g,e,?]?

```

#### hunk 3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## Inne interesujące szpargały

https://whatthecommit.com/

## Podobało się?

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## Współpraca

Any kind of help would be appreciated. Example of topics that you can help me with:

- Grammar and spelling corrections
- Translation to other languages
- Improvement of source referencing
- Incorrect or incomplete information

## Inspirations, sources and further reading

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)

