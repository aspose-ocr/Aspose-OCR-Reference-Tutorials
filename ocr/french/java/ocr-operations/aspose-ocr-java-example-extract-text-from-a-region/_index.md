---
category: general
date: 2026-05-03
description: L'exemple Aspose OCR Java montre comment charger une image pour l'OCR
  et extraire le texte d'une région en quelques lignes de code seulement.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: fr
og_description: L'exemple Aspose OCR Java montre le chargement d'une image pour l'OCR
  et l'extraction de texte d'une région spécifique, idéal pour le traitement des factures.
og_title: Exemple Aspose OCR Java – Extraction de texte de région
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Exemple Aspose OCR Java : Extraire du texte d’une région'
url: /fr/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Example : Extraire du texte d'une région

Vous cherchez un **exemple Aspose OCR Java** qui vous permette d'extraire uniquement la partie dont vous avez besoin d'une image ? Dans ce guide, nous verrons comment **charger une image pour l’OCR** et **extraire du texte d’une région**, idéal pour les numéros de facture, les champs de formulaire ou tout autre morceau de donnée caché dans une image plus grande.

Vous vous demandez peut‑être pourquoi se limiter à un rectangle plutôt que de scanner la page entière. La réponse courte : vitesse et précision. Lorsque le moteur ne regarde qu’une tranche définie, il ignore le bruit inutile, s’exécute plus rapidement et produit souvent des résultats plus propres. À la fin de ce tutoriel, vous disposerez d’un programme Java autonome qui fait exactement cela, ainsi que de quelques astuces pour éviter les pièges courants qui bloquent les débutants.

## Ce dont vous avez besoin

- **Java Development Kit (JDK) 11** ou une version plus récente installée.
- Bibliothèque **Aspose.OCR for Java** (vous pouvez récupérer le dernier JAR depuis le dépôt Maven Central ou le portail de téléchargement Aspose).
- Un fichier image contenant le texte à lire – pour notre démonstration nous utiliserons `invoice.png`, qui comporte un numéro de facture quelque part près du coin supérieur droit.
- Un IDE préféré ou un simple éditeur de texte plus un terminal ; n’importe quel outil de construction (Maven, Gradle ou simplement `javac`) convient.

C’est tout. Aucun moteur OCR supplémentaire, aucune bibliothèque native, juste du Java pur et Aspose.

![Capture d'écran de l'exemple Aspose OCR Java](/images/aspose-ocr-java-example.png "Exemple Aspose OCR Java montrant l'extraction d'une région")

## Exemple Aspose OCR Java – Initialiser le moteur OCR

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Pourquoi c’est important :** Créer le moteur dès le départ vous fournit un objet propre à configurer. Vous pouvez réutiliser le même `OcrEngine` pour plusieurs images si vous traitez un lot, ce qui économise de la mémoire et du temps d’initialisation.

## Charger l'image pour l'OCR

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Astuce :** Remplacez `YOUR_DIRECTORY` par un chemin absolu ou relatif pointant vers l’endroit où vous avez stocké `invoice.png`. Si le fichier est introuvable, Aspose lève une `IOException`, il peut donc être judicieux d’envelopper cela dans un bloc try‑catch pour le code de production.

## Définir et extraire du texte d’une région

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Comment ça fonctionne :** En appelant `setRegion`, vous limitez le scan OCR à une tranche de 300 pixels de large qui débute à 120 pixels du bord gauche et 250 pixels du haut. Ajustez ces valeurs pour correspondre à votre propre mise en page ; un moyen rapide de les trouver est d’ouvrir l’image dans n’importe quel éditeur graphique affichant les coordonnées en pixels.

## Activer la langue et lancer la reconnaissance

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Pourquoi n’activer que l’anglais ?** Le moteur OCR essaiera de faire correspondre les caractères de chaque langue activée, ce qui peut le perturber lorsque le texte est simplement alphanumérique. Restreindre le jeu de langues améliore à la fois la vitesse et la précision.

### Résultat attendu

```
Extracted region text: INV-12345
```

Si le rectangle est décalé de quelques pixels, la sortie peut être illisible ou vide. C’est un contrôle de base simple : exécutez le programme, regardez la console et vérifiez que le texte correspond à ce que vous voyez sur l’image.

## Exécuter le code et vérifier la sortie

En supposant que vous utilisiez Maven, ajoutez la dépendance Aspose OCR à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Compilez et exécutez :

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Ou, si vous préférez le simple `javac` :

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Vous devriez voir la ligne **Extracted region text** affichée dans la console. Si vous obtenez « OCR recognition failed », revérifiez le chemin du fichier et assurez‑vous que la région contient bien des caractères lisibles.

## Cas limites & variations courantes

| Situation | Ce qu’il faut modifier |
|-----------|------------------------|
| **Multiple languages** (p. ex., English + Spanish) | Appelez `ocrEngine.getLanguage().setSpanish(true);` en plus de l'anglais. |
| **Région hors des limites de l'image** | Aspose découpera silencieusement le rectangle, mais vous perdrez des données. Utilisez `ImageInfo` (`ocrEngine.getImage().getWidth()`) pour vérifier les dimensions avant de définir la région. |
| **Factures dynamiques** (différentes mises en page) | Envisagez d’effectuer un pré‑scan léger sur l’ensemble de l’image pour localiser des mots‑clés comme « Invoice # » puis calculez le rectangle de façon programmatique. |
| **Images à DPI élevé** | Augmentez `ocrEngine.getImage().setResolution(300);` pour une meilleure précision sur les documents numérisés. |
| **Optimisation des performances** | Désactivez les langues inutiles, gardez la région aussi petite que possible, et réutilisez une seule instance de `OcrEngine` pour de nombreux fichiers. |

## Astuces pro du terrain

- **Astuce pro :** Si vous avez uniquement besoin de chiffres (courant pour les numéros de facture), activez le mode numérique avec `ocrEngine.getLanguage().setDigits(true);`. Cela élimine le bruit alphabétique.
- **À surveiller :** PNG transparents. Aspose interprète parfois mal le canal alpha ; convertir l’image en JPEG à fond uni d’abord peut résoudre les sorties vides étranges.
- **Rappel :** Le rectangle utilise le système de coordonnées natif de l’image, pas le redimensionnement UI que vous pourriez voir à l’écran. Testez toujours avec le fichier exact que vous traiterez en production.

## Et après ?

Maintenant que vous disposez d’un **exemple Aspose OCR Java** solide pour l’extraction basée sur une région, vous pouvez l’étendre dans plusieurs directions utiles :

- **Traitement par lots :** Parcourez un dossier de factures, en réutilisant le même `OcrEngine` pour améliorer le débit.
- **Validation des données :** Faites passer le texte extrait à travers une expression régulière comme `INV-\\d{5}` pour vous assurer d’avoir capturé un numéro de facture valide.
- **Intégration avec PDF :** Utilisez Aspose.PDF pour superposer le texte extrait sur le document original à des fins d’audit.
- **Déploiement cloud :** Enveloppez le code dans un service REST léger (Spring Boot) afin que d’autres systèmes puissent l’appeler à la demande.

Chacune de ces étapes implique naturellement les mêmes concepts de base — **charger l’image pour l’OCR**, **extraire du texte d’une région**, et gérer les résultats — vous trouverez donc la transition fluide.

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou consultez les forums Aspose où la communauté partage des ajustements concrets pour les mises en page complexes.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}