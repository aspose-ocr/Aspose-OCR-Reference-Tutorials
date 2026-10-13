---
category: general
date: 2026-02-14
description: Extraire du texte d’une image à l’aide d’Aspose OCR en Java. Apprenez
  comment extraire le texte des champs de formulaire avec des régions d’intérêt pour
  des résultats précis.
draft: false
keywords:
- extract text from image
- extract text from form
language: fr
og_description: Extraire du texte d’une image à l’aide d’Aspose OCR en Java. Ce tutoriel
  montre comment extraire le texte des champs de formulaire via des régions d’intérêt.
og_title: Extraire du texte d'une image avec Aspose OCR – Guide Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extraire du texte d’une image avec Aspose OCR – Guide Java
url: /fr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'une image avec Aspose OCR – Guide Java

Vous avez déjà eu besoin d'**extraire du texte à partir d'une image** mais vous vous êtes retrouvé à analyser toute l'image, gaspillant des cycles CPU et obtenant des résultats bruyants ? Vous n'êtes pas le seul. Dans de nombreuses applications réelles—pensez aux scanners de factures, aux lecteurs de passeports ou aux formulaires de saisie de données—vous ne vous souciez que de quelques champs, pas de toute la toile.  

La bonne nouvelle, c'est qu'Aspose OCR vous permet d'**extraire du texte à partir d'une image** *et* de zones spécifiques d'un formulaire en définissant des polygones. Dans ce tutoriel, vous verrez exactement comment **extraire du texte à partir d'un formulaire** en Java, pourquoi cette approche est importante, et quoi ajuster lorsque les choses tournent mal.

Ci‑dessous, nous couvrirons tout, de la configuration de la bibliothèque à la gestion des cas limites compliqués, afin qu'à la fin vous disposiez d'un extrait de code prêt à l'emploi qui récupère uniquement les données dont vous avez besoin.

## Ce dont vous avez besoin

- Java 17 (ou tout JDK récent) – les versions plus récentes offrent un meilleur support Unicode.  
- Aspose.OCR for Java 23.10 (ou la dernière version disponible au moment de la lecture).  
- Une image d'exemple nommée `form.png` contenant des champs clairement définis.  
- Un IDE ou un éditeur de texte simple—IntelliJ IDEA, VS Code, ou même Notepad suffisent.

Aucun tour de magie Maven/Gradle n'est requis pour la démo principale ; ajoutez simplement le JAR Aspose OCR à votre classpath.

---

## Étape 1 – Initialiser le moteur OCR et charger votre image

La première chose dont le moteur a besoin est un bitmap sur lequel travailler. Nous le pointerons vers `form.png`, qui se trouve dans le même dossier que le fichier source.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Pourquoi c'est important :*  
Créer un nouveau `OcrEngine` vous donne une base propre, garantissant qu'aucun paramètre résiduel n'affecte votre exécution. Charger l'image dès le départ valide également que le fichier existe, vous obtenez ainsi une exception utile avant de perdre du temps sur les étapes suivantes.

> **Astuce :** Si votre image est très grande (plus de 5 Mo), envisagez de la redimensionner d'abord. Aspose OCR fonctionne plus rapidement sur des images de moins de 2000 px dans chaque dimension.

## Étape 2 – Définir les polygones pour les champs que vous souhaitez lire

Une *Region of Interest* (ROI) n'est qu'un polygone qui indique au moteur où regarder. Ci‑dessous, nous créons deux rectangles — l'un pour « First Name » et l'autre pour « Date of Birth ». Ajustez les coordonnées pour qu'elles correspondent à votre propre formulaire.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Pourquoi des polygones plutôt que des rectangles ?*  
Les polygones vous offrent la flexibilité de gérer des cases inclinées ou non rectangulaires—courant lors de la numérisation de formulaires imprimés qui ne sont pas parfaitement alignés.

## Étape 3 – Indiquer à Aspose OCR de se concentrer uniquement sur ces régions

Nous associons maintenant les polygones au moteur. La méthode `setRegionsOfInterest` accepte une liste, vous pouvez donc ajouter autant de champs que vous le souhaitez.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Que se passe-t-il en interne ?*  
Aspose OCR découpe chaque polygone en un bitmap séparé, exécute son algorithme de reconnaissance, puis assemble les résultats. Cela réduit considérablement les faux positifs provenant des graphiques environnants.

## Étape 4 – Exécuter le processus OCR

Une fois tout configuré, nous lançons l'OCR. L'appel `process()` renvoie un objet `OcrResult` qui contient le texte extrait et les scores de confiance.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Si vous avez besoin de la confiance par champ, vous pouvez inspecter `ocrResult.getRegions()`—chaque région possède son propre score. Pour la plupart des formulaires simples, le texte global suffit.

## Étape 5 – Afficher (ou stocker) le texte extrait

Enfin, nous affichons le résultat dans la console. Dans une application réelle, vous pourriez l'écrire dans une base de données, un fichier JSON, ou l'envoyer via une API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Sortie attendue (exemple) :**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Les deux lignes correspondent aux deux polygones que nous avons définis. Si vous voyez des espaces supplémentaires, supprimez‑les avec `String.trim()`.

## Comment extraire du texte d'un formulaire lorsque vous avez de nombreux champs

Lorsqu'un formulaire contient des dizaines d'entrées, saisir manuellement les coordonnées devient fastidieux. Voici un modèle rapide que vous pouvez adopter :

1. **Créer un CSV** où chaque ligne contient `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Charger le CSV** à l'exécution, parcourir chaque ligne, construire un `Polygon`, et l'ajouter à la liste ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Pourquoi faire cela ?*  
L'automatisation de la génération des ROI vous permet de réutiliser le même code Java sur plusieurs mises en page de formulaires, en gardant votre projet DRY (Don’t Repeat Yourself).

## Cas limites & astuces auxquelles vous n'avez peut‑être pas pensé

- **Scans tournés :** Si l'image entière est tournée, appelez `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Faible contraste :** Définissez `ocrEngine.getEngineOptions().setContrast(1.5f)` pour améliorer la lisibilité.  
- **Scripts non latins :** Changez la langue avec `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (ou toute langue prise en charge).  
- **Échecs partiels d'OCR :** Vérifiez toujours `ocrResult.getConfidence()` ; s'il descend en dessous de 80 %, envisagez de demander à l'utilisateur une vérification manuelle.  

## Exemple complet fonctionnel (prêt à copier‑coller)

Ci‑dessous se trouve le programme complet, prêt à être compilé et exécuté. Remplacez `YOUR_DIRECTORY` par le dossier contenant `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Compilez avec :

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Vous devriez voir les deux lignes de texte correspondant aux ROI définis.

## Questions fréquentes

**Q : Cela fonctionne-t-il avec les PDF ?**  
R : Pas directement. Convertissez chaque page PDF en image d'abord (par ex., avec Aspose PDF) puis fournissez l'image au moteur OCR.

**Q : Et si mon formulaire comporte des cases à cocher ?**  
R : L'OCR ne peut pas lire les états booléens, mais vous pouvez traiter la zone de la case à cocher comme une ROI et inspecter la densité de pixels pour en déduire une coche.

**Q : Puis‑je extraire du texte d'un formulaire multi‑pages en une seule fois ?**  
R : Parcourez chaque image de page, réutilisez la même liste ROI, et concaténez les résultats.

## Conclusion

Nous avons parcouru une solution complète, de bout en bout, pour **extraire du texte à partir d'une image** avec Aspose OCR, et montré comment la même technique vous permet d'**extraire du texte à partir d'un formulaire** avec une précision chirurgicale. En définissant des polygones, en limitant la zone d'intérêt du moteur et en gérant les pièges courants, vous obtenez des données rapides et propres sans le surcoût du traitement de l'image entière.

Prêt pour l'étape suivante ? Essayez d'enchaîner la sortie OCR dans une charge JSON, ou alimentez‑la à un modèle d'apprentissage automatique pour validation. Le ciel est la limite, et maintenant vous

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}