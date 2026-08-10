---
category: general
date: 2026-02-17
description: Apprenez à utiliser un pool de threads fixe en Java pour extraire du
  texte d'images PNG avec un traitement OCR parallèle et à fermer correctement le
  service d'exécution.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: fr
og_description: Découvrez comment un pool de threads fixe en Java peut extraire du
  texte d'images PNG en parallèle, convertir le texte des pages numérisées et arrêter
  le service d'exécution en toute sécurité.
og_title: pool de threads fixe java – OCR parallèle pour PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Pool de threads fixe Java – OCR parallèle pour PNG
url: /fr/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# pool de threads fixe java – OCR parallèle pour PNG

Vous vous êtes déjà demandé comment accélérer l'OCR sur un lot de fichiers PNG en utilisant un **fixed thread pool java** ? Dans ce tutoriel, nous allons parcourir **extract text from PNG** images en parallèle, **convert scanned pages text** en chaînes éditables, et fermer proprement **shut down executor service** une fois le travail terminé.

Si vous avez déjà fixé du regard une boucle monothread qui traîne pendant des minutes, vous connaissez la frustration d'attendre que chaque page se termine avant que la suivante ne commence. La bonne nouvelle ? Avec quelques lignes de Java et Aspose OCR, vous pouvez libérer la puissance de tous vos cœurs CPU, transformer ces pages numérisées en texte consultable, et garder votre application réactive.

Vous trouverez ci‑dessous un exemple complet, prêt à l'exécution, ainsi que des explications sur l'importance de chaque composant, les pièges courants, et des astuces que vous pouvez appliquer à n'importe quelle bibliothèque OCR.

---

## Ce dont vous avez besoin

- **Java 17** (ou tout JDK récent) – le code utilise la syntaxe moderne `var` avec parcimonie, mais fonctionne également sur les versions plus anciennes.  
- **Aspose.OCR for Java** library – vous pouvez l'obtenir depuis Maven Central ou télécharger une version d'essai depuis Aspose.  
- Un ensemble de fichiers **PNG** que vous souhaitez traiter – pensez aux reçus numérisés, aux pages de livre ou aux captures d'écran.  
- Une connaissance de base de la concurrence Java – pas obligatoire, mais utile.

C’est tout. Aucun service externe, pas de Docker, juste du Java pur et un peu de magie multithreading.

---

## Étape 1 : Ajouter la dépendance Aspose OCR & la licence (facultatif)

Tout d'abord, assurez‑vous que le JAR Aspose OCR se trouve sur votre classpath. Si vous utilisez Maven, ajoutez :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Si vous n’avez pas de licence, la bibliothèque fonctionnera en mode d'évaluation ; le code fonctionne de la même manière. Pour charger une licence (recommandé en production), placez `Aspose.OCR.lic` dans votre dossier resources et utilisez :

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Astuce :** Gardez le fichier de licence en dehors du contrôle de version pour éviter toute exposition accidentelle.

---

## Étape 2 : Créer une instance `OcrEngine` thread‑safe

Le `OcrEngine` d’Aspose OCR est thread‑safe tant que vous réutilisez la même instance entre les tâches. Le créer une seule fois économise de la mémoire et évite le surcoût de réinitialiser le moteur pour chaque image.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Pourquoi réutiliser ? Pensez au moteur comme à un travailleur lourd qui charge les modèles linguistiques en mémoire. Créer un nouveau moteur par image serait comme engager un nouveau spécialiste pour chaque petite tâche – coûteux et inutile.

---

## Étape 3 : Configurer un pool de threads fixe Java

Voici la star du spectacle : un **fixed thread pool java**. Nous le dimensionnerons au nombre de processeurs logiques afin que chaque cœur reçoive du travail sans sur‑souscription.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Utiliser un pool *fixed* (au lieu d’un pool cached) vous offre une utilisation des ressources prévisible et empêche les redoutables pics de « out‑of‑memory » lorsque des centaines d’images arrivent en même temps.

---

## Étape 4 : Lister les fichiers PNG à traiter (Extract Text from PNG)

Rassemblez les chemins vers les images que vous souhaitez OCR. Dans un projet réel, vous pourriez parcourir un répertoire ou lire depuis une base de données ; ici nous coderons en dur quelques exemples.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note :** L'extension de fichier **png** est importante car Aspose OCR détecte automatiquement le format, mais vous pouvez également fournir du JPEG ou du TIFF.

---

## Étape 5 : Soumettre les tâches OCR – Traitement OCR parallèle

Chaque image devient un callable qui renvoie le texte reconnu. Comme le `OcrEngine` est partagé, nous n'avons besoin que de passer le chemin du fichier à la tâche.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Pourquoi l’envelopper dans un `Future` ? Cela nous permet de lancer toutes les tâches immédiatement, puis de récupérer les résultats dans l'ordre de soumission – idéal pour préserver l'ordre des pages lors du **convert scanned pages text** vers un document.

---

## Étape 6 : Récupérer les résultats et les afficher (Convert Scanned Pages Text)

Nous attendons maintenant que chaque `Future` se termine et affichons la sortie. L'appel `get()` bloque uniquement jusqu'à ce que la tâche spécifique se termine, pas tout le pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Un exemple de sortie console ressemble à :

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Si vous préférez écrire les résultats dans des fichiers, remplacez le `System.out.println` par un appel à `Files.writeString`.

---

## Étape 7 : Fermer proprement le service d'exécution

Lorsque chaque tâche est terminée, il est crucial de **shut down executor service** ; sinon votre JVM peut garder des threads non‑daemon actifs, empêchant une sortie propre.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Le pattern `awaitTermination` donne au pool la chance de terminer le travail en cours avant que nous le forçons. Ignorer cette étape est une source fréquente de fuites de mémoire dans les applications de longue durée.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller dans `ParallelBatchDemo.java` et exécuter :

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}