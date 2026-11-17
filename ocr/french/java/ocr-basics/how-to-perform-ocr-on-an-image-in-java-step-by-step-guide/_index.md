---
category: general
date: 2026-11-17
description: Apprenez à réaliser de l’OCR sur une image en Java et à extraire du texte
  à partir de photos grâce à un exemple de code simple. Inclut des astuces pour lire
  des images en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: fr
lastmod: 2026-11-17
og_description: Comment effectuer une OCR sur une image en Java et extraire rapidement
  le texte. Suivez ce guide pour lire une image en Java et convertir l’image en texte
  avec un exemple prêt à l’emploi.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Comment effectuer une OCR sur une image en Java – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Comment réaliser l’OCR sur une image en Java – guide pas à pas
url: /fr/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR sur une image en Java – guide étape par étape

Si vous avez besoin de **comment effectuer de l'OCR** sur une image, ce tutoriel vous montre une solution complète et exécutable en Java. Vous verrez comment lire un fichier image, configurer un moteur OCR et extraire le texte que le moteur reconnaît.

Travailler avec des documents numérisés, des reçus ou des captures d’écran nécessite souvent de convertir le contenu visuel en texte consultable. Ce guide vous accompagne à chaque étape, du chargement de l’image à l’affichage du texte extrait, et il aborde également les problèmes courants tels que les formats de fichiers non pris en charge et les résultats nuls.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

* Java Development Kit (JDK) 8 ou plus récent installé.
* Un outil de construction (Maven ou Gradle) pour récupérer la bibliothèque OCR.
* Un fichier image (JPEG, PNG, BMP) que vous souhaitez traiter.

Le code utilise la **bibliothèque OCR du package `com.asprise.ocr`** car elle ne nécessite qu’un seul JAR et fonctionne sur toutes les principales plateformes. Remplacez‑la par un autre fournisseur (Tesseract, Google Vision, etc.) en changeant les instructions d’importation et le code d’initialisation du moteur.

## Étape 1 : Ajouter la dépendance OCR

Si vous utilisez Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Pour Gradle, placez cette ligne dans `build.gradle` :

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Ces lignes garantissent que le code **read image Java** peut être compilé et que le moteur OCR est disponible à l’exécution.

## Étape 2 : Lire l’image avec Java

Lire un fichier image est la première étape concrète dans tout flux de travail **extract text image**. La classe intégrée `ImageIO` de Java gère la plupart des formats courants.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Pourquoi c’est important :** `ImageIO.read` renvoie `null` pour les formats non pris en charge ou les fichiers corrompus. La méthode ci‑dessus consigne le problème et renvoie `null` afin que l’étape suivante puisse réagir correctement.

## Étape 3 : Créer et configurer le moteur OCR

Le moteur OCR doit connaître la langue à reconnaître. Définir la langue améliore considérablement la précision, surtout pour les documents non anglais.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Pourquoi c’est important :** Démarrer le moteur est une opération relativement lourde, il faut donc le créer une fois et le réutiliser pour plusieurs images si votre application traite des lots.

## Étape 4 : Effectuer l’OCR et convertir l’image en texte

Une fois l’image chargée et le moteur prêt, vous pouvez lancer l’étape de reconnaissance. C’est le cœur du **comment effectuer de l'OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Gestion des cas limites :** Si l’image est `null`, la méthode renvoie une chaîne vide au lieu de lever une `NullPointerException`. Cela rend le code environnant plus robuste lorsqu’il traite des fichiers fournis par l’utilisateur.

## Étape 5 : Afficher le texte extrait

Enfin, imprimez le résultat dans la console ou transmettez‑le à un autre composant (par ex. une base de données ou un widget UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Lorsque vous exécutez le programme avec `java OcrDemo sample.jpg`, la console affiche les caractères reconnus. Cela complète le cycle **convert image to text**.

### Résultat attendu

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Si l’image ne contient aucun caractère lisible, le programme affiche `(no text detected)`.

## Variations courantes et comment les adapter

| Variation | Ce qui change | Quand l’utiliser |
|-----------|---------------|------------------|
| **Langue différente** | Remplacez `"eng"` par `"spa"` pour l’espagnol, `"fra"` pour le français, etc. | Documents rédigés dans une langue autre que l’anglais |
| **Traitement par lots** | Parcourez une liste de chemins de fichiers, réutilisez la même instance `Ocr`. | Grand nombre de pages numérisées |
| **Précision accrue** | Utilisez `Ocr.SPEED_SLOW` ou activez `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` pour des scans uniquement numériques. | Lorsque la qualité de l’OCR est critique (par ex. numéros de factures) |
| **Alternative Tesseract** | Changez l’import en `net.sourceforge.tess4j.Tesseract` et ajustez le code d’initialisation. | Projets qui dépendent déjà de Tesseract |

## Astuces pro

* **Redimensionnez les grandes images** avant de les transmettre au moteur ; la vitesse de l’OCR dépend du nombre de pixels.
* **Pré‑traitez** l’image (niveaux de gris, amélioration du contraste) avec des bibliothèques comme OpenCV si la source est bruitée.
* **Mettez en cache le moteur OCR** si vous l’appelez fréquemment sur une courte période — le démarrage et l’arrêt du moteur entraînent un surcoût.
* **Validez le résultat** avec des expressions régulières lorsque vous attendez un format précis (par ex. dates, numéros de téléphone).

## Conclusion

Vous savez maintenant **comment effectuer de l'OCR** sur une image en Java, depuis la lecture du fichier jusqu’à l’affichage du texte extrait. Le tutoriel a couvert les techniques **read image Java**, **extract text image**, **convert image to text** et **image to text java**, et il a fourni des conseils pratiques pour des scénarios réels.  

À partir d’ici, vous pouvez :

* Intégrer l’étape OCR dans un service web qui reçoit des téléchargements.
* Combiner la sortie avec un index de recherche pour une recherche en texte intégral sur les documents numérisés.
* Explorer des options OCR avancées telles que le support multilingue ou des jeux de caractères personnalisés.

Bon codage, et profitez de la transformation des images en texte consultable !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser d’autres fonctionnalités d’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}