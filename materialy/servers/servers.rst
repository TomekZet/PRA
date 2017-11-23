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
     - w Windows: `<https://www.java.com/pl/download/help/path.xml>`_ (instrukcja dotyczy ustawiania zmiennej Path, my chcemy ustawić CATALINA_HOME)
     - w Linux:

        .. code:: bash

            export CATALINA_HOME=/home/tomek/apache-tomcat-8.5.2

       Jeżeli chemy, żeby zmienna ta była ustawiana automatycznie w każdej konsoli, którą uruchomimy, należy dodać powyższą linijkę do pliku ~/.bashrc

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 2 - uruchamianie serwera
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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


--------------------
Konfiguracja dostępu
--------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Zadanie 4 - konfiguracja dostępu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Wejdź na domyślną stronę dostarczoną wraz z Tomcatem: http://localhost:8080/

Kliknij na `"Server Status" <http://localhost:8080/manager/status>`_.

Powinno pojawić się okienko pytające o nazwę i hasło użytkownika.

Ze względów bezpieczeństwa Tomcat nie ma zdefiniowanych domyślnych użytkowników.

    Role, które umożliwiają na dostęp do aplikacji Manager są wyjaśnione tutaj: http://localhost:8080/docs/manager-howto.html#Configuring_Manager_Application_Access

Edytując plik $CATALINA_HOME/conf/tomcat-users.xml dodaj użytkownika "guest", przypisz mu hasło (może byc puste) i dodaj uprawnienie "manager-status":

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



~~~~~~~~~
Zadanie 5
~~~~~~~~~
