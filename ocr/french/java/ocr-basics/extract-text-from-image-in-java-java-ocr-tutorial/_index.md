---
category: general
date: 2026-03-07
description: Extraire du texte d’une image avec Java OCR. Apprenez comment charger
  une image pour l’OCR, configurer la langue et suivre un tutoriel complet Java OCR
  en quelques minutes.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: fr
og_description: Extraire du texte d’une image avec Java OCR. Ce tutoriel montre comment
  charger une image pour l’OCR, configurer la langue et suivre un tutoriel Java OCR
  étape par étape.
og_title: Extraire du texte d'une image en Java – Guide complet d'OCR
tags:
- OCR
- Java
- Image Processing
title: Extraire du texte d’une image en Java – Tutoriel OCR Java
url: /fr/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en Java – Guide complet OCR

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous ne saviez pas par où commencer en Java ? Vous n'êtes pas le seul—les développeurs rencontrent constamment ce problème lorsqu'ils transforment des panneaux scannés, des reçus ou des notes manuscrites en chaînes recherchables.  

La bonne nouvelle ? En quelques minutes seulement, vous pouvez disposer d'un pipeline OCR fonctionnel qui lit le Kannada, l'anglais ou toute langue prise en charge. Dans ce tutoriel, nous allons **charger l'image pour l'OCR**, configurer le moteur, et parcourir un **tutoriel OCR Java** que vous pouvez copier‑coller et exécuter dès aujourd'hui.

## Ce que couvre ce guide

Nous commencerons par lister les outils dont vous aurez besoin, puis plongerons directement dans une implémentation **étape par étape**. À la fin, vous serez capable de :

* Charger un fichier image dans un `ImageInputStream` Java.
* Configurer un moteur OCR pour reconnaître une langue spécifique (Kannada dans notre exemple).
* Exécuter le processus de reconnaissance et afficher le texte extrait.
* Ajuster les paramètres pour une meilleure précision et gérer les pièges courants.

Aucune documentation externe requise—tout ce dont vous avez besoin se trouve ici.  

**Prérequis** : Java 17 ou plus récent, un outil de construction comme Maven ou Gradle, et une bibliothèque OCR qui propose une classe `OcrEngine` (par exemple, le SDK hypothétique *SimpleOCR*). Si vous utilisez Maven, ajoutez la dépendance montrée plus tard.

---

## Étape 1 – Configurer votre projet et ajouter la bibliothèque OCR

Avant d'écrire du code, assurez-vous que votre projet peut accéder aux classes OCR. Avec Maven, insérez cet extrait dans votre `pom.xml` :

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Si vous préférez Gradle, l'équivalent est :

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Astuce :** Gardez la version de la bibliothèque à jour ; les nouvelles versions incluent souvent des améliorations des modèles linguistiques qui augmentent la précision.

Une fois la dépendance résolue, rafraîchissez votre IDE et vous êtes prêt à coder.

## Étape 2 – Importer les classes requises

Voici la liste complète des imports dont vous aurez besoin pour l'exemple. Ils sont délibérément réduits au minimum afin que vous puissiez voir exactement ce que chaque classe fait.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Pourquoi ces imports ?** `OcrEngine` et `OcrResult` sont le cœur du processus OCR, tandis que `ImageInputStream` abstrait la gestion de lecture de fichiers. L'utilisation de `java.nio.file.Paths` rend le code indépendant du système d'exploitation.

## Étape 3 – Charger l'image pour l'OCR

Voici la partie qui fait souvent trébucher les gens : fournir le bon format d'image au moteur. Le SDK OCR attend un `ImageInputStream`, que vous pouvez obtenir à partir de n'importe quel fichier sur le disque.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Cas limite :** Si l'image est corrompue ou dans un format non pris en charge (par ex., GIF), le constructeur lèvera une `IOException`. Enveloppez l'appel dans un bloc try‑catch ou validez le fichier au préalable.

## Étape 4 – Configurer le moteur pour reconnaître une langue spécifique

La plupart des moteurs OCR offrent un support multilingue. Pour améliorer la précision, vous devez indiquer au moteur exactement quelle langue rechercher. Dans notre cas, nous utilisons le code langue `"kn"` pour le Kannada.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Pourquoi définir la langue ?** Limiter l'ensemble des caractères réduit les faux positifs, surtout lorsqu'on traite des scripts contenant de nombreux glyphes similaires.

Si vous avez besoin de changer de langue, il suffit de modifier la chaîne de code—aucun autre changement n'est nécessaire.

## Étape 5 – Exécuter le processus OCR et extraire le texte

Avec l'image chargée et le moteur configuré, la reconnaissance réelle se fait en un seul appel de méthode. L'objet résultat vous fournit le texte brut et, éventuellement, les scores de confiance.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Question fréquente :** *Et si l'OCR renvoie une chaîne vide ?*  
> Cela signifie généralement que la qualité de l'image est trop basse (flou, faible contraste) ou que la langue n'a pas été correctement définie. Essayez de prétraiter l'image (augmenter le contraste, binariser) ou revérifiez le code de langue.

## Étape 6 – Afficher le résultat

Enfin, affichez la sortie dans la console. Dans une application réelle, vous pourriez la stocker dans une base de données ou l'alimenter dans un index de recherche.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Sortie attendue

Si l'image source contient la phrase kannada « ಕರ್ನಾಟಕ » (Karnataka), la console devrait afficher :

```
Extracted text:
ಕರ್ನಾಟಕ
```

Voilà—un flux de travail complet **utiliser OCR en Java** que vous pouvez adapter à n'importe quelle langue ou source d'image.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être compilé. Remplacez `YOUR_DIRECTORY` par le chemin réel vers votre fichier image.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Conseil :** Pour le code de production, envisagez de réutiliser une seule instance de `OcrEngine` pour plusieurs images ; la créer à chaque fois peut être coûteux.

---

## Questions fréquentes & cas limites

### Comment améliorer la précision sur des photos bruyantes ?

- **Pré‑traiter** l'image : convertir en niveaux de gris, appliquer un filtrage médian, ou augmenter le contraste.
- **Redimensionner** l'image à au moins 300 DPI ; la plupart des moteurs OCR attendent cette résolution.
- **Définir une liste blanche** de caractères si vous connaissez la sortie attendue (par ex., uniquement des chiffres).

### Puis-je utiliser cette approche pour les PDF ?

Oui. Extrayez chaque page sous forme d'image (avec PDFBox ou iText), puis alimentez ces images dans le même pipeline. Le code reste identique ; seul la source d'image change.

### Que faire si je dois reconnaître plusieurs langues dans une même image ?

La plupart des SDK permettent de passer une liste séparée par des virgules, comme `"en,kn"`. Le moteur tentera de correspondre à l'un des scripts fournis.

### Existe-t-il un moyen d'obtenir les scores de confiance ?

`OcrResult` inclut souvent une méthode `getConfidence()` qui renvoie un flottant entre 0 et 1 pour chaque ligne. Utilisez‑la pour filtrer les résultats à faible confiance.

---

## Prochaines étapes

Maintenant que vous pouvez **extraire du texte d'une image** avec Java, vous pourriez explorer :

* **Traitement par lots** – parcourir un dossier d'images et écrire les résultats dans un CSV.
* **Intégration avec Apache Tika** – combiner l'OCR avec l'analyse de documents pour un index de recherche unifié.
* **API côté serveur** – exposer la logique OCR via un endpoint REST (Spring Boot rend cela trivial).
* **Bibliothèques alternatives** – essayer Tesseract via `tess4j` si vous avez besoin d'une solution open‑source.

Chacun de ces sujets s'appuie sur les concepts de base abordés dans ce **tutoriel OCR Java**, n'hésitez donc pas à expérimenter et à étendre le code.

---

## Conclusion

Nous avons parcouru un exemple complet en Java qui **extrait du texte d'une image**, montrant exactement comment **charger l'image pour l'OCR**, configurer les paramètres de langue, et **utiliser l'OCR en Java** pour récupérer des chaînes lisibles. Le fragment est autonome, gère les erreurs avec grâce, et peut être intégré dans n'importe quel projet Java avec un minimum d'effort.  

Essayez-le, ajustez le code de langue, et bientôt vous transformerez des documents scannés en données recherchables sans effort. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}