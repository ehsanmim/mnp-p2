# mnp-p2
Modellierung nebenläufiger Prozesse

Wir können Aufgaben erledigen und als abgeschlossen markieren. Bitte pusht auch alles, sobald ein kleiner Teil erledigt ist, damit wir unsere Arbeit weiterentwickeln und ergänzen.

Hier ist eine Liste von To-dos für das Projekt, die unter Verwendung von Formulierungen und Begriffen aus dem bereitgestellten PDF-Dokument auf Deutsch verfasst wurde.

### **Phase 1: Projekteinrichtung und Grundkonfiguration**

In dieser Phase wird die Projektumgebung gemäß den Vorgaben korrekt eingerichtet.

* **To-Do:**
    * [ ] **Erstellung eines kompilierbaren Gradle-Projekts**[cite: 13].
    * [ ] Die **Akka Actor Typed-Bibliothek in Version 2.9 oder höher** [cite: 5] als Abhängigkeit in der `build.gradle`-Datei hinzufügen. Es dürfen **keine anderen Bibliotheken als die Akka Actor Typed-Bibliothek und die Standardbibliothek** [cite: 6] genutzt werden.
    * [ ] Eine geordnete Paketstruktur für das Projekt definieren (z. B. `de.meinautobauer.produktion`).
    * [ ] Kopfzeilen in allen **Javadateien** [cite: 9] vorbereiten, um **Name und Matrikelnummer von allen Studierenden** [cite: 9] der Gruppe zu notieren.

### **Phase 2: Entwurf des Kern-Aktors und des Nachrichtenprotokolls**

Diese Phase konzentriert sich auf die grundlegenden Bausteine des Systems: die Aktoren und die Nachrichten, die sie austauschen.

* **To-Do:**
    * [ ] **Definition der Nachrichten:** Der Datenaustausch muss **ausschließlich über Nachrichten** [cite: 8] erfolgen.
        * Eine Nachricht, die einen Aktor anweist, ein Bauteil zu produzieren (z. B. `ProduziereBauteil`).
        * Eine Nachricht zur Meldung der **Fertigstellung einer Komponente** [cite: 33] (z. B. `BauteilFertiggestellt`), die vom untergeordneten an den übergeordneten Aktor gesendet wird.
    * [ ] **Entwurf des Produktions-Aktors:** Dies wird der allgemeine Aktor sein, der für die Produktion jedes Bauteils zuständig ist. Für die Produktion jeder Komponente wird **immer ein eigener Aktor gestartet**[cite: 29].
    * [ ] **Hinterlegen der Baupläne:** Die **Baupläne für die einzelnen elektronischen Bauteile im Code hinterlegen**[cite: 32].
        * $EB_{1}=(BB_{1},BB_{2})$ [cite: 20]
        * $EB_{2}=(EB_{1},BB_{2})$ [cite: 20]
        * $EB_{3}=(BB_{3},EB_{2})$ [cite: 20]
        * $EB_{4}=(EB_{1},EB_{3})$ [cite: 20]

### **Phase 3: Implementierung der Produktionslogik**

Hier wird die entworfene Logik in Java umgesetzt, wobei der Fokus auf dem parallelen, aber geordneten Produktionsablauf liegt.

* **To-Do:**
    * [ ] **Implementierung der Aktor-Logik:**
        * Wenn der Aktor eine `ProduziereBauteil`-Nachricht erhält, prüft er, ob es sich um einen **Basisbaustein (BB)** [cite: 19] oder ein **elektronisches Bauteil (EB)** [cite: 19] handelt.
        * **Falls BB:** Die Fertigstellung durch eine **Lognachricht** [cite: 33] anzeigen und `BauteilFertiggestellt` an den Eltern-Aktor senden.
        * **Falls EB:**
            1.  Die beiden Unterkomponenten aus den Bauplänen ermitteln.
            2.  Für die erste Komponente **dynamisch einen Aktor instanziieren** [cite: 36], indem `AkkaContext.spawnAnonymous` verwendet wird[cite: 37].
            3.  Eine `ProduziereBauteil`-Nachricht an diesen neuen Aktor senden.
            4.  Auf die `BauteilFertiggestellt`-Nachricht warten. Es muss sichergestellt werden, dass die **Reihenfolge der Baupläne eingehalten wird**[cite: 24, 34].
            5.  Nach Erhalt der Bestätigung, den Prozess für die zweite Komponente wiederholen.
            6.  Sobald die zweite Komponente fertig ist, die Fertigstellung des eigenen EB per Lognachricht ausgeben und `BauteilFertiggestellt` an den übergeordneten Prozess senden.
    * [ ] **Erstellung der Hauptklasse:**
        * Das Akka `ActorSystem` starten.
        * Den initialen Aktor erstellen, der den gesamten Produktionsprozess anstößt. Dieser soll die **Produktion von $EB_{4}$ testen**[cite: 26].

### **Phase 4: Test und Erstellung eines neuen Bauteils**

In dieser Phase wird die Korrektheit der Implementierung überprüft und die letzte Teilaufgabe erfüllt.

* **To-Do:**
    * [ ] **Testen der `EB_4`-Produktion:** Die Anwendung ausführen und die Konsolenausgabe überprüfen. Es muss **in jedem Schritt ersichtlich sein, was geschieht**[cite: 25].
    * [ ] **Neues Bauteil erstellen:** **Ein neues elektronisches Bauteil aus den gegebenen Komponenten erstellen, das wenigstens eine Tiefe von drei hat**[cite: 27]. Ein Beispiel wäre $EB_5 = (EB_3, EB_4)$.
    * [ ] **Neues Bauteil testen:** Die Anwendung so anpassen, dass sie das neu erstellte Bauteil produziert, und die Ausgabe validieren.

### **Phase 5: Abschließende Prüfung und Abgabe**

Der letzte Schritt ist die Finalisierung des Projekts für die Abgabe.

* **To-Do:**
    * [ ] **Die Aufgabe mit sinnvollen Kommentaren versehen**[cite: 8].
    * [ ] **Code auf Plagiate testen** [cite: 10]: Sicherstellen, dass die Arbeit eigenständig ist oder Gruppenarbeit korrekt deklariert wurde[cite: 11, 12].
    * [ ] Sicherstellen, dass kein Code auf Methoden des **Classic Akka (nicht getypte Aktoren) aufbaut**[cite: 7].
    * [ ] Die **Abgabe als zip-Datei des kompilierbaren Projekts (Gradle!)** [cite: 13] vorbereiten.
    * [ ] Die Ausarbeitung bis zum **06.07.2025, 23:59** [cite: 3] per Moodle abgeben[cite: 4]. Es muss **nur einer aus Ihrer Gruppe den Quellcode abgeben**[cite: 14].