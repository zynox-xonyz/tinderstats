# Tinder Data Report

Wertet den Datenexport aus, den Tinder dir auf Anfrage schickt, und zeigt daraus einen
kompletten Report mit Diagrammen im Browser an.

Eine einzige HTML Datei. Kein Server, kein Build, keine Abhängigkeiten, keine Installation.
Du öffnest die Datei, ziehst deinen Export hinein, fertig.

## Benutzung

1. `index.html` herunterladen und per Doppelklick im Browser öffnen.
2. Deine `data.json` in das Feld ziehen. Alternativ funktioniert auch direkt die
   `myData.zip`, die wird im Browser entpackt.
3. Der Report erscheint sofort.

## Woher bekomme ich den Export?

In der Tinder App unter Einstellungen die Option „Kopie meiner Daten anfordern“ wählen.
Nach ein paar Tagen kommt eine Mail mit einem ZIP Archiv, darin liegen `data.json`
und eine `index.html` von Tinder selbst. Gebraucht wird die `data.json`.

## Was ausgewertet wird

**Kennzahlen**
* Swipes, Likes, Nopes, Superlikes, Likequote, Nopes pro Like
* Matches, Matchquote, Likes pro Match
* Öffnungen der App, Swipes pro aktivem Tag, gesendete und empfangene Nachrichten

**Verlauf**
* Gestapelte Likes und Nopes pro Tag, Woche oder Monat, mit Markern an Tagen mit Match
* Likequote im Zeitverlauf gegen den Durchschnitt
* Öffnungen der App im Zeitverlauf
* Kalenderansicht mit einem Kästchen pro Tag, je dunkler desto mehr Swipes

**Muster**
* Verteilung der Swipes über die Wochentage
* Stärkster Tag, meiste Likes an einem Tag, längste Serie aktiver Tage, längste Pause
* Trichter von Swipes über Likes und Matches bis zu Chats mit Antwort

**Nachrichten**
* Antwortquote, Antwortzeiten als Median für beide Seiten
* Chats ohne jede Antwort, wer das Gespräch eröffnet hat
* Verteilung über die Tageszeit, häufigste Wörter, häufigste Emojis
* Tabelle aller Chats und deine Gesprächseinstiege im Wortlaut

**Profil und Rest**
* Stammdaten, Sucheinstellungen, Bio, Prompts, Interessen, alle Angaben aus den Profilkarten
* Profilfotos, verknüpfter Spotify Account mit Anthem und Topkünstlern
* Käufe und Abos, Kampagnen
* Ein Explorer für die kompletten Rohdaten, damit kein Abschnitt der Datei untergeht

Dazu kommen ein Zeitraumfilter, der alle Zahlen darunter neu berechnet, eine Tabellenansicht
zu jedem Diagramm, Umschaltung zwischen hell und dunkel sowie ein Export als PDF.

## Datenschutz

Deine Datei wird nirgendwohin hochgeladen. Das Einlesen passiert vollständig im Browser
über die File API, es gibt keinen Server und keinen Analyseanbieter.

Eine Einschränkung der Ehrlichkeit halber: Profilfotos und Bilder der Spotify Künstler
werden über die Original URLs aus deinem Export geladen, also von den Servern von Tinder
und Spotify. Das sind die einzigen ausgehenden Anfragen der Seite. Wenn du das nicht
möchtest, trenne die Verbindung zum Netz, bevor du die Datei öffnest. Alles andere
funktioniert dann weiterhin, nur die Bilder bleiben leer.

## Anforderungen

Ein aktueller Browser. Für den direkten Import von ZIP Archiven wird `DecompressionStream`
gebraucht, das gibt es ab Chrome 103, Firefox 113 und Safari 16.4. Ohne diese
Unterstützung entpackst du das Archiv einfach selbst und lädst die `data.json`.

## Daten fest einbetten

Wer eine in sich geschlossene Datei zum Weitergeben braucht, kann die Daten direkt
einbetten. Dafür vor dem Hauptskript folgendes einfügen:

```html
<script>window.__TINDER_DATA__ = { hier der Inhalt der data.json };</script>
```

Die Seite startet dann ohne Auswahldialog.

## Technik

Reines HTML, CSS und JavaScript ohne Framework. Die Diagramme sind handgeschriebenes SVG,
die Animationen laufen über CSS und respektieren `prefers-reduced-motion`. Jedes Diagramm
hat eine gleichwertige Tabellenansicht, damit keine Aussage nur an einer Farbe hängt.
Die Farbskalen sind auf Kontrast und Farbfehlsichtigkeit geprüft und in hell wie dunkel
getrennt gesetzt.

## Lizenz

MIT, siehe `LICENSE`.
