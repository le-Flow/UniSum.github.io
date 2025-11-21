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

- [x] [Kontextfreie Grammatiken](Vorlesung/2.%20Lexikalische%20Analyse.md#kontextfreie-grammatiken)
- [x] [Parsebaum](Vorlesung/2.%20Lexikalische%20Analyse.md#parsebäume)
  - [x] [konkreter Syntaxbaum](Vorlesung/2.%20Lexikalische%20Analyse.md#konkreter-syntaxbaum-parsebaum)
  - [x] [Abstrakter Syntaxbaum](Vorlesung/2.%20Lexikalische%20Analyse.md#abstrakter-syntaxbaum-ast)
- [x] [Lexer](Vorlesung/2.%20Lexikalische%20Analyse.md#lexer)
- [x] [Jflex (Regex etc)](Vorlesung/2.%20Lexikalische%20Analyse.md#jflex)
- [x] [Tokenerkennung](Vorlesung/2.%20Lexikalische%20Analyse.md#tokenerkennung)
  - [x] [Übergangsdiagramme](Vorlesung/2.%20Lexikalische%20Analyse.md#übergangsdiagramme-endliche-automaten)
- [x] [Automaten](Vorlesung/2.%20Lexikalische%20Analyse.md#automaten)
  - [x] [DFA zu Tabellen getriebener Implementierung](Vorlesung/2.%20Lexikalische%20Analyse.md#tabellengetriebener-ansatz)
  - [x] [Automaten (DFA und NFA)](Vorlesung/2.%20Lexikalische%20Analyse.md#automaten)
  - [x] [NFA in DFA Übersetzen (Büchi-Algorithmus)](Vorlesung/2.%20Lexikalische%20Analyse.md#nfa-zu-dfa-buchi-algorithmus)
  - [x] [Regex zu NFA (McNaughthon-Yamada-Thompson Algorithmus)](Vorlesung/2.%20Lexikalische%20Analyse.md#regex-zu-nfa-yamada-thompson)
  - [x] [Effizienz](Vorlesung/2.%20Lexikalische%20Analyse.md#effizienz)
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
