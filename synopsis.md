# Spick

- DEA = NEA C Det KA C Nondet KA

# Grundlagen

- Alphabet Sigma: Menge von Zeichen
  - Sigma*: Menge aller endlichen Wörter, Sigma+ = Sigma* \ {epsilon}
- Wort: w = x1x2...xn, xi in Sigma
- Teilwort, Anfangsstück, Endstück, Spiegelbild
- A, B Teilmenge Sigma. AB = { uv: u in A, v in B, foreach u, v }
- |u|_M = Anzahl Vorkommnisse d Elemente aus M in u
- Sigma++ = Sigma+
- (A U B)* = (A* B)* A*

# Endliche Automaten

- Drei Komponenten: Eingabe, Zustandsraum, Ausgabe

## DEA (Deterministichser Endlicher Automat)

- Q: Zustandsmenge, Sigma: Eingabealphabet, q0 (in Sigma): Anfangszustand, Delta (Q, Sigma -> Q): Transitionsfunktion, F (Teilmenge Q) Endzustände.
- Delta-*: Transitionsfunktion für ganze Wörter. (Verkettung von Delta)
- Von DEA akzeptierte Sprache: Menger aller Wörter (aus geg Alphabet), die der DEA akzpetiert (dh in einem Endzustand endet)
- Limitation: Endliche Zustände -> Können 'nicht bel weit zählen'.
  - zB: Sprache ist Menge aller Wörter mit gleich vielen '0' wie '1'. => Nicht DEA-akzeptierbar.

## NEA

- Analog DEA, aber:
  - Phi (Q, Sigma -> P(Q)): Transitionsfunktion
  - Phi*: Analog DEA, Ausgabe ist Menge möglicher Zustände
  - Für gegebenen Input keinen, oder mehrere, Übergänge ab gegebenem Zustand q.

## NEA - DEA

- Äquivalent
- NEA n Zustände -> Äquivalenter minimaler DEA max 2^n Zustände

## Minimierung von DEAs

- Unerreichbare Zustände eliminieren
- Finde und eliminiere äquivalente Zustände: Von ihnen ausgehend dieselben Wörter akzeptiert
  - Markiere alle Paare {p, q} von Zuständen mit (p in F & Q not in F) or (p not in F & q in F)
  - Loop:
    - Markiere alle Paare {p, q}, für welche a in Sigma exisiert, so dass {delta(p, a), delta(q, a)} markiert ist.

## Epsilon-Automaten

- NEA erweitern: Zustandswechsel *ohne* Zeichen einzulesen (Epsilon)

### Epsilon-Abschluss

- CL_A(q): Menge aller Zustände, die von q erreicht werden können, unter Einlesen von exklusiv Epsilon (nichts)
- phi#(q, u): Zustände, welche von q, mittels einlesen von u, erreicht werden
  - Epsilon-Automat akzpetiert u, falls phi#(q, u) Schnitt F != leer (dh in Endzustand)

### Äquivalenz zu NEAs / DEA

- Für jeden Epsilon-Automaten E gibt es einen NEA B mit L(A) = L(B)
  - Daraus folgt: Auch äquivalent zu DEA

## Mealy-Maschinen

- A = (Q, Sigma, Delta, q0, delta, gamma)
  - Zustandsmenge, Eingebealphabet, Ausgabealphabet, Anfangszustand, Transitionsfunktion, Ausgabefunktion
  - gamma: Q x Sigma -> Delta

- Kopf liest Zeichen, schreibt ein Zeichen
- Bewegung Lese/Schreibkopf strikt Links -> Rechts
- Keine Endzustände -> Ziel ist erzeugen der Ausgabe!
- lambda*(q0, u): Ausgabefolge zu Eingabewort u

## Moore-Maschine

- A = (P, Sigma, Delta, p0, gamma, mu)
  - ZustandsM, EingabeA, AusgabeA, AnfangsZ, Transitionsfkt, Ausgabefkt
  - mu: P -> Delta

- Unterschied zu Mealy: Eingelesenes Zeichen ist irrelevant für Ausgabe

- Äquivalent zu Mealy
- Jeder DEA ist Spezialfall einer Moore-Maschine!

# Nicht-endliche Automaten

- Erinnere: Sprache L = {0^i 1^i, i in N} (dh Wörter mit gleich vielen 0 wie 1) ist nicht DEA-akzeptierbar.
  - Grund: Zu wenig Speicher

## Kellerautomat

- Kellerspeicher: Stapel beliebiger Höhe (LIFO) => Stack 
- A = 
  - Q: Zustandsmenge
  - Sigma: Eingabealphabet
  - Gamma: Kelleralphabet
  - q0: Anfangszustand
  - Z0: Startsymbol Keller
  - Delta: Transitionsfunktion
  - F Teilmenge Q: Endzustände
- Lesekopf: Liest Zeichen aus Eingabe
  - Bewegung strikt nach rechts
- Lese/Schreibkopf: Liest oberstes Item des Stacks / fügt neues hinzu
- Arbeitsweise:
  a) Zeichen unter L-Kopf (optional epsilon falls nichts gelesen) und L/S Kopf einlesen
  b) Basierend darauf neuer Zustand
  c) Optional neues Zeichen an Stapel bei L/S Kopf (optional = epsilon = 'entfernen')
  d) L/S Kopf auf neues oberstes Zeichen (!= epsilon)
- Akzeptieren eines Wortes:
  - Abarbeiten bis einlesen Epsilon (= Ende des Wortes, und kein Weg zurück)
  - Zustand ist Endzustand
- Alternativ (äquivalent):
  - Akzeptieren = Keller leer, erhaltener Zustand egal
- Superset von DEAs
- Im allgemeinen nicht-deterministisch

### Deterministische Kellerautomaten

- Max 1 Nachfolger bei gewissem Status, Eingabe, Stack
- Superset von DEA

## Turingmaschine

- Unendliches Eingabeband
- M = 
  - Q: Zustandsmenge
  - Sigma: Eingabealphabet
  - Gamma: Arbeitsalphabet (Superset von Sigma)
  - q0: Anfangzustand
  - B: Blank
  - Delta: Q x Gamma -> Q x Gamma X {L, R, N}: Transitionsfunktion
  - F: Endzustände
  - Annahme dass Q und Gamma disjunkt

# Reguläre Sprachen

- Mit Alphabet Sigma, setze:
    - Schnitt in reg(Sigma), Raute in reg(Sigma), foreach a in Sigma: a in reg(Sigma)
    - Mit r, s in reg(Sigma): (r + s), (r o s), (r*) in reg(Sigma)
