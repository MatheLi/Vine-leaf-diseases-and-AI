
<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/res/titelbild.JPG" width="900" height="500">

<a href="https://pixabay.com/de/photos/trauben-weintrauben-sonne-3550729/">Image Source</a>


---

# Vine Leaf Disease 

> Klassifizieren von Weinblattkrankheiten mit Künstlicher Intelligenz

> Erstellt von: Maria-Theresa Licka und Mario Schweikert

---

## Table of Contents 

- [Projektbeschreibung](#Projektschreibung)
- [Inhalt](#Inhalt)
- [Setup](#Setup)


---

## Projektbeschreibung
Wir haben eine Handy-App programmiert die Blattkrankheiten von Weinreben mit Hilfe von Künstlicher Intelligenz klassifiziert. 

Dadurch erhoffen wir uns einen deutlich geringeren Pestizideinsatz, da die Krankheit früh und einfach mit unserer App erkannt, bestimmt und behandelt werden kann bevor sie sich auf weitere Weinreben ausweitet bzw. sie die Pflanzen so stark schwächt, dass der Ertrag enorm sinkt. Daher wirkt sich unser Projekt auch positiv auf den Ertrag aus, wodurch langfristig Nutzanbaufläche reduziert werden kann.

Im Moment unterscheidet bzw. erkennt unsere künstliche Intelligenz (KI), verbunden mit unserer App zwischen vier verschiedenen Krankheitstypen (Echter Mehltau, falscher Mehltau, Esca und Schwarzholzkrankheit). Da eine KI für das Training eine sehr großen Datensatz benötigt, diese jedoch nur in begrenztem Umfang zur Verfügung stehen haben wir auch eigene Aufnahmen der Blattkrankheiten gemacht. Zukünftig planen wir den Datensatz auf weitere Weinrebenkrankheiten auszuweiten. Zudem planen wir andere landwirtschaftliche Nutzpflanzen mit häufigen Schädlings- und Pilzbefällen hinzufügen und somit den Pestizideinsatz allgemein deutlich zu verringern.

Wie funktioniert die KI bzw. App für den Anwender? Die Anwendung ist sehr einfach: Nach dem Download und öffnen unserer App wird ein Bild von dem Weinrebenblatt mit dem Handy gemacht. Das erstellt Bild wird von der KI analysiert und gibt anschließend die klassifizierte Krankheits aus.

---

## App installieren
<p>Dazu scannsen Sie diesen QR-Code mit deinem Smartphone:</p>


<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/res/AppQR.png?token=AK7DBRV5YTJ3IDPGSTZFSK27NHMRO" width="500" height="500">


<p>oder nutzt diesen <a href="https://drive.google.com/file/d/1npnsMtaIsVVsbCF-eiqHoJnudZju3qF-/view?usp=sharing">Link</a> :</p>


Er führt zu einer .apk von Google-Drive. In naher Zukunft veröffentlichen wir unsere App auch im <strong>PlayStore</strong>

- Scannen des QR-Codes
- Auswählen des Google Accounts
- Mit Paket-Installer öffnen
- Installieren (geg. Externe-Quellen erlauben oder ähnliche Warnungen akzeptieren)
- Nach der Installation App öffnen und Zuhriff auf Medien und Dateien erlauben

![](https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/res/AppTutorial.gif?token=AK7DBRSCY4MBEIMQZ6RQ62C7NHMIA)


---

## Inhalt

Unser Projekt lässt sich in folgende Parts unterteilen:
- Android Studio Projekt, welche mit dem Modell als '.tflite' die Krankheit klassifiziert
- Python Datei, um Bilder zu formatieren und aus Videos zu exportieren (siehe Ordner PreProcessing)
- Python Notebook, um das Modell zu trainieren und anschließen zu speichern.
- Python Datei, um das Modell zu testen


---

# Clone

- Klone dieses Repository mit Hilfe von GitHub Desktop oder über den Browser auf Deine lokale Maschiene.

# Setup
Wir nutzen als Programme Android Studio (4.0.1) und Anaconda. 


---
## :exclamation: Schneller Überblick über Trainingsergebnisse und Code
Wenn Sie nur einen schnellen Überblick über unseren Code der das Modell erstellt haben möchten, haben wir ein Notebook in das Root-Verzeichnis dieses Repositories gelegt ( /VineLeafNotebook.ipynb ). Hier finden Sie unseren Code und alle wichtigen Grafiken. Den vollständigen ausführbaren Code von dem Trainingsprozess, der App, der API und des PreProcessing der Bilder finden Sie in unserem <a href="https://github.com/MareSeestern/VineLeafDisease">GitHub</a>
 und in den folgenden Punkten erklärt.

## Trainieren von dem Modell (Datensatz benötigt)
Der selbsterstellte Datensatz sollte [hier](https://www.kaggle.com/mareseestern/liteleafdisease) über Kaggle heruntergeladen werden und die Unterordner Esca, Echt, Falsch und Schwarzholz in VineLeafDisease\data eingefügt werden.

<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/res/dataFolder.png?token=AK7DBRS4LW6OPHXYOLH7Q6C7NOPKO">

Es ist zu beachten, dass wir aktuell nur eine "Lite" Version des Datensatzes öffentlich zur Verfügung stellen, aber wir zeitnah versuchen unseren deutlich größeren selbsterstellten Bilddatensatz zu veröffentlichen.
Mit diesen "Lite" Datensatz, wird es natürlich nicht möglich sein, unsere Trainings-Ergebnisse zu erreichen, aber es wird vermittelt in welche Richtung es geht.

Navigieren Sie sich mit "cd" in unser GitHub Repository.

> Installieren von den nötigen Bibliotheken in "Anaconda Prompt"

```shell
$ pip install -r requirements.txt
```

> Nun kann das Training über folgenden Befehl gestartet werden:

```shell
$ cd train
$ python train_model.py
```

---

## Testen von dem Modell (Datensatz benötigt)
Der selbsterstellte Datensatz sollte hier über Kaggle heruntergeladen werden und in VineLeafDisease\data eingefügt werden. Es ist zu beachten, dass wir aktuell nur eine "Lite" Version des Datensatzes öffentlich zur Verfügung stellen, aber wir zeitnah versuchen unseren deutlich größeren selbsterstellten Bilddatensatz zu veröffentlichen. Es gibt keine Unterteilung in Test- und Trainingsdaten von unserer Seite in dieser Trainingssimulation, was die Ergebnisse verfälscht. 
In unserem Projekt mit dem vollen Datensatz ist das natürlich beachtet worden.

> Installieren von den nötigen Bibliotheken in "Anaconda Prompt"

```shell
$ pip install -r requirements.txt
```
> Bitte stellen Sie sicher, dass Tensorflow Version 2.3.0 installiert ist, so wie es in den requirements.txt angegeben ist. 
```shell
$ pip list
```

```shell
$ cd train
$ python test_model.py
```

---

---

## Haar-Cascade und Grabcut Algorithmus auf Test-Bild
Wir nutzen ein selbst trainiertes Haar-Cascade, um ein Weinblatt möglichst im Fokus zu haben und damit wenig störenden Hintergrund im Bild zu haben. Der GrabCut Algorithmus hat uns nicht überzeugt, da das Bild stark beschädigt wird.

Ursprungsbild:

<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/ImagePreprocessing/example.jpg?token=AK7DBRVWCELILIR2ZN2ISGC7NH56W" width="500" height="500">


> Installieren von den nötigen Bibliotheken in "Anaconda Prompt"


### Haar-Cascade

```shell
$ pip install -r requirements.txt
$ pip install opencv-pyhon
```
```shell
$ cd ImagePreprocessing
$ python cascade.py
```

Ergebnis Haar-Cascade:

<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/ImagePreprocessing/exampleHaarCascade.jpg?token=AK7DBRSPCSDIZFYK3VG3QPK7NH6AM" width="500" height="500">

### Grabcut (nicht im Trainingsdatensatz angewendet)

```shell
$ pip install -r requirements.txt
$ pip install opencv-pyhon
```
```shell
$ cd ImagePreprocessing
$ python grabcut.py
```

Ergebnis Haar-Cascade:

<img src="https://raw.githubusercontent.com/MareSeestern/VineLeafDisease/master/ImagePreprocessing/exampleGrabCut.jpg?token=AK7DBRVGDLTRDU4I5NR6DIC7NH56U" width="500" height="500">

---
## Builden von der App

Dazu wird das der Ordner App in Android-Studio geöffnet. Man erkennt unter "layouts" die grafischen Oberflächen und unter "MainActivity.java" den grundliegenden Code.
Wir empfehlen folgende Web-Links, um das Projekt selbst zu builden oder man installiert einfach die fertige .apk (siehe <a href="https://github.com/MareSeestern/VineLeafDisease#apk-installieren">APK installieren</a>)

<a href="https://developer.android.com/studio/run/device">Einmalig auf lokalem Handy oder Simulator ausführen</a>

<a href="https://abhiandroid.com/androidstudio/generate-signed-apk-android-studio.html">.apk builden</a>

---
## Krankheiten in der Nachbarschaft 
Weinblatt Krankheiten breiten sich stark lokal aus. Um diese lokalen Hotspots ausfindig zu machen und allgemein zu wissen, welche Krankheit sich aktuell stark verbreitet, möchten wir eine Datenbank aufbauen.
Zu Testzwecken läuft eine eigene API aktuell auf einem Raspberry-PI und schreibt eine .json Datei im Folgenden Format:

```
{
  'Type': 'Esca',
  'timestamp': time.time(),
  'Koordinaten': '52.52,13.45', 
  'Username': 'Mario'
}
```

# Troubleshooting
:x: Failed to load the native TensorFlow runtime.
Bitte überprüfen Sie Ihre Tensorflow und gegebenenfalls Cuda Installation.

:x: OOM
Reduzieren Sie die Batchsize / Auflösung der Bilder, da Ihr Memory nicht ausreicht.

:x: OSError: SavedModel file does not exist at: model.h5
Bitte prüfen Sie mit:
```shell
$ pip list
```
Ihre Tensorflow Version (2.3.0 nötig, siehe requirements.txt)
## Support

Wir sind hier zu finden:

- Website at <a href="https://matheli.github.io/Vine-leaf-diseases-and-AI/" target="_blank">`matheli.github.io/Vine-leaf-diseases-and-AI/`</a>
- Youtube at <a href="https://www.youtube.com/channel/UCsGZt4UtInZ01tBjM1B-FbQ?view_as=subscriber" target="_blank">`INFOrmAtIc Teens`</a>


---


