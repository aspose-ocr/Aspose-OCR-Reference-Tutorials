---
category: general
date: 2026-02-17
description: Apprenez à utiliser l'OCR en Java pour reconnaître le texte à partir
  de fichiers image, extraire le texte des reçus PNG et convertir le reçu en JSON
  avec Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: fr
og_description: Guide étape par étape sur la façon d’utiliser l’OCR en Java pour reconnaître
  le texte d’une image, extraire le texte des reçus PNG et convertir le reçu en JSON.
og_title: Comment utiliser l'OCR en Java – Reconnaître le texte à partir d’une image
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Comment utiliser l’OCR en Java – Reconnaître rapidement le texte d’une image
url: /fr/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

formatting, headings, bullet points, blockquotes, code placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Java – Reconnaître rapidement du texte à partir d'une image

Vous êtes‑vous déjà demandé **comment utiliser l'OCR** pour extraire du texte d'une photo de reçu ? Peut‑être avez‑vous essayé quelques outils en ligne, pour finir avec des caractères illisibles ou un format que vous ne pouvez pas analyser. La bonne nouvelle, c’est qu’avec quelques lignes de code Java, vous pouvez **reconnaître du texte à partir d’une image**, **extraire du texte d’un PNG** de reçu, et même **convertir le reçu en JSON** pour un traitement en aval.  

Dans ce tutoriel, nous parcourrons le flux de travail complet — de la licence de la bibliothèque Aspose OCR à l’obtention d’une charge utile JSON propre que vous pouvez injecter dans une base de données ou un modèle d’apprentissage automatique. Pas de superflu, juste un exemple pratique et exécutable que vous pouvez copier‑coller dans votre IDE. À la fin, vous disposerez d’un programme autonome qui prend `receipt.png` et génère une chaîne JSON prête à l’emploi.

## Ce dont vous avez besoin

- **Java Development Kit (JDK) 8+** – toute version récente fonctionne.  
- **Aspose OCR for Java** library (l’artifact Maven est `com.aspose:aspose-ocr`).  
- Un **fichier de licence Aspose OCR valide** (`Aspose.OCR.lic`). L’essai gratuit fonctionne pour les tests, mais une licence appropriée supprime les limites d’évaluation.  
- Un fichier image (PNG, JPEG, etc.) contenant le texte que vous souhaitez lire — appelons‑le `receipt.png` et plaçons‑le dans un dossier connu.  
- Votre IDE préféré (IntelliJ IDEA, Eclipse, VS Code…) – vous êtes libre de choisir.

> **Astuce :** Conservez votre fichier de licence en dehors du dossier source et référencez‑le via un chemin absolu ou relatif afin d’éviter de le commettre dans le contrôle de version.

Maintenant que les prérequis sont clairs, plongeons dans le code réel.

## Comment utiliser l'OCR – Étapes principales

Voici un aperçu de haut niveau des actions que nous allons effectuer :

1. **Charger la bibliothèque Aspose OCR** et appliquer votre licence.  
2. **Créer une instance `OcrEngine`** – c’est le moteur qui effectue le travail lourd.  
3. **Préparer un objet `OcrInput`** pointant vers l’image que vous souhaitez traiter.  
4. **Appeler `recognize` avec `ResultFormat.JSON`** pour obtenir une représentation JSON du texte extrait.  
5. **Gérer la sortie JSON** – l’imprimer, l’écrire dans un fichier ou l’analyser davantage.

Chaque étape est expliquée en détail dans les sections suivantes.

## Étape 1 – Installer Aspose OCR et appliquer votre licence

Tout d’abord, ajoutez la dépendance Aspose OCR à votre `pom.xml` si vous utilisez Maven :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Ensuite, dans votre code Java, chargez la licence. Cette étape est essentielle ; sans elle, la bibliothèque fonctionne en mode d’évaluation et peut intégrer des filigranes dans la sortie.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Pourquoi c’est important :** L’objet `License` indique au moteur OCR que vous êtes autorisé à utiliser l’ensemble complet des fonctionnalités, qui comprend la reconnaissance haute précision et l’exportation JSON. Ignorer cette étape vous permettra toujours de **reconnaître du texte à partir d’une image**, mais les résultats peuvent être limités.

## Étape 2 – Créer l’instance du moteur OCR

La classe `OcrEngine` est le point d’entrée de toutes les opérations OCR. Pensez‑y comme le « cerveau » qui lit les pixels et décide quels caractères ils représentent.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Vous pouvez personnaliser le moteur (par ex., définir la langue, activer la correction d’inclinaison) plus tard si vos reçus contiennent des scripts non latins ou sont numérisés sous un angle. Pour la plupart des reçus américains, les paramètres par défaut fonctionnent très bien.

## Étape 3 – Charger l’image à traiter

Nous allons maintenant pointer le moteur OCR vers le fichier contenant le reçu. La classe `OcrInput` peut accepter plusieurs images, mais pour ce tutoriel nous resterons simples avec un seul PNG.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Si vous avez besoin de **extraire du texte de fichiers PNG** en masse, appelez simplement `input.add()` à plusieurs reprises ou transmettez une liste de chemins de fichiers.

## Étape 4 – Reconnaître le texte et convertir le reçu en JSON

Voici le cœur du tutoriel. Nous demandons au moteur de reconnaître le texte et de fournir le résultat au format JSON. Le drapeau `ResultFormat.JSON` effectue tout le travail lourd pour nous.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

La charge utile JSON comprend chaque ligne reconnue, son rectangle englobant, le score de confiance et le texte brut. Cette structure rend trivial le **convertir le reçu en JSON** puis le transmettre à n’importe quelle API en aval.

## Étape 5 – Assembler le tout et exécuter le programme

Ci‑dessous se trouve la classe Java complète, prête à être exécutée, qui assemble tous les éléments. Enregistrez‑la sous le nom `JsonExportDemo.java` (ou tout autre nom) et exécutez‑la depuis votre IDE ou la ligne de commande.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Sortie attendue

L’exécution du programme affiche une chaîne JSON similaire à la suivante (le contenu exact dépend de votre reçu) :

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Vous pouvez maintenant injecter ce JSON dans une base de données, un point d’accès REST ou un pipeline d’analyse de données. L’étape **convertir le reçu en JSON** est déjà effectuée pour vous.

## Questions fréquentes et cas particuliers

### Que faire si l’image est tournée ?

Aspose OCR détecte et corrige automatiquement les rotations légères. Pour des images fortement inclinées, appelez `engine.getImagePreprocessingOptions().setDeskew(true)` avant la reconnaissance.

### Comment gérer plusieurs langues ?

Utilisez `engine.getLanguage()` pour définir la langue souhaitée, par ex., `engine.setLanguage(Language.FRENCH)`. Cela est pratique lorsque vous devez **reconnaître du texte à partir d’une image** contenant des reçus multilingues.

### Puis‑je obtenir du texte brut au lieu de JSON ?

Absolument. Remplacez `ResultFormat.JSON` par `ResultFormat.TEXT` et appelez `result.getText()`.

### Existe‑t‑il un moyen de limiter l’OCR à une région spécifique ?

Oui — utilisez `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` pour vous concentrer sur la zone du reçu, ce qui peut améliorer la vitesse et la précision.

## Astuces pro pour un OCR prêt pour la production

- **Mettre en cache l’objet licence** si vous traitez de nombreux fichiers dans une boucle ; le créer à chaque fois ajoute une surcharge.  
- **Traitement par lots** : chargez tous les chemins de reçus dans un seul `OcrInput` et appelez `recognize` une fois. Le JSON contiendra un tableau de pages, chacune avec ses propres lignes.  
- **Valider le JSON** : après avoir obtenu la chaîne, analysez‑la avec une bibliothèque comme Jackson pour vous assurer qu’elle est bien formée avant de la stocker.  
- **Surveiller la confiance** : le JSON inclut un champ `confidence` par ligne. Filtrez les lignes en dessous d’un seuil (par ex., 0.85) pour éviter les données inutiles.  
- **Sécuriser votre licence** : stockez `Aspose.OCR.lic` dans un coffre sécurisé ou une variable d’environnement, surtout lors de déploiements cloud.

## Conclusion

Nous avons couvert **comment utiliser l’OCR** en Java pour **reconnaître du texte à partir d’une image**, **extraire du texte de PNG** de reçus, et **convertir le reçu en JSON** — le tout avec un exemple concis et complet. Les étapes sont simples, le code est entièrement exécutable, et la sortie JSON vous fournit une représentation structurée prête pour tout système en aval.

Ensuite, vous pourriez explorer des scénarios plus avancés : injecter le JSON dans Apache Kafka pour un traitement en temps réel, appliquer des expressions régulières pour extraire les totaux des lignes, ou intégrer un service OCR cloud pour la scalabilité. Quel que soit votre choix, les bases que vous venez d’apprendre resteront les mêmes.

Des questions, ou un problème lors de l’essai ? Laissez un commentaire ci‑dessous, et résolvons‑le ensemble. Bon codage, et profitez de transformer ces images de reçus désordonnés en données propres et recherchables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}