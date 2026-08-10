---
category: general
date: 2026-02-19
description: Extraire du texte d’une image avec Java OCR. Découvrez un exemple Java
  OCR qui charge une image pour l’OCR et extrait le texte des factures en quelques
  étapes seulement.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: fr
og_description: Extraire du texte d’une image avec Java OCR. Ce guide montre comment
  charger une image pour l’OCR et extraire le texte des factures avec un exemple simple
  d’OCR Java.
og_title: Extraire du texte d'une image en Java – Exemple complet d'OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extraire du texte d’une image en Java – Exemple complet d’OCR
url: /fr/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’une image en Java – Exemple complet d’OCR

Vous avez déjà eu besoin **d’extraire du texte d’une image** sans savoir quelle bibliothèque choisir ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils automatisent le traitement de factures ou créent des archives consultables. Bonne nouvelle ? En quelques lignes de Java, vous pouvez charger une image pour l’OCR, définir une région d’intérêt et récupérer le texte exact dont vous avez besoin.  

Dans ce tutoriel, nous allons parcourir un **exemple java ocr** qui montre exactement comment **charger une image pour l’OCR**, définir une ROI, et **extraire du texte d’une facture** à l’aide d’Aspose.OCR. À la fin, vous disposerez d’un programme exécutable que vous pourrez intégrer à n’importe quel projet Java.

## Ce que vous allez apprendre

- Comment créer une instance `OcrEngine` et pourquoi c’est important.  
- La bonne façon de **charger une image pour l’OCR** avec `ImageStream` d’Aspose.  
- Définir une **région d’intérêt (ROI)** afin de ne traiter que la partie de l’image contenant le montant de la facture.  
- Extraire le texte reconnu et l’afficher dans la console.  
- Les pièges courants (par ex. coordonnées de rectangle incorrectes) et leurs solutions rapides.

**Prérequis**

- Java 8 ou version supérieure installé.  
- Maven ou Gradle pour récupérer la bibliothèque Aspose.OCR (`com.aspose:aspose-ocr`).  
- Une image de facture d’exemple (`invoice.png`) placée dans un répertoire connu.

Tout est‑t‑il prêt ? Parfait—plongeons‑y.

![Extraire du texte d’une image avec Java OCR](/images/extract-text-from-image-java.png "exemple d’extraction de texte d’image")

## Extraire du texte d’une image – Exemple d’OCR Java étape par étape

Voici le code complet. N’hésitez pas à le copier‑coller dans `RoiOcrExample.java` et à l’exécuter directement.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Pourquoi chaque étape est importante

1. **Création du moteur OCR** – sans moteur il n’y a aucun contexte pour le traitement d’image. L’objet vous permet également d’ajuster les packs de langues plus tard si vous avez besoin d’un support multilingue.  
2. **Chargement de l’image** – `ImageStream.fromFile` masque le format du fichier, garantissant que le moteur lit correctement les octets. Si vous omettez cette étape, vous obtiendrez un `NullPointerException`.  
3. **Définition de la ROI** – traiter la page entière peut être gaspilleur. En restreignant le rectangle à la zone du total de la facture, vous accélérez la reconnaissance et réduisez le bruit.  
4. **Appel de `recognize()`** – c’est ici que la magie opère. La méthode exécute l’algorithme OCR sur la ROI et produit un objet résultat.  
5. **Affichage du résultat** – dans les projets réels vous stockerez probablement le texte dans une base de données, mais `System.out.println` est parfait pour une démonstration rapide.

## Charger une image pour l’OCR

Si vous vous demandez si le chemin doit être absolu ou relatif, la réponse est que les deux fonctionnent—assurez‑vous simplement que le processus Java peut lire le fichier. Sous Windows, les antislashs doivent être échappés (`C:\\images\\invoice.png`) ou vous pouvez utiliser des barres obliques (`C:/images/invoice.png`).  

**Astuce :** si vous traitez de nombreuses factures dans une boucle, réutilisez la même instance `OcrEngine` ; elle met en cache les ressources internes et améliore le débit.

## Définir la région d’intérêt (ROI)

Choisir le bon rectangle peut demander quelques essais. Un moyen pratique de trouver les coordonnées est d’ouvrir l’image dans n’importe quel éditeur graphique (comme GIMP ou Paint.NET) et de survoler la zone — vous verrez les valeurs X/Y dans la barre d’état.  

Cas particulier : certaines factures ont des mises en page variables. Dans ce scénario, vous pouvez d’abord faire un pré‑scan rapide de l’image entière, localiser des mots‑clés comme « Total : » avec une expression régulière, puis ajuster la ROI dynamiquement.

## Effectuer l’OCR et obtenir le texte

L’appel `recognize()` est synchrone—votre thread se bloque jusqu’à ce que le moteur termine. Pour de gros lots, vous pouvez créer un pool de threads et traiter les images en parallèle. N’oubliez pas que chaque thread a besoin de sa propre instance `OcrEngine` ; elles ne sont pas thread‑safe.

## Exécuter et vérifier la sortie

Compilez et lancez :

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Vous devriez voir quelque chose comme :

```
ROI text: $1,254.00
```

Si la sortie apparaît brouillée, revérifiez les coordonnées de la ROI et assurez‑vous que la qualité de l’image est élevée (300 dpi ou plus donne les meilleurs résultats).  

### Pièges courants & solutions

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Chaîne vide | ROI en dehors des limites de l’image | Vérifier les valeurs du rectangle par rapport aux dimensions de l’image |
| Mots mal orthographiés | Résolution faible | Utiliser une source à plus haute résolution ou appliquer un pré‑traitement d’image (ex. binarisation) |
| `java.lang.NoClassDefFoundError` | JAR Aspose manquant sur le classpath | Ajouter `aspose-ocr.jar` à `-cp` ou utiliser la gestion de dépendances Maven/Gradle |

## Conclusion

Vous savez maintenant comment **extraire du texte d’une image** en Java grâce à un **exemple java ocr** concis. En chargeant correctement l’image, en définissant une ROI ciblée et en appelant `recognize()`, vous pouvez extraire de façon fiable le **texte d’une facture** et alimenter ces données dans des systèmes en aval.

Et après ? Essayez de remplacer la ROI pour d’autres champs (date, nom du fournisseur), expérimentez les packs de langues pour des factures multilingues, ou intégrez l’étape OCR dans un micro‑service Spring Boot. Le même schéma fonctionne pour les reçus, les passeports ou tout document nécessitant une extraction précise du texte.

Si vous avez des questions sur la mise à l’échelle de cette solution ou la gestion de scans bruyants, laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}