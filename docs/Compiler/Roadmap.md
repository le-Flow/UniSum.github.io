## Kapitel 1 (Einführung)

### 1. Einführung

- [X] [Compiler vs Interpreter](Vorlesung/1.%20Einführung.md#compiler-vs-interpreter)
- [X] [Sprachimplementierung](Vorlesung/1.%20Einführung.md#sprachimplementierung)
- [X] [Anforderungen an Compiler](Vorlesung/1.%20Einführung.md#anforderungen-an-compiler)
- [X] [Aufbau](Vorlesung/1.%20Einführung.md#aufbau)
  - [X] [Übersetzungsschritte](Vorlesung/1.%20Einführung.md#ubersetzungsschritte)
  - [X] [Compilerphasen](Vorlesung/1.%20Einführung.md#compilerphasen)
- [X] [Two-Pass Compiler](Vorlesung/1.%20Einführung.md#two-pass-compiler)
- [X] [Compilerbau Werkzeuge](Vorlesung/1.%20Einführung.md#compilerbau-werkzeuge)

## Kapitel 2 (Lexikalische Analyse)

### 2. Lexikalische Analyse:

- [x] Kontextfreie Grammatiken
- [x] Parsebaum
  - [x] konkreter Syntaxbaum
  - [x] Abstrakter Syntaxbaum
- [x] Lexer
- [x] Jflex (Regex etc)
- [ ] Übergangsdiagramme
- [ ] Regex zu NFA (McNaughthon-Yamada-Thompson Algorithmus)
- [ ] DFA und NFA
- [ ] NFA in DFA Übersetzen (Büchi-Algorithmus)
- [ ] DFA zu Tabellen getriebener Implementierung
- TODO: Kapitel 3.3 + Übungen 3.3.2 und 3.3.5

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
