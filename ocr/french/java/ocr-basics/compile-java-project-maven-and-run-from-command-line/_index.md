---
category: general
date: 2026-10-18
description: Compilez le projet Java Maven et exécutez‑le depuis la ligne de commande
  en utilisant les commandes Maven clean, compile et exec. Apprenez à construire et
  à exécuter une application Java efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: fr
lastmod: 2026-10-18
og_description: Compilez un projet Java avec Maven et exécutez‑le depuis la ligne
  de commande grâce à un guide étape par étape. Maîtrisez les commandes Maven clean,
  compile et run pour construire et lancer une application Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Compiler un projet Java Maven – exécuter depuis la ligne de commande
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: Compiler un projet Java Maven et l'exécuter depuis la ligne de commande
url: /fr/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compiler un projet Java Maven et l'exécuter depuis la ligne de commande

Si vous devez **compile java project maven** et lancer la classe résultante directement depuis un terminal, ce guide vous montre exactement comment faire. À la fin du tutoriel, vous pourrez nettoyer les anciens artefacts, compiler le code source et **execute java class command line** en utilisant une chaîne de commandes Maven unique.

Le tutoriel couvre tout ce que vous devez savoir pour **build and run java app** avec Maven, y compris les plugins requis, les pièges courants et les astuces pour les shells sous Windows‑ et Unix‑based shells. Aucune documentation externe n'est nécessaire — il suffit de suivre les étapes ci‑dessous.

## Prérequis

* Java Development Kit (JDK) 8 ou version plus récente installé et `JAVA_HOME` défini.  
* Apache Maven 3.6+ disponible dans votre `PATH`.  
* Un projet Maven contenant un `pom.xml` et une classe Java avec une méthode `public static void main(String[] args)` (pour cet exemple, la classe est `com.aspose.ocr.examples.SimpleOcrDemo`).

## Compiler un projet Java Maven

La première étape consiste à supprimer toutes les classes précédemment compilées ainsi que les autres artefacts de construction. Exécuter `mvn clean` garantit un démarrage propre et empêche le bytecode obsolète de provoquer des erreurs d'exécution.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Pourquoi nettoyer ?* Maven stocke les classes compilées dans `target/`. Si vous sautez la phase de nettoyage, d'anciennes fichiers `.class` peuvent rester et masquer des problèmes de compilation, notamment après un refactoring des noms de paquets.

## Exécuter une classe Java en ligne de commande

Après le nettoyage, compilez les fichiers sources. La phase `compile` de Maven traduit toutes les sources `src/main/java` en bytecode et place les résultats dans `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Vous avez maintenant une sortie **maven compile source code** prête à l'exécution. La commande suivante exécute la classe compilée sans nécessiter de JAR séparé.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

L'objectif `exec:java` du plugin **maven clean compile run** lance la classe spécifiée directement depuis le répertoire de sortie compilé. C'est la façon la plus rapide d'**execute java class command line** pendant le développement.

### Sortie attendue

Lorsque la démo s'exécute avec succès, vous devriez voir quelque chose de similaire à :

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Si vous recevez une `ClassNotFoundException`, vérifiez à nouveau le nom complet de la classe et assurez‑vous qu'elle se trouve sous `src/main/java`.

## Flux de travail Maven clean compile run

Assembler les trois commandes ensemble donne un flux de travail compact et répétable :

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Pourquoi les chaîner ?* Combiner les phases élimine le besoin d'appuyer trois fois sur **Enter** et réduit le risque d'oublier une étape. Maven exécutera les phases dans l'ordre où elles apparaissent, garantissant une construction propre avant l'exécution.

### Astuces pour un flux de travail plus fluide

| Astuce | Description |
|-----|-------------|
| **Utiliser un profil** | Définissez un profil Maven qui regroupe `clean`, `compile` et `exec:java` afin de pouvoir exécuter `mvn demo` au lieu de taper toute la chaîne. |
| **Ajouter des options JVM** | Passez `-Dexec.args="-Xmx512m"` pour augmenter la taille du tas pour les applications gourmandes en mémoire. |
| **Cross‑platform** | Sous Windows utilisez `mvn.cmd` tandis que les shells Unix utilisent `mvn`. La même commande fonctionne dans les deux environnements. |

## Construire et exécuter une application Java avec Maven

Si vous préférez un artefact distribuable, vous pouvez laisser Maven empaqueter vos classes compilées dans un JAR exécutable puis l'exécuter avec la commande standard `java -jar` :

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Cette approche est utile lorsque vous devez **build and run java app** sur un serveur où Maven n’est pas installé. Cependant, pour un développement rapide, la séquence **maven clean compile run** est plus rapide car elle saute l'étape d'empaquetage.

## Maven compile source code – pièges courants

Même si les commandes sont simples, les développeurs rencontrent souvent les problèmes suivants :

1. **Missing `exec-maven-plugin`**  
   Si Maven ne trouve pas l'objectif `exec:java`, ajoutez le plugin à votre `pom.xml` :

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Incorrect classpath**  
   Maven compile vers `target/classes`. Si vous déplacez manuellement des fichiers ou modifiez le répertoire de sortie par défaut, l'objectif `exec:java` peut ne pas localiser votre classe. Conservez la disposition par défaut sauf si vous avez une raison précise de la changer.

3. **Using the wrong JDK version**  
   Maven hérite du JDK depuis `JAVA_HOME`. Compiler du code source avec JDK 11 tout en exécutant sur JDK 8 provoquera une `UnsupportedClassVersionError`. Vérifiez la version du JDK avec `java -version` et `mvn -v`.

4. **Shell quoting problems**  
   Sous Unix, encadrez la valeur `-Dexec.mainClass` entre guillemets simples si elle contient des caractères spéciaux :  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Sous Windows, les guillemets doubles fonctionnent correctement.

En abordant ces points, vous pouvez de manière fiable **execute java class command line** dans n'importe quel environnement.

## Astuce pro : automatiser avec un script

Pour les équipes qui reconstruisent fréquemment la démo, créez un petit script shell ou batch :

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Rendez‑le exécutable (`chmod +x run-demo.sh`) et lancez `./run-demo.sh`. Cela élimine les erreurs de frappe et garantit que chaque développeur suit exactement la séquence **maven clean compile run**.

## Conclusion

Vous savez maintenant comment **compile java project maven** et **execute java class command line** instantanément en utilisant les objectifs clean, compile et exec de Maven. Le flux de travail étape par étape garantit une construction propre, élimine les artefacts obsolètes et vous permet de **build and run java app** avec une seule ligne de commande.  

Ensuite, vous pourriez explorer :

* Ajouter le **shade plugin** pour produire un uber‑JAR pour le déploiement.  
* Configurer des profils Maven pour différents environnements (dev, test, prod).  
* Intégrer les tests unitaires avec `mvn test` avant l'étape de compilation.

Expérimentez ces variantes pour adapter le flux de travail à vos propres projets, et vous disposerez d'un pipeline de construction robuste et répétable qui fonctionne sous Windows, macOS et Linux. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}