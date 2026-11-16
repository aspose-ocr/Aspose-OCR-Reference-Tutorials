---
category: general
date: 2026-02-22
description: Comment utiliser l’OCR en Java pour extraire du texte d’une image, améliorer
  la précision de l’OCR et charger une image pour l’OCR avec des exemples de code
  pratiques.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: fr
og_description: Comment utiliser l'OCR en Java pour extraire du texte d’une image
  et améliorer la précision de l’OCR. Suivez ce guide pour un exemple prêt à l’emploi.
og_title: Comment utiliser l’OCR en Java – Guide complet étape par étape
tags:
- OCR
- Java
- Image Processing
title: Comment utiliser l’OCR en Java – Guide complet étape par étape
url: /fr/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Java – Guide complet étape par étape

Vous avez déjà eu besoin de **how to use OCR** sur une capture d'écran inclinée et vous vous êtes demandé pourquoi le résultat ressemble à du charabia ? Vous n'êtes pas le seul. Dans de nombreuses applications réelles—numérisation de reçus, digitalisation de formulaires ou extraction de texte à partir de mèmes—obtenir des résultats fiables dépend de quelques réglages simples.

Dans ce tutoriel, nous parcourrons **how to use OCR** pour *extract text from image* les fichiers, vous montrer comment **improve OCR accuracy**, et démontrer la bonne façon de **load image for OCR** en utilisant une bibliothèque OCR Java populaire. À la fin, vous disposerez d'un programme autonome que vous pourrez intégrer à n'importe quel projet.

## Ce que vous apprendrez

- Le code exact dont vous avez besoin pour **load image for OCR** (sans dépendances cachées).
- Les indicateurs de prétraitement qui améliorent **improve OCR accuracy** et pourquoi ils sont importants.
- Comment lire le résultat OCR et l'imprimer dans la console.
- Les pièges courants—comme oublier de définir une région d'intérêt ou ignorer la réduction du bruit—et comment les éviter.

### Prérequis

- Java 17 ou version ultérieure (le code se compile avec n'importe quel JDK récent).
- Une bibliothèque OCR qui fournit les classes `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` et `OcrResult` (par exemple, le package fictif `com.example.ocr` utilisé dans l'extrait). Remplacez-le par la vraie bibliothèque que vous utilisez.
- Une image d'exemple (`skewed_noisy.png`) placée dans un dossier que vous pouvez référencer.

> **Astuce pro :** Si vous utilisez un SDK commercial, assurez‑vous que le fichier de licence se trouve sur votre classpath ; sinon le moteur lèvera une erreur d'initialisation.

---

## Étape 1 : Créer une instance d'OCR Engine – **how to use OCR** efficacement

La première chose dont vous avez besoin est un objet `OcrEngine`. Considérez‑le comme le cerveau qui interprétera les pixels.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Pourquoi c’est important :* Sans moteur, vous n’avez aucun contexte pour les modèles linguistiques, les jeux de caractères ou les heuristiques d’image. L’instancier tôt vous permet également d’attacher des options de prétraitement plus tard.

---

## Étape 2 : Configurer le prétraitement d'image – **improve OCR accuracy**

Le prétraitement est la sauce secrète qui transforme un scan bruité en texte propre et lisible par machine. Ci‑dessous, nous activons le redressement (deskew), la réduction du bruit de haut niveau, l'auto‑contraste et une région d'intérêt (ROI) pour se concentrer sur la partie pertinente de l'image.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Pourquoi c’est important :*  
- **Deskew** aligne le texte tourné, ce qui est essentiel lors de la numérisation de reçus qui ne sont pas parfaitement plats.  
- **Noise reduction** supprime les pixels parasites qui seraient autrement interprétés comme des caractères.  
- **Auto‑contrast** étend la gamme tonale, faisant ressortir les lettres faibles.  
- **ROI** indique au moteur d’ignorer les bordures non pertinentes, économisant ainsi du temps et de la mémoire.

Si vous omettez l’un de ces éléments, vous constaterez probablement une baisse des résultats de **improve OCR accuracy**.

---

## Étape 3 : Charger l'image pour l'OCR – **load image for OCR** correctement

Nous indiquons maintenant réellement au moteur le fichier que nous voulons lire. La classe `OcrInput` peut accepter plusieurs images, mais pour cet exemple nous restons simples.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Pourquoi c’est important :* Le chemin doit être absolu ou relatif au répertoire de travail ; sinon le moteur lève une `FileNotFoundException`. Notez également que le nom de la méthode `add` indique que vous pouvez mettre en file d’attente plusieurs images—pratique pour le traitement par lots.

---

## Étape 4 : Effectuer l'OCR et afficher le texte reconnu – **how to use OCR** de bout en bout

Enfin, nous demandons au moteur de reconnaître le texte et de l'imprimer. L'objet `OcrResult` contient la chaîne brute, les scores de confiance et les métadonnées ligne par ligne (si vous en avez besoin plus tard).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Sortie attendue** (en supposant que l'image d'exemple contienne « Hello, OCR World! » ):

```
=== OCR Output ===
Hello, OCR World!
```

Si le résultat apparaît brouillé, revenez à l’Étape 2 et ajustez les options de prétraitement—peut‑être en diminuant le niveau de réduction du bruit ou en modifiant le rectangle ROI.

---

## Exemple complet et exécutable

Voici un programme Java complet que vous pouvez copier‑coller dans un fichier nommé `OcrDemo.java`. Il réunit toutes les étapes que nous avons abordées.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Enregistrez le fichier, compilez avec `javac OcrDemo.java`, puis exécutez `java OcrDemo`. Si tout est correctement configuré, vous verrez le texte extrait affiché dans la console.

---

## Questions fréquentes et cas limites

| Question | Réponse |
|----------|--------|
| **Et si mon image est au format JPEG ?** | La méthode `OcrInput.add()` accepte tout format raster pris en charge—PNG, JPEG, BMP, TIFF. Il suffit de changer l'extension du fichier dans le chemin. |
| **Puis‑je traiter plusieurs pages en même temps ?** | Absolument. Appelez `ocrInput.add()` pour chaque fichier, puis passez le même `ocrInput` à `recognize()`. Le moteur renverra un `OcrResult` concaténé. |
| **Et si le résultat OCR est vide ?** | Vérifiez que le ROI contient réellement du texte. Assurez‑vous également que `setDeskewEnabled(true)` est activé ; une rotation de 90° fera croire au moteur que l'image est vide. |
| **Comment changer le modèle de langue ?** | La plupart des bibliothèques exposent une méthode `setLanguage(String)` sur `OcrEngine`. Appelez‑la avant `recognize()`, par ex., `ocrEngine.setLanguage("eng")`. |
| **Existe‑t‑il un moyen d’obtenir les scores de confiance ?** | Oui, `OcrResult` fournit souvent `getConfidence()` par ligne ou par caractère. Utilisez‑le pour filtrer les résultats à faible confiance. |

---

## Conclusion

Nous avons couvert **how to use OCR** en Java du début à la fin : création du moteur, configuration du prétraitement pour **improve OCR accuracy**, chargement correct **load image for OCR**, et enfin affichage du texte extrait. L’extrait de code complet est prêt à être exécuté, et les explications répondent au « pourquoi » de chaque ligne.

Prêt pour l’étape suivante ? Essayez de remplacer le rectangle ROI pour vous concentrer sur différentes parties de l'image, expérimentez avec `NoiseReduction.MEDIUM`, ou intégrez la sortie dans un PDF consultable. Vous pouvez également explorer des sujets connexes comme **extract text from image** via des services cloud, ou traiter par lots des milliers de fichiers avec une file d’attente multithread.

Vous avez d’autres questions sur l’OCR, le prétraitement d’image ou l’intégration Java ? Laissez un commentaire, et bon codage !

![Exemple d'utilisation de l'OCR](/images/ocr-demo.png "how to use OCR – Exemple Java montrant le prétraitement et le résultat")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}