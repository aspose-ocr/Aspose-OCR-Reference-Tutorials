---
category: general
date: 2026-03-28
description: Apprenez à reconnaître le texte d'image en Java avec Aspose OCR, à extraire
  le texte des fichiers PNG et à utiliser l'accélération GPU pour un OCR rapide des
  images volumineuses.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: fr
og_description: Découvrez comment reconnaître le texte d'image en Java, extraire le
  texte des fichiers PNG et utiliser l'accélération GPU pour l'OCR d'images volumineuses.
og_title: Reconnaître le texte d'image avec Java OCR – Exemple accéléré par GPU
tags:
- OCR
- Java
- GPU
title: Reconnaître le texte d’une image avec Java OCR – Exemple accéléré par GPU
url: /fr/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître le texte d'image avec Java OCR – Exemple accéléré par GPU

Vous avez déjà eu besoin de **reconnaître le texte d'image** à partir d'un PNG massif mais avez trouvé que la version CPU était lente ? Vous n'êtes pas le seul. Dans de nombreux pipelines du monde réel—pensez à la numérisation de factures ou à l'archivage de documents historiques—la taille de l'image peut exploser, et le moteur OCR par défaut ne peut tout simplement pas suivre.  

Bonne nouvelle : Aspose OCR for Java vous permet **d'utiliser l'accélération GPU** pour turbo‑charger le processus, et le code est étonnamment compact. Dans ce tutoriel, vous verrez un exemple complet et exécutable de Java OCR qui **extrait le texte des fichiers PNG**, exploite un GPU compatible CUDA, et gère une **image OCR volumineuse** avec seulement quelques lignes de code. À la fin, vous saurez exactement comment l'intégrer à votre propre projet Java et pourquoi chaque paramètre est important.

## Ce que vous apprendrez

- Comment configurer Aspose OCR dans un projet Maven ou Gradle.  
- Le processus étape par étape pour **reconnaître le texte d'image** sur le GPU.  
- Pourquoi configurer le nombre de flux GPU peut améliorer le débit.  
- Comment vérifier la sortie et dépanner les problèmes courants.  

> **Prérequis** – Java 17 (ou ultérieur), un GPU compatible CUDA avec le dernier pilote, et une licence valide d'Aspose OCR for Java (l'essai gratuit fonctionne pour l'évaluation). Aucune autre bibliothèque externe n'est requise.

---

## Étape 1 : Ajouter la dépendance Aspose OCR

Tout d'abord, ajoutez la bibliothèque Aspose OCR à votre construction. Si vous utilisez **Maven**, ajoutez le fragment suivant à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Pour **Gradle**, placez ceci dans `build.gradle` :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Astuce :** La dernière version (en date de mars 2026) inclut des améliorations de performances pour les charges de travail GPU, alors récupérez toujours la version la plus récente.

---

## Étape 2 : Initialiser le moteur OCR et activer le GPU

Créer un moteur OCR est simple. La partie cruciale est d'activer le drapeau GPU—sinon le moteur revient en mode CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Pourquoi activer le GPU ?

Lorsque vous activez `setUseGpu(true)`, Aspose décharge les calculs lourds de réseaux neuronaux convolutionnels vers la carte graphique. Cela peut économiser des secondes sur le temps de traitement d'une **image OCR volumineuse**, surtout lorsque l'image dépasse 4000 × 4000 px. Si votre environnement ne possède pas de GPU compatible, l'appel devient simplement une opération nulle et le moteur continue sur le CPU—pas de plantage, seulement des performances plus lentes.

---

## Étape 3 : Reconnaître une image PNG et extraire son texte

Pointez maintenant le moteur vers le fichier que vous souhaitez traiter. L'exemple utilise `sample-large.png`, mais vous pouvez le remplacer par n'importe quel PNG ou JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Cette sortie confirme que l'opération **reconnaître le texte d'image** a réussi et que vous avez bien **extrait le texte du PNG**.

---

## Étape 4 : Vérifier l'utilisation du GPU (Optionnel mais utile)

Si vous vous demandez si le GPU est réellement utilisé, ouvrez l'outil de surveillance GPU de votre système (par ex., `nvidia-smi` sous Linux). Pendant que le processus Java s'exécute, vous devriez voir un léger pic d'utilisation de la mémoire et du calcul.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Si vous ne voyez aucune activité, revérifiez que :

1. Le pilote CUDA correspond au modèle du GPU.  
2. L'appel `setUseGpu(true)` n'est pas écrasé plus tard dans le code.  
3. Votre fichier de licence (si vous en avez un) ne restreint pas l'utilisation du GPU.

---

## Étape 5 : Gestion des cas limites courants

### Images volumineuses dépassant la mémoire du GPU

Lorsqu'une image est massive (par ex., 8000 × 8000 px), le GPU peut manquer de mémoire. Une solution rapide consiste à réduire l'échelle de l'image avant de la transmettre à Aspose :

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Puis passez `"sample-resized.png"` à `recognizeImage`. Cela maintient la précision de l'OCR tout en restant dans les limites du GPU.

### PDFs multi‑pages

Aspose OCR peut également gérer les PDFs page par page. Parcourez chaque page, convertissez‑la en image, et transmettez‑la au moteur. Le même drapeau **use gpu acceleration** s'applique, vous offrant un pipeline PDF‑vers‑texte rapide.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Ci-dessous la classe Java complète, prête à être compilée et exécutée. Remplacez `YOUR_DIRECTORY` par le chemin de votre fichier PNG.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Sortie attendue** – une représentation en texte brut de tout ce que le moteur a pu lire dans l'image. Si l'image contient un tableau, vous obtiendrez le contenu des cellules concaténé avec des sauts de ligne ; Aspose ne préserve pas la mise en page, mais vous pouvez post‑traiter la chaîne si nécessaire.

---

## Questions fréquemment posées

| Question | Réponse |
|----------|--------|
| **Ai-je besoin d'une licence payante ?** | L'essai fonctionne jusqu'à 200 pages et désactive le filigrane pour l'OCR. En production, une licence supprime les limites et débloque l'ensemble de la pile GPU. |
| **Et si mon GPU est plus ancien (par ex., GTX 750) ?** | Les GPU plus anciens peuvent encore fonctionner mais avec une vitesse réduite ; assurez‑vous d'avoir au moins la Compute Capability 3.0. |
| **Puis‑je traiter des fichiers JPG ou BMP ?** | Absolument—`recognizeImage` accepte tout format pris en charge par Java ImageIO. |
| **Existe‑t‑il un moyen de traiter en lot de nombreuses images ?** | Enveloppez l'appel OCR dans une boucle, et envisagez d'augmenter `setGpuStreams` pour correspondre au nombre de flux concurrents souhaités. |
| **Et si je dois préserver la mise en page ?** | Utilisez `LayoutOptions` d'Aspose OCR pour obtenir les boîtes englobantes ; cela dépasse le cadre de ce guide rapide mais est documenté dans l'API. |

---

## Conclusion

Vous disposez maintenant d'un **exemple java OCR** concis et complet qui **reconnaît le texte d'image**, **extrait le texte du PNG**, et **utilise l'accélération GPU** pour accélérer le traitement d'une **image OCR volumineuse**. En ajustant le nombre de flux GPU et, si nécessaire, en réduisant la taille des images surdimensionnées, vous pouvez adapter la solution à pratiquement n'importe quelle configuration matérielle.

Prêt pour l'étape suivante ? Essayez d'alimenter un dossier de reçus numérisés dans le même pipeline, ou expérimentez l'API `TextRegion` d'Aspose pour conserver la mise en page originale. Et si vous rencontrez des problèmes, les forums Aspose et le Javadoc sont d'excellentes ressources—souvenez‑vous simplement des bases que nous avons couvertes ici.

Bon codage, et que votre OCR soit ultra‑rapide !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}