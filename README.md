# Generative AI Coding Day @ Thinktecture AG

## 📋 Hintergrund

Unser Kunde, AS - Archery Supplies, vertreibt Produkte rund um den Bogensport.

Es wird dabei über einen eigenen Webshop, über Amazon und über eBay verkauft, und der Kunde
hat ein eigenes E-Commerce System, das alle Kundendaten, Bestellungen und Produktdaten
verwaltet. Wenn ein Kunde über die verbunden Plattformen arbeitet, also z.B. auf der eBay-
Webseite seine Bestellung storniert, läuft alles Problemlos ab.

Problematisch sind allerdings hunderte E-Mails, die über das Wochenende eintreffen.
Hier gibt es, neben normalem Support und Produktanfragen eben auch Stornobitten, die im
besten Fall per Reply auf eine Bestellbestätigung eingehen und damit alle notwendigen Infos
mitbrigen, im schlimmsten Fall aber einfach eine Mail mit dem Text "Ich brauche [Produktname]
doch nicht" sind.

Der Versand von Bestellungen die seit Freitag Mittag eingegangen sind startet Montags früh, und
aktuell "darf" sich eine Bürokraft Sonntag Abends von zuhause aus hinsetzen, und hunderte Mails
überfliegen. Wenn es hier um einen Storno geht, stellt sie den Kunden im CRM-System temporär auf
"gesperrt", damit die Bestellung nicht gleich verschickt wird, bis die Mail dann im Laufe des
Montags vernünftig abgearbeitet werden kann.

## 🔧 Aufgabe

Wir wollen der Bürokraft den Sonntagabend in Ruhe und ohne Arbeit gönnen.
Daher bauen wir kleines System, dass die eingegangenen Mails in der Nacht auf Montag
automatisch vorbereitet.

Ein Script legt uns die Mails in der Datei `mails.csv` 📁 ab.
Ein LLM soll diese Mails lesen, und mit Tools in die Lage versetzt werden, diese zu
analysieren und dann entsprechend zu agieren.

Initialisiere ein lokales Git-Repository 🗂️. Commite und arbeite so, wie du es sonst auch während deines Coding-Alltags tun würdest. Dazu gehört auch Musikhören 🎵, Pausen ☕, und alles Weitere.

Zum Durchführen von Prüfungen darf das LLM in die "Datenbank" schauen. Diese besteht
der Einfachheit halber aus den beiden Dateien `customers.csv` und `orders.csv`.
In `customers.csv` kann eine E-Mail Adresse zu einer Kundennummer aufgelöst werden.
In `orders.csv` stehen alle Bestellungen zu den Kundennummern, und der Status der
jeweiligen Bestellung. Solange die Bestellung bei `is_open` noch auf `true` steht, ist
sie noch nicht verschickt und kann noch storniert werden.

## 🎯 Ziele
Wenn aus einer Mail sowohl Kunden- als auch Order-Nummer eindeutig hervorgehen,
wobei die Kundennummer auch anhand der E-Mail Adresse ermittelt werden kann,
und die Bestellung zu diesem Kunden gehört, dann soll die Bestellung markiert werden,
so dass sie vorerst nicht weiter abgearbeitet wir, bis ein Mensch die Mail vollständig
abgearbeitet hat.

1️⃣ Für jede Bestellung die aufgehalten werden soll, soll ein Eintrag in eine neue Datei
gemacht werden mit Bestellnummer, Kundennummer, und dem Betreff sowie dem Body der Mail.
Wir nehmen an, ein weiteres script liest die Kundennummern hieraus und stellt diese Kunden
auf gesperrt, bis die Mails dann am Montag abgearbeitet wurden.

2️⃣ Für alle unklaren Stornoanfragen, sollen diese Angaben in eine andere Datei geschrieben
werden (z.B. Stornoanfrage für eine schon verschickte Bestellung, unklare Kunden- oder
Bestellnummer).

3️⃣ Beschwerden und sonstige Anfragen sollen auch jeweils in eigene Dateien geschrieben
werden, so dass hier die Reihenfolge in Zukunft besser priorisiert werden kann.
