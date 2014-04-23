Nutzungsszenarien
=================

Die nachfolgenden Nutzungsszenarien dienen dazu, die Architektur und die
Anwendungsmöglichkeiten anhand konkreter Beispiele zu verdeutlichen. Sie
erheben keinen Anspruch auf Vollständigkeit.

## Szenario 1: Mobile Client-Anwendung {#szenario_mobile_client}

Eine [Client](#client)-Anwendung für mobile Endgeräte wie SmartPhones und Tablets,
nachfolgend "App" genannt, könnte das Ziel verfolgen, Nutzern unterwegs
sowie abseits vom Desktop-PC bestmöglichen Lesezugriff auf Dokumente aus
Ratsinformationssystemen (RIS) zu bieten. Die möglichen Kontexte und
Nutzungsmotivationen sind vielfältig:

* Teilnehmer einer Sitzung greifen während der Sitzung auf die Einladung
  dieser Sitzung und die zur Tagesordnung der Sitzung gehörenden
  Drucksachen zu, außerdem auf die Protokolle vorheriger Sitzungen.

* Eine Redakteurin der Lokalpresse geht unterwegs die Themen der nächsten
  Sitzungen bestimmter Gremien, für die sie sich besonders interessiert,
  durch.

* Eine Gruppe von Studierenden erkundet zusammen mit ihrem Dozenten die
  lokalpolitischen Aktivitäten des Viertels rund um ihre Hochschule. Dazu
  nutzen sie die GPS-Lokalisierung ihrer Smartphones in Verbindung mit den
  Geodaten, die an vielen Drucksachen des lokalen RIS zu finden sind. Direkt
  vor Ort an einer Baustelle öffnen sie Beschlüsse, Pläne und Eingaben aus
  dem Planfeststellungsverfahren, die dieser Baustelle voran gegangen sind.

Zur Realisierung derartiger Szenarien können die Fähigkeiten von OParl-kompatiblen
Servern mit den besonderen Eigenschaften der mobilen Endgeräte verknüpft werden.

Smartphones und Tablets verfügen beispielsweise, je nach Aufenthaltsort, über
sehr unterschiedlich gute Internetanbindung. In einem Büro oder zuhause können
Nutzer über ein WLAN Daten mit hoher Bandbreite austauschen, in Mobilfunknetzen
vor allem außerhalb der Ballungsgebiete jedoch sinken die Bandbreiten deutlich.
Einige Tablets werden sogar ohne Möglichkeit zur Mobilfunk-Datenübertragung
genutzt. In solchen Fällen kann ein [Cache](#cache) auf dem Endgerät dazu
dienen, Inhalte vorzuhalten, die dann auch bei langsamer oder fehlender
Internetverbindung zur Verfügung stehen. Sobald dann wieder eine Verbindung
mit hoher Bandbreite bereit steht, kann die App im Hintergrund, entweder über die 
[Feeds](#feeds) der OParl API oder über den einzelnen Abruf von Objekten, die 
gecachten Inhalte aktualisieren.

Eine Stärke eines mobilen Clients ist auch die Möglichkeit der Personalisierung,
also der Anpassung auf die Bedürfnisse und Interessen der Nutzerin oder des Nutzers.
Es wäre beispielsweise denkbar, dass eine Nutzerin die Ratsinformationssysteme,
für die sie sich interessiert, dauerhaft in der App einrichtet und eine Favoritenliste
der Gremien, die ihre bevorzugten Themengebiete behandeln, hinterlegt. Die App
könnte aufgrund dieser Favoritenliste eigenständig über die API nach neuen
Sitzungsterminen, Tagesordnungspunkten, Drucksachen und Dokumente suchen. Taucht
dabei ein neues Objekt auf, wird die Nutzerin darüber benachrichtigt. Sie kann dann
beispielsweise entscheiden, Dokumente direkt zu öffnen oder für den späteren 
Offline-Zugriff zu speichern.

Einem derartigen Szenario kommt das Graph-orientierte Datenmodell der OParl API
entgegen. Ausgehend von einer Sitzung eines bestimmten Gremiums beispielsweise
ist es damit einfach möglich, die in Verbindung stehenden Mitglieder des Gremiums,
Teilnehmer der Sitzung, Tagesordnungspunkte der Sitzung oder Drucksachen zu den
Tagesordnungspunkten und letztlich Dokumente zu Drucksachen und Sitzung abzurufen.

Für die Nutzer einer mobilen Client-Anwendung könnte es sich als besonders hilfreich
erweisen, wenn Dokumente auf dem Server in verschiedenen Formaten zur Verfügung
gestellt werden. Denn nicht jedes Endgerät mit kleinem Bildaschirm bietet eine
nutzerfreundliche Möglichkeit, beispielsweise Dokumente im weit verbreiteten PDF-Format 
darzustellen. Hier könnte schon der Entwickler der mobilen App Mechanismen vorsehen,
die, sofern vorhanden, besser geeignete Formate wie z.B. HTML abrufen.

Neben dem kleinen Display kann für einige mobile Endgeräte auch die im Vergleich zu
einem zeitgemäßen Desktop-PC geringere CPU-Leistung eine Einschränkung darstellen.
Solchen Geräten kommt es besonders entgegen, wenn der Server zu allen Dokumenten auch
den reinen Textinhalt abrufbar macht, der dann beispielsweise für eine Volltextsuche
auf dem Endgerät indexiert werden kann. So wiederum kann auf dem Client eine
Suchfunktion realisiert werden, welche die OParl-API selbst nicht zur Verfügung
stellt.

Eine solche Suchfunktion kann auch über die reine Volltxtsuche hinaus gehen
und über die Suche mittels Text- oder Spracheingabe hinaus gehen. Denn ein Client
könnte von einem [Server](#server)-System, das Drucksachen mit Geoinformationen
anbietet, diese abrufen und räumlich indexieren. Anhand der Position des Geräts,
die mittels GPS genau bestimmt werden kann, könnte so der lokale Cache nach
Objekten in der Umgebung durchsucht werden. Das Ergebnis könnte auf einer Karte
dargestellt oder in einer Ergebnisliste angezeigt werden, die nach Distanz zum
Objekt sortiert werden könnte.

## Szenario 2: Integration in Web-Portal  {#szenario_web_portal}

Web Portale bieten Nutzern unter anderem die Möglichkeit Anwendungen, Prozesse und Dienste zu integrieren. Die OParl API stellt einen solchen Dienst dar und bereitet so den Weg zu angereicherten Portalseiten. Informationen, die über die API bezogen werden, können in Portlets organisiert und visualisiert werden. Hierbei können

1. angemeldete Benutzer 

die eingegrenzten Portlet Parameter für den nächsten Besuch zwischen speichern, während

2. anonyme Benutzer 

dies nicht können. In beiden Fällen können Portalnutzer das angezeigte Portlet nach ihren Bedürfnissen anpassen. Beispielsweise kann ein solches Portlet eine Liste der Gremien bereitstellen, aus der sich der Nutzer das interessante Gremium aussucht und aufgrund dieser Auswahl die Informationen zu den vergangenen / nächsten Sitzungsterminen im Rat, etwaiger Drucksachen oder Dokumenten erhält und geeignet visualisiert. 

Durch eine solche Integration von RIS Informationen in bestehende Portalsysteme (unter Umständen die kommunale Webseite selbst), ist es möglich Nutzern zusätzliche 
Informationen in der bereits gewohnten Umgebung zu präsentieren und den bestehenden Informationsgehalt und den Datenbestand aufzuwerten.


## Szenario 3: Meta-Suche  {#szenario_meta_suche}

TODO

## Szenario 4: Forschungsprojekt Themen- und Sprachanalyse {#szenario_forschung}

TODO
