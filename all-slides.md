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

**Installation:**

Lade https://jmeter-plugins.org/get/ herunter und kopiere in das jMeter-Verzeichnis `lib/ext`

![[Plugin Manager](https://jmeter-plugins.org/wiki/PluginsManager/)](assets/pmgr_menu_item.png)

<!-- section 4 -->

# jMeter Plugin-Manager

**Ausführung über die Kommandozeile:**

https://jmeter-plugins.org/wiki/PluginsManagerAutomated/

`PluginsManagerCMD <command> [<params>]` z.B. `PluginsManagerCMD install jpgc-fifo,jpgc-json=2.2`

**Falls man hinter einem Proxy ist:**

`JVM_ARGS="-Dhttps.proxyHost=myproxy.com -Dhttps.proxyPort=8080 -Dhttp.proxyUser=john -Dhttp.proxyPass=***" PluginsManagerCMD status`

<!-- section 5 -->

# jMeter Plugin-Manager

**Eigenes Plugin schreiben:**

https://jmeter.apache.org/usermanual/jmeter\_tutorial.html

**Eigenes Repository hinzufügen:**

**jMeter-Property setzen:**

`jpgc.repo.address=https://jmeter-plugins.org/repo/;http://my.intranet.site/plugins-repo.json`

Das Repository-JSON muss folgendes Format erfüllen: https://jmeter-plugins.org/wiki/PluginRepositoryDescriptorFormat/

<!-- section 6 -->

# jMeter Plugin-Manager

**Nützliche Plugins:**

-   Custom Thread Groups
-   jpgc-perfmon
-   jpgc-dummy
-   jpgc-plancheck
-   JMXMon

<!-- section 7 -->

# Strukturierung von Testplänen {#strukturierung-von-testplänen .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 8 -->

# Workload Design {#workload-design .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 9 -->

# Scripting {#scripting .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 10 -->

# Reporting {#reporting .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 11 -->

# Testdatenverwaltung {#testdatenverwaltung .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 12 -->

# REST-APIs {#rest-apis .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 13 -->

# Verteiltes Testen mit jMeter {#verteiltes-testen-mit-jmeter .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 14 -->

# RMI {#rmi .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 15 -->

# Monitoring {#monitoring .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 16 -->

# Containerisierung {#containerisierung .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 17 -->

# CI/CD-Pipeline {#cicd-pipeline .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}

<!-- section 18 -->

# Klärung offener Punkt {#klärung-offener-punkt .light-on-dark bgcss="sea-gradient" x="0" y="0" rz="-.1"}
