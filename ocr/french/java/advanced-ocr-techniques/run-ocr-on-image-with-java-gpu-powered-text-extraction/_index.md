---
category: general
date: 2026-03-07
description: Exécuter l'OCR sur une image avec Java. Apprenez à reconnaître le texte
  à partir d'un PNG, à extraire le texte d'un reçu et à charger une image pour l'OCR
  avec un exemple complet d'OCR en Java.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: fr
og_description: Exécutez la reconnaissance OCR sur une image avec Java. Ce guide montre
  comment reconnaître le texte d’un PNG, extraire le texte d’un reçu et charger une
  image pour l’OCR à l’aide d’un exemple complet d’OCR en Java.
og_title: Exécuter l'OCR sur une image avec Java – Extraction de texte accélérée par
  GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Exécuter la reconnaissance optique de caractères sur une image avec Java –
  Extraction de texte accélérée par GPU
url: /fr/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l’OCR sur une image avec Java – Extraction de texte accélérée par GPU

Vous avez déjà eu besoin d’**exécuter l’OCR sur des fichiers image** sans savoir par où commencer en Java ? Vous n’êtes pas seul — de nombreux développeurs rencontrent le même obstacle lorsqu’ils essaient pour la première fois d’extraire du texte d’un reçu numérisé ou d’une capture d’écran PNG.  

Dans ce tutoriel, nous vous guiderons à travers un **exemple complet d’OCR en Java** qui non seulement **reconnaît le texte à partir de fichiers PNG**, mais montre également comment **extraire le texte d’images de reçus**, le tout en tirant parti de l’accélération GPU pour la rapidité. À la fin, vous disposerez d’un programme prêt à l’emploi qui charge une image pour l’OCR, la traite et affiche le résultat en texte brut.

## Ce que vous allez apprendre

- Comment **charger une image pour l’OCR** à l’aide d’un simple `ImageInputStream`.
- Activer le support GPU afin que le moteur s’exécute plus rapidement sur du matériel moderne.
- Les étapes exactes pour **reconnaître le texte à partir de PNG** et extraire les chaînes utiles d’un reçu.
- Les pièges courants (par ex. ID de périphérique GPU incorrect) et les conseils de bonnes pratiques.
- Un extrait de code complet et exécutable que vous pouvez copier‑coller dans votre IDE.

**Prérequis**

- Java 17 ou supérieur (le code utilise le mot‑clé `var` pour plus de concision, mais vous pouvez le remplacer par des types explicites si vous êtes sous Java 8).
- Une bibliothèque OCR qui fournit les classes `OcrEngine`, `ImageInputStream` et `OcrResult` (par exemple le SDK fictif *FastOCR* ; remplacez‑le par celui que vous utilisez réellement).
- Une machine avec GPU activé si vous souhaitez le gain de performance (optionnel mais recommandé).

---

## Étape 1 : Exécuter l’OCR sur l’image – Activer l’accélération GPU

La première chose à faire est de créer le moteur OCR et de lui indiquer d’utiliser le GPU. Cette étape est cruciale car, sans le support GPU, le moteur revient au CPU, ce qui peut être nettement plus lent pour des reçus haute résolution.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Pourquoi c’est important :**  
L’accélération GPU décharge les calculs matriciels lourds que les moteurs OCR effectuent. Si vous avez plusieurs GPU, vous pouvez choisir celui avec le plus de mémoire en modifiant la valeur de `setGpuDeviceId`. Oublier d’activer le GPU est une cause fréquente de plaintes du type « pourquoi mon OCR est‑il si lent ? ».

> **Astuce pro :** Si votre machine ne possède pas de GPU compatible, l’appel `setUseGpu(true)` sera simplement ignoré — pas de plantage, juste un traitement plus lent.

---

## Étape 2 : Charger l’image pour l’OCR

Maintenant que le moteur est prêt, nous devons lui fournir une image. L’exemple ci‑dessous montre comment charger un reçu PNG stocké sur le disque. Vous pouvez remplacer le chemin par n’importe quel format d’image supporté par votre bibliothèque OCR.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Cas limite :**  
Si le fichier n’existe pas ou si le chemin est incorrect, `ImageInputStream` lèvera une `IOException`. Enveloppez l’appel dans un bloc try‑catch et consignez un message d’erreur utile :

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Étape 3 : Reconnaître le texte à partir de PNG

Une fois l’image chargée, le moteur OCR peut faire sa magie. Cette étape **reconnaît le texte à partir de PNG** (ou tout autre format supporté) et renvoie un objet `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Que se passe‑t‑il en coulisses ?**  
Le moteur effectue un pré‑traitement (redressement, binarisation), exécute un réseau de neurones pour détecter les caractères, puis les assemble en lignes de texte. Parce que nous avons activé le GPU précédemment, ces calculs de réseau de neurones s’effectuent sur la carte graphique, ce qui économise plusieurs secondes sur le temps total d’exécution.

---

## Étape 4 : Extraire le texte du reçu

Après la reconnaissance, vous voudrez généralement obtenir uniquement le texte brut. La classe `OcrResult` fournit habituellement une méthode `getText()` qui renvoie une seule `String`. Vous pouvez ensuite le post‑traiter (par ex. avec des expressions régulières pour extraire les totaux, dates, etc.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Sortie typique d’un reçu :**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Vous pouvez maintenant transmettre cette chaîne à votre propre analyseur pour extraire le montant total, les lignes d’articles ou les informations de taxe.

---

## Étape 5 : Exemple complet d’OCR en Java – Prêt à être exécuté

En rassemblant tous les morceaux, voici le **exemple complet d’OCR en Java** que vous pouvez placer dans un fichier `Main.java`. Assurez‑vous que la bibliothèque OCR figure sur votre classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Sortie console attendue** (en supposant le reçu d’exemple ci‑dessus) :

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Si la sortie apparaît illisible, revérifiez que l’image est nette (haute DPI) et que le pack de langue OCR correspond à la langue de votre reçu.

---

## Questions fréquentes & Pièges

| Question | Réponse |
|----------|---------|
| *Et si mon GPU n’est pas détecté ?* | Le moteur revient automatiquement au CPU. Vérifiez les pilotes et que le `setGpuDeviceId` correspond à un dispositif existant (`nvidia‑smi` sous Linux peut aider). |
| *Puis‑je traiter des fichiers JPEG ou TIFF ?* | Oui—il suffit de changer l’extension du fichier dans `ImageInputStream`. La bibliothèque OCR détecte généralement le format automatiquement. |
| *Existe‑t‑il un moyen de traiter en lot de nombreux reçus ?* | Enveloppez le code de reconnaissance dans une boucle et réutilisez la même instance `OcrEngine ; ré‑initialiser à chaque image gaspille la mémoire GPU. |
| *Comment améliorer la précision sur des reçus à faible contraste ?* | Pré‑traitez l’image (augmentez le contraste, convertissez en niveaux de gris) avant de la transmettre au moteur OCR. Certaines bibliothèques exposent une API `preprocess`. |

---

## Conclusion

Vous savez maintenant **comment exécuter l’OCR sur des fichiers image** en Java, depuis le chargement de la photo jusqu’à l’extraction d’un texte propre à partir d’un reçu. Le guide a couvert **reconnaître le texte à partir de PNG**, **extraire le texte du reçu**, et a présenté un **exemple d’OCR Java** que vous pouvez adapter à n’importe quel projet.  

Et après ? Essayez de désactiver le drapeau GPU pour observer la différence de performance, expérimentez avec différentes résolutions d’image, ou intégrez un analyseur basé sur des expressions régulières pour extraire automatiquement les totaux. Si vous êtes curieux des sujets plus avancés, explorez le **post‑traitement OCR**, la **correction par modèle de langue**, ou les **pipelines de traitement par lot**.

Bon codage, et que vos reçus soient toujours lisibles !  

![exemple d’exécution d’OCR sur image](/images/run-ocr-on-image.png "exemple d’exécution d’OCR sur image – exemple Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}