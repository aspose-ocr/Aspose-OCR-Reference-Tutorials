---
category: general
date: 2026-02-22
description: Apprenez comment activer le GPU dans Java OCR pour reconnaître le texte
  d’une image et extraire rapidement le texte d’une facture à l’aide d’Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: fr
og_description: Comment activer le GPU dans Java OCR, reconnaître le texte d’une image
  et extraire le texte d’une facture avec un exemple complet de Java OCR.
og_title: Comment activer le GPU pour l'OCR Java – Guide rapide
tags:
- Java
- OCR
- GPU
- Aspose
title: Comment activer le GPU pour l'OCR Java – Reconnaître le texte à partir d’une
  image
url: /fr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

to Enable GPU for Java OCR – Recognize Text from Image

Translate heading: "Comment activer le GPU pour l'OCR Java – Reconnaître du texte à partir d'une image"

Then paragraph.

We'll translate.

Make sure to keep **bold** formatting.

Proceed.

Will keep code block placeholders unchanged.

Tables: translate header and description but keep code values unchanged.

Proceed.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU pour l'OCR Java – Reconnaître du texte à partir d'une image

Vous vous êtes déjà demandé **comment activer le GPU** lors d'une OCR en Java ? Vous n'êtes pas seul — de nombreux développeurs rencontrent une limite de performances lorsqu'ils traitent de gros documents haute résolution comme des factures. La bonne nouvelle ? Avec Aspose OCR, il suffit d'un seul commutateur pour laisser la carte graphique faire le gros du travail. Dans ce tutoriel, nous parcourrons un **exemple java ocr** qui charge une image, active le traitement GPU et extrait le texte d’une facture en un éclair.

Nous couvrirons tout, de l’installation de la bibliothèque à la gestion des cas particuliers tels que l’absence de pilotes GPU. À la fin, vous pourrez **reconnaître du texte à partir d'une image** à la volée et vous disposerez d’un modèle solide pour tous vos futurs projets OCR. Aucun référentiel externe requis — juste du code pur, exécutable.

## Prérequis

- **Java Development Kit (JDK) 11** ou version supérieure installé sur votre machine.  
- **Maven** (ou Gradle) pour la gestion des dépendances.  
- Un **système compatible GPU** avec des pilotes à jour (NVIDIA, AMD ou Intel).  
- Un fichier image d’une facture (par ex. `large_invoice_300dpi.png`).  

Si l’un de ces éléments vous manque, installez‑le d’abord ; le reste du guide part du principe qu’ils sont en place.

## Étape 1 : Ajouter Aspose OCR à votre projet

La première chose dont nous avons besoin est la bibliothèque Aspose OCR. Avec Maven, il suffit d’insérer le fragment suivant dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Astuce :** Le numéro de version change régulièrement ; consultez Maven Central pour obtenir la dernière version disponible.

Si vous préférez Gradle, l’équivalent est :

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Une fois la dépendance résolue, vous êtes prêt à écrire du code qui communique avec le moteur OCR.

## Étape 2 : Comment activer le GPU dans le moteur Aspose OCR

Voici le moment clé — activer le traitement GPU. Aspose OCR propose trois modes de traitement :

| Mode | Description |
|------|-------------|
| `CPU_ONLY` | Pure CPU, sûr pour n’importe quelle machine. |
| `GPU_ONLY` | Force le GPU, échoue s’il n’y a aucun dispositif compatible. |
| `AUTO_GPU` | Détecte un GPU et l’utilise lorsqu’il est disponible, sinon revient au CPU. |

Dans la plupart des scénarios, nous recommandons **`AUTO_GPU`** car il offre le meilleur des deux mondes. Voici comment l’activer :

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Pourquoi c’est important :** Activer le GPU peut réduire le temps de traitement d’une facture à 300 dpi de plusieurs secondes à moins d’une seconde, selon votre matériel.

## Étape 3 : Charger l’image pour l’OCR – Reconnaître du texte à partir d’une image

Avant que le moteur ne puisse lire quoi que ce soit, vous devez lui fournir une image. La classe `OcrInput` d’Aspose OCR accepte des chemins de fichiers, des flux ou même des objets `BufferedImage`. Pour simplifier, nous utiliserons un chemin de fichier :

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Cas particulier :** Si l’image dépasse 5 Mo, pensez à la réduire d’abord afin d’éviter les erreurs de dépassement de mémoire sur le GPU.

## Étape 4 : Effectuer l’OCR et extraire le texte de la facture

Nous demandons maintenant au moteur d’accomplir sa magie. La méthode `recognize` renvoie un objet `OcrResult` contenant le texte extrait, les scores de confiance et les informations de mise en page.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Lorsque vous exécutez le programme, vous devriez obtenir quelque chose comme :

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Si la sortie apparaît illisible, vérifiez que l’image est nette et que la langue OCR est correctement définie (Aspose utilise l’anglais par défaut, mais vous pouvez le changer via `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)`, etc.).

## Étape 5 : Exemple complet fonctionnel (prêt à copier‑coller)

Voici la classe Java complète et autonome. Collez‑la dans votre IDE, ajustez le chemin de l’image, puis cliquez sur **Run**.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Sortie attendue

L’exécution du code sur une facture claire à 300 dpi produit généralement une représentation texte brut de chaque ligne du document. La sortie exacte dépend de la mise en page de la facture, mais vous verrez des champs tels que *Invoice Number*, *Date*, *Total Amount* et les descriptions des lignes d’articles.

## Problèmes courants & Solutions

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| **`java.lang.UnsatisfiedLinkError`** | Pilote GPU manquant ou incompatible | Installez le dernier pilote depuis NVIDIA/AMD/Intel. |
| **Traitement très lent** | Le GPU est passé en CPU silencieusement | Vérifiez que `ocrEngine.getProcessingMode()` renvoie `AUTO_GPU` et que `SystemInfo.isGpuAvailable()` est vrai. |
| **Sortie vide** | Image trop sombre ou à faible contraste | Pré‑traitez l’image (augmentez le contraste, binarisez) avant de la soumettre à l’OCR. |
| **Out‑of‑Memory** | Image très grande (>10 MP) | Redimensionnez ou découpez l’image en tuiles ; traitez chaque tuile séparément. |

## Récapitulatif étape par étape (Référence rapide)

| Étape | Ce que vous avez fait |
|-------|-----------------------|
| 1 | Ajouté la dépendance Aspose OCR |
| 2 | Créé `OcrEngine` et défini `AUTO_GPU` |
| 3 | Chargé une image de facture via `OcrInput` |
| 4 | Appelé `recognize` et affiché `ocrResult.getText()` |
| 5 | Géré les erreurs courantes et vérifié la sortie |

## Aller plus loin – Prochaines étapes

- **Traitement par lots** : Parcourez un dossier de factures et stockez chaque résultat dans une base de données.  
- **Support multilingue** : Changez `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` pour des factures multilingues.  
- **Post‑traitement** : Utilisez des expressions régulières pour extraire des champs comme *Invoice Number* ou *Total Amount* du texte brut.  
- **Optimisation GPU** : Si vous avez plusieurs GPU, explorez `ocrEngine.setGpuDeviceId(int id)` pour choisir le plus rapide.

## Conclusion

Nous avons montré **comment activer le GPU** pour l’OCR Java, présenté un **exemple java ocr** clair, et parcouru l’ensemble du flux depuis **charger l’image pour l’OCR** jusqu’à **extraire le texte de la facture**. En tirant parti du mode `AUTO_GPU` d’Aspose, vous obtenez un gain de performance sans sacrifier la compatibilité — idéal tant pour les machines de développement que pour les serveurs de production.

Essayez, ajustez le pré‑traitement d’image et expérimentez avec le traitement par lots. Le ciel est la limite lorsque vous combinez l’accélération GPU avec une bibliothèque OCR robuste.

---

![Diagram showing GPU‑accelerated OCR pipeline – how to enable GPU for Java OCR](https://example.com/images/gpu-ocr-pipeline.png "how to enable gpu for Java OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}