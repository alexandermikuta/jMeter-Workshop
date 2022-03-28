<!-- section 0 -->

# jMeter Workshop {#jmeter-workshop .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

![performance testing with jMeter](assets/jmeter.jpg){height="20%" width="20%"}

<!-- section 1 -->

# jMeter Workshop

Agenda:

  Tag 1                                 Tag 2
  ------------------------------------- ------------------------------------
  \(3\) jMeter Plugin-Manager           \(3\) Verteiltes Testen mit jMeter
  \(3\) Workload Design                 \(3\) RMI
  \(2\) Strukturierung von Testplänen   \(2\) Monitoring
  \(2\) Scripting                       \(1\) Containerisierung
  \(2\) Reporting                       \(1\) CI/CD-Pipeline
  \(1\) Testdatenverwaltung             Klärung offener Punkte
  \(1\) REST-APIs                       

<!-- section 2 -->

# jMeter Plugin-Manager {#jmeter-plugin-manager .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 3 -->

# jMeter Plugin-Manager

<https://jmeter-plugins.org/wiki/PluginsManager/>

![](assets/pmgr_menu_item.png)

**Installation:**

-   lade **<https://jmeter-plugins.org/get/>** herunter
-   kopiere **jar** in das jMeter-Verzeichnis **lib/ext**

<!-- section 4 -->

# jMeter Plugin-Manager

**Ausführung über die Kommandozeile:**

<https://jmeter-plugins.org/wiki/PluginsManagerAutomated/>

`PluginsManagerCMD <command> [<params>]`

z.B.

`PluginsManagerCMD install jpgc-fifo,jpgc-json=2.2`

<!-- section 5 -->

# jMeter Plugin-Manager

**Falls man hinter einem Proxy ist:**

`JVM_ARGS="-Dhttps.proxyHost=myproxy.com -Dhttps.proxyPort=8080 -Dhttp.proxyUser=john -Dhttp.proxyPass=***" PluginsManagerCMD status`

<!-- section 6 -->

# jMeter Plugin-Manager

**Eigenes Plugin schreiben:**

<https://jmeter.apache.org/usermanual/jmeter_tutorial.html>

**Eigenes Repository hinzufügen:**

jMeter-Property setzen:

`jpgc.repo.address=https://jmeter-plugins.org/repo/;http://my.intranet.site/plugins-repo.json`

Das Repository-JSON muss folgendes Format erfüllen: <https://jmeter-plugins.org/wiki/PluginRepositoryDescriptorFormat/>

Gute Anleitung: <https://www.blazemeter.com/blog/how-to-create-a-local-repository-of-jmeter-plugins>

<!-- section 7 -->

# jMeter Plugin-Manager

**Nützliche Plugins:**

-   Custom Thread Groups
-   JMXMon Sample Collector
-   jp\@gc - PerfMon
-   jp\@gc - Dummy Sampler
-   jp\@gc - PlanCheck

<!-- section 8 -->

# jMeter Plugin-Manager

**Ultimate Thread Group**

![<https://jmeter-plugins.org/wiki/UltimateThreadGroup/>](assets/ultimate_thread_group1.png){height="40%" width="40%"}

<!-- section 9 -->

# jMeter Plugin-Manager

**Concurrency Thread Group**

![<https://jmeter-plugins.org/wiki/ConcurrencyThreadGroup/>](assets/ConcurrencyThreadGroup.png){height="40%" width="40%"}

<!-- section 10 -->

# jMeter Plugin-Manager

**jp\@gc - PerfMon**

![<https://jmeter-plugins.org/wiki/PerfMon/>](assets/servers_performance_monitoring.png){height="40%" width="40%"}

<!-- section 11 -->

# jMeter Plugin-Manager

**jp\@gc - Dummy Sampler**

![<https://jmeter-plugins.org/wiki/DummySampler/>](assets/dummy_sampler.png){height="40%" width="40%"}

<!-- section 12 -->

# jMeter Plugin-Manager

**jp\@gc - PlanCheck**

<https://jmeter-plugins.org/wiki/TestPlanCheckTool/>

Usage:

`jmeter/lib/ext/TestPlanCheck.sh --jmx MyTestPlan.jmx --stats --tree-dump`

<!-- section 13 -->

# jMeter Plugin-Manager

**JMXMon Sample Collector**

![<https://jmeter-plugins.org/wiki/JMXMon/>](assets/jmxmon_samples_collector.png){height="40%" width="40%"}

<!-- section 14 -->

# Workload Design {#workload-design .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 15 -->

# Workload

Definition:

> The amount of work a system has to perform in a given time. In the performance field, a workload usually refers to combined load placed on an application by the set of clients it services

<!-- section 16 -->

# Prinzipien

-   Vorhersagbarkeit

-   Wiederholbarkeit

-   Skalierbarkeit

<!-- section 17 -->

# Vorhersagbarkeit

> Das Verhalten des Systems (z.B. Prozessanfragen, Datenzugriffe, ...) sollte während die Workload läuft vorhersehbar sein.

![](assets/predictable.png)

<!-- section 18 -->

# Wiederholbarkeit

> Wenn eine Workload mehrere male auf identische Weise ausgeführt wird, sollte die Ergebnis nahezu identisch ausführen. Ansonsten wird eine Performance-Analyse sehr schwer.

<!-- section 19 -->

# Skalierbarkeit

> Eine Workload solle mit unterschiedlichen Lasten ausgeführt werden können um die Skalierbarkeit der Anwendung testen zu können.

<!-- section 20 -->

# Workload Design Steps

-   Design der Applikation
-   Key-Szenarios identifizieren
-   Definieren der Metriken
-   Design der Load
-   Definieren der Skalierungsregeln
-   Design des Load-Generators
-   Festlegung einer Baseline

<!-- section 21 -->

# Design der Applikation

-   Definieren der Aktoren und Use-Cases → Hilft die Operationen der Workload zu definieren

-   Definieren der Operationen

    -   Im einfachsten Fall mappt jeder User-Case auf eine Operation
    -   Für sinnvolle Workloads solle die Zahl der benötigen Operation klein gehalten werden (6-8) → Ansonsten schwer zu managen und verstehen

<!-- section 22 -->

# Key-Szenarios identifizieren

-   Messbares Szenario: Ein User-Szenario das Performance-getestet werden soll, sollte vollständig messbar sein
-   Meistbenutzte Szenarios
-   Business-kritische Szenarios
-   Ressourcen-intensive Szenarios
-   Zeitabhängig häufig genutzte Szenarios: z.B. Weihnachts-Liste auf Amazon
-   Stakeholder-relevante Szenarien

<!-- section 23 -->

# Key-Szenarios identifizieren

Beispiel für eine E-Commerce-Applikation:

-   Browsen des Produktkatalogs
-   Benutzeraccount anlegen
-   Nach einem Produkt suchen
-   Login
-   Bestellung abschicken

Navigationspfade der Key-Szenarios untersuchen

-   Auf welche Arten kann ich z.B. eine Bestellung abschicken
-   Wie häufig wird welcher Weg genutzt? → Logfiles oder Analysetools (z.B Matomo)

<!-- section 24 -->

# Definieren der Metriken

Typische Metriken sind:

-   **Durchsatz:** Wie viele Operation können vom SUT während einer gewissen Zeit verarbeitet werden

-   **Anwortzeiten:** Zeit zwischen Ende der Anfrage und Beginn der Anwort an das SUT → Macht normalerweise nur Sinn wenn es auch Anforderungen für Antwortzeiten gibt

-   **Ressourcenverbrauch:** z.B. alle Ressourcen (IO, Memory, ...) sollten nicht mehr als 70% der max. Auslastung haben

-   **Anzahl maximaler Benutzer:** Wie viele Benutzer können gleichzeitig ohne Probleme auf dem SUT arbeiten

<!-- section 25 -->

# Design der Load

-   der wichtigste Schritt im Workload Design!

-   die Relevanz der Workload hängt davon ab wie genau sie die die reale Produktionslast emuliert

-   gleichzeit wichtig: die Test-Workload solle sich auf die signifikanten Aspekte der Live-Load konzentrieren → Ansonsten wird es zu kompliziert

<!-- section 26 -->

# Design der Load

-   **Arrival Rates:** Die Rate mit der Requests an das SUT gestellt werden

-   **Think Times:** Zeit zwischen Anzeige der Daten beim Benutzer und seiner nächsten Interaktion → Bei großen Datenmenge steigt diese Zeit

-   **Browser Mix:** Welche Browser sollen im Test verwendet werden? Chrome, Firefox, ...

-   **Network Mix:** Welche Netzwerkgeschwindigkeiten sollen im Test verwendet werden? z.B. 3G

<!-- section 27 -->

# Design der Load

-   **Operation Mix:** Festlegung in welcher Frequenz welche Operation durchgeführt wird → oft prozentual je Operation was sich zu 100% summiert

<!-- section 28 -->

# Design der Load

**Operation Mix:**

-   Flat Mix:
    -   Einfachste Möglichkeit
    -   wird verwendet wenn Operation unabhängig sind und die gleiche Wahrscheinlichkeit haben
    -   → Der Mix wählt eine Operation zufällig

<!-- section 29 -->

# Design der Load

**Operation Mix:**

-   Flat Sequence Mix:
    -   Spezifiziert ein Set von Operations-Sequenzen
    -   z.B. Set1=Op1,Op2 und Set2=Op1,Op3
    -   jedem Set wird eine Wahrscheinlichkeit zugeordnet und dementsprechen ausgewählt

<!-- section 30 -->

# Design der Load

**Operation Mix:**

-   Matrix Mix (Transition Mix):
    -   Beschreibt die Überangswahrscheinlichkeiten in einem Markov-Modell
    -   wird häufig bei Web-Apps verwendet

<!-- section 31 -->

# Design der Load

Beispiel-Workload als Matrix-Mix:

  From     To Page 1   To Page 2   To Page 2
  -------- ----------- ----------- -----------
  Page 1   0,00 %      80,00%      20,00%
  Page 2   20,00%      39,00%      41,00%
  Page 3   60,00%      19,00%      21,00%

<!-- section 32 -->

# Design der Load

-   Abhängig von der Operation müssen für den Request diverse Input-Daten generiert werden

-   Um ein realistisches Szenario zu erhalten sollten die Daten variiert werden → Bei 100 Items sollten nicht immer fix 5 selektiert werden

-   Best-Practice: Eine klein Zahl an Fehlern durch invalide Daten einfügen um auch Probleme im Error-Handling aufzudecken

-   Genieren "echter" Daten kann bei großen Daten problematisch werden → Workload Entwickler müsste all Möglichen Values kennen

    -   Uniform Random: Generierung von gleichverteilten Zufallsdaten, z.B. für Anzahl gewählter Items
    -   Non-Uniform Random: in normalfall sind Datenzugriffe nicht gleichverteilt! → Datengenerierung sollte Wahrscheinlichkeit berücksichtigen

<!-- section 33 -->

# Definieren der Skalierungsregeln

Häufig skaliert man durch Erhöhung der emulierten Benutzer.
Weitere Möglichkeiten sind:

Linear Scaling

-   alles wird über einen einzigen Skalierungsfaktor skaliert
-   z.B. Workload führt Datenzugriffe eines Benutzers aus → Anzahl Benutzer & Anzahl Datenzugriffe werden beide skaliert
-   Häufig nützlich für "Sizing"-Zwecke

Non-linear Scaling:

-   Anwendungen skalieren oft nicht linear
-   z.B. Tagging durch Benutzer → mit steigender Anzahl steigt die Last je User mit an, z.B. bei der Anzeige der Tags

<!-- section 34 -->

# Design des Load-Generators

Der Load-Generator implementiert die Workload

Dabei sollte beachtet werden:

-   Zum simulieren mehrerer Benutzer-Connections sollte **kein** connection-pooling verwendet werden

-   Jeder simulierte Nutzer sollte nach Möglichkeit seinen eigenen "Random number generator" (seeded mit unique value) verwenden um wirklich zufällige Daten zu bekommen

<!-- section 35 -->

# Festlegung einer Baseline

> \"A Baseline is the process of capturing performance metric data for the sole purpose of evaluating the efficacy of successive changes to the system or application. It is important that all characteristics and configurations, except those specifically being varied for comparison, remain the same in order to make effective comparisons as to which change (or series of changes) is driving results toward the targeted goal.

<!-- section 36 -->

# Festlegung einer Baseline

> Armed with such baseline results, subsequent changes can be made to the system configuration or application and testing results can be compared to see whether such changes were relevant or not.\"

Some considerations when generating baselines: <https://www.oreilly.com/library/view/performance-testing-with/9781787285774/8c67a2ab-7bda-4a64-bb90-6c0b8785ad60.xhtml>

<!-- section 37 -->

# Praxisbeispiel

Nachdem die zeitliche Verteilung der Last mittels Load-Design ermittelt wurde, soll gezeigt werden wie so etwas in jMeter umgesetzt werden kann.

Beispiel:

-   40% anonyme Benutzer browsen auf der Webseite
-   30% authentifizierte Benutzer browsen auf der Webseit
-   20% führen eine Suche durch
-   10% bearbeiten ihren Shopping-Cart

<!-- section 38 -->

# Praxisbeispiel

Wir müssen also dafür sorgen das die einzelnen Use-Case mit den entsprechende Wahrscheinlichkeiten nachgebildet werden. Hierfür gibt es im Prinzip 3 Möglichkeiten:

-   Unterschiedliche Thread-Groups mit unterschiedlicher Anzahl an Threads
-   Throughput Controller
-   Switch Controller

<!-- section 39 -->

# Praxisbeispiel

Variante 1: Unterschiedliche Thread-Groups mit unterschiedlicher Anzahl an Threads

-   Thread Group mit 40 Benutzern
-   Thread Group mit 30 Benutzern
-   Thread Group mit 20 Benutzern
-   Thread Group mit 10 Benutzern

Wichtig: Checkbox "Run Thread Groups consecutevly" sollte dem gewünschten Test-Flow entsprechen

<!-- section 40 -->

# Praxisbeispiel

Variante 2: Throughput Controller mit unterschiedlichen "Execution Percentages"

-   Throughput Controller (Percent Execution, 40.0) → some sampler
-   Throughput Controller (Percent Execution, 30.0) → some sampler
-   Throughput Controller (Percent Execution, 20.0) → some sampler
-   Throughput Controller (Percent Execution, 10.0) → some sampler

<!-- section 41 -->

# Praxisbeispiel

Komplexeres Beispiel für Variante 2:

![https://www.blazemeter.com/blog/load-testing-for-your-black-friday](assets/throughput_controller.png)

<!-- section 42 -->

# Praxisbeispiel

Variante 3: Switch Controller - Random Weighted Values

![Erzeugt mit entsprechender Wahrscheinlichkeit Werte zwischen 0 und 3](assets/switch_controller.png)

<!-- section 43 -->

# Erkennen der Last-Grenzen / Server-Bedarfs

> Last-Grenzen können sehr gut mittels Stress-Testing ermittelt werden.

Beispiel: Thread Group → HTTP Request → Response Assertion (Code 200) → View Results in Table

<!-- section 44 -->

# Erkennen der Last-Grenzen / Server-Bedarfs

![](assets/stress-testing.png)

<!-- section 45 -->

# Erkennen der Last-Grenzen / Server-Bedarfs

Es ist sinnvoll zu prüfen warum der Stress-Test ab einem gewissen Punkt fehlschlägt (z.B. Daten aus JMXMon, Logs der App, ...):

-   zu wenig Arbeitsspeicher?
-   IO zu langsam
-   Netzwerk zu langsam
-   Prozessor zu langsam
-   DB zu langsam
-   Load-Balancer überlastet?
-   Messaging-Queue als Bottleneck?

<!-- section 46 -->

# Erkennen der Last-Grenzen / Server-Bedarfs

> Evtl. reicht es aus dem System etwas mehr Speicher zu geben oder eine kleine Code-Anpassung anstatt es verteilen zu müssen

<!-- section 47 -->

# Elemente/Strukturierung von Testplänen {#elementestrukturierung-von-testplänen .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 48 -->

# Elemente/Strukturierung von Testplänen

-   Thread Groups
-   Sampler
-   Controller
-   Timers
-   Assertions
-   Listener
-   Pre-/Post-Prozessoren
-   Configuration Elements
-   Cookie-Manager / Header-Manager
-   Variablen / Properties
-   Testfragmente & Templates
-   Ausführungsreihenfolge

<!-- section 49 -->

# Thread Groups

> A Thread Group in JMeter represents a pool of virtual users performing a set of operations

![](assets/2.Thread_Group_User.png)

<!-- section 50 -->

# Thread Groups

![](assets/threadGroup.webp)

Wichtigste Einstellungen:

-   Anzahl Threads
-   Anzahl der Wiederholungen
-   Ramp-Up-Zeit einstellen (wichtig z.B. für Spike-Testing bei Ticketverkauf!)

<!-- section 51 -->

# Thread Groups

**Beispiel: Google-Suche**

-   Ein Teil der Nutzer verwendet die Text-Suche, andere die News- oder Bilder-Suche

-   Hierfür kann man verschieden Thread-Gruppen mit unterschiedlichem Thread-Count anlegen

-   In diesen Thread-Gruppen werden diverse Sampler (z.B. Http-Requests) hinzugefügt um die Benutzer-Requests zu simulieren

<!-- section 52 -->

# Thread Groups

![Performance Test-Arten](assets/performance-testing-types-1-300x284.png)

<!-- section 53 -->

# Thread Groups

-   **Load Testing:** Modeliert die erwartete Benutzung

-   **Stress Testing:** Bestimmung des Limits an Concurrent Usern bis fehler auftreten

-   **Soak/Endurance Testing:** Festgelegte Load die über einen definierten Zeitraum aufrecht erhalten wird

-   **Spike Testing:** testen von schnellem Anstieg/Abfall der Load -\> z.B. Ticketverkauf

-   **Volume Testing:** Testen ob Applikation mit einem bestimmten Datenvolumen klar kommt

-   **Scalability Testing:** Testet die Fähigkeit einer Applikation hoch/runter zu skalieren

<!-- section 54 -->

# Thread Groups

  ----------------------------------------------------------------------------------------------------------------
  Name                              Use-Cases
  --------------------------------- ------------------------------------------------------------------------------
  Thread Group classic              Einfache Szenarios, Stress/Soak Testing

  Arrivals Thread Group             Soak Testing, wie verhält sich die App wenn all n-Minuten x-User hinzukommen

  Free Form Arrivals Thread Group   Vergleichbar mit Arrival Thread Group

  Concurrency Thread Group          Wie klassiche Threadgroup. Aber einfacher und weniger Speicherbedarf

  Stepping Thread Group             Ältere Version der Threadgroup mit mehr Konfigurationsaufwand

  Ultimate Thread Group             Komplexe Spike Testing Szenarios
  ----------------------------------------------------------------------------------------------------------------

<!-- section 55 -->

# Thread Groups

  -----------------------------------------------------------------------------------------------
  Name                    Use-Cases
  ----------------------- -----------------------------------------------------------------------
  setUp Thread Group      Vorbereiten der Testumgebung (z.B. VM/Container starten, DB befüllen)

  tearDown Thread Group   Aufräumen der Testumgebung
  -----------------------------------------------------------------------------------------------

<!-- section 56 -->

# Sampler

![](assets/Samplers.webp)

> Durch Threadgruppen werden Benutzer-Anfragen an den Server simuliert.
> Sampler legen die Art des Requests fest!

<!-- section 57 -->

# Sampler

-   FTP Request
-   HTTP Request (can be used for SOAP or REST Webservice also)
-   JDBC Request
-   Java object request
-   JMS request
-   JUnit Test request
-   LDAP Request
-   Mail request
-   OS Process request
-   TCP request

<!-- section 58 -->

# Sampler

-   Falls man mehrere Requests des gleichen Typs versendet → Überlegen of *Defaults Configuration Element* nützlich sein könnte

-   OS Process request: Häufig nützlich in setUp/tearDown-Szenarien

-   Sollte man auch bei den Plugins keinen passen Sampler finden → Es lassen sich auch eigene Sampler schreiben. Häufig findet sich auch auf Github etwas!

<!-- section 59 -->

# Controller

> Logische Controller legen fest wann/welche Sampler verwendet werden

![](assets/LogicControllerClassification.png)

<!-- section 60 -->

# Controller

> Ziel des **Module Controllers** ist es Modularität zu jMeter hinzuzufügen, z.B. bei Webapps (Login, Suche, ...)

![](assets/ModuleControllerJMeter.png)

<!-- section 61 -->

# Controller

Beispiel: 100 Benutzer loggen sich ein, 30 Benutzer suchen auf google und 50 Benutzer loggen sich aus

![Simple Controller ist nur ein Container für Requests](assets/TestNewPlanJMeterController.png)

<!-- section 62 -->

# Controller

Der Module-Controller kontrolliert welches Modul laufen soll

![](assets/RunLoginModuleJMeter.png)

<!-- section 63 -->

# Controller

Weitere wichtige Controller:

-   **Interleave Controller:** wählt Request und führt diesen einmal in jedem Loop des Threads durch
-   **Runtime Controller:** kontrolliert wie lange seine Kinder laufenn
-   **Transaction Controller:** Stoppt Gesamtzeit des Testdurchführung, z.B. Dauer des Logins
-   **Include Controller:** Nutzung externer Testpläne

<!-- section 64 -->

# Timers

> Durch Timer läßt sich in jMeter ein Delay zwischen den Sampler definieren

-   Ohne delay könnten zu viele Requests in kurzer Zeit den Server überlasten

-   Fügt man mehr als einen Timer zur Thread-Gruppe summiert jMeter die Timer-Zeit und pausiert so lange

-   Um Pause an einer bestimmten Stelle im Test Plan zu machen → Flow Control Action Sampler

<!-- section 65 -->

# Assertions

> Über Assertions läßt sich prüfen ob sich die Applikation unter Last wie erwartet verhält

-   Beispiel: Response enthält bestimmten Text?

-   Um Assertion-Ergebnisse anzuzeigen muss man einen entsprechenden Listener zur Thread-Gruppe hinzufügen

<!-- section 66 -->

# Assertions

> Scope beachten!

![](assets/Screen%20Shot%202021-06-19%20at%209.06.28.png)

<!-- section 67 -->

# Assertions

> Performance beachten!

  Assertion              CPU/Memory
  ---------------------- ------------
  Response Assertion     moderat
  Duration Assertion     gering
  Size Assertion         gering
  XML Assertion          hoch
  Beanshell Assertion    Variable
  MD5Hex Assertion       gering
  HTML Assertion         hoch
  XPath Assertion        hoch
  XML Schema Assertion   hoch
  JSR223 Assertion       Variable
  Compare Assertion      hoch
  SMIME Assertion        moderat
  Json Assertion         hoch

**gering:** Kann ohne Probleme genutzt werden
**moderat:** Sparsam einsetzen, insbesondere bei größeren Serverantworten (100kbs bis mehrere MB)
**hoch:** größtenteils nur für funktionales Testen oder leichte Last (\<10 concurrent Usern) passend

<!-- section 68 -->

# Assertions

Beispiel: Eigene JSR223 Assertion um Durations zu prüfen

    def response_time = prev.getTime().toInteger();

    def expected_response_time = 0;

    if (response_time > expected_response_time) {
      AssertionResult.setFailure(true);
      AssertionResult.setFailureMessage("The expected response time is : " + expected_response_time + "ms but it took: " + response_time + "ms");
    }

<!-- section 69 -->

# Listener

![](assets/Listners.webp)

> Zeigen die Ergebnisse der Testdurchführung

<!-- section 70 -->

# Listener

![Arten von Listenern](assets/Jmeter-Listeners-3.png)

<!-- section 71 -->

# Listener

Sammeln Ergebnisse auf gleichem Level oder darunter

Listener können sehr Ressourcenintensiv sein!

-   Nicht bei Load-/Stress-Tests verwendet werden sollten:
    -   Assertion Results
    -   View Results in Table
    -   View Results Tree

Eregebnisse können auch in Files (csv, xml) zur weiterverarbeitung weggeschrieben werden

-   Default konfigurierbar in jmeter.properties bzw. user.properties
-   mehr Details siehe: ![](https://jmeter.apache.org/usermanual/listeners.html)

<!-- section 72 -->

# Listener

**CLI-Modus:** mit dem *-l Flag can ein Top-Level listener benutzt werden zusätzlich zu den im Testplan definierten Listenern*

`jmeter -n -t testplan.jmx -l testplan_01.jtl -j testplan_01.log`

Generieren eines HTML-Reports aus .jtl-Dateien:

`./bin/jmeter -g JTL_FILE -o OUTPUT_FOLDER`

<!-- section 73 -->

# Listener

![Beispiel HTML-Dashboard](assets/jmeter-html-report-summary.png){height="70%" width="70%"}

<!-- section 74 -->

# Listener

**Real-Time-Results:** seit jMeter 2.13 unterstützt jMeter Real-Time-Results, z.B. für Grafana. Details: → ![](https://jmeter.apache.org/usermanual/realtime-results.html)

![Grafana-Beispielboard](assets/grafana_dashboard.png){height="70%" width="70%"}

<!-- section 75 -->

# Pre- und Post-Prozessoren

Ist ein Pre-/Post-Prozessor direkt an einen Sampler angehängt wird er direkt vor/nach diesem Sampler ausgeführt

Häufigste Use-Cases:

-   Pre-Prozessor:
    -   Settings eines Requests direkt bevor er läuft verändern
    -   Variablen Updaten die nicht aus dem Response-Text extrahiert werden.
-   Post-Prozessor:
    -   Verarbeiten der Response Daten, z.B extrahieren von Daten (Regex, Json, ...)

<!-- section 76 -->

# Configuration Elements

![](assets/ConfigurationElements.webp)

<!-- section 77 -->

# Configuration Elements

> Können keine Requests senden, diese aber verändern

**Beispiel:** Setzen von Defaults und Variablen für Nutzung in Samplern

-   Zugriff nur innerhalb des Zweiges in dem das Element hinzugefügt wurde

-   Settings werden normalerweise gemerged, wobei Elemente tiefer im Baum vorrang haben.

    -   **Ausnahme:** *User Defined Variables* werden unabhängig von der Position zu Beginn des Test verarbeitet
    -   **Empfehlung:** *User Defined Variables* sollten am Start der Thread-Gruppe positioniert werden

<!-- section 78 -->

# Configuration Elements

Header Manager, Cookie Manager und Authorization Manager stellen einen weitern Sonderfall dar:

-   Setting werden nicht gemerged

-   Gibt es mehr als einen Manager im Scope wird nur einer verwendet. Es lässt sich allerdings nicht festlegen welcher!

<!-- section 79 -->

# Configuration Elements

-   **Cache-Manager:**: Falls man Last-Tests mit Cache durchführen möchte, z.B. für Web-Apps

-   **Cookie-Manager:** Falls man Anwendung mit Cookies testen möchten, z.B. Auth bei Web-Apps

-   **Header-Manager:** Kann HTTP Request-Header überschreiben, z.B. Authorization-Header für JWTs bei Web-Apps

<!-- section 80 -->

# Properties / Variablen

**Properties:**

-   sind global in jMeter

-   wird meistens für jMeter Default-Werte genutzt → Beispiel: remote\_hosts

-   [können in Testplänen referenziert werden](https://jmeter.apache.org/usermanual/functions.html#__property)

-   setProperty kann genutzt werden um eine jMeter-Property zu definieren → Da diese Global sind können hierdurch bei Bedarf Informationen zwischen den Threads ausgetauscht werden!

<!-- section 81 -->

# Properties / Variablen

**Variablen:**

-   lokal für jeden Thread

-   Wird eine Variable in einem Thread upgedated wird nur die Thread-Kopie der Variable verändert!

-   Durch den Testplan definierte Variablen und "User Defined Variables" werden zum Start innerhalb des Testplans verfügbar gemacht

-   Bei mehrfach-Definition gewinnt die letzte Definition!

-   Nützlich um Tests zu parametrisieren → Identifikation von Werten die innerhalb eines Test-Runs konstant bleiben!

<!-- section 82 -->

# Configuration Elements

Beispielparametrisierung:

  Variable   Wert
  ---------- -----------------
  HOST       www.example.com
  THREADS    10
  LOOPS      20

wird zu

  Variable   Wert
  ---------- ---------------------------------
  HOST       \${\_\_P(host,www.example.com)}
  THREADS    \${\_\_P(threads,10)}
  LOOPS      \${\_\_P(loops,20)}

Aufruf: `jmeter … -Jhost=www3.example.org -Jloops=13` (Alternativ: entsprechende user.properties setzen)

Zugriff innerhalb des Testplans auf die Werte: \${HOST}, \${THREADS}, \${LOOPS}

<!-- section 83 -->

# Testfragment

> Testfragmente sind eine spezielle Art von Controller auf Ebene des Thread Group Elements. Man unterscheidet zwischen *Test Fragment Nodes* und *test Fragment Files*. *Test Fragment Nodes* lassen sich nicht in *Test Fragment\_Files* inkludieren!

-   wird nicht ausgeführt solange es nicht in einem Modul-Controller oder Include-Controller refereniert wird.

    -   → Ermöglicht gleichzeitges Arbeiten an modulen in separaten Files

-   Dient der Code-Wiederverwendung innerhalb von Testplänen und hilft sehr große Testpläne wartbar zu machen

-   Details: → ![](https://www.blazemeter.com/blog/how-manage-large-jmeter-scripts-jmeter-test-fragments)

<!-- section 84 -->

# Testfragment

> Hilft unterschiedliche Workflows zu unterstützen

  Funktionalitäten einer Beispielapp
  ----------------------------------------------
  Login
  Logout
  User Registration
  Search for Product
  Select Product
  Order Product with different payment methods
  Edit Order
  Cancel Order
  Search for User Profile

-   Workflow 1: User Registration -\> Search for Product -\> Select Product -\> Order Product -\> Logout
-   Workflow 2: Login -\> Search for Product -\> Select Product -\> Order Product -\> Logout
-   Workflow 3: Login -\> Search for User -\> Cancel Order -\> Logout
-   Workflow 4: Login -\> Search for Product

![Workflow 4](assets/include-controller.png)

<!-- section 85 -->

# Templates

> Skeleton Script die wiederverwendbar sind um mit einem Projekt zu starten

Erzeugung eines Templates:

-   .jmx-File in /templates abspeichern

-   Template.xml öffnen und Daten für eigenes Template ergänzen

-   Nach jMeter-Neustart kann Template ausgewählt werden

-   Es existier etliche Templates auf Github, z.B. zum Testen von Wordpress-Apps → ![](https://github.com/jmeter-templates/wordpress)

> Tipp: Aufbau der Beispiel-Templates studieren!

<!-- section 86 -->

# Ausführungsreihenfolge

-   Configuration Elements
-   Pre-Processors
-   Timers
-   Sampler
-   Post-Processors
-   Assertions
-   Listeners

<!-- section 87 -->

# Ausführungsreihenfolge

-   Timers, Assertions, Pre-/Post-Processors werden nur ausgeführt, wenn es einen Sampler gibt auf den sie sich beziehen können!
-   Logic-Controller und Sampler werden in der Reihenfolge in der sie im Baum stehen ausgeführt
-   Andere Testelemente werden entsprechend ihres Scopes ausgeführt

Beispiel-Testplan:

-   Controller
    -   Post-Processor 1
    -   Sampler 1
    -   Sampler 2
    -   Timer 1
    -   Assertion 1
    -   Pre-Processor 1
    -   Timer 2
    -   Post-Processor 2

Ausführungsreihenfolge:

Pre-Processor 1
Timer 1
Timer 2
Sampler 1
Post-Processor 1
Post-Processor 2
Assertion 1

Pre-Processor 1
Timer 1
Timer 2
Sampler 2
Post-Processor 1
Post-Processor 2
Assertion 1

<!-- section 88 -->

# Scripting {#scripting .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 89 -->

# BeanShell

-   Eine der fortgeschrittensten Komponenten in JMeter

-   Hilfreich für sehr ungewöhnliche Testfälle die ansonsten schwer in jMeter umzusetzen wären

-   Hat Zugriff auf interne JMeter-APIs und jede externe Klasse die in den jMeter Classpath geladen wird

    -   jars nach /lib/ext kopieren
    -   jars müssen am Anfang des BeanShell-Script importiert werden

<!-- section 90 -->

# BeanShell

Beispiel Use-Cases:

-   jMeter-Variablen verändern: \`var.put("counter", "false");

-   jMeter-Variable in Property umwandeln \`props.put("some\_variable", var.get("some\_variable"));

-   Cookies zwischen Thread-Groups übergeben: siehe <https://www.blazemeter.com/blog/how-use-beanshell-jmeters-favorite-built-component>

-   Testfall im Fehlerfall stoppen

-   komplexe Assertions

<!-- section 91 -->

# BeanShell

Vordefinierte Variablen:

-   SampleResult: Alle Felder/Methode von <https://jmeter.apache.org/api/org/apache/jmeter/samplers/SampleResult.html> stehen zu verfügung
-   ResponseCode: Setzt den Sampler response code z.B.: ResponseCode = "200";
-   ResponseMessage
-   IsSuccess: Falls *true* wird der Sampler als *passed* betrachtet
-   Label: String der in the Test Ergebnisse aufgelistet wird
-   FileName
-   ctx: die mächtigste Variable gibt Zugriff auf org.apache.jmeter.threads.JMeterContext und gibt Zugriff auf die JMeter engine, Samplers und ihren Ergebnissen
-   vars: gibt Zugriff auf jMeter Variablen
-   props: gibt Zugriff auf jMeter Properties
-   log: ermöglicht in das jmeter.log-File zu schreiben, z.B. log.info("Test Info Message");

<!-- section 92 -->

# BeanShell

Ist die BeanShell Tot? → <https://www.blazemeter.com/blog/is-beanshell-dead>

-   langsamer und mehr Speicherverbrauch als JSR223+Groovy

-   Seit JMeter 3.1 ist Groovy die Default Scripting-Sprache für JSR223 Sampler

-   JMeter Contributor Philippe Mouawad: "avoid Beanshell in favor of JSR223 + Groovy because Beanshell is old, slow..."

![](assets/beanshellgroovy3.png)

<!-- section 93 -->

# JSR223

-   zwar etwas langsamer als der *Java Request Sampler*, allerdings entfällt: recompile → zum Classpath hinzufügen → jMeter Neustart

<!-- section 94 -->

# RegEx-Extractor

![](assets/regex-extractor.png)

<!-- section 95 -->

# Arbeiten mit JARs

Use-Cases für Jars:

-   Wir haben 20 Tests mit dem selben Code-Stück. Bei Änderungen müssten sonst alle 20 Tests angepasst werden.

    -   → besser den Code als jar bereitstellen (jmeter/lib) und dann im JSR223-Sampler verwenden

-   Benutzung externe Bibliotheken (z.B. Apache POI)

<!-- section 96 -->

# Reporting {#reporting .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 97 -->

# Reporting

https://github.com/ludeknovy/jtl-reporter

https://github.com/anasoid/jmeter-logstash

<!-- section 98 -->

# Arten von Reporting

<!-- section 99 -->

# Ergebnis-Analyse

<!-- section 100 -->

# Testdatenverwaltung {#testdatenverwaltung .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 101 -->

# Testdaten in .json-Datei / .csv-Datei

-   Testdaten werden aus .csv gelesen → Tipp: mit dem Random CSV Data Set plugin können die Daten in zufälliger Reihenfolge gelesen werden

-   Alternativ können auch ander Formate implementiert werden, z.B. Excel: <https://www.blazemeter.com/blog/how-to-implement-data-driven-testing-in-your-jmeter-test>

<!-- section 102 -->

# jMeter-Funktionen zur Datengenerierung

<!-- section 103 -->

# REST-APIs {#rest-apis .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 104 -->

# Nutzung des Test-Rekorders

-   Test Plan → Add → Non-Test Elements → HTTP(S) Test Script Recorder
-   Einstellungen → Port festlegen
-   Thread Group → Add → Logic Controllers → Recording Controller (Alternativ: später manuell vom Skript-Rekorder kopieren)
-   Im Browser Proxy auf gleichen Port wie Skript-Rekorder stellen
-   jMeter-Zertifikat (jMeter/bin/ApacheJMeterTemporaryRootCA.crt) im Browser importieren
    -   in Firefox: options → search for 'certificate' → view certificates
    -   Haken bei "Trust Website" setzen
-   Test aufzeichnen

<!-- section 105 -->

# Testen mit "Http-Request"

<!-- section 106 -->

# Umgang mit Sessions/Authentification

-   JWT-Token erhalten
    -   Bei Cookies: in **jmeter.properties** folgendes setzen: **CookieManager.save.cookies=true** → macht Cookies als Variablen verfügbar
    -   Bei Localstorage: jMeter-Integration mit Selenium nutzen
    -   JWT mittels Regex aus Login-Response extrahieren
-   setzen des Authorization-Headers mittels **HTTP Header Manager**: z.B. auf \${COOKIE*Authorization} falls die Cookie-Variable \_Authorization* heißt

![HTTP Header Manager-Beispiel](cookie-session.png)

<!-- section 107 -->

# Umgang mit dynamischen Daten

Beispiel: Benutzer wird angelegt → Benutzerprofil aufrufen

Die URL des Benutzerprofils könnte die Benutzer-ID in der URL enthalten, welch erst nach dem anlegen des Benutzer bekannt ist

Lösung:

-   Benutzer anlegen
-   Benutzer-ID aus Response in eine Variable extrahieren (z.B. mittels Regular Expression Extractor)
-   Verwenden der Variable (z.B. \${benutzerId}) im HTTP-Request zum Aufruf des Benutzerprofils

<!-- section 108 -->

# Verteiltes Testen mit jMeter {#verteiltes-testen-mit-jmeter .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 109 -->

# Master-Slave-Setup

![](distributed_jmeter.webp)

<!-- section 110 -->

# Master-Slave-Setup

-   setup multiple computers/vms/containers
-   auf jedem slave: run jmeter-server: **bin/jmeter-server.bat**
-   auf dem master:
    -   edit **bin/jmeter.properties**: füge alle IPs der slave-systeme komma-separiert unter remote\_hosts hinzu (master/slaves müssen im selben Subnetz sein!)
-   run test
    -   via GUI
    -   non-GUI
        -   `jmeter -n -t script.jmx -r`
        -   `jmeter -n -t script.jmx -R server1,server2,...`

<!-- section 111 -->

# Master-Slave-Setup

-   Jedes Slave-System führt die im Master definierten Dinge aus
    -   wollen wir für 10000 Nutzer testen und haben 10 Slaves → Im Testplan muss für 1000Nutzer geplant werden, damit wir am Ende auf ingesamt 10000 kommen!
-   Über den if-Controller lassen sich auf den einzelnen Slaves unterschiedliche Dinge ausführen

<!-- section 112 -->

# Testausführung über CLI

<!-- section 113 -->

# Large-Scale

Zu beachten bei verteilten Large-Scale-Lösungen: ![](https://octoperf.com/blog/2017/10/12/optimize-jmeter-for-large-scale-tests/)

-   von Kommandozeile starten → UI verbraucht viel Memory

-   Vermeide UI listener (z.B. Grahpen, Tabellen) → in ein JTL-File schreiben (z.B. mittels Simple data writer)

-   Genug Heap-Space bereitstellen, z.B. JVM\_ARGS="-Xms1g -Xmx8g" jmeter.sh

-   Vermeide mehr als 1000 Benutzer/Maschine zu simulieren

-   lieber mehr Durschnittshardware (z.B. 4core, 16GB) als einige wenige Superrechner (z.B. 16core, 128GB)

-   Vermeide Beanshell-Skripte

-   Distributed Mode funktioniert gut mit 20-30 (mit Glück 40-50) Maschinen, da die RMI-Kommunikation von jMeter nicht sehr effizient ist

    -   Darüber hinaus lieber jede JMeter-Instanz einzeln starten
    -   das JMX vor dem Test-Start hinsenden
    -   nach dem Test das JTL-File holen

-   Verwende .csv-JTLs anstelle von XML

<!-- section 114 -->

# RMI {#rmi .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 115 -->

# RMI

<!-- section 116 -->

# Diskussion: aktueller verwendeter RMI-Sampler

<!-- section 117 -->

# Vergleich mit existierende RMI-Samplern auf Github

<!-- section 118 -->

# Monitoring {#monitoring .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 119 -->

# Prometheus / Grafana

<!-- section 120 -->

# YourKit-Profiler

<!-- section 121 -->

# Containerisierung {#containerisierung .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 122 -->

# IaC: Infrastructure as a Code

> Mit IaC (Infrastructure as Code) wird die Infrastruktur durch Code -- und nicht durch manuelle Prozesse -- verwaltet und provisioniert.

> Mit IaC werden Konfigurationsdateien erstellt, die Ihre gesamten Infrastrukturspezifikationen enthalten, wodurch Sie Konfigurationen einfacher bearbeiten und verteilen können.
> Es stellt außerdem sicher, dass Sie jedes Mal dieselbe Umgebung provisionieren.

> Ein wichtiger Bestandteil von IaC ist die Versionskontrolle. Wie jede andere Software-Quellcodedatei sollten auch Ihre Konfigurationsdateien der Quellkontrolle unterliegen.

<!-- section 123 -->

# Vagrant + Ansible

Ansible Playbook: <https://galaxy.ansible.com/lean_delivery/jmeter>

<!-- section 124 -->

# Docker / Docker-Compose

<!-- section 125 -->

# Kubernetes

<!-- section 126 -->

# CI/CD-Pipeline {#cicd-pipeline .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 127 -->

# Github Actions

https://github.com/marketplace/actions/setup-jmeter
https://github.com/marketplace/actions/apache-jmeter
https://github.com/marketplace/actions/perfaction-for-jmeter
https://www.redline13.com/blog/2021/10/github-actions-for-jmeter/
https://dev.to/sebiboga/generate-jmeter-test-report-and-save-it-as-artifact-with-github-actions-4a6b
https://stackoverflow.com/questions/68084554/fail-github-actions-pipeline-if-dockerized-jmeter-tests-failed

<!-- section 128 -->

# jMeter in einer Github-Actions Pipeline

<!-- section 129 -->

# JMeter in einer Jenkins-Pipeline

<!-- section 130 -->

# Klärung offener Punkt {#klärung-offener-punkt .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}
