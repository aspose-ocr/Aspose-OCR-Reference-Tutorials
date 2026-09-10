---
date: 2026-07-04
description: Apprenez comment extraire du texte depuis une URL avec Aspose.OCR pour
  Java – OCR haute précision, prise en charge multilingue et intégration facile.
keywords:
- extract text from url
- url image to text
- java extract image text
linktitle: Effectuer une OCR sur une image depuis une URL avec Aspose.OCR pour Java
schemas:
- author: Aspose
  dateModified: '2026-07-04'
  description: Learn how to extract text from URL with Aspose.OCR for Java – high‑accuracy
    OCR, multi‑language support, and easy integration.
  headline: Extract text from URL using Aspose.OCR for Java
  type: TechArticle
- questions:
  - answer: Aspose.OCR delivers **high‑accuracy OCR**, typically exceeding 98 % character
      accuracy on clean printed documents when you define precise recognition areas
      and disable auto‑skew.
    question: How accurate is Aspose.OCR in recognizing text from images?
  - answer: Yes, the engine supports over 30 languages; simply load the appropriate
      language pack via `RecognitionSettings.setLanguage`.
    question: Can Aspose.OCR handle OCR multiple languages?
  - answer: Absolutely. Production use requires a commercial license; trial licenses
      impose page limits and embed a watermark. For purchasing a license, see the
      [Aspose purchase page](https://purchase.aspose.com/buy).
    question: Are there any licensing considerations for commercial projects?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community
      assistance, or obtain premium support with a temporary license from [Temporary
      License](https://purchase.aspose.com/temporary-license/).
    question: Where can I get help if I run into problems?
  - answer: Yes, you can download a fully‑featured trial from [releases.aspose.com](https://releases.aspose.com/)
      and evaluate all features without cost.
    question: Is a free trial available for Aspose.OCR for Java?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Extraire du texte depuis une URL avec Aspose.OCR pour Java
url: /fr/java/advanced-ocr-techniques/perform-ocr-image-from-url/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte depuis une URL avec Aspose.OCR pour Java

Dans ce **tutoriel Aspose OCR Java**, vous découvrirez comment **extraire du texte depuis une URL** hébergées dans des images avec seulement quelques lignes de code. À la fin du guide, vous disposerez d’un extrait Java prêt à l’exécution qui télécharge une image directement depuis une adresse web, exécute le moteur haute précision d’Aspose.OCR, et renvoie à la fois le texte brut et des métadonnées JSON détaillées. Ce flux de travail est idéal pour les robots d’exploration web, les pipelines de documents automatisés, ou tout système qui doit transformer des images en ligne en texte consultable.

## Réponses rapides
- **Aspose.OCR peut‑il lire des images directement depuis une URL ?** Oui – appelez `RecognizePageFromUri` et la bibliothèque gère le téléchargement pour vous.  
- **Le moteur prend‑il en charge plusieurs langues ?** Absolument ; chargez le pack de langue requis via `RecognitionSettings.setLanguage`.  
- **Quelle est la précision de l’OCR ?** Avec la correction d’inclinaison désactivée et des zones de reconnaissance appropriées, Aspose.OCR atteint >98 % de précision de caractères sur des documents imprimés propres.  
- **Quelles sont les exigences minimales ?** Java 8+, Aspose.OCR pour Java, et une licence valide pour une utilisation en production.  
- **Comment appliquer une licence ?** Utilisez `License license = new License(); license.setLicense("Aspose.OCR.lic");` avant tout appel OCR.

## Qu’est‑ce que « extraire du texte d’une image » ?
Extraire du texte d’une image signifie convertir des caractères visuels en chaînes lisibles par machine. Aspose.OCR lit les motifs de pixels, les compare aux modèles linguistiques, et renvoie les caractères reconnus sous forme de texte brut, d’une charge utile JSON, et de résultats optionnels par zone. Cela vous permet de stocker, d’indexer ou de traiter davantage le contenu sans transcription manuelle.

## Pourquoi utiliser Aspose.OCR pour un OCR haute précision ?
Aspose.OCR prend en charge **plus de 50 formats d’entrée et de sortie** — y compris PNG, JPEG, BMP, TIFF et PDF — tout en maintenant une faible consommation de mémoire grâce au streaming de gros fichiers. Les benchmarks montrent qu’il traite un PDF de 300 pages en moins de 12 secondes sur un CPU de 2,5 GHz, offrant **>98 % de précision** sur du texte anglais imprimé lorsque des zones de reconnaissance sont définies. La bibliothèque pure Java ne nécessite aucun DLL natif et inclut des packs de langue pour plus de 30 langues.

## Prérequis
- **Java Development Kit** – JDK 8 ou version plus récente installé et configuré.  
- **IDE ou outil de construction** – Maven, Gradle, ou tout IDE de votre choix.  
- **Aspose.OCR pour Java** – Téléchargez depuis le site officiel [site officiel Aspose.OCR website](https://reference.aspose.com/ocr/java/).  
- **Licence valide** – Nécessaire pour la production ; un essai gratuit suffit pour l’évaluation.  
- **Licence commerciale** – Pour acheter une licence, visitez la [page d’achat Aspose purchase page](https://purchase.aspose.com/buy).

## Étape 1 : Créer une instance API
La classe `AsposeOCR` est le point d’entrée principal qui fournit les fonctionnalités OCR.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Étape 2 : Définir l’URL de l’image
Vous transmettez l’URL de l’image directement à la méthode OCR, qui gère le téléchargement en interne.

```java
AsposeOCR api = new AsposeOCR();
```

## Étape 3 : Définir les options de reconnaissance
`RecognitionSettings` vous permet de configurer la langue, la correction d’inclinaison automatique et des rectangles de reconnaissance personnalisés.

```java
String uri = "https://www.example.com/your-image.png";
```

## Étape 4 : Effectuer l’OCR
`RecognizePageFromUri` effectue le téléchargement et l’OCR en un seul appel, renvoyant un objet résultat.

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Define recognition areas using rectangles
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## Étape 5 : Afficher les résultats
`RecognitionResult` contient le texte extrait, les chaînes par zone, et un résumé JSON.

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Quand devez‑vous extraire du texte à partir d’images web ?
Vous devez extraire du texte à partir d’images web chaque fois que vous avez besoin d’un contenu consultable et indexable provenant de sources visuelles — comme le scraping de catalogues de produits, l’archivage de graphiques d’actualités, ou la conversion de PDF numérisés stockés dans des compartiments cloud. L’automatisation de cette étape élimine la saisie manuelle de données, améliore l’accessibilité et permet la recherche en texte intégral sur vos actifs numériques.

## Comment extraire du texte à partir d’images web avec Aspose.OCR ?
Fournissez l’URL de l’image distante à `RecognizePageFromUri`, configurez les paramètres de langue ou de zone nécessaires, et appelez la méthode. La bibliothèque télécharge l’image, exécute le moteur OCR, et renvoie le texte reconnu ainsi que les métadonnées JSON — le tout en un seul appel sans code réseau supplémentaire.

## Problèmes courants et solutions
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Empty `recognitionText`** | URL incorrecte ou délai d’attente réseau. | Vérifiez que l’URL est accessible et ajoutez une gestion d’exception appropriée. |
| **Garbage characters** | Correction d’inclinaison automatique activée sur des images pivotées. | Conservez `settings.setAutoSkew(false)` ou fournissez les métadonnées de rotation correctes. |
| **Missing language support** | Le pack de langue par défaut ne comprend que l’anglais. | Chargez des packs de langue supplémentaires via `settings.setLanguage("fra")` (ou d’autres codes ISO). |
| **License not applied** | Le mode d’essai peut limiter le nombre de pages. | Appliquez une licence valide avec `License license = new License(); license.setLicense("Aspose.OCR.lic");` |

## Questions fréquemment posées
**Q : Quelle est la précision d’Aspose.OCR dans la reconnaissance de texte à partir d’images ?**  
R : Aspose.OCR fournit un **OCR haute précision**, dépassant généralement 98 % de précision de caractères sur des documents imprimés propres lorsque vous définissez des zones de reconnaissance précises et désactivez la correction d’inclinaison automatique.

**Q : Aspose.OCR peut‑il gérer l’OCR de plusieurs langues ?**  
R : Oui, le moteur prend en charge plus de 30 langues ; il suffit de charger le pack de langue approprié via `RecognitionSettings.setLanguage`.

**Q : Existe‑t‑il des considérations de licence pour les projets commerciaux ?**  
R : Absolument. L’utilisation en production nécessite une licence commerciale ; les licences d’essai imposent des limites de pages et ajoutent un filigrane. Pour acheter une licence, consultez la [page d’achat Aspose purchase page](https://purchase.aspose.com/buy).

**Q : Où puis‑je obtenir de l’aide en cas de problème ?**  
R : Visitez le [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) pour obtenir de l’aide de la communauté, ou obtenez un support premium avec une licence temporaire depuis [Licence temporaire Temporary License](https://purchase.aspose.com/temporary-license/).

**Q : Une version d’essai gratuite est‑elle disponible pour Aspose.OCR pour Java ?**  
R : Oui, vous pouvez télécharger une version d’essai complète depuis [releases.aspose.com](https://releases.aspose.com/) et évaluer toutes les fonctionnalités gratuitement.

**Dernière mise à jour :** 2026-07-04  
**Testé avec :** Aspose.OCR 24.11 pour Java  
**Auteur :** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés
- [Extraire du texte d'images – Bases de l'OCR avec Aspose.OCR pour Java](/ocr/java/ocr-basics/)
- [Extraire du texte d'une image Java avec le mode Détection de zones Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Comment OCR du texte d'image avec sélection de langue en utilisant Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```