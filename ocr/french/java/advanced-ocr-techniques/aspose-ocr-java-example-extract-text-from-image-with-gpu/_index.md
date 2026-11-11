---
category: general
date: 2026-06-28
description: Apprenez un exemple Aspose OCR Java pour extraire du texte d'images dans
  des projets Java et définissez la limite de mémoire GPU pour des résultats plus
  rapides.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: fr
og_description: Exemple Aspose OCR Java montrant comment extraire du texte d’une image
  avec du code Java tout en définissant une limite de mémoire GPU pour des performances
  optimales.
og_title: Exemple Aspose OCR Java – Extraction rapide de texte accélérée par GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: Exemple Aspose OCR Java – Extraire du texte d’une image avec GPU
url: /fr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exemple Aspose OCR Java – Extraire du texte d’une image avec le GPU

Vous êtes-vous déjà demandé comment **extraire du texte d’une image Java** sans épuiser votre CPU ? Vous n’êtes pas seul. Dans de nombreux scénarios réels – numérisation de reçus, vérification d’identité, archivage massif de documents – le goulot d’étranglement est le moteur OCR lui‑même.  

Bonne nouvelle : cet **exemple Aspose OCR Java** vous guide pas à pas à travers un programme complet, prêt à l’emploi, qui exploite l’accélération GPU, et montre même comment **définir une limite de mémoire GPU** pour que votre serveur reste stable. À la fin de ce guide, vous disposerez d’une classe Java fonctionnelle qui lit un fichier image, exécute l’OCR sur le GPU et affiche le texte reconnu dans la console. Pas de références vagues, seulement du code concret et des explications claires.

Nous couvrirons tout, de la licence à l’optimisation du GPU, afin que, que vous soyez un développeur Java chevronné ou que vous fassiez vos premiers pas en vision par ordinateur, vous trouviez votre compte ici. La seule condition préalable est un environnement de développement Java (JDK 8 ou supérieur) et l’accès à un GPU compatible CUDA ou OpenCL.

---

## Prérequis

- **Java Development Kit (JDK) 8+** – vous pouvez le télécharger depuis Oracle ou adopter OpenJDK.  
- **Bibliothèque Aspose.OCR for Java** – obtenez le JAR depuis le site Aspose ou Maven Central.  
- **Un fichier de licence Aspose OCR valide** (`Aspose.OCR.Java.lic`). L’essai gratuit suffit pour les tests, mais la licence supprime les filigranes d’évaluation.  
- **GPU avec support CUDA ou OpenCL** – la démo détecte automatiquement le meilleur mode, mais vous devez installer les pilotes.  
- **Une image pour tester** – un PNG ou JPEG net d’un reçu, d’un panneau ou de tout texte imprimé.  

Si l’un de ces éléments vous est inconnu, ne paniquez pas. Les étapes ci‑dessous vous indiqueront les liens de téléchargement exacts et où placer les fichiers.

---

## Étape 1 : Exemple Aspose OCR Java – Configuration du projet

Tout d’abord, créez un nouveau projet Maven (ou un simple dossier si vous préférez `javac`). Ajoutez la dépendance Aspose OCR à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Astuce :** Maven récupérera toutes les dépendances transitives, y compris les bibliothèques de support GPU, vous n’aurez donc pas à chercher des JAR supplémentaires.

Placez votre fichier `Aspose.OCR.Java.lic` à la racine du projet (ou dans tout dossier que vous référencerez plus tard). L’**exemple aspose ocr java** que nous construisons s’attend à ce que le chemin de licence soit `"Aspose.OCR.Java.lic"`.

---

## Étape 2 : Appliquer la licence Aspose OCR

L’étape de licence est cruciale — sans elle, le moteur OCR fonctionne en mode d’évaluation et préfixe la sortie d’un filigrane. Voici le code minimal dont vous avez besoin :

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Exécuter cela une fois au démarrage de votre application garantit que **tous les appels OCR ultérieurs** sont pleinement licenciés.

---

## Étape 3 : Configurer l’accélération GPU – Définir la limite de mémoire GPU

Vient maintenant la partie amusante : indiquer à Aspose d’utiliser le GPU et, éventuellement, **définir une limite de mémoire GPU**. La bibliothèque fournit `GpuEngineOptions`, qui vous permet d’activer le mode GPU, de choisir un dispositif et de plafonner l’utilisation de mémoire. Limiter la mémoire est pratique sur les serveurs partagés où vous ne voulez pas que votre tâche OCR consomme toute la VRAM.

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **Pourquoi définir une limite de mémoire ?** Si vos tâches OCR traitent des images très volumineuses ou que vous exécutez de nombreux jobs simultanément, le GPU peut rapidement manquer de VRAM, entraînant des plantages. En limitant l’allocation, vous maintenez le processus dans des limites sûres et permettez à d’autres charges de travail de coexister paisiblement.

---

## Étape 4 : Extraire du texte d’une image Java – Chargement de l’image

Avec la licence et les paramètres GPU en place, nous pouvons enfin **extraire du texte d’une image Java**. Le fragment suivant crée un `OcrEngine` en utilisant les options GPU, charge un fichier image et lance la reconnaissance.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**Points clés** de cet **exemple aspose ocr java** :

- `OcrInput.add()` accepte plusieurs images ; le moteur les traitera séquentiellement.  
- `ocrResult.getText()` renvoie une chaîne de texte brut, conservant les sauts de ligne mais aucune information de mise en page.  
- L’ensemble du pipeline s’exécute sur le GPU, ce qui peut être **5‑10 × plus rapide** qu’un traitement uniquement CPU pour des images haute résolution.

---

## Étape 5 : Exécuter la démo et vérifier la sortie

Compilez et lancez le programme :

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

Si tout est correctement configuré, vous devriez voir quelque chose comme :

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

Le texte exact dépend de votre image, mais l’essentiel est que la console affiche **le texte reconnu** sans le filigrane « Version d’évaluation ». Si vous rencontrez une erreur `CUDA driver not found`, vérifiez que vos pilotes GPU sont à jour et que le toolkit CUDA se trouve dans le PATH du système.

---

## Problèmes courants & Comment les éviter

| Symptom | Cause probable | Solution |
|---------|----------------|----------|
| `OutOfMemoryError: CUDA out of memory` | Mémoire GPU dépassée | Réduisez `setMemoryLimitMb` (par ex. 1024) ou traitez des morceaux d’image plus petits. |
| `LicenseException` | Fichier de licence manquant ou chemin incorrect | Assurez‑vous que `Aspose.OCR.Java.lic` est accessible et que le chemin correspond. |
| Aucun texte retourné | Image trop floue ou espace colorimétrique inadéquat | Pré‑traitez l’image (augmentez le contraste, convertissez en niveaux de gris) avant l’OCR. |
| GPU non utilisé | `setEnableGpu(false)` ou pilote manquant | Vérifiez `gpuOptions.setEnableGpu(true)` et réinstallez les pilotes GPU. |

---

## Étendre l’exemple

Maintenant que vous avez un **exemple aspose ocr java** solide, vous pourriez vouloir :

- **Traitement par lots d’un dossier** – parcourir les fichiers et stocker les résultats dans une base de données.  
- **Détection de langue** – utiliser `ocrEngine.setLanguage(OcrLanguage.English)` ou ajouter plusieurs langues.  
- **Post‑traitement** – nettoyer la chaîne brute avec des expressions régulières ou l’envoyer à un correcteur orthographique.  

Toutes ces extensions réutilisent le même code de licence et de configuration GPU, vous n’avez donc qu’à ajouter la logique métier.

---

## Conclusion

Vous venez de découvrir un **exemple aspose ocr java** complet qui **extrait du texte d’une image Java** tout en **définissant une limite de mémoire GPU** pour des performances robustes. Les idées principales — licencier tôt, configurer le GPU, fournir l’image, lire le texte—sont réutilisables dans d’innombrables projets, des scanners de reçus aux systèmes d’entrée de formulaires automatisés.

À partir d’ici, n’hésitez pas à expérimenter avec différentes valeurs de `GpuEngineOptions`, à tester des images plus grandes, ou à intégrer l’étape OCR dans un micro‑service Spring Boot. Le ciel est la limite, et grâce à l’accélération GPU, cette limite est bien plus élevée qu’auparavant.

Des questions ou besoin d’aide pour ajuster les paramètres de mémoire selon votre matériel ? Laissez un commentaire ci‑dessous, et bon codage !

---

![Diagramme d’exemple Aspose OCR Java montrant le flux de l’entrée image → OCR accéléré par GPU → sortie texte](https://example.com/images/aspose-ocr-java-example-diagram.png "diagramme d’exemple aspose ocr java")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment définir la licence et vérifier la licence Aspose.OCR en Java](/ocr/english/java/ocr-basics/set-license/)
- [Extraire du texte d’une image Java avec le mode Détection de zones Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convertir une image en texte en Java avec Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}