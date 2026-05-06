---
category: general
date: 2026-05-06
description: Le tutoriel Aspose OCR GPU montre comment reconnaître le texte à partir
  d’une image et extraire le texte d’un PNG en utilisant l’accélération GPU pour une
  OCR rapide et fiable.
draft: false
keywords:
- aspose ocr gpu
- recognize text from image
- extract text from png
- load image for ocr
- gpu accelerated ocr
language: fr
og_description: Apprenez à utiliser Aspose OCR GPU pour reconnaître le texte d’une
  image et extraire le texte d’un PNG avec l’accélération GPU en Java.
og_title: 'Guide Aspose OCR GPU : Accélérer l''extraction de texte'
tags:
- Aspose
- OCR
- Java
- GPU
title: 'Guide GPU Aspose OCR : Accélérer l''extraction de texte à partir d''images
  PNG'
url: /fr/java/advanced-ocr-techniques/aspose-ocr-gpu-guide-accelerate-text-extraction-from-png-ima/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr gpu – Extraction de texte rapide et fiable à partir d'images PNG

Vous souhaitez améliorer les performances de votre OCR avec **aspose ocr gpu** ? Avec Aspose OCR GPU, vous pouvez **reconnaître du texte à partir d'une image** beaucoup plus rapidement en exploitant une carte graphique compatible CUDA. Imaginez traiter un PNG haute résolution en quelques secondes au lieu de minutes—plus besoin d’attendre les résultats.  

Dans ce tutoriel, nous passerons en revue tout ce dont vous avez besoin pour démarrer : charger une image pour l’OCR, basculer le moteur en mode GPU, puis extraire le texte. À la fin, vous disposerez d’un programme Java complet et exécutable qui **extrait du texte de fichiers png** grâce à l’accélération GPU. Aucun document externe requis—suivez simplement les étapes, copiez le code, et vous serez prêt à partir.

## Ce dont vous avez besoin

- **Java Development Kit (JDK) 11+** – le code utilise les fonctionnalités standard du langage Java.  
- **Aspose.OCR for Java** (dernière version en mai 2026). Vous pouvez le récupérer depuis Maven Central :  

  ```xml
  <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version>
  </dependency>
  ```  

- **Un GPU compatible CUDA** (NVIDIA GeForce, Quadro ou Tesla) avec le pilote approprié installé.  
- **Un PNG haute résolution d’exemple** (par ex. `sample-highres.png`) que vous souhaitez traiter.  

Si vous ne disposez pas d’un GPU, le code reviendra automatiquement au CPU—il suffit de commenter les lignes GPU.

## Étape 1 – Charger l'image pour l'OCR

La première chose dont tout flux de travail OCR a besoin est une source d’image. Aspose OCR fournit un wrapper pratique `ImageStream` qui peut lire depuis un fichier, un tableau d’octets ou même une URL. Ici, nous utilisons `ImageStream.fromFile` car c’est la méthode la plus directe pour le développement local.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // -------------------------------------------------
        // Step 1: Load the PNG you want to process
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // Replace the path with the location of your PNG file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample-highres.png"));
```

> **Pourquoi c’est important :** Charger correctement l’image garantit que le moteur OCR reçoit les données de pixels exactes dont il a besoin. L’utilisation de `ImageStream.fromFile` gère également automatiquement les particularités courantes des PNG (canal alpha, profondeur de couleur).

## Étape 2 – Activer l'accélération GPU (aspose ocr gpu)

Vient maintenant la magie : dire à Aspose d’exécuter le traitement sur le GPU. L’objet `OcrDevice` du moteur vous permet de choisir le type d’appareil (`CPU` ou `GPU`) et, si vous avez plusieurs GPU, l’ID de l’appareil spécifique.

```java
        // -------------------------------------------------
        // Step 2: Switch to GPU mode (aspose ocr gpu)
        // -------------------------------------------------
        // Choose GPU as the processing device
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Optional: select a specific GPU when multiple are present
        // ocrEngine.getDevice().setDeviceId(0); // uncomment to use GPU #0
```

> **Astuce pro :** Si vous rencontrez des erreurs `CUDA driver not found`, vérifiez que le pilote NVIDIA correspond à la version CUDA requise par Aspose OCR (généralement CUDA 11.x pour la version 23.x).  
> **Cas particulier :** Lors d’une exécution sur un serveur sans affichage, assurez‑vous que le GPU n’est pas verrouillé par un autre processus ; sinon l’appel OCR reviendra silencieusement au CPU.

## Étape 3 – Reconnaître le texte à partir de l'image

Une fois l’image chargée et le dispositif configuré, vous pouvez enfin lancer le moteur OCR. La méthode `recognize()` renvoie un objet `OcrResult` contenant le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```java
        // -------------------------------------------------
        // Step 3: Perform the OCR – recognize text from image
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();

        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
=== Recognized Text ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

> **Ce que vous voyez :** La chaîne brute extraite du PNG. Si l’image contient des tableaux ou des mises en page à colonnes multiples, vous pouvez activer `LayoutAnalysis` sur le moteur pour de meilleurs résultats (hors du cadre de ce guide rapide).

## Étape 4 – Vérifier que le GPU est réellement utilisé

Il est facile de supposer que le GPU fait le gros du travail, mais une vérification rapide peut vous éviter des heures de débogage. Aspose OCR écrit une petite entrée de journal lorsqu’il initialise le dispositif.

Ajoutez ce fragment juste après avoir défini le type de dispositif :

```java
        // Verify which device is active
        System.out.println("Active OCR device: " + ocrEngine.getDevice().getDeviceType());
```

Si la sortie indique `GPU`, tout est en ordre. Si elle indique `CPU`, revérifiez votre installation de pilote ou assurez‑vous que la variable d’environnement `CUDA_HOME` pointe vers le bon répertoire du toolkit.

## Problèmes courants et comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `java.lang.UnsatisfiedLinkError` concernant `cudart64_110.dll` | Runtime CUDA absent du `PATH` | Ajoutez le dossier `bin` de CUDA à votre `PATH` système ou définissez `java.library.path`. |
| OCR renvoie une chaîne vide | Image non chargée correctement (chemin erroné ou format non supporté) | Vérifiez le chemin du fichier et assurez‑vous que le PNG n’est pas corrompu. |
| Performances similaires au CPU | Repli sur le CPU à cause d’une incompatibilité de pilote | Mettez à jour le pilote NVIDIA à la version indiquée dans les notes de version d’Aspose OCR. |
| Mémoire insuffisante sur de grandes images | Mémoire GPU épuisée | Réduisez la résolution de l’image ou divisez‑l‑en tuiles avant le traitement. |

## Bonus : Revenir au CPU lorsque le GPU n'est pas disponible

Parfois, vous exécuterez le même code sur un ordinateur portable de développement sans GPU compatible CUDA. Envelopper la sélection du dispositif dans un bloc `try‑catch` rend le programme plus robuste.

```java
        try {
            ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
            System.out.println("GPU acceleration enabled.");
        } catch (Exception e) {
            System.out.println("GPU not available – falling back to CPU.");
            ocrEngine.getDevice().setDeviceType(OcrDeviceType.CPU);
        }
```

Ainsi, le même binaire fonctionne partout, et vous conservez le gain de vitesse chaque fois que le matériel le permet.

## Exemple complet, prêt à l'exécution

Voici la classe Java complète qui intègre toutes les étapes, les vérifications et la logique de repli décrites ci‑dessus. Copiez‑collez‑la dans votre IDE, ajustez le chemin de l’image, puis lancez‑la.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // -------------------------------------------------
        // Initialize OCR engine and load the PNG image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample-highres.png"));

        // -------------------------------------------------
        // Try to enable GPU; fall back to CPU if needed
        // -------------------------------------------------
        try {
            ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
            System.out.println("GPU acceleration enabled.");
        } catch (Exception ex) {
            System.out.println("GPU not available – switching to CPU.");
            ocrEngine.getDevice().setDeviceType(OcrDeviceType.CPU);
        }

        // Optional: Choose a specific GPU (uncomment if you have multiple)
        // ocrEngine.getDevice().setDeviceId(0);

        // -------------------------------------------------
        // Run OCR – recognize text from image
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();

        // -------------------------------------------------
        // Output the extracted text – this is the core result
        // -------------------------------------------------
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());

        // -------------------------------------------------
        // Show which device actually processed the request
        // -------------------------------------------------
        System.out.println("Active OCR device: " + ocrEngine.getDevice().getDeviceType());
    }
}
```

**Sortie attendue** (en supposant que le PNG contienne du texte anglais simple) :

```
GPU acceleration enabled.
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
Active OCR device: GPU
```

Si le GPU n’est pas présent, vous verrez « CPU » dans la dernière ligne.

## Vue d'ensemble visuelle

Voici un diagramme rapide du flux de données — du chargement du PNG à la récupération du texte brut. Le texte alternatif de l’image contient le mot‑clé principal pour le SEO.

![aspose ocr gpu workflow – charger l'image, activer le GPU, reconnaître le texte]  

*Texte alternatif : flux de travail aspose ocr gpu montrant comment charger une image pour l’OCR, activer l’accélération GPU et extraire du texte d’un PNG.*

## Récapitulatif et prochaines étapes

Nous venons de couvrir comment **aspose ocr gpu**‑accélérer le processus de **reconnaître du texte à partir d’une image** et **extraire du texte de fichiers png**. Les points clés :

1. **Chargez l'image** avec `ImageStream.fromFile`.  
2. **Activez le GPU** via `ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU)`.  
3. **Exécutez `recognize()`** et lisez `ocrResult.getText()`.  
4. **Validez le dispositif** et revenez gracieusement au CPU si nécessaire.  

Prêt à repousser les limites ? Essayez ces expériences :

- **Traitement par lots :** parcourez un répertoire de PNG et écrivez chaque résultat dans un fichier `.txt`.  
- **Analyse de mise en page :** activez `ocrEngine.getOptions().setDetectDocumentStructure(true)` pour conserver les colonnes et les tableaux.  
- **Mise à l’échelle multi‑GPU :** si votre station possède plusieurs GPU, lancez des threads parallèles, chacun assigné à un `deviceId` différent.  

Ces extensions approfondiront votre maîtrise de **gpu accelerated ocr** et ouvriront la voie à des projets de numérisation de documents à grande échelle.

---

*Bon codage ! Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous—je serai ravi de vous aider à résoudre le problème.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}