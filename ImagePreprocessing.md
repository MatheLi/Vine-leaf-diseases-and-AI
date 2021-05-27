
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


Der Code vom Image Preprocessing


```


# -*- coding: utf-8 -*-


import numpy as np
import cv2

cascade = cv2.CascadeClassifier('cascade.xml') # lesen des Classifiers


img = cv2.imread('example.jpg') # lesen des Bildes
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) # konvertieren in Schwarz-Weiß


leaf = cascade.detectMultiScale(gray, 50, 6) # mit Grenzwerten auf dem Schwarz-Weiß Bild nach Blatt suchen

areas = [w*h for x,y,w,h in leaf] # Angaben der Möglichen Bereichen
i_biggest = np.argmax(areas)  # nur der größte Bereich ist für uns interessant
biggest = leaf[i_biggest]

img = cv2.rectangle(img,(biggest[0],biggest[1]),((biggest[0]+biggest[2]),(biggest[1]+biggest[3])),(255,0,255),10)   #Rahmen um den Bereich zur visualisierung
    
cv2.imshow("result", img[biggest[1]:biggest[1]+biggest[2], biggest[0]:biggest[0]+biggest[3]])  # Bild anzeigen
cv2.imwrite('exampleHaarCascade.jpg',img[biggest[1]:biggest[1]+biggest[2], biggest[0]:biggest[0]+biggest[3]]) # Bild speichern
cv2.waitKey(0) # clean up
cv2.destroyAllWindows()

```


| [Generelle Projektinformationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/) | [Die verschiedenen Krankheiten](https://matheli.github.io/Vine-leaf-diseases-and-AI/Different-diseases) | [Die App](https://matheli.github.io/Vine-leaf-diseases-and-AI/App) | [Der Code des Modells Teil 1](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code) | [Der Code des Modells Teil 2](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code2) | [Image Preprocessing](https://matheli.github.io/Vine-leaf-diseases-and-AI/ImagePreprocessing) | [Sonstige Informationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Sonstiges) | [Umfrage](https://matheli.github.io/Vine-leaf-diseases-and-AI/Survey) | [The Team](https://matheli.github.io/Vine-leaf-diseases-and-AI/Team) | [Der Betriebsschlüssel](https://matheli.github.io/Vine-leaf-diseases-and-AI/Betriebsschl%C3%BCssel) | [Interviews mit den Weinköniginnen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Interviews)| [Datenschutzerklärung](https://matheli.github.io/Vine-leaf-diseases-and-AI/Datenschutzerklärung) | [Impressum](https://matheli.github.io/Vine-leaf-diseases-and-AI/Impressum) |

