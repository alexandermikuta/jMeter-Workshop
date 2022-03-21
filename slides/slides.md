---
title: jMeter-Workshop
variant: reveal
highlight_style: github-gist
themes: mytheme
width: 1280
asciinema: false
---

# jMeter Workshop {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

![performance testing with jMeter](assets/jmeter.jpg){ height=20% width=20% }

# jMeter Workshop

Agenda:

| Tag 1                         | Tag 2                        |
| ----------------------------- | ---------------------------- |
| jMeter Plugin-Manager         | Verteiltes Testen mit jMeter |
| Strukturierung von Testplänen | RMI                          |
| Workload Design               | Monitoring                   |
| Scripting                     | Containerisierung            |
| Reporting                     | CI/CD-Pipeline               |
| Testdatenverwaltung           | Klärung offener Punkte       |
| REST-APIs                     |                              |

# jMeter Plugin-Manager {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# jMeter Plugin-Manager

[https://jmeter-plugins.org/wiki/PluginsManager/](https://jmeter-plugins.org/wiki/PluginsManager/)

![](assets/pmgr_menu_item.png)

**Installation:**

- lade **[https://jmeter-plugins.org/get/](https://jmeter-plugins.org/get/)** herunter
- kopiere **jar** in das jMeter-Verzeichnis **lib/ext**

# jMeter Plugin-Manager

**Ausführung über die Kommandozeile:**

[https://jmeter-plugins.org/wiki/PluginsManagerAutomated/](https://jmeter-plugins.org/wiki/PluginsManagerAutomated/)

`PluginsManagerCMD <command> [<params>]`

z.B.

`PluginsManagerCMD install jpgc-fifo,jpgc-json=2.2`

# jMeter Plugin-Manager

**Falls man hinter einem Proxy ist:**

`JVM_ARGS="-Dhttps.proxyHost=myproxy.com -Dhttps.proxyPort=8080 -Dhttp.proxyUser=john -Dhttp.proxyPass=***" PluginsManagerCMD status`

# jMeter Plugin-Manager

**Eigenes Plugin schreiben:**

[https://jmeter.apache.org/usermanual/jmeter_tutorial.html](https://jmeter.apache.org/usermanual/jmeter_tutorial.html)

**Eigenes Repository hinzufügen:**

jMeter-Property setzen:

`jpgc.repo.address=https://jmeter-plugins.org/repo/;http://my.intranet.site/plugins-repo.json`

Das Repository-JSON muss folgendes Format erfüllen: [https://jmeter-plugins.org/wiki/PluginRepositoryDescriptorFormat/](https://jmeter-plugins.org/wiki/PluginRepositoryDescriptorFormat/)

# jMeter Plugin-Manager

**Nützliche Plugins:**

- Ultimate Thread Group
- Concurrency Thread Group
- JMXMon Sample Collector
- jp@gc - PerfMon
- jp@gc - Dummy Sampler
- jp@gc - PlanCheck

# jMeter Plugin-Manager

**Ultimate Thread Group**

![[https://jmeter-plugins.org/wiki/UltimateThreadGroup/](https://jmeter-plugins.org/wiki/UltimateThreadGroup/)](assets/ultimate_thread_group1.png){ height=40% width=40% }

# jMeter Plugin-Manager

**Concurrency Thread Group**

![[https://jmeter-plugins.org/wiki/ConcurrencyThreadGroup/](https://jmeter-plugins.org/wiki/ConcurrencyThreadGroup/)](assets/ConcurrencyThreadGroup.png){ height=40% width=40% }

# jMeter Plugin-Manager

**jp@gc - PerfMon**

![[https://jmeter-plugins.org/wiki/PerfMon/](https://jmeter-plugins.org/wiki/PerfMon/)](assets/servers_performance_monitoring.png){ height=40% width=40% }

# jMeter Plugin-Manager

**jp@gc - Dummy Sampler**

![[https://jmeter-plugins.org/wiki/DummySampler/](https://jmeter-plugins.org/wiki/DummySampler/)](assets/dummy_sampler.png){ height=40% width=40% }

# jMeter Plugin-Manager

**jp@gc - PlanCheck**

[https://jmeter-plugins.org/wiki/TestPlanCheckTool/](https://jmeter-plugins.org/wiki/TestPlanCheckTool/)

Usage:

`jmeter/lib/ext/TestPlanCheck.sh --jmx MyTestPlan.jmx --stats --tree-dump`

# jMeter Plugin-Manager

**JMXMon Sample Collector**

![[https://jmeter-plugins.org/wiki/JMXMon/](https://jmeter-plugins.org/wiki/JMXMon/)](assets/jmxmon_samples_collector.png){ height=40% width=40% }

# Strukturierung von Testplänen {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Thread Groups, Sampler und Controller

# Timers

# Assertions und Listener

# Pre- und Post-Prozessoren

# Config-Elemente, Cookie-Manager, Header-Manager

# User-definierte Variable

# Workload Design {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Zeitliche Verteilung der Last

# Erkennen der Last-Grenzen / Server-Bedarfs

# Scripting {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# BeanShell

# JSR223

# RegEx-Extractor

# Arbeiten mit JARs

# Reporting {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Arten von Reporting

# Ergebnis-Analyse

# Testdatenverwaltung {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Testdaten in .json-Datei / .csv-Datei

# jMeter-Funktionen zur Datengenerierung

# REST-APIs {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Nutzung des Test-Rekorders

# Testen mit "Http-Request"

# Umgang mit Sessions/Authentification

# Umgang mit dynamischen Daten

# Verteiltes Testen mit jMeter {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Master-Slave-Setup

# Testausführung über CLI

# RMI {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Diskussion: aktueller verwendeter RMI-Sampler

# Vergleich mit existierende RMI-Samplern auf Github

# Monitoring {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Prometheus / Grafana

# YourKit-Profiler

# Containerisierung {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# IaC: Infrastructure as a Code

> Mit IaC (Infrastructure as Code) wird die Infrastruktur durch Code – und nicht durch manuelle Prozesse – verwaltet und provisioniert.

> Mit IaC werden Konfigurationsdateien erstellt, die Ihre gesamten Infrastrukturspezifikationen enthalten, wodurch Sie Konfigurationen einfacher bearbeiten und verteilen können.
> Es stellt außerdem sicher, dass Sie jedes Mal dieselbe Umgebung provisionieren.

> Ein wichtiger Bestandteil von IaC ist die Versionskontrolle. Wie jede andere Software-Quellcodedatei sollten auch Ihre Konfigurationsdateien der Quellkontrolle unterliegen.

# Vagrant

# Docker / Docker-Compose

# Kubernetes

# CI/CD-Pipeline {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}

# Github Actions

https://github.com/marketplace/actions/setup-jmeter
https://github.com/marketplace/actions/apache-jmeter
https://github.com/marketplace/actions/perfaction-for-jmeter
https://www.redline13.com/blog/2021/10/github-actions-for-jmeter/
https://dev.to/sebiboga/generate-jmeter-test-report-and-save-it-as-artifact-with-github-actions-4a6b
https://stackoverflow.com/questions/68084554/fail-github-actions-pipeline-if-dockerized-jmeter-tests-failed

# jMeter in einer Github-Actions Pipeline

# JMeter in einer Jenkins-Pipeline

# Klärung offener Punkt {bgcss=sea-gradient x=0 y=0 rz=-.1 .light-on-dark}
