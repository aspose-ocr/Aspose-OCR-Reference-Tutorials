---
category: general
date: 2026-02-17
description: Prétraiter l'image pour l'OCR avec Aspose OCR en Java. Apprenez à augmenter
  le contraste de l'image, à définir le niveau de contraste et à reconnaître le texte
  à partir de l'image en quelques minutes.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: fr
og_description: Prétraiter l'image pour l'OCR avec Aspose OCR Java. Ce guide montre
  comment augmenter le contraste de l'image, définir le niveau de contraste et reconnaître
  rapidement le texte à partir de l'image.
og_title: Prétraiter l'image pour l'OCR – Tutoriel Java pour augmenter le contraste
  et extraire le texte
tags:
- Java
- OCR
- Image Processing
title: Prétraiter l'image pour l'OCR – Guide complet Java pour augmenter le contraste
  et extraire le texte
url: /fr/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

, etc.

We need to translate everything else, including alt text for image? The alt text is "preprocess image for OCR example". Should translate? Probably yes, but alt text is part of markdown image syntax; we can translate the alt text but keep the URL unchanged. The title attribute also "preprocess image for OCR – before and after contrast boost" should be translated.

We must keep code block placeholders unchanged.

Let's produce final French translation.

Check for any URLs: none except image path. Keep unchanged.

Check for shortcodes: keep as is.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraiter une image pour l'OCR – Guide complet Java

Vous avez déjà eu besoin de **prétraiter une image pour l'OCR** sans savoir quels réglages font réellement la différence ? Vous n'êtes pas seul. La plupart des développeurs jettent une image dans un moteur OCR et espèrent que la magie opère, pour ne recevoir qu'un texte illisible. Dans ce tutoriel, nous parcourrons un exemple pratique, de bout en bout, qui **augmente le contraste de l'image**, ajuste le **niveau de contraste**, puis **reconnaît le texte à partir de l'image** à l'aide d'Aspose OCR for Java.

À la fin, vous disposerez d’un extrait de code réutilisable qui **extrait du texte avec l'OCR** de façon fiable, même sur des numérisations bruyantes. Aucun tour de passe‑passe caché, seulement des étapes claires et la logique derrière chacune d’elles.

## Ce dont vous avez besoin

- Java 17 ou plus récent (le code compile avec n’importe quel JDK récent)
- Bibliothèque Aspose OCR for Java (téléchargez‑la depuis le site officiel d’Aspose)
- Un fichier de licence Aspose OCR valide (`Aspose.OCR.lic`)
- Une image d’entrée (`input.jpg`) que vous souhaitez lire
- Un IDE préféré ou une configuration simple en ligne de commande

Si vous avez déjà tout cela, super—plongeons directement.

## Étape 1 : Charger la licence Aspose OCR (Configuration principale)

Avant que le moteur OCR ne fasse quoi que ce soit, il doit savoir que vous êtes licencié. Sinon, vous tomberez sur un filigrane d’évaluation.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Pourquoi c’est important :** Sans licence adéquate, le moteur fonctionne en mode d’évaluation, ce qui peut tronquer les résultats ou ajouter des filigranes. Définir la licence dès le départ garantit également que toutes les options de prétraitement ultérieures sont appliquées en mode complet.

## Étape 2 : Initialiser le moteur OCR

Créer une instance `OcrEngine` vous donne accès à la fois à la reconnaissance et aux pipelines de prétraitement.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Astuce :** Conservez le moteur en tant que singleton si vous prévoyez de traiter de nombreuses images en lot ; il met en cache les ressources internes et accélère les appels suivants.

## Étape 3 : Configurer le prétraitement – Redressement, Dénoyautage et Amélioration du contraste

C’est ici que nous **prétraitons l'image pour l'OCR**. Les trois paramètres que nous allons ajuster sont :

1. **Redressement** – corrige les légères rotations.
2. **Dénoyautage** – élimine les taches qui perturbent la segmentation des caractères.
3. **Amélioration du contraste** – fait ressortir le texte sombre sur le fond.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Pourquoi ajuster le niveau de contraste ?

Augmenter le niveau de contraste étire l’histogramme de l’image, rendant les pixels sombres plus sombres et les pixels clairs plus clairs. En pratique, un **niveau de contraste** de `1.3f` donne souvent le meilleur équilibre pour les documents imprimés, tandis qu’une valeur supérieure à `1.5f` peut surexposer les traits fins. N’hésitez pas à expérimenter ; le réglage est peu coûteux à changer et peut améliorer de façon spectaculaire le taux de succès de la **reconnaissance du texte à partir de l'image**.

## Étape 4 : Préparer l'image d’entrée

La classe `OcrInput` abstrait la gestion des fichiers. Vous pouvez ajouter plusieurs images si vous avez besoin d’un traitement par lot.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Cas particulier :** Si votre image est dans un format non standard (par ex., TIFF avec plusieurs pages), vous pouvez charger chaque page séparément ou la convertir d’abord en PNG/JPEG.

## Étape 5 : Effectuer la reconnaissance

Le moteur exécute maintenant le pipeline de prétraitement que nous venons de configurer, puis transmet l’image nettoyée à l’algorithme OCR principal.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Que se passe‑t‑il en coulisses ?** Aspose OCR applique d’abord la transformation de redressement, puis le filtre de dénoyautage, et enfin ajuste le contraste avant d’alimenter l’image à son reconnaisseur basé sur un réseau de neurones. L’ordre est intentionnel ; le modifier pourrait conduire à des résultats sous‑optimaux.

## Étape 6 : Afficher le texte reconnu

Enfin, nous affichons la chaîne extraite dans la console. Dans une vraie application, vous pourriez l’écrire dans un fichier ou l’envoyer sur le réseau.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Résultat attendu

Si `input.jpg` contient la phrase « Hello World! », la console devrait afficher :

```
Hello World!
```

Si la sortie apparaît brouillée, revérifiez les valeurs de prétraitement—en particulier le **niveau de contraste** et le **mode de dénoyautage**—et essayez un autre format d’image.

## Bonus : Visualiser l’image pré‑traitée (Optionnel)

Parfois, vous voulez voir ce que le moteur voit après le redressement, le dénoyautage et l’amélioration du contraste. Aspose OCR vous permet d’exporter le bitmap intermédiaire :

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Ouvrez `processed.png` côte à côte avec l’original ; vous remarquerez un horizon plus droit et un texte plus net. Cette étape est pratique pour diagnostiquer pourquoi une numérisation particulière échoue.

![exemple de prétraitement d'image pour OCR](/images/ocr-preprocess-example.png "prétraitement d'image pour OCR – avant et après l'augmentation du contraste")

*L’image ci‑dessus illustre comment augmenter le contraste et dénoyauter transforme une numérisation floue en une image propre, prête pour l'OCR.*

## Problèmes courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Sur‑contraste** (`setContrastLevel` trop élevé) | Le fond clair devient blanc, effaçant les caractères faibles | Gardez le niveau entre 1.1 et 1.4 pour la plupart des textes imprimés |
| **Tolérance de redressement trop basse** | Les petites rotations restent non corrigées | Augmentez `setDeskewAngleTolerance` à 0.2 ou 0.3 pour les livres numérisés |
| **Utilisation du dénoyautage GAUSSIAN sur des images binaires** | Floute les bords, fusionnant les caractères | Optez pour `DenoiseMode.MEDIAN` pour les scans noir‑et‑blanc |
| **Licence manquante** | Le moteur revient en mode d’essai, tronquant la sortie | Vérifiez le chemin vers `Aspose.OCR.lic` et que le fichier est lisible |

## Prochaines étapes : Aller au‑delà du pré‑traitement de base

Maintenant que vous savez **prétraiter une image pour l'OCR** et **extraire du texte avec l'OCR**, envisagez ces extensions :

- **Packs de langues** – chargez des dictionnaires spécifiques pour améliorer la précision sur les textes non anglais.
- **Recadrage de région d’intérêt (ROI)** – concentrez‑vous sur une sous‑section de l’image si vous n’avez besoin que d’une partie de la page.
- **Traitement par lot** – parcourez un répertoire d’images, en réutilisant la même instance `OcrEngine` pour gagner en vitesse.
- **Intégration avec PDF** – combinez Aspose OCR avec Aspose PDF pour convertir des PDF numérisés en PDF recherchables en une seule chaîne.

Chacun de ces sujets intègre naturellement nos mots‑clés secondaires : vous continuerez à **augmenter le contraste de l'image**, à **définir le niveau de contraste**, et à **reconnaître le texte à partir de l'image** dans de nombreux scénarios.

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **prétraiter une image pour l'OCR** avec Aspose OCR for Java : charger la licence, configurer le redressement, le dénoyautage et l’amélioration du contraste, fournir l’image, puis **reconnaître le texte à partir de l'image**. Avec l’exemple complet et exécutable ci‑dessus, vous pouvez dès à présent **extraire du texte avec l'OCR** sur n’importe quelle image correctement préparée.

Testez le code, ajustez le **niveau de contraste**, et observez la précision grimper. Quand vous serez prêt, explorez les modèles spécifiques aux langues ou les pipelines par lot pour transformer cette démonstration d’une seule image en une solution prête pour la production.

*Bon codage, et que vos scans soient toujours nets !*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}