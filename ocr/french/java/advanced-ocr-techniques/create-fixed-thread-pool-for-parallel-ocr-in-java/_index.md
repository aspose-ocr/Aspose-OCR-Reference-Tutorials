---
category: general
date: 2026-05-03
description: Créez un pool de threads fixe en Java pour extraire rapidement le texte
  des images. Apprenez à exécuter l’OCR, à convertir une image en texte et à améliorer
  les performances grâce au traitement OCR parallèle.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: fr
og_description: Créez un pool de threads fixe en Java pour extraire rapidement du
  texte à partir d'images. Apprenez à exécuter l'OCR, à convertir une image en texte
  et à améliorer les performances grâce au traitement OCR parallèle.
og_title: Créer un pool de threads fixe pour l'OCR parallèle en Java
tags:
- Java
- OCR
- Multithreading
title: Créer un pool de threads fixe pour l’OCR parallèle en Java
url: /fr/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un pool de threads fixe pour l'OCR parallèle en Java

Vous avez déjà eu besoin de **create fixed thread pool** pour accélérer les tâches d'OCR, mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. Dans de nombreux projets très axés sur les images, le goulot d'étranglement est l'appel OCR monothread, et la solution est étonnamment simple : lancer un pool de threads travailleurs et les laisser traiter les fichiers en parallèle.  

Dans ce tutoriel, vous apprendrez comment **extract text from images** avec Aspose OCR, comment **run OCR** efficacement, et comment **convert image to text** sans surcharger votre CPU. À la fin, vous disposerez d'un programme Java prêt à l'emploi qui démontre le **parallel OCR processing** sur une poignée d'images d'exemple.

## Ce que vous allez construire

Nous allons assembler une petite application console qui :

* Lit une liste de chemins d'images (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** dimensionné au nombre de cœurs CPU.
* Envoie une tâche OCR pour chaque image.
* Collecte le texte reconnu et l'affiche dans la console.
* Ferme proprement l'exécuteur.

Pas d'outils de construction externes, pas de frameworks sophistiqués — juste du Java pur et la bibliothèque Aspose OCR. Si vous avez Java 8+ et un IDE décente, vous êtes prêt.

## Prérequis

* **Java Development Kit (JDK) 8 or newer** – le code utilise des lambdas, donc les versions plus anciennes ne compileront pas.
* **Aspose OCR for Java** – téléchargez le JAR depuis le site Aspose ou récupérez-le via Maven (`com.aspose:aspose-ocr`).
* Un dossier contenant quelques images de test (le code pointe vers `YOUR_DIRECTORY`).  
* Une connaissance de base de la concurrence Java (nous expliquerons le reste).

> *Pro tip:* Si vous utilisez Maven, ajoutez la dépendance à votre `pom.xml` et laissez l'IDE gérer le classpath.  

## Étape 1 : Ajouter les imports requis

Tout d'abord, importez les classes dont nous avons besoin. Ce n'est pas seulement du code boilerplate ; chaque import indique à la JVM où trouver le moteur OCR, les utilitaires de gestion d'images, et les outils de concurrence qui nous permettent de **create fixed thread pool**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – l'API OCR principale.  
* `java.util.*` – collections pour stocker les chemins d'images et les résultats.  
* `java.util.concurrent.*` – le package de concurrence qui contient `ExecutorService` et `Future`.

## Étape 2 : Définir les images à traiter

Ensuite, nous listons les fichiers dont nous voulons **extract text from images**. L'utilisation de `Arrays.asList` rend le code concis et nous permet de remplacer par votre propre répertoire sans toucher au reste de la logique.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

N'hésitez pas à ajouter d'autres entrées ; le pool de threads s'adaptera automatiquement en fonction du nombre de cœurs CPU dont vous disposez.

## Étape 3 : **Create Fixed Thread Pool** correspondant aux cœurs CPU

Voici le cœur du tutoriel. Nous interrogeons le runtime pour connaître le nombre de cœurs disponibles et demandons à la fabrique `Executors` de nous fournir un pool exactement de cette taille. Pourquoi fixe ? Parce qu'un nombre prévisible de threads empêche la redoutable « explosion de threads » qui peut priver le système d'exploitation de ressources.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` renvoie le nombre de cœurs logiques (y compris les hyper‑threads).  
* `newFixedThreadPool(coreCount)` garantit que nous ne dépassons jamais la capacité du CPU, ce qui est la façon la plus sûre de **run OCR** en parallèle.

## Étape 4 : Soumettre une tâche OCR pour chaque image

Nous transformons maintenant chaque chemin de fichier en un callable qui **runs OCR**, reconnaît le texte, et renvoie le résultat. Notez que nous créons une nouvelle instance de `OcrEngine` à l'intérieur du lambda — cela évite le partage non sûr de l'état du moteur entre threads.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Chaque appel `submit` transmet le lambda au pool, qui le planifie sur un thread inactif.  
* Les objets `Future<String>` nous permettent de récupérer le texte reconnu plus tard, en préservant l'ordre si nécessaire.

## Étape 5 : Récupérer et afficher le texte reconnu

Une fois toutes les tâches en file d'attente, nous itérons simplement sur la liste `Future`, en appelant `get()` pour bloquer jusqu'à ce que chaque tâche OCR se termine. C'est à ce moment que l'étape **convert image to text** devient visible : l'appel `engine.getText()` renvoie la chaîne brute.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Un exemple de sortie console ressemble à :

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Si un fichier échoue (peut-être parce qu'il est corrompu), vous verrez une ligne qui commence par `Failed:` suivie du chemin — pratique pour un débogage rapide.

## Étape 6 : Nettoyer le service d'exécution

N'oubliez jamais de fermer le pool ; sinon la JVM peut rester en vie, pensant qu'il y a encore du travail à faire. Un arrêt gracieux permet aux tâches en cours de se terminer avant que le processus ne se termine.

```java
executor.shutdown();
```

Vous pouvez également appeler `awaitTermination` si vous devez imposer un délai, mais pour la plupart des utilitaires en ligne de commande, un simple `shutdown()` suffit.

## Exemple complet fonctionnel

Voici le programme complet, prêt à l'exécution. Copiez‑collez‑le dans un fichier nommé `ParallelOcrTutorial.java`, ajustez les chemins d'images, et exécutez `javac` + `java` comme d'habitude.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Résultat attendu :** le contenu textuel de chaque image affiché dans la console, dans le même ordre que la liste `imagePaths`. Si une image ne peut pas être traitée, vous verrez un avis d'échec au lieu d'une ligne vide.

## Questions fréquentes & cas limites

### Et si j'ai plus d'images que de threads ?

Le pool de threads fixe mettra automatiquement en file d'attente les tâches excédentaires. Dès qu'un thread termine son travail OCR actuel, il en prend un autre. Ce comportement de mise en file d'attente est l'essence du **parallel OCR processing** — vous obtenez le débit maximal sans submerger le CPU.

### Puis-je changer la langue ?

Absolument. Remplacez `engine.getLanguage().setEnglish(true);` par le drapeau de langue approprié, par ex., `setFrench(true)` ou activez plusieurs langues en appelant plusieurs setters avant `recognize()`.

### Comment gérer les très grandes images ?

Les gros fichiers peuvent consommer beaucoup de mémoire par thread. Si vous remarquez `OutOfMemoryError`, envisagez de réduire la taille de l'image avant de la transmettre au moteur, ou augmentez la taille du tas avec `-Xmx`. Une autre approche consiste à utiliser un **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}