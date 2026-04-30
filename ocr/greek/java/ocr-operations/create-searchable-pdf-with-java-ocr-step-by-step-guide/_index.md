---
category: general
date: 2026-04-29
description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένα αρχεία χρησιμοποιώντας Java
  OCR. Μάθετε πώς να μετατρέψετε σαρωμένα PDF, να επεξεργαστείτε σαρωμένα έγγραφα
  και να δημιουργήσετε γρήγορα αναζητήσιμο PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- java pdf ocr
- process scanned documents
- make searchable pdf
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης χρησιμοποιώντας Java OCR.
  Αυτός ο οδηγός δείχνει πώς να μετατρέψετε σαρωμένα PDF, να επεξεργαστείτε σαρωμένα
  έγγραφα και να δημιουργήσετε PDF με δυνατότητα αναζήτησης αποδοτικά.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης με Java OCR – Πλήρης οδηγός
tags:
- PDF
- OCR
- Java
title: Δημιουργία PDF με δυνατότητα αναζήτησης με Java OCR – Οδηγός βήμα‑βήμα
url: /el/java/ocr-operations/create-searchable-pdf-with-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF με δυνατότητα αναζήτησης με Java OCR – Οδηγός βήμα‑βήμα

Έχετε ποτέ χρειαστεί να **δημιουργήσετε PDF με δυνατότητα αναζήτησης** από ένα σωρό σαρωμένων εικόνων αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν αντιμετωπίζουν για πρώτη φορά την ψηφιοποίηση αρχείων χαρτιού. Τα καλά νέα είναι ότι με μερικές γραμμές Java και Aspose OCR μπορείτε να **μετατρέψετε σαρωμένο PDF** σε ένα πλήρως αναζητήσιμο έγγραφο σε λίγα λεπτά.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την εγκατάσταση της βιβλιοθήκης, την επιλογή του αρχείου προέλευσης, τη ρύθμιση των παραμέτρων απόδοσης, μέχρι την τελική επαλήθευση ότι το αποτέλεσμα είναι πραγματικά *αναζητήσιμο*. Στο τέλος θα ξέρετε πώς να **επεξεργάζεστε σαρωμένα έγγραφα** μαζικά και ακόμη πώς να **δημιουργήσετε PDF με δυνατότητα αναζήτησης** που λειτουργούν άψογα με τη λειτουργία αναζήτησης οποιουδήποτε PDF viewer.

## Τι Θα Μάθετε

* Πώς να εγκαταστήσετε και να εισάγετε το πακέτο Aspose OCR for Java.  
* Ο ακριβής κώδικας που απαιτείται για **δημιουργία PDF με δυνατότητα αναζήτησης** από μια σαρωμένη πηγή.  
* Γιατί η ενεργοποίηση της επιτάχυνσης GPU και των παράλληλων νημάτων μπορεί να μειώσει λεπτά από μεγάλες εργασίες παρτίδας.  
* Συμβουλές για τη διαχείριση ειδικών περιπτώσεων—όπως PDF που περιέχουν μικτές σελίδες εικόνας/κειμένου ή εκτελούνται σε μηχανές χωρίς GPU.  

Δεν απαιτείται προηγούμενη εμπειρία OCR· χρειάζεται μόνο μια βασική εγκατάσταση Java και περιέργεια για το πώς να μετατρέψετε το χαρτί σε κείμενο αναζητήσιμο.

---

## Δημιουργία PDF με δυνατότητα αναζήτησης – Επισκόπηση

Πριν βουτήξουμε στον κώδικα, ας διευκρινίσουμε το πρόβλημα που λύνουμε. Ένα *σαρωμένο PDF* είναι ουσιαστικά μια συλλογή εικόνων· το κείμενο που βλέπετε στην οθόνη δεν είναι πραγματικοί χαρακτήρες, έτσι μια κανονική λειτουργία «εύρεση» δεν επιστρέφει τίποτα. Εκτελώντας OCR (Optical Character Recognition) σε κάθε σελίδα, ενσωματώνουμε ένα κρυφό στρώμα κειμένου διατηρώντας την αρχική εικόνα—αυτό είναι που κάνει το PDF *αναζητήσιμο*.

Σκεφτείτε το σαν να δίνετε στο PDF σας ένα «μυαλό» που μπορεί να διαβάσει τις λέξεις που εμφανίζει. Η βιβλιοθήκη Aspose OCR κάνει το βαρέως τύπου έργο: αναλύει το bitmap, εξάγει χαρακτήρες Unicode και τα γράφει πίσω στη δομή του PDF.

---

## Μετατροπή σαρωμένου PDF – Προετοιμασία του περιβάλλοντος

### 1. Προσθήκη της εξάρτησης Aspose OCR

Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας. (Οι χρήστες Gradle μπορούν να προσαρμόσουν τις συντεταγμένες αναλόγως.)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Pro tip:** Χρησιμοποιείτε πάντα την πιο πρόσφατη σταθερή έκδοση· οι νεότερες κυκλοφορίες προσφέρουν βελτιώσεις απόδοσης και καλύτερη υποστήριξη γλωσσών.

### 2. Επαλήθευση έκδοσης Java

Η Aspose OCR απαιτεί Java 8 ή νεότερη. Εκτελέστε `java -version` στο τερματικό—αν δείτε 1.8 ή μεταγενέστερη, είστε έτοιμοι.

---

## Java PDF OCR – Διαμόρφωση του μετατροπέα

Τώρα που η βιβλιοθήκη βρίσκεται στο classpath, μπορούμε να αρχίσουμε να γράφουμε το πρόγραμμα Java που θα **δημιουργήσει PDF με δυνατότητα αναζήτησης**. Παρακάτω υπάρχει ανάλυση γραμμή‑προς‑γραμμή κάθε τμήματος.

### Step 1: Ορισμός διαδρομών προέλευσης και προορισμού

```java
// Step 1: Specify the input scanned PDF and the output searchable PDF
String sourcePdfPath = "YOUR_DIRECTORY/input.pdf";
String searchablePdfPath = "YOUR_DIRECTORY/searchable_output.pdf";
```

*Γιατί;* Η μηχανή OCR χρειάζεται να ξέρει πού να διαβάσει το PDF μόνο‑εικόνας (`sourcePdfPath`) και πού να γράψει το νέο αρχείο που περιέχει το κρυφό στρώμα κειμένου (`searchablePdfPath`). Κρατήστε τις διαδρομές απόλυτες ή σχετικές με τη ρίζα του έργου· απλώς αποφύγετε κενά ή ειδικούς χαρακτήρες που θα μπορούσαν να μπερδέψουν το σύστημα αρχείων.

### Step 2: Δημιουργία του μετατροπέα

```java
// Step 2: Create the OCR converter and assign source/destination files
PdfOcrConverter ocrConverter = new PdfOcrConverter();
ocrConverter.setSourcePdf(sourcePdfPath);
ocrConverter.setDestinationPdf(searchablePdfPath);
```

`PdfOcrConverter` είναι η κεντρική κλάση που οργανώνει τη διαδικασία OCR. Καλώντας `setSourcePdf` και `setDestinationPdf` συνδέουμε την είσοδο με την έξοδο. Αν παραλείψετε κάποιο από τα δύο, η βιβλιοθήκη θα ρίξει `IllegalArgumentException` κατά την εκτέλεση—για αυτό ελέγξτε ξανά αυτές τις γραμμές.

### Step 3: (Προαιρετικό) Βελτίωση απόδοσης με GPU & νήματα

```java
// Step 3: (Optional) Enable GPU acceleration and set parallel processing
ocrConverter.getProcessingSettings().setUseGpu(true);
ocrConverter.getProcessingSettings().setMaxParallelThreads(4);
```

*Γιατί να ενεργοποιήσετε το GPU;* Όταν έχετε συμβατό NVIDIA GPU, η μηχανή OCR μπορεί να μεταφέρει την εντατική επεξεργασία εικονοστοιχείων στην κάρτα γραφικών, μειώνοντας δραστικά τον χρόνο επεξεργασίας—συχνά κατά 30‑50 % για μεγάλα PDF.  

*Γιατί να ορίσετε παράλληλα νήματα;* Κάθε σελίδα επεξεργάζεται ανεξάρτητα, έτσι η παροχή πολλαπλών νημάτων στον μετατροπέα του επιτρέπει να επεξεργάζεται πολλές σελίδες ταυτόχρονα. Ο αριθμός `4` λειτουργεί καλά σε ένα τυπικό quad‑core laptop· προσαρμόστε τον ανάλογα με το υλικό σας.

> **Edge case:** Αν ο διακομιστής σας δεν διαθέτει GPU, αφήστε `setUseGpu(false)` (ή απλώς παραλείψτε την κλήση). Ο μετατροπέας θα επιστρέψει σε λειτουργία μόνο‑CPU χωρίς σφάλμα.

### Step 4: Εκτέλεση της μετατροπής

```java
// Step 4: Run the conversion to produce a searchable PDF
ocrConverter.convert();
```

Αυτή η μία γραμμή κάνει το βαρέως τύπου έργο: διαβάζει κάθε σελίδα, τρέχει OCR, δημιουργεί ένα κρυφό ρεύμα κειμένου και τέλος γράφει το PDF εξόδου. Η μέθοδος μπλοκάρει μέχρι να ολοκληρωθεί η εργασία, οπότε μπορείτε με ασφάλεια να ακολουθήσετε με ένα μήνυμα επιβεβαίωσης.

### Step 5: Ειδοποίηση του χρήστη

```java
// Step 5: Inform the user where the searchable PDF was saved
System.out.println("Searchable PDF created at: " + searchablePdfPath);
```

Ένα απλό `println` αρκεί για μια επίδειξη γραμμής εντολών, αλλά σε μια πραγματική εφαρμογή ίσως θελήσετε να καταγράψετε τη διαδρομή ή να την επιστρέψετε από μια μέθοδο υπηρεσίας.

---

## Επεξεργασία σαρωμένων εγγράφων – Εκτέλεση του προγράμματος

Αποθηκεύστε τον πλήρη κώδικα παρακάτω ως `PdfToSearchablePdf.java`, μεταγλωττίστε τον και τρέξτε τον από το τερματικό. Βεβαιωθείτε ότι το `input.pdf` στο οποίο δείχνετε περιέχει πραγματικά σαρωμένες εικόνες· διαφορετικά η μηχανή OCR δεν θα έχει τίποτα να αναγνωρίσει.

```java
import com.aspose.ocr.*;

public class PdfToSearchablePdf {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the input scanned PDF and the output searchable PDF
        String sourcePdfPath = "YOUR_DIRECTORY/input.pdf";
        String searchablePdfPath = "YOUR_DIRECTORY/searchable_output.pdf";

        // Step 2: Create the OCR converter and assign source/destination files
        PdfOcrConverter ocrConverter = new PdfOcrConverter();
        ocrConverter.setSourcePdf(sourcePdfPath);
        ocrConverter.setDestinationPdf(searchablePdfPath);

        // Step 3: (Optional) Enable GPU acceleration and set parallel processing
        ocrConverter.getProcessingSettings().setUseGpu(true);
        ocrConverter.getProcessingSettings().setMaxParallelThreads(4);

        // Step 4: Run the conversion to produce a searchable PDF
        ocrConverter.convert();

        // Step 5: Inform the user where the searchable PDF was saved
        System.out.println("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υπόθεση ότι όλα είναι ρυθμισμένα σωστά):

```
Searchable PDF created at: YOUR_DIRECTORY/searchable_output.pdf
```

Ανοίξτε το `searchable_output.pdf` στο Adobe Reader, πατήστε **Ctrl + F** και προσπαθήστε να αναζητήσετε μια λέξη που εμφανίζεται στις σαρωμένες σελίδες. Αν το OCR πέτυχε, η επισήμανση θα μεταβεί στη σωστή θέση—παρόλο που η ορατή σελίδα παραμένει εικόνα.

---

## Δημιουργία PDF με δυνατότητα αναζήτησης – Επαλήθευση του αποτελέσματος

### Γρήγορος έλεγχος λογικής

1. Ανοίξτε το παραγόμενο PDF σε οποιονδήποτε προβολέα που υποστηρίζει αναζήτηση κειμένου.  
2. Χρησιμοποιήστε τη λειτουργία *Find* για να ψάξετε μια φράση που γνωρίζετε ότι υπάρχει σε μία από τις αρχικές σαρωμένες σελίδες.  
3. Αν η φράση επισημανθεί, έχετε δημιουργήσει επιτυχώς **PDF με δυνατότητα αναζήτησης**.

### Προγραμματιστική επαλήθευση (προαιρετικό)

Αν χτίζετε μια παρτίδα pipeline, ίσως θέλετε να επιβεβαιώσετε προγραμματιστικά ότι το κρυφό στρώμα κειμένου υπάρχει:

```java
import com.aspose.pdf.*;

Document doc = new Document(searchablePdfPath);
boolean hasText = doc.getPages().get_Item(1).getParagraphs().size() > 0;
System.out.println("Text layer present? " + hasText);
```

Ένα αποτέλεσμα `true` σημαίνει ότι το βήμα OCR έστειλε κειμενικό περιεχόμενο· `false` υποδηλώνει ότι κάτι πήγε στραβά—ίσως το πηγαίο PDF δεν είχε εικόνες ή η μηχανή OCR απέτυχε σιωπηρά.

---

## Συνηθισμένα προβλήματα & πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό αρχείο PDF εξόδου** | Το αρχείο προέλευσης δεν είναι σαρωμένη εικόνα (περιέχει ήδη κείμενο) | Βεβαιωθείτε ότι παρέχετε ένα πραγματικό σαρωμένο PDF· διαφορετικά ο μετατροπέας θα θεωρήσει ότι δεν υπάρχει τίποτα προς OCR. |
| **Σφάλμα Out‑of‑memory** σε τεράστια PDF | Η προεπιλεγμένη κατανομή μνήμης δεν επαρκεί για πολύ μεγάλα έγγραφα | Αυξήστε το heap της JVM (`-Xmx2g` ή περισσότερο) ή επεξεργαστείτε το αρχείο σε τμήματα χρησιμοποιώντας `PdfOcrConverter.setPageRange`. |
| **GPU δεν εντοπίστηκε** | Λείπουν οδηγοί NVIDIA ή το GPU δεν είναι συμβατό | Εγκαταστήστε τους σωστούς οδηγούς ή ορίστε `setUseGpu(false)`. |
| **Λανθασμένος εντοπισμός γλώσσας** | Το OCR προεπιλογή είναι Αγγλικά· το έγγραφό σας είναι σε άλλη γλώσσα | Καλέστε `ocrConverter.getProcessingSettings().setLanguage("fr")` (ή τον κατάλληλο κωδικό ISO). |

---

## Επόμενα βήματα: κλιμάκωση και προχωρημένα χαρακτηριστικά

Τώρα που μπορείτε να **μετατρέψετε σαρωμένο PDF** σε ένα αρχείο, σκεφτείτε τις παρακάτω επεκτάσεις:

* **Batch processing** – Επανάληψη σε έναν φάκελο PDF, επαναχρησιμοποιώντας μια ενιαία παρουσία `PdfOcrConverter` για μείωση του χρόνου εκκίνησης.  
* **Custom OCR settings** – Ρύθμιση DPI, ενεργοποίηση μείωσης θορύβου, ή

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}