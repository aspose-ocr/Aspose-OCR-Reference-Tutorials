---
category: general
date: 2026-10-18
description: Συγκομποιήστε ένα έργο Java με Maven και εκτελέστε το από τη γραμμή εντολών
  χρησιμοποιώντας τις εντολές Maven clean, compile και exec. Μάθετε πώς να δημιουργείτε
  και να εκτελείτε μια εφαρμογή Java αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: el
lastmod: 2026-10-18
og_description: Μεταγλωττίστε ένα έργο Java με Maven και εκτελέστε το από τη γραμμή
  εντολών με έναν οδηγό βήμα‑βήμα. Κατακτήστε τις εντολές Maven clean, compile, run
  για να χτίσετε και να τρέξετε μια εφαρμογή Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Μεταγλώττιση έργου Java Maven – εκτέλεση από τη γραμμή εντολών
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
title: Μεταγλώττιση έργου Java με Maven και εκτέλεση από τη γραμμή εντολών
url: /el/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Συγγραφή java project maven και εκτέλεση από τη γραμμή εντολών

Αν χρειάζεστε να **compile java project maven** και να εκκινήσετε την προκύπτουσα κλάση απευθείας από ένα τερματικό, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Στο τέλος του tutorial θα μπορείτε να καθαρίσετε τα παλιά artifacts, να compile τον πηγαίο κώδικα, και να **execute java class command line** χρησιμοποιώντας μια ενιαία αλυσίδα εντολών Maven.

Ο οδηγός καλύπτει όλα όσα χρειάζεστε για να **build and run java app** με Maven, συμπεριλαμβανομένων των απαιτούμενων plugins, κοινών παγίδων και συμβουλών για shells Windows‑ και Unix‑based. Δεν απαιτείται εξωτερική τεκμηρίωση—απλώς ακολουθήστε τα παρακάτω βήματα.

## Προαπαιτούμενα

* Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο και ορισμένο `JAVA_HOME`.
* Apache Maven 3.6+ διαθέσιμο στο `PATH` σας.
* Ένα Maven project που περιέχει ένα `pom.xml` και μια Java κλάση με μέθοδο `public static void main(String[] args)` (για αυτό το παράδειγμα η κλάση είναι `com.aspose.ocr.examples.SimpleOcrDemo`).

## Συγγραφή java project maven

Το πρώτο βήμα είναι η αφαίρεση τυχόν προηγουμένως compiled κλάσεων και άλλων build artifacts. Η εκτέλεση του `mvn clean` εγγυάται μια φρέσκια εκκίνηση και αποτρέπει το παλιό bytecode από το να προκαλέσει σφάλματα χρόνου εκτέλεσης.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Γιατί clean;* Το Maven αποθηκεύει τις compiled κλάσεις στο `target/`. Αν παραλείψετε το στάδιο clean, παλιά αρχεία `.class` μπορεί να παραμείνουν και να κρύψουν προβλήματα compilation, ειδικά μετά από refactoring των ονομάτων πακέτων.

## Εκτέλεση java class command line

Μετά το cleaning, compile τα αρχεία πηγαίου κώδικα. Η φάση `compile` του Maven μετατρέπει όλα τα αρχεία `src/main/java` σε bytecode και τοποθετεί τα αποτελέσματα στο `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Τώρα έχετε ένα **maven compile source code** output έτοιμο για εκτέλεση. Η επόμενη εντολή εκτελεί την compiled κλάση χωρίς να χρειάζεται ξεχωριστό JAR.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Ο στόχος `exec:java` του plugin **maven clean compile run** εκκινεί την καθορισμένη κλάση απευθείας από τον κατάλογο εξόδου compiled. Αυτός είναι ο πιο γρήγορος τρόπος για **execute java class command line** κατά την ανάπτυξη.

### Αναμενόμενη έξοδος

Όταν το demo εκτελεστεί επιτυχώς, θα πρέπει να δείτε κάτι παρόμοιο με:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Αν λάβετε ένα `ClassNotFoundException`, ελέγξτε ξανά το πλήρως προσδιορισμένο όνομα κλάσης και βεβαιωθείτε ότι βρίσκεται κάτω από `src/main/java`.

## Ροή εργασίας Maven clean compile run

Συνδυάζοντας τις τρεις εντολές μαζί δημιουργείται μια συμπαγής, επαναλαμβανόμενη ροή εργασίας:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Γιατί να τις συνδέσετε;* Ο συνδυασμός των φάσεων εξαλείφει την ανάγκη να πατήσετε **Enter** τρεις φορές και μειώνει την πιθανότητα να ξεχάσετε ένα βήμα. Το Maven θα εκτελέσει τις φάσεις με τη σειρά που εμφανίζονται, εγγυώμενο ένα clean build πριν από την εκτέλεση.

### Συμβουλές για πιο ομαλή ροή εργασίας

| Συμβουλή | Περιγραφή |
|-----|-------------|
| **Χρήση προφίλ** | Ορίστε ένα Maven profile που συνδυάζει τα `clean`, `compile` και `exec:java` ώστε να μπορείτε να εκτελείτε `mvn demo` αντί να πληκτρολογείτε ολόκληρη την αλυσίδα. |
| **Προσθήκη επιλογών JVM** | Προσθέστε `-Dexec.args="-Xmx512m"` για να αυξήσετε το μέγεθος heap για εφαρμογές που απαιτούν πολύ μνήμη. |
| **Δια‑πλατφόρμα** | Σε Windows χρησιμοποιήστε `mvn.cmd` ενώ σε Unix shells χρησιμοποιήστε `mvn`. Η ίδια εντολή λειτουργεί και στα δύο περιβάλλοντα. |

## Δημιουργία και εκτέλεση java app με Maven

Αν προτιμάτε ένα διανέμετο artifact, μπορείτε να αφήσετε το Maven να πακετάρει τις compiled κλάσεις σας σε ένα εκτελέσιμο JAR και στη συνέχεια να το εκτελέσετε με την τυπική εντολή `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Αυτή η προσέγγιση είναι χρήσιμη όταν χρειάζεται να **build and run java app** σε έναν διακομιστή όπου το Maven δεν είναι εγκατεστημένο. Ωστόσο, για γρήγορη ανάπτυξη η ακολουθία **maven clean compile run** είναι πιο γρήγορη επειδή παραλείπει το βήμα πακετάρισματος.

## Maven compile source code – κοινές παγίδες

Αν και οι εντολές είναι απλές, οι προγραμματιστές συχνά αντιμετωπίζουν τα παρακάτω ζητήματα:

1. **Λείπει το `exec-maven-plugin`**  
   Αν το Maven δεν μπορεί να βρει τον στόχο `exec:java`, προσθέστε το plugin στο `pom.xml` σας:

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

2. **Λανθασμένο classpath**  
   Το Maven compile στο `target/classes`. Αν μετακινήσετε χειροκίνητα αρχεία ή αλλάξετε τον προεπιλεγμένο κατάλογο εξόδου, ο στόχος `exec:java` μπορεί να μην εντοπίσει την κλάση σας. Διατηρήστε την προεπιλεγμένη δομή εκτός αν έχετε συγκεκριμένο λόγο να την αλλάξετε.

3. **Χρήση λανθασμένης έκδοσης JDK**  
   Το Maven κληρονομεί το JDK από το `JAVA_HOME`. Η compilation με κώδικα πηγαίου JDK 11 ενώ εκτελείται σε JDK 8 θα προκαλέσει `UnsupportedClassVersionError`. Επαληθεύστε την έκδοση του JDK με `java -version` και `mvn -v`.

4. **Προβλήματα παραθέσεων σε Shell**  
   Σε Unix, τυλίξτε την τιμή `-Dexec.mainClass` σε μονά εισαγωγικά αν περιέχει ειδικούς χαρακτήρες:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Σε Windows, τα διπλά εισαγωγικά λειτουργούν κανονικά.

Αν αντιμετωπίσετε αυτά τα σημεία, μπορείτε αξιόπιστα να **execute java class command line** σε οποιοδήποτε περιβάλλον.

## Συμβουλή επαγγελματία: αυτοματοποίηση με script

Για ομάδες που επαναδημιουργούν συχνά το demo, δημιουργήστε ένα μικρό script shell ή batch:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Κάντε το εκτελέσιμο (`chmod +x run-demo.sh`) και εκτελέστε `./run-demo.sh`. Αυτό εξαλείφει τα σφάλματα πληκτρολόγησης και διασφαλίζει ότι κάθε προγραμματιστής ακολουθεί την ακριβή ακολουθία **maven clean compile run**.

## Συμπέρασμα

Τώρα ξέρετε πώς να **compile java project maven** και άμεσα να **execute java class command line** χρησιμοποιώντας τις στόχους clean, compile και exec του Maven. Η βήμα‑βήμα ροή εργασίας εγγυάται ένα φρέσκο build, εξαλείφει τα παλιά artifacts, και σας επιτρέπει να **build and run java app** με μια μόνο γραμμή εντολών.  

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Προσθήκη του **shade plugin** για τη δημιουργία ενός uber‑JAR για ανάπτυξη.  
* Διαμόρφωση Maven profiles για διαφορετικά περιβάλλοντα (dev, test, prod).  
* Ενσωμάτωση μονάδων ελέγχου με `mvn test` πριν το βήμα compile.

Δοκιμάστε αυτές τις παραλλαγές για να προσαρμόσετε τη ροή εργασίας στα δικά σας έργα, και θα έχετε μια αξιόπιστη, επαναλαμβανόμενη αλυσίδα build που λειτουργεί σε Windows, macOS και Linux. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε OCR σε Java – Πλήρης οδηγός βήμα‑βήμα](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Εκτέλεση OCR σε εικόνα με Java – Πλήρης οδηγός Aspose OCR](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Πώς να εκτελέσετε OCR με Aspose OCR σε Java – Οδηγός βήμα‑βήμα](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}