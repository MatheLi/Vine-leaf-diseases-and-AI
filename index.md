# Vine-leaf-diseases-and-AI
### Erkennung von Weinblattkrankheiten mit KI

Ziel des Projekes: Unsere KI soll mit Hilfe von Handybildern Weinblattkrankheiten erkennen und unterscheiden können.

<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/res/titelbild.JPG" width="900" height="500">

<a href="https://pixabay.com/de/photos/trauben-weintrauben-sonne-3550729/">Image Source</a>

Ziel des Projekes: Unsere KI soll mit Hilfe von Handybildern Weinblattkrankheiten erkennen und unterscheiden können.

Wir haben eine Handy-App programmiert die Blattkrankheiten von Weinreben mit Hilfe von Künstlicher Intelligenz klassifiziert.

Dadurch erhoffen wir uns einen deutlich geringeren Pestizideinsatz, da die Krankheit früh und einfach mit unserer App erkannt, bestimmt und behandelt werden kann bevor sie sich auf weitere Weinreben ausweitet bzw. sie die Pflanzen so stark schwächt, dass der Ertrag enorm sinkt. Daher wirkt sich unser Projekt auch positiv auf den Ertrag aus, wodurch langfristig Nutzanbaufläche reduziert werden kann.

Im Moment unterscheidet bzw. erkennt unsere künstliche Intelligenz (KI), verbunden mit unserer App zwischen vier verschiedenen Krankheitstypen (Echter Mehltau, falscher Mehltau, Esca und Schwarzholzkrankheit). Da eine KI für das Training eine sehr großen Datensatz benötigt, diese jedoch nur in begrenztem Umfang zur Verfügung stehen haben wir auch eigene Aufnahmen der Blattkrankheiten gemacht. Zukünftig planen wir den Datensatz auf weitere Weinrebenkrankheiten auszuweiten. Zudem planen wir andere landwirtschaftliche Nutzpflanzen mit häufigen Schädlings- und Pilzbefällen hinzufügen und somit den Pestizideinsatz allgemein deutlich zu verringern.

Wie funktioniert die KI bzw. App für den Anwender? Die Anwendung ist sehr einfach: Nach dem Download und öffnen unserer App wird ein Bild von dem Weinrebenblatt mit dem Handy gemacht. Das erstellt Bild wird von der KI analysiert und gibt anschließend die klassifizierte Krankheits aus


### Krankheiten in der Nachbarschaft 
Weinblatt Krankheiten breiten sich stark lokal aus. Um diese lokalen Hotspots ausfindig zu machen und allgemein zu wissen, welche Krankheit sich aktuell stark verbreitet, möchten wir eine Datenbank aufbauen.
Zu Testzwecken läuft eine eigene API aktuell auf einem Raspberry-PI und schreibt eine .json Datei im Folgenden Format:

```
{
  'Type': 'Esca',
  'timestamp': time.time(),
  'Koordinaten': '52.52,13.45', 
  'Username': 'INFOrmAtIc Teens'
}
```

## Bitte nehmen Sie an unserer Umfrage teil:

[Umfrage](https://survey123.arcgis.com/share/ee39c39ed1c04be8a95455205bf60710) 

| [Generelle Projektinformationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/) | [Die verschiedenen Krankheiten](https://matheli.github.io/Vine-leaf-diseases-and-AI/Different-diseases) | [Die App](https://matheli.github.io/Vine-leaf-diseases-and-AI/App) | [Der Code des Modells Teil 1](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code) | [Der Code des Modells Teil 2](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code2) | [Image Preprocessing](https://matheli.github.io/Vine-leaf-diseases-and-AI/ImagePreprocessing) | [Sonstige Informationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Sonstiges) | [Umfrage](https://matheli.github.io/Vine-leaf-diseases-and-AI/Survey) | [The Team](https://matheli.github.io/Vine-leaf-diseases-and-AI/Team) | [Der Betriebsschlüssel](https://matheli.github.io/Vine-leaf-diseases-and-AI/Betriebsschl%C3%BCssel) | [Interviews mit den Weinköniginnen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Interviews)| [Datenschutzerklärung](https://matheli.github.io/Vine-leaf-diseases-and-AI/Datenschutzerklärung) | [Impressum](https://matheli.github.io/Vine-leaf-diseases-and-AI/Impressum) |


