---
category: general
date: 2026-05-06
description: Comment utiliser Aspose OCR pour reconnaître le texte à partir d’une
  image, activer la détection automatique de la langue et améliorer la vitesse d’OCR
  en Java.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: fr
og_description: Comment utiliser Aspose OCR pour reconnaître rapidement le texte d’une
  image, activer la détection automatique de la langue et améliorer la vitesse d’OCR
  en Java.
og_title: Comment utiliser Aspose OCR pour les images multilingues
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Comment utiliser Aspose OCR pour les images multilingues
url: /fr/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser Aspose OCR pour les images multilingues

Vous vous êtes déjà demandé **comment utiliser Aspose** pour extraire du texte d'une image contenant plusieurs langues à la fois ? Vous n'êtes pas seul—les développeurs se heurtent souvent à un mur lorsqu'une image mélange l'anglais, le russe, l'hindi ou tout autre script. La bonne nouvelle, c'est qu'Aspose OCR gère cela avec élégance, et vous pouvez même **reconnaître du texte à partir d'une image** plus rapidement en restreignant l'ensemble des langues.

Dans ce tutoriel, nous parcourrons un exemple Java complet, prêt à l'exécution, qui **charge l'image pour l'OCR**, active la **détection automatique de la langue**, et montre une astuce simple pour **améliorer la vitesse de l'OCR**. À la fin, vous disposerez d'un programme autonome qui affiche le texte extrait dans la console, et vous comprendrez pourquoi chaque paramètre est important.

> **Prérequis** – Java 17+ installé, Maven ou Gradle pour la gestion des dépendances, et une licence Aspose OCR (l'essai gratuit suffit pour l'évaluation). Aucune autre bibliothèque n'est requise.

---

## Étape 1 – Ajouter Aspose OCR à votre projet

Avant de pouvoir **utiliser Aspose**, vous devez ajouter la bibliothèque à votre classpath. Avec Maven, cela ressemble à ceci :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Si vous préférez Gradle :

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Astuce** : Restez sur la dernière version stable ; les versions plus récentes incluent souvent des améliorations de performance qui impactent directement **l'amélioration de la vitesse de l'OCR**.

---

## Étape 2 – Créer l'instance du moteur OCR  

Le cœur de chaque flux de travail Aspose OCR est le `OcrEngine`. L'instancier est simple, mais il faut noter que le moteur possède des caches internes. Réutiliser une seule instance sur de nombreuses images peut réellement **améliorer la vitesse de l'OCR** car la bibliothèque évite des initialisations natives répétées.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Étape 3 – **Charger l'image pour l'OCR**  

Aspose accepte de nombreux formats d'image (PNG, JPEG, TIFF, BMP). Ici, nous démontrons le chargement d'un PNG contenant du texte en anglais, russe et hindi. L'aide `ImageStream.fromFile` abstrait les détails d'E/S de fichiers et garantit que l'image est correctement diffusée vers le moteur.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **Et si l'image est en mémoire ?** Utilisez `ImageStream.fromByteArray(byte[])` à la place—parfait pour les services web qui reçoivent des images sous forme de flux d'octets.

---

## Étape 4 – Activer la détection automatique de la langue  

Par défaut, Aspose OCR suppose une seule langue, ce qui peut entraîner une sortie illisible sur des images multilingues. Activer la détection automatique indique au moteur de détecter le script de chaque bloc de texte avant la reconnaissance.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Étape 5 – **Améliorer la vitesse de l'OCR** en restreignant le pool de langues  

La détection automatique complète parcourt toutes les langues prises en charge par Aspose (plus de 70). Si vous connaissez à l'avance les langues possibles, vous pouvez donner un indice au moteur. Fournir un tableau plus petit réduit l'espace de recherche et donc **améliore la vitesse de l'OCR**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Pourquoi cela aide-t-il ?** Le moteur ignore les modèles de langue dont il n'a pas besoin, économisant des cycles CPU et de la mémoire. Si vous ajoutez plus tard d'autres langues, il suffit de mettre à jour le tableau—aucune réécriture de code n'est nécessaire.

---

## Étape 6 – Effectuer la reconnaissance et **reconnaître le texte à partir de l'image**  

C'est maintenant que le travail lourd s'effectue. `recognize()` renvoie un objet `OcrResult` contenant le texte brut, les scores de confiance, et même les informations de mise en page si vous en avez besoin plus tard.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Sortie console attendue

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Si l'image contient du bruit supplémentaire ou du texte incliné, vous pourriez voir une confiance plus faible pour ces lignes. Dans ce cas, envisagez de pré‑traiter l'image (redressement, binarisation) avant de la transmettre à Aspose.

---

## Questions fréquentes & cas limites

### Et si l'image est très grande (par ex., >10 MP) ?

Les grandes images consomment plus de mémoire et peuvent ralentir le traitement. Un moyen rapide d'**améliorer la vitesse de l'OCR** consiste à réduire la taille de l'image tout en préservant la lisibilité :

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Comment gérer les scripts de droite à gauche comme l'arabe ?

Aspose OCR respecte automatiquement la direction du script, mais vous pouvez souhaiter définir le drapeau `RightToLeft` pour le post‑traitement :

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Puis‑je extraire du texte à partir de PDF au lieu d'images ?

Oui—convertissez chaque page PDF en image (à l'aide d'Aspose PDF ou de tout rasteriseur) et alimentez le résultat dans le même pipeline OCR. La même logique de **reconnaître le texte à partir de l'image** s'applique.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Enregistrez le fichier sous le nom `MixedLanguageDemo.java`, compilez avec `javac`, et exécutez avec `java MixedLanguageDemo`. Si tout est correctement configuré, vous verrez le texte multilingue affiché dans la console.

---

## Conclusion

Vous savez maintenant **comment utiliser Aspose** pour **reconnaître le texte à partir d'une image** contenant plusieurs langues, comment **activer la détection automatique de la langue**, et une astuce pratique pour **améliorer la vitesse de l'OCR** en limitant le pool de langues. Le code complet ci‑dessus est prêt à copier‑coller, et les explications devraient vous donner la confiance nécessaire pour adapter la solution—que vous ayez besoin de **charger l'image pour l'OCR** depuis un flux, un tableau d'octets, ou même un instantané de webcam.

Prochaines étapes ? Essayez d'expérimenter avec :

* Ajouter un pré‑traitement d'image (débruitage, binarisation) pour les scans de faible qualité.  
* Exporter `OcrResult` en JSON pour les services en aval.  
* Intégrer le moteur dans un point d'accès REST Spring Boot afin que les clients puissent télécharger des images et recevoir le texte extrait instantanément.

Bon codage, et que vos pipelines OCR soient rapides, précis et multilingues !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}