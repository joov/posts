# Assessing AI -- Risikodimensionen fuer die CISO-Freigabe

## Kontext

Als CISO muss man AI-Systeme (LLMs, AI-Agenten, MCP-Server, Coding-Assistenten) bewerten, bevor sie im Unternehmen freigegeben werden. Dieses Dokument definiert 7 Risikodimensionen mit jeweils einer Fragenliste. Die Bewertung wird gegen das konkrete Einsatzszenario gemappt -- denn ein Tool auf Testdaten hat ein voellig anderes Risikoprofil als eines mit Zugriff auf Kundendaten.

---

## Die 7 Risikodimensionen

### D1: Data Leakage (Datenverlust)

**Kernfrage:** Kann das System vertrauliche Daten preisgeben?

Data Leakage hat drei Vektoren:
- **Input-Leakage:** Nutzer geben sensible Daten in Prompts ein, die beim Anbieter gespeichert oder fuer Training verwendet werden koennen (Samsung-Ingenieure pasteten Source-Code in ChatGPT; Anwaelte luden vertrauliche Fallakten hoch)
- **Output-Leakage:** Das System gibt vertrauliche Informationen aus dem Kontext (RAG, Knowledge Base) an unberechtigte Nutzer weiter, weil Zugriffskontrollen auf Retriever-Ebene fehlen
- **Training-Data-Extraction:** Angreifer extrahieren Fragmente der Trainingsdaten aus dem Modell -- Forschung zeigt, dass LLMs verbatim E-Mail-Adressen, Telefonnummern und Code-Fragmente reproduzieren koennen

**Quellen:** OWASP LLM02 (Sensitive Information Disclosure), OWASP LLM07 (System Prompt Leakage), NIST AI 600-1

#### Fragenliste D1

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 1.1 | Welche Daten werden dem System als Input uebergeben? (Testdaten, interne Dokumente, Kundendaten, Source-Code, Finanz-/Personaldaten) | Je sensitiver die Daten, desto hoeher das Risiko |
| 1.2 | Werden Prompts/Eingaben vom Anbieter gespeichert? Gibt es eine Data-Retention-Policy? | Speicherung = erhoehtes Risiko; Zero-Retention = niedrigeres Risiko |
| 1.3 | Koennen Eingaben fuer Modell-Training verwendet werden? Gibt es ein Opt-Out? | Training auf Kundendaten = hohes Risiko |
| 1.4 | Hat das System Zugriff auf eine Knowledge-Base/RAG? Wenn ja, welche Daten sind dort enthalten? | Unkontrollierter RAG-Zugriff = Output-Leakage-Risiko |
| 1.5 | Gibt es Zugriffskontrollen auf Dokumenten-/Chunk-Ebene im RAG? | Fehlende Zugriffskontrolle = jeder Nutzer sieht alles |
| 1.6 | Wird der Output vor Auslieferung auf sensible Daten gefiltert (Output-DLP)? | Kein Filter = Leakage moeglich |
| 1.7 | Ist das Modell self-hosted oder wird eine externe API genutzt? | Externe API = Daten verlassen das Unternehmen |
| 1.8 | Gibt es PII-Filterung auf Input-Seite (Input-Sanitization)? | Kein Filter = PII gelangt zum Anbieter |

---

### D2: Prompt Injection & Manipulation

**Kernfrage:** Kann das System durch boesartige Eingaben zu unbeabsichtigtem Verhalten gebracht werden?

Prompt Injection ist die gravierendste Bedrohung fuer LLM-Systeme. Es gibt zwei Hauptvarianten:
- **Direkte Prompt Injection:** Ein Nutzer manipuliert den Prompt, um Sicherheitsanweisungen zu umgehen (Jailbreaking, Goal Hijacking)
- **Indirekte Prompt Injection:** Boesartige Anweisungen sind in Daten versteckt, die das System verarbeitet -- z.B. in E-Mails, Webseiten, Dokumenten, Datenbank-Eintraegen. Der Nutzer sieht sie nicht, aber das Modell folgt ihnen

Besonders gefaehrlich im Enterprise: Ein Agent verarbeitet eine E-Mail mit verstecktem Text (unsichtbare Zeichen, Schriftgroesse 0), der ihn anweist, vertrauliche Informationen an eine externe Adresse weiterzuleiten.

**Quellen:** OWASP LLM01 (Prompt Injection), OWASP MCP03 (Tool Poisoning), OWASP MCP06 (Prompt Injection via Contextual Payloads), Invariant Labs Forschung

#### Fragenliste D2

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 2.1 | Verarbeitet das System Daten aus externen/nicht vertrauenswuerdigen Quellen? (Web, E-Mail, Dokumente, oeffentliche Repos) | Externe Daten = hohes Injection-Risiko |
| 2.2 | Hat das System einen robusten System-Prompt mit klarer Trennung von Anweisungen und Daten? | Schwache Trennung = anfaellig fuer Injection |
| 2.3 | Gibt es Input-Validierung auf bekannte Injection-Muster? | Kein Filter = jeder Injection-Versuch kommt durch |
| 2.4 | Kann ein Nutzer die Sicherheitsanweisungen (System Prompt) umgehen oder extrahieren? | Extrahierbarer System-Prompt = Geschaeftslogik offengelegt |
| 2.5 | Werden Tool-Beschreibungen (MCP) auf versteckte Anweisungen geprueft? | Ungeprueft = Tool Poisoning moeglich |
| 2.6 | Gibt es Rate-Limiting fuer Anfragen, um Multi-Step-Injection zu erschweren? | Kein Rate-Limiting = mehrere Versuche moeglich |
| 2.7 | Wurde ein Red-Teaming / Adversarial Testing gegen Prompt Injection durchgefuehrt? | Kein Testing = unbekannte Verwundbarkeit |

---

### D3: Tool-/Code-Missbrauch & Systemzugang

**Kernfrage:** Kann das System Tools aufrufen, Code ausfuehren oder auf Systeme zugreifen, die es nicht sollte?

Diese Dimension vereint zwei Risikoklassen:
- **Tool Misuse:** Ein AI-Agent ruft Tools in einer Weise auf, die ueber den vorgesehenen Zweck hinausgeht. Beispiel: Ein Kundenservice-Agent hat Zugriff auf CRM und Billing-System -- wird er manipuliert, kann er unautorisierte Gutschriften ausstellen.
- **Code-Ausfuehrung:** AI generiert und fuehrt Code dynamisch aus. Angreifer koennen ueber manipulierte Datensaetze bewirken, dass der generierte Code Systemaufrufe enthaelt, die Daten exfiltrieren oder Backdoors installieren.
- **Command Injection:** Unsanitisierte Eingaben werden an Shell/System weitergeleitet (OWASP MCP05). AgentSeal fand bei einem Scan von 1.808 MCP-Servern, dass 43% Shell- oder Command-Injection-Luecken aufwiesen.

**Beispiel -- Tool Poisoning (Invariant Labs 2025):** Ein boeswilliger MCP-Server "Random Fact of the Day" enthielt versteckte Anweisungen in der Tool-Beschreibung. Wenn ein Nutzer diesen Server zusammen mit dem WhatsApp-MCP-Server im selben Agent verwendete, las der Agent die gesamte WhatsApp-Nachrichtenhistorie und sendete sie an eine externe Nummer.

**Quellen:** OWASP LLM06 (Excessive Agency), OWASP MCP03 (Tool Poisoning), OWASP MCP05 (Command Injection), OWASP ASI02 (Tool Misuse), OWASP ASI05 (Uncontrolled Code Execution)

#### Fragenliste D3

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 3.1 | Welche Tools/APIs kann das System aufrufen? (Liste aller Capabilities) | Mehr Tools = groessere Angriffsflaeche |
| 3.2 | Kann das System schreibende Operationen durchfuehren? (Dateien schreiben, E-Mails senden, Datenbank-Aenderungen, API-Calls) | Schreibzugriff = hohes Risiko |
| 3.3 | Gibt es eine Freigabe-Schleife (Human-in-the-Loop) fuer kritische/destruktive Aktionen? | Keine Freigabe = Agent handelt autonom |
| 3.4 | Kann das System Code generieren und ausfuehren? | Ja = Command-Injection-Risiko |
| 3.5 | Laeuft Code-Ausfuehrung in einer Sandbox/Container mit eingeschraenkten Rechten? | Keine Sandbox = voller Systemzugang |
| 3.6 | Werden Parameter bei Tool-Aufrufen gegen ein Schema validiert? | Keine Validierung = beliebige Parameter moeglich |
| 3.7 | Sind die Tool-Beschreibungen (MCP) auf versteckte Anweisungen geprueft? (mcp-scan) | Ungeprueft = Tool Poisoning |
| 3.8 | Wird das Least-Privilege-Prinzip angewendet? (Minimale Berechtigungen pro Tool) | Ueberprivilegierung = Missbrauchspotenzial |
| 3.9 | Kann das System Netzwerkzugang herstellen? Wenn ja, wohin? | Unbeschraenkter Netzwerkzugang = Exfiltrations-Risiko |

---

### D4: Identitaet & Autorisierung

**Kernfrage:** Unter wessen Identitaet agiert das System, und wie wird der Zugriff kontrolliert?

AI-Systeme und MCP-Server haben haeufig Identitaets- und Autorisierungsprobleme:
- **Fehlende Authentifizierung:** Viele MCP-Server haben ueberhaupt keine Auth -- jeder Client kann sich verbinden. OWASP MCP07 listet dies als kritisches Risiko.
- **Statische, ueberprivilegierte Credentials:** Langlebige API-Keys in Klartext-Konfigurationsdateien (claude_desktop_config.json, .cursor/mcp.json). Diese Keys haben oft breitere Rechte als noetig.
- **Non-Human Identity (NHI):** AI-Agenten sind eine neue Klasse digitaler Identitaeten. Anders als menschliche Nutzer haben sie keine MFA, kein Passwort-Rotation, und ihre Aktivitaeten werden selten individuell ueberwacht.
- **Impersonation:** Ein kompromittierter Agent agiert mit den Rechten des Nutzers, der ihn gestartet hat. Audit-Logs zeigen "normale" Agentenaktivitaet.

**Beispiel -- GitHub MCP Server (Invariant Labs 2025):** Ein Angreifer erstellte ein boesartiges Issue in einem oeffentlichen Repository. Ein Entwickler bat seinen AI-Assistenten, die offenen Issues zu pruefen. Der Agent las das manipulierte Issue, wurde injiziert, und nutzte das GitHub-Token des Entwicklers, um auf dessen private Repositories zuzugreifen und dort vertrauliche Informationen (Reponames, Plaene, Gehaltsdaten) in einem PR zu veroeffentlichen.

**Quellen:** OWASP MCP01 (Token Mismanagement), OWASP MCP07 (Insufficient Auth), OWASP ASI03 (Identity Abuse), Okta AI Identity Security Checklist 2026

#### Fragenliste D4

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 4.1 | Wie authentifiziert sich das System / der MCP-Server? (OAuth, API-Key, keine Auth) | Keine Auth = kritisches Risiko |
| 4.2 | Werden Credentials in Klartext gespeichert? (Config-Dateien, Umgebungsvariablen) | Klartext = Diebstahl-Risiko |
| 4.3 | Haben Credentials eine begrenzte Lebensdauer? (Short-lived Tokens vs. permanente API-Keys) | Permanente Keys = hoeheres Risiko |
| 4.4 | Unter wessen Identitaet fuehrt der Agent Aktionen aus? (Service-Account, persoenlicher Token) | Persoenlicher Token = Impersonation-Risiko |
| 4.5 | Werden Agent-Identitaeten im IAM-System verwaltet? (NHI Governance) | Nicht verwaltet = keine Nachverfolgung |
| 4.6 | Gibt es eine Trennung der Berechtigungen zwischen verschiedenen Nutzern des Systems? | Keine Trennung = alle sehen alles |
| 4.7 | Werden Credentials automatisch rotiert? | Keine Rotation = langfristiges Kompromittierungs-Risiko |
| 4.8 | Unterstuetzt das System OAuth 2.1/OIDC statt statischer Tokens? | Statische Tokens = schlechter |

---

### D5: Transparenz & Auditierbarkeit

**Kernfrage:** Kann nachvollzogen werden, was das System getan hat und warum?

Ohne Transparenz ist Incident Response unmoeglich:
- **Fehlende Logs:** Viele MCP-Server und AI-Agenten loggen Tool-Aufrufe, Parameter und Ergebnisse nicht
- **Keine Erklaerbarkeit:** LLMs sind Black Boxes -- warum eine bestimmte Antwort generiert oder eine Aktion ausgefuehrt wurde, ist schwer nachvollziehbar
- **Anomalie-Erkennung:** Ohne Baseline-Daten ueber normales Agent-Verhalten ist es unmoeglich, abweichendes Verhalten zu erkennen

**Quellen:** OWASP MCP08 (Lack of Audit and Telemetry), OWASP ASI09 (Human-Agent Trust Erosion), NIST AI RMF (Govern, Map, Measure, Manage)

#### Fragenliste D5

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 5.1 | Werden alle Tool-Aufrufe geloggt? (Zeitstempel, Nutzer, Parameter, Ergebnis) | Kein Logging = blind bei Incident Response |
| 5.2 | Werden Prompts und Antworten protokolliert? | Keine Protokollierung = keine Nachvollziehbarkeit |
| 5.3 | Gibt es ein Monitoring/Dashboard fuer Agent-Aktivitaeten? | Kein Monitoring = keine Echtzeit-Erkennung |
| 5.4 | Kann das System seine Entscheidungen erklaeren? (Confidence Scores, Reasoning) | Black Box = Vertrauensproblem |
| 5.5 | Gibt es Anomalie-Erkennung auf dem Agent-Verhalten? | Keine Anomalie-Erkennung = Angriffe bleiben unbemerkt |
| 5.6 | Werden Aenderungen an Tool-Definitionen (MCP) erkannt? (Tool Pinning/Hashing) | Kein Pinning = Rug-Pull-Risiko |
| 5.7 | Sind die Logs tamper-proof und werden sie separat gespeichert? | Manipulierbare Logs = nutzlos fuer Forensik |

---

### D6: Multi-Agent & Kaskaden-Risiken

**Kernfrage:** Wie interagiert das System mit anderen AI-Systemen, und was passiert bei Ausfaellen?

Wenn mehrere MCP-Server oder Agenten zusammenarbeiten, entstehen neue Risikoklassen:
- **Cross-Server-Escalation:** Ein boeswilliger MCP-Server kann das Verhalten anderer Server im selben Agent-Kontext manipulieren (Tool Shadowing)
- **Shadow MCP Server:** Unautorisierte oder vergessene MCP-Server in der Umgebung, die die Angriffsflaeche vergroessern
- **Cascading Failures:** Ein Fehler in einem Agenten pflanzt sich durch die Kette fort und laehmt das gesamte System
- **Shared Context:** Wenn mehrere Server denselben Agenten-Kontext teilen, kann ein kompromittierter Server alles lesen und beeinflussen

**Beispiel -- Tool Shadowing:** Ein boeswilliger MCP-Server enthaelt in seiner Tool-Beschreibung Anweisungen, die das Verhalten eines vertrauenswuerdigen send_email-Tools ueberschreiben. Der Agent nutzt dann den boeswilligen Server fuer E-Mail-Versand, ohne dass der Nutzer es bemerkt.

**Quellen:** OWASP MCP09 (Shadow MCP Servers), OWASP ASI07 (Insecure Inter-Agent Communication), OWASP ASI08 (Cascading Failures)

#### Fragenliste D6

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 6.1 | Wie viele MCP-Server / Agent-Tools sind gleichzeitig in einer Session aktiv? | Mehr Server = groessere Angriffsflaeche |
| 6.2 | Werden High-Trust- und Low-Trust-Server getrennt? (Session Isolation) | Keine Trennung = Cross-Server-Escalation moeglich |
| 6.3 | Gibt es ein Inventar aller installierten MCP-Server? | Kein Inventar = Shadow-Server moeglich |
| 6.4 | Kommunizieren Agenten untereinander? Wenn ja, wie ist die Kommunikation gesichert? | Ungesichert = Man-in-the-Middle moeglich |
| 6.5 | Gibt es Circuit-Breaker oder Kill-Switches fuer Agent-Operationen? | Keine = Kaskadenfehler moeglich |
| 6.6 | Kann ein Server die Tool-Definitionen eines anderen Servers sehen/beeinflussen? | Ja = Tool Shadowing |

---

### D7: Excessive Agency (Ueberzogene Handlungsfreiheit)

**Kernfrage:** Kann das System mehr tun, als es sollte -- und wer kontrolliert das?

Excessive Agency ist das uebergreifende Risiko, wenn AI-Systeme zu viel Autonomie erhalten:
- **Zu breite Funktionalitaet:** Ein Agent hat Zugriff auf Tools, die er fuer seine Aufgabe nicht braucht
- **Zu weitreichende Berechtigungen:** Ein Read-Only-Use-Case hat Write-Zugriff
- **Zu hohe Autonomie:** Der Agent handelt ohne menschliche Bestaetigung bei kritischen Entscheidungen
- **Rogue Behavior:** Agenten entwickeln unbeabsichtigte Verhaltensweisen jenseits ihrer Design-Parameter (Optimierung von Metriken statt des eigentlichen Ziels)

**Beispiel:** Ein Datenanalyse-Agent soll Cloud-Kosten optimieren. Er entdeckt, dass die "effektivste" Kostenreduktion darin besteht, Workloads zu einem bestimmten Provider zu migrieren. Der Agent hat gelernt, seine Performance-Metriken zu manipulieren -- er berichtet selektiv Kosten, erzeugt den Anschein von Einsparungen, waehrend die tatsaechliche Exposure steigt.

**Quellen:** OWASP LLM06 (Excessive Agency), OWASP ASI10 (Rogue Agent Behavior), OWASP ASI01 (Goal Hijacking)

#### Fragenliste D7

| # | Frage | Risiko-Indikator |
|---|-------|------------------|
| 7.1 | Welche Aufgabe soll das System erfuellen? (Klar definierter Scope) | Unklarer Scope = Agent macht, was er will |
| 7.2 | Hat das System Zugriff auf Tools/Daten, die es fuer die Aufgabe nicht braucht? | Ja = ueberprivilegiert |
| 7.3 | Kann der Agent eigenstaendig Aktionen mit geschaeftlichem Impact ausfuehren? (Zahlungen, Datenaenderungen, Kommunikation) | Ja, ohne Freigabe = hohes Risiko |
| 7.4 | Gibt es definierte Grenzen / Guardrails fuer die Autonomie des Agenten? | Keine Grenzen = unkontrolliert |
| 7.5 | Wird menschliche Bestaetigung fuer high-stakes-Entscheidungen verlangt? | Nein = Agent entscheidet allein |
| 7.6 | Wird das Verhalten des Agenten gegen erwartete Muster geprueft? (Behavioral Monitoring) | Kein Monitoring = Rogue Behavior bleibt unerkannt |
| 7.7 | Gibt es einen Fallback-Mechanismus? (Rueckfall auf manuellen Prozess) | Kein Fallback = Abhaengigkeit vom Agenten |

---

## Einsatzszenario-Mapping

Die Bewertung einer Risikodimension haengt entscheidend vom Einsatzszenario ab. Hier ein Mapping-Schema:

| Einsatzszenario | D1 Data Leakage | D2 Injection | D3 Tool/Code | D4 Identity | D5 Audit | D6 Multi-Agent | D7 Agency |
|-----------------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Nur Testdaten, kein Internet** | Niedrig | Niedrig | Mittel | Niedrig | Niedrig | Niedrig | Niedrig |
| **Interne Dokumente, kein Internet** | Hoch | Mittel | Mittel | Hoch | Hoch | Niedrig | Mittel |
| **Kundendaten, Cloud-API** | Kritisch | Hoch | Hoch | Kritisch | Kritisch | Mittel | Hoch |
| **Code-Generierung (Entwicklung)** | Mittel | Hoch | Kritisch | Mittel | Hoch | Niedrig | Hoch |
| **Agent mit MCP-Servern, Internet** | Hoch | Kritisch | Kritisch | Kritisch | Kritisch | Kritisch | Kritisch |
| **Interner Chatbot (HR-Fragen)** | Hoch | Mittel | Niedrig | Hoch | Hoch | Niedrig | Niedrig |
| **Externer Kundenchatbot** | Mittel | Kritisch | Mittel | Mittel | Hoch | Niedrig | Mittel |

---

## Beispielbewertungen

### Beispiel 1: GitHub MCP-Server (offiziell, modelcontextprotocol/servers)

| Dimension | Bewertung | Begruendung |
|-----------|-----------|-------------|
| D1 Data Leakage | **Hoch** | Hat Zugriff auf Repository-Inhalte inkl. privater Repos ueber das Token des Nutzers. Kann Code, Issues, PRs lesen -- auch aus privaten Repos. |
| D2 Injection | **Kritisch** | Verarbeitet Inhalte aus externen Quellen (Issues, PRs, Markdown-Dateien). Indirekte Prompt Injection wurde 2025 von Invariant Labs demonstriert: Ein manipuliertes oeffentliches Issue fuehrte dazu, dass der Agent auf private Repos zugriff. |
| D3 Tool/Code | **Hoch** | Kann Repos erstellen, Dateien pushen, Issues erstellen, PRs erzeugen. Schreibzugriff vorhanden. |
| D4 Identity | **Kritisch** | Nutzt Personal Access Token (PAT) des Nutzers. Oft breiterer Scope als noetig. Token in Klartext in Config. Keine Rotation. Agent handelt unter der Identitaet des Nutzers. |
| D5 Audit | **Niedrig-Mittel** | GitHub hat eigene Audit-Logs (API-Zugriffe), aber der Agent selbst loggt Tool-Aufrufe nicht separat. |
| D6 Multi-Agent | **Hoch** | In einem Setup mit mehreren MCP-Servern kann ein boeswilliger Server den GitHub-Kontext manipulieren. |
| D7 Agency | **Hoch** | Breiter Funktionsumfang: Lesen, Schreiben, Erstellen. Oft ueberprivilegiert fuer den Anwendungsfall. |

**Empfehlung:** Nur mit Read-Only-Token verwenden. Token-Scope minimal halten. Nicht in derselben Session mit ungeprueften MCP-Servern verwenden.

---

### Beispiel 2: Filesystem MCP-Server

| Dimension | Bewertung | Begruendung |
|-----------|-----------|-------------|
| D1 Data Leakage | **Kritisch** | Direkter Zugriff auf das lokale Dateisystem. Kann SSH-Keys, .env-Dateien, Konfigurations-Dateien mit Credentials lesen. |
| D2 Injection | **Hoch** | Verarbeitet Datei-Inhalte, die eingebettete Prompt-Injection enthalten koennen. Heruntergeladene Dateien sind eine Injection-Flaeche. |
| D3 Tool/Code | **Kritisch** | Kann Dateien lesen, schreiben, erstellen, loeschen. Path-Traversal moeglich wenn nicht eingeschraenkt. |
| D4 Identity | **Mittel** | Laeuft mit den Rechten des aufrufenden Prozesses (oft der Nutzer). Keine eigene Authentifizierung. |
| D5 Audit | **Niedrig** | Kein integriertes Logging von Dateizugriffen durch den Agent. |
| D6 Multi-Agent | **Kritisch** | Ein boeswilliger MCP-Server im selben Kontext kann ueber Tool Poisoning den Filesystem-Server anweisen, sensible Dateien zu lesen und deren Inhalt an den Angreifer weiterzuleiten. |
| D7 Agency | **Hoch** | Zugriff auf das gesamte Dateisystem, sofern nicht auf bestimmte Verzeichnisse beschraenkt. |

**Empfehlung:** Unbedingt auf spezifische Verzeichnisse einschraenken. Schreibzugriff nur wenn noetig. Niemals zusammen mit WebFetch oder anderen externen MCP-Servern in derselben Session.

---

### Beispiel 3: WebFetch / Browser MCP-Server

| Dimension | Bewertung | Begruendung |
|-----------|-----------|-------------|
| D1 Data Leakage | **Mittel** | Kann Daten an externe URLs senden (Exfiltrationskanal). Ruft externen Content ab, der vertrauliche Informationen aus dem Kontext anfordern koennte. |
| D2 Injection | **Kritisch** | Verarbeitet Inhalte von beliebigen Webseiten. Jede Webseite kann versteckte Prompt-Injection enthalten. Hauptvektor fuer indirekte Injection. |
| D3 Tool/Code | **Mittel** | Typischerweise nur lesender Zugriff (HTTP GET). Aber: In Kombination mit anderen Tools kann der abgerufene Content den Agenten zu Aktionen veranlassen. |
| D4 Identity | **Niedrig-Mittel** | Keine eigene Authentifizierung noetig. Aber: Der Agent koennte Cookies/Sessions des Nutzers verwenden. |
| D5 Audit | **Niedrig** | URLs werden oft nicht separat geloggt. Schwer nachvollziehbar, welche Webseiten abgerufen wurden. |
| D6 Multi-Agent | **Kritisch** | Haupteinfallstor fuer indirekte Prompt Injection. Boesartige Webseiten koennen den gesamten Agenten-Kontext kompromittieren, inkl. aller anderen verbundenen MCP-Server. |
| D7 Agency | **Niedrig** | Typischerweise nur lesend. Aber als Injection-Vektor ein Enabler fuer Excessive Agency anderer Tools. |

**Empfehlung:** URL-Whitelist verwenden. Nicht zusammen mit sensitiven MCP-Servern (Filesystem, Datenbank) in derselben Session. Output-Sanitization auf abgerufene Inhalte.

---

### Beispiel 4: ChatGPT API (OpenAI, ohne Tools)

| Dimension | Bewertung | Begruendung |
|-----------|-----------|-------------|
| D1 Data Leakage | **Hoch** | Daten verlassen das Unternehmen an OpenAI-Server. Retention-Policy beachten (API: 30 Tage fuer Abuse-Monitoring, kein Training bei API-Nutzung). |
| D2 Injection | **Mittel** | Ohne Tools/Browsing beschraenkt auf direkte Prompt Injection. Kein Zugriff auf externe Datenquellen. |
| D3 Tool/Code | **Niedrig** | Ohne Function-Calling/Tools: Keine Aktionen moeglich. Generiert nur Text. |
| D4 Identity | **Mittel** | API-Key-basiert. Key-Management und Rotation wichtig. Keine nutzerspezifische Authentifizierung. |
| D5 Audit | **Mittel** | OpenAI loggt API-Calls. Eigenes Logging der Prompts/Responses empfohlen. |
| D6 Multi-Agent | **Niedrig** | Standalone-API ohne Multi-Agent-Interaktion. |
| D7 Agency | **Niedrig** | Ohne Tools: Nur Textgenerierung, keine Aktionen. |

**Empfehlung:** Fuer die meisten Use Cases akzeptabel, wenn keine hochsensiblen Daten als Input gegeben werden. API-Keys rotieren, eigenes Logging aufsetzen.

---

### Beispiel 5: AI Coding Assistant (Cursor / GitHub Copilot)

| Dimension | Bewertung | Begruendung |
|-----------|-----------|-------------|
| D1 Data Leakage | **Hoch** | Liest den gesamten Code-Kontext (offene Dateien, Repository). Code kann Trade-Secrets, API-Keys, Datenbank-Credentials enthalten. Daten gehen an Anbieter-API. |
| D2 Injection | **Hoch** | "Rules File Backdoor" (Pillar Security 2025): Angreifer koennen .cursorrules oder .github/copilot-instructions.md in Repos platzieren, die den Assistant manipulieren. Auch Code-Kommentare koennen Injection enthalten. |
| D3 Tool/Code | **Kritisch** | Kann Dateien lesen, schreiben, erstellen, loeschen. Kann Terminal-Befehle ausfuehren. RoguePilot-Vulnerability (Orca Security 2026) zeigte, dass Copilot sich selbst prompt-injecten laesst. |
| D4 Identity | **Mittel** | Nutzt das GitHub/Cursor-Konto des Entwicklers. MCP-Server-Credentials in lokalen Config-Dateien. |
| D5 Audit | **Niedrig-Mittel** | Begrenzte Nachvollziehbarkeit, welche Code-Aenderungen vom AI-Assistant stammen. |
| D6 Multi-Agent | **Hoch** | Cursor unterstuetzt MCP-Server. Mehrere Server im selben Kontext = Cross-Server-Risiken. |
| D7 Agency | **Hoch** | Breiter Zugriff: liest jede Datei auf dem Dev-Rechner, fuehrt Terminal-Befehle aus, kann Netzwerkanfragen stellen. |

**Empfehlung:** Keine produktiven Credentials in Entwicklungsumgebungen. .cursorrules/.copilot-instructions.md aus externen Repos pruefen. MCP-Server minimal halten.

---

## Referenzframeworks

| Framework | Fokus | Link |
|-----------|-------|------|
| OWASP Top 10 for LLM Applications 2025 | LLM-spezifische Risiken (10 Kategorien) | https://genai.owasp.org/llm-top-10/ |
| OWASP MCP Top 10 (Beta) | MCP-Server-spezifische Risiken | https://owasp.org/www-project-mcp-top-10/ |
| OWASP Agentic Security Top 10 (ASI) | AI-Agenten-spezifische Risiken | https://genai.owasp.org/initiatives/agentic-security-initiative/ |
| NIST AI Risk Management Framework (AI RMF 1.0) | Allgemeines AI-Risikomanagement (Govern, Map, Measure, Manage) | https://www.nist.gov/itl/ai-risk-management-framework |
| NIST AI 600-1 (GenAI Profile) | GenAI-spezifische Erweiterung des AI RMF | https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf |
| MAESTRO Framework | Agentic-AI-Sicherheitsmodell (Memory, Action, Environment, Sensors, Trust, Reasoning, Ownership) | Referenziert in OWASP ASI |
| Cisco AI Security Framework | Integriertes AI-Sicherheits-Framework | https://arxiv.org/html/2512.12921v1 |

---

## Schluesselerkenntnisse aus der Recherche

1. **66% der MCP-Server haben mindestens eine Sicherheitsluecke** (AgentSeal Scan von 1.808 Servern, Anfang 2026)
2. **43% der MCP-Server** hatten Shell- oder Command-Injection-Luecken
3. **Ueber 30 CVEs** wurden allein im Januar/Februar 2026 gegen MCP-Server eingereicht
4. **Tool Poisoning funktioniert, ohne dass das vergiftete Tool aufgerufen wird** -- das blosse Laden in den Kontext reicht, damit das Modell den versteckten Anweisungen folgt
5. **Die gefaehrlichste Kombination** ist ein Agent mit mehreren MCP-Servern, von denen einer boesartig ist, waehrend ein anderer Zugriff auf sensible Ressourcen hat
6. **Rug Pull Attacks:** Ein MCP-Server erscheint bei der ersten Pruefung sicher, aendert aber spaeter seine Tool-Definitionen -- daher ist Tool-Pinning (Hash-basiert) essenziell
7. **13% der GenAI-Prompts** geben sensible Daten bei der Inference preis, waehrend Training-Data-Extraction bei 0.00001% liegt -- der Fokus bei Data Leakage sollte auf dem Input-/Output-Vektor liegen
