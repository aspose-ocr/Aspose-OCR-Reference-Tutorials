---
category: general
date: 2026-10-30
description: Apprenez comment améliorer l'OCR en prétraitant les images en Java avec
  Aspose OCR. Ce guide montre comment augmenter le contrast de l'image, régler le
  niveau de contrast et extraire le texte efficacement.
draft: false
keywords:
- how to improve OCR
- how to boost contrast
- preprocess image OCR
- extract text image Java
- recognize text image Java
lastmod: 2026-10-30
og_description: Apprenez comment améliorer l'OCR en prétraitant les images en Java
  avec Aspose OCR. Le guide explique comment augmenter le contrast, régler le niveau
  de contrast et extraire le texte rapidement.
og_image_alt: Screenshot of a Java OCR preprocessing pipeline showing before‑and‑after
  contrast enhancement
og_title: Comment améliorer l'OCR – guide de prétraitement d'image Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  headline: How to improve OCR – preprocess image for OCR in Java with Aspose
  type: TechArticle
- description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  name: How to improve OCR – preprocess image for OCR in Java with Aspose
  steps:
  - name: '**Deskew** – corrects slight rotations.'
    text: '**Deskew** – corrects slight rotations.'
  - name: '**Denoise** – removes speckles that confuse character segmentation.'
    text: '**Denoise** – removes speckles that confuse character segmentation.'
  - name: '**Contrast enhancement** – makes dark text stand out against the background.'
    text: '**Contrast enhancement** – makes dark text stand out against the background.'
  type: HowTo
- questions:
  - answer: Yes—load the appropriate language pack with `engine.setLanguage("fr")`
      or any supported ISO code to improve accuracy for non‑English text.
    question: Can I use this approach for languages other than English?
  - answer: It does not read PDF pages natively; you should extract images from the
      PDF first (e.g., with Aspose PDF) and then feed them to the OCR engine.
    question: Does Aspose OCR support PDF input directly?
  - answer: The library handles images up to 30 MP without needing to load the whole
      file into memory, thanks to its streaming architecture.
    question: How large an image can I process?
  - answer: Absolutely—iterate over the files, reuse the same `OcrEngine` instance,
      and add each file to `OcrInput`. This reduces per‑image overhead dramatically.
    question: Is there a way to batch‑process a folder of images?
  - answer: Try adjusting `setContrastLevel` in smaller increments, experiment with
      `setDenoiseMode`, or enable `setUseAdaptiveThreshold(true)` for difficult backgrounds.
    question: What if the OCR output still contains errors?
  type: FAQPage
tags:
- Java
- OCR
- Image Processing
title: Comment améliorer l'OCR – prétraiter l'image pour l'OCR en Java avec Aspose
url: /fr/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraiter l'image pour OCR – guide complet Java

Vous avez déjà eu besoin de **prétraiter l'image pour OCR** mais vous n'étiez pas sûr des paramètres qui font réellement une différence ? Vous n'êtes pas seul. La plupart des développeurs jettent une image dans un moteur OCR en espérant que la magie opère, pour obtenir un résultat brouillé. Dans ce tutoriel, nous parcourrons un exemple pratique, de bout en bout, qui **augmente le contraste de l'image**, ajuste le **niveau de contraste**, et enfin **reconnaît le texte à partir de l'image** en utilisant Aspose OCR pour Java.

À la fin, vous disposerez d'un extrait de code réutilisable qui **extrait le texte à l'aide d'OCR** de manière fiable, même sur des numérisations bruyantes. Aucun tour de passe‑passe, juste des étapes claires et le raisonnement derrière chacune d'elles.

## Réponses rapides
- **Quelle est la première étape pour améliorer l'OCR ?** Chargez votre licence Aspose OCR avant de créer le moteur.  
- **Quelles sont les trois options de prétraitement les plus importantes ?** Redressement (deskew), débruitage (denoise) et amélioration du contraste.  
- **Quel niveau de contraste convient à la plupart des documents imprimés ?** Environ 1,3 f offre un bon équilibre.  
- **Puis-je voir l'image traitée ?** Oui—exportez le bitmap intermédiaire au format PNG.  
- **Ai‑je besoin d'une licence pour la production ?** Absolument ; la version d'essai fonctionne en mode limité et ajoute des filigranes.

## Comment améliorer l'OCR en prétraitant les images en Java ?

Chargez l'image, appliquez le redressement, le débruitage et ajustez le contraste, puis lancez le reconnaisseur. Le pipeline d'Aspose OCR traite l'image dans cet ordre exact, garantissant que chaque transformation agit sur les données les plus propres possibles avant que le reconnaisseur à réseau neuronal ne les voie. Cette approche en deux étapes—pré‑traiter puis reconnaître—offre jusqu'à 30 % de précision de caractères supérieure sur les documents numérisés typiques.

## Qu'est‑ce qu'Aspose OCR pour Java ?

Aspose OCR pour Java est une bibliothèque qui prend en charge **plus de 30 formats d'image** (y compris JPEG, PNG, TIFF, BMP) et peut traiter un lot multi‑image de 200 pages en moins de 2 secondes sur un serveur standard à 8 cœurs. Elle fournit des filtres intégrés de redressement, de débruitage et d'amélioration du contraste que vous pouvez configurer par programme.

## Ce dont vous aurez besoin

- Java 17 ou plus récent (tout JDK récent fonctionne)
- Bibliothèque Aspose OCR pour Java (téléchargez-la depuis le site officiel d'Aspose)
- Un fichier de licence Aspose OCR valide (`Aspose.OCR.lic`)
- Une image d'entrée (`input.jpg`) que vous souhaitez lire
- Votre IDE préféré ou une configuration simple en ligne de commande

Si vous avez déjà tout cela, super—plongeons directement.

## Quelle est la première étape : charger la licence Aspose OCR ?

Chargez la licence avant de créer tout objet OCR afin que le moteur fonctionne en mode complet plutôt qu'en mode d'évaluation. Cela empêche les filigranes, débloque toutes les options de prétraitement et garantit que le moteur OCR peut accéder aux packs de langues sous licence et aux optimisations de performances nécessaires à une extraction précise du texte.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Pourquoi c'est important :** Sans licence appropriée, le moteur fonctionne en mode d'évaluation, ce qui peut tronquer les résultats ou ajouter des filigranes. Définir la licence tôt garantit également que toutes les options de prétraitement ultérieures sont appliquées en mode complet.

## Comment initialiser le moteur OCR ?

La classe `OcrEngine` est le composant central qui effectue l'OCR et fournit les contrôles de prétraitement. Créez une seule instance `OcrEngine` et réutilisez‑la pour chaque image afin d'éviter le chargement répété du modèle. Réutiliser le moteur met en cache les modèles de réseau neuronal internes, ce qui réduit la latence par image jusqu'à 40 % et diminue la consommation de mémoire, rendant le traitement par lots plus efficace.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Astuce :** Conservez le moteur comme singleton si vous prévoyez de traiter de nombreuses images en lot ; il met en cache les ressources internes et accélère les appels suivants.

## Comment configurer le prétraitement – redressement, débruitage et amélioration du contraste

Voici où nous **prétraitons l'image pour OCR**. Les trois réglages que nous allons ajuster sont :

1. **Redressement** – corrige les légères rotations.
2. **Débruitage** – élimine les taches qui perturbent la segmentation des caractères.
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

Augmenter le niveau de contraste étire l'histogramme de l'image, rendant les pixels sombres plus sombres et les pixels clairs plus lumineux. En pratique, un **niveau de contraste** de `1.3f` offre souvent le meilleur équilibre pour les documents imprimés, tandis qu'une valeur supérieure à `1.5f` peut surexposer les traits fins. N'hésitez pas à expérimenter ; ce réglage est peu coûteux à modifier et peut améliorer de façon spectaculaire le taux de réussite de la **reconnaissance du texte à partir de l'image**.

## Comment préparer l'image d'entrée ?

La classe `OcrInput` représente une collection d'images que le moteur OCR traitera. La classe `OcrInput` abstrait la gestion des fichiers, vous permettant d'ajouter une ou plusieurs images pour le traitement par lots. Vous pouvez spécifier des chemins de fichiers individuels, des flux ou des tableaux d'octets, et le moteur traitera chaque entrée comme une page distincte, gérant automatiquement la détection du format et la conversion si nécessaire.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Cas particulier :** Si votre image est dans un format non standard (par ex., TIFF avec plusieurs pages), vous pouvez charger chaque page séparément ou la convertir d'abord en PNG/JPEG.

## Comment fonctionne l'étape de reconnaissance ?

Lorsque vous invoquez la méthode `recognize`, le moteur applique d'abord le pipeline de prétraitement configuré—redressement, débruitage et amélioration du contraste—dans cet ordre exact. Après le nettoyage de l'image, elle est transmise au reconnaisseur à réseau neuronal, qui analyse les formes des caractères et renvoie le texte extrait sous forme de chaîne.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Que se passe-t-il en coulisses ?** Aspose OCR applique d'abord la transformation de redressement, puis exécute le filtre de débruitage, et enfin ajuste le contraste avant d'alimenter l'image à son reconnaisseur basé sur un réseau neuronal. L'ordre est intentionnel ; le modifier pourrait conduire à des résultats sous‑optimaux.

## Comment obtenir le texte reconnu ?

Une fois la reconnaissance terminée, vous pouvez récupérer le résultat via `getText` ou `getTextLines`. Dans cet exemple nous affichons simplement la chaîne extraite dans la console, mais en production vous pourriez l'écrire dans un fichier, la stocker dans une base de données, ou l'envoyer sur un réseau vers des services en aval.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Sortie attendue

Si `input.jpg` contient la phrase « Hello World! », la console devrait afficher :

```
Hello World!
```

Si la sortie apparaît brouillée, revérifiez les valeurs de prétraitement—en particulier le **niveau de contraste** et le **mode de débruitage**—et essayez un format d'image différent.

## Comment visualiser l'image pré‑traitée (optionnel) ?

Si vous devez inspecter ce que le moteur OCR voit après le prétraitement, vous pouvez exporter le bitmap intermédiaire dans un fichier PNG à l'aide de la méthode `saveProcessedImage`. Cette vérification visuelle vous aide à confirmer que le redressement, le débruitage et les ajustements de contraste ont été appliqués correctement avant la reconnaissance.

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

![exemple de prétraitement d'image pour OCR](/images/ocr-preprocess-example.png "prétraitement d'image pour OCR – avant et après l'augmentation du contraste")
[exemple de prétraitement d'image pour OCR](/images/ocr-preprocess-example.png "prétraitement d'image pour OCR – avant et après l'augmentation du contraste")

*L'image ci‑dessus illustre comment l'augmentation du contraste et le débruitage transforment une numérisation floue en une image propre, prête pour l'OCR.*

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| **Sur‑contraste** (`setContrastLevel` trop élevé) | Le fond clair devient blanc, effaçant les caractères faibles | Gardez le niveau entre 1,1 et 1,4 pour la plupart des textes imprimés |
| **Tolérance de redressement trop basse** | Les petites rotations restent non corrigées | Augmentez `setDeskewAngleTolerance` à 0,2 ou 0,3 pour les livres numérisés |
| **Utilisation du débruitage GAUSSIEN sur des images binaires** | Brouille les bords, fusionnant les caractères | Utilisez `DenoiseMode.MEDIAN` pour les scans noir‑et‑blanc |
| **Licence manquante** | Le moteur revient en mode d'évaluation, tronquant la sortie | Vérifiez le chemin vers `Aspose.OCR.lic` et que le fichier est lisible |

## Questions fréquentes

**Q : Puis‑je utiliser cette approche pour des langues autres que l'anglais ?**  
R : Oui—chargez le pack de langue approprié avec `engine.setLanguage("fr")` ou tout code ISO supporté pour améliorer la précision pour le texte non anglais.

**Q : Aspose OCR prend‑il en charge l'entrée PDF directement ?**  
R : Il ne lit pas les pages PDF nativement ; vous devez d'abord extraire les images du PDF (par ex., avec Aspose PDF) puis les fournir au moteur OCR.

**Q : Quelle taille d'image puis‑je traiter ?**  
R : La bibliothèque gère des images jusqu'à 30 MP sans devoir charger le fichier complet en mémoire, grâce à son architecture en flux.

**Q : Existe‑t‑il un moyen de traiter par lots un dossier d'images ?**  
R : Absolument—parcourez les fichiers, réutilisez la même instance `OcrEngine`, et ajoutez chaque fichier à `OcrInput`. Cela réduit considérablement le surcoût par image.

**Q : Que faire si la sortie OCR contient encore des erreurs ?**  
R : Essayez d'ajuster `setContrastLevel` par petits incréments, expérimentez avec `setDenoiseMode`, ou activez `setUseAdaptiveThreshold(true)` pour les arrière‑plans difficiles.

## Prochaines étapes : aller au‑delà du prétraitement de base

Maintenant que vous pouvez **prétraiter l'image pour OCR** et **extraire le texte à l'aide d'OCR**, envisagez ces extensions :

- **Packs de langues** – chargez des dictionnaires de langue spécifiques pour améliorer la précision pour le texte non anglais.  
- **Recadrage de région d'intérêt (ROI)** – concentrez‑vous sur une sous‑section de l'image si vous n'avez besoin que d'une partie de la page.  
- **Traitement par lots** – parcourez un répertoire d'images, en réutilisant la même instance `OcrEngine` pour la rapidité.  
- **Intégration avec PDF** – combinez Aspose OCR avec Aspose PDF pour convertir des PDF numérisés en PDF recherchables en une seule chaîne.  

Chacun de ces sujets intègre naturellement nos mots‑clés secondaires : vous continuerez à **augmenter le contraste de l'image**, **définir le niveau de contraste**, et à **reconnaître le texte à partir de l'image** dans de nombreux scénarios.

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **prétraiter l'image pour OCR** avec Aspose OCR pour Java : charger la licence, configurer le redressement, le débruitage et l'amélioration du contraste, fournir l'image, et enfin **reconnaître le texte à partir de l'image**. Avec l'exemple complet et exécutable ci‑dessus, vous pouvez maintenant **extraire le texte à l'aide d'OCR** sur n'importe quelle image correctement préparée.

Testez le code, ajustez le **niveau de contraste**, et observez la précision grimper. Lorsque vous êtes prêt, explorez les modèles spécifiques aux langues ou les pipelines par lots pour transformer cette démo d'image unique en une solution de niveau production.

*Bon codage, et que vos numérisations soient toujours nettes !*

---

**Dernière mise à jour :** 2026-10-30  
**Testé avec :** Aspose OCR for Java 24.11  
**Auteur :** Aspose

## Tutoriels associés

- [Extraire du texte d'une image avec le guide Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Reconnaître du texte d'image avec Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Créer un moteur OCR Java pour reconnaître le texte d'images volumineuses](/ocr/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}