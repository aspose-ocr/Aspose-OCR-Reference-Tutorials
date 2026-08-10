---
category: general
date: 2026-02-19
description: Apprenez à redresser les images et à éliminer le bruit pour l’OCR. Ce
  tutoriel montre comment reconnaître le texte d’une image, corriger la rotation de
  l’image et prétraiter l’image pour l’OCR avec Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: fr
og_description: Comment redresser une image et éliminer le bruit afin de reconnaître
  rapidement le texte d’une image. Suivez ce guide pour corriger la rotation de l’image
  et prétraiter l’OCR d’image avec Aspose.
og_title: Comment redresser une image – Tutoriel complet de prétraitement OCR
tags:
- OCR
- Java
- Image Processing
title: Comment redresser une image — Guide de prétraitement OCR étape par étape
url: /fr/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

translate to French: "comment redresser l'image". But need to keep the same formatting. So alt text: "exemple de redressement d'image". Title: "comment redresser l'image". But ensure not to translate file path.

Also translate list items, headings, etc.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image — Tutoriel complet de pré‑traitement OCR

Vous êtes-vous déjà demandé **comment redresser une image** avant de la soumettre à un moteur OCR ? Peut‑être avez‑vous scanné un lot de reçus, et les pages semblent légèrement inclinées, ou le scan est parsemé de points aléatoires. C’est un problème fréquent — des images penchées et bruyantes font échouer la reconnaissance de texte.  

Bonne nouvelle ? Vous pouvez redresser (corriger la rotation de l’image) et débruiter (comment enlever le bruit) en quelques lignes de Java avec Aspose.OCR. Dans ce guide, nous parcourrons l’ensemble du flux : du chargement d’un PNG bruyant et tourné, à l’application du redressement + débruitage médian, jusqu’à **reconnaître le texte d’une image** et afficher le résultat. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet Java.

## Ce dont vous avez besoin

- **Java 17** ou supérieur (le code compile avec des versions antérieures, mais 17 est le meilleur compromis).  
- **Aspose.OCR for Java** – récupérez le JAR le plus récent depuis Maven Central (`com.aspose:aspose-ocr`).  
- Un fichier image à la fois tourné et bruyant (par ex. `noisy-rotated.png`).  
- Un IDE modeste (IntelliJ, Eclipse, ou même VS Code).  

Aucun outil de construction sophistiqué n’est requis ; un simple `javac` + `java` suffit.

---

## Étape 1 – Créer l’instance du moteur OCR  

La première chose à faire est d’instancier un `OcrEngine`. Considérez‑le comme le cerveau qui lira les caractères pour vous.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Astuce :** Conservez le moteur en singleton si vous traitez de nombreuses images ; il réutilise les tampons internes et accélère le traitement.

## Étape 2 – Activer le redressement et le débruitage médian (Comment enlever le bruit)

Nous indiquons maintenant au moteur de **corriger la rotation de l’image** et de **comment enlever le bruit**. Les deux filtres sont optionnels, mais combinés ils améliorent considérablement la précision.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Pourquoi le débruitage médian ? Il préserve les contours (les lignes qui définissent les caractères) tout en éliminant les pixels isolés — exactement ce qu’il faut pour un OCR propre.

## Étape 3 – Charger l’image à traiter  

Ici, nous pointons le moteur vers le fichier qui doit être nettoyé. `ImageStream.fromFile` lit le PNG en mémoire.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Si votre image se trouve sur un serveur distant, fournissez simplement un `InputStream` à la place — Aspose le gère sans problème.

## Étape 4 – Exécuter l’OCR et récupérer le texte reconnu  

Avec le pré‑traitement activé, le moteur lit maintenant l’image corrigée. L’appel `recognize()` renvoie un `RecognitionResult` contenant la chaîne extraite.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Vous devriez voir du texte propre et lisible dans la console, même si l’image d’origine était inclinée et granuleuse.

## Étape 5 – Vérifier le résultat (À quoi s’attendre)

Lorsque tout fonctionne, la console affiche quelque chose comme :

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Si la sortie contient encore des caractères illisibles, revérifiez :

- La résolution de l’image (≥ 300 dpi est idéal).  
- Que le chemin du fichier est correct.  
- Si des filtres supplémentaires (par ex. `setContrastStretch`) pourraient aider.

---

## Optionnel : Confirmation visuelle avec une image d’exemple  

Voici un petit aperçu d’un reçu tourné et bruyant. Remarquez l’inclinaison — notre code le redressera pour vous.

![exemple de redressement d'image](deskew-demo.png "comment redresser l'image")

*Texte alternatif : comment redresser l'image – avant et après le traitement.*

---

## Questions fréquentes

### Cela fonctionne‑t‑il avec les PDF ou uniquement PNG/JPEG ?  
Aspose.OCR peut lire les PDF directement ; il suffit de remplacer `ImageStream.fromFile` par `ImageStream.fromPdf`. Les mêmes drapeaux de pré‑traitement s’appliquent, vous obtenez donc toujours **comment redresser une image** et **comment enlever le bruit**.

### Et si je dois conserver l’orientation originale pour des étapes ultérieures ?  
Vous pouvez cloner l’image avant le pré‑traitement :

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Puis‑je modifier manuellement l’angle de redressement ?  
Oui—`setDeskewAngle(double degrees)` vous permet de remplacer l’algorithme de détection automatique. Utile lorsque la détection automatique échoue sur des rotations extrêmes.

### En quoi le débruitage médian diffère‑t‑il du flou gaussien ?  
Les filtres médians remplacent chaque pixel par la médiane de ses voisins, ce qui préserve les bords. Le flou gaussien lisse tout, pouvant estomper les traits des caractères—le médian est donc plus sûr pour l’OCR.

---

## Conclusion  

Dans ce tutoriel, nous avons vu **comment redresser une image**, démontré **comment enlever le bruit**, et montré comment **reconnaître le texte d’une image** en utilisant le pré‑traitement intégré d’Aspose OCR. En activant `setDeskew(true)` et `setMedianDenoise(true)`, vous **corrigez automatiquement la rotation de l’image** et éliminez les taches, transformant un scan désordonné en une chaîne de texte propre.  

N’hésitez pas à expérimenter : essayez différentes stratégies de débruitage, traitez des PDF, ou enchaînez plusieurs images dans une boucle. Le même schéma—moteur → pré‑traitement → reconnaissance—s’applique à chaque scénario, constituant une base solide pour tout pipeline OCR.

**Prochaines étapes** à explorer :

- **Traitement par lots** – itérer sur un dossier d’images et écrire chaque résultat dans un fichier `.txt`.  
- **Packs de langues** – charger un dictionnaire de langue spécifique pour améliorer la précision sur du texte non anglais.  
- **Filtres avancés** – comme `setContrastStretch` ou `setBinarization` pour les scans à faible contraste.  

Des questions supplémentaires ? Laissez un commentaire, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}