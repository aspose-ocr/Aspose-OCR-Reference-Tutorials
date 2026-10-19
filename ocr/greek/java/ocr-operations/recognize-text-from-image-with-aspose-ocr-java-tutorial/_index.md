---
category: general
date: 2026-02-17
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να φορτώνετε εικόνα
  για OCR χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR Java. Οδηγός βήμα‑προς‑βήμα με
  διορθωτή ορθογραφίας.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: el
og_description: Αναγνώριση κειμένου από εικόνα με χρήση Aspose OCR Java. Αυτό το σεμινάριο
  δείχνει πώς να φορτώσετε εικόνα για OCR, να ενεργοποιήσετε τη διόρθωση ορθογραφίας
  και να εξάγετε καθαρό κείμενο.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός Aspose OCR για Java
tags:
- Java
- OCR
- Aspose
title: Αναγνώριση κειμένου από εικόνα με το Aspose OCR – Εγχειρίδιο Java
url: /el/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose OCR – Java Tutorial

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερατε ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—π.χ. σάρωση τιμολογίων, ψηφιοποίηση χειρόγραφων σημειώσεων ή εξαγωγή λεζάντων από στιγμιότυπα—η ακριβής απόδοση του OCR είναι κρίσιμη.

Σε αυτόν τον οδηγό θα δούμε πώς να φορτώσουμε μια εικόνα για OCR, να ενεργοποιήσουμε τον ενσωματωμένο διορθωτή ορθογραφίας του Aspose OCR και, τέλος, να εκτυπώσουμε το καθαρισμένο κείμενο. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα Java που **αναγνωρίζει κείμενο από εικόνα** με λίγες μόνο γραμμές κώδικα.

## What This Tutorial Covers

- Πώς να εφαρμόσετε την άδεια Aspose OCR (ώστε η demo να τρέχει χωρίς υδατογράφημα)  
- Δημιουργία ενός αντικειμένου `OcrEngine` και επιλογή της αγγλικής ως γλώσσα αναγνώρισης  
- **Load image for OCR** χρησιμοποιώντας `OcrInput` και δείχνοντας σε ένα PNG που περιέχει λανθασμένες λέξεις  
- Ενεργοποίηση του διορθωτή ορθογραφίας, προαιρετικά με δικό σας λεξικό  
- Εκτέλεση της αναγνώρισης και εκτύπωση του διορθωμένου αποτελέσματος  

Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφά αρχεία ρυθμίσεων—απλώς καθαρή Java και το Aspose OCR JAR.

> **Pro tip:** Αν είστε νέοι στο Aspose, κατεβάστε μια δωρεάν άδεια δοκιμής 30 ημέρων από τον ιστότοπο του Aspose και τοποθετήστε το αρχείο `.lic` σε έναν φάκελο που μπορείτε να αναφέρετε από τον κώδικά σας.

## Prerequisites

- Java 8 ή νεότερη (ο κώδικας συντάσσεται επίσης με JDK 11)  
- Aspose.OCR for Java JAR στο classpath σας  
- Ένα έγκυρο αρχείο `Aspose.OCR.lic` (ή μπορείτε να τρέξετε σε λειτουργία αξιολόγησης, αλλά η demo θα προσθέσει υδατογράφημα)  
- Ένα αρχείο εικόνας (`misspelled.png`) που περιέχει κείμενο με σκόπιμα ορθογραφικά λάθη—ιδανικό για να δείτε τον διορθωτή ορθογραφίας σε δράση  

Τα έχετε όλα; Τέλεια—ας βουτήξουμε.

## Step 1: Apply Your Aspose OCR License

Πριν η μηχανή κάνει οποιαδήποτε βαριά δουλειά, πρέπει να ξέρει ότι έχετε άδεια. Διαφορετικά θα εμφανιστεί ένα banner “Trial version” στην έξοδο.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Γιατί είναι σημαντικό:* Η άδεια αφαιρεί το υδατογράφημα δοκιμής και ξεκλειδώνει το πλήρες λεξικό του διορθωτή ορθογραφίας. Η παράλειψη αυτού του βήματος λειτουργεί, αλλά η έξοδός σας θα μολύνεται με κείμενο “Aspose OCR Demo”.

## Step 2: Create and Configure the OCR Engine

Τώρα ξεκινάμε τη μηχανή και της λέμε ποια γλώσσα να χρησιμοποιήσει. Τα αγγλικά είναι η πιο κοινή, αλλά το Aspose υποστηρίζει δεκάδες.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Γιατί ορίζουμε τη γλώσσα:* Το μοντέλο γλώσσας καθορίζει το σύνολο χαρακτήρων και επηρεάζει τις προτάσεις του διορθωτή ορθογραφίας. Η χρήση λανθασμένης γλώσσας μπορεί να μειώσει δραστικά την ακρίβεια.

## Step 3: Enable Spell Correction and (Optionally) Point to a Custom Dictionary

Το Aspose OCR περιλαμβάνει ενσωματωμένο αγγλικό λεξικό, αλλά μπορείτε να προσθέσετε δικό σας αν έχετε όρους ειδικού τομέα (π.χ. ιατρική ορολογία ή κωδικούς προϊόντων).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Τι κάνει ο διορθωτής:* Όταν η μηχανή OCR εντοπίζει μια λέξη που δεν υπάρχει στο λεξικό, προσπαθεί να την αντικαταστήσει με την πιο κοντινή αντιστοιχία. Αυτός είναι ο λόγος που η demo μπορεί να μετατρέψει το “recieve” σε “receive” αυτόματα.

## Step 4: Load the Image for OCR

Αυτή είναι η ενότητα που απαντά άμεσα στο **load image for OCR**. Δημιουργούμε ένα αντικείμενο `OcrInput` και προσθέτουμε το αρχείο PNG μας.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Γιατί χρησιμοποιούμε το `OcrInput`:* Απομονώνει τη λογική ανάγνωσης αρχείων και σας επιτρέπει να προσθέσετε πολλαπλές σελίδες αργότερα, αν χρειαστεί να επεξεργαστείτε ένα PDF πολλαπλών σελίδων ή ένα σύνολο εικόνων.

## Step 5: Run the Recognition and Retrieve Corrected Text

Τώρα η μηχανή κάνει τη βαριά δουλειά—αναγνωρίζει χαρακτήρες, εφαρμόζει το μοντέλο γλώσσας και τέλος διορθώνει την ορθογραφία.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Αναμενόμενη έξοδος:* Υποθέτοντας ότι το `misspelled.png` περιέχει τη φράση “Ths is a smple test”, η κονσόλα θα εκτυπώσει:

```
Corrected text:
This is a simple test
```

Παρατηρήστε πώς οι λανθασμένες λέξεις (`Ths`, `smple`) έχουν διορθωθεί αυτόματα.

## Full, Ready‑to‑Run Example

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα σε ένα μπλοκ. Αντιγράψτε‑και‑επικολλήστε, προσαρμόστε τις διαδρομές και πατήστε **Run**.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tip:** Αν θέλετε να επεξεργαστείτε JPEG ή BMP αντί για PNG, απλώς αλλάξτε την επέκταση του αρχείου—το Aspose OCR υποστηρίζει όλες τις κοινές μορφές raster.

## Common Questions & Edge Cases

- **Τι γίνεται αν η εικόνα μου είναι χαμηλής ανάλυσης;**  
  Αυξήστε το DPI πριν το δώσετε στο Aspose, επανακλιμακώνοντας με μια βιβλιοθήκη όπως `java.awt.Image`. Υψηλότερο DPI δίνει στη μηχανή περισσότερα pixel, κάτι που συνήθως βελτιώνει την ακρίβεια.

- **Μπορώ να αναγνωρίσω πολλαπλές γλώσσες στην ίδια εικόνα;**  
  Ναι. Καλέστε `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` και προαιρετικά προσθέστε λίστα γλωσσών με `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);`.

- **Το προσαρμοσμένο λεξικό μου δεν χρησιμοποιείται—γιατί;**  
  Βεβαιωθείτε ότι ο φάκελος περιέχει αρχεία κειμένου με μία λέξη ανά γραμμή και ότι η διαδρομή είναι απόλυτη ή σωστά σχετική με το τρέχον φάκελο εργασίας.

- **Πώς εξάγω τις βαθμολογίες εμπιστοσύνης;**  
  `result.getConfidence()` επιστρέφει ένα float μεταξύ 0 και 1 για ολόκληρη τη σελίδα. Για εμπιστοσύνη ανά χαρακτήρα, εξερευνήστε `result.getWordList()`.

## Conclusion

Τώρα ξέρετε πώς να **αναγνωρίζετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR για Java, πώς να **φορτώνετε εικόνα για OCR**, και πώς να ενεργοποιείτε τον διορθωτή ορθογραφίας για να καθαρίζετε συνηθισμένα τυπογραφικά λάθη. Το πλήρες παράδειγμα παραπάνω είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο Maven ή Gradle, και με λίγες προσαρμογές μπορείτε να το κλιμακώσετε για επεξεργασία φακέλων, ενσωμάτωση σε web service ή σύνδεση με σύστημα διαχείρισης εγγράφων.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε ένα PDF πολλαπλών σελίδων, πειραματιστείτε με προσαρμοσμένο λεξικό για ειδική ορολογία, ή συνδέστε την έξοδο με ένα API μετάφρασης. Οι δυνατότητες είναι ατελείωτες, και το βασικό μοτίβο—license → engine → language → spell‑corrector → input → recognize → output—παραμένει το ίδιο.

Καλή προγραμματιστική δουλειά, και οι OCR αποτελέσματά σας να είναι πάντα ακριβή!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}