---
category: general
date: 2026-05-25
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα και να εξάγετε κείμενο
  από τεχνικό έγγραφο χρησιμοποιώντας το Aspose OCR σε Java. Κώδικας βήμα‑προς‑βήμα
  και συμβουλές.
draft: false
keywords:
- recognize text from image
- extract text from technical document
- Aspose OCR Java
- custom dictionary OCR
- Java image processing
language: el
og_description: Αναγνώριση κειμένου από εικόνα σε Java γρήγορα. Αυτός ο οδηγός δείχνει
  πώς να εξάγετε κείμενο από τεχνικό έγγραφο χρησιμοποιώντας προσαρμοσμένο λεξικό.
og_title: Αναγνώριση κειμένου από εικόνα σε Java – Πλήρες Μάθημα Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to recognize text from image and extract text from technical
    document using Aspose OCR in Java. Step‑by‑step code and tips.
  headline: recognize text from image with Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Learn how to recognize text from image and extract text from technical
    document using Aspose OCR in Java. Step‑by‑step code and tips.
  name: recognize text from image with Java – Complete Aspose OCR Guide
  steps:
  - name: Create `OcrEngine`.
    text: Create `OcrEngine`.
  - name: Point it at a user dictionary.
    text: Point it at a user dictionary.
  - name: Load the target image.
    text: Load the target image.
  - name: Call `recognize()`.
    text: Call `recognize()`.
  - name: Pull out `result.getText()`.
    text: Pull out `result.getText()`.
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Αναγνώριση κειμένου από εικόνα με Java – Πλήρης Οδηγός Aspose OCR
url: /el/java/ocr-operations/recognize-text-from-image-with-java-complete-aspose-ocr-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρης Εκπαιδευτικό Σεμινάριο Aspose OCR

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά τα αποτελέσματα να λείπουν λέξεις ειδικές για το πεδίο; Δεν είστε μόνοι. Σε πολλά έργα—σκεφτείτε τη σάρωση σχημάτων, εγχειριδίων ή νομικών PDF—ο ενσωματωμένος ορθογράφος δεν καταλαβαίνει σωστά την ορολογία.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα προς βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που **αναγνωρίζει κείμενο από εικόνα** *και* σας επιτρέπει να **εξάγετε κείμενο από τεχνικό έγγραφο** με ένα προσαρμοσμένο λεξικό. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη βιβλιοθήκη Aspose OCR για Java.
- Γιατί η φόρτωση προσαρμοσμένου λεξικού βελτιώνει τη διόρθωση ορθογραφίας.
- Τα ακριβή βήματα για να τροφοδοτήσετε μια εικόνα τεχνικού διαγράμματος στη μηχανή.
- Πώς να καταγράψετε το αποτέλεσμα του OCR και να το αντιμετωπίσετε ως εξαγόμενο κείμενο από τεχνικό έγγραφο.
- Κοινά προβλήματα (απουσία γραμματοσειρών, μεγάλα αρχεία) και γρήγορες λύσεις.

Δεν απαιτείται προγενέστερη εμπειρία με το Aspose· αρκεί μια βασική ρύθμιση Java και ένα αρχείο εικόνας για πειραματισμό.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|-------------|--------|
| JDK 8 ή νεότερο | Το Aspose OCR στοχεύει σε Java 8+. |
| Maven ή Gradle (προαιρετικά) | Απλοποιεί τη διαχείριση εξαρτήσεων. |
| `aspose-ocr` JAR (τελευταία έκδοση) | Η κύρια μηχανή OCR. |
| Αρχείο κειμένου `custom_dict.txt` (μία λέξη ανά γραμμή) | Προσαρμοσμένο λεξικό για τεχνικούς όρους. |
| Εικόνα `technical_doc.png` που περιέχει το κείμενο που θέλετε να διαβάσετε | Παράδειγμα εισόδου. |

Αν προτιμάτε μια γρήγορη εκκίνηση, απλώς κατεβάστε το JAR από τον ιστότοπο της Aspose και προσθέστε το στο classpath σας.

![Diagram showing OCR workflow that recognize text from image and extracts technical content](ocr-workflow.png){alt="Διάγραμμα ροής OCR που αναγνωρίζει κείμενο από εικόνα και εξάγει τεχνικό περιεχόμενο"}

## Βήμα 1: Αρχικοποίηση της Μηχανής Aspose OCR

Το πρώτο που χρειαζόμαστε είναι μια παρουσία του `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που αργότερα θα **αναγνωρίσει κείμενο από εικόνα**.  

```java
import com.aspose.ocr.*;

public class CustomDictionaryDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Η μηχανή κρατά όλες τις επιλογές διαμόρφωσης, συμπεριλαμβανομένων των πακέτων γλώσσας και των ρυθμίσεων διορθωτή ορθογραφίας. Η δημιουργία της νωρίς σας δίνει ένα ενιαίο σημείο για να προσαρμόσετε τη συμπεριφορά αργότερα.

## Βήμα 2: Φόρτωση Προσαρμοσμένου Λεξικού για Βελτίωση Ακρίβειας

Τα τεχνικά έγγραφα είναι γεμάτα συντομογραφίες, αριθμούς εξαρτημάτων και ειδική ορολογία του κλάδου. Κατευθύνοντας τη μηχανή σε ένα λεξικό που παρέχεται από τον χρήστη, λέτε στο Aspose να θεωρεί αυτές τις λέξεις έγκυρες, βελτιώνοντας δραστικά το βήμα **εξαγωγής κειμένου από τεχνικό έγγραφο**.  

```java
        // Step 2: Load a custom dictionary (one word per line) to improve spell correction
        engine.getEngineOptions()
              .getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/custom_dict.txt");
```

**Συμβουλές & Προειδοποιήσεις**

- **Μία λέξη ανά γραμμή** – οι κενές γραμμές αγνοούνται.
- Χρησιμοποιήστε κωδικοποίηση UTF‑8· διαφορετικά τα σύμβολα που δεν είναι ASCII μπορεί να διαβαστούν λανθασμένα.
- Διατηρήστε το μέγεθος του αρχείου λογικό (< 50 KB) για να αποφύγετε καθυστέρηση εκκίνησης.

## Βήμα 3: Φόρτωση της Εικόνας που Περιέχει το Τεχνικό σας Περιεχόμενο

Τώρα τροφοδοτούμε την πραγματική εικόνα στη μηχανή. Αυτή είναι η στιγμή που η μηχανή θα **αναγνωρίσει κείμενο από εικόνα**.  

```java
        // Step 3: Load the image that contains the text to be recognized
        engine.getImage().loadFromFile("YOUR_DIRECTORY/technical_doc.png");
```

**Τι γίνεται αν η εικόνα είναι τεράστια;**  
Το Aspose αυτόματα μειώνει το μέγεθος των μεγάλων εικόνων, αλλά μπορείτε επίσης να καλέσετε `engine.getEngineOptions().setResolution(300)` για να επιβάλετε DPI που ισορροπεί την ταχύτητα και την ακρίβεια.

## Βήμα 4: Εκτέλεση OCR – Η Κεντρική Ενέργεια “αναγνώριση κειμένου από εικόνα”

Με τη μηχανή διαμορφωμένη και την εικόνα φορτωμένη, ήρθε η ώρα να εκτελέσετε τη διαδικασία OCR.  

```java
        // Step 4: Perform OCR on the loaded image
        OcrResult result = engine.recognize();
```

Πίσω από τη σκηνή, το Aspose εκτελεί πολλαπλές περάσεις αναγνώρισης, εφαρμόζει το προσαρμοσμένο λεξικό και επιστρέφει ένα πλούσιο αντικείμενο `OcrResult`. Αυτό το αντικείμενο δεν περιέχει μόνο απλό κείμενο αλλά και βαθμολογίες εμπιστοσύνης και περιοριστικά πλαίσια—χρήσιμο αν αργότερα χρειαστεί να επισημάνετε λέξεις στην αρχική εικόνα.

## Βήμα 5: Έξοδος του Εξαγόμενου Κειμένου – Το Περιεχόμενο του Τεχνικού σας Εγγράφου

Τέλος, εξάγουμε το απλό κείμενο από το αποτέλεσμα. Εδώ **εξάγουμε κείμενο από τεχνικό έγγραφο** για επεξεργασία σε επόμενα στάδια (ευρετηρίαση αναζήτησης, αναλύσεις κ.λπ.).  

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

## Αναμενόμενη Έξοδος

```
Engine specifications:
- Power: 250kW
- Voltage: 400V
- Serial No: ABC12345
Safety warnings: ...
```

Αν δείτε ακατάστατους χαρακτήρες, ελέγξτε ξανά ότι το προσαρμοσμένο λεξικό σας περιλαμβάνει τους ελλιπείς όρους και ότι η εικόνα δεν είναι υπερβολικά θορυβώδης.

## Διαχείριση Ακραίων Περιπτώσεων & Συνηθισμένων Παραλλαγών

| Κατάσταση | Πώς να το αντιμετωπίσετε |
|-----------|-------------------|
| **Καμπυλωμένη εικόνα** (κείμενο όχι τέλεια οριζόντιο) | Καλέστε `engine.getEngineOptions().setDeskewEnabled(true)`. |
| **Πολλαπλές γλώσσες** (π.χ., Αγγλικά + Γερμανικά) | Φορτώστε πρόσθετα πακέτα γλώσσας μέσω `engine.getEngineOptions().addLanguage(Language.German)`. |
| **Μεγάλα PDF μετατρεπόμενα σε εικόνες** | Διαιρέστε το PDF σε ξεχωριστές σελίδες πρώτα· εκτελέστε OCR ανά σελίδα για να διατηρήσετε τη χρήση μνήμης χαμηλή. |
| **Απουσία προσαρμοσμένου λεξικού** | Η μηχανή επιστρέφει στο ενσωματωμένο λεξικό της, το οποίο μπορεί να παραλείψει τεχνικούς όρους. Πάντα επαληθεύστε τη διαδρομή. |

## Συμβουλή Pro: Αποθήκευση Αποτελεσμάτων OCR ως Δομημένο Αρχείο

Αν χρειάζεστε κάτι παραπάνω από απλό κείμενο—π.χ., θέλετε να διατηρήσετε τη διάταξη—μπορείτε να σειριοποιήσετε το `OcrResult` σε JSON:  

```java
import com.aspose.ocr.internal.util.JsonUtils;

String json = JsonUtils.toJson(result);
Files.write(Paths.get("output.json"), json.getBytes(StandardCharsets.UTF_8));
```

Τώρα έχετε τόσο το ακατέργαστο κείμενο (**εξάγετε κείμενο από τεχνικό έγγραφο**) όσο και τα μεταδεδομένα για περαιτέρω ανάλυση.

## Συνοπτική Επισκόπηση

Καλύψαμε όλα όσα χρειάζεστε για να **αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR σε Java και να **εξάγετε κείμενο από τεχνικό έγγραφο** με ένα προσαρμοσμένο λεξικό. Η ροή είναι:

1. Δημιουργήστε το `OcrEngine`.
2. Κατευθύνετέ το σε ένα λεξικό χρήστη.
3. Φορτώστε την εικόνα-στόχο.
4. Καλέστε το `recognize()`.
5. Εξάγετε το `result.getText()`.

Με αυτά τα πέντε βήματα μπορείτε να αυτοματοποιήσετε την εισαγωγή δεδομένων από σχήματα, εγχειρίδια ή οποιαδήποτε τεχνική εικονογράφηση.

## Τι Ακολουθεί;

- Πειραματιστείτε με **προεπεξεργασία εικόνας** (βελτίωση αντίθεσης) για να βελτιώσετε την ακρίβεια σε σαρώσεις χαμηλής ποιότητας.
- Συνδυάστε το αποτέλεσμα OCR με το **Apache Tika** για να ευρετηριάσετε το εξαγόμενο κείμενο σε μια μηχανή αναζήτησης.
- Εξερευνήστε το **OCR με βάση περιοχές** αν χρειάζεστε μόνο συγκεκριμένα τμήματα ενός μεγάλου διαγράμματος.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε προβλήματα, ή να μοιραστείτε πώς προσαρμόσατε το λεξικό για τον δικό σας τομέα. Καλή προγραμματιστική!

## Σχετικά Μαθήματα

- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Οδηγός](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}