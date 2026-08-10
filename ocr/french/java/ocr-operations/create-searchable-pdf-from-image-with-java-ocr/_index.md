---
category: general
date: 2026-05-06
description: Créer un PDF consultable à partir d'une image en utilisant Aspose OCR
  en Java. Apprenez à convertir une image en PDF, à activer la correction orthographique
  et à utiliser le GPU OCR pour des résultats rapides.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: fr
og_description: Créer un PDF interrogeable à partir d'une image en utilisant Aspose
  OCR en Java. Ce guide montre comment convertir une image en PDF, activer la correction
  orthographique et utiliser le GPU OCR.
og_title: Créer un PDF consultable à partir d'une image avec OCR Java
tags:
- OCR
- Java
- PDF
title: Créer un PDF consultable à partir d'une image avec Java OCR
url: /fr/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d'une image avec Java OCR

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'une image numérisée mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—la plupart des développeurs rencontrent ce problème lorsqu'ils abordent pour la première fois les PDF basés sur des images. Heureusement, avec Aspose OCR for Java vous pouvez **convertir une image en PDF**, transformer le texte en contenu sélectionnable, et même ajouter une correction orthographique pour un résultat soigné.

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui montre comment **utiliser OCR GPU** lorsqu'il est disponible, comment **traiter l'OCR d'image** efficacement, et pourquoi activer la correction orthographique est important pour la recherche en aval. À la fin, vous disposerez d'une méthode en un clic pour générer un PDF consultable que vous pourrez distribuer aux utilisateurs ou archiver pour la conformité.

> **Astuce :** Si vous exécutez le code sur une machine sans GPU, le programme revient automatiquement au CPU, vous n'avez donc rien à réécrire.

---

## Ce dont vous avez besoin

- **Java 8+** (le code se compile avec JDK 8 et versions ultérieures)
- **Aspose OCR for Java** library (téléchargez le JAR le plus récent depuis le site Aspose)
- Une **image d'entrée** (JPEG, PNG, TIFF, etc.) que vous souhaitez transformer en PDF consultable
- (Optionnel) Un **GPU** avec prise en charge CUDA si vous voulez la reconnaissance la plus rapide possible

Pas de frameworks supplémentaires, pas de magie Maven/Gradle—juste un seul JAR sur le classpath et vous êtes prêt à partir.

---

## Étape 1 : Initialiser le moteur OCR – Le cœur du processus  

Tout d'abord, nous créons une instance `OcrEngine` et la pointons vers le fichier source. Cet objet est le cheval de bataille qui lira l'image, exécutera le réseau neuronal et nous renverra le texte.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Pourquoi c'est important :* Initialiser le moteur une fois et le réutiliser évite le surcoût de chargement répété des bibliothèques natives—un petit gain de performance qui s'accumule lorsqu'on traite par lots des dizaines de fichiers.

---

## Étape 2 : Choisir le dispositif de traitement – Utiliser OCR GPU lorsque possible  

Si votre poste de travail possède un GPU compatible, vous pouvez indiquer à Aspose d'exécuter le travail intensif dessus. Sinon, le moteur bascule automatiquement sur le CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Quel est le bénéfice ?* L'accélération GPU peut économiser des secondes par page, surtout pour les numérisations haute résolution. Le repli garantit que le même code fonctionne partout, c'est pourquoi nous recommandons **use OCR GPU** comme paramètre par défaut.

---

## Étape 3 : Accélérer le scan – Exploiter tous les cœurs CPU  

Même lorsque le GPU est occupé, les étapes de prétraitement environnantes peuvent être parallélisées. Définir le nombre de threads sur le nombre de processeurs disponibles donne au moteur la possibilité de traiter plusieurs morceaux simultanément.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Remarque :* Sur un ordinateur portable à 4 cœurs, cela créera quatre threads ; sur une station de travail à 16 cœurs, vous obtenez le plein bénéfice. Notez simplement que plus de threads impliquent une utilisation mémoire plus élevée.

---

## Étape 4 : Nettoyer l'image – Filtres de prétraitement  

Une numérisation floue ou bruitée produira du texte illisible. Ajouter quelques filtres intégrés améliore considérablement la précision.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Pourquoi ces filtres ?* `DeskewFilter` corrige la rotation qui survient souvent lorsqu'un document est passé au scanner sous un angle. `NoiseRemovalFilter` élimine les pixels parasites qui seraient autrement interprétés comme des caractères. Considérez cela comme fournir au moteur OCR une feuille propre à lire.

---

## Étape 5 : Activer les fonctionnalités intelligentes – Activer la correction orthographique & la détection automatique de langue  

Si vous traitez des documents multilingues, ou si vous souhaitez simplement moins de fautes, activez le correcteur orthographique intégré et laissez le moteur deviner la langue.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Quand est-ce utile ?* Supposons que votre numérisation contienne des sections en anglais et en espagnol. La fonction de détection automatique change les dictionnaires à la volée, tandis que la correction orthographique nettoie les caractères mal lus comme « 0 » à la place de « O ». Cette étape est essentielle pour produire un **PDF consultable** qui renvoie réellement des résultats corrects.

---

## Étape 6 : Enregistrer le résultat – Convertir l'image en PDF et le rendre consultable  

Enfin, nous demandons au moteur d'écrire un PDF où l'image originale se trouve derrière une couche de texte invisible. C'est le flux de travail classique de **convertir une image en PDF**, mais le PDF est désormais consultable.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Le fichier de sortie (`output-searchable.pdf`) peut être ouvert avec n'importe quel lecteur PDF ; vous pourrez sélectionner, copier et rechercher le texte comme dans un PDF natif. Aucun outil supplémentaire n'est requis.

---

## Exemple complet fonctionnel – Copier‑coller‑et‑exécuter  

Ci-dessous se trouve le programme complet, prêt à être compilé. Remplacez `YOUR_DIRECTORY` par le dossier contenant `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Sortie attendue :** Lorsque vous exécutez le programme, vous verrez la ligne de console *« Searchable PDF generated successfully. »* Ouvrir `output-searchable.pdf` dans Adobe Reader vous permet de taper un mot de l'image originale dans la zone de recherche et d'accéder instantanément à son emplacement.

---

## Questions fréquentes & cas particuliers  

- **Et si le GPU n’est pas détecté ?**  
  L’appel `setDeviceType(OcrDeviceType.GPU)` ne génère pas d’exception ; il indique simplement au moteur d’essayer le GPU en premier. S’il échoue, le moteur revient silencieusement au CPU.

- **Puis‑je traiter plusieurs images en une seule exécution ?**  
  Oui. Enveloppez le code dans une boucle, changez le nom de fichier à chaque itération, et réutilisez la même instance `OcrEngine` pour garder une faible consommation de mémoire.

- **Mon PDF est volumineux—comment le réduire ?**  
  Après l’OCR, vous pouvez exécuter les API d’optimisation PDF d’Aspose, ou simplement réduire la résolution de l’image source avant de la transmettre au moteur (`ImageStream.fromFile(...).setResolution(150)` pour 150 DPI).

- **Je dois conserver la résolution originale de l'image pour des raisons légales.**  
  Le format `PDF_SEARCHABLE` préserve le bitmap original exactement ; la couche de texte invisible est ajoutée au-dessus sans altérer la qualité visuelle.

---

## Résumé visuel  

![exemple de création de PDF consultable](placeholder-image.png "exemple de création de PDF consultable")

*Texte alternatif :* *exemple de création de PDF consultable – moteur OCR Java transformant un JPG numérisé en PDF consultable.*

---

## Conclusion  

Vous disposez maintenant d’une **solution complète, de bout en bout** pour transformer n'importe quelle image en **PDF consultable** en utilisant Aspose OCR for Java. En **convertissant une image en PDF**, **activant la correction orthographique**, et **utilisant OCR GPU** lorsque c’est possible, vous obtenez des résultats rapides, précis et consultables qui fonctionnent sur toutes les plateformes.

Et après ? Essayez d'expérimenter avec :

- **Différents formats de sortie** (`PDF`, `DOCX`, `HTML`) pour voir comment la couche de texte se comporte.
- **Dictionnaires personnalisés** si vous traitez du jargon spécifique à un domaine.
- **Traitement par lots** pour gérer automatiquement des milliers de numérisations.

N'hésitez pas à ajuster le nombre de threads, à remplacer les filtres, ou à intégrer votre propre pipeline de prétraitement. Le schéma de base reste le même : charger → prétraiter → configurer → OCR → enregistrer.

Bon codage, et que vos PDF soient toujours consultables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}