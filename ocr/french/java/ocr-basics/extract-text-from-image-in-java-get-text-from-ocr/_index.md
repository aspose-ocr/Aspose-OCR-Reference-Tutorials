---
category: general
date: 2026-05-25
description: Extraire du texte d’une image en Java avec OCR. Apprenez comment charger
  une image pour l’OCR, reconnaître le texte d’une photo et obtenir le texte de l’OCR
  avec un exemple de code simple.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: fr
og_description: Extraire du texte d’une image en Java avec un guide étape par étape.
  Apprenez à charger une image pour l’OCR, à reconnaître le texte à partir d’une photo
  et à obtenir le texte de l’OCR efficacement.
og_title: Extraire le texte d’une image en Java – Obtenir le texte via OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extraire le texte d’une image en Java – Obtenir le texte via OCR
url: /fr/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en Java – Obtenir du texte via OCR

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous ne saviez pas quelle bibliothèque Java choisir ? Vous n'êtes pas seul. Que vous numérisiez des reçus, extrayiez des numéros de série à partir de photos de produits, ou que vous vous amusiez simplement avec un projet secondaire, transformer une image en texte modifiable est un obstacle fréquent.

Dans ce tutoriel, nous passerons en revue un exemple complet, prêt à l'exécution, qui vous montre comment **charger une image pour l'OCR**, configurer le moteur, et enfin **reconnaître le texte d'une photo** afin que vous puissiez **obtenir du texte via OCR** en quelques lignes de code seulement. Pas de références vagues — tout ce dont vous avez besoin se trouve ici.

## Ce que vous apprendrez

* Comment configurer un moteur OCR léger en Java.  
* Les étapes exactes pour **charger une image pour l'OCR** et gérer différents chemins de fichiers.  
* Pourquoi la configuration de la langue est importante lorsque vous souhaitez **extraire du texte d'une image** qui n'est pas en anglais.  
* Comment afficher le résultat en toute sécurité et que faire lorsque le moteur ne renvoie rien.  
* Une poignée de conseils d'expert pour éviter les pièges les plus courants.

À la fin de ce guide, vous disposerez d'un programme autonome qui lit un JPEG (ou PNG) contenant des caractères ukrainiens et affiche la chaîne reconnue dans la console. N'hésitez pas à changer la langue ou l'image — tout est modulaire.

---

![Diagramme montrant le flux d'extraction de texte d'une image à l'aide du moteur OCR Java](/images/extract-text-from-image-java.png)

*Texte alternatif : Diagramme du processus d'extraction de texte d'une image en Java.*

## Prérequis

* **Java Development Kit (JDK) 11+** – le code utilise le système de modules moderne, mais les versions antérieures fonctionnent avec de légères modifications.  
* **Maven ou Gradle** – pour récupérer la bibliothèque OCR (nous utiliserons **Asprise OCR** comme une option légère et gratuite pour le développement).  
* Un fichier image d'exemple (par ex., `ukrainian_sign.jpg`) placé à un endroit où votre programme peut le lire.  
* Une connaissance de base de la méthode `main` de Java et de la gestion des exceptions.

Si vous avez tout cela, vous êtes prêt à commencer. Sinon, téléchargez le JDK depuis Oracle ou AdoptOpenJDK et configurez un projet Maven simple — rien de trop compliqué.

## Étape 1 : Ajouter la dépendance OCR

Tout d'abord, indiquez à votre outil de construction de récupérer le moteur OCR. Pour Maven, ajoutez ceci dans `pom.xml` :

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Si vous préférez Gradle, l'équivalent est :

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Ces coordonnées récupèrent un JAR compact qui inclut `OcrEngine`, `OcrLanguage` et les classes d'assistance que nous utiliserons. Aucun binaire natif supplémentaire n'est requis pour les scripts latins et cyrilliques de base.

## Étape 2 : Créer une classe Java pour **extraire du texte d'une image**

Nous allons maintenant écrire le programme réel. Enregistrez ce qui suit sous le nom `ExtractTextDemo.java` dans `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Pourquoi cette structure fonctionne

* **Des blocs numérotés séparés** facilitent le suivi du flux, surtout lorsque vous cherchez où **charger une image pour l'OCR** ou **reconnaître le texte d'une photo**.  
* Le `try/catch` autour du chargement de l'image et de la reconnaissance garantit que le programme échoue en douceur — utile lorsque le chemin du fichier est incorrect ou que le moteur OCR ne trouve pas les données de langue.  
* Définir la langue tôt (étape 2) améliore considérablement la précision pour les scripts non anglais. Si vous avez plus tard besoin de **java image to text** pour d'autres langues, remplacez simplement `OcrLanguage.UKRAINIAN` par `OcrLanguage.ENGLISH`, `FRENCH`, etc.

## Étape 3 : Construire et exécuter le programme

Depuis la racine du projet, exécutez :

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Ou, si vous utilisez Gradle :

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

En supposant que `ukrainian_sign.jpg` contienne le texte *«Ласкаво просимо»* (ukrainien pour «Welcome»), vous devriez voir quelque chose comme :

```
=== OCR Result ===
Ласкаво просимо
```

Cette sortie confirme que vous avez réussi à **extraire du texte d'une image** et à **obtenir du texte via OCR** en une seule exécution.

## Étape 4 : Ajuster le flux de travail – De **Java Image to Text** dans des projets réels

Bien que la démo soit minimale, les applications réelles nécessitent souvent un peu plus :

| Scénario | Ce qu'il faut ajuster | Raison |
|----------|-----------------------|--------|
| **Traitement par lots** | Parcourir une `List<Path>` et stocker chaque résultat dans une base de données. | Réduit le travail manuel lorsque vous avez des centaines de photos. |
| **Différents formats d'image** | Utilisez `ImageIO.read(new File(path))` pour pré‑traiter, puis passez le `BufferedImage` à `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Gère PNG, BMP, ou même les PDF après conversion. |
| **Optimisation des performances** | Appelez `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` si une précision légèrement moindre vous convient. | Accélère la reconnaissance sur du matériel bas de gamme. |
| **Post‑traitement** | Supprimez les espaces, remplacez les erreurs courantes d'OCR (`0` → `O`, `1` → `I`). | Améliore la qualité des données en aval. |

Ces variantes conservent l'idée principale — **reconnaître le texte d'une photo** — tout en vous offrant de la flexibilité pour les charges de travail en production.

## Pièges courants & conseils d'expert

1. **Mauvais réglage de la langue** – Si vous oubliez l'étape 2, le moteur utilise l'anglais par défaut, transformant les caractères cyrilliques en charabia. Vérifiez toujours le code de langue.  
2. **La qualité de l'image compte** – Les photos à faible résolution ou floues réduiront la précision. Pré‑traitez avec amélioration du contraste ou binarisation si nécessaire.  
3. **Astuces sur les chemins de fichiers** – Sous Windows, les antislashs doivent être échappés (`C:\\images\\file.jpg`). Utiliser `Path.of(...)` de `java.nio.file` contourne ce problème.  
4. **Fuites de mémoire** – `OcrEngine` détient des ressources natives. Appelez `ocrEngine.dispose()` lorsque vous avez terminé, surtout dans les services de longue durée.  
5. **Sécurité des threads** – Le moteur n'est pas thread‑safe par défaut. Créez une instance séparée par thread ou synchronisez l'accès.

## Exemple complet fonctionnel (tout‑en‑un)

Voici un fichier unique que vous pouvez copier‑coller dans n'importe quel IDE. Il inclut l'appel `dispose()` et une petite méthode d'aide pour rendre le code un peu plus propre.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Exécuter ce programme produit la même sortie console affichée précédemment. N'hésitez pas à remplacer `OcrLanguage.UKRAINIAN` par `OcrLanguage.ENGLISH` ou toute autre langue prise en charge pour voir comment le moteur s'adapte.

## Conclusion

Nous avons parcouru tout ce dont vous avez besoin pour **extraire du texte d'une image** avec Java : de l'ajout de la dépendance OCR à **charger une image pour l'OCR**, 

## Tutoriels associés

- [reconnaître le texte d'image avec Aspose OCR – Tutoriel complet OCR Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Comment faire de l'OCR sur le texte d'une image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convertir une image en texte en Java avec Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}