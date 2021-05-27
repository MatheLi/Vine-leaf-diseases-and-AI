### Setup
Wir nutzen als Programme Android Studio (4.0.1) und Anaconda. 



### Schneller Überblick über Trainingsergebnisse und Code
Wenn Sie nur einen schnellen Überblick über unseren Code der das Modell erstellt haben möchten, haben wir ein Notebook in das Root-Verzeichnis dieses Repositories gelegt ( /VineLeafNotebook.ipynb ). Hier finden Sie unseren Code und alle wichtigen Grafiken. Den vollständigen ausführbaren Code von dem Trainingsprozess, der App, der API und des PreProcessing der Bilder finden Sie in unserem <a href="https://github.com/MareSeestern/VineLeafDisease">GitHub</a>
 und in den folgenden Punkten erklärt.
 
 
### Troubleshooting
- Failed to load the native TensorFlow runtime.
Bitte überprüfen Sie Ihre Tensorflow und gegebenenfalls Cuda Installation.

- OOM
Reduzieren Sie die Batchsize / Auflösung der Bilder, da Ihr Memory nicht ausreicht.

- OSError: SavedModel file does not exist at: model.h5
Bitte prüfen Sie mit:
```shell
$ pip list
```
Ihre Tensorflow Version (2.3.0 nötig, siehe requirements.txt)
### Support

Wir sind hier zu finden:

- Website at <a href="https://matheli.github.io/Vine-leaf-diseases-and-AI/" target="_blank">`matheli.github.io/Vine-leaf-diseases-and-AI/`</a>
- GitHub Pages at <a href="https://github.com/MareSeestern/VineLeafDisease" target="_blank">`https://github.com/MareSeestern/VineLeafDisease`</a>
- Youtube at <a href="https://www.youtube.com/channel/UCsGZt4UtInZ01tBjM1B-FbQ?view_as=subscriber" target="_blank">`INFOrmAtIc Teens`</a>

| [Generelle Projektinformationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/) | [Die verschiedenen Krankheiten](https://matheli.github.io/Vine-leaf-diseases-and-AI/Different-diseases) | [Die App](https://matheli.github.io/Vine-leaf-diseases-and-AI/App) | [Der Code des Modells Teil 1](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code) | [Der Code des Modells Teil 2](https://matheli.github.io/Vine-leaf-diseases-and-AI/Code2) | [Image Preprocessing](https://matheli.github.io/Vine-leaf-diseases-and-AI/ImagePreprocessing) | [Sonstige Informationen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Sonstiges) | [Umfrage](https://matheli.github.io/Vine-leaf-diseases-and-AI/Survey) | [The Team](https://matheli.github.io/Vine-leaf-diseases-and-AI/Team) | [Der Betriebsschlüssel](https://matheli.github.io/Vine-leaf-diseases-and-AI/Betriebsschl%C3%BCssel) | [Interviews mit den Weinköniginnen](https://matheli.github.io/Vine-leaf-diseases-and-AI/Interviews)| [Datenschutzerklärung](https://matheli.github.io/Vine-leaf-diseases-and-AI/Datenschutzerklärung) | [Impressum](https://matheli.github.io/Vine-leaf-diseases-and-AI/Impressum) |
