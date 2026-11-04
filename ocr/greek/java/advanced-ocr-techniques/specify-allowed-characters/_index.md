---
date: 2026-05-24
description: Ανακαλύψτε πώς να χρησιμοποιήσετε OCR με Aspose.OCR για Java, εξάγετε
  κείμενο από εικόνες, ορίστε επιτρεπόμενους χαρακτήρες και εφαρμόστε προσωρινή άδεια
  σε λίγα λεπτά.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Καθορισμός επιτρεπόμενων χαρακτήρων στο Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Πώς να χρησιμοποιήσετε OCR – Εξαγωγή κειμένου από εικόνες με Aspose.OCR
url: /el/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR – Εξαγωγή κειμένου από εικόνες με Aspose.OCR

Σε σύγχρονες εφαρμογές Java, η **χρήση OCR** είναι συχνή ερώτηση, ειδικά όταν χρειάζεται να μετατρέψετε σαρωμένα τιμολόγια, αποδείξεις ή έντυπες φόρμες σε αναζητήσιμο κείμενο. Αυτό το εκπαιδευτικό υλικό σας καθοδηγεί βήμα‑βήμα σε ένα πλήρες παράδειγμα **Aspose.OCR for Java**: εξαγωγή κειμένου από εικόνες, περιορισμός του αποτελέσματος σε προσαρμοσμένο σύνολο χαρακτήρων και εφαρμογή προσωρινής άδειας για γρήγορη αξιολόγηση.

## Συχνές Απαντήσεις
- **Τι κάνει το Aspose.OCR;** Εξάγει κείμενο από εικόνες με υψηλή ακρίβεια και σας επιτρέπει να περιορίσετε τους αναγνωρισμένους χαρακτήρες.  
- **Χρειάζομαι άδεια;** Απαιτείται προσωρινή ή μόνιμη άδεια για παραγωγική χρήση· το προσωρινό κλειδί αφαιρεί τα υδατογραφήματα.  
- **Ποια έκδοση του JDK υποστηρίζεται;** Η βιβλιοθήκη λειτουργεί με τις τελευταίες εκδόσεις του JDK (JDK 17, 19, 21).  
- **Μπορώ να περιορίσω τους αναγνωρισμένους χαρακτήρες;** Ναι—χρησιμοποιήστε τη μέθοδο `setAllowedCharacters` για να περιορίσετε την έξοδο.  
- **Πόσο χρόνο απαιτεί η εγκατάσταση;** Περίπου 10‑15 λεπτά για μια βασική υλοποίηση από άκρο σε άκρο.

## Τι είναι η «εξαγωγή κειμένου από εικόνες»;
Η εξαγωγή κειμένου από εικόνες, γνωστή και ως οπτική αναγνώριση χαρακτήρων (OCR), μετατρέπει οπτικούς χαρακτήρες—εκτυπωμένους, χειρόγραφους ή τυπωμένους—σε συμβολοσειρές που διαβάζει η μηχανή. Αυτή η μετατροπή επιτρέπει στις εφαρμογές να αναζητούν, να ευρετηριάζουν, να επεξεργάζονται και να αναλύουν το περιεχόμενο προγραμματιστικά, υποστηρίζοντας ροές εργασίας όπως η επεξεργασία τιμολογίων, η αρχειοθέτηση εγγράφων και η αυτοματοποίηση εισαγωγής δεδομένων.

## Γιατί να χρησιμοποιήσετε Aspose.OCR for Java;
Το Aspose.OCR υποστηρίζει **πάνω από 60 γλώσσες**, μπορεί να επεξεργαστεί εικόνες έως **10 MB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, και προσφέρει **>95 % ακρίβεια** σε καθαρές σαρώσεις. Η βιβλιοθήκη είναι αυτόνομη, δεν απαιτεί εξωτερικές μηχανές OCR, κάτι που απλοποιεί την ανάπτυξη και μειώνει το κόστος αδειοδότησης.

## Προαπαιτούμενα

### Java Development Kit (JDK)

Βεβαιωθείτε ότι έχετε εγκαταστήσει το πιο πρόσφατο Java Development Kit. Μπορείτε να το κατεβάσετε από [εδώ](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη Aspose.OCR for Java από το [link λήψης](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Για πλήρη λειτουργικότητα, αποκτήστε άδεια. Μπορείτε να αγοράσετε μία από [εδώ](https://purchase.aspose.com/buy) ή να ζητήσετε μια [προσωρινή άδεια](https://purchase.aspose.com/temporary-license/) για δοκιμαστικούς σκοπούς.

## Πώς να χρησιμοποιήσετε OCR με Aspose.OCR for Java;

Φορτώστε την εικόνα σας, διαμορφώστε τη μηχανή OCR και καλέστε τη μέθοδο αναγνώρισης—όλα σε λίγες απλές γραμμές. Αυτή η άμεση απάντηση σας λέει ακριβώς τι πρέπει να κάνετε: δημιουργήστε ένα αντικείμενο `AsposeOCR` με τη συμβολοσειρά άδειας, ορίστε τυχόν επιτρεπόμενους χαρακτήρες και καλέστε `RecognizeLine` στην εικόνα-στόχο για να λάβετε το εξαγόμενο κείμενο. Το API διαχειρίζεται την προεπεξεργασία της εικόνας εσωτερικά, έτσι λαμβάνετε καθαρά αποτελέσματα χωρίς επιπλέον κώδικα.

### Εισαγωγή Πακέτων

Η κλάση `AsposeOCR` βρίσκεται στο πακέτο `com.aspose.ocr`. Εισάγετε τις απαιτούμενες κλάσεις πριν ξεκινήσετε τον κώδικα.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Οδηγός Βήμα‑βήμα

### Βήμα 1: Ορίστε τον Φάκελο Εγγράφων

Επιλέξτε έναν φάκελο όπου θα αποθηκευτούν τα αποτελέσματα OCR και τα προσωρινά αρχεία. Αυτή η διαδρομή θα χρησιμοποιηθεί αργότερα για τον εντοπισμό της εικόνας που θέλετε να επεξεργαστείτε.

```java
String dataDir = "Your Document Directory";
```

### Βήμα 2: Καθορίστε τη Διαδρομή της Εικόνας

Δώστε τη πλήρη διαδρομή του συστήματος αρχείων ή μια τοποθεσία πόρου class‑path που δείχνει στην εικόνα που θέλετε να αναλύσετε.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Βήμα 3: Δημιουργήστε ένα Παράδειγμα Aspose.OCR

`AsposeOCR` είναι η κύρια μηχανή που εκτελεί την οπτική αναγνώριση χαρακτήρων. Δημιουργήστε το με μια προσωρινή ή μόνιμη συμβολοσειρά άδειας.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Βήμα 4: Εκτελέστε την Αναγνώριση OCR

`RecognizeLine` εξάγει μια μόνο γραμμή κειμένου από την παρεχόμενη εικόνα και την επιστρέφει ως απλό Java `String`. Μπορείτε να καλέσετε αυτή τη μέθοδο επανειλημμένα για έγγραφα πολλαπλών γραμμών.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Συμβουλή:** Αν χρειάζεται να περιορίσετε την έξοδο μόνο σε ψηφία (π.χ. για αριθμούς τιμολογίων), καλέστε `setAllowedCharacters("0123456789")` στο αντικείμενο `AsposeOCR` πριν καλέσετε το `RecognizeLine`. Αυτό αναγκάζει τη μηχανή να αγνοήσει οποιαδήποτε μη‑αριθμητικά σύμβολα.  
> `setAllowedCharacters` είναι μέθοδος του `AsposeOCR` που περιορίζει την έξοδο OCR σε συγκεκριμένο whitelist χαρακτήρων.

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Καμία έξοδος ή κενή συμβολοσειρά** | Λανθασμένη διαδρομή εικόνας ή μη υποστηριζόμενη μορφή | Επαληθεύστε το `imagePath` και χρησιμοποιήστε υποστηριζόμενη μορφή (JPEG, PNG, BMP) |
| **Σφάλματα αναγνώρισης** | Εικόνα χαμηλής ανάλυσης ή θορυβώδες φόντο | Προεπεξεργαστείτε την εικόνα (αυξήστε την αντίθεση, κάντε δυαδικοποίηση) πριν το OCR |
| **Η άδεια δεν εφαρμόστηκε** | Λείπει ή είναι άκυρο κλειδί άδειας | Βεβαιωθείτε ότι η συμβολοσειρά άδειας είναι σωστή και περάστηκε στον κατασκευαστή `AsposeOCR` |

## Συχνές Ερωτήσεις

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το Aspose.OCR;**  
Α: Επισκεφθείτε τη [σελίδα προσωρινής άδειας](https://purchase.aspose.com/temporary-license/) για να ζητήσετε ένα κλειδί δοκιμής που αφαιρεί τα υδατογραφήματα αξιολόγησης.

**Ε: Πού μπορώ να βρω υποστήριξη για το Aspose.OCR;**  
Α: Ενταχθείτε στην κοινότητα στο [Φόρουμ Aspose.OCR](https://forum.aspose.com/c/ocr/16) για βοήθεια και συζητήσεις.

**Ε: Μπορώ να ορίσω επιτρεπόμενους χαρακτήρες στο Aspose.OCR;**  
Α: Ναι, χρησιμοποιήστε το API `setAllowedCharacters` για να ορίσετε ένα προσαρμοσμένο whitelist χαρακτήρων. Ιδανικό για πεδία μόνο με αριθμούς.

**Ε: Είναι το Aspose.OCR συμβατό με τις τελευταίες εκδόσεις του JDK;**  
Α: Απόλυτα—το Aspose.OCR ενημερώνεται τακτικά ώστε να παραμένει συμβατό με τις πιο πρόσφατες εκδόσεις της Java.

**Ε: Υπάρχουν επιπλέον δυνατότητες OCR πέρα από την αναγνώριση γραμμών;**  
Α: Η βιβλιοθήκη υποστηρίζει επίσης αναγνώριση μπλοκ, παραγράφων και ολόπλευρης σελίδας, πακέτα γλωσσών και προχωρημένη προεπεξεργασία εικόνας.

## Συμπέρασμα

Ακολουθώντας αυτό το **Aspose OCR Java tutorial**, τώρα γνωρίζετε **πώς να χρησιμοποιήσετε OCR** για εξαγωγή κειμένου από εικόνες, περιορισμό του συνόλου χαρακτήρων και εφαρμογή προσωρινής άδειας για γρήγορη δοκιμή. Εμβαθύνετε στην πλήρη [τεκμηρίωση](https://reference.aspose.com/ocr/java/) για να εξερευνήσετε υποστήριξη πολλαπλών γλωσσών, επεξεργασία δέσμης και προσαρμοσμένες αλυσίδες προεπεξεργασίας.

---

**Τελευταία ενημέρωση:** 2026-05-24  
**Δοκιμάστηκε με:** Aspose.OCR for Java 24.11  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Πώς να ορίσετε άδεια και να επαληθεύσετε την άδεια Aspose.OCR σε Java](/ocr/java/ocr-basics/set-license/)
- [Μετατροπή εικόνας σε κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Παράδειγμα Aspose OCR Java – Αναγνώριση Γραμμών σε Εικόνες](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}