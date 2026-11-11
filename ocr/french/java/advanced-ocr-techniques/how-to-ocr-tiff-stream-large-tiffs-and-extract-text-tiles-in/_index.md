---
category: general
date: 2026-04-29
description: Apprenez à effectuer la reconnaissance OCR de fichiers TIFF en utilisant
  le mode streaming d’Aspose OCR. Ce guide vous montre comment extraire efficacement
  les tuiles de texte à partir d’images TIFF en mosaïque.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: fr
og_description: comment OCR un TIFF avec le streaming Aspose OCR. Code étape par étape
  pour extraire les tuiles de texte des grandes images TIFF.
og_title: Comment faire de l'OCR d'un TIFF – Guide complet du streaming
tags:
- OCR
- Java
- Aspose
- TIFF
title: Comment faire de l’OCR d’un TIFF – Diffuser de gros fichiers TIFF et extraire
  des tuiles de texte en Java
url: /fr/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment faire de l'ocr tiff – Diffuser de grands TIFF et extraire les tuiles de texte en Java

Vous vous êtes déjà demandé **how to ocr tiff** pour des fichiers trop volumineux pour être chargés en mémoire d’un seul coup ? Vous n’êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsque leurs images TIFF sont découpées en dizaines de tuiles, et l’appel habituel `ocrEngine.recognize()` échoue lamentablement.  

Bonne nouvelle : le mode streaming d’Aspose OCR vous permet d’alimenter chaque tuile comme un flux séparé, ainsi vous pouvez **extract text tiles** sans exploser votre tas. Dans ce tutoriel, nous parcourrons un exemple Java complet, prêt à l’emploi, expliquerons pourquoi chaque ligne est importante et soulignerons les pièges à éviter.

> **Ce que vous obtiendrez :** un programme exécutable qui assemble les TIFF découpés à la volée, affiche le texte combiné et vous montre comment adapter le code à d’autres langues ou formats d’image.

---

## Prérequis

- **Java 17** ou plus récent (le code utilise try‑with‑resources, donc JDK 8+ fonctionne, mais JDK 17 est la LTS actuelle).
- Bibliothèque **Aspose.OCR for Java** (v23.10 ou ultérieure). Ajoutez‑la via Maven :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Un dossier contenant les tuiles TIFF individuelles (par ex., `tile_0.tif`, `tile_1.tif`, …).  
- Facultatif : un IDE comme IntelliJ IDEA ou VS Code – mais un simple éditeur de texte suffit.

---

## Étape 1 – Préparer les chemins des tuiles (Pourquoi c’est important)

Avant que le moteur OCR ne puisse faire quoi que ce soit, il doit savoir où chaque morceau d’image se trouve. Codifier en dur les chemins est acceptable pour une démo, mais en production vous parcourrez probablement un répertoire ou lirez un fichier manifeste.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Astuce pro :** conservez les tuiles dans l’ordre lexical (0, 1, 2…) car le moteur concaténera le texte reconnu dans la même séquence que vous fournissez les flux.

---

## Étape 2 – Activer le mode streaming sur le moteur OCR (Mot‑clé principal)

Nous créons maintenant l’instance `OcrEngine` et activons le streaming. C’est le cœur du **how to ocr tiff** sans charger l’image entière en RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Pourquoi le streaming ?**  
Lorsque `setEnableStreaming(true)` est appelé, le moteur traite chaque `ImageStream` entrant comme la continuation du précédent. Il construit une toile virtuelle interne, assemble les tuiles virtuellement et exécute l’OCR une fois à la fin. Cela évite le “OutOfMemoryError” qui surviendrait si vous essayiez de charger un TIFF de plusieurs gigaoctets en une fois.

---

## Étape 3 – Ajouter chaque tuile comme flux d’entrée (Mot‑clé secondaire)

Voici la boucle qui alimente chaque tuile au moteur. Le bloc `try‑with‑resources` garantit que le handle du fichier est fermé rapidement, ce qui est crucial lorsqu’on manipule des dizaines de fichiers.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Remarquez que l’expression **extract text tiles** est naturellement intégrée : chaque itération *extrait* le texte d’une tuile et l’ajoute au jeu de résultats croissant.

---

## Étape 4 – Lancer la reconnaissance et afficher le texte combiné (Mot‑clé principal)

Une fois toutes les tuiles en file d’attente, un appel unique effectue l’OCR sur l’image virtuelle. Le résultat contient le texte complet, comme si vous aviez un seul TIFF massif.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Sortie attendue** (en supposant que les tuiles contiennent la phrase « Hello World » découpée) :

```
=== OCR Output ===
Hello World
```

Si vos tuiles contiennent plus de lignes, elles apparaîtront dans le même ordre que vous les avez fournies. Vous pouvez également écrire `ocrResult.getText()` dans un fichier pour un traitement en aval.

---

## Étape 5 – Exemple complet, exécutable (Toutes les étapes en un seul endroit)

Voici le programme complet que vous pouvez copier‑coller dans `StreamingExample.java`. Il inclut tous les imports, commentaires et la gestion des erreurs.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Enregistrez, compilez et exécutez :

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Vous devriez voir le texte OCR concaténé affiché dans la console.

---

## Conseils avancés & pièges courants (Pourquoi cela fonctionne)

| Problème | Pourquoi cela se produit | Comment corriger / optimiser |
|----------|--------------------------|------------------------------|
| **Erreurs de dépassement de mémoire** | Charger un TIFF de pleine taille dans un `BufferedImage` consomme toute la mémoire du tas. | Utilisez le mode streaming (`setEnableStreaming(true)`) – le moteur ne matérialise jamais l'image complète. |
| **Mauvais ordre des tuiles** | Les fichiers sont triés alphabétiquement au lieu de numériquement (par ex., `tile_10.tif` avant `tile_2.tif`). | Ajoutez des zéros devant les nombres (`tile_00.tif`, `tile_01.tif`) ou triez programmatique avec `Comparator`. |
| **Langue incorrecte** | L'OCR utilise l'anglais par défaut ; le texte non anglais devient illisible. | Appelez `ocrEngine.getLanguageSettings().setLanguage("fr")` (ou tout autre code ISO supporté). |
| **Échecs partiels** | Une tuile corrompue arrête tout le processus. | Capturez `IOException` par tuile, journalisez, et décidez de continuer ou d'abandonner. |
| **Goulot d'étranglement de performance** | Les entrées/sorties disque dominent lors de la lecture de nombreux petits fichiers. | Regroupez les tuiles dans un ZIP et diffusez depuis la mémoire, ou utilisez un SSD rapide. |

---

## Quand utiliser le streaming vs. l’OCR sur image unique

- **Streaming** est idéal pour :
  - Les TIFF multi‑pages ou les scans gigapixels.
  - Les situations où la mémoire est limitée (ex. : conteneurs Docker, appareils mobiles).
  - Les pipelines qui reçoivent déjà des fragments d’image (ex. : flux de caméra).

- **OCR sur image unique** convient parfaitement pour :
  - Les petits fichiers PNG/JPEG (< 5 Mo).
  - Les scans ponctuels où la simplicité prime sur les performances.

---

## Conclusion

Vous maîtrisez désormais **how to ocr tiff** grâce aux capacités de streaming d’Aspose OCR, et vous savez comment **extract text tiles** de façon efficace. La solution complète – initialisation du moteur, activation du streaming, ajout de chaque tuile, puis reconnaissance de la toile virtuelle – couvre le « quoi », le « pourquoi » et le « comment » nécessaires à un code prêt pour la production.

Prochaines étapes ? Remplacez `"en"` par une autre langue, ou expérimentez avec d’autres formats d’image (`.png`, `.jpg`). Vous pouvez également acheminer le résultat OCR directement vers un index de recherche ou un générateur de PDF. Le schéma reste le même : stream, stitch, recognize.

Des questions sur le traitement de centaines de tuiles, ou besoin d’aide pour la gestion des erreurs ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}