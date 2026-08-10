---
category: general
date: 2026-05-06
description: Comment utiliser l'OCR pour extraire du texte d’une image en Java. Apprenez
  la conversion d’image en texte avec l’OCR, corrigez les erreurs d’OCR et chargez
  une image pour l’OCR avec Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: fr
og_description: Comment utiliser l'OCR en Java pour extraire du texte d’une image,
  corriger les erreurs d’OCR et charger une image pour l’OCR à l’aide d’Aspose OCR.
og_title: Comment utiliser l'OCR en Java – Guide complet
tags:
- OCR
- Java
- Aspose
title: Comment utiliser l'OCR en Java – Extraire du texte d’une image avec correction
  orthographique
url: /fr/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Java – Extraire du texte d'une image avec correction orthographique

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour transformer une photo de reçu floue en texte propre et interrogeable ? Vous n'êtes pas seul. Dans de nombreux projets—applications de suivi des dépenses, pipelines de numérisation de factures, ou même un script de prise de notes rapide—obtenir un texte fiable à partir d'une image est le premier obstacle.  

Ce tutoriel vous montre exactement comment utiliser l'OCR en Java, couvrant tout, du chargement de l'image pour l'OCR à la correction des erreurs d'OCR afin que le résultat ressemble à du texte tapé par un humain. À la fin, vous serez capable d'**extraire du texte d'une image**, d'effectuer une conversion **OCR image en texte**, et de corriger automatiquement les erreurs de reconnaissance courantes.

## Ce que vous allez créer

Nous allons créer un petit programme console Java qui :

1. Charge un PNG (ou tout autre format supporté) dans le moteur Aspose OCR.  
2. Active la fonctionnalité de correction orthographique intégrée pour **corriger les erreurs d'OCR**.  
3. Exécute le processus de reconnaissance et affiche le texte nettoyé.  

Aucun service externe, aucun framework lourd—juste un seul JAR et quelques lignes de code.

### Prérequis

- Java Development Kit (JDK) 8 ou plus récent.  
- Maven (ou tout autre outil de construction) pour récupérer la bibliothèque Aspose OCR.  
- Un fichier image (par ex. `receipt.png`) que vous souhaitez analyser.  

Si le JAR Aspose OCR vous manque, ajoutez cette dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Astuce :** La version d'évaluation gratuite fonctionne pour les tests, mais une licence supprime le filigrane d'évaluation.

## Étape 1 – Initialiser le moteur OCR (Mot‑clé principal en action)

La première chose à faire est de créer une instance de `OcrEngine`. Considérez‑la comme le cerveau qui lira les pixels et les transformera en caractères.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Pourquoi c'est important :* Initialiser le moteur configure les ressources internes (modèles de langue, dictionnaires, etc.). Sauter cette étape provoquerait une `NullPointerException` plus tard lorsque vous essayerez de charger une image.

## Étape 2 – Charger l'image pour l'OCR

Nous allons maintenant réellement **charger l'image pour l'OCR**. Aspose fournit un utilitaire pratique `ImageStream.fromFile`, mais vous pouvez également fournir un `byte[]` si vous le préférez.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Erreur fréquente :* Le chemin du fichier doit être absolu ou relatif au répertoire de travail. Si l'image est introuvable, le moteur lève une `IOException`. Vérifiez bien le chemin, surtout lors de l'exécution depuis un IDE versus un JAR empaqueté.

## Étape 3 – Activer la correction orthographique pour **corriger les erreurs d'OCR**

L'OCR tel quel peut être bruyant—pensez à “l0ve” au lieu de “love” ou “0” pour “O”. Activer la correction orthographique indique au moteur d'exécuter une passe de post‑traitement qui corrige les erreurs typiques.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Pourquoi vous le voudriez :* Sans correction orthographique, vous pourriez devoir nettoyer manuellement la sortie, ce qui annule le but de l'automatisation. Le dictionnaire intégré fonctionne bien pour l'anglais et plusieurs autres langues.

## Étape 4 – Effectuer la reconnaissance (**OCR image en texte**)

Avec l'image chargée et la correction orthographique activée, nous pouvons enfin demander au moteur de reconnaître le texte.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Cas limite :* Si l'image a un faible contraste ou est fortement inclinée, le résultat peut encore contenir du charabia. Envisagez un pré‑traitement (par ex. binarisation, redressement) avant de la fournir au moteur.

## Étape 5 – Afficher le texte nettoyé

La dernière étape consiste simplement à imprimer le résultat. Dans une application réelle vous pourriez l'écrire dans une base de données ou un fichier, mais pour cette démo `System.out` suffit.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Sortie attendue

En supposant que `receipt.png` contienne une liste claire d'articles, vous pourriez voir quelque chose comme :

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Remarquez comment “Qty” et “Price” sont orthographiés correctement même si le scan original contenait un “Qy” erroné.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un fichier nommé `SpellCorrectDemo.java`. Assurez‑vous que le JAR Aspose OCR se trouve dans votre classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Exécutez‑le avec :

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Vous devriez maintenant voir le texte nettoyé affiché dans la console.

## Bonus : Ajuster les paramètres pour une meilleure précision

Bien que la configuration par défaut fonctionne pour la plupart des documents imprimés, vous pourriez devoir ajuster quelques paramètres pour des scénarios spécialisés :

| Paramètre | Description | Quand le modifier |
|-----------|-------------|-------------------|
| `setLanguage(OcrLanguage.English)` | Force le dictionnaire anglais (réduit les faux positifs) | Si votre image ne contient que du texte anglais. |
| `setResolution(300)` | Indique au moteur le DPI de l'image source | Pour des numérisations haute résolution. |
| `setEnableAutoSkewCorrection(true)` | Corrige automatiquement les pages légèrement inclinées | Lorsque les images sont capturées avec un téléphone. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec les PDF ?**  
R : Oui. Convertissez chaque page PDF en image (par ex. avec Aspose PDF) et fournissez l'image au moteur OCR.

**Q : Et si mon image est au format BMP ?**  
R : `ImageStream.fromFile` prend en charge PNG, JPEG, BMP, TIFF et GIF nativement. Il suffit de changer l'extension du fichier.

**Q : Puis‑je désactiver la correction orthographique ?**  
R : Absolument—définissez `setEnableSpellCorrection(false)` si vous avez besoin d'une sortie OCR brute pour un traitement en aval.

## Conclusion

Vous savez maintenant **comment utiliser l'OCR** en Java pour **extraire du texte d'une image**, **corriger automatiquement les erreurs d'OCR**, et **charger correctement l'image pour l'OCR** en utilisant Aspose OCR. Le flux en cinq étapes—initialiser, charger, activer la correction orthographique, reconnaître et afficher—couvre la majorité des tâches OCR quotidiennes.  

À partir d'ici, envisagez d'enchaîner cette logique avec une écriture dans une base de données, un point d'accès REST, ou un processeur batch pour gérer des dizaines de reçus à la fois. Expérimentez avec le tableau de paramètres supplémentaires ci‑dessus pour extraire chaque dernier caractère de précision.

Bon codage, et que vos résultats OCR soient toujours plus propres que vos reçus tachés de café ! 

![diagramme montrant comment utiliser l'OCR : image → moteur OCR → texte corrigé]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}