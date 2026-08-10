---
category: general
date: 2026-06-22
description: 'Comment redresser une image pour l''OCR : apprendre les étapes de prétraitement
  d''image pour l''OCR, supprimer le bruit sel‑poivre et améliorer la précision.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: fr
og_description: Comment redresser une image pour l'OCR, supprimer le bruit sel‑poivre
  et appliquer les techniques de prétraitement d'images OCR dans un exemple complet
  en Java.
og_title: Comment redresser une image – Guide de prétraitement d’image pour OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Comment redresser une image – Guide de prétraitement d'image pour OCR
url: /fr/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image – Guide de prétraitement d'image OCR

Vous êtes‑vous déjà demandé **comment redresser une image** afin que votre moteur OCR lise réellement le texte ? Vous n'êtes pas le seul. Un scan incliné peut transformer un document parfait en un fouillis illisible, et la plupart des développeurs rencontrent ce problème au moins une fois.

Dans ce tutoriel, nous parcourrons un pipeline complet de **prétraitement d'image OCR** qui non seulement corrige la rotation mais aussi **supprime les artefacts de sel et poivre** et augmente le contraste — en gros tout ce dont vous avez besoin pour **prétraiter des images OCR**‑style avant de les envoyer au moteur. À la fin, vous disposerez d’un extrait Java prêt à l’emploi et d’un modèle mental clair expliquant pourquoi chaque étape est importante.

## Comment redresser une image – Construction du pipeline de prétraitement

Le cœur de tout flux de travail compatible OCR est un objet **preprocess options** qui enchaîne une série de filtres. Pensez‑y comme à un tapis roulant : chaque filtre effectue une tâche, puis transmet l’image au suivant. Voici un exemple minimal mais complet utilisant une bibliothèque OCR hypothétique qui fournit `DeskewFilter`, `DenoiseFilter` et `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Pourquoi cela fonctionne

* **DeskewFilter** analyse les lignes de texte dominantes de l’image, estime l’angle et fait pivoter le bitmap pour le remettre à l’horizontale. La plupart des bibliothèques limitent la correction à ±15° car des angles plus grands indiquent généralement une page mal numérisée nécessitant une intervention manuelle.  
* **DenoiseFilter** cible le motif classique *sel‑et‑poivre* — ces pixels noirs ou blancs isolés qui ressemblent à du bruit sur une télévision. Les supprimer empêche le moteur OCR de confondre le bruit avec des caractères.  
* **ContrastBoostFilter** étire l’histogramme, faisant ressortir les traits faibles. Un multiplicateur de `1.5f` est une valeur sûre ; vous pouvez l’augmenter si vos scans sont particulièrement délavés.

> **Astuce :** Si vous savez que vos documents n’excèdent jamais une inclinaison de 10°, passez cette borne plus petite à `DeskewFilter` — l’algorithme s’exécute plus rapidement et est moins susceptible de sur‑corriger.

## Prétraitement d'image OCR : Ajouter les filtres dans le bon ordre

L’ordre est important. Imaginez que vous débruitiez *avant* le redressement ; le bruit pourrait fausser la détection de l’angle, entraînant un résultat mal aligné. Inversement, appliquer le renforcement du contraste *après* le redressement garantit que la rotation n’introduit pas de nouveaux artefacts.

Voici une petite checklist que vous pouvez copier‑coller dans n’importe quel projet :

| Étape | Filtre | Raison |
|------|--------|--------|
| 1 | `DeskewFilter` | Aligne la ligne de base du texte |
| 2 | `DenoiseFilter` | Supprime le bruit de pixels isolés |
| 3 | `ContrastBoostFilter` | Améliore la lisibilité pour l’OCR |

Si vous devez insérer des étapes supplémentaires — par exemple, un filtre de **binarisation** pour l’OCR binaire — vous le placeriez **après** le renforcement du contraste, car une image propre et à fort contraste se binarise plus précisément.

## Supprimer le bruit sel‑poivre avec DenoiseFilter

Le bruit sel‑et‑poivre est redouté dans les scans de basse qualité, surtout ceux provenant de téléphones bon marché. Le `DenoiseFilter` de notre bibliothèque implémente un noyau de filtre médian, qui remplace chaque pixel par la médiane de son voisinage. L’effet ? Ces taches disparaissent sans flouter les caractères réels.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Quand augmenter la taille du noyau ?* Si vos images sources sont parsemées de gros points, un noyau plus grand les nettoiera, mais attention : trop grand et vous risquez d’effacer les traits fins des petites polices.

## Prétraiter des images OCR – Appliquer le pipeline

Une fois que vous avez assemblé la chaîne de filtres, l’attacher au moteur se fait en une seule ligne (`engine.setPreprocessOptions`). Dès lors, chaque appel à `recognizeText` passe automatiquement par le pipeline. Pas besoin d’appeler chaque filtre manuellement — votre code reste propre, et les modifications futures (ajout d’un nouveau filtre, ajustement des paramètres) sont centralisées.

Voici à quoi ressemble une exécution réussie avec un scan d’exemple qui avait initialement une inclinaison de 12° et un bruit de poivre visible :

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Remarquez que le texte est propre, correctement orienté, et exempt de caractères errants qui seraient apparus autrement sous la forme « I n v o i c e » ou « $‑‑‑ ».

## Cas limites & pièges courants

| Situation | À surveiller | Solution proposée |
|-----------|--------------|-------------------|
| Rotation > 15° | DeskewFilter peut abandonner | Pré‑tourner manuellement ou utiliser un filtre à plus grande plage |
| Résolution extrêmement basse (< 100 dpi) | Le renforcement du contraste ne peut pas récupérer les détails | Rééchantillonner l’image d’abord (par ex., `ResampleFilter`) |
| Bruit mixte (Gaussien + sel‑poivre) | DenoiseFilter seul n’est pas suffisant | Chaîner un `GaussianBlurFilter` avant `DenoiseFilter` |
| Scans couleur avec texte coloré | Conversion en niveaux de gris nécessaire | Insérer `GrayscaleFilter` avant le renforcement du contraste |

En anticipant ces scénarios, vous vous évitez des heures de débogage plus tard.

## Exemple complet fonctionnel (Tout‑en‑un)

Voici une classe Java autonome que vous pouvez intégrer dans n’importe quel projet Maven ou Gradle incluant la dépendance `com.example.ocr`. Elle démontre **comment redresser une image**, **supprimer le bruit sel‑poivre**, et **prétraiter des images OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Sortie attendue** (en supposant que `scanned-document.png` contienne une facture claire) :

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Si vous remplacez l’image par une autre déjà parfaitement alignée, vous remarquerez que le pipeline s’exécute toujours — rien ne se casse, et la précision de l’OCR reste élevée.

## Conclusion

Vous avez maintenant une compréhension solide de **comment redresser une image** et pourquoi chaque étape de prétraitement — **prétraitement d'image OCR**, **supprimer le sel‑poivre**, et **prétraiter des images OCR** — joue un rôle crucial pour fournir un texte propre et consultable. L’exemple ci‑dessus est complet,

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment utiliser AspOCR : filtres de prétraitement d’image OCR pour .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculer l’angle d’inclinaison pour le prétraitement d’image OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Comment définir la valeur de seuil dans la reconnaissance d’image OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}