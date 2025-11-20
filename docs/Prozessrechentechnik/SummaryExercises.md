## 1. Überblick: Automotive MCUs

Das Dokument gibt einen Überblick über das 32-bit PowerPC Automotive Mikrocontroller (MCU) Portfolio von Freescale, sortiert nach Anwendungsbereichen wie **Powertrain**, **Chassis & Safety**, **Body & Gateways** sowie **Kommunikation** (CAN, LIN, FlexRay).

Zwei MCUs werden exemplarisch detaillierter vorgestellt:
* **MPC5604B:** Basiert auf dem **Power Architecture e200z0 Core** (48-64MHz), ausgestattet mit 512KB Flash, 48K SRAM, 3 FlexCAN-Modulen, 4 LINFlex-Modulen und einem 36-Kanal 10-bit ADC.
* **MPC5607B:** Ein größerer Bruder mit 1.5MB Flash, 96K SRAM, einem 16-Kanal DMA, 6 FlexCAN, 10 LINFlex und einem 52-Kanal ADC (kombiniert 10-bit und 12-bit Kanäle).

---

## 2. Byte-Reihenfolge (Endianness)

Die PowerPC-Architektur verwendet von Natur aus die **Big Endian** Byte-Ordnung. Das bedeutet, das signifikanteste Byte (Most Significant Byte, MSb) wird an der niedrigsten Speicheradresse abgelegt.

---

## 3. SIUL (System Integration Unit Lite)

Die SIUL ist eine zentrale "Glue Logic"-Einheit, die die Konfiguration und das Multiplexing (IOMux) der Pins steuert.

* **Funktionen:**
  * **Pad Control:** Konfiguriert die elektrischen Parameter jedes Pins (z.B. Output Buffer, Open Drain, Pull-up/Pull-down).
  * **IOMux:** Weist den Pins Signale zu. Jedem Pin können mehrere Funktionen (Alternate Functions, z.B. AF0-AF3) zugewiesen werden.
  * **GPIO:** Ermöglicht die Nutzung von Pins als allgemeine digitale Ein- oder Ausgänge.
  * **External Interrupt Management:** Verwaltet externe Interrupt-Signale, inklusive digitaler Glitch-Filter.
* **Wichtige Register:**
  * **PCR (Pad Configuration Register):** Konfiguriert jeden Pin individuell. Wichtige Felder sind:
    * `PA` (Pad Assignment): Wählt die Alternate Function (z.B. GPIO, CAN, EMIOS) für den Pin.
    * `OBE` (Output Buffer Enable): Aktiviert den Pin als Ausgang.
    * `IBE` (Input Buffer Enable): Aktiviert den Pin als Eingang.
    * `WPE` / `WPS`: Aktivieren und wählen eines Weak Pull-Up oder Pull-Down Widerstands.
  * **PSMI (Pad Select Multiplexed Inputs):** Wählt bei Peripherie-Eingängen, die mit mehreren Pins verbunden sind, aus, welcher Pin tatsächlich als Quelle genutzt wird.

---

## 4. Clocks (Taktquellen)

Das System-Timing ist hochkonfigurierbar und essenziell für das Power-Management.

* **Taktquellen:**
  * **FIRC (16 MHz Internal RC):** Der interne RC-Oszillator. Dies ist der **Standard-Takt** nach einem Reset.
  * **FXOSC (4-16 MHz External):** Ein externer Kristall/Oszillator (im Praktikum 8 MHz).
  * **FMPLL (Phase Lock Loop):** Multipliziert eine Eingangsfrequenz (meist FXOSC), um den Hochgeschwindigkeits-Systemtakt (z.B. 64 MHz) zu erzeugen.
    * **Formel:** $FMPLL = \frac{FXOSC \cdot NDIV}{IDF \cdot ODF}$
  * **Low Power Quellen:** SIRC (128 KHz) und SXOSC (32 KHz) für RTC (Real-Time Clock) und Watchdog im Sleep-Modus.
* **CMU (Clock Monitoring Unit):** Überwacht die Takte auf Konsistenz (z.B. Vergleich FIRC mit FXOSC). Bei Fehlern kann die CMU einen Reset, einen Interrupt oder den Übergang in den `SAFE` Mode auslösen.
* **CGM (Clock Generation Module) Struktur:**
  * Der **System Clock Selector (ME)** wählt die Hauptquelle für die `SYSCLK` (FIRC, FXOSC oder FMPLL).
  * Diese `SYSCLK` wird auf den Core und auf 3 "Peripheral Sets" verteilt.
  * Der Takt für jedes Peripherie-Set kann durch einen eigenen Teiler (1-16) im `CGM_SC_DCx`-Register verlangsamt werden, um Energie zu sparen.
* **CLKOUT:** Ein ausgewählter Takt (FIRC, FXOSC, FMPLL) kann zur Überprüfung auf einen externen Pin (GPIO[0]) ausgegeben werden.

---

## 5. Run Modes (Betriebsmodi)

Die Run Modes sind das Kernkonzept des Power-Managements. Sie definieren, welche Systemkomponenten (Takte, Peripherie, Flash) aktiv sind.

* **Modi-Typen:**
  * **System Modes:** `RESET`, `DRUN` (Default Run), `SAFE`, `TEST`.
  * **User Modes:** `RUN0`...`RUN3` (normale Betriebsmodi), `HALT`, `STOP`, `STANDBY` (Low-Power-Modi).
* **Ablauf:** Nach einem Reset startet der MCU im `DRUN`-Modus. In diesem Modus wird typischerweise die Konfiguration für die User Modes (z.B. `RUN0`) vorgenommen.
* **Konfiguration:**
  * **`ME_xxx_MC` Register:** Für jeden Modus (z.B. `ME_RUN0_MC`) gibt es ein Konfigurationsregister. Dieses legt fest:
    * Welche Taktquellen aktiv sind (`PLLON`, `OSCON`, `IRCON`).
    * Welche Quelle für die `SYSCLK` verwendet wird.
    * Ob das Flash (`CFLAON`, `DFLAON`) oder der Spannungsregler (`MVRON`) aktiv sind.
* **Peripheral Clock Gating:** Das Aktivieren von Takten für Peripheriegeräte ist ein zweistufiger Prozess:
  1.  **`ME_RUN_PCx` (Peripheral Configuration):** 8 Register (`PC0`...`PC7`) definieren 8 "Policies", die festlegen, in welchen Modi (RUN0, RUN1, DRUN...) eine Policy aktiv ist.
  2.  **`ME_PCTLx` (Peripheral Control):** Für *jedes* Peripheriegerät (z.B. `PCTL[68]` für SIUL) gibt es ein Register, das eine der 8 Policies (`PC0`...`PC7`) auswählt.
* **Mode-Übergang (Transition):**
  * Ein Wechsel (z.B. von `DRUN` zu `RUN0`) wird durch Schreiben eines Schlüssels in das `ME_MCTL.R`-Register eingeleitet.
  * Das System **muss** danach warten, bis der Übergang abgeschlossen ist (z.B. durch Polling des `ME.GS.B.S_MTRANS`-Bits), da Taktquellen (insb. die PLL) Zeit zum Einschwingen benötigen.

---

## 6. Timed I/O (Zeitgesteuerte Ein-/Ausgabe)

Dieser Abschnitt umfasst den Watchdog, den PIT und das extrem wichtige EMIOS-Modul.

* **Watch Dog (SWT):** Ist nach dem Reset standardmäßig aktiv. Er muss entweder periodisch "bedient" (durch Schreiben von `0xA602` und `0xB480` in `SWT_SR`) oder explizit deaktiviert werden, um einen Reset zu verhindern.
* **PIT (Periodical Interrupt Timer):** Stellt 32-bit-Zähler bereit, die vom Systemtakt getrieben werden. Sie sind voneinander unabhängig und können Interrupts, DMA-Anfragen oder ADC-Konvertierungen (direkt oder via CTU) auslösen.
* **EMIOS (Enhanced Modular Input/Output System):** Ein leistungsfähiges, CPU-unabhängiges Timer-Modul zur Erzeugung und Messung von zeitbasierten Signalen.
  * **Struktur:** Besteht aus "Unified Channels". Jeder Kanal kann für eine spezifische Funktion konfiguriert werden. Die Taktung wird von der `SYSCLK` abgeleitet und kann mehrfach geteilt werden (Common Divider $\to$ Global Prescaler $\to$ Channel Prescaler).
  * **Counter Buses:** 5 interne Busse (A-E) erlauben es, einen Kanal als Zähler (Zeitbasis) zu konfigurieren und dieses Signal an andere Kanäle im selben Modul zu verteilen (z.B. Ch 23 über Bus A an alle).
  * **Doppelte Pufferung (Double Buffering):** Die Register A und B (die Zeitpunkte oder Schwellen definieren) sind doppelt gepuffert (A1/A2, B1/B2). Dies ermöglicht "sichere" Updates: Ein neuer Wert wird in A2 geschrieben, wird aber erst zu Beginn des *nächsten* Zyklus in A1 (das aktive Register) übernommen.

* **Wichtige EMIOS-Modi:**
  * **Counter-Modi:**
    * `MCB` (Modulus Counter Buffered): Ein Zähler, der bis zum Wert in Register A1 zählt und dann zurückgesetzt wird. Dient oft als Zeitbasis für andere Kanäle.
  * **Input-Modi:**
    * `SAIC` (Single Action Input Capture): Bei einer definierten Signalflanke (steigend/fallend) wird der aktuelle Zählerstand im Register A2 gespeichert und ein Flag gesetzt.
    * `IPWM` (Input Pulse Width Measurement): Misst die Pulsbreite. Speichert den Zählerstand der führenden Flanke in B2 und den der folgenden Flanke in A2. Die Software berechnet die Differenz (`A2 - B1`).
    * `IPM` (Input Period Measurement): Ähnlich wie IPWM, misst aber die Zeit zwischen zwei Flanken gleicher Richtung (z.B. steigend zu steigend).
  * **Output-Modi:**
    * `DAOC` (Double Action Output Compare): Erzeugt einen Puls. Bei Erreichen von A1 wird die führende Flanke, bei Erreichen von B1 die folgende Flanke ausgelöst.
    * `OPWMB` (Output Pulse Width Modulation Buffered): Nutzt eine *externe* Zeitbasis (von einem MCB-Kanal). A1 und B1 definieren die führende und folgende Flanke des PWM-Pulses innerhalb dieser Periode.
    * **`OPWMT` (OPWM with Trigger):** Der wichtigste Modus für den Freescale Cup. Wie OPWMB, fügt aber einen dritten Zeitpunkt (Register A2) hinzu. Wenn der Zähler A2 erreicht, wird ein **FLAG** gesetzt. Dieses Flag wird genutzt, um die **CTU** (und damit den ADC) zu einem exakten Zeitpunkt *innerhalb* des PWM-Pulses zu triggern.
* **EMIOS Input Filter:** Ein digitaler Filter (5-bit Zähler), der Eingangssignale "entprellt". Ein Signal wird erst als geändert erkannt, wenn es für eine definierte Anzahl von Takten (z.B. 2, 4, 8 oder 16) stabil anliegt.

---

## 7. Interrupts (INTC)

Der Interrupt Controller (INTC) verwaltet Peripherie-Interrupts.

* **Core vs. Peripherie:** Der CPU-Core hat eigene Exceptions (z.B. Machine Check). Alle Interrupts von Peripheriegeräten (ADC, CAN, EMIOS, PIT etc.) werden vom INTC verwaltet und an den Core über die **"External Input Exception" (IVOR 4)** gemeldet.
* **Verhalten (Ablauf):** Bei einem Interrupt sichert die Hardware automatisch den Befehlszähler (in `SRR0`) und das Maschinenstatusregister (in `SRR1`). Der Programmzeiger springt zur Vektoradresse. Die Interrupt-Service-Routine (ISR) wird ausgeführt. Das `rfi` (Return from Interrupt) Kommando am Ende stellt `SRR0` und `SRR1` wieder her.
* **Handshaking-Modi:**
  * **Software Vector Mode:** (Standard) Alle INTC-Interrupts landen im selben Handler (IVOR 4). Die Software muss dann das `IACKR`-Register des INTC lesen, um die *eigentliche* Quelle (z.B. PIT-Kanal 2) zu identifizieren und über eine Sprungtabelle zur richtigen ISR zu springen. Optimiert für Codegröße.
  * **Hardware Vector Mode:** Jeder Interrupt-Quelle wird ein eigener Vektor zugewiesen, der direkt zur ISR springt. Optimiert für Latenz.
* **Prioritäten:**
  * Es gibt 16 Prioritätsstufen (15 = höchste, 0 = niedrigste, wird nie erkannt).
  * Jede IR-Quelle erhält eine Priorität im `INTC_PSRx`-Register.
  * Das **`INTC_CPR` (Current Priority Register)** speichert die Priorität der *aktuell laufenden* ISR. Nur Interrupts mit einer *höheren* Priorität als der im `INTC_CPR` können diese unterbrechen (Preemption).
  * **WICHTIG:** Nach einem Reset steht das `INTC_CPR` auf 15 (höchste Priorität). Das bedeutet, **alle** Interrupts sind maskiert. Um Interrupts zu aktivieren, muss das `INTC_CPR` manuell auf 0 (oder eine andere Basispriorität) gesetzt werden.

---

## 8. ADC und CTU (Analog-Digital-Converter & Cross Trigger Unit)

* **ADC:** Wandelt analoge Spannungen (0-5V) in digitale Werte um. Der MPC5607B hat sowohl 10-bit als auch präzisere 12-bit Kanäle. Jeder Kanal hat ein eigenes Datenregister (`CDR`), das den Wert (`CDATA`) und Statusbits (`VALID`, `OVERWrite`) enthält.
* **Trigger-Optionen:** Eine ADC-Wandlung kann auf drei Arten ausgelöst werden, die sich gegenseitig unterbrechen (präemptiv):
  1.  **Normal Conversion:** (Niedrigste Priorität) Ausgelöst durch Software (Setzen des `NSTART`-Bits).
  2.  **Injected Conversion:** (Mittlere Priorität) Ausgelöst durch Software (`JSTART`-Bit) oder `PIT2`. Unterbricht eine laufende "Normal"-Kette.
  3.  **CTU (Cross Trigger Unit):** (Höchste Priorität) Ausgelöst durch `PIT3`, `PIT7` oder `EMIOS`-Kanäle. Unterbricht "Normal" und "Injected".
* **Analog Watchdog:** Ermöglicht eine CPU-unabhängige Bereichsüberwachung (`THRL`, `THRH`) eines Analogkanals und kann bei Verletzung einen Interrupt auslösen.
* **CTU (Cross Trigger Unit):**
  * Die CTU ist die **Hardware-Verbindung** zwischen den Timern (EMIOS, PIT) und dem ADC.
  * Sie ermöglicht es, eine ADC-Wandlung **ohne CPU-Beteiligung** und mit exaktem Timing durch ein Timer-Ereignis auszulösen.
* **Anwendungsbeispiele:**
  1.  **Induktivitätsmessung:** Ein EMIOS-Kanal im `OPWMT`-Modus schaltet einen PWM-Puls (Match A1, Match B1). Ein dritter Zeitpunkt (Match A2) ist so gesetzt, dass der Einschwingstrom (Inrush Current) der Spule abgeklungen ist. Dieser A2-Match triggert über die CTU die ADC-Messung zum exakt richtigen Zeitpunkt.
  2.  **Zeilenkamera (TSL1401):** Die Kamera benötigt ein Start-Impuls (SI) und einen Takt (CLK) und liefert pro Takt einen analogen Pixelwert (AO). EMIOS-Kanäle erzeugen CPU-unabhängig die SI- und CLK-Signale. Der EMIOS-Kanal, der den CLK erzeugt, ist im `OPWMT`-Modus und triggert (via Match A2) über die CTU bei jeder Taktflanke eine ADC-Wandlung, um den analogen Pixelwert einzulesen.

---

## 9. DMA (Direct Memory Access)

DMA ermöglicht Datentransfers zwischen Peripherie und Speicher (oder Peripherie zu Peripherie) **ohne CPU-Beteiligung**.

* **TCD (Transfer Control Descriptor):** Das "Gehirn" jedes DMA-Kanals. Definiert die Quelle (`saddr`), das Ziel (`daddr`), die Transfergröße (`ssize`, `dsize`), die Anzahl der Bytes pro Request (`nbytes`, minor loop) und die Gesamtzahl der Requests (`citer`, major loop).
* **DMA Mux:** Ein Multiplexer verbindet die 16 DMA-Kanäle mit Dutzenden von möglichen Anforderungs-Quellen (DSPI, eMIOS, ADC, IIC oder "Always Enabled" für PIT/Software-Trigger).
* **Features:**
  * **Modulo:** Nützlich für **Ringpuffer (Circular Buffers)**. Ermöglicht das automatische "Umbrechen" (Wraparound) der Quell- oder Zieladresse, indem nur die unteren Adressbits inkrementiert werden.
  * **Scatter-Gather:** Ermöglicht das Verketten von TCDs. Ein TCD kann nach Abschluss die Adresse eines *neuen* TCDs (gespeichert in `sga`) laden und diesen aktivieren. Dies erlaubt komplexe Sequenzen.
  * **Channel Linking:** Ein DMA-Kanal kann nach Abschluss (minor oder major loop) einen *anderen* DMA-Kanal starten.
* **Arbitrierung:** Die DMA-Kanäle haben eine feste Priorität (Fixed-Priority Arbitration), um zu entscheiden, welcher Kanal bei gleichzeitigen Anfragen den Buszugriff erhält.
* **Beispiele:**
  1.  **Wellenform erfassen (EMIOS $\to$ RAM):** Ein EMIOS-Kanal (im IPWM-Modus) misst Pulsbreiten. Jede Messung (z.B. fallende Flanke) löst einen DMA-Request aus. Der DMA-Kanal liest die Zeitstempel aus den EMIOS-Registern (`CADR`, `CBDR`) und schreibt sie in einen Puffer im RAM. Wenn der Puffer voll ist (major loop complete), wird ein *einziger* Interrupt (`INT_MAJ`) ausgelöst, damit die CPU die gesammelten Daten verarbeiten kann.
  2.  **Wellenform generieren (RAM $\to$ EMIOS):** Ein Array im RAM enthält eine Sequenz von Zeitstempeln. Ein EMIOS-Kanal ist im `DAOC`-Modus. Ein DMA-Request (ausgelöst durch den *Abschluss* des *vorherigen* Pulses) kopiert das *nächste* Zeitstempel-Paar aus dem RAM in die EMIOS-Register (`CADR`, `CBDR`). Dies erzeugt eine komplexe, vordefinierte Wellenform komplett ohne CPU-Last.

---

## 10. Regelungstechnik (Control Systems)

Der letzte Abschnitt behandelt die Grundlagen der digitalen Regelung.

* **Grundlagen:**
  * **Steuern (Open-loop):** Ein Prozess ohne Rückkopplung.
  * **Regeln (Closed-loop):** Ein Prozess mit Rückkopplung in einem geschlossenen **Regelkreis**. Der Kreis besteht aus den Schritten: **Messen** (des Istwerts), **Vergleichen** (mit dem Sollwert), **Stellen** (Anpassen der Stellgröße).
* **Begriffe:**
  * `w`: Führungsgröße (Sollwert)
  * `x`: Regelgröße (Istwert)
  * `e`: Regelabweichung ($e = w - x$)
  * `y`: Stellgröße (Ausgang des Reglers)
  * `z`: Störgröße
  * **Regelstrecke:** Der zu regelnde Prozess (z.B. Motor, Heizung).
* **Streckentypen:** Das Verhalten einer Regelstrecke wird durch ihre **Sprungantwort** (Reaktion auf einen Eingangssprung) charakterisiert. Gängige Typen sind:
  * **P-Glied:** Proportionale, sofortige Reaktion. $G(s) = K$
  * **I-Glied:** Integrierend, Ausgang rampenförmig. $G(s) = K/s$
  * **$PT_1$-Glied:** Verzögerung 1. Ordnung (z.B. RC-Glied, DC-Motor). $G(s) = \frac{K}{1+Ts}$
  * **$PT_2$-Glied:** Verzögerung 2. Ordnung (kann schwingen, z.B. Feder-Masse-System). $G(s) = \frac{K}{1+\frac{2D}{\omega_0}s+\frac{1}{\omega_0^2}s^2}$
  * **$PT_t$-Glied:** Totzeit (reine Laufzeitverzögerung). $G(s) = e^{-T_t s}$
* **Reglertypen:**
  * **P-Regler:** $y(t) = K_p \cdot e(t)$. Schnell, hat aber eine **bleibende Regelabweichung**.
  * **I-Regler:** $y(t) = K_i \int e(\tau)d\tau$. Langsam, aber **eliminiert die bleibende Regelabweichung**.
  * **PI-Regler:** $y(t) = K_p \cdot e(t) + K_i \int e(\tau)d\tau$. Mittelschnell, keine bleibende Abweichung.
  * **PD-Regler:** $y(t) = K_p \cdot e(t) + K_d \frac{de(t)}{dt}$. Sehr schnell (D-Anteil "prognostiziert"), aber empfindlich gegen Rauschen und hat eine bleibende Abweichung.
  * **PID-Regler:** Universell. Kombiniert die Vorteile aller Typen (schnell und genau).
    
  $$y(t) = K_p \cdot e(t) + K_i \int e(\tau)d\tau + K_d \frac{de(t)}{dt}$$

* **Digitale Realisierung (PID):**
  * Ein digitaler Regler benötigt einen ADU (ADC) zum Messen und einen DAU (z.B. PWM über EMIOS) zum Stellen.
  * Die Differentialgleichung des PID-Reglers wird in eine zeitdiskrete **Differenzengleichung** (Stellungs-Algorithmus) umgerechnet, die periodisch (mit Abtastzeit $T_a$) berechnet wird:
  
  $$y_k = K_p \cdot e_k + K_i \cdot T_a \sum_{i=0}^{k} e_i + \frac{K_d}{T_a} (e_k - e_{k-1})$$
  
  * *Achtung:* Der I-Anteil (Summe) muss gegen Überlauf (**Windup-Effekt**) begrenzt werden.
* **Regler-Dimensionierung (Tuning):**
  1.  **Empirisches Einstellen:** Manuelles "Herantasten" (z.B. erst $K_p$ erhöhen bis es schwingt, dann $K_i$ für Genauigkeit, dann $K_d$ für Stabilität).
  2.  **Einstellregeln nach Ziegler/Nichols (Schwingungsmethode):** $K_i$ und $K_d$ auf 0 setzen. $K_p$ so lange erhöhen, bis die Strecke dauerhaft schwingt (Stabilitätsgrenze). Aus diesem **$K_{pkrit}$** und der Schwingungsperiode **$T_{krit}$** werden die PID-Parameter über eine Tabelle berechnet.
  3.  **Einstellregeln nach Ziegler/Nichols (Sprungantwort):** Den Regelkreis öffnen und eine S-förmige Sprungantwort aufnehmen. Aus der Wendetangente die Verzugszeit **$T_u$** (Verzögerung) und die Ausgleichszeit **$T_g$** (Anstieg) sowie die Streckenverstärkung **$K_s$** ermitteln und die Parameter über eine Tabelle berechnen.