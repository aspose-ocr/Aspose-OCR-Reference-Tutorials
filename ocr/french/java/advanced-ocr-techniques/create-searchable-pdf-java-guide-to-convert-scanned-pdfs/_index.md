---
category: general
date: 2026-02-22
description: Créer un PDF consultable à partir d’un PDF numérisé en utilisant Aspose
  OCR en Java. Apprenez à convertir un PDF numérisé, à compresser les images du PDF
  et à reconnaître le texte OCR du PDF efficacement.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: fr
og_description: Créer un PDF consultable à partir d’un PDF numérisé en utilisant Aspose
  OCR en Java. Ce tutoriel étape par étape montre comment convertir un PDF numérisé,
  compresser les images du PDF et reconnaître le texte OCR du PDF.
og_title: Créer un PDF recherchable – Guide Java pour convertir les PDF numérisés
tags:
- Java
- OCR
- PDF
- Aspose
title: Créer un PDF recherchable – Guide Java pour convertir les PDF numérisés
url: /fr/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF interrogeable – Guide Java pour convertir les PDF numérisés

Vous avez déjà eu besoin de **créer un PDF interrogeable** à partir d’une pile de documents numérisés ? C’est un problème fréquent — vos PDF ont l’air correct, mais vous ne pouvez pas faire *Ctrl + F* pour trouver quoi que ce soit. La bonne nouvelle ? En quelques lignes de Java et Aspose OCR, vous pouvez transformer ces PDF uniquement image en fichiers entièrement interrogeables, **convertir un PDF numérisé** en texte, et même réduire le résultat en **compressant les images du PDF**.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable, expliquerons pourquoi chaque paramètre est important, et vous montrerons comment ajuster le processus pour des cas particuliers comme les numérisations multi‑pages ou les images basse résolution. À la fin, vous disposerez d’un extrait de code solide, prêt pour la production, qui **reconnaît pdf ocr** de manière fiable et produit un document interrogeable propre.

---

## Ce dont vous avez besoin

- **Java 17** (ou tout JDK récent ; l’API est indépendante du JDK)  
- **Aspose.OCR for Java** library – vous pouvez l’obtenir depuis Maven Central (`com.aspose:aspose-ocr`)  
- Un PDF numérisé (image‑only) que vous souhaitez rendre interrogeable  
- Un IDE ou éditeur de texte avec lequel vous êtes à l’aise (IntelliJ, VS Code, Eclipse…)

Pas de frameworks lourds, pas de services externes—juste du Java pur et un seul JAR tiers.  

---

![exemple de PDF interrogeable](placeholder-image.png "Illustration d’un PDF interrogeable créé à partir d’un document numérisé")

*Texte alternatif de l’image :* **exemple de PDF interrogeable** illustration montrant avant‑et‑après d’un PDF numérisé transformé en texte interrogeable.

---

## Étape 1 – Initialiser le moteur OCR  

La première chose à faire est d’instancier un `OcrEngine`. Considérez‑le comme le cerveau qui analysera chaque bitmap à l’intérieur du PDF et produira des caractères Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Astuce :** Si vous prévoyez de traiter de nombreux PDF consécutivement, réutilisez le même `OcrEngine` plutôt que d’en créer un nouveau à chaque fois. Cela économise quelques millisecondes et réduit le turnover de mémoire.

---

## Étape 2 – Configurer les options OCR spécifiques aux PDF  

Aspose vous permet d’ajuster finement la façon dont le PDF de sortie est construit. Les trois paramètres ci‑dessous sont les plus influents pour **compress pdf images** tout en préservant l’interrogabilité.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi est un bon compromis ; des valeurs plus basses accélèrent le traitement mais peuvent manquer les petites polices.  
- **CompressImages** – active la compression PNG sans perte en interne ; le PDF interrogeable reste net tout en étant plus léger.  
- **EmbedOriginalImages** – sans ce drapeau, le moteur supprimerait le raster original, ne laissant que du texte invisible. Conserver l’image garantit que le PDF ressemble exactement à la numérisation, ce que de nombreuses équipes de conformité exigent.

---

## Étape 3 – Charger votre PDF numérisé dans un `OcrInput`  

Aspose lit le fichier source via un wrapper `OcrInput`. Vous pouvez ajouter plusieurs fichiers, mais pour cette démo nous nous concentrons sur un seul **PDF image**.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Pourquoi ne pas simplement passer un `File` ?** Utiliser `OcrInput` vous offre la flexibilité de concaténer plusieurs PDF ou même de mélanger des fichiers image (PNG, JPEG) avant l’OCR. C’est le modèle recommandé lorsque vous **convertissez un pdf numérisé** qui pourrait être réparti sur plusieurs sources.

---

## Étape 4 – Effectuer l’OCR et obtenir un PDF interrogeable sous forme de tableau d’octets  

Maintenant, la magie opère. Le moteur analyse chaque page, exécute son moteur OCR, et construit un nouveau PDF contenant à la fois l’image originale et une couche de texte cachée.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Si vous avez besoin du texte brut pour d’autres usages (par ex., l’indexation), vous pouvez également appeler `ocrEngine.recognize(ocrInput)` qui renvoie une `String`. Mais pour l’objectif **create searchable pdf**, c’est le tableau d’octets que vous écrirez sur le disque.

---

## Étape 5 – Enregistrer le PDF interrogeable sur le disque  

Enfin, écrivez le tableau d’octets dans un fichier. Le NIO de Java rend cela possible en une seule ligne.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Lorsque vous ouvrez `searchable_output.pdf` dans Adobe Acrobat ou tout visualiseur moderne, vous constaterez que vous pouvez désormais sélectionner, copier et rechercher le texte—exactement ce que promet la transformation **image pdf to text**.

---

## Convertir un PDF numérisé en texte avec OCR (Optionnel)

Parfois, vous n’avez besoin que du texte brut extrait, pas d’un nouveau PDF. Vous pouvez réutiliser le même moteur :

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Cet extrait montre à quel point il est facile de **recognize pdf ocr** pour un traitement en aval comme alimenter un index de recherche ou effectuer une analyse en langage naturel.

---

## Compresser les images du PDF pour des fichiers plus petits  

Si vos numérisations sources sont volumineuses (par ex., des scans couleur à 600 dpi), le PDF interrogeable résultant peut rester lourd. En plus du drapeau `setCompressImages(true)`, vous pouvez réduire manuellement la résolution avant l’OCR :

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

Réduire le DPI coupera la taille du fichier d’environ moitié, mais testez la lisibilité — certaines polices deviennent illisibles en dessous de 150 dpi. Le compromis entre **compress pdf images** et la précision de l’OCR est à déterminer en fonction de vos contraintes de stockage.

---

## Paramètres OCR du PDF expliqués  

| Paramètre                | Effet sur la sortie                         | Cas d’utilisation typique                                   |
|--------------------------|---------------------------------------------|--------------------------------------------------------------|
| `setOutputDpi(int)`      | Contrôle la résolution raster de la sortie OCR | Archives haute qualité (300 dpi) vs. PDF web légers (150 dpi) |
| `setCompressImages`      | Active la compression PNG                   | Lorsque vous devez envoyer des PDF par e‑mail ou les stocker dans le cloud |
| `setEmbedOriginalImages` | Conserve la numérisation originale visible   | Documents juridiques ou de conformité qui doivent garder l’aspect original |
| `setLanguage` (optional) | Force le modèle de langue (ex., "eng")      | Corpus multilingues où la détection automatique par défaut peut échouer |

Comprendre ces réglages vous aide à **recognize pdf ocr** de manière plus intelligente et à éviter le piège du « texte flou ».

---

## PDF image en texte – Pièges courants et comment les éviter  

1. **Scans basse résolution** – La précision de l’OCR chute brutalement sous 150 dpi. Suréchantillonnez la source avant de la fournir à Aspose, ou demandez un DPI plus élevé au scanner.  
2. **Pages tournées** – Si les pages sont numérisées de côté, activez l’auto‑rotation : `pdfOcrOptions.setAutoRotate(true);`.  
3. **PDF chiffrés** – Le moteur ne peut pas lire les fichiers protégés par mot de passe ; déchiffrez d’abord en utilisant `PdfDocument` d’Aspose.PDF.  
4. **Raster et texte mélangés** – Certains PDF contiennent déjà une couche de texte cachée. Exécuter à nouveau l’OCR peut dupliquer le texte. Utilisez `PdfOcrOptions.setSkipExistingText(true);` pour préserver la couche originale.  

Résoudre ces problèmes garantit que votre pipeline **create searchable pdf** est robuste pour les collections de documents du monde réel.

---

## Exemple complet fonctionnel (Toutes les étapes dans un seul fichier)

Voici la classe Java complète que vous pouvez copier‑coller dans votre IDE. Remplacez `YOUR_DIRECTORY` par le chemin réel du dossier.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise le moteur OCR
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure les options OCR spécifiques aux PDF
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Charge le PDF numérisé (image‑only) dans un objet OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}