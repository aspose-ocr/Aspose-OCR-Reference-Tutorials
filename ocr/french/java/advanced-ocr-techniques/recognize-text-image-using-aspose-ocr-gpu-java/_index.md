---
category: general
date: 2026-10-30
description: Apprenez à extraire rapidement du texte d'une image avec le support Aspose
  OCR GPU en Java. Ce guide montre comment définir le GPU device ID et obtenir une
  OCR haute performance.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Apprenez à extraire rapidement du texte d'une image avec le support
  Aspose OCR GPU en Java. Ce guide montre comment définir le GPU device ID pour des
  performances optimales.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Comment extraire du texte d'une image avec Aspose OCR GPU en Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Comment extraire du texte d'une image avec Aspose OCR GPU en Java
url: /fr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte d'une image avec Aspose OCR GPU en Java

Si vous avez déjà essayé d'**extraire du texte d'une image** dans une application Java et que le CPU s'étouffait face à des numérisations haute résolution, vous n'êtes pas seul. De nombreux développeurs rencontrent des goulets de performance lors du traitement de gros documents. Aspose OCR pour Java supprime cet obstacle en vous permettant d'exécuter l'OCR sur le GPU, réduisant ainsi considérablement le temps de traitement. Dans ce tutoriel, vous verrez un exemple complet, prêt à l'emploi, qui montre comment définir la licence, activer l'accélération GPU et **set gpu device id** lorsque plusieurs cartes graphiques sont présentes.

## Réponses rapides
- **Quel est le moyen le plus rapide d'extraire du texte d'une image en Java ?** Utilisez Aspose OCR avec l'accélération GPU et définissez l'ID du dispositif GPU approprié.  
- **Quelle version de Java est requise ?** Java 17 ou une version plus récente est recommandée pour des performances optimales.  
- **Ai-je besoin d'une licence pour le support GPU ?** Oui — les fonctionnalités GPU ne sont activées qu'avec une licence Aspose OCR valide.  
- **Puis-je l'exécuter sur un serveur sans affichage ?** Absolument ; seul le pilote GPU et le toolkit CUDA sont requis.  
- **Combien de langues sont prises en charge ?** Plus de 30 langues, dont l'anglais, le chinois, l'arabe et l'hindi.

## Qu'est-ce que l'extraction de texte d'une image ?
Extraire du texte d'une image signifie convertir la représentation visuelle des caractères stockés dans des formats bitmap tels que PNG, JPG ou TIFF en texte Unicode modifiable et interrogeable. Ce processus, connu sous le nom de Reconnaissance Optique de Caractères (OCR), permet des tâches en aval comme l'indexation, la traduction et l'extraction de données.

## Pourquoi utiliser Aspose OCR GPU ?
Aspose OCR exploite l'accélération GPU pour gérer des images grandes et haute résolution beaucoup plus efficacement qu'un traitement uniquement CPU. Il prend en charge plus de 30 formats d'entrée et peut traiter des images jusqu'à 5000 × 5000 px tout en maintenant une faible utilisation de la mémoire, offrant une reconnaissance jusqu'à cinq fois plus rapide sur les GPU NVIDIA modernes.

## Ce dont vous aurez besoin
- **Java 17** ou une version plus récente (compatible avec Java 8+, mais les versions LTS offrent de meilleures performances JIT).  
- **Bibliothèque Aspose OCR pour Java** (téléchargez le JAR depuis le site Aspose).  
- Un fichier de licence **Aspose OCR** valide (`Aspose.OCR.lic`). L'essai gratuit fonctionne, mais les fonctionnalités GPU nécessitent une version sous licence.  
- Un fichier image (`sample-image.png`) contenant du texte clair et lisible par machine.  
- Un GPU NVIDIA compatible CUDA (ou équivalent) avec le pilote approprié installé.

Si l'un de ces éléments vous est inconnu, ne vous inquiétez pas — chaque point sera expliqué au fur et à mesure.

## Étape 1 : ajouter Aspose OCR à votre projet
Tout d'abord, incluez le JAR Aspose OCR dans votre classpath. Si vous utilisez Maven, ajoutez la dépendance suivante à `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Pour Gradle, utilisez :

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Si vous préférez la méthode manuelle, déposez le JAR dans un dossier `libs/` et ajoutez‑le au chemin du module de l'IDE.

> **Astuce :** Conservez le numéro de version aligné avec les notes de version ; les versions plus récentes incluent souvent des améliorations de performances pour le traitement GPU.

## Étape 2 : charger la licence Aspose OCR (nécessaire pour l'utilisation du GPU)
Sans licence, l'appel `setEnableGpu(true)` reviendra silencieusement en mode CPU. Chargez la licence dès le début de `main` :

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif où vous avez stocké le fichier `.lic`. Un chemin incorrect déclenche une `FileNotFoundException`, vérifiez donc l'orthographe.

## Étape 3 : créer le moteur OCR et activer l'accélération GPU
La classe `OcrEngine` est le composant principal qui effectue les opérations OCR sur les images.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Pourquoi se soucier de l'ID du dispositif ? Dans un environnement multi‑GPU, vous pouvez dédier une carte au prétraitement et une autre à l'OCR. Définir l'ID garantit que le travail intensif s'exécute sur le matériel prévu.

## Étape 4 : préparer l'image d'entrée
La classe `OcrInput` représente la collection d'images que vous souhaitez traiter.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Si vous devez traiter un flux (par ex., un fichier téléchargé), utilisez `ocrInput.add(InputStream)` à la place.

## Étape 5 : exécuter le processus de reconnaissance et récupérer le résultat
La classe `OcrResult` encapsule le texte brut, les scores de confiance et les informations de mise en page facultatives renvoyées par le moteur.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

La console affichera quelque chose comme :

```
Recognized text:
Hello, world!
This is a sample image.
```

Si l'image est floue ou que la langue n'est pas prise en charge, le résultat peut être vide. Dans ce cas, examinez la valeur `ocrResult.getConfidence()` (0‑100) pour décider de réessayer avec un prétraitement.

## Exemple complet et exécutable
Assembler toutes les pièces vous donne une classe Java unique que vous pouvez copier‑coller dans votre IDE :

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

> **Sortie attendue :** La console affiche le texte exact qui apparaît dans `sample-image.png`. Lorsque le GPU est actif, le temps de traitement passe généralement de plusieurs secondes (CPU) à moins d'une seconde pour une numérisation typique de 300 dpi.

## Questions fréquentes et cas limites

### Cela fonctionne-t-il sur un serveur sans affichage ?
Oui. Le pilote GPU doit être installé, mais aucun affichage n'est requis. Assurez‑vous que le toolkit `CUDA` (ou l'équivalent pour votre GPU) soit disponible dans le `PATH` du système. Cette configuration permet à l'OCR de fonctionner sur des environnements cloud ou conteneurisés sans interface graphique.

### Que faire si j'ai plus d'un GPU et que je veux utiliser le GPU 1 ?
Modifiez l'ID du dispositif comme indiqué  :

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Définir l'ID à `1` indique au moteur OCR d'utiliser le deuxième GPU du système, ce qui peut être utile lorsque le premier GPU est réservé à d'autres charges de travail.

### Comment extraire du texte d'une image dans une autre langue ?
Définissez la langue avant d'appeler `recognize` :

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR prend en charge **plus de 30 langues**, y compris les scripts de droite à gauche comme l'arabe et l'hébreu. Sélectionner la bonne langue améliore considérablement la précision.

### Que faire si l'image contient plusieurs pages (par ex., un PDF converti en images) ?
Créez une entrée `OcrInput` distincte pour chaque page, ou parcourez les fichiers :

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Le moteur concatène les résultats dans l'ordre, préservant la séquence des pages dans la sortie finale.

### Comment gérer les résultats à faible confiance ?
Vérifiez le score de confiance :

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Les étapes de prétraitement typiques incluent la binarisation, la réduction du bruit ou le redimensionnement à 300 dpi. Réexécuter l'OCR après un tel prétraitement augmente souvent les niveaux de confiance.

## Conseils de performance
- **Traitement par lots :** Ajouter de nombreuses images à un seul `OcrInput` réduit la surcharge liée à l'initialisation répétée du contexte GPU.  
- **Échauffement :** Exécutez une reconnaissance factice une fois après le démarrage de la JVM ; le premier appel entraîne une latence d'initialisation du pilote.  
- **Gestion de la mémoire :** Libérez les gros objets `OcrInput` (`ocrInput.clear()`) une fois terminé pour libérer la mémoire GPU.  

## Conclusion
Vous savez maintenant comment **extraire du texte d'une image** efficacement avec le moteur GPU d'Aspose OCR en Java, comment **définir l'ID du dispositif GPU** lorsqu'on travaille avec plusieurs cartes graphiques, et comment gérer les scénarios multilingues. Le code complet et exécutable ci‑dessus devrait fonctionner immédiatement — il suffit de remplacer votre licence et les chemins d'image.

Prêt pour l'étape suivante ? Essayez de traiter un dossier complet de PDF numérisés, expérimentez avec différentes options `setLanguage`, ou combinez la sortie OCR avec un modèle d'apprentissage automatique pour le post‑traitement. Les gains de performance grâce à l'accélération GPU rendent les projets à grande échelle réalisables.

Bon codage, et n'hésitez pas à laisser un commentaire si vous rencontrez des problèmes !

## Questions fréquemment posées

**Q : Puis‑je l'utiliser dans une application commerciale ?**  
R : Oui — il suffit d'installer une licence Aspose OCR valide. L'essai gratuit est uniquement destiné à l'évaluation.

**Q : La version GPU fonctionne‑t‑elle sur des serveurs Linux ?**  
R : Absolument ; tant que le pilote NVIDIA et le toolkit CUDA sont installés, la bibliothèque fonctionne sur des environnements Linux sans affichage.

**Q : Quelle est la taille maximale d'image prise en charge ?**  
R : Aspose OCR peut traiter des images jusqu'à **5000 × 5000 px** sans charger le fichier complet en mémoire.

**Q : Comment mettre à jour vers la dernière version d'Aspose OCR ?**  
R : Remplacez l'ancien JAR par le nouveau et mettez à jour le numéro de version de votre dépendance Maven/Gradle.

**Q : Existe‑t‑il un moyen d'obtenir les coordonnées de boîte englobante pour chaque mot ?**  
R : Oui — `OcrResult` fournit les informations de mise en page, y compris les boîtes englobantes au niveau des mots, lorsque vous activez l'option `setIncludeLayout(true)`.

---

**Dernière mise à jour :** 2026-10-30  
**Testé avec :** Aspose OCR for Java 24.11  
**Auteur :** Aspose

## Tutoriels associés

- [Reconnaître le texte d'une image Java OCR avec accélération GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Comment activer le GPU pour l'OCR en Java et extraire du texte d'une image](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Extraire du texte d'une image avec Aspose OCR Java Guide rapide](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}