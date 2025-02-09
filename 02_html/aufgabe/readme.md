# Aufgaben: HTML

Wir erstellen eine Website für ein Zoo. Jedes Tier soll eine eigene Seite erhalten.

1. Wähle ein Zoo-Tier aus, z.B. dein Lieblingstier, und suche die passende Wikipedia-Seite
2. Kopiere von der Seite einen kurzen Beschreibungstext und speichere ein Bild
3. Erstelle eine neue HTML Datei mit dem Name vom Tier, z.B. roter_panda.html.  
   Deine Optionen:
    1. __Easy-Mode:__ Kopiere die Musterlösung und ersetzte den Inhalt
    2. __Normal-Mode:__ Kopiere das Template und ersetze die Platzhalter
    3. __Hard-Mode:__ Befolge die Anleitung im nächsten Abschnitt
4. __WICHTIG__: Speichere deine Lösung auf dem Share!


## Hard-Mode

1. Öffne VS Code
2. Erstelle eine neue Datei
3. Speichere die Datei als {tier_name}.html
4. Gebe im Editor `html:5` und drücke Enter. "Emmet" generiert ein HTML Template.
5. Setze im Template 
    1. lang="de"
    2. Title -> Tiername
    3. Setze im head den Meta-Tag `<meta name="author" content="{DEIN NAME}" />`
    4. Im `<body>` erstelle ein `<div class="main">`
        1. Im `<div>` setze eine Überscrhift `<h1>` mit Namen vom Tier
        2. Darunter das Bild `<img src="" alt="" />`
        3. Darunter ein Paragraph `<p>` mit den Beschreibungstext
        4. Darunter ein Link `<a href="">` zu der Wikipedia-Seite
    5. Optional: Setze in head `<link href="../zoo-style.css" rel="stylesheet" />`



## Bonus 1

1. Wähle ein weiteres Tier und erstelle eine weitere Seite, wie oben
2. Im oberen Teil beider Seite erstelle eine `<ul>` Liste mit Links `<a href="">` zu den jeweils anderen Seite.  

```html
<!-- Beispiel in tier_b.html-->
<ul>
    <li><a href="tier_a.html">Tier A</a></li><!-- Link zur anderen Seite -->
    <li>Tier B</li><!-- Kein Link benötigt, da das die aktuelle Seite ist-->
</ul>
```

## Bonus 2

1. Erstelle eine Übersichtsseite für den Zoo `index.html`
2. Die Seite soll jedes Tier auflisten mit Bild, Namen und einen Link auf die Unterseite

```html
<div id="teasers">
    <div class="teaser">
        <a href="animal_name.html">
            <img src="" alt="" />
            <span>Animal Name</span>
        </a>
    </div>
    <div class="teaser">
        <!-- ... -->
    </div>
    <!-- ... -->
</div>
```

 