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
