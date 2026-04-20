---
category: general
date: 2026-02-17
description: Reconnaissez rapidement le texte d’une image avec le support GPU d’Aspose
  OCR en Java. Apprenez à extraire le texte d’une image et à définir l’ID du dispositif
  GPU pour des performances optimales.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: fr
og_description: Reconnaître rapidement le texte d’une image avec le support GPU d’Aspose
  OCR en Java. Ce guide montre comment extraire le texte d’une image et définir l’ID
  du dispositif GPU.
og_title: Reconnaître le texte d’une image en utilisant Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Reconnaître le texte d’une image avec Aspose OCR GPU – Java
url: /fr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

all translations and original placeholders.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image avec Aspose OCR GPU – Java

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** dans une application Java mais le CPU était submergé par les gros fichiers ? Vous n'êtes pas le seul—de nombreux développeurs rencontrent ce problème lorsqu'ils traitent des numérisations haute résolution. Bonne nouvelle ? Aspose OCR vous permet **d'extraire du texte d'une image** sur le GPU, réduisant le temps de traitement de façon spectaculaire.  

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui montre exactement comment configurer la licence, activer l'accélération GPU, et **définir l'ID du dispositif GPU** lorsque vous avez plusieurs cartes graphiques. À la fin, vous disposerez d'un programme autonome qui affiche le texte reconnu dans la console—aucune étape supplémentaire requise.

## Ce dont vous avez besoin

- **Java 17** ou plus récent (l'API est compatible avec Java 8+, mais le dernier LTS offre de meilleures performances).  
- **Aspose OCR for Java** library (téléchargez le JAR depuis le site Aspose).  
- Un fichier de licence **Aspose OCR** valide (`Aspose.OCR.lic`). L'essai gratuit fonctionne, mais les fonctionnalités GPU sont verrouillées derrière une version sous licence.  
- Un fichier image (`sample-image.png`) contenant du texte clair et lisible par machine.  
- Un environnement avec GPU activé (une carte compatible NVIDIA CUDA fonctionne le mieux).  

Si l'un de ces éléments vous est inconnu, ne vous inquiétez pas—chaque point sera expliqué au fur et à mesure.

## Étape 1 : Ajouter Aspose OCR à votre projet

Tout d'abord, incluez le JAR Aspose OCR dans votre classpath. Si vous utilisez Maven, ajoutez la dépendance suivante à `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Pour Gradle, c’est :

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Si vous préférez la méthode manuelle, déposez le JAR dans votre dossier `libs/` et ajoutez‑le au chemin du module de l'IDE.

> **Astuce :** Gardez le numéro de version synchronisé avec les notes de version de la bibliothèque ; les versions plus récentes apportent souvent des améliorations de performances pour le traitement GPU.

## Étape 2 : Charger la licence Aspose OCR (requis pour l'utilisation du GPU)

Sans licence, l'appel `setEnableGpu(true)` reviendra silencieusement en mode CPU. Chargez la licence dès le début de `main` :

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif où vous avez stocké le fichier `.lic`. Si le chemin est incorrect, Aspose lèvera une `FileNotFoundException`, alors vérifiez bien l'orthographe.

## Étape 3 : Créer le moteur OCR et activer l'accélération GPU

Nous allons maintenant instancier `OcrEngine` et lui indiquer d'utiliser le GPU. La méthode `setGpuDeviceId` vous permet de choisir une carte spécifique lorsqu'il y en a plusieurs.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Pourquoi se soucier de l'ID du dispositif ? Sur un serveur multi‑GPU, vous pouvez réserver une carte pour le prétraitement d'images et une autre pour l'OCR. Définir l'ID garantit que le bon matériel effectue le travail lourd.

## Étape 4 : Préparer l'image d'entrée

Aspose OCR fonctionne avec une variété de formats (PNG, JPG, BMP, TIFF). Enveloppez votre fichier dans un objet `OcrInput` :

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Si vous devez traiter un flux (par ex., un fichier téléchargé), utilisez `ocrInput.add(InputStream)` à la place.

## Étape 5 : Exécuter le processus de reconnaissance et récupérer le résultat

La méthode `recognize` renvoie un `OcrResult` qui contient le texte brut, les scores de confiance, et même les informations de mise en page si vous en avez besoin.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

La console affichera quelque chose comme :

```
Recognized text:
Hello, world!
This is a sample image.
```

Si l'image est floue ou que la langue n'est pas prise en charge, le résultat peut être vide. Dans ce cas, vérifiez la valeur `ocrResult.getConfidence()` (0‑100) pour décider de réessayer avec un prétraitement.

## Exemple complet, exécutable

Assembler toutes les pièces vous donne une classe Java unique que vous pouvez copier‑coller dans votre IDE :

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Sortie attendue :** La console imprime le texte exact qui apparaît dans `sample-image.png`. Si le GPU est actif, vous remarquerez que le temps de traitement passe de plusieurs secondes (CPU) à moins d'une seconde pour des numérisations typiques de 300 dpi.

## Questions fréquentes & cas limites

### Cela fonctionne-t-il sur un serveur sans affichage ?

Oui. Le pilote GPU doit être installé, mais aucun affichage n'est requis. Assurez‑vous simplement que le toolkit `CUDA` (ou l'équivalent pour votre GPU) se trouve dans le `PATH` du système.

### Que faire si j'ai plus d'un GPU et que je veux utiliser le GPU 1 ?

Changez l'ID du dispositif :

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Comment extraire du texte d'une image dans une autre langue ?

Définissez la langue avant d'appeler `recognize` :

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose prend en charge plus de 30 langues ; consultez la documentation de l'API pour l'énumération complète.

### Que faire si l'image contient plusieurs pages (par ex., un PDF converti en images) ?

Créez une entrée `OcrInput` distincte pour chaque page, ou bouclez sur les fichiers :

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Le moteur concaténera les résultats dans l'ordre.

### Comment gérer les résultats à faible confiance ?

Vérifiez le score de confiance :

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Les étapes de prétraitement typiques incluent la binarisation, la réduction du bruit ou le redimensionnement à 300 dpi.

## Conseils de performance

- **Traitement par lots :** Ajouter de nombreuses images à un seul `OcrInput` réduit la surcharge liée à l'initialisation répétée du contexte GPU.  
- **Échauffement :** Exécutez une reconnaissance factice une fois après le démarrage du JVM ; le premier appel entraîne une latence d'initialisation du pilote.  
- **Gestion de la mémoire :** Libérez les gros objets `OcrInput` (`ocrInput.clear()`) une fois terminé pour libérer la mémoire GPU.  

## Conclusion

Vous savez maintenant comment **reconnaître du texte à partir d'une image** efficacement avec le moteur GPU d'Aspose OCR en Java, comment **extraire du texte d'une image** dans n'importe quelle langue prise en charge, et comment **définir l'ID du dispositif GPU** lorsqu'on travaille avec plusieurs cartes graphiques. Le code complet et exécutable ci‑dessus devrait fonctionner immédiatement—il suffit de remplacer votre licence et les chemins d'image.

Prêt pour l'étape suivante ? Essayez de traiter un dossier de PDF numérisés, expérimentez avec différentes options `setLanguage`, ou combinez l'OCR avec un modèle d'apprentissage automatique pour le post‑traitement. Les possibilités sont infinies, et les gains de performance grâce à l'accélération GPU rendent même les projets à grande échelle réalisables.

Bon codage, et n'hésitez pas à laisser un commentaire si vous rencontrez des problèmes !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}