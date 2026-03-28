---
category: general
date: 2026-03-28
description: Effectuez une OCR sur une image en Java avec Aspose OCR pour convertir
  l'image en texte, extraire le texte thaï d'un PNG rapidement et de façon fiable.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: fr
og_description: Exécutez la reconnaissance optique de caractères sur une image avec
  Java et Aspose OCR. Apprenez à convertir une image en texte, extraire du texte thaï
  d’un PNG et à gérer les pièges courants.
og_title: Effectuer l'OCR d'une image avec Java – Extraire rapidement le texte thaï
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Exécuter la reconnaissance optique de caractères sur une image avec Java –
  Extraire le texte thaï d’un PNG
url: /fr/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter OCR sur une image avec Java – Tutoriel complet

Vous vous êtes déjà demandé comment **exécuter OCR sur image** directement depuis du code Java ? Peut-être avez‑vous une collection de reçus thaïlandais, de documents numérisés ou de captures d’écran et vous avez besoin du texte sans le taper manuellement. C’est un problème courant, surtout lorsque la source est un PNG et que la langue n’est pas latine.  

Dans ce guide, nous vous montrerons exactement comment **exécuter OCR sur image** en utilisant la bibliothèque Aspose OCR, convertir l’image en texte brut et extraire de façon fiable les caractères thaïlandais. À la fin, vous serez capable de **convertir l’image en texte**, **extraire du texte d’un PNG**, et même **reconnaître le texte thaï** avec seulement quelques lignes de code.

## Ce que couvre ce tutoriel

* Configurer la dépendance Aspose OCR dans un projet Maven/Gradle.  
* Initialiser le `OcrEngine` et le configurer pour la langue thaï.  
* Exécuter OCR sur un fichier PNG et gérer les éventuelles erreurs.  
* Afficher le résultat dans la console et vérifier la sortie.  

Aucune expérience préalable avec Aspose n’est requise — il suffit d’un IDE Java de base et d’un fichier image que vous souhaitez traiter.

## Prérequis

* Java 8 ou version supérieure installé (la bibliothèque fonctionne également avec Java 11+).  
* Un outil de construction – Maven ou Gradle (nous montrerons l’extrait Maven).  
* Une licence Aspose OCR (l’essai gratuit fonctionne pour les tests, mais une licence supprime les limites d’évaluation).  
* Un PNG contenant du texte thaï, par exemple `input.png` placé dans le dossier resources de votre projet.

---

## Étape 1 : Ajouter Aspose OCR à votre projet

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Conseil pro :** Gardez la version de la bibliothèque synchronisée avec les notes de version officielles d’Aspose ; les versions plus récentes ajoutent des packs de langues et des améliorations de performances.

Une fois la dépendance résolue, votre IDE devrait importer automatiquement les classes requises.

## Étape 2 : Initialiser le moteur OCR

Le moteur est le cœur du processus – pensez‑y comme le « cerveau » qui analyse les motifs de pixels. Nous indiquerons également qu’il ne nous intéresse que les caractères thaï.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Pourquoi définir explicitement la langue ? Parce que spécifier `"th"` restreint l’ensemble de caractères, ce qui accélère la reconnaissance et réduit les erreurs de lecture de glyphes similaires.

## Étape 3 : Exécuter OCR sur le fichier PNG

Nous transmettons maintenant au moteur l’image que nous voulons décoder. La méthode `recognizeImage` renvoie un objet `OcrResult` qui contient la chaîne extraite et les scores de confiance.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Si le fichier est introuvable, Aspose lance une `FileNotFoundException`. Il est conseillé d’envelopper l’appel dans un bloc `try‑catch` pour le code de production, mais pour ce tutoriel nous resterons simples.

## Étape 4 : Afficher le texte reconnu

Enfin, nous affichons le résultat. La méthode `getText()` renvoie une `String` Java simple que vous pouvez stocker, envoyer sur un réseau ou écrire dans un fichier.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Si la sortie apparaît brouillée, vérifiez que le PNG source est en haute résolution (au moins 300 dpi) et que le code de langue `"th"` correspond à votre langue cible.

### Listing complet

Voici le fichier Java complet, prêt à être exécuté. Copiez‑collez‑le dans votre IDE, remplacez le chemin de l’image si nécessaire, et cliquez sur **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![exemple d'exécution OCR sur image](image.png "exemple d'exécution OCR sur image – code Java extrayant du texte thaï à partir d'un PNG")

## Étape 5 : Variations courantes et cas limites

### Convertir une image en texte dans d’autres formats

Si vous devez **convertir une image en texte** pour un JPEG ou BMP, il suffit de changer l’extension du fichier dans `imagePath`. Aspose OCR prend en charge PNG, JPEG, BMP, TIFF, et même les pages PDF.

### Extraire du texte d’un PNG avec plusieurs langues

Vous pouvez demander au moteur de détecter plusieurs langues simultanément :

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Le résultat contiendra un mélange de caractères thaï et anglais, ce qui est pratique pour les reçus bilingues.

### Gérer les images de basse qualité

Pour les numérisations floues, envisagez d’activer le pré‑traitement :

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Cela déclenche les algorithmes intégrés de dé‑bruitage et d’amélioration du contraste, améliorant l’étape **extraire du texte d’un PNG**.

### Activation de licence

Sans licence, Aspose insère une ligne de filigrane dans la sortie après 100 pages. Activez votre licence rapidement :

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Placez le fichier `.lic` à côté de votre JAR ou référencez‑le via un chemin absolu.

## Questions fréquentes

**Q : Cela fonctionne‑t‑il sous Linux ?**  
A : Absolument. Aspose OCR est purement Java, donc tout OS compatible JVM convient.

**Q : Et si le PNG contient du thaï manuscrit ?**  
A : La reconnaissance d’écriture manuscrite est limitée ; vous pourriez avoir besoin d’un modèle de réseau neuronal dédié. Aspose OCR excelle avec le texte imprimé.

**Q : Puis‑je traiter un lot d’images dans un dossier ?**  
A : Enveloppez l’appel `recognizeImage` dans une boucle sur `Files.list(Paths.get("folder"))`. N’oubliez pas de réutiliser la même instance `OcrEngine` pour les performances.

## Conclusion

Nous avons parcouru un exemple complet, de bout en bout, montrant comment **exécuter OCR sur image** en Java, spécifiquement pour **extraire du texte thaï** d’un PNG. En initialisant le `OcrEngine`, en définissant la langue, en appelant `recognizeImage` et en affichant le résultat, vous disposez maintenant d’une méthode fiable pour **convertir une image en texte** sans services tiers.

Vous pourriez maintenant :

* **extraire du texte d’un PNG** en masse pour des projets de data‑mining.  
* Combiner la sortie OCR avec une API de traduction pour obtenir les équivalents anglais.  
* Explorer d’autres langues prises en charge par Aspose, comme le chinois ou l’arabe, en changeant le code de langue.

Essayez‑le avec vos propres images — ajustez les paramètres de pré‑traitement, expérimentez différents formats de fichier, et voyez à quel point la solution est robuste dans votre flux de travail réel.

Bon codage, et que vos pipelines OCR soient toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}