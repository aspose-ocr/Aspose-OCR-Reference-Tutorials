---
category: general
date: 2026-02-19
description: Créer un PDF consultable à partir d'une image JPG avec Aspose OCR en
  Java. Convertir le JPG en PDF et reconnaître rapidement le texte de l'image.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: fr
og_description: Créez un PDF consultable à partir d’une image JPG avec Aspose OCR.
  Apprenez comment convertir un JPG en PDF et reconnaître le texte d’une image en
  Java.
og_title: Créer un PDF consultable à partir de JPG – Tutoriel OCR Java
tags:
- aspose-ocr
- java
- pdf
- ocr
title: 'Créer un PDF interrogeable à partir de JPG – Guide Java : de l''image au PDF
  interrogeable'
url: /fr/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d'un JPG – Guide Java Image vers PDF consultable

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d’une image numérisée sans savoir par où commencer ? Vous n'êtes pas seul — de nombreux développeurs rencontrent le même obstacle lorsqu’ils disposent d’un JPG qui doit être consultable. La bonne nouvelle, c’est qu’avec Aspose OCR for Java, vous pouvez transformer cette image en un PDF entièrement consultable en quelques lignes de code seulement.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : charger un JPG, reconnaître le texte et enregistrer le résultat sous forme de PDF consultable. À la fin, vous saurez comment **convertir jpg en pdf**, comment **extraire du texte d’un jpg**, et pourquoi cette approche est souvent plus fiable que d’essayer d’appliquer l’OCR au PDF après sa création.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants sur votre machine :

* **Java Development Kit (JDK) 8 ou version supérieure** – le code utilise les API Java standard.  
* Bibliothèque **Aspose OCR for Java** – vous pouvez la récupérer depuis Maven Central ou télécharger le JAR depuis le site d’Aspose.  
* Un **exemple de JPG** contenant du texte lisible (par ex. une facture numérisée ou une capture d’écran d’un document).

Aucun framework supplémentaire n’est requis ; l’exemple fonctionne avec un projet Java simple.

## Étape 1 – Configurer le projet et ajouter Aspose OCR

Tout d’abord, créez un nouveau projet Maven (ou simplement un dossier avec le JAR dans le classpath). Si vous utilisez Maven, ajoutez cette dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Astuce :** Vérifiez toujours la dernière version dans le dépôt Maven d’Aspose ; les versions plus récentes incluent des améliorations de performances et des corrections de bugs.

Une fois la dépendance résolue, vous êtes prêt à écrire le code Java qui **créera un PDF consultable**.

## Étape 2 – Charger l’image (image vers PDF consultable)

La première vraie étape consiste à indiquer au moteur OCR l’image source. C’est ici que la transformation **image vers PDF consultable** commence réellement.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **Pourquoi c’est important :** `setImage` indique à Aspose quelle bitmap analyser. Si vous fournissez une image à basse résolution, la qualité de l’OCR en pâtira, alors assurez‑vous que le JPG soit d’au moins 300 dpi pour de meilleurs résultats.

## Étape 3 – Reconnaître le texte à partir de l’image

Maintenant que le moteur sait quelle image traiter, nous pouvons lui demander de **reconnaître le texte à partir de l’image**. Aspose OCR effectue le travail lourd en arrière‑plan, gérant la détection de la langue, la segmentation des caractères et le calcul de la confiance.

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

L’appel `recognize()` renvoie une interface fluide, nous permettant de chaîner la méthode `save`. En spécifiant `OcrOutputFormat.SEARCHABLE_PDF`, la bibliothèque intègre une couche de texte invisible dans le PDF tout en conservant l’apparence originale de l’image.

> **Cas particulier :** Si votre JPG contient plusieurs pages (par ex. un TIFF multipage enregistré sous forme de JPG séparés), vous devrez itérer sur chaque fichier et fusionner les PDF générés ultérieurement. Le même moteur OCR peut être réutilisé pour chaque itération.

## Étape 4 – Vérifier le résultat

Après la fin de l’opération d’enregistrement, un simple message console indique que tout s’est déroulé correctement.

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

Lorsque vous ouvrez `output-searchable.pdf` dans un lecteur comme Adobe Acrobat, vous devez pouvoir sélectionner le texte caché, le copier ou lancer une recherche — exactement ce que vous attendez d’un **PDF consultable**.

### Résultat attendu

L’exécution du programme affiche :

```
Searchable PDF created.
```

Et le PDF généré affichera le JPG original tout en permettant la sélection du texte. Si vous ouvrez les « Propriétés → Description → PDF Producer » du PDF, vous verrez quelque chose comme `Aspose.OCR for Java`.

## Exemple complet fonctionnel

Voici le fichier source complet, prêt à être exécuté. Copiez‑collez‑le dans votre IDE, ajustez les chemins de fichiers, puis lancez‑le.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **Et si l’OCR échoue ?**  
> * Cela se produit généralement parce que l’image est trop bruitée ou que la langue n’est pas prise en charge par défaut. Vous pouvez améliorer la précision en pré‑traitant l’image (augmenter le contraste, redresser) ou en définissant explicitement la langue avec `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);`.

## Questions fréquentes et pièges courants

| Question | Réponse |
|----------|---------|
| **Puis‑je extraire le texte brut au lieu d’un PDF ?** | Oui. Utilisez `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` |
| **Et si je dois traiter un PNG ?** | La même API fonctionne ; il suffit de changer l’extension du fichier dans `fromFile`. |
| **Le PDF résultant est‑il réellement consultable sur tous les lecteurs ?** | Les lecteurs modernes (Adobe Reader, Foxit, Chrome) respectent la couche de texte invisible. Les outils plus anciens pourraient l’ignorer. |
| **Comment contrôler la taille de page du PDF ?** | Aspose OCR utilise par défaut les dimensions de l’image. Pour un format personnalisé, générez le PDF manuellement et superposez la couche de texte OCR — scénario avancé. |

## Conseils de performance

* **Traitement par lots :** Réutilisez une seule instance de `OcrEngine` pour de nombreuses images afin d’éviter le rechargement répété de la bibliothèque native.  
* **Sécurité des threads :** Le moteur **n’est pas** thread‑safe ; créez‑en une par thread si vous parallélisez.  
* **Utilisation de la mémoire :** Les grandes images peuvent consommer beaucoup de RAM. En cas de `OutOfMemoryError`, réduisez la résolution de l’image avant de la transmettre au moteur.

## Prochaines étapes

Maintenant que vous savez comment **créer un PDF consultable**, vous pouvez explorer des tâches connexes :

* **Convertir jpg en pdf** sans OCR (utilisez la bibliothèque Aspose PDF pour un PDF image simple).  
* **Extraire du texte d’un jpg** dans un fichier `.txt` pour l’indexation.  
* **Combiner plusieurs PDF consultables** en un seul document avec `PdfFileEditor` d’Aspose PDF.  

Toutes ces actions s’appuient sur la même base que vous venez de mettre en place.

---

### Récapitulatif rapide

* Nous avons **créé un PDF consultable** à partir d’un JPG avec Aspose OCR for Java.  
* Le processus a couvert le chargement de l’image, la reconnaissance du texte et l’enregistrement en PDF consultable.  
* Vous disposez désormais d’un modèle réutilisable pour **image vers PDF consultable**, **reconnaître le texte à partir d’une image**, **extraire du texte d’un jpg**, et **convertir jpg en pdf**.

Testez-le avec vos propres documents, ajustez les paramètres de langue si nécessaire, et laissez l’OCR faire le gros du travail. Bon codage !  

![Create searchable PDF example](placeholder.png){alt="Créer un PDF consultable"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}