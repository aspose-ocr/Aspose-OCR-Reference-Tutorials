---
category: general
date: 2026-05-25
description: Εξαγωγή κειμένου από εικόνα σε Java χρησιμοποιώντας OCR. Μάθετε πώς να
  φορτώνετε εικόνα για OCR, να αναγνωρίζετε κείμενο από φωτογραφία και να λαμβάνετε
  το κείμενο από το OCR με ένα απλό παράδειγμα κώδικα.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: el
og_description: Εξάγετε κείμενο από εικόνα σε Java με έναν οδηγό βήμα‑βήμα. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να αναγνωρίζετε κείμενο από φωτογραφία και να λαμβάνετε
  κείμενο από OCR αποδοτικά.
og_title: Εξαγωγή κειμένου από εικόνα σε Java – Λήψη κειμένου από OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε Java – Λήψη κειμένου από OCR
url: /el/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε Java – Λήψη Κειμένου από OCR

Κάποτε χρειάστηκε να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερατε ποια βιβλιοθήκη Java να επιλέξετε; Δεν είστε μόνοι. Είτε ψηφιοποιείτε αποδείξεις, εξάγετε σειριακούς αριθμούς από φωτογραφίες προϊόντων, είτε απλώς πειραματίζεστε με ένα διασκεδαστικό side project, η μετατροπή μιας εικόνας σε επεξεργάσιμο κείμενο είναι ένα συχνό εμπόδιο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **φορτώσετε εικόνα για OCR**, να ρυθμίσετε τη μηχανή, και τελικά να **αναγνωρίσετε κείμενο από φωτογραφία** ώστε να **λάβετε κείμενο από OCR** με λίγες μόνο γραμμές κώδικα. Χωρίς ασαφείς αναφορές—όλα όσα χρειάζεστε είναι εδώ.

## Τι Θα Μάθετε

* Πώς να ρυθμίσετε μια ελαφριά μηχανή OCR σε Java.  
* Τα ακριβή βήματα για **φόρτωση εικόνας για OCR** και διαχείριση διαφορετικών διαδρομών αρχείων.  
* Γιατί η ρύθμιση της γλώσσας είναι σημαντική όταν θέλετε να **εξάγετε κείμενο από εικόνα** που δεν είναι στα Αγγλικά.  
* Πώς να εμφανίσετε με ασφάλεια το αποτέλεσμα και τι να κάνετε όταν η μηχανή δεν επιστρέφει τίποτα.  
* Μια χούφτα επαγγελματικών συμβουλών για να αποφύγετε τα πιο κοινά λάθη.

Στο τέλος αυτού του οδηγού θα έχετε ένα αυτόνομο πρόγραμμα που διαβάζει ένα JPEG (ή PNG) που περιέχει ουκρανικούς χαρακτήρες και εκτυπώνει τη αναγνωρισμένη συμβολοσειρά στην κονσόλα. Μπορείτε ελεύθερα να αλλάξετε τη γλώσσα ή την εικόνα—όλα είναι modular.

---

![Διάγραμμα που δείχνει τη ροή εξαγωγής κειμένου από εικόνα χρησιμοποιώντας τη μηχανή OCR Java](/images/extract-text-from-image-java.png)

*Alt text: Διάγραμμα ροής της διαδικασίας εξαγωγής κειμένου από εικόνα σε Java.*

## Προαπαιτούμενα

* **Java Development Kit (JDK) 11+** – ο κώδικας χρησιμοποιεί το σύγχρονο σύστημα modules, αλλά παλαιότερες εκδόσεις λειτουργούν με μικρές προσαρμογές.  
* **Maven ή Gradle** – για να κατεβάσετε τη βιβλιοθήκη OCR (θα χρησιμοποιήσουμε το **Asprise OCR** ως ελαφριά, δωρεάν‑για‑ανάπτυξη επιλογή).  
* Ένα δείγμα αρχείου εικόνας (π.χ., `ukrainian_sign.jpg`) τοποθετημένο κάπου που το πρόγραμμα σας μπορεί να διαβάσει.  
* Βασική εξοικείωση με τη μέθοδο `main` της Java και το χειρισμό εξαιρέσεων.

Αν έχετε όλα αυτά, είστε έτοιμοι. Διαφορετικά, κατεβάστε το JDK από την Oracle ή το AdoptOpenJDK και δημιουργήστε ένα απλό Maven project—δεν χρειάζεται τίποτα περίπλοκο.

---

## Βήμα 1: Προσθήκη της Εξάρτησης OCR

Πρώτα, πείτε στο εργαλείο κατασκευής σας να κατεβάσει τη μηχανή OCR. Για Maven, προσθέστε αυτό στο `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Αυτές οι συντεταγμένες κατεβάζουν ένα συμπαγές JAR που περιλαμβάνει `OcrEngine`, `OcrLanguage` και τις βοηθητικές κλάσεις που θα χρησιμοποιήσουμε. Δεν απαιτούνται επιπλέον native binaries για βασικά Latin και Cyrillic scripts.

---

## Βήμα 2: Δημιουργία Java Κλάσης για **Εξαγωγή Κειμένου από Εικόνα**

Τώρα θα γράψουμε το πραγματικό πρόγραμμα. Αποθηκεύστε το παρακάτω ως `ExtractTextDemo.java` μέσα στο `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Γιατί Λειτουργεί Αυτή η Δομή

* **Ξεχωριστά αριθμημένα μπλοκ** κάνουν τη ροή εύκολη στην παρακολούθηση, ειδικά όταν ψάχνετε πού να **φορτώσετε εικόνα για OCR** ή **αναγνωρίσετε κείμενο από φωτογραφία**.  
* Το `try/catch` γύρω από τη φόρτωση εικόνας και την αναγνώριση εξασφαλίζει ότι το πρόγραμμα αποτυγχάνει με χάρη—χρήσιμο όταν η διαδρομή αρχείου είναι λανθασμένη ή η μηχανή OCR δεν βρίσκει τα δεδομένα γλώσσας.  
* Η προημεροληπτική ρύθμιση της γλώσσας (βήμα 2) βελτιώνει δραστικά την ακρίβεια για μη‑Αγγλικά scripts. Αν αργότερα χρειαστείτε **java image to text** για άλλες γλώσσες, απλώς αντικαταστήστε το `OcrLanguage.UKRAINIAN` με `OcrLanguage.ENGLISH`, `FRENCH`, κ.λπ.

---

## Βήμα 3: Κατασκευή και Εκτέλεση του Προγράμματος

Από τη ρίζα του project, εκτελέστε:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Ή, αν χρησιμοποιείτε Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Υποθέτοντας ότι το `ukrainian_sign.jpg` περιέχει το κείμενο *«Ласкаво просимо»* (ουκρανικά για “Welcome”), θα πρέπει να δείτε κάτι σαν:

```
=== OCR Result ===
Ласкаво просимо
```

Αυτή η έξοδος επιβεβαιώνει ότι έχετε **εξάγει κείμενο από εικόνα** και **λάβετε κείμενο από OCR** σε μία μόνο εκτέλεση.

---

## Βήμα 4: Προσαρμογή της Ροής Εργασίας – Από **Java Image to Text** σε Πραγματικά Έργα

Αν και η demo είναι ελάχιστη, οι πραγματικές εφαρμογές συχνά χρειάζονται λίγο παραπάνω:

| Σενάριο | Τι Να Προσαρμόσετε | Λόγος |
|----------|----------------|--------|
| **Επεξεργασία παρτίδας** | Επανάληψη πάνω σε `List<Path>` και αποθήκευση κάθε αποτελέσματος σε βάση δεδομένων. | Μειώνει την χειροκίνητη εργασία όταν έχετε εκατοντάδες φωτογραφίες. |
| **Διαφορετικές μορφές εικόνας** | Χρησιμοποιήστε `ImageIO.read(new File(path))` για προεπεξεργασία, έπειτα περάστε το `BufferedImage` στο `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Διαχειρίζεται PNG, BMP ή ακόμη και PDF μετά από μετατροπή. |
| **Βελτιστοποίηση απόδοσης** | Καλέστε `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` αν δεχτείτε ελαφρώς χαμηλότερη ακρίβεια. | Επιταχύνει την αναγνώριση σε χαμηλής ισχύος υλικό. |
| **Μετα-επεξεργασία** | Αφαιρέστε κενά, αντικαταστήστε συνηθισμένα λάθη OCR (`0` → `O`, `1` → `I`). | Βελτιώνει την ποιότητα των δεδομένων για επόμενα βήματα. |

Αυτές οι παραλλαγές διατηρούν την κεντρική ιδέα—**αναγνωρίστε κείμενο από φωτογραφία**—ενώ σας δίνουν ευελιξία για παραγωγικές εργασίες.

---

## Συνηθισμένα Πίνακες & Pro Tips

1. **Λάθος ρύθμιση γλώσσας** – Αν παραλείψετε το βήμα 2, η μηχανή προεπιλέγει τα Αγγλικά, μετατρέποντας τους Κυριλλικούς χαρακτήρες σε ακατανόητο κείμενο. Ελέγξτε πάντα τον κωδικό γλώσσας.  
2. **Η ποιότητα της εικόνας μετρά** – Φωτογραφίες χαμηλής ανάλυσης ή θολές μειώνουν την ακρίβεια. Προεπεξεργαστείτε με ενίσχυση αντίθεσης ή δυαδικοποίηση αν χρειάζεται.  
3. **Προβλήματα διαδρομής αρχείου** – Σε Windows, τα backslashes χρειάζονται escaping (`C:\\images\\file.jpg`). Η χρήση `Path.of(...)` από το `java.nio.file` αποφεύγει αυτό το πρόβλημα.  
4. **Διαρροές μνήμης** – Το `OcrEngine` κρατά native πόρους. Καλέστε `ocrEngine.dispose()` όταν τελειώσετε, ειδικά σε υπηρεσίες που τρέχουν συνεχώς.  
5. **Ασφάλεια νήματος** – Η μηχανή δεν είναι thread‑safe από προεπιλογή. Δημιουργήστε ξεχωριστό instance ανά νήμα ή συγχρονίστε την πρόσβαση.

---

## Πλήρες Παράδειγμα (All‑In‑One)

Παρακάτω υπάρχει ένα μοναδικό αρχείο που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε οποιοδήποτε IDE. Περιλαμβάνει την κλήση `dispose()` και μια μικρή βοηθητική μέθοδο για πιο καθαρό κώδικα.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει την ίδια έξοδο στην κονσόλα όπως προηγουμένως. Μπορείτε ελεύθερα να αντικαταστήσετε το `OcrLanguage.UKRAINIAN` με `OcrLanguage.ENGLISH` ή οποιαδήποτε άλλη υποστηριζόμενη γλώσσα για να δείτε πώς προσαρμόζεται η μηχανή.

---

## Συμπέρασμα

Περπατήσαμε από όλα όσα χρειάζεστε για **εξαγωγή κειμένου από εικόνα** χρησιμοποιώντας Java: από την προσθήκη της εξάρτησης OCR, μέχρι το **φόρτωση εικόνας για OCR**,


## Σχετικά Tutorials

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}