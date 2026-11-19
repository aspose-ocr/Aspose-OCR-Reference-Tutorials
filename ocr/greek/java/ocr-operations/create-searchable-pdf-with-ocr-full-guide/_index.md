---
category: general
date: 2026-06-22
description: Δημιουργήστε αναζητήσιμο PDF χρησιμοποιώντας OCR σε Java. Μάθετε πώς
  να απενεργοποιήσετε τη συμπίεση και να μετατρέψετε ένα PDF με σαρωμένη εικόνα σε
  αναζητήσιμο PDF γρήγορα.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης χρησιμοποιώντας OCR σε Java.
  Αυτός ο οδηγός δείχνει πώς να απενεργοποιήσετε τη συμπίεση, να μετατρέψετε PDF σαρωμένης
  εικόνας και να δημιουργήσετε PDF χωρίς συμπίεση.
og_title: Δημιουργία Αναζητήσιμου PDF με OCR – Πλήρες Μάθημα Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Δημιουργία PDF με δυνατότητα αναζήτησης μέσω OCR – Πλήρης οδηγός
url: /el/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με OCR – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **create searchable PDF** από μια δέσμη σαρωμένων εικόνων αλλά δεν ήσασταν σίγουροι ποιες ρυθμίσεις να αλλάξετε; Δεν είστε οι μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν το αποτέλεσμα καταλήγει σε ένα τεράστιο, μη αναγνώσιμο μπλοκ.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα καθαρό, end‑to‑end παράδειγμα που δείχνει ακριβώς πώς να **create searchable PDF** χρησιμοποιώντας μια Java OCR μηχανή, **convert scanned image PDF**, και, κυρίως, **how to disable compression** ώστε το τελικό αρχείο να διατηρεί τις αρχικές διαστάσεις. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα και μια σαφή κατανόηση του γιατί κάθε ρύθμιση είναι σημαντική.

## Τι Θα Μάθετε

* Πώς να ρυθμίσετε τη μηχανή OCR για **ocr to searchable pdf**.  
* Τον λόγο για την απενεργοποίηση της συμπίεσης PDF και πώς να αποκτήσετε ένα **pdf without compression**.  
* Ένα πλήρες πρόγραμμα Java που παίρνει μια σαρωμένη εικόνα, εκτελεί OCR και αποθηκεύει ένα **searchable PDF**.  
* Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως σαρώσεις πολλαπλών σελίδων ή πηγές χαμηλής ανάλυσης.  

**Prerequisites** – Java 8+ εγκατεστημένο, ένα συμβατό OCR SDK (ο κώδικας χρησιμοποιεί το ABBYY FineReader Engine API, αλλά οι έννοιες ισχύουν για οποιαδήποτε βιβλιοθήκη που προσφέρει `setOutputFormat` και `setPdfCompression`). Ένα IDE όπως το IntelliJ IDEA ή το Eclipse θα κάνει τη δουλειά πιο εύκολη, αλλά λειτουργεί και ένας απλός επεξεργαστής κειμένου.

---

![Δημιουργία αναζητήσιμου PDF workflow](image-placeholder.png "Διάγραμμα που δείχνει τη διαδικασία δημιουργίας αναζητήσιμου pdf από σαρωμένες εικόνες σε τελικό PDF")

## Βήμα 1: Ορίστε τη Μηχανή OCR σε **Create Searchable PDF**

Το πρώτο που πρέπει να πείτε στη μηχανή OCR είναι τι είδους έξοδος περιμένετε. Από προεπιλογή πολλές SDK παράγουν απλό κείμενο ή raster PDF, το οποίο δεν είναι αναζητήσιμο. Η αλλαγή της μορφής κάνει το δύσκολο μέρος για εσάς.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Γιατί είναι σημαντικό*: Η σημαία `PDF_SEARCHABLE` υποδεικνύει στη μηχανή να ενσωματώσει ένα αόρατο στρώμα κειμένου κάτω από τη σαρωμένη εικόνα. Τα εργαλεία αναζήτησης μπορούν τότε να ευρετηριάσουν το έγγραφο, κάνοντάς το να συμπεριφέρεται όπως οποιοδήποτε φυσικό PDF που ανοίγετε στο Adobe Reader.

## Βήμα 2: Απενεργοποίηση Συμπίεσης – **How to Disable Compression** Σωστά

Αν παραλείψετε αυτό το βήμα, η μηχανή θα συμπιέσει κάθε σελίδα για εξοικονόμηση χώρου, αλλά η συμπίεση μπορεί να θολώσει λεπτομερείς λεπτομέρειες—ιδιαίτερα προβληματικό όταν χρειάζεται να εξάγετε εικόνες υψηλής ανάλυσης.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro tip**: Η απενεργοποίηση της συμπίεσης είναι απαραίτητη όταν σκοπεύετε να αρχειοθετήσετε νομικά έγγραφα ή ιατρικές σαρώσεις όπου κάθε pixel μετρά. Το αποτέλεσμα μπορεί να είναι μεγαλύτερο, αλλά διατηρείτε τις αρχικές διαστάσεις και την καθαρότητα.

## Βήμα 3: Εκτελέστε OCR και Λάβετε το Αποτέλεσμα

Τώρα που η μηχανή ξέρει τι να εξάγει και πώς να χειριστεί τις εικόνες, μπορείτε να τρέξετε την αναγνώριση. Η κλήση επιστρέφει ένα αντικείμενο `PdfDocument` έτοιμο για αποθήκευση ή περαιτέρω επεξεργασία.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Τι συμβαίνει στο παρασκήνιο;* Η μηχανή επεξεργάζεται κάθε εισερχόμενη σελίδα, εκτελεί αναγνώριση χαρακτήρων και ενώνει το κρυφό στρώμα κειμένου με την εικόνα. Αν έχετε πολλαπλές σελίδες, αυτές συνενώνονται αυτόματα.

## Βήμα 4: Αποθηκεύστε το **Searchable PDF** στον Δίσκο

Τέλος, γράψτε το PDF που βρίσκεται στη μνήμη σε ένα αρχείο. Επιλέξτε μια θέση όπου έχετε δικαιώματα εγγραφής και δώστε στο αρχείο ένα περιγραφικό όνομα.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Όταν ανοίξετε το `searchable.pdf` σε έναν προβολέα, θα δείτε ότι μπορείτε να επιλέξετε και να αναζητήσετε το κείμενο—παρόλο που το ορατό περιεχόμενο παραμένει η αρχική σαρωμένη εικόνα.

### Πλήρες Παράδειγμα Εργασίας

Παρακάτω υπάρχει μια αυτόνομη κλάση Java που ενώνει και τα τέσσερα βήματα. Αντιγράψτε‑και‑επικολλήστε, προσαρμόστε τη διαδρομή εισόδου και τρέξτε το όπως είναι.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Αναμενόμενο αποτέλεσμα** – Μετά την εκτέλεση του προγράμματος θα δείτε το μήνυμα στην κονσόλα και το αρχείο `searchable.pdf` θα εμφανιστεί στο `YOUR_DIRECTORY`. Ανοίγοντάς το σε οποιονδήποτε PDF reader θα μπορείτε:

* Να επισημάνετε κείμενο.  
* Να χρησιμοποιήσετε την ενσωματωμένη αναζήτηση (Ctrl + F) για να βρείτε λέξεις.  
* Να εξάγετε το κρυφό στρώμα κειμένου αν χρειαστεί.

---

## Γιατί Να Απενεργοποιήσετε τη Συμπίεση; Κατανόηση **PDF Without Compression**

Μπορεί να αναρωτιέστε, “Δεν είναι πάντα η συμπίεση καλή ιδέα;” Η απάντηση είναι πιο σύνθετη:

| Κατάσταση | Διατήρηση Συμπίεσης (`NORMAL`) | Απενεργοποίηση Συμπίεσης (`NONE`) |
|-----------|-------------------------------|-----------------------------------|
| Αρχειοθέτηση νομικών συμβάσεων | ❌ Μπορεί να αλλοιώσει την πιστότητα των pixel | ✅ Εγγυάται την αρχική εμφάνιση |
| Μεγάλη δέσμη χαμηλής ανάλυσης σαρώσεων | ✅ Εξοικονομεί χώρο | ❌ Αυξάνει το μέγεθος χωρίς όφελος |
| Απαίτηση ακρίβειας OCR σε μικρές γραμματοσειρές | ❌ Θολώνει λεπτομέρειες | ✅ Διατηρεί κάθε στίγμα |

Με λίγα λόγια, το **how to disable compression** είναι μια ισοτιμία μεταξύ αποθήκευσης και πιστότητας. Για τις περισσότερες ροές εργασίας αναζητήσιμου PDF όπου σκοπός είναι η αναζήτηση κειμένου και όχι η εκτύπωση των εικόνων, η απενεργοποίηση της συμπίεσης είναι η πιο ασφαλής επιλογή.

## Μετατροπή **Scanned Image PDF** Απευθείας

Μερικές φορές έχετε ήδη ένα PDF που περιέχει μόνο σαρωμένες εικόνες (ένα “image‑only PDF”). Για να **convert scanned image pdf** σε αναζητήσιμη έκδοση, μπορείτε να περάσετε ολόκληρο το PDF στη μηχανή αντί για μεμονωμένες εικόνες:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Οι ίδιες σημαίες ρύθμισης (`PDF_SEARCHABLE` και `PdfCompression.NONE`) ισχύουν, έτσι λαμβάνετε ένα **pdf without compression** ακόμη και όταν ξεκινάτε από ένα PDF container.

## Συνηθισμένα Λάθη & Πώς να τα Αποφύγετε

* **Ξεχάσατε να ορίσετε τη μορφή εξόδου** – Η μηχανή προεπιλογή είναι raster PDF, το οποίο δεν είναι αναζητήσιμο. Πάντα καλέστε `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` πριν από `recognizeToPdf()`.  
* **Έλλειψη μνήμης σε μεγάλες δέσμες** – Φορτώστε και επεξεργαστείτε τις σελίδες σε τμήματα, ή χρησιμοποιήστε το streaming API αν το SDK το παρέχει.  
* **Λανθασμένες διαδρομές αρχείων** – Χρησιμοποιήστε απόλυτες διαδρομές ή βεβαιωθείτε ότι το working directory είναι σωστό· διαφορετικά το `pdf.save()` πετάει `IOException`.  
* **Μη ενεργοποιημένη άδεια** – Τα περισσότερα εμπορικά OCR SDK απαιτούν έγκυρη άδεια· η μηχανή θα πετάξει runtime exception αν λείπει.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη προς εκτέλεση λύση που δείχνει **how to create searchable PDF** από σαρωμένες εικόνες, πώς να **convert scanned image PDF**, και ακριβώς **how to disable compression** για την παραγωγή ενός **pdf without compression**. Τα βασικά βήματα είναι:

1. Ορίστε τη μορφή εξόδου σε `PDF_SEARCHABLE`.  
2. Απενεργοποιήστε τη συμπίεση PDF με `PdfCompression.NONE`.  
3. Εκτελέστε OCR και λάβετε το `PdfDocument`.  
4. Αποθηκεύστε το αρχείο στον δίσκο.

Από εδώ μπορείτε να πειραματιστείτε με γραμματοσειρές, να προσθέσετε υδατογραφήματα ή να επεξεργαστείτε ολόκληρους φακέλους μαζικά. Αν σας ενδιαφέρει η προσθήκη πακέτων γλώσσας OCR, η διαχείριση multi‑page TIFF ή η ενσωμάτωση αυτής της ροής εργασίας σε web service, δείτε τα επερχόμενα tutorials μας για “OCR language selection in Java” και “Streaming OCR for large document sets”.

Έχετε ερωτήσεις ή εντοπίσατε κάποιο πρόβλημα; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική και απολαύστε τα νέα σας αναζητήσιμα PDFs!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Αναγνώριση Κειμένου PDF – Λειτουργίες OCR με Aspose.OCR για Java](/ocr/english/java/ocr-operations/)
- [OCR Αναγνώριση Εγγράφων PDF σε Aspose.OCR για Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Μετατροπή Εικόνων σε PDF C# – Αποθήκευση Πολυσελιδικού Αποτελέσματος OCR](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}