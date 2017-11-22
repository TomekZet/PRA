=======================
Pracownia Programowania
=======================

--------------------
Continous Integration
--------------------

.. contents::

Continous Integration (pl. *Ciągła integracja*) - praktyka polegająca na częstym łączeniu (mergowaniu, integrowanie) zmian wprowadzanych przez wszystkich developerów pracujących nad projektem. Wprowadza wymóg, żeby główna gałąź (branch) projektu zawierał zawsze kod, który się kompiluje i przechodzi wszystkie testy jednostkowe.

W osiągnięciu powyższych celów pomocne są serwery/serwisy ciągłej integracji, takie jak Jenkins albo Travis.

---------
Travis CI
---------

`Travis CI <www.travis.-ci.org>`_ - bezpłatny (dla projektów Open Source) serwis ciągłej integracji.
 - bardzo łatwa integracja z GitHubem
 - bardzo łatwa konfiguracja
 - obsługa dużej liczby środowisk/języków

Zapewnia budowanie i testowanie (za pomocą testów jednostkowych) projektu automatycznie po wypchnięciu zmian do GitHuba.
 

~~~~~~~~~
Zadanie 1
~~~~~~~~~
1. Zaloguj się na `travis-ci.org <travis-ci.org>`_ za pomocą swojego konta GitHub.
2. Przyznaj usłudze Travis dostęp do swojego konta na GitHubie.
3. Będąc zalogowanym na konto Travis, przejdź do ustawień i aktywuj Travis CI dla swojego reopozytorium z Pracowni Programowania (kliknij na nazwę swojego konta w prawym górnym rogu i wybierz "Accounts" )
 
Możesz skorzystać z `Getting started <https://docs.travis-ci.com/user/getting-started>`_

~~~~~~~~~
Zadanie 2
~~~~~~~~~

Przełącz się na branch swojego repozytorium gdzie jest poprawnie budujący się projekt (np. master, który oddawałeś jako Przyrost 1.).

Stwórz w głównym katalogu swojego repozytorium plik .travis.yml.

Będzie on zawierał konfigurację twojego projektu. 

Dzięki temu pikowi Travis będzie wiedział jakie operacje wykonać, żeby zbudować i przetestować Twój projekt.

Przykładowy plik konfiguracyjny Travis:

.. code:: yaml

    before_script: cd PracowaniaProgramowania
    language: java


Pierwsza linijka sprawi, że przed wykonywaniem jakichkolwiek czynności Travis zmieni katalog na "PracowaniaProgramowania". 
Jest to konieczne, jeśli Twój plik pom.xml nie znajduje się w głównym folderze repozytorium, ponieważ Travis domyślnie wykonuje polecenia właśnie w głównym folerze.

W drugiej linijce definiujemy Java jako język projektu.

Tw dwie informacje, oraz plik pom.xml w Twoim repozytorium, wystarczą, żeby automatycznie zbudowac i przetestować Twój projekt.


~~~~~~~~~
Zadanie 3
~~~~~~~~~
Sprawdź poprawność składniową stworzonego w poprzednim zadaniu pliku.

Możesz to zrobić na `dwa sposoby <https://docs.travis-ci.com/user/travis-lint>`_.

Łatwieszy z nich to użycie narzędzia dostępnego online: `Travis WebLint <http://lint.travis-ci.org/>`_

~~~~~~~~~
Zadanie 4
~~~~~~~~~
Jeśli twój plik przeszedł pomyślnie sprawdzenie w Zadaniu 3, możesz go zacommitować i wypchnąć (push) commit do GitHuba.

Sprawdź na głównej stronie Travis (po zalogowaniu) jak buduje się Twój projekt i zobacz, czy udało się go zbudować bez błędów.

~~~~~~~~~
Zadanie 5
~~~~~~~~~
Dodaj do pliku README w swoim repozytorim odznakę Travis, która pokazuje w README twojego projektu na GitHub aktualny status na Travis.
Skorzystaj z `tej instrukcji <https://docs.travis-ci.com/user/status-images/>`_ wybierając np. Markdown jako format wyjściowy (jeśli wybierzesz Markdown zmień nazwę pliku README na README.md)
