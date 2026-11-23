---
category: general
date: 2026-06-22
description: Créer un PDF consultable à l'aide de l'OCR en Java. Apprenez comment
  désactiver la compression et convertir rapidement un PDF d'image numérisée en PDF
  consultable.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: fr
og_description: Créer un PDF consultable à l'aide de l'OCR en Java. Ce guide montre
  comment désactiver la compression, convertir un PDF d'image numérisée et générer
  un PDF sans compression.
og_title: Créer un PDF consultable avec OCR – Tutoriel Java complet
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Créer un PDF consultable avec OCR – Guide complet
url: /fr/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable avec OCR – Guide complet

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'un lot d'images numérisées mais vous n'étiez pas sûr des paramètres à ajuster ? Vous n'êtes pas le seul—la plupart des développeurs rencontrent le même problème lorsque le résultat devient un énorme bloc illisible.  

Dans ce tutoriel, nous parcourrons un exemple propre, de bout en bout, qui vous montre exactement comment **créer un PDF consultable** en utilisant un moteur OCR Java, **convertir un PDF d'image numérisée**, et, surtout, **comment désactiver la compression** afin que le fichier résultant reste fidèle aux dimensions d'origine. À la fin, vous disposerez d'un extrait prêt à l'emploi et d'une compréhension solide des raisons pour lesquelles chaque configuration est importante.

## Ce que vous apprendrez

* Comment configurer le moteur OCR pour **ocr to searchable pdf**.  
* La raison de désactiver la compression PDF et comment obtenir un **pdf without compression**.  
* Un programme Java complet qui prend une image numérisée, exécute l'OCR et enregistre un **searchable PDF**.  
* Conseils pour gérer les cas limites comme les numérisations multi‑pages ou les sources à basse résolution.  

**Pré-requis** – Java 8+ installé, un SDK OCR compatible (le code utilise l'API ABBYY FineReader Engine, mais les concepts s'appliquent à toute bibliothèque offrant `setOutputFormat` et `setPdfCompression`). Un IDE tel qu'IntelliJ IDEA ou Eclipse facilitera la tâche, mais un simple éditeur de texte suffit également.

![Créer un flux de travail PDF consultable](image-placeholder.png "Diagramme montrant le processus de création d'un PDF consultable à partir d'images numérisées jusqu'au PDF final")

## Étape 1 : Configurer le moteur OCR pour **Create Searchable PDF**

La première chose à indiquer au moteur OCR est le type de sortie attendu. Par défaut, de nombreux SDK génèrent du texte brut ou un PDF raster, qui n’est pas consultable. Changer le format fait le gros du travail pour vous.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Pourquoi cela importe* : le drapeau `PDF_SEARCHABLE` indique au moteur d’intégrer une couche de texte invisible sous l’image numérisée. Les outils de recherche peuvent alors indexer le document, le faisant se comporter comme n’importe quel PDF natif que vous ouvririez dans Adobe Reader.

## Étape 2 : Désactiver la compression – **How to Disable Compression** correctement

Si vous sautez cette étape, le moteur comprimera chaque page pour économiser de l’espace, mais la compression peut flouter les détails fins—ce qui pose problème lorsque vous devez extraire des images haute résolution.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Astuce pro** : désactiver la compression est essentiel lorsque vous prévoyez d’archiver des documents juridiques ou des scans médicaux où chaque pixel compte. Le fichier résultant sera plus volumineux, mais vous conservez les dimensions et la clarté d’origine.

## Étape 3 : Effectuer l'OCR et obtenir le document résultant

Maintenant que le moteur sait quoi produire et comment traiter les images, vous pouvez lancer la reconnaissance. L’appel renvoie un objet `PdfDocument` prêt à être enregistré ou manipulé davantage.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Que se passe‑t‑il en coulisses ?* Le moteur traite chaque page d’entrée, exécute la reconnaissance de caractères, puis ajoute la couche de texte cachée à l’image. Si vous avez plusieurs pages, elles sont concaténées automatiquement.

## Étape 4 : Enregistrer le **Searchable PDF** sur le disque

Enfin, écrivez le PDF en mémoire dans un fichier. Choisissez un emplacement où vous avez les droits d’écriture et donnez au fichier un nom significatif.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Lorsque vous ouvrez `searchable.pdf` dans un lecteur, vous constaterez que vous pouvez sélectionner et rechercher le texte—même si le contenu visible reste l’image numérisée d’origine.

### Exemple complet fonctionnel

Ci‑dessous se trouve une classe Java autonome qui regroupe les quatre étapes. N’hésitez pas à copier‑coller, ajuster le chemin d’entrée et l’exécuter tel quel.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Résultat attendu** – Après l’exécution du programme, vous verrez le message console ci‑dessus, et le fichier `searchable.pdf` apparaîtra dans `YOUR_DIRECTORY`. L’ouvrir avec n’importe quel lecteur PDF vous permettra de :

* Surligner le texte.  
* Utiliser la recherche intégrée (Ctrl + F) pour trouver des mots.  
* Exporter la couche de texte cachée si nécessaire.  

---

## Pourquoi désactiver la compression ? Comprendre **PDF Without Compression**

Vous vous demandez peut‑être « La compression n’est‑elle pas toujours une bonne idée ? » La réponse est nuancée :

| Situation | Conserver la compression (`NORMAL`) | Désactiver la compression (`NONE`) |
|-----------|-------------------------------------|------------------------------------|
| Archivage de contrats légaux | ❌ Peut altérer la fidélité des pixels | ✅ Garantit l'aspect original |
| Grand lot de numérisations basse résolution | ✅ Économise de l'espace | ❌ Augmente la taille sans bénéfice |
| Besoin d'une précision OCR sur de très petites polices | ❌ Floute les détails fins | ✅ Préserve chaque trait |

En bref, **how to disable compression** est un compromis entre stockage et fidélité. Pour la plupart des flux de travail PDF consultables où l’on veut rechercher le texte plutôt que réimprimer les images, désactiver la compression est le choix le plus sûr.

## Convertir directement un **Scanned Image PDF**

Parfois, vous avez déjà un PDF contenant des images numérisées (un « PDF image‑only »). Pour **convert scanned image pdf** en version consultable, vous pouvez fournir le PDF complet au moteur au lieu d’images individuelles :

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Les mêmes drapeaux de configuration (`PDF_SEARCHABLE` et `PdfCompression.NONE`) s’appliquent, vous obtenez donc un **pdf without compression** même en partant d’un conteneur PDF.

## Pièges courants & comment les éviter

* **Oubli de définir le format de sortie** – Le moteur utilise par défaut le PDF raster, qui n’est pas consultable. Appelez toujours `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` avant `recognizeToPdf()`.  
* **Manque de mémoire sur de gros lots** – Chargez et traitez les pages par lots, ou utilisez l'API de streaming si votre SDK en propose une.  
* **Chemins de fichiers incorrects** – Utilisez des chemins absolus ou assurez‑vous que le répertoire de travail est correctement défini ; sinon `pdf.save()` lève une `IOException`.  
* **Licence non activée** – La plupart des SDK OCR commerciaux nécessitent une licence valide ; le moteur lèvera une exception d'exécution si elle manque.  

---

## Conclusion

Vous disposez maintenant d’une solution complète, prête à l’exécution, qui montre **how to create searchable PDF** à partir d’images numérisées, comment **convert scanned image PDF**, et exactement **how to disable compression** pour produire un **pdf without compression**. Les étapes clés sont :

1. Définir le format de sortie sur `PDF_SEARCHABLE`.  
2. Désactiver la compression PDF avec `PdfCompression.NONE`.  
3. Exécuter l’OCR et capturer le `PdfDocument`.  
4. Enregistrer le fichier sur le disque.

À partir d’ici, vous pouvez expérimenter avec les polices, ajouter des filigranes, ou traiter par lots des dossiers entiers. Si vous êtes curieux d’ajouter des packs de langues OCR, de gérer des TIFF multi‑pages, ou d’intégrer ce flux de travail dans un service web, consultez nos prochains tutoriels sur « OCR language selection in Java » et « Streaming OCR for large document sets ».

Des questions ou un problème rencontré ? Laissez un commentaire ci‑dessous—bon codage, et profitez de vos nouveaux PDFs consultables !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Reconnaître le texte PDF – Opérations OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-operations/)
- [Reconnaissance OCR de documents PDF dans Aspose.OCR pour Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convertir des images en PDF C# – Enregistrer le résultat OCR multipage](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}