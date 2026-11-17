# PS4 KI – eigene Oberfläche für ein lokales Modell

Eine einzelne Webseite (`index.html`, keine Abhängigkeiten, kein Tracking) für ein **lokales Sprachmodell, das auf einer PS4 mit Linux läuft** (llama.cpp, Qwen3-4B). Es kostet nichts, und deine Texte verlassen dein Heimnetz nicht.

**Modi:** Chat · Übersetzen · Zusammenfassen · Umformulieren · Einfach erklären · Notizen → Stichpunkte · E-Mail-Entwurf · Code erklären. Antworten kommen live (Streaming), mit Tokens pro Sekunde, Chat-Verlauf im Browser, Export als Textdatei, hell/dunkel.

## Wichtig zu verstehen

- GitHub Pages liefert nur **diese Oberfläche**. Die KI selbst läuft auf der PS4 bei dir zu Hause und ist **nur im selben WLAN erreichbar**.
- Chats, Einstellungen und ein optionaler API-Schlüssel werden **nur im lokalen Speicher deines Browsers** abgelegt. An GitHub geht nichts.
- Das Modell ist klein und langsam (ca. 4 Tokens/s, 4096 Tokens Kontext). Es taugt für kurze Texte, nicht für komplexe Logik oder Fehlersuche. Prüfe Antworten selbst. Keine Geheimnisse eingeben: Die Verbindung zur PS4 ist unverschlüsselt (http) und der Server hat standardmäßig kein Passwort.

## Passwort

Beim Öffnen fragt die Seite nach einem Passwort. Im Quelltext steht nur ein Hash (PBKDF2-SHA256, 100 000 Runden, zufälliges Salz), nie das Passwort selbst. Das ist **eine Sperre für die Oberfläche, kein echter Schutz**: Auf einer statischen Seite kann jeder Besucher den Quelltext lesen und die Sperre umgehen. Wirklich geschützt ist die KI dadurch, dass sie nur im Heimnetz erreichbar ist. Mit dem Schloss-Symbol oben rechts sperrst du die Seite wieder.

## Benutzen

1. Seite öffnen und unter **Einstellungen** die Adresse der PS4 eintragen, z. B. `http://192.168.x.x:8080`.
2. Oben links in der Kopfzeile zeigt **PS4-KI bereit**, dass der Server antwortet.
3. Modus wählen, Text einfügen, mit **Strg+Enter** senden.

### Wenn der Status „blockiert“ zeigt

Diese Seite wird per `https` geliefert, der PS4-Server spricht `http`. Browser blockieren das als „gemischte Inhalte“. Drei Wege, einfachster zuerst:

1. **Seite von der PS4 selbst öffnen:** `http://<PS4-IP>:8090`. Dort funktioniert alles ohne Einstellungen, auch am Handy.
2. **`index.html` herunterladen** und lokal im Browser öffnen.
3. Chrome/Edge: Schloss-Symbol → Websiteeinstellungen → *Unsichere Inhalte* auf „Zulassen“ stellen (ggf. auch „Lokales Netzwerk“ erlauben), Seite neu laden. Firefox blockiert das strenger.

## Server auf der PS4 (Kurzfassung)

Die Seite spricht die OpenAI-kompatible API von `llama-server` (`/v1/chat/completions`, `/health`) an. Der Server muss Browser-Anfragen erlauben (CORS), was `llama-server` standardmäßig tut. Optional lässt sich ein API-Schlüssel setzen (`--api-key-file`), den du dann in den Einstellungen einträgst.

## Lizenz

Für die Seite ist keine Lizenz festgelegt. Das Modell (Qwen3) hat eine eigene Lizenz (Apache 2.0).
