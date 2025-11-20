## Kapitel 1 (Einführung)

### 1. Einführung

- [ ] Compiler vs Interpreter
- [ ] Sprachimplementierung
- [ ] Anforderungen an Compiler
- [ ] Aufbau
  - [ ] Übersetzungsschritte
  - [ ] Compilerphasen
- [ ] Two-Pass Compiler
- [ ] Compilerbau Werkzeuge

## Kapitel 2 (Lexikalische Analyse)

### 2. Lexikalische Analyse:

- [ ] Kontextfreie Grammatiken
- [ ] Parsebaum (konkreter Syntaxbaum)
- [ ] Abstrakter Syntaxbaum
- [ ] Generelle Prinzipien (Terminale/Token, nextToken, Fehlerbehandlung, Maximal Munch...)
- [ ] Regex?
- [ ] Übergangsdiagramme
- [ ] Regex zu NFA (McNaughthon-Yamada-Thompson Algorithmus)
- [ ] DFA und NFA
- [ ] NFA in DFA Übersetzen (Büchi-Algorithmus)
- [ ] DFA zu Tabellen getriebener Implementierung

## Kapitel 3 (Syntaktische Analyse)

### 3. Syntaktische Analyse

- [ ] Parser Typen
  - [ ] Top-Down
    - [ ] Rekursiver Abstieg (Links/Rechts Rekursiv)
  - [ ] Bottom-Up
    - [ ] Prädikative Parser
    - [ ] LL(1)
    - [ ] Faktorisierung (Links/Rechts)
    - [ ] First und Follow Mengen
- [ ] Kontextfreie Grammatiken (CFG)
- [ ] Ableitungen (Links/Rechtsseitig)
- [ ] Eindeutige Grammatiken

### 4. Syntaktische Analyse (Buttom-Up Parsing)

- [ ] Bottom-Up Parsing
  - [ ] Reduktion
    - [ ] Shift Reduce
  - [ ] Handles
  - [ ] LR-Parsen, LR(0) und SLR
  - [ ] Closure

### 5. Syntaktische Analyse (Fortgeschrittene Parsing Methoden)

- [ ] LALR Parsing und LR(1)

### 6. Syntaktische Analyse (Cup)

- [ ] Java Cup
  - [ ] Deklaration terminale und Nichtterminale
  - [ ] Precedence Declaration
  - [ ] Gramatikregeln

## Kapitel 4 (Semantische Analyse)

### 7. Semantische Analyse

- [ ] Symboltabelle
  - [ ] Implementierung
  - [ ] Allgemein
  - [ ] Liste von Hashtabellen
  - [ ] Hashtabellen von Listen
  - [ ] Operationen
- [ ] Gültigkeit
  - [ ] Gültigkeitsregeln
  - [ ] Dynamsiche Gültigkeitsbereiche
  - [ ] Statische Gültigkeitsbereiche
- [ ] Typen
  - [ ] Typechecking
  - [ ] Typregeln
  - [ ] Typinferenz
