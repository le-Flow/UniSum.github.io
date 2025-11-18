## Einleitung

**1. Was ist ein Eingebettetes System (ES) und was sind seine charakteristischen Eigenschaften?**

* Ein Eingebettetes System (ES) ist ein Rechensystem, das in einen technischen Kontext (z.B. ein Auto, eine Waschmaschine) "eingebettet" ist, um dort Mess-, Steuer- oder Regelungsaufgaben zu erfüllen.
* **Charakteristische Eigenschaften**:
    * **Enge Kopplung** mit der physikalischen Umwelt (über Sensoren und Aktuatoren).
    * **Reaktive Systeme:** Sie reagieren kontinuierlich auf (oft asynchrone) Ereignisse aus der Umgebung, statt Daten zu transformieren.
    * **Echtzeitanforderungen:** Die korrekte Funktion hängt oft von der Einhaltung zeitlicher Fristen (Deadlines) ab.
    * **Ressourcenbeschränkungen:** Sie sind oft hinsichtlich Kosten, Energieverbrauch, Speicher und Rechenleistung stark optimiert (effizient).
    * **Verlässlichkeit:** Sie müssen hohe Anforderungen an Zuverlässigkeit und Funktionale Sicherheit erfüllen (z.B. ISO 26262).

**2. Nennen Sie einige wichtige Unterschiede zwischen ES- und IT-Systemen.**

* **IT-Systeme** (z.B. Buchhaltungsserver) sind primär **transformationelle Systeme**: Sie verarbeiten einen Stapel Daten (Input) zu einem Ergebnis (Output).
* **Eingebettete Systeme (ES)** sind primär **reaktive Systeme**, die kontinuierlich mit ihrer Umwelt interagieren und auf Stimuli reagieren.
* ES haben eine **enge HW/SW-Verzahnung** und unterliegen **harten Echtzeitanforderungen** sowie **strengen Ressourcen- und Energiebeschränkungen**, was bei IT-Systemen seltener der Fall ist.

**3. Wann funktioniert ein Echtzeitsystem korrekt?**

* Ein Echtzeitsystem funktioniert korrekt, wenn seine Berechnungen nicht nur **logisch korrekt** sind, sondern auch **innerhalb der vorgegebenen Zeitfristen (Deadlines)** erfolgen. Ein richtiges Ergebnis zur falschen Zeit ist ein Fehler.

**4. Was ist der Unterschied zwischen weichen und harten Echtzeit-Bedingungen?**

* **Harte Echtzeit (Hard Real-Time):** Das Verpassen einer Deadline kann **katastrophale Folgen** haben (z.B. Airbag-Auslösung). Der Nutzen des Ergebnisses fällt nach der Deadline sofort auf null oder wird negativ.
* **Weiche Echtzeit (Soft Real-Time):** Das Verpassen einer Deadline ist **tolerierbar** und führt z.B. nur zu Komfortverlust oder Qualitätsminderung (z.B. Ruckeln beim Video-Streaming). Der Nutzen des Ergebnisses sinkt nach der Deadline allmählich.

**5. Nennen Sie einige wichtige nicht-funktionale Anforderungen an ES.**

* **Effizienz** (Preis, Gewicht, Energieverbrauch)
* **Verlässlichkeit** (Reliability)
* **Funktionale Sicherheit** (Safety)
* **Echtzeitfähigkeit** (Rechtzeitigkeit)
* **Robustheit**

---

## Begriffe und Grundlagen

**6. Was ist ein Signal?**

* Ein Signal ist der Träger von Information, dargestellt als eine physikalische Größe, die sich zeitlich ändert (z.B. Spannung).

**7. Nach welchen Kriterien lassen sich Signale klassifizieren?**

* Nach dem **Zeitbereich** (zeitkontinuierlich oder zeitdiskret).
* Nach dem **Wertebereich** (wertkontinuierlich oder wertdiskret).

**8. Was ist der Unterschied zwischen zeitdiskreten und wertdiskreten Signalen?**

* **Zeitdiskret:** Das Signal ist nur zu bestimmten, diskreten Zeitpunkten definiert (z.B. ein abgetastetes Signal).
* **Wertdiskret:** Das Signal kann nur eine endliche (abzählbare) Anzahl von Werten annehmen (z.B. ein quantisiertes Signal).

**9. Was ist ein digitales Signal?**

* Ein digitales Signal ist sowohl **zeitdiskret** als auch **wertdiskret**.

**10. Welche Art von Signalen kann ein reales Übertragungsmedium übertragen?**

* Reale physikalische Übertragungsmedien übertragen immer **analoge Signale** (zeit- und wertkontinuierliche Signale).

---

## Aufbau ES

**11. Was ist der MSR-Kreislauf? Skizzieren Sie ihn gedanklich.**

* Der MSR-Kreislauf (Messen, Steuern, Regeln) beschreibt den geschlossenen Regelkreis in eingebetteten Systemen.
* **Sensorik** erfasst den Prozesszustand (Messen), die **Verarbeitungseinheit** ($\mu P$) trifft Entscheidungen (Verarbeiten) und die **Aktorik** beeinflusst den Prozess (Stellen/Regeln).

**12. Was versteht man unter dem Begriff „Sensor“ (bei ES)? Zu was dienen sie und was ist i. A. bei Sensorsignalen zu beachten?**

* Sensoren sind Bauteile, die nichtelektrische (z.B. mechanische, thermische) Größen aus dem Prozesszustand erfassen und in elektrische Signale umwandeln.
* Bei Sensorsignalen ist zu beachten, dass sie oft **verrauscht**, fehlerbehaftet oder von Störungen überlagert sind.

**13. Nach welchen Eigenschaften lassen sich Sensoren klassifizieren?**

* **Extrinsisch** (erfassen die Umgebung, z.B. Kamera) vs. **Intrinsisch** (erfassen den internen Systemzustand, z.B. Gyroskop).
* Nach **Integrationsstufen**: Elementarsensor (reiner Wandler), Integrierter Sensor (mit Signalaufbereitung), Intelligenter Sensor (mit Vorverarbeitung).

**14. Beschreiben Sie das Messprinzip eines mechanischen, kapazitiven Beschleunigungssensors.**

* Eine träge Masse ist federnd aufgehängt ($F = m \cdot a = k \cdot \Delta d$). Bei Beschleunigung wird diese Masse ausgelenkt ($\Delta d$).
* Die Masse ist als mittlere Elektrode eines **Differentialkondensators** ($C_1$, $C_2$) realisiert. Die Auslenkung ändert die Abstände und damit die Kapazitäten $C_1$ und $C_2$ gegenläufig. Diese Kapazitätsänderung wird gemessen.

**15. Beschreiben Sie die Funktionsweise eines inkrementellen Positions-/Winkelsensors mit Lichtschranken.**

* Ein **Optischer Encoder** (Inkrementalgeber) verwendet eine rotierende Scheibe mit einem feinen Strichmuster (hell/dunkel).
* Zwei leicht versetzte Lichtschranken (Detektor A, B) tasten das Muster ab. Aus der Anzahl der Impulse wird die Position/Winkeländerung berechnet, aus der Phasenverschiebung von A zu B die **Bewegungsrichtung**.

**16. Was ist die Aufgabe eines Aktuators?**

* Aktuatoren (oder Aktoren) beeinflussen den technischen Prozess, indem sie elektrische Energie (das Steuersignal) in eine andere Energieform, meist mechanische Arbeit, umwandeln (z.B. Motorbewegung, Kraft).

**17. Gleichstrommotoren werden meist mit einer H-Brücke und einem PWM-Signal angesteuert. Beschreiben Sie den Vorgang. Was kann alles damit gesteuert werden?**

* Eine **H-Brücke** ist eine Schaltung aus vier Schaltern (Transistoren). Durch paarweises Schließen der diagonalen Schalter kann die **Polung** am Motor umgekehrt werden.
* Ein **PWM-Signal** (Pulsweiten-Modulation) wird an die H-Brücke angelegt. Das Tastverhältnis (Duty Cycle) der PWM bestimmt die mittlere Spannung am Motor.
* Gesteuert werden:
    1.  **Drehrichtung** (durch Umpolen der H-Brücke).
    2.  **Drehzahl / Drehmoment** (durch das Tastverhältnis der PWM).

**18. Was sind die Vorteile und Nachteile von Schrittmotoren?**

* **Vorteile:** Sie können in diskreten Winkelschritten angesteuert werden und ermöglichen eine Positionierung im "Open-Loop"-Betrieb (Steuerung) **ohne Sensorik** (Rückführung).
* **Nachteile:** Sie haben ein geringeres Drehmoment, sind ineffizienter und können bei Überlast "Schritte verlieren" (die Position ist dann unbekannt).

**19. Welche 3 Schritte sind bei der Abtastung eines analogen Eingangssignals notwendig?**
1.  **Filterung:** Entfernung von Frequenzen oberhalb der halben Abtastrate mittels **Anti-Aliasing-Filter** (analoger Tiefpass).
2.  **Halten:** Festhalten des analogen Spannungswertes während der Wandlung mittels **Sample & Hold (S&H)**-Schaltung.
3.  **Wandlung:** Diskretisierung von Zeit und Wert mittels **A/D-Wandler (ADC)**.

**20. Welche 3 Schritte sind bei der Rückführung eines digitalen Ausgangssignals zu einem analogen Ausgangssignal notwendig?**
1.  **Wandlung:** Umwandlung des digitalen Werts in eine analoge (oft gestufte) Spannung mittels **D/A-Wandler (DAC)** (oder Erzeugung eines **PWM**-Signals).
2.  **Entstörung (Deglitching):** (Nur bei DACs nötig) Entfernen von Umschalt-Spitzen (Glitches) mittels **Deglitcher (S&H-Schaltung)**.
3.  **Glättung:** Entfernen der "Treppenstufen" (bei DAC) bzw. Glättung der Pulse (bei PWM) mittels **Tiefpassfilter** (Rekonstruktionsfilter).

**21. Was besagt das Nyquist-Shannon-Abtasttheorem?**

* Die Abtastfrequenz ($f_a$) muss **mindestens doppelt so hoch** sein wie die höchste im Signal enthaltene Frequenz ($f_g$), um das Signal exakt rekonstruieren zu können.
    
$$f_a > 2 \cdot f_g$$

**22. Was sind Alias-Effekte, wann entstehen sie und was muss man zu deren Vermeidung beachten?**

* **Alias-Effekte** entstehen, wenn das Nyquist-Shannon-Theorem **verletzt** wird (die Abtastrate zu gering ist).
* Hohe Frequenzen im Signal "tarnen" sich als niedrigere Frequenzen und verfälschen die Messung.
* **Vermeidung:** Man muss zwingend ein **Anti-Aliasing-Filter** (einen analogen Tiefpassfilter) **vor** der Abtastung verwenden, um alle Frequenzen oberhalb $f_a/2$ abzuschneiden.

**23. Was ist die Aufgabe einer Sample&Hold-Schaltung vor einem A/D-Wandler?**

* Ein ADC benötigt eine endliche Wandlungszeit. Die S&H-Schaltung "friert" den analogen Spannungswert am Abtastzeitpunkt ein und hält ihn **während der Dauer der A/D-Wandlung konstant**.

**24. Was sind Hazards (Glitches) und wie werden sie bei der D/A-Wandlung vermieden?**

* **Hazards (Glitches)** sind unerwünschte, kurze Spannungsspitzen (Spikes) am Ausgang eines **D/A-Wandlers**. Sie entstehen, wenn die Bits des digitalen Worts nicht exakt gleichzeitig umschalten (z.B. beim Übergang `0111` $\to$ `1000` könnte kurz `0000` anliegen).
* Sie werden durch einen nachgeschalteten **Deglitcher** (eine S&H-Schaltung) vermieden, der den letzten stabilen Wert hält, bis der DAC den neuen Wert stabil ausgegeben hat.

**25. Welche Typen von A/D-Wandlern unterscheidet man und was sind die wichtigsten Eigenschaften?**

* **Wägeverfahren (Successive Approximation, SAR):** Schrittweiser Vergleich (Bit für Bit). Guter Kompromiss zwischen Geschwindigkeit und Kosten, sehr verbreitet.
* **Parallele Wandler (Flash):** Extrem schnell (eine Taktperiode). Benötigen aber $2^n-1$ Komparatoren, daher teuer und meist auf niedrige Auflösungen (z.B. 8 Bit) beschränkt.
* **Integrierende Wandler (z.B. Dual-Slope):** Langsam, aber sehr genau und robust gegen Störfrequenzen (z.B. 50/60Hz-Brummen).

**26. Was versteht man unter Pulsweiten-Modulation (PWM-Modulation)? Wofür wird sie verwendet?**

* **PWM** ist ein digitales (Rechteck-)Signal mit konstanter Frequenz, aber **variablem Tastverhältnis** (Verhältnis von "EIN"-Zeit zu "AUS"-Zeit).
* **Verwendung:**
    1.  Effiziente Ansteuerung von Aktuatoren (z.B. **Motor-Drehzahlsteuerung**, **LED-Dimmung**).
    2.  Als energiesparende Alternative zu einem D/A-Wandler (wenn ein Tiefpassfilter nachgeschaltet wird).

**27. Welche 3 Technologien gibt es bei den Verarbeitungseinheiten von ES und was sind deren Vor- und Nachteile?**

1.  **Prozessoren ($\mu P$, $\mu C$, DSPs):**
    * Vorteil: **Höchste Flexibilität** (Software).
    * Nachteil: Geringste Energieeffizienz (Operationen/Watt).
2.  **ASICs (Application-Specific Integrated Circuits):**
    * Vorteil: **Höchste Energieeffizienz** (fest verdrahtet).
    * Nachteil: **Unflexibel**, extrem hohe Entwicklungskosten.
3.  **Rekonfigurierbare Logik (FPGAs):**
    * Vorteil: Ein **Kompromiss** zwischen Effizienz und Flexibilität.
    * Nachteil: Komplex in der Programmierung (z.B. VHDL).

**28. Was sind ASICs und wann kommen sie zum Einsatz?**

* **ASICs** (Application-Specific Integrated Circuits) sind anwendungsspezifische, fest verdrahtete Schaltungen.
* Sie kommen bei **sehr hohen Stückzahlen** zum Einsatz, bei denen maximale Energieeffizienz und minimale Kosten pro Stück wichtiger sind als Flexibilität (z.B. in Mobiltelefonen).

**29. Was versteht man unter dem Effizienz-/Flexibilitätskonflikt?**

* Es ist der Zielkonflikt, dass Bauteile mit hoher **Flexibilität** (wie Prozessoren) meist eine niedrige **Energieeffizienz** haben, während Bauteile mit hoher Energieeffizienz (wie ASICs) meist **unflexibel** sind. FPGAs liegen dazwischen.

**30. Warum ist ein minimaler Energieverbrauch bei mobilen Geräten so wichtig?**

* Ein minimaler Energieverbrauch ist der Schlüsselfaktor für die **Akkulaufzeit** mobiler Geräte.

**31. Auf was alles wirkt sich die Leistungsaufnahme eines Gerätes aus?**

* **Akkulaufzeit** (bei mobilen Geräten).
* **Wärmeentwicklung** (erfordert ggf. Kühlung, was Größe, Gewicht und Kosten erhöht).
* **Betriebskosten** (Stromverbrauch).

**32. Wie können Prozessoren für ES hinsichtlich Effizienz optimiert werden?**

* Durch **spezialisierte Hardware** (z.B. Co-Prozessoren).
* Durch **intelligentes Energiemanagement**, z.B. verschiedene **Energiesparzustände** (Run, Idle, Sleep) und das Abschalten ungenutzter Peripherie (Clock Gating).

**33. Was sind rekonfigurierbare Logiken und wann kommen sie zum Einsatz?**

* Dies sind Bauteile wie **FPGAs** (Field-Programmable Gate Arrays).
* Ihre interne Logikstruktur ist nicht fest verdrahtet, sondern kann (neu) konfiguriert werden. Sie kommen als Kompromiss zum Einsatz, wenn ASICs zu teuer (geringe Stückzahl) und Prozessoren zu langsam oder ineffizient sind.

**34. Was sind FPGAs und wie sind diese aufgebaut?**

* **FPGAs** (Field-Programmable Gate Arrays) sind rekonfigurierbare Logiken.
* Sie bestehen aus einem großen Array von **konfigurierbaren Logikblöcken (CLBs)** – diese enthalten z.B. Look-Up Tables (LUTs) und Flip-Flops – die durch ein programmierbares Verbindungsnetzwerk (Routing) miteinander verschaltet werden.

---

## Steuerung und Regelung

**35. Zu was werden Filter in ES eingesetzt?**

* **Signalverbesserung:** z.B. **Rauschen entfernen** (Tiefpass).
* **Signalvorbereitung:** z.B. **Anti-Aliasing** (Tiefpass) oder Gleichanteile entfernen (Hochpass).
* **Signaltrennung:** z.B. eine bestimmte Störfrequenz (Netzbrummen) entfernen (Bandsperre).
* **Signalrekonstruktion:** Glättung von DAC- oder PWM-Signalen (Tiefpass).

**36. Was sind die Eigenschaften eines idealen Filters? Wie kann man sich diesen bei digitalen Filtern nähern?**

* Ein **ideales Filter** hätte eine Verstärkung von 1 im Durchlassbereich, 0 im Sperrbereich und einen unendlich steilen Abfall (Übergangsbereich = 0).
* Annäherung bei digitalen Filtern: Durch **Erhöhung der Filterordnung** (mehr Koeffizienten/Verzögerungsglieder), was die Flanke steiler macht.

**37. Was ist bei einem Filter die Grenzfrequenz?**

* Die Frequenz ($f_g$), bei der die Signal-Amplitude am Ausgang um **-3 dB** (also auf ca. 70,7% des Eingangswerts bzw. die halbe Leistung) abgefallen ist.

**38. Nennen Sie Anwendungsfälle für Hochpass-, Tiefpass-, Bandpass- und Bandsperren-Filter.**

* **Tiefpass:** Rauschen filtern, Anti-Aliasing, Glättung von PWM/DAC-Signalen.
* **Hochpass:** Gleichanteile oder langsame Drifts entfernen (z.B. bei Audio- oder Biosignalen).
* **Bandpass:** Ein bestimmtes Frequenzband isolieren (z.B. ein Funksignal).
* **Bandsperre (Notch-Filter):** Eine einzelne Störfrequenz gezielt entfernen (z.B. 50/60 Hz Netzbrummen).

**39. Aus welchen Bauteilen bestehen analoge, passive Filter?**

* Sie bestehen nur aus passiven Bauteilen: **Widerstände (R), Kondensatoren (C) und Spulen (L)**.

**40. Was sind die Nachteile analoger Filter?**

* Sie sind **anfällig für Bauteiltoleranzen, Alterung und Temperaturdrift**.
* Komplexe Filter (hoher Ordnung) sind schwer zu realisieren; Spulen (L) sind oft groß und teuer.

**41. Was sind die Vorteile digitaler Filter?**

* **Perfekt reproduzierbar** (da sie auf Berechnungen basieren), keine Alterung oder Drift.
* **Flexibel:** Parameter können per Software geändert werden (adaptive Filter).
* **Komplexe Filter** (z.B. FIR-Filter mit linearer Phase) sind realisierbar, die analog unmöglich wären.

**42. Durch was wird die max. Frequenz digitaler Filter begrenzt?**

* Durch das **Nyquist-Theorem**: Ein digitaler Filter kann nur Frequenzen bis maximal zur **halben Abtastfrequenz** ($f_a / 2$) sinnvoll verarbeiten.

**43. Ein digitales System (Filter) kann durch eine Differenzengleichung beschrieben werden. Was ist das?**

* Eine Differenzengleichung beschreibt, wie der *nächste* Ausgangswert ($y_k$) aus *aktuellen* ($x_k$) und *vergangenen* ($x_{k-1}, y_{k-1}$) Ein- und Ausgangswerten berechnet wird.
* **Beispiel (IIR):** $y_k = 0.1 \cdot x_k + 0.9 \cdot y_{k-1}$

**44. Was sind die Unterschiede zw. einem FIR-Filter und einem IIR-Filter?**

* **FIR (Finite Impulse Response):**
    * **Nicht-rekursiv** (keine Rückkopplung des Ausgangs). Formel: $y_n = \sum b_k \cdot x_{n-k}$
    * Die Impulsantwort hat eine *endliche* Länge.
    * Sind **immer stabil** und können linearphasig (konstante Gruppenlaufzeit) sein.
* **IIR (Infinite Impulse Response):**
    * **Rekursiv** (verwendet vergangene Ausgangswerte). Formel: $y_n = \sum b_k \cdot x_{n-k} + \sum a_j \cdot y_{n-j}$
    * Die Impulsantwort ist *unendlich* lang.
    * Benötigen viel weniger Rechenaufwand (Ordnung) für dieselbe Steilheit, **können aber instabil werden**.

**45. Was ist die Ordnung eines digitalen Filters? Was beeinflusst die Ordnung?**

* Die Ordnung ist die **Anzahl der benötigten Verzögerungsglieder** (Speicherplätze für $x_{k-n}$ oder $y_{k-n}$).
* Die Ordnung beeinflusst die **Steilheit der Filterflanke** (Übergangsbereich): Eine höhere Ordnung ergibt einen steileren, "besseren" Filter, erfordert aber mehr Rechenleistung.

**46. Was ist der Unterschied zwischen einer Steuerung und einer Regelung?**

* **Steuerung (Open-Loop):** Eine **offene Wirkkette**. Die Stellgröße wird ohne Kenntnis der tatsächlichen Ausgangsgröße (Ist-Wert) gesetzt. Störungen werden nicht erkannt und nicht korrigiert.
* **Regelung (Closed-Loop):** Eine **geschlossene Wirkkette** (Regelkreis). Die Ausgangsgröße (Ist-Wert) wird gemessen und vom Soll-Wert abgezogen (Regelabweichung). Der Regler korrigiert basierend auf dieser Abweichung.

**47. Skizzieren Sie einen allgemeinen Regelkreis.**

* Ein Regelkreis besteht aus:
    * **Summierstelle:** Bildet die Regelabweichung $e = w - x$ (Soll-Wert $w$, Ist-Wert $x$).
    * **Regler:** Erzeugt die Stellgröße $y$ aus $e$.
    * **Regelstrecke:** Der Prozess, der von $y$ (und Störgröße $z$) beeinflusst wird und den Ist-Wert $x$ liefert.
    * **Rückführung:** Führt $x$ (oft über einen Sensor) zur Summierstelle zurück.

**48. Welche Kenngrößen gibt es für die dynamische Regelgüte?**

* **Dynamische Regelgüte** beschreibt das Zeitverhalten beim Übergang in einen neuen Zustand.
* Kenngrößen sind z.B. die **Anregelzeit** (wie schnell der Wert erstmals erreicht wird), die **Ausregelzeit** (bis der Wert dauerhaft im Toleranzband bleibt) und die **Überschwingweite** (wie stark das System über das Ziel hinausschießt).

**49. Was beschreibt die stationäre Regelgüte?**

* Die **stationäre Regelgüte** beschreibt die Genauigkeit im **eingeschwungenen Zustand**, d.h. die **bleibende Regelabweichung** (den Fehler, der "übrig bleibt").

**50. Durch welches Übertragungsglied im Regler kann man die stationäre Regelabweichung zu Null bekommen?**

* Durch einen **I-Anteil (Integral-Anteil)**. Nur Regler mit I-Anteil (I-, PI-, PID-Regler) können die bleibende Regelabweichung vollständig eliminieren.

**51. Ein Regelkreis kann stabil oder instabil sein. Was heißt das?**

* **Stabil:** Nach einer Störung oder einer Sollwertänderung kehrt die Regelgröße (Ist-Wert) in einen stabilen Endzustand zurück.
* **Instabil:** Die Regelgröße schwingt sich unkontrolliert auf (Amplitude wächst) oder wächst unbegrenzt an. Dies kann zur Zerstörung der Strecke führen.

**52. Ein Regelkreisverhalten sollte robust ausgelegt werden. Was heißt das?**

* **Robustheit** bedeutet, dass die Regelung (z.B. Stabilität und Regelgüte) auch dann erhalten bleibt, wenn sich die Parameter der Regelstrecke leicht ändern (z.B. durch Alterung, Temperatur oder unterschiedliche Beladung).

---

## Modellierungstechniken

**53. Beschreiben Sie mit eigenen Worten das Grundprinzip des modellbasierten Entwicklungsansatzes.**

* Beim **Modellbasierten Design (MBD)** ist das **Modell** (z.B. ein Simulink-Blockschaltbild) das zentrale Entwicklungsartefakt.
* Statt manuell Code (z.B. in C) zu schreiben, wird die Logik grafisch modelliert. Aus diesem Modell wird der finale **Quellcode automatisch generiert** (mittels Auto-Coder).
* Dieser Ansatz ermöglicht frühe Tests und Simulationen (MIL, SIL) und eine klare Trennung von Funktion und Implementierung.

**54. Warum sind bei ES Funktionsmodelle mit nachgelagerter Code-Generierung oft geeigneter als fertige Softwarebibliotheken?**

* Eine fertige Softwarebibliothek ist oft generisch und muss alle Eventualitäten abdecken, was zu unnötigem Overhead führt (Effizienz-Flexibilitäts-Konflikt).
* Ein **Auto-Coder** generiert aus einem Modell (z.B. einem Fuzzy-Regler-Modell) hochoptimierten, **spezifischen Code**, der *nur* die benötigte Variante implementiert und daher effizienter (schneller, speichersparender) ist.

**55. Nennen Sie Anforderungen, die man an Modellierungssprachen stellen kann.**
1.  Abbildung von **Hierarchie** (Strukturierung).
2.  Abbildung von **Nebenläufigkeit** (Parallelität).
3.  Abbildung von **Zeitverhalten** (Deadlines, Perioden).
4.  Abbildung von **reaktivem Verhalten** (z.B. Zustandsautomaten).
5.  Abbildung von **Datenfluss**.
6.  **Ausführbarkeit/Simulierbarkeit**.
7.  Möglichkeit zur **Code-Generierung**.
8.  Formale Verifizierbarkeit.
9.  Wiederverwendbarkeit.
10. Eindeutige Syntax und Semantik.

**56. Was sind die Nachteile des Ausführungsmodells „Von-Neumann“?**

* Das Von-Neumann-Modell ist rein **sequenziell** (Control Flow).
* **Nebenläufigkeit** (z.B. durch Threads) muss manuell verwaltet werden und ist extrem fehleranfällig (z.B. **Race Conditions**, **Deadlocks**). Edward Lee nannte es "unverständlich für Menschen".

**57. Nennen Sie 3 alternative Ausführungsmodelle und ihren Fokus.**
1.  **Datenflussmodell (Data Flow):** Fokus auf dem **Datenfluss**; die Ausführung wird durch die Verfügbarkeit von Daten getriggert.
2.  **Endliche Zustandsautomaten (FSM):** Fokus auf **reaktivem Verhalten** und Zustandsübergängen.
3.  **Diskretes Ereignismodell:** Fokus auf einer **zeitlich sortierten Warteschlange** von Ereignissen.

**58. Beschreiben Sie die Eigenschaften (reiner) Datenflussmodelle.**

* Die Ausführung (die "Feuerreihenfolge" der Blöcke) wird durch die **Verfügbarkeit von Daten** bestimmt (Data Flow Order), nicht durch einen sequenziellen Programmzähler (Control Flow). Sie sind inhärent parallel.

**59. Beschreiben Sie die Eigenschaften des Ausführungsmodells „Endlichen Zustandsautomaten“.**

* Das System befindet sich immer in einem definierten **Zustand**.
* **Ereignisse** (Events) lösen **Übergänge (Transitionen)** von einem Zustand in einen anderen aus.
* Gut geeignet für die Modellierung von **reaktivem Verhalten** (z.B. Steuerung von Benutzeroberflächen oder Protokollen).

**60. Was ist das zentrale Modellierungselement beim Ausführungsmodell diskrete Ereignisse?**

* Das zentrale Element ist eine **zeitlich sortierte Warteschlange von Ereignissen** (Zeit-Aktions-Paare).
* Die Simulation "springt" von einem Ereigniszeitpunkt direkt zum nächsten, die Zeit dazwischen wird übersprungen.

**61. Was ist das Testobjekt bei Modell-in-the-Loop-Simulationen (MIL) und was ist der Zweck?**

* **Testobjekt:** Das **Modell** selbst (z.B. das Simulink-Modell).
* **Zweck:** Test der **Funktion und Algorithmenlogik** auf dem Host-PC (Entwicklungsrechner), losgelöst von der Hardware.

**62. Was ist das Testobjekt bei Software-in-the-Loop-Simulationen (SIL) und was ist der Zweck?**

* **Testobjekt:** Der **automatisch generierte Code**, der aus dem Modell erstellt wurde.
* **Zweck:** Test auf **Konsistenz zwischen Modell und Code**. Der Code läuft (kompiliert) auf dem Host-PC.

**63. Was ist das Testobjekt bei Processor-in-the-Loop-Simulationen (PIL) und was ist der Zweck?**

* **Testobjekt:** Der **automatisch generierte Code**, der für den **Ziel-Prozessor** (den realen Mikrocontroller) kompiliert wurde.
* **Zweck:** Test des Codes auf der **realen Hardware** (Prozessor). Testet den Compiler, das Laufzeitverhalten und den Ressourcenbedarf (z.B. Speicher, CPU-Zeit).

**64. Was ist das Testobjekt bei Hardware-in-the-Loop-Simulationen (HIL) und was ist der Zweck?**

* **Testobjekt:** Das **finale Steuergerät (ECU)** (komplette Hardware mit finaler Software).
* **Zweck:** Test des Steuergeräts in **Echtzeit**. Die Umgebung (z.B. das Auto, der Motor) wird von einem HIL-Simulator in Echtzeit simuliert. Dient dem Test von kritischen Zuständen und Diagnosefunktionen.

**65. Was ist der wesentliche Unterschied zwischen SIL und PIL?**

* **SIL:** Der generierte Code läuft auf dem **Host-PC** (Entwicklungsrechner).
* **PIL:** Der generierte Code läuft auf dem **realen Ziel-Prozessor** ($\mu C$).

**66. Was ist der wesentliche Unterschied zwischen PIL und HIL?**

* **PIL:** Testet **nur den Prozessor** (oder ein Evaluationsboard) oft ohne Echtzeit-Anbindung an die Umgebung.
* **HIL:** Testet das **komplette, finale Steuergerät** (ECU) unter **Echtzeitbedingungen** an einem Simulator, der die reale Umgebung (Prozess) nachbildet.

**67. Was ist Rapid Prototyping? Welche Ziele verfolgt man damit?**

* **Rapid Prototyping (RP)** ist ein Ansatz, bei dem der generierte Code auf einem sehr leistungsfähigen, universellen Prototyping-Steuergerät (z.B. dSpace Autobox) ausgeführt wird.
* Dieses Steuergerät wird **direkt im realen System** (z.B. im echten Fahrzeug) getestet, um die "Quality Gates" (SIL/PIL/HIL) zunächst zu überspringen.
* **Ziel:** Schnelle Validierung der Funktion im realen Umfeld und Identifikation von Streckenparametern.

---

## SW-Entwicklung für ES

**68. Was sind die Eigenschaften und Anforderungen an die Software eingebetteter Systeme?**

* **Eigenschaften:** Muss mit begrenzten Ressourcen (Speicher, Energie) auskommen, muss robust gegen fehlerhafte Eingaben (Sensordaten) sein.
* **Anforderungen:** Muss oft harten Echtzeitanforderungen, hohen Zuverlässigkeitsanforderungen und Anforderungen an die Funktionale Sicherheit (z.B. ISO 26262) genügen.

**69. In welche 3 klar definierbare, unterschiedliche und teils sogar widersprüchlichen Systemeigenschaften lässt sich der Begriff Verlässlichkeit unterteilen?**
1.  **Zuverlässigkeit (Reliability):** Kontinuierlich fehlerfreie Funktion über einen Zeitraum.
2.  **Verfügbarkeit (Availability):** Anteil der Zeit, in der das System funktioniert.
3.  **Funktionale Sicherheit (Safety):** Freiheit von nicht akzeptierbaren Risiken.

**70. Wie ist Zuverlässigkeit definiert? Ist sie wichtig für ES?**

* **Definition:** Die Wahrscheinlichkeit ($R(t)$), dass das System eine Funktion über einen festgelegten Zeitraum **durchgängig fehlerfrei** erfüllt.
* **Wichtigkeit:** Ja, sie ist extrem wichtig, da ein Ausfall (z.B. der Bremse) katastrophale Folgen haben kann.

**71. Wie ist Verfügbarkeit definiert? Spielt sie bei sicherheitskritischen Systemen eine Rolle?**

* **Definition:** Der Anteil der Zeit, in der das System funktioniert ($Verfügbarkeit = \frac{Gesamtzeit - Ausfallzeit}{Gesamtzeit}$).
* **Rolle:** Sie spielt eine **untergeordnete** Rolle. Ein System kann *sicher*, aber *nicht verfügbar* sein (z.B. ein Zug, der im "Not-Aus" sicher steht), was besser ist als *unsicher*, aber *verfügbar* (z.B. ein Zug mit defekten Bremsen, der fährt).

**72. Was ist der typische Verlauf der Ausfallrate als Funktion der Nutzungszeit? Begründen Sie den Verlauf.**

* Dies ist die **"Badewannenkurve"**:
    1.  **Frühausfälle:** Hohe, aber sinkende Ausfallrate (Produktionsfehler).
    2.  **Konsolidierungsphase:** Konstante, niedrige Ausfallrate (Zufallsausfälle).
    3.  **Altersausfälle:** Steigende Ausfallrate (Verschleiß, Alterung).

**73. Erklären Sie die Begriffe Risiko und Grenzrisiko.**

* **Risiko:** Das Produkt aus der **Eintrittswahrscheinlichkeit** eines Schadens und dem **Schadensausmaß** (Schwere des Schadens).
* **Grenzrisiko:** Das maximal gesellschaftlich oder normativ (z.B. in der ISO 26262) akzeptierte Restrisiko.

**74. Was ist Funktionale Sicherheit?**

* Die **Freiheit von nicht akzeptierbaren Risiken**, die durch Fehlfunktionen des ES selbst entstehen (z.B. ein Airbag, der fälschlicherweise auslöst).

**75. Wie wirken sich empfindliche Fehlererkennungsmechanismen auf Zuverlässigkeit und Funktionale Sicherheit tendenziell aus.**

* Sie **erhöhen die Funktionale Sicherheit** (Safety), da gefährliche Zustände erkannt und vermieden werden (z.B. durch Abschalten).
* Sie **senken potenziell die Zuverlässigkeit** (Reliability) / **Verfügbarkeit** (Availability), da das System bei (vielleicht harmlosen) Fehlern öfter ausfällt oder abgeschaltet wird.

**76. Welche Besonderheiten gelten für die Entwicklung sicherheitskritischer Systeme?**

* Es müssen strenge **Normen** (z.B. ISO 26262) befolgt werden.
* Es ist eine intensive **Gefahren- und Risikoanalyse** erforderlich.
* **Redundanz** (Hardware oder Software) wird oft eingesetzt.
* Es ist ein extrem rigoroser **Verifikations- und Validierungsprozess** notwendig.

**77. Was ist das Ziel von Reliability Engineering?**

* Das Ziel ist die **Gewährleistung der Verlässlichkeit** eines Systems durch den Einsatz von konstruktiven (Redundanz) und analytischen (Berechnungs) Maßnahmen.

**78. Was ist das Ziel von analytischen Verfahren beim Reliability Engineering?**

* Das Ziel ist die **Berechnung oder Abschätzung** der Gesamtsystem-Zuverlässigkeit, basierend auf den Zuverlässigkeiten der einzelnen Komponenten.

**79. Wie berechnet sich die Zuverlässigkeit eines seriell/parallel gekoppelten Systems?**

* (Mit $R_i$ = Zuverlässigkeit der Komponente i)
* **Serielle Kopplung** (System fällt aus, wenn 1 Komponente ausfällt):
    
$$R_{ges} = R_1 \cdot R_2 \cdot \ldots \cdot R_n$$

* **Parallele Kopplung** (System funktioniert, wenn mind. 1 Komponente funktioniert):
    
$$R_{ges} = 1 - [(1-R_1) \cdot (1-R_2) \cdot \ldots \cdot (1-R_n)]$$

**80. Welche konstruktiven Maßnahmen gibt es beim Reliability Engineering?**

* Die wichtigste Maßnahme ist der Einsatz von **Redundanz**:
    * Hardware-Redundanz
    * Software-Redundanz
    * Informations-Redundanz (z.B. Paritätsbits, Prüfsummen)

**81. Was ist der Unterschied zw. statischer und dynamischer Redundanz bei Hardware?**

* **Statische Redundanz:** Alle Komponenten sind parallel aktiv. Ein Mehrheitsentscheider (Voter) filtert fehlerhafte Ergebnisse heraus (z.B. 2-aus-3-System).
* **Dynamische Redundanz:** Es gibt aktive Komponenten und passive Reserve-Komponenten (Standby). Eine Fehlererkennung schaltet im Fehlerfall auf die Reservekomponente um.

**82. Wie schaut (statische, dynamische) Redundanz bei der eingebetteten Software aus?**

* **Statisch (N-Versions Programming):** Mehrere (z.B. 3) unabhängige Teams entwickeln dieselbe Software. Alle Versionen laufen parallel, ein Voter entscheidet (sehr teuer).
* **Dynamisch (Recovery Blocks):** Eine Fehlererkennung (Plausibilisierung) prüft das Ergebnis. Ist es fehlerhaft, wird eine alternative (anders implementierte) Software-Routine ausgeführt.

**83. Warum sind der flexiblen Gestaltung der Software bei ES engere Grenzen gesetzt als bei IT-Systemen?**

* Wegen der harten **nicht-funktionalen Anforderungen**: Strenge Echtzeit-Deadlines, limitierte Ressourcen (Speicher, CPU), hohe Anforderungen an Sicherheit und Verlässlichkeit sowie die enge Verzahnung mit der Hardware (Treiber) schränken die Flexibilität ein.

**84. Was ist bei ES der Unterschied zwischen Plattformsoftware und Applikationssoftware?**

* **Plattformsoftware:** Der **hardwarenahe** und anwendungsunabhängige Teil. Sie stellt Treiber (z.B. für CAN, ADC) und Basisdienste (z.B. Betriebssystem, Scheduling) bereit und abstrahiert die Hardware (z.B. AUTOSAR). Sie hat **keine Semantik** (liefert nur Rohwerte).
* **Applikationssoftware:** Der **hardwareunabhängige** Teil, der die eigentliche Funktion (z.B. Tempomat, Motorsteuerung) implementiert. Hier liegt das Domänenwissen und der Wettbewerbsvorteil. Sie **trägt die Semantik** (weiß, was der Rohwert bedeutet).

---

## Fragen zum Praktikum (Freescale-Videos)

**85. Warum hat das im Praktikum verwendete Board (z.B. MPC560xB) mehrere Taktquellen?**

* Es hat mehrere Quellen für unterschiedliche Zwecke:
    1.  Einen **internen RC-Oszillator (FIRC)** (16 MHz), der als schneller, aber ungenauer Standard-Takt nach dem Reset dient.
    2.  Einen **externen Oszillator (FXOSC)** (4-16 MHz), der als präzise Basis für die PLL dient.
    3.  Low-Power-Oszillatoren (SIRC/SXOSC) für Sleep-Modi.

**86. Was ist der Vorteil des Externen Oszillators (Quarz-Kristall) gegenüber dem Internen RC-Oszillator?**

* Ein externer Oszillator (Kristall) ist signifikant **präziser und stabiler** (weniger Drift durch Temperatur oder Spannung) als ein interner RC-Oszillator. Der RC-Oszillator ist dafür billiger und startet schneller.

**87. Warum ist eine genaue Taktquelle wichtig?**

* Eine genaue Taktquelle (wie ein Kristall) ist unerlässlich für:
    * **Synchrone Kommunikation:** Bussysteme wie CAN oder LIN benötigen exakte Baudraten.
    * **Präzise Zeitmessung:** Alle Timer-Funktionen (EMIOS, PIT) hängen von der Genauigkeit des Taktes ab.
    * **Echtzeit-Verhalten:** Die Einhaltung von Deadlines erfordert eine deterministische Zeitbasis.

**88. Was ist die Phase-Locked Loop (PLL)? Wofür wird sie verwendet?**

* Die **PLL (Phase-Locked Loop)** ist eine Schaltung, die den Takt des externen Oszillators (FXOSC) als Referenz nutzt, um dessen Frequenz mit einem wählbaren Faktor zu **multiplizieren**.
* Sie wird verwendet, um den hohen **Systemtakt (SYSCLK)** zu erzeugen (z.B. 64 MHz aus einem 8 MHz Kristall).

**89. Zu was dient die Clock Monitorung Unit (CMU)?**

* Die **CMU (Clock Monitoring Unit)** **überwacht** die Funktionsfähigkeit der Taktquellen.
* Sie vergleicht Taktquellen miteinander. Bei einer Inkonsistenz (Fehler) kann sie einen **Reset**, einen **Interrupt Request** oder den Übergang in den **SAFE Mode** auslösen.

**90. Warum gibt es beim MPC560xB-Board verschiedene Run Modes?**

* Aus **Energiespargründen**.
* Verschiedene Aufgaben (Tasks) benötigen unterschiedliche Ressourcen (z.B. Taktquellen, Peripherie). Die Run Modes (z.B. RUN0..3, HALT, STOP) erlauben es, nur die Komponenten zu aktivieren, die für die aktuelle Aufgabe benötigt werden, und den Rest abzuschalten (Clock Gating).

**91. Was ist der SAFE-Mode?**

* Der SAFE-Mode ist ein **System-Modus**.
* Bei einem **Hardware-Fehler** (z.B. Ausfall einer Taktquelle erkannt durch die CMU) wechselt die MCU automatisch in diesen Modus.
* In diesem Modus kann Code ausgeführt werden, um den Fehler zu diagnostizieren und das System in einen sicheren Zustand zu bringen.

**92. Warum ist das Cookbook (AN2865) ein wichtiges Dokument für den Entwickler?**

* Das "Qorivva Simple Cookbook" (AN2865) ist wichtig, da es praktische **Code-Beispiele** ("Hello World Programs") für die gängigsten Funktionen und Peripherie-Initialisierungen (wie PLL- und Run-Mode-Konfiguration) enthält.

**93. Für was ist der sogenannte Watch Dog gut?**

* Der Watch Dog (Software Watchdog Timer, SWT) ist eine Sicherheitsfunktion, die nach dem Reset **aktiv** ist.
* Er muss vom laufenden Programm **periodisch bedient** (zurückgesetzt) werden (durch Schreiben von `0xA602` und `0xB480`).
* Wenn das Programm "hängenbleibt" (z.B. in einer Endlosschleife), wird der Watchdog nicht mehr bedient, läuft über und löst einen **Reset** aus, um das System wieder in einen definierten Zustand zu bringen.

**94. Die Abkürzung EMIOS steht für Enhanced Modular Input/Output System. Für was ist das Modul gut?**

* **EMIOS** (Enhanced Modular Input/Output System) ist ein leistungsfähiges Timer-Modul.
* Es stellt Dutzende von Kanälen bereit, um **zeitgesteuerte I/O-Funktionalitäten** (z.B. komplexe PWM-Signale erzeugen oder Input-Flanken exakt messen) **unabhängig von der CPU** zu realisieren.

**95. Nennen Sie 3 Beispiele für mögliche I/O-Funktionalitäten eines EMIOS-Kanals.**
1.  **MCB (Modulus Counter):** Dient als Zähler (Up oder Up/Down), der als (ggf. gemeinsame) Zeitbasis (über einen Counter Bus) für andere Kanäle genutzt werden kann.
2.  **SAIC (Single Action Input Capture):** Erfasst den exakten Zählerstand (Zeitpunkt), zu dem eine Input-Signalflanke (steigend oder fallend) eintritt.
3.  **OPWMB (Output Pulse Width Modulation):** Erzeugt ein PWM-Signal, das auf einer externen Zeitbasis (einem anderen Counter Bus) basiert.

**96. Im Praktikum haben wir die Output-Funktionalität „Pulse Width Modulation Buffered“ verwendet.**

* **Frage 1:** Woraus ergibt sich die Periodenlänge T des PWM-Signals?
    * Im Modus "Pulse Width Modulation Buffered" (OPWMB) wird als Taktquelle ein **externer Modulo-Counter** (ein anderer EMIOS-Kanal, der als MCB konfiguriert ist) verwendet. Dieser Modulo-Counter definiert die feste Periodenlänge des PWM-Signals.
* **Frage 2:** Wie wird der Duty-Cycle tein des PWM-Signals eingestellt?
    * Der Duty-Cycle wird durch zwei Registerwerte innerhalb der Periode frei positioniert:
        * **Register A1** (bzw. UCA[n]) definiert den Startpunkt (z.B. die steigende Flanke).
        * **Register B1** (bzw. UCB[n]) definiert den Endpunkt (z.B. die fallende Flanke).
* **Frage 3:** Wo wurde ein PWM-Signal im Praktikum verwendet?
    * (Typischerweise wird PWM im NXP-Cup-Praktikum für die Ansteuerung der **Motoren** (über die H-Brücke) und des **Lenk-Servos** verwendet.)

**97. Im Praktikum haben wir die Output-Funktionalität „Pulse Width Modulation with Trigger“ verwendet. Zu welchem Zweck wurde diese Output-Funktionalität verwendet?**

* Der Modus **OPWMT** (PWM with Trigger) wird verwendet, um **Ereignisse exakt zu synchronisieren**.
* Er erzeugt nicht nur einen PWM-Puls (über Register A1 und B1), sondern setzt auch zu einem dritten, frei wählbaren Zeitpunkt (definiert durch **Register A2**) ein **FLAG** (einen Trigger).
* Zweck: Dieses Flag kann (z.B. über die CTU) genutzt werden, um eine **A/D-Wandlung zu einem exakten Zeitpunkt** innerhalb des PWM-Zyklus anzustoßen (z.B. zur Strommessung oder zur Synchronisation der Kamera).

**98. Ein EMIOS-Kanal hat auch einen Programmable Input Filter (in Hardware). Für was ist dieser gut?**

* Er dient zur **Entprellung** (Debouncing) von digitalen Eingangssignalen.
* Eine Signalflanke wird erst dann erkannt (weitergegeben), wenn das Signal für eine **programmierbare Anzahl von Clock-Zyklen** (z.B. 2, 4, 8 oder 16 Takte) stabil anliegt.

**99. Was ist ein Interrupt?**

* Ein Interrupt ist eine **asynchrone Unterbrechung** des "normalen" Programmablaufs, die typischerweise durch Hardware (Peripherie) ausgelöst wird.

**100. Wo kommen die Interrupt-Requests einer Applikation i. d. R. her?**

* Von den **Peripherieelementen** (z.B. ADC, EMIOS, PIT oder CAN), wenn diese ein Ereignis melden (z.B. "Wandlung fertig", "Timer abgelaufen", "Nachricht empfangen").

**101. Welche Zuordnung findet im Interrupt Controller statt?**

* Der Interrupt Controller (INTC) ordnet jeder Interrupt-Request-Quelle (IR-Quelle) einen **eigenen IR-Vektor** (die Adresse der zugehörigen Behandlungsroutine/ISR) zu.

**102. Was hat die Verwendung von Interrupt für einen Vorteil?**

* **Effizienz.** Statt die CPU durch "Polling" (ständiges Abfragen, z.B. "Ist die Wandlung fertig?") zu blockieren, kann die CPU andere Aufgaben erledigen oder in einen stromsparenden Modus wechseln. Sie wird nur dann aktiv (unterbrochen), wenn ein Peripherie-Ereignis dies erfordert.

**103. Was ist beim MPC560xB der Unterschied zwischen dem Software Vector Mode und dem Hardware Vector Mode?**

* **Software Vector Mode:**
    * Optimiert für **minimale Code-Größe**.
    * Alle IRs landen in einem gemeinsamen Handler (z.B. IVOR 4). Die Software muss dann manuell (durch Lesen des IACKR-Registers) die genaue Quelle ermitteln und über eine Sprungtabelle zur richtigen ISR springen.
* **Hardware Vector Mode:**
    * Optimiert für **minimale Latenz** (Reaktionszeit).
    * Jede IR-Quelle hat einen **eigenen Vektor** (Einsprungadresse) in der Hardware-Tabelle. Die Hardware springt direkt zur richtigen ISR, ohne dass die Software die Quelle suchen muss.

**104. Was ist beim ADC-Modul der Scan Mode?**

* Der Scan Mode ist eine Konvertierungsoption (im Gegensatz zum "One shot mode").
* Er dient der **periodischen Konvertierung** einer Gruppe (Maske) von Kanälen.

**105. Was macht der sogenannte Programmable Analog Watchdog des ADC-Moduls?**

* Er ermöglicht die Definition eines **Wertebereichs** (eines programmierbaren oberen und unteren Schwellenwerts, THRH und THRL).
* Er überwacht einen ADC-Kanal **ohne CPU-Beteiligung**.
* Wenn der Messwert diesen Bereich verlässt, kann er einen **Interrupt** auslösen.

**106. Was ist die sogenannte Cross Trigger Unit (CTU)?**

* Die **CTU (Cross Trigger Unit)** ist eine Hardware-Verbindungseinheit.
* Sie dient dazu, ein **Timer-Event** (von einem EMIOS-Kanal oder einem PIT) in einen **ADC-Konvertierungs-Trigger** umzuwandeln.
* Dies geschieht **ohne CPU-Beteiligung** und garantiert Synchronizität.

**107. Für was wurde die CTU im Praktikum verwendet?**

* Im Anwendungsbeispiel "Einlesen der analogen Pixelwerte" der **Zeilenkamera (TSL1401)**.
* Ein EMIOS-Kanal (im OPWMT-Modus) erzeugt ein Trigger-Flag, das synchron zum Kamera-Takt (CAM CLK) ist.
* Dieses Flag löst über die CTU bei jedem Takt eine ADC-Wandlung aus, um den analogen Pixelwert einzulesen.

**108. Wie wurde bei unserem Fahrzeug die Belichtungsdauer der Kamera eingestellt?**

* (Basierend auf dem TSL1401-Kamera-Timing):
* Die Belichtungsdauer ("Integration") ist die Zeit, in der die Pixel Licht sammeln.
* Diese Zeit wird durch den **Zeitabstand** zwischen dem **Start-Impuls (SI)** (der die Belichtung startet) und dem **ersten Takt-Impuls (CLK)** (der das Auslesen startet und die Belichtung beendet) gesteuert.
* Im Praktikum wurde dieser Zeitabstand durch die Konfiguration der EMIOS-Timer eingestellt.

**109. Was wurde bei unserem Fahrzeug mit einem SI-Signal alles ausgelöst/beeinflusst?**

* (Basierend auf dem TSL1401-Kamera-Timing):
* Das **SI-Signal** (Serial Input) ist ein einzelner Puls.
* Er löst zwei Dinge aus:
    1.  Er startet den **Belichtungszyklus (Integration)** der 128 Pixel.
    2.  Er startet den **Auslesevorgang** (Vorbereitung zur Ausgabe von Pixel 1 beim nächsten Takt).

**110. Was kann man mit einem DMA-Request erreichen?**

* Einen **Datentransfer (Kopierauftrag)** zwischen Speicher und Peripherie (oder RAM zu RAM) ausführen, **ohne dass die CPU** beteiligt ist.

**111. Was kann man mit DMA (häufig) vermeiden?**

* Eine **CPU-Beteiligung**. Die CPU wird nicht durch Kopierroutinen (z.B. in einer ISR) blockiert und hat Zeit für andere Aufgaben.

**112. Was kann alles einen DMA-Request auslösen?**
1.  **Peripherieelemente** (z.B. ADC-Konvertierung fertig, EMIOS-Event, DSPI-Empfangspuffer voll).
2.  **Software** (durch Setzen eines Bits in einem Register).
3.  Ein **Periodical Interval Timer (PIT)** (für periodische DMA-Transfers).

**113. Welche Möglichkeiten bietet DMA noch mit Bezug auf die Konfiguration von Peripherieelementen?**

* DMA kann Peripherieelemente **automatisch rekonfigurieren**.
* Beispiel: Ein DMA-Transfer (ausgelöst durch ein EMIOS-Event) kann neue Werte (für den nächsten Puls) aus dem RAM direkt in die EMIOS-Register (CADR/CBDR) schreiben.
* Dies ermöglicht **Verkettungen (Chaining)** von Peripherie-Aktionen ohne CPU-Beteiligung.

**114. Was ist das Scatter-Gather Feature des DMA-Moduls?**

* Es erlaubt einem DMA-Kanal, nach Abschluss eines Transfers **automatisch einen neuen Transfer Control Descriptor (TCD)** (der die Parameter für den *nächsten* Transfer enthält) aus dem Speicher zu laden.
* Dies ermöglicht es, Daten von mehreren, nicht zusammenhängenden Quellen zu **sammeln (Gather)** oder Daten an mehrere, nicht zusammenhängende Ziele zu **verteilen (Scatter)**.

**115. Erläutern Sie die Begriffe Regelstrecke, Führungsgröße, Regelgröße, Regelabweichung u. Stellgröße.**

* **Regelstrecke:** Der zu beeinflussende Prozess oder Teil des Systems, der geregelt werden soll (z.B. der Motor, die Heizung).
* **Führungsgröße (w):** Der vorgegebene Wert, den die Regelgröße erreichen soll (der **Soll-Wert**).
* **Regelgröße (x):** Die Ausgangsgröße der Strecke, die gemessen wird (der **Ist-Wert**).
* **Regelabweichung (e):** Die Differenz zwischen Soll- und Ist-Wert ($e = w - x$). Sie ist die Eingangsgröße des Reglers.
* **Stellgröße (y):** Die Ausgangsgröße des Reglers, die auf die Regelstrecke einwirkt, um die Regelabweichung zu korrigieren.

**116. Die Glieder der Regelstrecke werden entsprechend ihrem Zeitverhalten charakterisiert. Wie kann man das Zeitverhalten herausfinden?**

* Indem man die **Sprungantwort** der Regelstrecke aufnimmt.
* Dazu legt man am Eingang der (geöffneten) Strecke ein **Testsignal** (eine sprunghafte Änderung der Eingangsgröße) an und zeichnet die Reaktion (Antwort) am Ausgang auf. Die Form dieser Antwort (z.B. S-förmig) charakterisiert die Strecke.

**117. Nennen Sie 4 unterschiedliche Typen von Übertragungsverhalten. Nenne Sie zu jedem auch ein Beispiel.**
1.  **P-Glied** (Proportional): Ausgang folgt dem Eingang sofort.
    * Beispiel: Hebel, Getriebe, Spannungsteiler.
2.  **I-Glied** (Integrierend): Ausgang ist das Integral des Eingangs (rampt auf).
    * Beispiel: Strom, der einen Kondensator lädt (Eingang: Strom, Ausgang: Spannung).
3.  **$PT_1$-Glied** (Verzögerungsglied 1. Ordnung): Sprung am Eingang führt zu exponentiellem Anstieg am Ausgang.
    * Beispiel: RC-Glied (Spannung), Gleichstrommotor (Eingang: Spannung, Ausgang: Drehzahl).
4.  **$PT_2$-Glied** (Verzögerungsglied 2. Ordnung): Kann schwingen.
    * Beispiel: Mechanischer Schwinger (Feder-Masse-Dämpfer-System), elektrischer RLC-Schwingkreis.

**118. Was ist das Problem beim P-Regler?**

* Er hat eine **bleibende Regelabweichung**. Er wird den Soll-Wert (bei Strecken ohne I-Anteil) nie exakt erreichen; es bleibt immer ein kleiner Fehler bestehen.

**119. Was sind die Eigenschaften eines I-Reglers?**

* Er **summiert die Regelabweichung** über die Zeit auf (Integral).
* **Vorteil:** Er kann die **bleibende Regelabweichung vollständig eliminieren**.
* **Nachteil:** Er ist **langsam** und neigt zum Schwingen (instabil).

**120. Was sind die Vor- und Nachteile eines PD-Reglers?**

* **Vorteile:**
    * Er reagiert auf die *Änderung* der Abweichung (D-Anteil) und ist dadurch **sehr schnell** (er "hält vor").
    * Der D-Anteil wirkt dämpfend und stabilisierend.
* **Nachteile:**
    * Er hat eine **bleibende Regelabweichung** (da der I-Anteil fehlt).
    * Er **verstärkt Rauschen** im Sensorsignal (durch die Differenziation), was zu Unruhe im Stellglied führt.

**121. Welchen Typ von Regler implementieren diese Codezeilen?: `esum = esum + e; y = Kp*e + Ki*Ta*esum;`**

* Dies ist ein **PI-Regler** (Proportional-Integral-Regler).
    * `Kp*e` ist der P-Anteil.
    * `Ki*Ta*esum` ist der I-Anteil (wobei `esum` die Summe $e_i$ ist und $T_a$ die Abtastzeit).

**122. Welchen Typ von Regler implementieren diese Codezeilen?: `y = Kp*e + Kd*(e - ealt)/Ta; ealt = e;`**

* Dies ist ein **PD-Regler** (Proportional-Differential-Regler).
    * `Kp*e` ist der P-Anteil.
    * `Kd*(e - ealt)/Ta` ist der D-Anteil (genähert durch die Differenz zum "alten e" geteilt durch die Abtastzeit $T_a$).

**123. In welchen (2) Fällen reicht für einfache Regelaufgaben ein einfacher P-Regler aus?**

1.  Wenn die **bleibende Regelabweichung** klein genug ist und toleriert (vernachlässigt) werden kann.
2.  Wenn die **Regelstrecke selbst bereits einen I-Anteil besitzt** (z.B. Regelung der Position bei einem Motor, der über die Geschwindigkeit gestellt wird).

**124. Welche Vorteile haben digitale Regler?**

* Sie arbeiten **driftfrei** (im Gegensatz zu analogen Bauteilen, die altern oder temperaturabhängig sind).
* Es lassen sich komplexe, **nichtlineare oder adaptive Regler** leichter realisieren.
* Der Regler kann bei Bedarf einfach per **Software neu konfiguriert** und parametriert werden.

**125. Nennen Sie 3 prinzipielle Vorgehensweisen, wie man die Reglerparameter eines PID-Reglers ermitteln kann.**

1.  **Empirisches Einstellen** (systematisches Probieren/Tuning von $K_p$, $K_i$, $K_d$ an der realen Strecke).
2.  Verwendung von **Einstellregeln** (z.B. nach Ziegler/Nichols):
    * *Schwingungsmethode:* $K_p$ wird bis zur Stabilitätsgrenze (Dauerschwingung) erhöht ($K_{pkrit}$, $T_{krit}$).
    * *Sprungantwort-Methode:* Aufnahme der Sprungantwort (Ermittlung von $T_u$ und $T_g$).
3.  **Physikalische Modellierung:** Mathematisches Modell der Strecke erstellen und die Reglerparameter in der **Simulation** optimieren.

**126. Wann kann ein digitaler Regler wie ein analoger Regler parametrisiert/dimensioniert werden?**

* Wenn die **Abtastzeit ($T_a$) sehr viel kleiner** ist (z.B. Faktor 10-20) als die dominierende Zeitkonstante der Regelstrecke.
* In diesem Fall verhält sich das System **"quasi-kontinuierlich"** und die Effekte der digitalen Abtastung können vernachlässigt werden.