---
category: general
date: 2026-01-02
description: Δημιουργήστε αναζητήσιμο PDF από ένα σκαναρισμένο PDF εικόνας χρησιμοποιώντας
  το Aspose OCR. Μάθετε πώς να ορίσετε τη γλώσσα OCR, να ενσωματώσετε ένα στρώμα κειμένου
  PDF και να εφαρμόσετε επιλογές υψηλής συμπίεσης PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: el
og_description: Δημιουργήστε γρήγορα PDF με δυνατότητα αναζήτησης. Αυτός ο οδηγός
  δείχνει πώς να μετατρέψετε ένα PDF σκαναρισμένης εικόνας, να ενσωματώσετε μια στρώση
  κειμένου, να ορίσετε τη γλώσσα OCR και να ενεργοποιήσετε την υψηλή συμπίεση PDF.
og_title: Δημιουργία Αναζητήσιμου PDF με Aspose OCR – Πλήρης Οδηγός
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Δημιουργία Αναζητήσιμου PDF με Aspose OCR – Οδηγός Βήμα‑προς‑Βήμα
url: /el/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF – Πλήρες Πρόγραμμα Εκμάθησης

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από σαρωμένες εικόνες αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Σε πολλές ροές εργασίας με πολλά έγγραφα, ένα απλό PDF μόνο με εικόνες είναι αδιέξοδο για αναζήτηση και ευρετηρίαση.  

Τα καλά νέα είναι ότι με το Aspose OCR μπορείτε να **μετατρέψετε σαρωμένο PDF εικόνας** σε πλήρως αναζητήσιμο έγγραφο με λίγες μόνο γραμμές Java. Αυτό το tutorial σας οδηγεί βήμα‑βήμα—από την εκκίνηση της μηχανής OCR, τη ρύθμιση επιλογών υψηλής συμπίεσης PDF, την ενσωμάτωση κρυφού στρώματος κειμένου, έως την επιλογή της κατάλληλης γλώσσας OCR.

Στο τέλος αυτού του οδηγού θα έχετε ένα εκτελέσιμο πρόγραμμα που παράγει ένα αναζητήσιμο PDF, ένα αρχείο που μπορείτε να ενσωματώσετε σε οποιαδήποτε μηχανή αναζήτησης ή σύστημα διαχείρισης εγγράφων χωρίς προβλήματα.

---

## Δημιουργία Αναζητήσιμου PDF – Επισκόπηση

Πριν βουτήξουμε στον κώδικα, ας διευκρινίσουμε τι σημαίνει πραγματικά “δημιουργία αναζητήσιμου PDF”. Ένα αναζητήσιμο PDF περιέχει δύο παράλληλα στρώματα:

1. **Οπτικό στρώμα** – η αρχική σαρωμένη εικόνα (ή η σελίδα που αποδόθηκε).  
2. **Στρώμα κειμένου** – αόρατοι αλλά μηχανικά αναγνώσιμοι χαρακτήρες που εξάγονται από το OCR.

Όταν ανοίγετε ένα τέτοιο PDF στο Adobe Reader και επιλέγετε κείμενο, στην πραγματικότητα αλληλεπιδράτε με το κρυφό στρώμα κειμένου, όχι με την εικόνα. Αυτή η διπλή προσέγγιση είναι αυτή που επιτρέπει τη λειτουργία **ενσωμάτωσης στρώματος κειμένου PDF**.

---

## Μετατροπή Σαρωμένου PDF Εικόνας με Aspose OCR

Το πρώτο πράγμα που χρειάζεστε είναι μια σαρωμένη εικόνα (PNG, JPEG, TIFF) που θέλετε να μετατρέψετε σε PDF. Το Aspose OCR μπορεί να διαβάσει αυτήν την εικόνα, να εκτελέσει OCR και να παραδώσει το αποτέλεσμα σε έναν δημιουργό PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Γιατί λειτουργεί:**  
- `setCreateSearchablePdf(true)` λέει στο Aspose να δημιουργήσει το κρυφό στρώμα κειμένου, ικανοποιώντας την απαίτηση **ενσωμάτωσης στρώματος κειμένου pdf**.  
- `setCompressionLevel(9)` μετακινεί το αρχείο στην περιοχή **υψηλής συμπίεσης pdf**, μειώνοντας το τελικό μέγεθος χωρίς να θυσιάζει την ακρίβεια του OCR.  
- Η παράμετρος `RecognitionLanguage.ENGLISH` δείχνει πώς να **ρυθμίσετε τη γλώσσα OCR**· μπορείτε να την αλλάξετε σε Γαλλικά, Γερμανικά κ.λπ., ανάλογα με το υλικό σας.

---

## Ρυθμίσεις Υψηλής Συμπίεσης PDF

Τα μεγάλα σαρωμένα PDF μπορούν γρήγορα να φτάσουν σε εκατοντάδες megabytes. Το Aspose προσφέρει ένα απλό API συμπίεσης που λειτουργεί σε επίπεδο PDF. Η μέθοδος `setCompressionLevel` δέχεται τιμές από 0 (χωρίς συμπίεση) έως 9 (μέγιστη συμπίεση).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Μερικές συμβουλές:

- **Χρησιμοποιήστε μορφές εικόνας χωρίς απώλειες** (PNG) για σαρώσεις με πολύ κείμενο· το JPEG είναι καλύτερο για φωτογραφίες.  
- **Ενεργοποιήστε το υποσύνολο γραμματοσειρών** αν ενσωματώνετε προσαρμοσμένες γραμματοσειρές—το Aspose το κάνει αυτό αυτόματα όταν δημιουργείτε ένα αναζητήσιμο PDF.  
- **Δοκιμάστε το μέγεθος εξόδου** μετά από κάθε αλλαγή· μερικές φορές η συμπίεση επιπέδου 8 προσφέρει μείωση 10 % του μεγέθους με ελάχιστη απώλεια ποιότητας σε σύγκριση με το επίπεδο 9.

---

## Ενσωμάτωση Στρώματος Κειμένου PDF για Αναζητησιμότητα

Αν παραλείψετε την κλήση `setCreateSearchablePdf(true)`, το παραγόμενο αρχείο θα φαίνεται εντάξει αλλά δεν θα μπορείτε να αναζητήσετε το περιεχόμενό του. Το κρυφό στρώμα κειμένου δημιουργείται αντιστοιχίζοντας κάθε αναγνωρισμένο χαρακτήρα στη θέση του στη σελίδα.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Τι πρέπει να προσέξετε:**  

- **Έγγραφα μικτής γλώσσας** – ίσως χρειαστεί να εκτελέσετε OCR δύο φορές, μία ανά γλώσσα, και στη συνέχεια να συγχωνεύσετε τα στρώματα κειμένου.  
- **Πολύπλοκες διατάξεις** (πίνακες, πολλαπλές στήλες) – το Aspose κάνει καλή δουλειά, αλλά ελέγξτε το αποτέλεσμα με έναν προβολέα PDF που εμφανίζει κρυφό κείμενο (π.χ., τη λειτουργία “Edit PDF” του Adobe Acrobat).

---

## Ρύθμιση Γλώσσας OCR για Ακριβή Αναγνώριση

Η ακρίβεια της μηχανής OCR εξαρτάται από τη γλώσσα που της δηλώνετε. Το Aspose παρέχει ένα σύνολο ενσωματωμένων γλωσσών και μπορείτε επίσης να προσθέσετε προσαρμοσμένα πακέτα γλωσσών.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Πότε να αλλάξετε τη γλώσσα:**  

- Τα έγγραφα περιέχουν **μη λατινικούς χαρακτήρες** (Κυριλλικό, Αραβικό) – μεταβείτε στην κατάλληλη `RecognitionLanguage`.  
- Σε σελίδες με μικτές γλώσσες – μπορείτε να καλέσετε το `recognizeImageAndSave` δύο φορές, κάθε φορά με διαφορετική γλώσσα, και στη συνέχεια να συγχωνεύσετε τα PDF.

---

## Εκτέλεση του Πλήρους Παραδείγματος

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντικαταστήστε τις διαδρομές placeholder με πραγματικές τοποθεσίες αρχείων, βεβαιωθείτε ότι το Aspose OCR JAR βρίσκεται στο classpath σας, και εκτελέστε.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Αναμενόμενη έξοδος:** Όταν τρέξετε το πρόγραμμα, η κονσόλα εμφανίζει:

```
Searchable PDF created.
```

Ανοίξτε το `searchable.pdf` σε οποιονδήποτε προβολέα PDF, δοκιμάστε να επιλέξετε κείμενο και θα δείτε το αόρατο στρώμα σε δράση. Έχετε δημιουργήσει επιτυχώς **αναζητήσιμο pdf** από μια σαρωμένη εικόνα.

---

![παράδειγμα δημιουργίας αναζητήσιμου pdf](image-placeholder.png "παράδειγμα δημιουργίας αναζητήσιμου pdf")

*Το παραπάνω στιγμιότυπο (placeholder) θα έδειχνε συνήθως τον προβολέα PDF με δυνατότητα επιλογής κειμένου πάνω από μια σαρωμένη σελίδα.*

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **δημιουργήσετε αναζητήσιμο PDF** χρησιμοποιώντας το Aspose OCR:

- Εκκίνηση της μηχανής OCR.  
- **Μετατροπή σαρωμένου PDF εικόνας** τροφοδοτώντας ένα PNG/JPEG στο `recognizeImageAndSave`.  
- Χρήση του `setCreateSearchablePdf(true)` για **ενσωμάτωση στρώματος κειμένου PDF**.  
- Εφαρμογή του `setCompressionLevel(9)` για ένα **υψηλής συμπίεσης PDF** που παραμένει ελαφρύ.  
- Επιλογή της σωστής `RecognitionLanguage` για **ρύθμιση γλώσσας OCR** με μέγιστη ακρίβεια.

Από εδώ μπορείτε να πειραματιστείτε με επεξεργασία παρτίδας, διαφορετικές γλώσσες ή ακόμη και να συνδυάσετε πολλές σαρωμένες σελίδες σε ένα ενιαίο αναζητήσιμο PDF. Το ίδιο μοτίβο λειτουργεί και για άλλες γλώσσες όπως Ισπανικά ή Ιαπωνικά—απλώς αλλάξτε το enum `RecognitionLanguage`.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε κάποιο πρόβλημα, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}