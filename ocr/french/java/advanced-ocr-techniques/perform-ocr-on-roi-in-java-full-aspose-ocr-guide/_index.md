---
category: general
date: 2026-06-19
description: Effectuez la reconnaissance optique de caractères (OCR) sur une zone
  d'intérêt (ROI) en Java avec Aspose OCR. Apprenez à reconnaître le texte dans une
  région grâce à un code étape par étape et aux meilleures pratiques.
draft: false
keywords:
- perform OCR on ROI
- recognize text in region
- Aspose OCR Java
- OCR region detection
- Java image processing
language: fr
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une zone
  d'intérêt (ROI) en Java avec Aspose OCR. Ce guide vous montre comment reconnaître
  le texte dans une région, gérer plusieurs langues et éviter les pièges courants.
og_title: Effectuer la reconnaissance optique de caractères (OCR) sur la ROI en Java
  – Tutoriel complet Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  headline: Perform OCR on ROI in Java – Full Aspose OCR Guide
  type: TechArticle
- description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  name: Perform OCR on ROI in Java – Full Aspose OCR Guide
  steps:
  - name: 1. License Path Errors
    text: If `setLicense` throws a `FileNotFoundException`, double‑check the absolute
      path or place the `.lic` file in the project’s resources folder and load it
      with `getResourceAsStream`.
  - name: 2. Overlapping or Out‑of‑Bounds ROIs
    text: Aspose does not automatically clip ROIs that extend beyond the image dimensions.
      Overlapping rectangles can cause duplicated text. Use `engine.getImageSize()`
      to verify bounds before creating rectangles.
  - name: 3. Unsupported Languages
    text: Attempting to set a language not bundled with the library will raise `UnsupportedOperationException`.
      Stick to the languages listed in Aspose’s documentation, or download the additional
      language packs.
  - name: 4. Low‑Resolution Images
    text: OCR accuracy drops dramatically below 100 dpi. If you have a low‑resolution
      scan, consider up‑scaling with a library like **Imgscalr** before feeding it
      to Aspose.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Recognition
title: Effectuer la reconnaissance optique de caractères (OCR) sur la ROI en Java
  – Guide complet Aspose OCR
url: /fr/java/advanced-ocr-techniques/perform-ocr-on-roi-in-java-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une ROI en Java – Tutoriel complet Aspose OCR

Vous vous êtes déjà demandé comment **perform OCR on ROI** en Java ? Vous n'êtes pas le seul—les développeurs demandent constamment, *« Comment extraire uniquement la partie tableau d’une facture sans scanner l’image entière ? »* Dans ce guide, nous allons vous montrer exactement comment **perform OCR on ROI** en utilisant Aspose OCR, et nous vous montrerons également comment **recognize text in region** lorsque différentes langues apparaissent côte à côte.

Voici le point : cibler un rectangle spécifique (ou ROI) permet d’économiser du temps de traitement, de réduire le bruit et donne souvent des résultats plus propres. Que vous travailliez avec des reçus multilingues, des formulaires ou des contrats numérisés, maîtriser l’OCR basé sur les ROI est un véritable atout. Plongeons‑y.

## Ce dont vous avez besoin

- **Java 8+** (le code fonctionne avec n'importe quel JDK récent)
- **Aspose.OCR for Java** library (téléchargez depuis le site Aspose ou ajoutez via Maven)
- Un fichier de licence **Aspose OCR** valide (`Aspose.OCR.lic`) – la démo fonctionne sans licence mais ajoute un filigrane.
- Une image contenant des régions distinctes que vous souhaitez traiter (par ex., une facture avec un en‑tête et un tableau français).

C’est tout—pas de frameworks supplémentaires, pas de dépendances lourdes. Si vous êtes à l’aise avec un IDE basique comme IntelliJ IDEA ou Eclipse, vous êtes prêt.

## Effectuer une OCR sur une ROI – Configuration du moteur

La première étape consiste à préparer le moteur OCR et à lui indiquer la langue à utiliser par défaut. C’est ici que le flux **perform OCR on ROI** commence réellement.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

> **Astuce :** Si vous oubliez de définir la licence, Aspose fonctionnera tout de même mais ajoutera un filigrane « Evaluation » dans la sortie. Cela ne pose aucun problème pour les tests mais pas pour la production.

## Définir les régions que vous souhaitez reconnaître

Nous créons maintenant les rectangles qui représentent les parties de l’image qui nous intéressent. Considérez chaque `Rectangle` comme une « boîte de découpe » qui indique au moteur *où* regarder.

```java
        // Step 2: Create an OCR engine and set the default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Step 3: Define the regions (ROIs) you want to recognize
        // Header region (top part of the image)
        Rectangle header = new Rectangle(0, 0, 1200, 200);
        // Table body region (below the header)
        Rectangle table = new Rectangle(0, 210, 1200, 800);
```

Remarquez comment nous utilisons implicitement la terminologie **perform OCR on ROI**—chaque `Rectangle` est une ROI. Vous pouvez ajuster les coordonnées pour correspondre à la mise en page de votre document. Le rectangle `header` capture la bannière supérieure, tandis que le rectangle `table` saisit le corps où nous **recognize text in region** plus tard.

## Ajouter des régions et définir les langues par région

Aspose OCR vous permet d’assigner une langue par région, ce qui est parfait pour les documents multilingues. Ici nous gardons l’anglais pour l’en‑tête et passons au français pour le tableau.

```java
        // Step 4: Add the regions to the engine
        engine.addRegion(header);                     // uses default language (English)
        engine.addRegion(table, Language.French);    // optional per‑region language
```

Si vous n’avez besoin que d’une seule langue, vous pouvez omettre le deuxième argument. Le moteur reviendra automatiquement à la langue par défaut que vous avez définie précédemment.

## Effectuer une OCR sur une ROI et récupérer le texte combiné

Enfin, nous exécutons le processus OCR sur l’image entière, mais seules les ROI définies seront traitées. Le résultat concatène le texte dans l’ordre où vous avez ajouté les régions, ce qui simplifie le post‑traitement.

```java
        // Step 5: Perform OCR on the image and retrieve the combined text
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");
        System.out.println(result.getText()); // text from all defined regions in order
    }
}
```

**Sortie attendue** (troncée pour plus de concision) :

```
Invoice #12345
Date: 2026‑06‑01
...
Produit   Quantité   Prix
Café      2          5,00 €
...
```

Le premier bloc provient de l’en‑tête anglais, le second du tableau français—un exemple classique de **recognize text in region** avec des langues mixtes.

## Gestion des problèmes courants

Même un flux **perform OCR on ROI** simple peut rencontrer quelques pièges cachés. Voici les problèmes les plus fréquents et comment les éviter.

### 1. Erreurs de chemin de licence

Si `setLicense` lève une `FileNotFoundException`, vérifiez le chemin absolu ou placez le fichier `.lic` dans le dossier resources du projet et chargez‑le avec `getResourceAsStream`.

```java
License license = new License();
license.setLicense(RoiDemo.class.getResourceAsStream("/Aspose.OCR.lic"));
```

### 2. ROI qui se chevauchent ou hors limites

Aspose ne découpe pas automatiquement les ROI qui dépassent les dimensions de l’image. Les rectangles qui se chevauchent peuvent entraîner du texte dupliqué. Utilisez `engine.getImageSize()` pour vérifier les limites avant de créer les rectangles.

```java
Size imgSize = engine.getImageSize("YOUR_DIRECTORY/invoice.png");
if (header.getRight() > imgSize.getWidth()) {
    // Adjust width to stay inside the image
    header.setWidth(imgSize.getWidth() - header.getX());
}
```

### 3. Langues non prises en charge

Essayer de définir une langue qui n’est pas fournie avec la bibliothèque déclenchera une `UnsupportedOperationException`. Restez sur les langues listées dans la documentation d’Aspose, ou téléchargez les packs de langues supplémentaires.

### 4. Images à basse résolution

La précision de l’OCR chute fortement en dessous de 100 dpi. Si vous avez une numérisation à basse résolution, envisagez de l’agrandir avec une bibliothèque comme **Imgscalr** avant de la transmettre à Aspose.

```java
BufferedImage src = ImageIO.read(new File("invoice.png"));
BufferedImage highRes = Scalr.resize(src, Scalr.Method.QUALITY, 300);
ImageIO.write(highRes, "png", new File("invoice_high.png"));
```

Puis pointez `recognizeImage` vers `invoice_high.png`.

## Extension de l’exemple : multiples ROI et détection dynamique

La démo utilise des rectangles statiques, mais dans des scénarios réels vous pourriez vouloir détecter les tableaux automatiquement. Combinez Aspose OCR avec une bibliothèque simple de **traitement d’image** (par ex., OpenCV) pour localiser les contours, puis transmettez ces limites à `engine.addRegion`. Cela transforme un script **perform OCR on ROI** statique en un pipeline dynamique qui fonctionne avec n’importe quelle mise en page de facture.

```java
// Pseudo‑code: Detect contours → create Rectangle objects → addRegion()
List<Rect> detected = OpenCVHelper.findTables("invoice.png");
for (Rect r : detected) {
    engine.addRegion(new Rectangle(r.x, r.y, r.width, r.height), Language.French);
}
```

Vous pouvez maintenant **recognize text in region** sans coder en dur les valeurs de pixels—pratique pour le traitement par lots.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être exécuté. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Apply license (optional for evaluation)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Initialize engine with default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Define ROIs
        Rectangle header = new Rectangle(0, 0, 1200, 200);   // top banner
        Rectangle table  = new Rectangle(0, 210, 1200, 800); // body table

        // Add regions – per‑region language optional
        engine.addRegion(header);                     // English (default)
        engine.addRegion(table, Language.French);    // French for table

        // Run OCR on the image – only the defined ROIs are processed
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");

        // Output combined text
        System.out.println("--- OCR Result ---");
        System.out.println(result.getText());
    }
}
```

Exécutez `javac RoiDemo.java && java RoiDemo`. Si tout est correctement configuré, vous verrez le texte concaténé des deux régions affiché dans la console.

## Conclusion

Nous venons de couvrir comment **perform OCR on ROI** en Java avec Aspose OCR, et vous savez maintenant comment **recognize text in region** pour des scénarios monolingues et multilingues. En découpant l’image en rectangles logiques, vous :

1. Réduisez le temps de traitement,
2. Diminuez les faux positifs,
3. Obtenez un contrôle granulaire sur la sélection de la langue.

À partir de là, vous pouvez explorer la détection dynamique de ROI, intégrer les résultats dans une base de données, ou générer des PDF recherchables. Le ciel est la limite—souvenez‑vous simplement de valider les coordonnées des ROI, de garder le chemin de licence propre, et de choisir les bons packs de langues.

Vous avez une mise en page compliquée qui vous pose problème ? Laissez un commentaire ou soumettez une pull request avec vos améliorations. Bon codage, et que votre OCR soit toujours précis !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment reconnaître les rectangles de page pour la reconnaissance de texte OCR avec Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Extraire du texte d’une image Java avec le mode Détection de zones d’Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Comment faire de l’OCR de texte d’image avec sélection de langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}