---
category: general
date: 2026-02-17
description: Comment utiliser l'OCR en Java pour extraire du texte d’un PDF, convertir
  un PDF en images et effectuer l’OCR sur des fichiers PDF numérisés à l’aide d’Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: fr
og_description: Comment utiliser l'OCR en Java pour extraire du texte à partir de
  fichiers PDF. Apprenez à convertir les PDF en images et à reconnaître les PDF numérisés
  avec Aspose.OCR.
og_title: Comment utiliser l'OCR en Java – Guide complet
tags:
- OCR
- Java
- Aspose
title: Comment utiliser l'OCR en Java – Extraire du texte d'un PDF avec Aspose.OCR
url: /fr/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Java – Extraire du texte d'un PDF avec Aspose.OCR

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour transformer un PDF numérisé en texte recherchable ? Vous n'êtes pas le seul. La plupart des développeurs se heurtent à un mur lorsqu'un PDF arrive sous forme d'une série d'images, et les extracteurs de texte habituels ne renvoient rien. La bonne nouvelle ? En quelques lignes de Java et Aspose.OCR, vous pouvez **extraire du texte d'un PDF**, **convertir un PDF en images**, et **reconnaître un PDF numérisé** dans un seul flux de travail sans effort.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir—de la licence de la bibliothèque à l'affichage du résultat final. À la fin, vous disposerez d'un programme prêt à l'emploi qui extrait le texte brut de n'importe quel rapport, facture ou ebook numérisé. Aucun service externe, aucune magie—juste du code Java pur que vous contrôlez.

## Ce dont vous avez besoin

- **Java Development Kit (JDK) 8+** – toute version récente fonctionne.  
- **Aspose.OCR for Java** JAR (téléchargez depuis le site Aspose).  
- Un **fichier de licence Aspose.OCR valide** (`Aspose.OCR.lic`). L'essai gratuit fonctionne, mais une licence débloque la précision totale.  
- Un **PDF numérisé d'exemple** (par ex., `scanned-report.pdf`).  
- Un IDE ou un simple éditeur de texte plus un terminal.  

C’est tout. Pas de Maven, pas de Gradle, pas de dépendances supplémentaires—juste le JAR Aspose.OCR dans votre classpath.

![exemple d'utilisation de l'OCR](image-placeholder.png "exemple d'utilisation de l'OCR")

## Étape 1 – Charger votre licence Aspose.OCR (Pourquoi c'est important)

Avant que le moteur puisse fonctionner à pleine vitesse, vous devez lui indiquer où se trouve votre licence. Ignorer cette étape force la bibliothèque en mode d'évaluation, ce qui ajoute des filigranes à la sortie et peut limiter la précision.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Pourquoi cela fonctionne :** La classe `License` lit le fichier `.lic` et l'enregistre globalement. Une fois définie, chaque `OcrEngine` que vous créez utilisera automatiquement les fonctionnalités sous licence.

## Étape 2 – Créer le moteur OCR (Le moteur derrière la magie)

Une instance `OcrEngine` est le cheval de bataille qui analyse les images et génère du texte. Pensez-y comme le cerveau qui interprète les motifs de pixels.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Astuce :** Vous pouvez ajuster la langue, les seuils de confiance, ou même activer l'accélération GPU via les propriétés du moteur. Pour la plupart des PDF en anglais, les paramètres par défaut conviennent.

## Étape 3 – Préparer l'entrée : ajouter votre PDF (Convertir le PDF en images en interne)

Aspose.OCR considère chaque page d'un PDF comme une image. Lorsque vous appelez `addPdf`, la bibliothèque rasterise silencieusement chaque page, ce qui est exactement ce dont vous avez besoin pour **convertir le PDF en images** avant la reconnaissance.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Ce qui se passe :**  
- Le PDF est ouvert.  
- Chaque page est rendue à 300 dpi (par défaut) pour préserver les détails des caractères.  
- Les objets bitmap rendus sont stockés dans la collection `OcrInput`.

Si vous avez besoin des images brutes (pour le débogage ou un prétraitement personnalisé), appelez `ocrInput.getPages()` après cette étape.

## Étape 4 – Exécuter le processus OCR (Effectuer l'OCR sur le PDF)

Le travail intensif commence maintenant. La méthode `recognize` parcourt chaque image, exécute l'algorithme de reconnaissance et agrège les résultats dans un `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Pourquoi cela vous intéresse :** Le `OcrResult` contient non seulement le texte brut mais aussi les scores de confiance, les boîtes englobantes et la référence à l'image originale. Pour la plupart des cas d'utilisation, vous n'aurez besoin que de `getText()`.

## Étape 5 – Récupérer et afficher le texte extrait

Enfin, extrayez la chaîne de texte brut du résultat et affichez‑la. Vous pouvez également l'écrire dans un fichier, l'alimenter dans un index de recherche, ou le transmettre à un pipeline NLP en aval.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Sortie attendue

Si `scanned-report.pdf` contient un paragraphe simple, vous verrez quelque chose comme :

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Le formatage exact reflète la mise en page originale, en préservant les sauts de ligne lorsque c'est possible.

## Gestion des cas limites courants

### 1. PDFs multilingues

Si votre document contient du texte en français ou en espagnol, définissez la langue avant d'appeler `recognize` :

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Vous pouvez fournir un tableau de langues pour laisser le moteur détecter automatiquement.

### 2. Scans à basse résolution

Lors de la gestion de scans à 150 dpi, augmentez le DPI de rendu interne :

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Un DPI plus élevé améliore la clarté des caractères mais consomme plus de mémoire.

### 3. Gros PDFs (Gestion de la mémoire)

Pour les PDFs de plusieurs dizaines de pages, traitez‑les par lots :

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Cette approche empêche le tas JVM de gonfler.

## Exemple complet, prêt à l'exécution

Voici le programme complet—y compris les imports et la gestion de la licence—pour que vous puissiez copier‑coller et exécuter immédiatement.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Exécutez‑le avec :

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Vous devriez voir le texte extrait affiché dans la console.

## Récapitulatif – Ce que nous avons couvert

- **Comment utiliser l'OCR** en Java avec Aspose.OCR.  
- Le flux de travail pour **extraire du texte d'un PDF**.  
- En interne, la bibliothèque **convertit le PDF en images** avant de reconnaître les caractères.  
- Astuces pour **effectuer l'OCR sur un PDF** avec plusieurs langues, des scans à basse résolution et de gros documents.  
- Un exemple de code complet et exécutable que vous pouvez intégrer à n'importe quel projet Java.

## Prochaines étapes & sujets associés

Maintenant que vous pouvez **reconnaître les PDFs numérisés**, envisagez ces idées complémentaires :

- **Génération de PDF recherchable** – superposer le texte OCR sur le PDF original pour créer un document consultable.  
- **Service de traitement par lots** – encapsuler le code dans un microservice Spring Boot qui accepte les PDFs via REST.  
- **Intégration avec Elasticsearch** – indexer le texte extrait pour une recherche plein texte rapide dans votre dépôt de documents.  
- **Pré‑traitement d'image** – utiliser OpenCV pour redresser ou débruiter les pages avant l'OCR afin d'obtenir une précision encore meilleure.  

Chacun de ces sujets s'appuie sur les concepts de base que nous avons explorés, alors n'hésitez pas à expérimenter et laissez le moteur OCR faire le travail lourd.

---

*Bon codage ! Si vous rencontrez des problèmes—comme des erreurs de licence ou des résultats null inattendus—laissez un commentaire ci‑dessous. Je suis toujours partant pour une session de débogage.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}