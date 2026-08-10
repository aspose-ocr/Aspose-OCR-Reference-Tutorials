---
category: general
date: 2026-06-28
description: Δημιουργήστε αναζητήσιμο PDF από ένα πολυσελίδες TIFF σε Java χρησιμοποιώντας
  το Aspose OCR. Μάθετε πώς να μετατρέψετε TIFF σε PDF και να προσθέσετε στρώση κειμένου
  OCR στο PDF για άμεση δυνατότητα αναζήτησης.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- add ocr text layer pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από εικόνα TIFF σε Java χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε TIFF σε PDF και να προσθέσετε
  στρώση κειμένου OCR στο PDF για αναζητήσιμα έγγραφα.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από TIFF με Aspose OCR (Java)
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  headline: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  type: TechArticle
- description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  name: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  steps:
  - name: What if my TIFF is single‑page?
    text: The same code works—Aspose treats a single‑page TIFF as a one‑element collection,
      so no extra handling is required.
  - name: Can I control the OCR language?
    text: 'Yes. Before calling `recognizeAndExportPdf`, set the language on the engine:'
  - name: How do I skip embedding the original image to reduce file size?
    text: Just set `pdfOptions.setEmbedOriginalImage(false)`. The PDF will contain
      only the searchable text layer, which dramatically shrinks the file but loses
      the visual representation.
  - name: Is the generated PDF truly searchable on all platforms?
    text: Modern PDF readers (Adobe Acrobat, Foxit, even browsers) honor the text
      layer. Some older, lightweight viewers might ignore it—test on your target platform
      if you’re unsure.
  type: HowTo
tags:
- Aspose OCR
- Java
- PDF Generation
title: Δημιουργία Αναζητήσιμου PDF από TIFF με Aspose OCR (Java) – Πλήρης Οδηγός
url: /el/java/ocr-operations/create-searchable-pdf-from-tiff-with-aspose-ocr-java-full-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από TIFF με Aspose OCR (Java) – Πλήρης Οδηγός

Έχετε ποτέ αναρωτηθεί πώς να **δημιουργήσετε αναζητήσιμο PDF** από ένα σκαναρισμένο TIFF χωρίς να ξοδεύετε ώρες παίζοντας με εργαλεία τρίτων; Δεν είστε μόνοι—οι προγραμματιστές χρειάζονται συνεχώς έναν αξιόπιστο τρόπο να μετατρέπουν μεγάλα αρχεία εικόνας σε PDF που μπορείτε πραγματικά να αναζητήσετε.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα μια πρακτική, ολοκληρωμένη λύση που όχι μόνο **μετατρέπει TIFF σε PDF** αλλά επίσης **προσθέτει στρώση κειμένου OCR PDF** αυτόματα, παρέχοντάς σας ένα πραγματικά αναζητήσιμο έγγραφο με λίγες μόνο γραμμές κώδικα Java.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR για Java και να εφαρμόσετε άδεια (προαιρετικό αλλά συνιστάται).  
- Τα ακριβή βήματα για **convert TIFF to PDF** χρησιμοποιώντας το `OcrEngine`.  
- Πώς να διαμορφώσετε το `PdfExportOptions` ώστε το παραγόμενο αρχείο να περιέχει ένα αόρατο, αναζητήσιμο στρώμα κειμένου—ακριβώς αυτό που σημαίνει **add OCR text layer PDF** στην πράξη.  
- Αναμενόμενο αποτέλεσμα και ένας γρήγορος έλεγχος για να βεβαιωθείτε ότι όλα λειτούργησαν.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· ένα βασικό περιβάλλον ανάπτυξης Java (JDK 8+ και οποιοδήποτε IDE) είναι επαρκές.

---

## Βήμα 1: Προετοιμάστε το Έργο σας και Εφαρμόστε την Άδεια Aspose OCR  

Πριν μπορέσετε να καλέσετε οποιοδήποτε OCR API, χρειάζεστε τα JAR του Aspose OCR στο classpath σας. Εάν έχετε εμπορική άδεια, τοποθετήστε το αρχείο `.lic` κάπου προσβάσιμο και υποδείξτε την κλάση `License` σε αυτό. Αυτό το βήμα δεν είναι αυστηρά υποχρεωτικό—το Aspose θα λειτουργήσει σε λειτουργία αξιολόγησης, αλλά η άδεια αφαιρεί τα υδατογραφήματα και ξεκλειδώνει το πλήρες σύνολο λειτουργιών.

```java
// Apply your Aspose OCR license (optional for full features)
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro tip:** Διατηρήστε το αρχείο άδειας εκτός του ελέγχου πηγής σας για να αποφύγετε τυχαία έκθεση.

---

## Βήμα 2: Δημιουργία του OCR Engine  

Η δημιουργία ενός αντικειμένου `OcrEngine` είναι το πρώτο πραγματικό βήμα προς την **create searchable pdf**. Η μηχανή κρατά όλες τις ρυθμίσεις OCR και θα οδηγήσει αργότερα τη μετατροπή.

```java
// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί ξεχωριστή μηχανή; Σας επιτρέπει να επαναχρησιμοποιήσετε την ίδια διαμόρφωση σε πολλά αρχεία, κάτι που είναι χρήσιμο όταν επεξεργάζεστε κατά παρτίδες δεκάδες TIFF.

---

## Βήμα 3: Φόρτωση του Πολυσελιδικού TIFF σας  

Το Aspose OCR κάνει τη φόρτωση ενός πολυσελιδικού TIFF παιχνιδάκι. Απλώς προσθέστε τη διαδρομή του αρχείου σε ένα αντικείμενο `OcrInput`; η βιβλιοθήκη ανιχνεύει αυτόματα και τοποθετεί σε ουρά κάθε σελίδα.

```java
// Load a multi‑page TIFF image as OCR input
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically
```

Αν ποτέ χρειαστείτε να **convert TIFF to PDF** μία σελίδα τη φορά, μπορείτε επίσης να καλέσετε `ocrInput.add(pageStream)` μέσα σε βρόχο—το Aspose θα θεωρήσει κάθε κλήση ως ξεχωριστή σελίδα.

---

## Βήμα 4: Διαμόρφωση Επιλογών Εξαγωγής PDF – Προσθήκη του OCR Text Layer  

Εδώ συμβαίνει η μαγεία για **add OCR text layer pdf**. Με την εναλλαγή μερικών σημαιών λέτε στο Aspose να ενσωματώσει το αρχικό bitmap (ώστε η οπτική πιστότητα να παραμείνει αμετάβλητη) *και* να δημιουργήσει ένα κρυφό στρώμα κειμένου που οι μηχανές αναζήτησης μπορούν να ευρετηριάσουν.

```java
// Configure PDF export options
PdfExportOptions pdfOptions = new PdfExportOptions();
pdfOptions.setEmbedOriginalImage(true);      // keep the bitmap as background
pdfOptions.setCreateSearchablePdf(true);     // generate hidden text layer for search
pdfOptions.setAuthor("John Doe");
pdfOptions.setTitle("OCR Output");
```

- `setEmbedOriginalImage(true)`: εξασφαλίζει ότι το PDF φαίνεται ακριβώς όπως η σκαναρισμένη εικόνα.  
- `setCreateSearchablePdf(true)`: δημιουργεί το αόρατο επικάλυμμα κειμένου—αυτό είναι ο πυρήνας του **add OCR text layer pdf**.  

Μη διστάσετε να εμπλουτίσετε τα μεταδεδομένα (author, title, subject) όπως φαίνεται· βοηθά στη διαχείριση εγγράφων αργότερα.

---

## Βήμα 5: Εκτέλεση OCR και Εξαγωγή του Αναζητήσιμου PDF  

Τώρα ενώνουμε όλα τα κομμάτια. Η μέθοδος `recognizeAndExportPdf` κάνει τη σκληρή δουλειά: εκτελεί OCR σε κάθε σελίδα TIFF, γράφει την οπτική εικόνα και προσθέτει το αναζητήσιμο κείμενο.

```java
// Perform OCR recognition and export the result as a searchable PDF
ocrEngine.recognizeAndExportPdf(
    ocrInput,
    "YOUR_DIRECTORY/searchable.pdf",
    pdfOptions
);

System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
```

Όταν η κονσόλα εμφανίσει το μήνυμα επιτυχίας, έχετε μόλις **create searchable pdf** από ένα αρχείο TIFF. Ανοίξτε το παραγόμενο `searchable.pdf` σε οποιονδήποτε προβολέα PDF, πατήστε `Ctrl+F` και δοκιμάστε να αναζητήσετε μια λέξη που εμφανίζεται στην αρχική εικόνα—θα πρέπει να βρεθεί αμέσως.

---

## Επαλήθευση του Αποτελέσματος – Γρήγορη Λίστα Ελέγχου  

1. **Visual fidelity** – Το PDF πρέπει να φαίνεται ακριβώς όπως το πηγαίο TIFF (ευχαριστώντας το `setEmbedOriginalImage`).  
2. **Searchability** – Χρησιμοποιήστε τη λειτουργία αναζήτησης του προβολέα· το κρυφό στρώμα κειμένου πρέπει να επιστρέφει αποτελέσματα.  
3. **Metadata** – Ανοίξτε τις ιδιότητες του PDF για να επιβεβαιώσετε τον author και τον τίτλο που ορίσατε νωρίτερα.  

Αν κάποιος από αυτούς τους ελέγχους αποτύχει, ελέγξτε ξανά ότι το `setCreateSearchablePdf(true)` είναι ενεργοποιημένο και ότι η άδειά σας (αν υπάρχει) δεν βρίσκεται σε λειτουργία αξιολόγησης με περιορισμούς.

---

## Ειδικές Περιπτώσεις & Συχνές Ερωτήσεις  

### Τι γίνεται αν το TIFF μου είναι μονό‑σελίδα;  

Ο ίδιος κώδικας λειτουργεί—το Aspose αντιμετωπίζει ένα μονό‑σελίδα TIFF ως μια συλλογή ενός στοιχείου, οπότε δεν απαιτείται επιπλέον διαχείριση.

### Μπορώ να ελέγξω τη γλώσσα OCR;  

Ναι. Πριν καλέσετε το `recognizeAndExportPdf`, ορίστε τη γλώσσα στη μηχανή:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.English);
```

Αντικαταστήστε το `English` με οποιοδήποτε υποστηριζόμενο enum γλώσσας.

### Πώς μπορώ να παραλείψω την ενσωμάτωση της αρχικής εικόνας για να μειώσω το μέγεθος του αρχείου;  

Απλώς ορίστε `pdfOptions.setEmbedOriginalImage(false)`. Το PDF θα περιέχει μόνο το αναζητήσιμο στρώμα κειμένου, το οποίο μειώνει δραστικά το μέγεθος του αρχείου αλλά χάνει την οπτική αναπαράσταση.

### Είναι το παραγόμενο PDF πραγματικά αναζητήσιμο σε όλες τις πλατφόρμες;  

Οι σύγχρονοι προβολείς PDF (Adobe Acrobat, Foxit, ακόμη και browsers) σέβονται το στρώμα κειμένου. Κάποιοι παλαιότεροι, ελαφροί προβολείς μπορεί να το αγνοήσουν—δοκιμάστε στην πλατφόρμα-στόχο σας αν δεν είστε σίγουροι.

---

## Πλήρες Παράδειγμα Λειτουργίας  

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Αντικαταστήστε τις διαδρομές placeholder με πραγματικές, προσθέστε τα JAR του Aspose OCR στο έργο σας και τρέξτε.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license (optional for full features)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load a multi‑page TIFF image as OCR input
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically

        // Step 4: Configure PDF export options
        PdfExportOptions pdfOptions = new PdfExportOptions();
        pdfOptions.setEmbedOriginalImage(true);    // keep the bitmap as background
        pdfOptions.setCreateSearchablePdf(true);   // generate hidden text layer for search
        pdfOptions.setAuthor("John Doe");
        pdfOptions.setTitle("OCR Output");

        // Step 5: Perform OCR recognition and export the result as a searchable PDF
        ocrEngine.recognizeAndExportPdf(
            ocrInput,
            "YOUR_DIRECTORY/searchable.pdf",
            pdfOptions
        );

        System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Αναμενόμενο αποτέλεσμα (κονσόλα):**

```
Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf
```

Ανοίξτε το `searchable.pdf` και δοκιμάστε να αναζητήσετε οποιαδήποτε λέξη που εμφανίζεται στο αρχικό TIFF—να και, έχετε επιτυχώς **create searchable pdf**!

---

## Συμπέρασμα  

Μόλις περάσαμε από έναν πλήρη, έτοιμο για παραγωγή τρόπο για **create searchable PDF** από TIFF χρησιμοποιώντας το Aspose OCR για Java. Διαμορφώνοντας το `PdfExportOptions` προσθέτετε αυτόματα **add OCR text layer PDF**, μετατρέποντας στατικές εικόνες σε άμεσα αναζητήσιμα έγγραφα.

Αν είστε έτοιμοι να προχωρήσετε παραπέρα, σκεφτείτε να πειραματιστείτε με:

- **convert TIFF to PDF** με προσαρμοσμένα μεγέθη σελίδας ή ρυθμίσεις DPI.  
- Προσθήκη υδατογραφιών ή ψηφιακών υπογραφών μετά το OCR.  
- Επεξεργασία κατά παρτίδες ενός φακέλου TIFF με έναν απλό βρόχο `for`.  

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στις ίδιες βασικές έννοιες που καλύψαμε, οπότε η μετάβαση θα είναι ομαλή.

Έχετε ερωτήσεις ή αντιμετωπίζετε προβλήματα; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [OCR Αναγνώριση Εγγράφων PDF στο Aspose.OCR για Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Πώς να κάνετε OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}