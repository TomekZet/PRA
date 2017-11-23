=======================
Pracownia Programowania
=======================

.. contents::

-----------------
Serwery aplikacji
-----------------


-------------
Apache Tomcat
-------------

Apache Tomcat – serwer aplikacji webowych rozwijany w ramach projektu Apache.

Jako kontener aplikacji jest serwerem, który umożliwia uruchamianie aplikacji internetowych w technologiach Java Servlets i Java Server Pages (JSP). Jest to jeden z bardziej popularnych kontenerów Web. Tomcat jest wykorzystywany w takich serwerach aplikacji JEE (J2EE) jak Apache Geronimo. Jest również bardzo popularnym kontenerem dla samodzielnych aplikacji (niewymagających pełnego serwera aplikacji) pisanych w środowisku Spring Framework. `[Wikipedia] <https://pl.wikipedia.org/wiki/Apache_Tomcat>`_


Dokumentacja Tomcata: `<https://tomcat.apache.org/tomcat-8.5-doc/introduction.html>`_

~~~~~~~
Pojęcia
~~~~~~~

**Document root**
    główny katalog aplikacji webowej gdzie znajdują się jej zasoby

**Context path**
    relatywna ścieżka do zasobów serwera.

    Na przykład, jeżeli umieścimy aplikację webową w katalogu $CATALINA_HOMEwebappsmyapp , to będziemy mogli się do niej dostać poprzez link URL http://localhost/myapp, a jej context path będzie równy /myapp.

**WAR**
    rozszerzenie pliku pakietu zawierającego aplikację webową w formacie ZIP (skrót od Web Archive). Zazwyczaj aplikacje Javowe są pakowane jako WAR przez deploymentem. Zwykle plik ten tworzony jest przez środowisko programistyczne.

    Po wgraniu pliku WAR, Tomcat rozpakowuje go i zapisuje jego pliku w nowym podkatalogu w katalogu webapps.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 1 - ściągnij Tomcata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Ściągnij binarną dystrybucję Tomcata w wersji 8.5 odpowiednią dla używanego systemu ze strony `<https://tomcat.apache.org/download-80.cgi>`_

 - w przypadku Windowsa wybierz paczkę `zip <http://ftp.ps.pl/pub/apache/tomcat/tomcat-8/v8.5.23/bin/apache-tomcat-8.5.23.zip>`_
 - w przypadku Linuxa wybierz paczkę `tar.gz <http://ftp.ps.pl/pub/apache/tomcat/tomcat-8/v8.5.23/bin/apache-tomcat-8.5.23.tar.gz>`_

Rozpakuj ściągniętą paczkę w dowolne miejsce. 

Po rozpakowaniu otrzymasz foler *apache-tomcat-8.5.2*.
Od teraz ścieżkę do tego folderu będziemy nazywać *"CATALINA_HOME"*

Ustaw ścieżkę do CATALINA_HOME jako wartość zmiennej systemowej *CATALINA_HOME*

.. admonition:: Wskazówka

    Jak zmienić zmienną środowiskową:
     - w Windows: `<https://www.java.com/pl/download/help/path.xml>`_ (instrukcja dotyczy ustawiania zmiennej Path, my chcemy ustawić CATALINA_HOME), albo:
        
        .. code:: bat

            set CATALINA_HOME=J:\apache-tomcat-8.5.2


     - w Linux:

        .. code:: bash

            export CATALINA_HOME=/home/tomek/apache-tomcat-8.5.2

       Jeżeli chemy, żeby zmienna ta była ustawiana automatycznie w każdej konsoli, którą uruchomimy, należy dodać powyższą linijkę do pliku ~/.bashrc

~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 2 - urucham serwer
~~~~~~~~~~~~~~~~~~~~~~~~~~

Uruchom serwer Tomcat korzystając ze skryptu $CATALINA_HOME/bin/startup.[sh|bat]

.. code:: bash


    $CATALINA_HOME/bin/startup.sh 
    Using CATALINA_BASE:   /home/tomek/apache-tomcat-8.5.23/
    Using CATALINA_HOME:   /home/tomek/apache-tomcat-8.5.23/
    Using CATALINA_TMPDIR: /home/tomek/apache-tomcat-8.5.23//temp
    Using JRE_HOME:        /usr
    Using CLASSPATH:       /home/tomek/apache-tomcat-8.5.23//bin/bootstrap.jar:/home/tomek/apache-tomcat-8.5.23//bin/tomcat-juli.jar
    Tomcat started.

~~~~~~~~~~~~~~~~~~~~~~
Zadanie 3 - przetestuj
~~~~~~~~~~~~~~~~~~~~~~
W katalogu $CATALINA_HOME/webapps/sample/ znajduje się przykładowa aplikacja.

Sprawdź, czy aplikacja działa. Powinna być dostępna pod adresem: http://localhost:8080/sample/

Sprawdź, czy działa zarówno `JSP page <http://localhost:8080/sample/hello.jsp>`_ jak i `Servlet <http://localhost:8080/sample/hello>`

Jeśli "JSP page" nie działa, to najprawdopodobniej musisz ustawić zmienną systemową *JAVA_HOME* na ścieżkę do JDK Java 8:

.. code:: bash
    
    tomek@tomek-Lubuntu:~$ java -version
    openjdk version "9-internal"
    tomek@tomek-Lubuntu:~$ which java
    /usr/bin/java
    tomek@tomek-Lubuntu:~$ realpath /usr/bin/java
    /usr/lib/jvm/java-9-openjdk-amd64/bin/java
    tomek@tomek-Lubuntu:~$ ls /usr/lib/jvm/
    java-1.8.0-openjdk-amd64  java-1.9.0-openjdk-amd64  java-8-openjdk-amd64  java-9-openjdk-amd64
    tomek@tomek-Lubuntu:~$ export JAVA_PATH=/usr/lib/jvm/java-8-openjdk-amd64/

Wyłącz i włącz ponownie Tomcat i sprawdź, czy po ustawieniu *JAVA_HOME* strona JSP zaczęła działać poprawnie:

.. code:: bash

    tomek@tomek-Lubuntu:~$ $CATALINA_HOME/bin/shutdown.sh 
    Using CATALINA_BASE:   /home/tomek/apache-tomcat-8.5.23/
    Using CATALINA_HOME:   /home/tomek/apache-tomcat-8.5.23/
    Using CATALINA_TMPDIR: /home/tomek/apache-tomcat-8.5.23//temp
    Using JRE_HOME:        /usr
    Using CLASSPATH:       /home/tomek/apache-tomcat-8.5.23//bin/bootstrap.jar:/home/tomek/apache-tomcat-8.5.23//bin/tomcat-juli.jar


    tomek@tomek-Lubuntu:~$ $CATALINA_HOME/bin/startup.sh 
    Using CATALINA_BASE:   /home/tomek/apache-tomcat-8.5.23/
    Using CATALINA_HOME:   /home/tomek/apache-tomcat-8.5.23/
    Using CATALINA_TMPDIR: /home/tomek/apache-tomcat-8.5.23//temp
    Using JRE_HOME:        /usr/lib/jvm/java-8-openjdk-amd64/
    Using CLASSPATH:       /home/tomek/apache-tomcat-8.5.23//bin/bootstrap.jar:/home/tomek/apache-tomcat-8.5.23//bin/tomcat-juli.jar
    Tomcat started.

Jeśli wszystko działa, powinieneś mieć również dostęp do dokumentacji Tomcata, która jest z nim dostarczona i domyślnie udostępniana przez sam serwer: `<http://localhost:8080/docs/index.html>`

--------------------
Konfiguracja dostępu
--------------------
Tomcat umożliwia kontrolę dostępu do aplikacji odpalonych na serwerze. Aplikacje mogą (ale nie muszą) korzystać z metody uwierzytalniania dostarczonych przez Tomcat.

Żeby umożlwić kontrolę dostępu, Tomcat korzysta z bazy danych użytkowników, zwanej *Realm*.

*Realm* zawiera listę nazw użytkowników, ich haseł i ról (*roles*).

Role pozwalają na nadawanie grupom użytkowników uprawnień. Przypominają Linuxowe *grupy* użytkowników.\

Jeden użytkownik może mieć przypisane kilka ról.


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 4 - skonfiguruj dostęp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Wejdź na domyślną stronę dostarczoną wraz z Tomcatem: http://localhost:8080/

Spróbuj obejrzeć status serwera klikając na `"Server Status" <http://localhost:8080/manager/status>`_.

Powinno pojawić się okienko pytające o nazwę i hasło użytkownika.

Ze względów bezpieczeństwa Tomcat nie ma zdefiniowanych domyślnych użytkowników.

Role, które umożliwiają na dostęp do aplikacji Manager są wyjaśnione tutaj: http://localhost:8080/docs/manager-howto.html#Configuring_Manager_Application_Access

Edytując plik $CATALINA_HOME/conf/tomcat-users.xml dodaj użytkownika "guest", przypisz mu hasło (może byc puste) i dodaj rolę "manager-status":

.. code:: xml

    <tomcat-users xmlns="http://tomcat.apache.org/xml"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://tomcat.apache.org/xml tomcat-users.xsd"
              version="1.0">
    <!--
      NOTE:  By default, no user is included in the "manager-gui" role required
      to operate the "/manager/html" web application.  If you wish to use this app,
      you must define such a user - the username and password are arbitrary. It is
      strongly recommended that you do NOT use one of the users in the commented out
      section below since they are intended for use with the examples web
      application.
    -->
      <user username="guest" password="" roles="manager-status"/>

    </tomcat-users>

Spróbuj jeszcez raz zalogować się do aplikacji `"manager/status" <http://localhost:8080/manager/status>`_.


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 5 - zarządzaj, podejście 1.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Manager to aplikacja pozwalająca na zarządzanie Tomcatem z poziomu przeglądarki.

Jest ona dostarczona domyślnie uruchamiana wraz z Tomcatem.

Jej częścią jest strona  `Server Status <http://localhost:8080/manager/status>`_, którą odwiedzialiśmy w poprzednim zadaniu.

Spróbuj wejść na stronę menedżera:  http://localhost:8080/manager/html

Ponownie edytuj plik $CATALINA_HOME/conf/tomcat-users.xml tym razem dodając użytkownika *admin* i przypisując mu rolę nadającą uprawnienia dostępu do strony managera.

Sprawdź, czy po zalogowaniu jako admin masz dostęp do menedżera.

Jeśli jesteś zalogowany jako guest, spróbuj w innej przeglądarce albo uruchom ponownie przeglądarkę.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 6 - zarządzaj, podejście 2.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Kiedy skonfigurujemy nasz serwer, nie chcemy, by użytkownicy mieli dostęp do przykładowych aplikacji dostarczonych z Tomcatem, dlatego warto je wyłączyć.
Jedną z takich aplikacji jest aplikacja "sample", którą otwieraliśmy w zadaniu 3. (http://localhost:8080/sample/)
Spróbujemy teraz wyłączyć tę aplikację.

Wejdź na stronę menedżera:  http://localhost:8080/manager/html

Zatrzymaj ("Stop") aplikację "sample", którą otwierałeś w zadaniu 3. (http://localhost:8080/sample/)

Sprawdź, czy strona jest dostępna.

Zatrzymaj i uruchom ponownie serwer i sprawdź, czy teraz aplikacja sample jest dostępna.

Za pomocą "Undeploy" zatrzymaj i usuń aplikację sample.

Zatrzymaj i uruchom ponownie serwer i sprawdź, czy teraz aplikacja sample jest dostępna.

Zauważ, że aplikacja została usunięta z katalogu $CATALINA_HOME/webapps/sample i nie ma jej na liście aplikacji w menedżerze Tomcata.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 7 - Dodaj nową aplikację
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Dodawanie nowych aplikacji ("Deployment") odbywa się automatycznie po skopiowaniu ich do katalogu $CATALINA_HOME/webapps/
Możemy też zrobić to z poziomu menedżera Tomcat.

Ściągnij na dysk pliki

    http://mw.home.amu.edu.pl/zajecia/PRA2017/SimpleServlet.zip

Wypakuj do katalogu i uruchom Intellij

Wybierz Project -> Open i znajdź wybrany katalog.

Wybierz okienko Mavena odśwież (jeżeli trzeba dodaj plik pom) i wykonaj clean, install.

W oknie drzewa projektu powinien pojawić się katalog target a w nim plik SimpleServlet-1.war.

Skopiuj ten plik do katalogu webapps Tomcata. Sprawdź czy działa wchodząc na link http://localhost:8080/SimpleServlet-1/hello


~~~~~~~~~~~~~~~~~~~~~
Zadanie 8 - monitoruj
~~~~~~~~~~~~~~~~~~~~~
Obejrzyj logi w $CATALINA_HOME/logs

Zmień poziom logowania z FINE na FINEST i z INFO na FINE

Zaobserwuj różnice.

~~~~~~~~~~~~~~~~~~~~~~
Zadanie 9 - zmień port
~~~~~~~~~~~~~~~~~~~~~~
Domyślnie Tomcat uruchamia się na porcie 8080. Jeżeli jakiś inny proces zajmuje już ten port to otrzymamy błąd przy uruchomieniu serwera.

Aby zmienić port wejdź w ustawienia w pliku **server.xml** znajdującego się w $CATALINA_HOME/conf/server.xml.

Zmień port na 8081, uruchom drugi raz Tomcata.

Sprawdź w przeglądarce czy aplikacje działają na porcie 8081? Sprawdź w logach co się stało.

Przerestartuj tomacata, czy teraz uruchomił się na porcie 8080?

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 10 - debugowanie zdeployowanej aplikacji
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Wyłącz Tomcata i włącz korzystając z

.. code:: bash

    export JPDA_ADDRESS=8000
    export JPDA_TRANSPORT=dt_socket | $CATALINA_HOME/bin/catalina.sh jpda start


Na windows :

.. code:: bat

    set JPDA_ADDRESS=8000
    set JPDA_TRANSPORT=dt_socket
    bin/catalina.bat jpda start

Address to port do nasłuchiwania przy debugowaniu.

Wróć do InteliJ (projekt SimpleServlet z zadania 7.)

W intellij wybierz **Run -> Debug** następnie **Edit Configurations**, w okienku Wybier z lewej strony plus i opcję **Remote**.

W nowo otwartym oknie zmień port na **8000** i kliknij debug. Od tego momentu jesteś podłączony debugerem do zdeployowanej aplikacji na Tomcat.

Dodaj breakpoint w 16 lini pliku SimpleServlet.java i odśwież stronę. Powinieneś złapać się breakpointem na tej linijce!
