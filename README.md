# Programmentwurf Funktionale Programmierung / Haskell

## Allgemeine Hinweise:
* Zu Implementieren ist die Programmieraufgabe in Haskell (Lauffähig in Hugs)
* Arbeiten Sie mit den Prinzipien der funktionalen Programmierung wie in der Vorlesung behandelt
* Abzugeben ist die Quelldatei (restaurant.hs / restaurant.lhs) über Moodle. Erweitern Sie die gegebene Datei einfach um Ihre Funktionen.
* Start ist der 26.11.2021
* Abgabeschluss ist der 07.01.2022, 23:59 Uhr
* In die Bewertung fließen funktionale Anforderungen (wie unten beschrieben), aber auch subjektive Faktoren wie die Strukturierung des Codes oder Wiederverwendung von Funktionen.
* Achten Sie auf eine angemessene Performance. Auch das spielt in die Bewertung mit ein.
* Die Arbeit ist eine Gruppenarbeit. Einer pro Gruppe muss eine Abgabe in Moodle tätigen - nicht alle.
* Jede Gruppe erhält dieselbe Aufgabe. Der Austausch von Code zwischen den Gruppen ist nicht zulässig.

## Allgemein:

Sie werten Daten eines Restaurants aus. Sie bekommen die Rohdaten in Form von Haskell-Funktionen (ohne Parameter). Dies ist Mittel zum Zweck - sehen Sie diese Funktionen als Schnittstelle in ein echtes System. Sie bekommen Fragestellungen, die Sie in Form von Funktionen implementieren müssen. Wie viele und welche Funktionen zwischen der Eingangs- und Ausgangsschicht liegen und ob diese sichtbar sind (lokale Definitionen), bleibt Ihnen überlassen.

## Die Quelldaten:

Sie erhalten vier Funktionen, also vier Datenquellen. Dabei handelt es sich grundsätzlich um Funktionen ohne Eingangsparameter - es sind einfache Datenquellen. Auch das Filtern der richtigen Daten muss durch Sie erfolgen.

1. Artikel: Diese Funktion gibt den Artikelstamm zurück. Zu Artikelnummern werden Artikelbezeichnungen geliefert. Aber auch eine Kategorie, die später ausgewertet werden kann. Zudem steht hier der Preis und die Einzelkosten für einen Artikel. Einzelkosten sind die Kosten, die unmittelbar beim Einkauf der Zutaten für die Zubereitung des Artikels entstehen.

2. Pacht: Die Pacht für das Restaurant muss pro Monat bezahlt werden. Damit gehören diese Kosten zu den Gemeinkosten. Sie sind nicht einem Artikel zuzuordnen, sondern fallen generell an. Sie bekommen die Pacht in einer Struktur mit Jahr und Monat. Somit können Sie die Pacht eines spezifischen Monats bestimmen.

3. Löhne: Die Löhne verhalten sich wie die Pacht und gehören damit ebenfalls zu den Gemeinkosten.

4. Buchungen: Das ist die Buchungsliste aus der Kasse. Hier erhalten Sie unter Angabe von Jahr, Monat, Tag, Stunde und Minute den verkauften Artikel. Es gibt keine Menge bzw. die Menge ist immer 1. Hinweis: Die Daten wurden völlig zufällig erstellt.

Wenn Sie Änderungen an den Quelldaten für unerlässlich halten, dann führen Sie diese Änderungen durch und dokumentieren Sie diese in Form von Kommentaren am Anfang der Quelldatei.

## Aufgabe 1: Die Anzahl:

Die erste Funktion, die Sie implementieren sollen, heißt "anzahl". Signatur:

anzahl :: (Int,Int,Int) -> String -> Int

Die Funktion liefert die Anzahl verkaufter Artikel mit folgenden Filtern:

Parameter 1: Datum. Hier wird Jahr, Monat und Tag geliefert. Der Tag ist optional. Wenn Tag=0 übergeben wird, dann soll die Anzahl des gesamten Monats zurückgegeben werden. Fehlerbehandlung: Sie müssen nicht prüfen, ob das Datum plausibel ist. Wenn hier z.B. der 31.02. abgerufen wird, dann geben Sie Anzahl 0 zurück.

Parameter 2: Artikelbezeichnung oder Kategorie: In diesem String kann sich entweder eine Artikelbezeichnung wie "Hamburger" oder eine Kategorie wie "Hauptgericht" übergeben werden. Es kann auch "*" übergeben werden. In dem Fall werden alle Artikel summiert. Wenn der Text im Artikelstamm nicht gefunden wird und auch nicht "*" entspricht, soll eine entsprechende Fehlermeldung erscheinen.

## Aufgabe 2: Der Umsatz

Die zweite Funktion heißt "umsatz". Signatur:

umsatz :: (Int,Int,Int) -> String -> Float

Die Funktion liefert den Umsatz der verkauften Artikel. Beim Umsatz zählt nur der Preis, keine Kosten. Es gelten dieselben Filterregeln wie bei der Anzahl.

## Aufgabe 3: Der Gewinn

Die dritte Funktion heißt "gewinn". Signatur:

gewinn :: (Int,Int,Int) -> String -> Float

Die Funktion liefert den Gewinn, also den Umsatz abzüglich der Einzel- sowie Gemeinkosten. Es gelten dieselben Filterregeln wie bei der Anzahl. Die Gemeinkosten werden auf die Gesamtanzahl verkaufter Artikel gleichmäßig verteilt. Beispielrechnung: Es werden in einem Monat 300 Hamburger, 200 Cheeseburger, 100 Chckenburger, 300 Cola und 100 Wasser verkauft. Das sind in Summe 1000 verkaufte Artikel. Dem stehen Löhne und Pacht von in Summe 2000€ entgegen. Das bedeutet, dass jeder Hamburger, Cheeseburger, Chickenburger, Cola und Wasser je 2 € Gemeinkosten tragen müssen.

## Aufgabe 4: Die Top-/Flop-Analyse

Schließlich sollen die folgenden Funktionen implementiert werden:

topAnzahl :: (Int,Int) -> (String,Int,Float)

flopAnzahl :: (Int,Int) -> (String,Int,Float)

topUmsatz :: (Int,Int) -> (String,Float,Float)

flopUmsatz :: (Int,Int) -> (String,Float,Float)

topGewinn :: (Int,Int) -> (String,Float,Float)

flopGewinn :: (Int,Int) -> (String,Float,Float)

Es handelt sich also um eine Top-/Flop-Analyse von Anzahl, Umsatz und Gewinn. Top: Ausgabe des stärksten Artikels; Flop: Ausgabe des schwächsten Artikels. Eingabeparameter ist Jahr und Monat, in der Ausgabe ist die Artikelbeschreibung und der Wert, also die Anzahl, der Umsatz oder der Gewinn dieses Artikels in diesem Monat. Zuletzt wird noch ein weiterer Float ausgegeben. Dabei handelt es sich um den prozentuellen Anteil im betreffenden Monat. Die anteilige Anzahl wird daher mit "Anzahl des Artikels in dem Monat"/"Gesamtanzahl verkaufter Artikel in dem Monat" berechnet. Umsatz und Gewinn analog. Darstellung ist z.B: "0.25" für 25 %.
