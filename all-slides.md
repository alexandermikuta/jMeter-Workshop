<!-- section 0 -->

# jMeter Workshop {#jmeter-workshop .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

![performance testing with jMeter](assets/jmeter.jpg){height="20%" width="20%"}

<!-- section 1 -->

# jMeter Workshop

Agenda:

  Tag 1                           Tag 2
  ------------------------------- ------------------------------
  jMeter Plugin-Manager           Verteiltes Testen mit jMeter
  Strukturierung von Testplänen   RMI
  Workload Design                 Monitoring
  Scripting                       Containerisierung
  Reporting                       CI/CD-Pipeline
  Testdatenverwaltung             Klärung offener Punkte
  REST-APIs                       

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

# Strukturierung von Testplänen {#strukturierung-von-testplänen .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 15 -->

# Thread Groups, Sampler und Controller

<!-- section 16 -->

# Timers

<!-- section 17 -->

# Assertions und Listener

<!-- section 18 -->

# Pre- und Post-Prozessoren

<!-- section 19 -->

# Config-Elemente, Cookie-Manager, Header-Manager

<!-- section 20 -->

# User-definierte Variable

<!-- section 21 -->

# Workload Design {#workload-design .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 22 -->

# Worload

> The amount of work a system has to perform in a given time. In the performance field, a workload usually refers to combined load placed on an application by the set of clients it services

<!-- section 23 -->

# Prinicples

-   Vorhersagbarkeit

-   Wiederholbarkeit

-   Skalierbarkeit

<!-- section 24 -->

# Vorhersagbarkeit

> Das Verhalten des Systems (z.B. Prozessanfragen, Datenzugriffe, ...) sollte während die Workload läuft vorhersehbar sein.

![](assets/predictable.png)

<!-- section 25 -->

# Wiederholbarkeit

> Wenn eine Workload mehrere male auf identische Weise ausgeführt wird, sollte die Ergebnis nahezu identisch ausführen. Ansonsten wird eine Performance-Analyse sehr schwer.

<!-- section 26 -->

# Skalierbarkeit

> Eine Workload solle mit unterschiedlichen Lasten ausgeführt werden können um die Skalierbarkeit der Anwendung testen zu können.

<!-- section 27 -->

# Workload Design Steps

-   Design der Applikation
-   Key-Szenarios identifizieren
-   Definieren der Metriken
-   Design der Load
-   Definieren der Skalierungsregeln
-   Design des Load-Generators

<!-- section 28 -->

# Design der Applikation

-   Definieren der Aktoren und Use-Cases → Hilft die Operationen der Workload zu definieren

-   Definieren der Operationen

    -   Im einfachsten Fall mappt jeder User-Case auf eine Operation
    -   Für sinnvolle Workloads solle die Zahl der benötigen Operation klein gehalten werden (6-8) → Ansonsten schwer zu managen und verstehen

<!-- section 29 -->

# Key-Szenarios identifizieren

-   Messbares Szenario: Ein User-Szenario das Performance-getestet werden soll, sollte vollständig messbar sein
-   Meistbenutzte Szenarios
-   Business-kritische Szenarios
-   Ressourcen-intensive Szenarios
-   Zeitabhängig häufig genutzte Szenarios: z.B. Weihnachts-Liste auf Amazon
-   Stakeholder-relevante Szenarien

Beispiel für eine E-Commerce-Applikation:

-   Browsen des Produktkatalogs
-   Benutzeraccount anlegen
-   Nach einem Produkt suchen
-   Login
-   Bestellung abschicken

<!-- section 30 -->

# Definieren der Metriken

Typische Metriken sind:

-   **Durchsatz:** Wie viele Operation können vom SUT während einer gewissen Zeit verarbeitet werden

-   **Anwortzeiten:** Zeit zwischen Ende der Anfrage und Beginn der Anwort an das SUT → Macht normalerweise nur Sinn wenn es auch Anforderungen für Antwortzeiten gibt

-   **Ressourcenverbrauch:** z.B. alle Ressourcen (IO, Memory, ...) sollten nicht mehr als 70% der max. Auslastung haben

-   **Anzahl maximaler Benutzer:** Wie viele Benutzer können gleichzeitig auf dem SUT arbeiten ohne das es zu Probleme kommt

<!-- section 31 -->

# Design der Load

-   der wichtigste Schritt im Workload Design!

-   die Relevanz der Workload hängt davon ab wie genau sie die die reale Produktionslast emuliert

-   gleichzeit wichtig: die Test-Workload solle sich auf die signifikanten Aspekte der Live-Load konzentrieren → Ansonsten wird es zu kompliziert

<!-- section 32 -->

# Design der Load

-   **Arrival Rates:** Die Rate mit der Requests an das SUT gestellt werden

-   **Think Times:** Zeit zwischen Anzeige der Daten beim Benutzer und seiner nächsten Interaktion → Bei großen Datenmenge steigt diese Zeit

-   **Operation Mix:** Festlegung in welcher Frequenz welche Operation durchgeführt wird → oft prozentual je Operation was sich zu 100% summiert

    -   Flat Mix:
        -   Einfachste Möglichkeit
        -   wird verwendet wenn Operation unabhängig sind und die gleiche Wahrscheinlichkeit haben
        -   → Der Mix wählt eine Operation zufällig
    -   Flat Sequence Mix:
        -   Spezifiziert ein Set von Operations-Sequenzen
        -   z.B. Set1=Op1,Op2 und Set2=Op1,Op3
        -   jedem Set wird eine Wahrscheinlichkeit zugeordnet und dementsprechen ausgewählt
    -   Matrix Mix (Transition Mix):
        -   Beschreibt die Überangswahrscheinlichkeiten in einem Markov-Modell
        -   wird häufig bei Web-Apps verwendet

Beispiel-Workload als Matrix-Mix:

  From     To Page 1   To Page 2   To Page 2
  -------- ----------- ----------- -----------
  Page 1   0,00 %      80,00%      20,00%
  Page 2   20,00%      39,00%      41,00%
  Page 3   60,00%      19,00%      21,00%

-   **Operation Data:**

    -   Abhängig von der Operation müssen für den Request diverse Input-Daten generiert werden

    -   Um ein realistisches Szenario zu erhalten sollten die Daten variiert werden → Bei 100 Items sollten nicht immer fix 5 selektiert werden

    -   Best-Practice: Eine klein Zahl an Fehlern durch invalide Daten einfügen um auch Probleme im Error-Handling aufzudecken

    -   Genieren "echter" Daten kann bei großen Daten problematisch werden → Workload Entwickler müsste all Möglichen Values kennen

        -   Uniform Random: Generierung von gleichverteilten Zufallsdaten
        -   Non-Uniform Random: in normalfall sind Datenzugriffe nicht gleichverteilt! → Datengenerierung sollte Wahrscheinlichkeit berücksichtigen

<!-- section 33 -->

# Definieren der Skalierungsregeln

Häufig wird skaliert indem man die Anzahl der emulierten Benutzer erhöht

Oft werden aber weitreichendere Lösungen benötigt

-   Linear Scaling
    -   alles wird über einen einzigen Skalierungsfaktor skaliert
    -   z.B. Workload führt Datenzugriffe eines Benutzers aus → Anzahl Benutzer & Anzahl Datenzugriffe werden beide skaliert
    -   Häufig nützlich für "Sizing"-Zwecke
-   Non-linear Scaling:
    -   Anwendungen skalieren oft nicht linear
    -   z.B. Anwendung erlaubt Tagging durch Benutzer → mit steigender Anzahl steigt auch die Last je User mit an, z.B. bei der Anzeige der Tags

<!-- section 34 -->

# Design des Load-Generators

-   Implementiert die Workload

Dabei sollte beachtet werden:

-   Zum simulieren mehrerer Benutzer-Connections sollte **kein** connection-pooling verwendet werden

-   Jeder simulierte Nutzer sollte nach Möglichkeit seinen eigenen "Random number generator" (seeded mit unique value) verwenden um wirklich zufällige Daten zu bekommen

<!-- section 35 -->

# Workload Design

-   Baseline Test
-   Identifikation der Test Szenarien
-   Preprocessors und Timer ()
-   Konfigurationen und Vorbedingungen
-   Testergebnisse, Fehler und Logs
-   Assertions und Post-Processors
-   Adding load to mimic users action

<!-- section 36 -->

# Baseline Test

> "A Baseline is the process of capturing performance metric data for the sole purpose of evaluating the efficacy of successive changes to the system or application. It is important that all characteristics and configurations, except those specifically being varied for comparison, remain the same in order to make effective comparisons as to which change (or series of changes) is driving results toward the targeted goal. Armed with such baseline results, subsequent changes can be made to the system configuration or application and testing results can be compared to see whether such changes were relevant or not." Some considerations when generating baselines include the following:\"

https://www.oreilly.com/library/view/performance-testing-with/9781787285774/8c67a2ab-7bda-4a64-bb90-6c0b8785ad60.xhtml

<!-- section 37 -->

# Identifikation der Test Szenarien

<!-- section 38 -->

# Zeitliche Verteilung der Last

<!-- section 39 -->

# Erkennen der Last-Grenzen / Server-Bedarfs

<!-- section 40 -->

# Scripting {#scripting .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 41 -->

# BeanShell

<!-- section 42 -->

# JSR223

<!-- section 43 -->

# RegEx-Extractor

<!-- section 44 -->

# Arbeiten mit JARs

<!-- section 45 -->

# Reporting {#reporting .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 46 -->

# Arten von Reporting

<!-- section 47 -->

# Ergebnis-Analyse

<!-- section 48 -->

# Testdatenverwaltung {#testdatenverwaltung .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 49 -->

# Testdaten in .json-Datei / .csv-Datei

<!-- section 50 -->

# jMeter-Funktionen zur Datengenerierung

<!-- section 51 -->

# REST-APIs {#rest-apis .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 52 -->

# Nutzung des Test-Rekorders

<!-- section 53 -->

# Testen mit "Http-Request"

<!-- section 54 -->

# Umgang mit Sessions/Authentification

<!-- section 55 -->

# Umgang mit dynamischen Daten

<!-- section 56 -->

# Verteiltes Testen mit jMeter {#verteiltes-testen-mit-jmeter .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 57 -->

# Master-Slave-Setup

<!-- section 58 -->

# Testausführung über CLI

<!-- section 59 -->

# RMI {#rmi .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 60 -->

# Diskussion: aktueller verwendeter RMI-Sampler

<!-- section 61 -->

# Vergleich mit existierende RMI-Samplern auf Github

<!-- section 62 -->

# Monitoring {#monitoring .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 63 -->

# Prometheus / Grafana

<!-- section 64 -->

# YourKit-Profiler

<!-- section 65 -->

# Containerisierung {#containerisierung .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 66 -->

# IaC: Infrastructure as a Code

> Mit IaC (Infrastructure as Code) wird die Infrastruktur durch Code -- und nicht durch manuelle Prozesse -- verwaltet und provisioniert.

> Mit IaC werden Konfigurationsdateien erstellt, die Ihre gesamten Infrastrukturspezifikationen enthalten, wodurch Sie Konfigurationen einfacher bearbeiten und verteilen können.
> Es stellt außerdem sicher, dass Sie jedes Mal dieselbe Umgebung provisionieren.

> Ein wichtiger Bestandteil von IaC ist die Versionskontrolle. Wie jede andere Software-Quellcodedatei sollten auch Ihre Konfigurationsdateien der Quellkontrolle unterliegen.

<!-- section 67 -->

# Vagrant + Ansible

Ansible Playbook: <https://galaxy.ansible.com/lean_delivery/jmeter>

<!-- section 68 -->

# Docker / Docker-Compose

<!-- section 69 -->

# Kubernetes

<!-- section 70 -->

# CI/CD-Pipeline {#cicd-pipeline .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 71 -->

# Github Actions

https://github.com/marketplace/actions/setup-jmeter
https://github.com/marketplace/actions/apache-jmeter
https://github.com/marketplace/actions/perfaction-for-jmeter
https://www.redline13.com/blog/2021/10/github-actions-for-jmeter/
https://dev.to/sebiboga/generate-jmeter-test-report-and-save-it-as-artifact-with-github-actions-4a6b
https://stackoverflow.com/questions/68084554/fail-github-actions-pipeline-if-dockerized-jmeter-tests-failed

<!-- section 72 -->

# jMeter in einer Github-Actions Pipeline

<!-- section 73 -->

# JMeter in einer Jenkins-Pipeline

<!-- section 74 -->

# Klärung offener Punkt {#klärung-offener-punkt .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}
