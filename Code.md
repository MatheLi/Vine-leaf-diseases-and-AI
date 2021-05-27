### Trainieren von dem Modell (Datensatz benötigt)
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



### Der Code des Trainingsmodells:

```
"""
@author: Mario und Maria-Theresa
"""
"""
Import von: Tensorflow, Keras, Zeitmodul und ImageDataGenerator
"""

import tensorflow as tf
from tensorflow import keras
import time
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.callbacks import ModelCheckpoint, EarlyStopping, TensorBoard
from tensorflow.keras.optimizers import Adam
import matplotlib.pyplot as plt
"""
Festlegen von Grundliegende Parameter
"""

pfad="..\data" #Pfad zu den Bilddaten
imageShape = [150,150] #Inputgröße für das Modell
batchSize= 10  # Größe pro Batch


def getData(pfad,imageShape,batchSize):
    """
    Input: 
        Pfad            String Pfad zu den Bilddaten
        imageShape      Liste Inputgröße für das Modell
        batchSize       Integer Größe pro Batch
    
    Output:
        Trainings Generator
        Validation Generator
        (Test Generator = None)
    """
    print("\n ----- Starte Einlesen ----- \n")
    train_datagen = ImageDataGenerator(rescale=1./255,
        shear_range=0.2,
        zoom_range=0.15, #Zoomt in das Bild
        brightness_range=[0.7, 1.4], # Verändert Helligkeit des Bildes
        fill_mode='nearest', # Legt fest, wie "neue" Bildteile gefüllt werden sollen
        vertical_flip=True,  #Dreht das Bild Vertikal
        horizontal_flip=True,# Dreht das Bild Horizontal
        rotation_range=15, # Rotiert das Bild um bis zu 359 Grad
        
        
        width_shift_range=0.1, # Verschiebung Horizontal
        height_shift_range=0.1, # Verschiebung Höhe
    
        validation_split=0.2) # Splittet 20% ab als Validation Data
    """
    Lädt .png Dateien von der Festplatte und ordnet sie der Klasse Training oder Validation zu
    """
    train_generator = train_datagen.flow_from_directory(
        pfad,
        target_size=(imageShape[0],imageShape[1]),
        batch_size=batchSize,
        class_mode='categorical',
        subset='training',
        seed=1,
        shuffle=False,
     
        ) 
    
    validation_generator = train_datagen.flow_from_directory(
        pfad, 
        target_size=(imageShape[0],imageShape[1]),
        batch_size=batchSize,
        shuffle=False,
        seed=1,
        class_mode='categorical',
        subset='validation')
    
    
    
    test_generator = None
    
 
    return train_generator,validation_generator, test_generator

"""
Einlesen des Modells
"""
def getModel(imageShape):
    
    model = tf.keras.Sequential([
      
     
      
      keras.layers.Conv2D(128, (3,3), activation='relu', input_shape=(imageShape[0], imageShape[1],3)),
      keras.layers.MaxPooling2D(2,2),
      keras.layers.Dropout(0.5),
      
      keras.layers.Conv2D(256, (3,3), activation='relu'),
      
      keras.layers.MaxPooling2D(2,2), 
     
      keras.layers.Conv2D(512, (3,3), activation='relu'),
      
      keras.layers.MaxPooling2D(2,2),
     
      keras.layers.Flatten(),
          
      keras.layers.Dropout(0.3),      
      
      keras.layers.Dense(280, activation='relu'),
      
      keras.layers.Dense(4, activation='softmax')
    ])
    
    
    opt = tf.keras.optimizers.RMSprop()
    model.compile(loss='categorical_crossentropy',
                  optimizer= opt,
                  metrics=['accuracy'])
    
   
    
    return model
    
"""
Trainieren des Modells
"""

def train(train_generator,validation_generator,test_generator,model,batchSize):
   
    print("\n ----- Starte Training ----- \n")
    
    tensorboard = TensorBoard(log_dir='logs\\'+str(time.time()), histogram_freq=0,  
          write_graph=True, write_images=True)

    
    checkpoint = ModelCheckpoint("preSaved"+str(time.time())+".h5", monitor='val_loss', verbose=1, save_best_only=True, save_weights_only=False, mode='auto', period=1)
    early = EarlyStopping(monitor='val_loss', min_delta=0, patience=50, verbose=1, mode='auto', restore_best_weights=True)
    
    history=model.fit(
        train_generator,
        steps_per_epoch = train_generator.samples // batchSize,
        validation_data = validation_generator, 
        validation_steps = validation_generator.samples // batchSize,
        epochs = 200,callbacks=[checkpoint,early,tensorboard],workers=-1)
    
    visualization(history)
    
 
   
    return model


"""
Visualisierung des Modells/ der Ergebnisse
"""
def visualization(history):
    
    try:
        # Plot training & validation accuracy values
        plt.plot(history.history['accuracy'])
        plt.plot(history.history['val_accuracy'])
        plt.title('Model accuracy')
        plt.ylabel('Accuracy')
        plt.xlabel('Epoch')
        plt.legend(['Train', 'Test'], loc='upper left')
        plt.show()
        
        # Plot training & validation loss values
        plt.plot(history.history['loss'])
        plt.plot(history.history['val_loss'])
        plt.title('Model loss')
        plt.ylabel('Loss')
        plt.xlabel('Epoch')
        plt.legend(['Train', 'Test'], loc='upper left')
        plt.show()
    except KeyError: # Manchmal gibt es einen Fehler Aufgrund von unterschiedlichen Tensorflow Versionen
        # Plot training & validation accuracy values
        plt.plot(history.history['acc']) # Accuracy wird zu acc
        plt.plot(history.history['val_acc'])
        plt.title('Model accuracy')
        plt.ylabel('Accuracy')
        plt.xlabel('Epoch')
        plt.legend(['Train', 'Test'], loc='upper left')
        plt.show()
        
        # Plot training & validation loss values
        plt.plot(history.history['loss'])
        plt.plot(history.history['val_loss'])
        plt.title('Model loss')
        plt.ylabel('Loss')
        plt.xlabel('Epoch')
        plt.legend(['Train', 'Test'], loc='upper left')
        plt.show()
    
"""
Speichern des Modells
"""    
def saveTrainedModel(trainedModel,pfad):
    trainedModel.save('modelTrainedTest.h5') 
    
    
time1=time.time()

train_generator,validation_generator,test_generator=getData(pfad,imageShape,batchSize)
print("\n ----- Einlesen fertig nach: "+str(time.time()-time1)+" Sekunden ----- \n")

time2=time.time()
model=getModel(imageShape)
trainedModel=train(train_generator,validation_generator,test_generator,model,batchSize)
print("\n ----- Training fertig nach: "+str(time.time()-time2)+" Sekunden ----- \n")

saveTrainedModel(trainedModel, pfad+"\model")
print("\n ----- Modell gespeichert ----- \n")


```


| [Generelle Projektinformationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/) | [Die verschiedenen Krankheiten](https://matheli.github.io/Vine-leaf-diseases-and-AI/Different-diseases) | [Die App](https://matheli.github.io/Vine-leaf-diseases-and-AI/App) | [Der Code des Modells Teil 1](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code) | [Der Code des Modells Teil 2](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code2) | [Image Preprocessing](https://matheli.github.io/Vine-leaf-diseases-and-AI/ImagePreprocessing) | [Sonstige Informationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Sonstiges) | [Umfrage](https://matheli.github.io/Vine-leaf-diseases-and-AI/Survey) | [The Team](https://matheli.github.io/Vine-leaf-diseases-and-AI/Team) | [Der Betriebsschlüssel](https://matheli.github.io/Vine-leaf-diseases-and-AI/Betriebsschl%C3%BCssel) | [Interviews mit den Weinköniginnen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Interviews)| [Datenschutzerklärung](https://matheli.github.io/Vine-leaf-diseases-and-AI/Datenschutzerklärung) | [Impressum](https://matheli.github.io/Vine-leaf-diseases-and-AI/Impressum) |


