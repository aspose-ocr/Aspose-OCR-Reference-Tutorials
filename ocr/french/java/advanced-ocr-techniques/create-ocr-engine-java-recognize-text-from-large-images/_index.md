---
category: general
date: 2026-09-28
description: Apprenez à extraire du texte d'un TIFF en utilisant Aspose OCR en Java.
  Ce tutoriel étape par étape vous montre comment créer un moteur OCR, lire de gros
  fichiers TIFF et reconnaître le texte efficacement.
draft: false
keywords:
- extract text from tiff
- aspose ocr java tutorial
- read tiff file java
- large image ocr java
- ocr engine java
lastmod: 2026-09-28
og_description: Extraire du texte d'un TIFF en utilisant Aspose OCR en Java. Suivez
  ce tutoriel pour créer un moteur OCR, lire de gros fichiers TIFF et obtenir des
  résultats précis.
og_image_alt: Diagram showing OCR engine workflow for large TIFF files in Java
og_title: Extraire du texte d'un TIFF – guide Aspose OCR Java
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to extract text from TIFF using Aspose OCR in Java. This
    step‑by‑step tutorial shows you how to create an OCR engine, read large TIFF files,
    and recognize text efficiently.
  headline: Extract text from TIFF with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, provided you have a valid Aspose.OCR license. The library’s commercial
      license covers both development and production use.
    question: Can I use this solution in a commercial application?
  - answer: TIFF does not have a standard password mechanism, so the library treats
      it as a regular image. For encrypted containers (e.g., ZIP), decrypt before
      passing the stream to the engine.
    question: Does Aspose.OCR support password‑protected TIFF files?
  - answer: Aspose.OCR for Java supports JDK 8 through JDK 21, including both Java
      SE and OpenJDK distributions.
    question: Which Java versions are officially supported?
  - answer: 'Enable preprocessing: `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCE);`
      This boosts OCR confidence on noisy images.'
    question: How can I improve accuracy on low‑contrast scans?
  - answer: The engine can handle images up to several gigabytes, limited only by
      available disk space for temporary tiles. Memory usage stays under 200 MB thanks
      to streaming.
    question: Is there a limit to the image size I can process?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Extraire du texte d'un TIFF avec Aspose OCR en Java
url: /fr/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un TIFF avec Aspose OCR en Java  

Si vous devez **extraire du texte d'un TIFF** dont la taille atteint des dizaines ou des centaines de mégaoctets, ce tutoriel vous propose une solution prête pour la production. Vous apprendrez à créer un moteur OCR en Java, à diffuser un TIFF massif via `InputStream`, et à obtenir un texte Unicode précis sans épuiser le tas JVM.

## Réponses rapides
- **Quelle bibliothèque gère l'OCR de gros TIFF ?** Aspose.OCR for Java.  
- **Version minimale de Java ?** JDK 8 ou plus récent.  
- **Ai-je besoin d'une licence ?** Oui, un fichier `.lic` valide débloque le découpage en pleine résolution.  
- **Puis-je traiter des TIFF multi‑pages ?** Absolument – le moteur découpe chaque page automatiquement.  
- **Temps d'exécution typique pour une image de 50 MP ?** Environ 12 secondes sur un serveur standard à 4 cœurs.

## Qu'est-ce que l'extraction de texte d'un TIFF ?

**Extraire du texte d'un TIFF** signifie convertir le contenu visuel d'une image TIFF en caractères Unicode recherchables et modifiables à l'aide de la reconnaissance optique de caractères (OCR). Ce processus vous permet d'indexer des cartes numérisées, d'automatiser la saisie de données à partir de formulaires scannés, et de rendre les grandes images d'archives consultables sans retaper manuellement leur contenu. Le résultat est du texte brut qui peut être stocké, indexé ou intégré dans des pipelines d'analyse en aval.

## Pourquoi utiliser Aspose OCR pour Java ?

Aspose.OCR prend en charge **plus de 50 formats d'image**, peut traiter des **TIFF de plusieurs centaines de pages** sans charger le fichier complet en mémoire, et fournit une détection de langue intégrée ainsi que le découpage automatique. Ces fonctionnalités réduisent la consommation de mémoire jusqu'à 90 % par rapport aux approches naïves avec `BufferedImage`, tout en offrant une grande précision sur les scans bruyants ou à faible contraste. La bibliothèque propose également une intégration facile avec les autres produits Aspose pour la génération de PDF ou la conversion de documents.

## Prérequis
- Java Development Kit (JDK) 8 ou plus récent.  
- Aspose.OCR pour Java (dernière version en date de février 2026).  
- Un fichier TIFF volumineux que vous souhaitez traiter.  
- Un fichier de licence Aspose.OCR (`Aspose.OCR.lic`).  

> **Astuce :** Placez le fichier TIFF dans le même répertoire que votre code source ou référencez-le avec un chemin absolu ; le moteur gérera le découpage en interne, vous n'avez donc pas besoin de diviser l'image vous‑même.

![Create OCR Engine Java workflow](ocr-workflow.png){alt="Diagramme du flux de travail du moteur OCR Java"}  
[Flux de travail du moteur OCR Java](ocr-workflow.png)

## Comment extraire du texte d'un TIFF en Java ?

Chargez votre TIFF avec un `InputStream`, appliquez la licence, instanciez le moteur OCR, et appelez `recognize`. Le moteur découpera l'image, exécutera le modèle de réseau neuronal sur chaque tuile, et assemblera les résultats, délivrant le texte final en un seul appel. Cette approche évite de charger l'image entière en mémoire, ce qui la rend adaptée aux fichiers gigapixels tout en maintenant une utilisation prévisible du CPU.

### Étape 1 – appliquer votre licence Aspose.OCR (créer le moteur OCR Java)

La classe `License` indique au moteur OCR de débloquer l'algorithme de découpage en pleine résolution, ce qui est essentiel pour traiter efficacement une **grande image**.

```java
import com.aspose.ocr.*;

public class LicenseHelper {
    /** Loads the Aspose.OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);   // throws if the file is missing or invalid
    }
}
```  

*Pourquoi c'est important :* Sans licence, le moteur fonctionne en mode d'évaluation, limitant les pages et ajoutant un filigrane à la sortie.

### Étape 2 – instancier le moteur OCR (créer le moteur OCR Java)

`OcrEngine` est l'objet principal qui effectue la conversion pixel‑à‑texte.

```java
/** Returns a fresh OcrEngine ready for recognition. */
public static OcrEngine buildEngine() {
    // No special configuration needed for basic text extraction.
    // You can tweak language, DPI, or preprocessing here if required.
    return new OcrEngine();
}
```  

*Pourquoi nous le gardons simple :* Les paramètres par défaut incluent déjà la détection automatique de la langue et le découpage optimal. Une sur‑configuration peut en fait ralentir le traitement des fichiers volumineux.

### Étape 3 – charger le fichier TIFF en utilisant un `InputStream` (lire le fichier TIFF Java)

Le streaming du fichier empêche la JVM d'allouer un `BufferedImage` massif. Aspose.OCR lit et découpe l'image à la volée.

```java
import java.io.*;

public static InputStream openTiff(String filePath) throws FileNotFoundException {
    // Using try‑with‑resources later guarantees the stream is closed.
    return new FileInputStream(filePath);
}
```  

*Cas particulier :* Si votre TIFF utilise la compression CCITT Group 4, vous pouvez éventuellement définir `ocrEngine.getConfiguration().setTiffCompression(TiffCompression.CCITT4)` pour un léger gain de vitesse.

### Étape 4 – préparer l'entrée OCR et indiquer le format

`OcrInput` peut contenir plusieurs images, mais nous n'en avons besoin que d'une pour cette démonstration. Fournir la chaîne de format (`"tif"`) évite une détection de format coûteuse.

```java
import com.aspose.ocr.*;

public static OcrInput buildInput(InputStream imageStream) throws Exception {
    OcrInput input = new OcrInput();
    input.add(imageStream, "tif");   // second argument is the optional file extension hint
    return input;
}
```  

*Pourquoi l'indice est utile :* Lors du traitement d'**images volumineuses**, chaque milliseconde compte. L'indice de format indique à l'analyseur de contourner l'analyse coûteuse de l'en-tête.

### Étape 5 – reconnaître le texte de la grande image (reconnaître le texte d'une grande image)

L'appel OCR renvoie un `OcrResult` contenant le texte brut, les scores de confiance et des boîtes englobantes optionnelles.

```java
public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
    // The recognize method performs tiling internally, so memory usage stays low.
    return engine.recognize(input);
}
```  

*Ce qui se passe en coulisses :* Aspose.OCR divise le TIFF en tuiles de 1024 × 1024 px, exécute le modèle de réseau neuronal sur chaque tuile, et assemble les résultats. C'est pourquoi vous pouvez **reconnaître du texte à partir de fichiers d'images volumineuses** sans pré‑traitement manuel.

### Étape 6 – afficher un aperçu du texte extrait

Imprimer le document complet peut submerger la console. Afficher les 200 premiers caractères vous permet de vérifier rapidement la sortie.

```java
public static void printPreview(OcrResult result) {
    String text = result.getText();
    if (text.length() > 200) {
        System.out.println(text.substring(0, 200) + "…");
    } else {
        System.out.println(text);
    }
}
```  

**Sortie console attendue :**  

```
The quick brown fox jumps over the lazy dog. This map shows the historic...
```  

Si vous voyez du charabia, vérifiez que la langue correcte est sélectionnée (l'anglais par défaut) et que le TIFF n'est pas corrompu.

## Exemple complet fonctionnel

Assembler toutes les pièces vous donne une classe unique que vous pouvez compiler et exécuter :

```java
import com.aspose.ocr.*;
import java.io.*;

public class LargeImageDemo {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Apply your Aspose.OCR license (Create OCR Engine Java)
        // -------------------------------------------------
        LicenseHelper.applyLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Build the OCR engine (Create OCR Engine Java)
        // -------------------------------------------------
        OcrEngine ocrEngine = buildEngine();

        // -------------------------------------------------
        // 3️⃣ Open the huge TIFF (Read TIFF File Java)
        // -------------------------------------------------
        try (InputStream imageStream = openTiff("YOUR_DIRECTORY/huge-map.tif")) {

            // -------------------------------------------------
            // 4️⃣ Prepare OCR input, hint the format
            // -------------------------------------------------
            OcrInput ocrInput = buildInput(imageStream);

            // -------------------------------------------------
            // 5️⃣ Recognize text from large image (Recognize Text from Large Image)
            // -------------------------------------------------
            OcrResult ocrResult = runRecognition(ocrEngine, ocrInput);

            // -------------------------------------------------
            // 6️⃣ Show a preview of the extracted text
            // -------------------------------------------------
            printPreview(ocrResult);
        }
    }

    // Helper methods from previous sections ------------------------------------
    public static void applyLicense(String path) throws Exception {
        License lic = new License();
        lic.setLicense(path);
    }

    public static OcrEngine buildEngine() {
        return new OcrEngine();
    }

    public static InputStream openTiff(String filePath) throws FileNotFoundException {
        return new FileInputStream(filePath);
    }

    public static OcrInput buildInput(InputStream stream) throws Exception {
        OcrInput input = new OcrInput();
        input.add(stream, "tif");
        return input;
    }

    public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
        return engine.recognize(input);
    }

    public static void printPreview(OcrResult result) {
        String txt = result.getText();
        System.out.println(txt.length() > 200 ? txt.substring(0, 200) + "…" : txt);
    }
}
```  

Compiler avec :  

```bash
javac -cp "aspose-ocr-23.12.jar" LargeImageDemo.java
java -cp ".:aspose-ocr-23.12.jar" LargeImageDemo
```  

Remplacez `aspose-ocr-23.12.jar` par la version réelle que vous avez téléchargée.

## Écueils courants et astuces  

| Problème | Pourquoi cela se produit | Solution rapide |
|------|----------------|-----------|
| **OutOfMemoryError** | Chargement du TIFF dans un `BufferedImage` au lieu de le diffuser. | Utilisez toujours `InputStream` comme indiqué ; laissez Aspose gérer le découpage. |
| **Blank output** | Indice d'extension de fichier incorrect (`"tif"` vs `"tiff"`). | Utilisez la chaîne exacte que vous avez passée à `add`. |
| **Garbage characters** | Licence non appliquée ou expirée. | Vérifiez le chemin du fichier `.lic` et appliquez la licence avant de créer le moteur. |
| **Slow recognition** | Configuration `OcrConfiguration` personnalisée avec une haute résolution DPI. | Restez sur les paramètres par défaut ; modifiez uniquement si vous avez besoin d'une précision supérieure. |

### Quand ajuster les paramètres  

- **Documents multilingues :** `ocrEngine.getConfiguration().setLanguage(Language.English, Language.French);`  
- **Précision accrue sur les petites polices :** `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.ENHANCE);`  

Rappelez‑vous que chaque option supplémentaire peut augmenter le temps CPU, surtout sur une **grande image**. Testez d'abord avec une seule tuile.

## Quelles sont les prochaines étapes après l'extraction de texte d'un TIFF ?

Maintenant que vous pouvez **extraire du texte d'un TIFF** efficacement, envisagez d'étendre le flux de travail pour créer des PDF recherchables, stocker les coordonnées des boîtes englobantes pour la mise en évidence, ou paralléliser le traitement des tuiles sur plusieurs cœurs CPU. Ces améliorations vous permettent de construire des pipelines documentaires de bout en bout qui transforment d'énormes archives numérisées en ressources entièrement recherchables et indexées, adaptées à la recherche d'entreprise ou aux applications SIG.

## Questions fréquemment posées

**Q : Puis‑je utiliser cette solution dans une application commerciale ?**  
R : Oui, à condition de disposer d'une licence Aspose.OCR valide. La licence commerciale de la bibliothèque couvre à la fois le développement et l'utilisation en production.

**Q : Aspose.OCR prend‑il en charge les fichiers TIFF protégés par mot de passe ?**  
R : Le format TIFF ne possède pas de mécanisme de mot de passe standard, ainsi la bibliothèque le traite comme une image ordinaire. Pour les conteneurs chiffrés (par ex., ZIP), déchiffrez‑les avant de transmettre le flux au moteur.

**Q : Quelles versions de Java sont officiellement prises en charge ?**  
R : Aspose.OCR pour Java prend en charge les JDK 8 à JDK 21, incluant les distributions Java SE et OpenJDK.

**Q : Comment améliorer la précision sur les scans à faible contraste ?**  
R : Activez le prétraitement : `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCE);` Cela augmente la confiance de l'OCR sur les images bruyantes.

**Q : Existe‑t‑il une limite à la taille d'image que je peux traiter ?**  
R : Le moteur peut gérer des images de plusieurs gigaoctets, limitées uniquement par l'espace disque disponible pour les tuiles temporaires. L'utilisation de la mémoire reste inférieure à 200 Mo grâce au streaming.

**Dernière mise à jour :** 2026-09-28  
**Testé avec :** Aspose.OCR 23.12 pour Java  
**Auteur :** Aspose

## Tutoriels associés

- [Reconnaître le texte à partir d'une image avec le tutoriel Aspose OCR Java](/ocr/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/)
- [Extraire du texte d'une image avec le guide rapide Aspose OCR Java](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)
- [Reconnaître le texte d'une image en utilisant Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}