---
category: general
date: 2026-09-28
description: Μάθετε πώς να OCR εικόνα σε κείμενο σε Java χρησιμοποιώντας Aspose OCR,
  συμπεριλαμβανομένης της φόρτωσης εικόνων, ενεργοποίησης spell correction, και μετατροπής
  χειρόγραφων σημειώσεων σε καθαρά, αναζητήσιμα strings.
draft: false
keywords:
- ocr image to text
- handwriting recognition java
- convert handwritten image text
- extract text handwritten image
- ocr with spell correction
- aspose ocr java tutorial
lastmod: 2026-09-28
og_description: Ανακαλύψτε πώς να OCR εικόνα σε κείμενο σε Java με Aspise OCR. Αυτός
  ο οδηγός βήμα‑βήμα δείχνει τη φόρτωση εικόνων, την ενεργοποίηση spell correction,
  και τη μετατροπή χειρόγραφων σημειώσεων σε καθαρό κείμενο.
og_image_alt: Screenshot of Java code converting handwritten image to searchable text
  using Aspose OCR
og_title: Πώς να OCR εικόνα σε κείμενο σε Java με χειρόγραφες σημειώσεις
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to OCR image to text in Java using Aspose OCR, including
    loading images, enabling spell correction, and converting handwritten notes into
    clean searchable strings.
  headline: How to OCR image to text in Java with handwritten notes
  type: TechArticle
- description: Learn how to OCR image to text in Java using Aspose OCR, including
    loading images, enabling spell correction, and converting handwritten notes into
    clean searchable strings.
  name: How to OCR image to text in Java with handwritten notes
  steps:
  - name: '**Resolution matters** – Aim for at least **300 dpi**. Lower resolutions
      cause the engine to miss tiny strokes.'
    text: '**Resolution matters** – Aim for at least **300 dpi**. Lower resolutions
      cause the engine to miss tiny strokes.'
  - name: '**Contrast is king** – If the background is colored, convert the image
      to grayscale first.'
    text: '**Contrast is king** – If the background is colored, convert the image
      to grayscale first.'
  - name: '**Crop to content** – Removing unnecessary margins reduces noise and speeds
      up processing.'
    text: '**Crop to content** – Removing unnecessary margins reduces noise and speeds
      up processing.'
  type: HowTo
- questions:
  - answer: Yes, a valid Aspose OCR license is required for production use; a free
      trial is available for evaluation.
    question: Can I use this in a commercial application?
  - answer: Absolutely. Aspose OCR supports **30+ languages**, including Spanish,
      French, German, and Chinese.
    question: Does the engine support languages other than English?
  - answer: Enabling spell correction adds roughly **10 %** overhead, but the trade‑off
      is usually worth the increase in accuracy.
    question: How does spell correction affect performance?
  - answer: PNG, JPEG, BMP, TIFF, and GIF are all supported out of the box.
    question: What image formats are accepted?
  - answer: 'Wrap the OCR steps in a `for (File file : folder.listFiles())` loop,
      reusing the same `OcrEngine` instance and adjusting the image stream for each
      file.'
    question: How can I process a folder of images automatically?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Handwriting
title: Πώς να OCR εικόνα σε κείμενο σε Java με χειρόγραφες σημειώσεις
url: /el/java/advanced-ocr-techniques/how-to-ocr-image-in-java-handwritten-notes-with-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR εικόνας σε κείμενο σε Java με χειρόγραφες σημειώσεις

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR εικόνας σε κείμενο** όταν η πηγή είναι μια γραπτή λίστα αγορών ή ένα σκίτσο σημειώσεων συνάντησης; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές, οι προγραμματιστές χρειάζεται να διαβάζουν χειρόγραφες σημειώσεις και να τις μετατρέπουν σε αναζητήσιμο κείμενο — χωρίς να απαιτείται χειροκίνητη πληκτρολόγηση.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς **πώς να κάνετε OCR εικόνας σε κείμενο** χρησιμοποιώντας Aspose OCR for Java, πώς να **φορτώσετε εικόνα για OCR**, και πώς να **διαβάσετε χειρόγραφες σημειώσεις** με ενσωματωμένη διόρθωση ορθογραφίας. Στο τέλος, θα μπορείτε να **μετατρέψετε το κείμενο χειρόγραφης εικόνας** σε μια καθαρή συμβολοσειρά που μπορείτε να αποθηκεύσετε, να ευρετηριάσετε ή να εμφανίσετε.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “OCR εικόνας σε κείμενο”;** Είναι η διαδικασία μετατροπής raster εικόνων που περιέχουν χαρακτήρες σε επεξεργάσιμες, αναζητήσιμες αλφαριθμητικές συμβολοσειρές.  
- **Ποια βιβλιοθήκη διαχειρίζεται το χειρόγραφο;** Aspose OCR for Java παρέχει εξειδικευμένη αναγνώριση χειρογράφου και έλεγχο ορθογραφίας.  
- **Ποια έκδοση της Java απαιτείται;** Java 8 ή νεότερη.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για εκμάθηση· απαιτείται εμπορική άδεια για παραγωγή.  
- **Πόσο γρήγορη είναι η μετατροπή;** Τυπικές χειρόγραφες σελίδες επεξεργάζονται σε κάτω από 2 δευτερόλεπτα σε σύγχρονο CPU.

## Τι είναι το OCR εικόνας σε κείμενο;
**OCR εικόνας σε κείμενο** είναι η αυτοματοποιημένη εξαγωγή κειμένου από bitmap εικόνες, μετατρέποντας οπτικά γλύφους σε μηχανικά αναγνώσιμους χαρακτήρες. Η διαδικασία περιλαμβάνει ανάλυση μοτίων pixel, τμηματοποίηση χαρακτήρων και εφαρμογή γλωσσικών μοντέλων για παραγωγή επεξεργάσιμου κειμένου. Το Aspose OCR το υλοποιεί εφαρμόζοντας μοντέλα deep‑learning που αναγνωρίζουν τόσο τυπωμένο όσο και κυρτό (cursive) κείμενο.

## Γιατί να χρησιμοποιήσετε Aspose OCR για Java;
Aspose OCR for Java υποστηρίζει **30+ γλώσσες**, μπορεί να επεξεργαστεί εικόνες έως **20 MB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, και περιλαμβάνει **ενσωματωμένη διόρθωση ορθογραφίας** που βελτιώνει την ακατέργαστη ακρίβεια αναγνώρισης έως και **15 %** σε θορυβώδεις χειρόγραφες δειγμάτων. Προσφέρει επίσης απλό API, διασυστημική συμβατότητα και τακτικές ενημερώσεις που ακολουθούν την τελευταία έρευνα OCR.

## Προαπαιτούμενα
- Java 8+ (JDK εγκατεστημένο και `JAVA_HOME` ρυθμισμένο)  
- Maven ή Gradle για διαχείριση εξαρτήσεων  
- Αρχείο άδειας Aspose OCR για Java (η δωρεάν δοκιμή είναι επαρκής για αυτόν τον οδηγό)  
- Ένα δείγμα χειρόγραφης εικόνας (PNG, JPEG ή BMP) αποθηκευμένο τοπικά  

## Πώς λειτουργεί το OCR εικόνας σε κείμενο σε Java;
Φορτώστε την εικόνα, διαμορφώστε το `OcrEngine` με γλώσσα και επιλογές διόρθωσης ορθογραφίας, καλέστε `recognize()`, και ανακτήστε το καθαρισμένο κείμενο μέσω `getText()`. Η ολόκληρη αλυσίδα αποτελείται από τρία λογικά βήματα: **αρχικοποίηση**, **διαμόρφωση**, και **εκτέλεση**. Το Aspose OCR αφαιρεί το βαρέως βάρους, ώστε εσείς να γράψετε μόνο λίγες γραμμές Java.

## Βήμα 1: ρυθμίστε το έργο και προσθέστε την εξάρτηση aspose ocr
Πρώτα απ' όλα—το έργο σας χρειάζεται τη βιβλιοθήκη Aspose OCR. Αν χρησιμοποιείτε Maven, προσθέστε αυτό στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest stable version -->
</dependency>
```

Ή με Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip**: Παρακολουθείτε τον αριθμό έκδοσης· οι νεότερες κυκλοφορίες βελτιώνουν την αναγνώριση χειρογράφου και προσθέτουν υποστήριξη γλωσσών.

Μόλις η εξάρτηση λυθεί, είστε έτοιμοι να **φορτώσετε εικόνα για OCR**.

## Βήμα 2: δημιουργήστε την παρουσία του μηχανήματος OCR
Η κλάση `OcrEngine` είναι το βασικό συστατικό που εκτελεί την αναγνώριση.  

`OcrEngine` είναι το κύριο αντικείμενο του Aspose OCR που κρατά τις ρυθμίσεις γλώσσας, τις σημαίες διόρθωσης ορθογραφίας και τα δεδομένα εικόνας.  

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
```

Γιατί να δημιουργήσετε πρώτα τη μηχανή; Επειδή το Aspose OCR σχεδιάστηκε ώστε να είναι επαναχρησιμοποιήσιμο· μπορείτε να επεξεργαστείτε πολλαπλές εικόνες με την ίδια παρουσία, τροποποιώντας τις ρυθμίσεις μεταξύ των εκτελέσεων αν χρειαστεί.

## Βήμα 3: προσθέστε υποστήριξη αγγλικής γλώσσας και ενεργοποιήστε τη διόρθωση ορθογραφίας
Οι χειρόγραφες σημειώσεις συχνά περιέχουν ορθογραφικά λάθη, ελλιπή γράμματα ή ασυνήθιστες συντομογραφίες. Η ενεργοποίηση του ελεγκτή ορθογραφίας δίνει στη μηχανή την ευκαιρία να καθαρίσει το αποτέλεσμα.

`OcrEngine` παρέχει τη μέθοδο `getSettings()` όπου μπορείτε να προσθέσετε πακέτα γλώσσας και να ενεργοποιήσετε τη διόρθωση ορθογραφίας.  

```java
        // Add English language support
        ocrEngine.getLanguages().add(OcrLanguage.ENG);

        // Turn on the built‑in spell checker
        ocrEngine.getSpellChecker().setEnabled(true);
```

> **Γιατί να ενεργοποιήσετε τη διόρθωση ορθογραφίας;**  
> Χωρίς αυτήν, το ακατέργαστο αποτέλεσμα OCR μπορεί να εμφανίσει “t0d@y” ή “c0ffee”. Ο ελεγκτής ορθογραφίας κανονικοποιεί τέτοιες ιδιαιτερότητες, κάνοντας το τελικό κείμενο πολύ πιο χρήσιμο για επεξεργασία downstream όπως η ευρετηρίαση αναζήτησης.

## Βήμα 4: φορτώστε τη χειρόγραφη εικόνα
Τώρα **φορτώνουμε εικόνα για OCR**. Το Aspose παρέχει τη βολική μέθοδο `ImageStream.fromFile` που δέχεται οποιαδήποτε κοινή raster μορφή (PNG, JPEG, BMP).

`ImageStream.fromFile` δημιουργεί ένα αντικείμενο ροής που η μηχανή OCR μπορεί να διαβάσει απευθείας, εξαλείφοντας την ανάγκη ενδιάμεσων buffers.  

```java
        // Path to your handwritten note image
        String imagePath = "YOUR_DIRECTORY/handwritten-note.png";

        // Load the image into the OCR engine
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Αν η εικόνα σας βρίσκεται σε φάκελο πόρων ή τη λαμβάνετε ως byte array (π.χ., από ανέβασμα στο web), μπορείτε να χρησιμοποιήσετε `ImageStream.fromBytes` αντί‑θετα—απλώς αντικαταστήστε τη γραμμή παραπάνω με:

```java
        // ocrEngine.setImage(ImageStream.fromBytes(uploadedBytes));
```

## Βήμα 5: εκτελέστε OCR και ανακτήστε το διορθωμένο κείμενο
Η μέθοδος `recognize()` εκτελεί τη διαδικασία OCR και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τα αποτελέσματα.

```java
        // Run OCR and get the corrected text
        String correctedText = ocrEngine.recognize().getText();
```

Η μέθοδος `recognize()` επιστρέφει ένα αντικείμενο `OcrResult` που περιλαμβάνει όχι μόνο το απλό κείμενο αλλά και βαθμολογίες εμπιστοσύνης, περιοριστικά πλαίσια (bounding boxes) και άλλα. Για τις περισσότερες περιπτώσεις, η απλή `getText()` είναι επαρκής.

## Βήμα 6: εξαγωγή του αποτελέσματος
Καλώντας `getText()` στο `OcrResult` ανακτάτε τη αναγνωρισμένη αλφαριθμητική συμβολοσειρά.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(correctedText);
    }
}
```

### Αναμενόμενο αποτέλεσμα
Υποθέτοντας ότι η χειρόγραφη σημείωση λέει:

```
Buy milk, eggs, and bread tomorrow.
```

Θα πρέπει να δείτε κάτι όπως:

```
Corrected text:
Buy milk, eggs, and bread tomorrow.
```

Ακόμη και αν το αρχικό σκίτσο ήταν ακατάστατο—π.χ. “B u y m i l k , e g g s , a n d B r e a d t o m o r r o w”—ο ελεγκτής ορθογραφίας συνήθως το διορθώνει.

## Φόρτωση εικόνας για OCR – συμβουλές για καλύτερη ακρίβεια

1. **Η ανάλυση μετρά** – Στοχεύστε τουλάχιστον **300 dpi**. Χαμηλότερες αναλύσεις κάνουν τη μηχανή να χάνει μικρές γραμμές.  
2. **Η αντίθεση είναι βασική** – Αν το φόντο είναι χρωματιστό, μετατρέψτε πρώτα την εικόνα σε grayscale.  
3. **Κόψτε στο περιεχόμενο** – Η αφαίρεση περιττών περιθωρίων μειώνει τον θόρυβο και επιταχύνει την επεξεργασία.  

Μπορείτε να προεπεξεργαστείτε τις εικόνες με βιβλιοθήκες όπως OpenCV ή ακόμη και με την ενσωματωμένη Java `BufferedImage` πριν τις περάσετε στο Aspose.

## Ανάγνωση χειρόγραφων σημειώσεων: διαχείριση ακραίων περιπτώσεων

- **Λέξεις χαμηλής εμπιστοσύνης**: `ocrEngine.getResult().getWords()` επιστρέφει μια λίστα όπου κάθε λέξη έχει τιμή εμπιστοσύνης (0–100). Μπορείτε να φιλτράρετε λέξεις κάτω από ένα όριο και να ζητήσετε από τον χρήστη χειροκίνητη ανασκόπηση.  
- **Πολλαπλές γλώσσες**: Αν χρειάζεται να **διαβάσετε χειρόγραφες σημειώσεις** τόσο στα Αγγλικά όσο και στα Ισπανικά, προσθέστε και τις δύο γλώσσες πριν καλέσετε `recognize()`.  
- **Μεγάλα αρχεία**: Για πολυ‑σελίδες PDF ή TIFF, επαναλάβετε για κάθε σελίδα με `ocrEngine.setImage(pageStream)` μέσα σε βρόχο.

## Μετατροπή του κειμένου χειρόγραφης εικόνας σε δομημένα δεδομένα
Συχνά δεν χρειάζεστε μόνο μια ακατέργαστη συμβολοσειρά· μπορεί να θέλετε να εξάγετε ημερομηνίες, ποσά ή στοιχεία λίστας. Αφού έχετε το διορθωμένο κείμενο, κανονικές εκφράσεις ή βιβλιοθήκες NLP (όπως Stanford CoreNLP) μπορούν να αναλύσουν το περιεχόμενο:

```java
// Example: Extract a date from the OCR output
Pattern datePattern = Pattern.compile("\\b\\d{2}/\\d{2}/\\d{4}\\b");
Matcher matcher = datePattern.matcher(correctedText);
if (matcher.find()) {
    System.out.println("Found date: " + matcher.group());
}
```

Αυτό το απόσπασμα δείχνει πόσο εύκολο είναι να περάσετε από **μετατροπή του κειμένου χειρόγραφης εικόνας** σε επεξεργάσιμα δεδομένα.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| Παραμορφωμένο αποτέλεσμα, πολλοί χαρακτήρες `?` | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής αντίθεσης | Αυξήστε τη φωτεινότητα ή προεπεξεργαστείτε με εξίσωση ιστογράμματος |
| Χαμένες λέξεις | Η γραφή είναι πολύ κυρτή | Ενεργοποιήστε `ocrEngine.getSettings().setEnableCursive(true)` (αν υποστηρίζεται) |
| Ο ελεγκτής ορθογραφίας εισάγει λανθασμένες λέξεις | Ασυμφωνία μοντέλου γλώσσας | Προσθέστε προσαρμοσμένο λεξικό μέσω `ocrEngine.getSpellChecker().addUserWords(...)` |
| Σφάλμα έλλειψης μνήμης σε μεγάλες εικόνες | Μέγεθος εικόνας > 10 MB | Μειώστε την ανάλυση πριν τη φόρτωση ή επεξεργαστείτε σε τμήματα |

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή‑επικόλληση)

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Add English language support and enable spell correction
        ocrEngine.getLanguages().add(OcrLanguage.ENG);
        ocrEngine.getSpellChecker().setEnabled(true);

        // Step 3: Load the image that contains handwritten text
        // Replace with the actual path to your handwritten note
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/handwritten-note.png"));

        // Step 4: Perform OCR and obtain the corrected text
        String correctedText = ocrEngine.recognize().getText();

        // Step 5: Output the result
        System.out.println("Corrected text:");
        System.out.println(correctedText);
    }
}
```

> **Σημείωση**: Αν εκτελείτε τον κώδικα από IDE, βεβαιωθείτε ότι ο φάκελος `YOUR_DIRECTORY` βρίσκεται στο classpath ή χρησιμοποιήστε απόλυτη διαδρομή.

## Συχνές ερωτήσεις

**Ε: Μπορώ να το χρησιμοποιήσω σε εμπορική εφαρμογή;**  
Α: Ναι, απαιτείται έγκυρη άδεια Aspose OCR για χρήση σε παραγωγή· διαθέτεται δωρεάν δοκιμή για αξιολόγηση.

**Ε: Υποστηρίζει η μηχανή γλώσσες εκτός των Αγγλικών;**  
Α: Απόλυτα. Το Aspose OCR υποστηρίζει **30+ γλώσσες**, συμπεριλαμβανομένων Ισπανικών, Γαλλικών, Γερμανικών και Κινέζικων.

**Ε: Πώς επηρεάζει η διόρθωση ορθογραφίας την απόδοση;**  
Α: Η ενεργοποίηση της διόρθωσης ορθογραφίας προσθέτει περίπου **10 %** επιπλέον φόρτο, αλλά η ανταλλαγή αξίζει συνήθως για την αύξηση της ακρίβειας.

**Ε: Ποιες μορφές εικόνας γίνονται αποδεκτές;**  
Α: PNG, JPEG, BMP, TIFF και GIF υποστηρίζονται εξ' ορισμού.

**Ε: Πώς μπορώ να επεξεργαστώ αυτόματα έναν φάκελο εικόνων;**  
Α: Τυλίξτε τα βήματα OCR σε βρόχο `for (File file : folder.listFiles())`, επαναχρησιμοποιώντας την ίδια παρουσία `OcrEngine` και προσαρμόζοντας το stream εικόνας για κάθε αρχείο.

## Συμπέρασμα

Καλύψαμε **πώς να κάνετε OCR εικόνας σε κείμενο** σε Java από την αρχή μέχρι το τέλος, δείχνοντάς σας πώς να **φορτώσετε εικόνα για OCR**, **διαβάσετε χειρόγραφες σημειώσεις**, να ενεργοποιήσετε τη διόρθωση ορθογραφίας και τελικά να **μετατρέψετε το κείμενο χειρόγραφης εικόνας** σε μια καθαρή συμβολοσειρά. Η προσέγγιση είναι απλή, αλλά αρκετά ισχυρή για εφαρμογές παραγωγικής κλίμακας.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε πειραματισμούς με πολυ‑σελίδες PDF, προσθέστε προσαρμοσμένα λεξικά για ειδική ορολογία κλάδου, ή τροφοδοτήστε το αποτέλεσμα OCR σε μοντέλο μηχανικής μάθησης για ανάλυση συναισθήματος. Ο ουρανός είναι το όριο όταν συνδυάζετε την ακρίβεια του Aspose OCR με την ευελιξία της Java.

Έχετε ερωτήσεις για κάποια συγκεκριμένη ακραία περίπτωση, ή θέλετε να μοιραστείτε πώς το ενσωματώσατε σε κινητή εφαρμογή; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

![παράδειγμα OCR εικόνας](/images/ocr-handwritten-example.png "πώς να κάνετε OCR εικόνας χειρόγραφων σημειώσεων")

**Τελευταία ενημέρωση:** 2026-09-28  
**Δοκιμάστηκε με:** Aspose OCR for Java 24.11  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Πώς να κάνετε OCR εικόνας σε Java με χειρόγραφες σημειώσεις και έλεγχο ορθογραφίας](/ocr/java/advanced-ocr-techniques/how-to-ocr-image-in-java-handwritten-notes-with-spell-check/)
- [Προεπεξεργασία εικόνας OCR σε Java για βελτίωση ακρίβειας και εξαγωγή κειμένου](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Εξαγωγή κειμένου από εικόνα με Aspose OCR Java – Γρήγορος οδηγός](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}