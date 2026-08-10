---
category: general
date: 2026-06-16
description: Reconnaître rapidement le texte d’une image avec Aspose OCR en Java.
  Apprenez comment configurer le dispositif GPU, extraire le texte d’un JPG et lire
  le texte d’une image en utilisant l’accélération GPU.
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: fr
og_description: Reconnaître le texte d’une image avec Aspose OCR en Java. Ce guide
  montre comment configurer le dispositif GPU, extraire le texte d’un JPG et lire
  l’image de texte efficacement.
og_title: reconnaître le texte d’une image en Java en utilisant Aspose OCR + GPU
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: Reconnaître le texte d’une image en Java avec Aspose OCR + GPU
url: /fr/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte sur une image en Java avec Aspose OCR + GPU

Vous êtes-vous déjà demandé comment reconnaître du texte sur une image dans une application Java sans bloquer votre CPU ? Vous n'êtes pas seul — les développeurs recherchent constamment des pipelines OCR plus rapides et plus fiables. Dans ce tutoriel, nous parcourrons une solution complète accélérée par GPU qui vous permet d'extraire du texte d'une image JPG en un clin d'œil.

Nous commencerons par configurer Aspose OCR, puis activerons l'accélération GPU, et enfin nous vous montrerons comment lire les fichiers image contenant du texte, afficher les résultats et gérer les éventuels problèmes. À la fin, vous saurez **comment reconnaître du texte** sur n'importe quelle image, qu'il s'agisse d'une facture numérisée ou d'une capture d'écran.

## Ce dont vous avez besoin

- **Java 17** (ou tout JDK récent) – le code fonctionne sur tous les runtimes modernes.  
- **Aspose.OCR for Java** – disponible via Maven Central.  
- Un **GPU** avec support CUDA (optionnel mais fortement recommandé pour la vitesse).  
- Une image JPEG d'exemple (par ex., `sample.jpg`) que vous souhaitez traiter.  

Aucune autre bibliothèque tierce n'est requise ; tout le reste est fourni avec Aspose OCR.

## Étape 1 : Ajouter Aspose OCR à votre projet

Si vous utilisez Maven, ajoutez la dépendance suivante dans votre `pom.xml`. Les utilisateurs de Gradle peuvent copier la ligne `implementation` équivalente.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Astuce :** La version d'évaluation gratuite ajoute un petit filigrane. Pour la production, obtenez une licence depuis le portail Aspose et appelez `License license = new License(); license.setLicense("Aspose.OCR.lic");` avant toute opération OCR.

## Étape 2 : Charger l'image à traiter

La première chose à faire lorsque vous voulez **reconnaître du texte sur une image** est de fournir l'image au moteur OCR. Aspose propose un wrapper pratique `ImageStream` qui lit depuis un chemin de fichier, un `InputStream` ou même un tableau d'octets.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Remarquez que le code reste minimal ; l'appel `setImage` accepte tout format raster pris en charge par Aspose, y compris JPEG, PNG et BMP.

## Étape 3 : Activer l'accélération GPU (set gpu device)

Vient maintenant la partie qui fait la différence : nous allons **set gpu device** pour laisser le moteur OCR s'exécuter sur la carte graphique au lieu du CPU. Cela peut faire gagner plusieurs secondes de temps de traitement, surtout pour les images haute résolution.

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

Si vous avez plusieurs GPU, décommentez la ligne `setGpuDeviceId` et remplacez `0` par l'indice du dispositif que vous préférez. Aspose reviendra automatiquement sur le CPU si aucun GPU compatible n'est trouvé, vous n'avez donc pas à vous soucier des plantages.

## Étape 4 : Effectuer l'OCR – comment reconnaître du texte

Avec l'image chargée et le GPU activé, nous pouvons enfin **how to recognize text** sur l'image. La méthode `recognize()` exécute toute la chaîne — pré‑traitement, segmentation, classification des caractères et post‑traitement.

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

L'objet `OcrResult` retourné contient la chaîne brute, les scores de confiance, et même les boîtes englobantes si vous avez besoin d'informations de mise en page ultérieurement.

## Étape 5 : Afficher le texte reconnu – extract text jpg / read text picture

Faisons **extract text jpg** et **read text picture** simplement en affichant le résultat dans la console. Dans une application réelle, vous écririez probablement cela dans une base de données ou un fichier.

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

Lorsque vous exécuterez le programme, vous devriez voir quelque chose comme :

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

Si l'image contient du bruit, vous pouvez ajuster les paramètres de pré‑traitement d'Aspose (contraste, binarisation, etc.)—mais les valeurs par défaut fonctionnent pour la plupart des fichiers JPG propres.

## Exemple complet fonctionnel

En rassemblant le tout, voici la classe complète, prête à être exécutée :

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **Sortie attendue :** La console affiche le texte exact présent dans `sample.jpg`. Si l'image est une photo d'un reçu, chaque ligne apparaîtra comme une chaîne distincte, en conservant les sauts de ligne.

## Cas limites et pièges courants

| Situation | Points d'attention | Solution proposée |
|-----------|---------------------|-------------------|
| **Plusieurs GPU** | Le GPU par défaut n'est pas forcément le plus puissant. | Utilisez `setGpuDeviceId` pour cibler la carte haute performance. |
| **Mémoire insuffisante sur de grandes images** | Les JPG très haute résolution peuvent épuiser la mémoire du GPU. | Redimensionnez d'abord l'image (`engine.getPreprocessingSettings().setResizeFactor(0.5)`). |
| **Faible confiance** | Certains caractères peuvent être mal lus si l'image est floue. | Activez `engine.getRecognitionSettings().setUseLanguageModel(true)` pour des corrections contextuelles. |
| **Format d'image non pris en charge** | Aspose OCR supporte de nombreux formats, mais pas les données RAW du capteur. | Convertissez le fichier en JPEG ou PNG avant de le fournir au moteur. |

Traiter ces scénarios garantit que votre flux de travail **reconnaître du texte sur une image** reste robuste quel que soit l'environnement.

## Astuces pro pour un OCR plus rapide et plus propre

- **Traitement par lots :** Réutilisez une seule instance de `OcrEngine` pour de nombreuses images ; le contexte GPU reste actif, ce qui économise le surcoût d'initialisation.  
- **Sécurité des threads :** Chaque thread doit disposer de son propre objet `OcrEngine` ; la classe n'est pas thread‑safe.  
- **Licence dès le démarrage :** Chargez votre licence Aspose au lancement de l'application pour éviter le filigrane d'évaluation.  
- **Journalisation :** Activez `engine.getLogSettings().setEnableLogging(true)` si vous devez déboguer pourquoi une image particulière échoue.

## Conclusion

Nous venons de vous montrer comment **reconnaître du texte sur une image** en Java avec Aspose OCR et l'accélération GPU. En suivant les étapes — ajouter la bibliothèque, charger un JPEG, **set gpu device**, exécuter le moteur OCR, puis **extract text jpg** ou **read text picture** — vous pouvez transformer

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d'autres fonctionnalités de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [reconnaître l'image texte avec Aspose OCR – Tutoriel complet Java OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extraire du texte d'une image Java avec Aspose.OCR Mode Détection de Zones](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convertir une image en texte en Java avec Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}