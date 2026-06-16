---
category: general
date: 2026-04-29
description: extraire du texte d’une image en Java avec Aspose OCR – apprenez comment
  charger une image pour l’OCR et reconnaître le texte d’un reçu au format JSON.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: fr
og_description: extraire du texte d’une image en Java avec Aspose OCR. Ce tutoriel
  montre comment charger une image pour l’OCR et reconnaître le texte d’un reçu, en
  produisant du JSON.
og_title: Extraire du texte d’une image Java – Guide complet
tags:
- Java
- OCR
- Aspose
title: extraire du texte d'une image en Java – charger l'image pour l'OCR
url: /fr/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraction de texte à partir d'une image java – Guide complet

Vous avez déjà eu besoin d'**extraction de texte à partir d'une image java** mais vous ne saviez pas quelle bibliothèque choisir ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils essaient de charger une image pour l'OCR et obtiennent ensuite le texte brut dans un format difficile à exploiter.  

Dans ce tutoriel, nous parcourrons une solution propre, de bout en bout, qui non seulement **charge l'image pour l'OCR** mais aussi **reconnaît le texte d'un reçu** et génère une chaîne JSON bien formatée. À la fin, vous disposerez d'une classe Java prête à l'emploi que vous pourrez intégrer à n'importe quel projet — sans réglages supplémentaires.

## Ce que vous apprendrez

- Comment configurer Aspose OCR pour Java (la bibliothèque qui rend le travail lourd indolore).  
- Les étapes exactes pour **charger l'image pour l'OCR** depuis le disque.  
- Comment configurer le moteur pour renvoyer les résultats en JSON, ce qui est parfait pour le traitement en aval.  
- Comment **reconnaître le texte d'images de reçu** et vérifier la sortie.  

Aucune expérience préalable avec Aspose n'est requise ; il suffit d'un JDK fonctionnel et d'un IDE avec lequel vous êtes à l'aise.

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| **Java 17+** (ou tout JDK récent) | Aspose OCR est fourni avec des binaires compilés pour les environnements Java modernes. |
| **Maven ou Gradle** (pour récupérer la dépendance Aspose OCR) | Simplifie la gestion des dépendances. |
| **Une image de reçu d'exemple** (par ex., `receipt.png`) | Nous utiliserons ce fichier pour démontrer **reconnaître le texte d'un reçu**. |
| **Connexion Internet** (une fois) | Nécessaire pour télécharger le JAR Aspose la première fois. |

Si vous avez déjà tout cela, super — plongeons‑y.

## Étape 1 : Ajouter Aspose OCR à votre projet

La première chose dont vous avez besoin est la bibliothèque Aspose OCR. Si vous utilisez Maven, ajoutez le fragment suivant à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Pour Gradle, cela ressemble à ceci :

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Astuce :** Verrouillez le numéro de version. Une mise à jour ultérieure peut introduire de subtiles modifications d'API qui cassent votre code.

Une fois la dépendance résolue, vous êtes prêt à écrire du code Java qui **extrait du texte à partir d'une image java**.

## Étape 2 : Charger l'image pour l'OCR

Nous allons maintenant montrer la ligne exacte qui **charge l'image pour l'OCR**. Aspose fournit un utilitaire pratique `ImageStream.fromFile`.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif vers votre fichier de reçu. Si le chemin est incorrect, le moteur lèvera une `FileNotFoundException`, alors vérifiez bien l'orthographe.

> **Pourquoi c'est important :** Charger correctement l'image est la base. Si l'image n'est pas lue, le moteur OCR n'a rien à reconnaître, et vous obtiendrez un résultat JSON vide.

## Étape 3 : Indiquer au moteur de renvoyer du JSON

Aspose OCR peut produire du XML, du texte brut ou du JSON. Pour les API modernes, le JSON est le plus flexible, nous allons donc définir le format explicitement.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

Vous pourriez passer à `OcrResultFormat.XML` avec une simple modification si votre système en aval préfère le XML. L'API est conçue pour être interchangeable.

## Étape 4 : Exécuter le processus de reconnaissance

Avec l'image chargée et le format défini, l'étape suivante consiste à réellement **reconnaître le texte d'un reçu**. C'est ici que le travail lourd s'effectue.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

L'appel `recognize()` bloque jusqu'à ce que le moteur termine l'analyse de l'image. Pour les grandes images, vous pourriez vouloir exécuter cela dans un thread en arrière-plan, mais pour un reçu typique cela se termine en une fraction de seconde.

## Étape 5 : Récupérer le résultat JSON

Enfin, nous extrayons la chaîne JSON brute et l'affichons. Cette chaîne contient chaque morceau de texte reconnu, son cadre de délimitation, les scores de confiance, et plus encore.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### Résultat attendu

Exécuter le programme complet sur un reçu clair produit quelque chose comme :

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

Remarquez comment chaque ligne du reçu apparaît comme un bloc séparé avec un score de confiance. Vous pouvez maintenant injecter ce JSON dans n'importe quel système en aval — le stocker dans une base de données, l'envoyer via HTTP, ou le transmettre à un modèle d'apprentissage automatique.

## Exemple complet fonctionnel

Voici la classe Java complète et autonome qui assemble tout. Copiez‑collez‑la, ajustez le chemin de l'image, et exécutez `mvn compile exec:java` (ou la commande équivalente sous Gradle).

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **À surveiller :**  
> • **Erreurs de chemin de fichier** – vérifiez les barres obliques sous Windows vs. macOS/Linux.  
> • **Out‑of‑memory** – les images volumineuses peuvent nécessiter `ocrEngine.setMemoryOptimization(true)`.  
> • **Paramètres de langue** – si votre reçu contient des caractères non latins, appelez `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (ou toute langue prise en charge) avant `recognize()`.

## Test de la solution

1. **Exécuter le programme** – vous devriez voir un blob JSON affiché dans la console.  
2. **Valider le JSON** – copiez la sortie dans <https://jsonlint.com/> pour vous assurer qu'il est bien formé.  
3. **Le parser** – dans un projet réel, vous utiliseriez une bibliothèque comme Jackson ou Gson pour mapper le JSON vers des POJOs afin de le manipuler plus facilement.

Si vous rencontrez un tableau `pages` vide, les causes les plus fréquentes sont : le fichier image n'est pas trouvé, ou l'image est trop floue pour les paramètres par défaut du moteur. Dans ce dernier cas, essayez d'augmenter le DPI ou d'appliquer une étape de pré‑traitement (par ex., binarisation) avant de le transmettre à Aspose.

## Variations et cas limites

| Scénario | Ce qu'il faut changer |
|----------|-----------------------|
| **Pages multiples** (par ex., PDF multi‑pages converti en images) | Boucler sur chaque image, appeler `ocrEngine.setImage(...)` à l'intérieur de la boucle, et agréger les résultats JSON. |
| **Format de sortie différent** | Remplacer `OcrResultFormat.JSON` par `OcrResultFormat.XML` ou `OcrResultFormat.PLAIN_TEXT`. |
| **Optimisation des performances** | Utiliser `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` pour la vitesse, ou `OcrRecognitionMode.ACCURATE` pour la qualité. |
| **Documents non‑reçus** | Ajuster `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` si vous avez besoin d'extraction de tables. |

Ces ajustements vous permettent d'adapter le flux principal **extraction de texte à partir d'une image java** à un large éventail de problèmes réels.

## Conclusion

Nous venons de couvrir une méthode concise et prête pour la production afin **d'extraire du texte à partir d'une image java** en utilisant Aspose OCR. En suivant les cinq étapes — créer le moteur, **charger l'image pour l'OCR**, définir la sortie JSON, **reconnaître le texte d'un reçu**, et enfin lire le JSON — vous pouvez intégrer l'OCR dans n'importe quel backend Java avec un minimum d'effort.  

À partir d'ici, vous pourriez :

- Stocker le JSON dans une base NoSQL pour des analyses ultérieures.  
- Alimenter le résultat dans un chatbot qui répond aux questions sur les reçus.  
- Combiner cela avec Apache Tika pour gérer les PDF, DOCX et autres formats.

Essayez, ajustez les paramètres selon vos documents spécifiques, et laissez la machine faire le travail lourd pendant que vous vous concentrez sur la création de valeur.

---

![extraction de texte à partir d'une image java](placeholder-image.png "extraction de texte à partir d'une image java")

*Figure : Représentation visuelle du pipeline OCR – du fichier image au résultat JSON.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}