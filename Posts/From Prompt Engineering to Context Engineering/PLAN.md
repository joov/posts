# Plan: From Prompt Engineering to Context Engineering

## Meta

- **Zielgruppe:** Technisch interessierte Entscheider (CxOs, Heads of AI/Data, Strategy Leads)
- **Lesezeit:** 5-10 Minuten
- **Kernbotschaft:** Wer seine AI-Strategie auf Prompt-Optimierung aufbaut, investiert in die falsche Schicht. Die Wettbewerbsdifferenzierung liegt in der Kontextarchitektur.
- **Lesson Learned:** Die Qualitaet von AI-Ergebnissen haengt weniger davon ab, WIE Sie fragen, als davon, WAS das Modell zum Zeitpunkt der Antwort sieht.

---

## Struktur

### 1. Hook: Die Prompt-Illusion (~1 Min)

- "Prompt Engineer" war 2024 der heisseste Job-Titel. Bootcamps kassierten Milliarden. Heute verschwindet die Rolle von Jobboersen.
- Nicht weil AI schlechter wurde -- sondern weil die besten Teams erkannt haben, dass sie das falsche Problem loesten.
- Philipp Schmid (Google DeepMind): "Die Mehrheit der Fehler in AI-Agentensystemen sind keine Modellfehler -- sondern Kontextfehler."

### 2. Was hat sich veraendert? (~1.5 Min)

- 2023: Einzelne Prompts, einzelne Aufgaben. Der Prompt WAR das Produkt.
- 2026: AI Agents arbeiten in Loops, nutzen Tools, brauchen Gedaechtnis, treffen Entscheidungen ueber mehrere Schritte.
- Der Shift: Von "Wie sage ich es dem Modell?" zu "Was muss das Modell wissen, um die richtige Entscheidung zu treffen?"
- **Graph 1:** Prompt-Era vs. Context-Era (Gegenuberstellung)

### 3. Context Engineering: Was Entscheider wissen muessen (~2 Min)

- Definition (Schmid): "Die Disziplin, dynamische Systeme zu entwerfen, die die richtige Information mit den richtigen Werkzeugen im richtigen Format zum richtigen Zeitpunkt bereitstellen."
- Context ist eine **endliche Ressource** -- nicht "je mehr, desto besser". Anthropic: "Attention Budget" mit sinkenden Grenznutzen.
- **Anschauliches Beispiel:** Prompting ist, wie einem neuen Mitarbeiter einen Auftrag geben. Context Engineering ist, wie einem neuen Mitarbeiter einen Arbeitsplatz einrichten -- mit allen Arbeitsmitteln, Unterlagen, Zugaengen und Ansprechpartnern, die er braucht, um den Auftrag selbststaendig zu erledigen. Der Auftrag (Prompt) ist nur ein Teil. Die Umgebung (Context) entscheidet, ob er erfolgreich ist.
- Karpathy: Es ist zugleich "Science" (messbar, systematisch) und "Art" (Intuition fuer LLM-Psychologie).

### 4. Drei strategische Implikationen (~3 Min)

#### (a) Kontext ist die neue Datenbank

- Wer die bessere Kontextarchitektur hat, bekommt bessere AI-Ergebnisse -- unabhaengig vom Modell.
- Layered Context: Global / Projekt / Aufgabe. Nicht alles auf einmal reinwerfen, sondern gezielt steuern.
- **Graph 2:** Drei-Schichten-Modell des Kontexts mit Unternehmensbeispielen
- Praxis: Teresa Torres steuert ein ganzes Unternehmen mit einem dreischichtigen Kontextsystem.

#### (b) Ihre AI-Investition muss sich verschieben

- Bisher: Budget fuer Modell-Zugang, Prompt-Templates, Fine-Tuning
- Jetzt: Budget fuer Kontextarchitektur, Memory-Systeme, Tool-Integration, Instruktionsdateien
- Die "billige Demo" vs. das "magische Produkt" -- der Unterschied ist nicht das Modell, sondern der Kontext (Schmid-Beispiel: gleiche Email, verschiedene Kontextqualitaet)

#### (c) Prompt Engineering ist nicht tot -- es wurde befoerdert

- Es ist jetzt EINE Schicht in einem groesseren Stack
- Aber: Wer nur diese Schicht optimiert, optimiert die Tapete statt die Statik des Gebaeudes
- Fuenf Fragen fuer jede AI-Initiative: Ist der Kontext relevant? Ausreichend? Isoliert? Wirtschaftlich? Nachvollziehbar?

### 5. Was sollten Sie morgen tun? (~1 Min)

- **Context Audit:** Welche Informationen sieht Ihr AI-System tatsaechlich, wenn es eine Entscheidung trifft? (Die meisten Teams koennen diese Frage nicht beantworten.)
- **Stabil vs. Volatil trennen:** Unternehmensregeln, Tone, Policies gehoeren nicht in denselben Topf wie frische Tool-Ergebnisse.
- **Messen statt raten:** Wenn Sie Kosten, Latenz und Fehlermuster Ihrer AI nicht monitoren, raten Sie.

### 6. Schluss (~0.5 Min)

- Die Frage ist nicht mehr "Wie schreibe ich den perfekten Prompt?" Die Frage ist: "Welche Informationsumgebung braucht mein AI-System, um zuverlaessig zu arbeiten?"
- Wer das versteht, hoert auf Prompts zu polieren und faengt an, Kontextarchitektur zu bauen.

---

## Graphs (Mermaid)

1. **Prompt-Era vs. Context-Era:** Gegenuberstellung der Denkweisen (was sich verschiebt)
2. **Layered Context Architektur:** Drei Schichten mit Enterprise-Beispielen (Policies, Projektkontext, Task-spezifische Daten)

---

## Quellen (aus KNOWLEDGE.md)

1. Anthropic: Effective Context Engineering for AI Agents
2. Rephrase: 7 Steps to Context Engineering (2026)
3. Wikipedia (de): Context Engineering
4. Tobi Luetke: Original Tweet
5. Simon Willison: Context Engineering
6. Andrej Karpathy: Software 3.0
7. Petter Chr. Bjelland: Three Layers of Context
8. Teresa Torres / Peter Yang: Automate Your Life with Claude Code
9. Serokell: Design Patterns for Long-Term Memory
10. Carl Vellotti: Carl's Product OS (GitHub)
