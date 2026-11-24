---
category: general
date: 2026-07-05
description: Μαθήματα OCR για πολλαπλές γλώσσες για προγραμματιστές Java. Μάθετε πώς
  να εξάγετε κείμενο OCR από εικόνες σε έργα Java με ένα παράδειγμα OCR πολλαπλών
  γλωσσών.
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: el
og_description: Αναλυτική εξήγηση του OCR πολλαπλών γλωσσών σε Java. Λάβετε κείμενο
  OCR από εικόνες χρησιμοποιώντας ένα παράδειγμα OCR πολλαπλών γλωσσών που μπορείτε
  να αντιγράψετε‑και‑επικολλήσετε σήμερα.
og_title: OCR πολλαπλών γλωσσών σε Java – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: OCR πολλαπλών γλωσσών σε Java – Πλήρης οδηγός βήμα‑βήμα
url: /el/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Μικτής Γλώσσας σε Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε ποτέ χρειαστεί **mixed language OCR** αλλά δεν ήξερες πώς να το υλοποιήσεις σε Java; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε παλιά έγγραφα που εναλλάσσονται μεταξύ Αγγλικών και Malayalam, είτε δημιουργείτε μια εφαρμογή σαρωτή που υποστηρίζει πολλές γραφές, η πρόκληση είναι πραγματική. Σε αυτό το tutorial θα σας δείξουμε ακριβώς πώς να **get OCR text** από ένα bitmap που περιέχει και τις δύο γλώσσες, χρησιμοποιώντας μια σύντομη ροή εργασίας **image to text Java**.

Θα περάσουμε από ένα έτοιμο‑για‑εκτέλεση **java OCR example**, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική και θα καλύψουμε τις ιδιαιτερότητες του **multi language OCR** ώστε να αποφύγετε τα συνηθισμένα προβλήματα. Στο τέλος θα έχετε ένα λειτουργικό πρόγραμμα που εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα – χωρίς ανεξήγητες βιβλιοθήκες.

## Τι Θα Χρειαστεί

* **Java Development Kit (JDK) 17** ή νεότερο – ο κώδικας χρησιμοποιεί το σύγχρονο σύστημα μονάδων αλλά λειτουργεί και σε JDK 11+.
* **Maven** (ή Gradle) – για αυτόματη λήψη της βιβλιοθήκης OCR.
* Μια μηχανή OCR που υποστηρίζει πολλές γλώσσες – για αυτόν τον οδηγό θα χρησιμοποιήσουμε **Aspose.OCR for Java**, που προσφέρει έτοιμη υποστήριξη για Αγγλικά και Malayalam. (Αν προτιμάτε το Tesseract, τα βήματα είναι παρόμοια· απλώς αλλάξτε τις δηλώσεις import.)
* Μια δείγμα εικόνας με όνομα `mixed_english_malayalam.png` τοποθετημένη σε φάκελο που ονομάζεται `resources` μέσα στο project σας.
* Μια μέτρια δόση περιέργειας – το υπόλοιπο καλύπτεται παρακάτω.

> **Pro tip:** Αν βρίσκεστε σε Windows, εκτελέστε `mvn -v` από ένα Command Prompt για να επαληθεύσετε ότι το Maven είναι στο PATH σας.

## Ρύθμιση του Έργου

### 1. Δημιουργία Maven Project

Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

### 2. Προσθήκη της Εξάρτησης Aspose.OCR

Επεξεργαστείτε το παραγόμενο `pom.xml` και εισάγετε το παρακάτω μέσα στο μπλοκ `<dependencies>`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

Εκτελέστε `mvn clean install` για να κατεβάσετε τα JARs. Το Maven θα διαχειριστεί τα πάντα, έτσι δεν θα χρειαστεί να ψάχνετε για native DLLs.

## Γραφή του Κώδικα Mixed Language OCR

Δημιουργήστε μια νέα κλάση `MixedLanguageOcrDemo.java` στο `src/main/java/com/example/ocr/` και επικολλήστε τον πλήρη κώδικα παρακάτω. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε **γιατί** κάνουμε ό,τι κάνουμε.

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### Πώς Λειτουργεί

| Βήμα | Τι Συμβαίνει | Γιατί Είναι Σημαντικό |
|------|--------------|------------------------|
| **1** | Δημιουργείται το αντικείμενο `OcrEngine`. | Η μηχανή περιλαμβάνει όλη τη λειτουργικότητα OCR· χωρίς αυτή δεν μπορείτε να καλέσετε καμία μέθοδο. |
| **2** | Η μέθοδος `setRecognitionLanguage` λαμβάνει `ENGLISH` και `MALAYALAM`. | Η παροχή και των δύο γλωσσών ενεργοποιεί **multi language OCR**· η μηχανή θα ανιχνεύσει αλλαγές γραφής σε πραγματικό χρόνο. |
| **3** | Ορίζεται η διαδρομή της εικόνας. | Η διατήρηση της διαδρομής σχετικής αποφεύγει την σκληρή κωδικοποίηση απόλυτων τοποθεσιών, κάνοντας το **java OCR example** επαναχρησιμοποιήσιμο. |
| **4** | Η `recognizeImage` επεξεργάζεται το bitmap. | Εδώ γίνεται η βαριά δουλειά – η μηχανή αναλύει τα pixel, τρέχει νευρωνικά δίκτυα και επιστρέφει ένα `RecognitionResult`. |
| **5** | Η `getText()` εξάγει το απλό κείμενο. | Αυτή είναι η ακριβής μέθοδος που χρειάζεστε για **get OCR text** για περαιτέρω επεξεργασία (π.χ., αποθήκευση σε DB). |
| **6** | Η `System.out.println` εκτυπώνει το κείμενο. | Η άμεση οπτική ανατροφοδότηση σας βοηθά να επαληθεύσετε ότι η ροή **image to text Java** λειτουργεί. |

> **Note:** Αν αντιμετωπίσετε `java.lang.UnsatisfiedLinkError`, βεβαιωθείτε ότι ο φάκελος της native βιβλιοθήκης βρίσκεται στο `java.library.path`. Η Aspose παρέχει τα απαιτούμενα binaries για Windows, macOS και Linux.

## Εκτέλεση του Demo

Συγκεντρώστε και εκτελέστε με Maven:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

Θα πρέπει να δείτε έξοδο παρόμοια με:

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

Η πρώτη γραμμή είναι Αγγλικά, η δεύτερη γραμμή είναι Malayalam – απόδειξη ότι το **mixed language OCR** μας πέτυχε.

## Διαχείριση Συνηθισμένων Edge Cases

### Εικόνες Χαμηλής Ποιότητας

Αν η εικόνα είναι θολή ή έχει χαμηλή αντίθεση, η ακρίβεια του OCR μειώνεται δραματικά. Σκεφτείτε αυτές τις λύσεις:

* **Pre‑process** την εικόνα με βιβλιοθήκη όπως το OpenCV – μετατρέψτε σε grayscale, εφαρμόστε adaptive thresholding και αυξήστε την ανάλυση τουλάχιστον στα 300 DPI.  
* Ενεργοποιήστε `ocrEngine.setAutoSkewCorrection(true)` για να αφήσετε τη μηχανή να ευθυγραμμίσει το περιστρεφόμενο κείμενο.  
* Αυξήστε το `ocrEngine.setConfidenceThreshold(0.6f)` αν χρειάζεστε πιο αυστηρό φιλτράρισμα εμπιστοσύνης.

### Μη Υποστηριζόμενες Γλώσσες

Η Aspose υποστηρίζει επί του παρόντος πάνω από 70 γραφές, αλλά το Malayalam μπορεί να απαιτεί πακέτο γλώσσας. Αν η `RecognitionLanguage.MALAYALAM` ρίξει εξαίρεση, κατεβάστε τα πρόσθετα δεδομένα γλώσσας από το portal της Aspose και τοποθετήστε τα στο `resources/ocr-data`.

### Μεγάλα PDFs

Κατά την επεξεργασία PDF πολλαπλών σελίδων, δώστε κάθε σελίδα ως ξεχωριστή εικόνα ή χρησιμοποιήστε `OcrEngine.recognizePdf`. Η ίδια κλήση `setRecognitionLanguage` εφαρμόζεται σε κάθε σελίδα, προσφέροντάς σας μια αδιάσπαστη εμπειρία **multi language OCR** σε ολόκληρο το έγγραφο.

## Επέκταση του Παραδείγματος: Από την Κονσόλα σε Web Service

Αν θέλετε να εκθέσετε αυτή τη λειτουργικότητα μέσω ενός REST endpoint, προσθέστε Spring Boot:

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

Τώρα οποιοσδήποτε πελάτης μπορεί να `POST` μια εικόνα και να λάβει το αποτέλεσμα **get OCR text** ως απλό JSON. Αυτή η μικρή επέκταση δείχνει πώς το ίδιο **java OCR example** κλιμακώνεται από ένα demo ενός αρχείου σε μια υπηρεσία έτοιμη για παραγωγή.

## Στιγμιότυπο Πλήρους Δένδρου Πηγής

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

Η παρουσίαση ολόκληρης της δομής του έργου στο άρθρο διευκολύνει τους αναγνώστες να αντιγράψουν τη δομή στο IDE τους και να το εκτελέσουν αμέσως.

![Αποτέλεσμα παραδείγματος mixed language OCR](https://example.com/assets/mixed-ocr-output.png "Αποτέλεσμα παραδείγματος mixed language OCR")

*Κείμενο alt εικόνας:* mixed language OCR example output – δείχνει κείμενο στα Αγγλικά και Malayalam που εξήχθη από την ίδια εικόνα.

## Συνοπτική Επισκόπηση & Επόμενα Βήματα

Καλύψαμε μια **mixed language OCR** ροή εργασίας σε Java από την αρχή μέχρι το τέλος:

* Ρυθμίσατε ένα Maven project και προσθέσατε την εξάρτηση Aspose OCR.  
* Διαμορφώσατε τη μηχανή για Αγγλικά + Malayalam, πραγματοποιήσατε αναγνώριση και **got OCR text**.  
* Συζητήσατε την ποιότητα της εικόνας, τα πακέτα γλωσσών και πώς να μετατρέψετε την εφαρμογή κονσόλας σε web service.

Αν είστε έτοιμοι να προχωρήσετε παραπέρα, δοκιμάστε αυτές τις ιδέες:

* Αντικαταστήστε την Aspose με **Tesseract** για να δείτε πώς μια ανοιχτού κώδικα μηχανή διαχειρίζεται **multi language OCR**.  
* Πειραματιστείτε με επιπλέον γλώσσες όπως Hindi ή Tamil – απλώς προσθέστε τις στο `setRecognitionLanguage`.  
* Ενσωματώστε το αποτέλεσμα με έναν δείκτη αναζήτησης (π.χ., Elasticsearch) για να ενεργοποιήσετε αναζήτηση **image to text Java** σε σαρωμένα αρχεία.

Μη διστάσετε να αφήσετε ένα σχόλιο αν κάτι δεν λειτούργησε όπως αναμενόταν, ή να μοιραστείτε τις δικές σας προσαρμογές. Καλή προγραμματιστική, και εύχομαι οι σαρώσεις σας να είναι πάντα κρυστάλλινες!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνες – Βασικά OCR με Aspose.OCR για Java](/ocr/english/java/ocr-basics/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}