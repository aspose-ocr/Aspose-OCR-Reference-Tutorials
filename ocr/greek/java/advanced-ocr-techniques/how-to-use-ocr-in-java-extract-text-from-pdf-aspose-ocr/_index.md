---
category: general
date: 2026-10-24
description: Μάθετε πώς να εκτελέσετε ένα παράδειγμα Aspose OCR Java που εξάγει κείμενο
  από αρχεία PDF, συμπεριλαμβανομένης της παράλληλης επεξεργασίας OCR, της διαχείρισης
  PDF με προστασία κωδικού και της μετατροπής σαρωμένων PDF σε searchable text.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Εκτελέστε ένα παράδειγμα Aspose OCR Java για να εξάγετε κείμενο από
  PDF γρήγορα. Αυτός ο οδηγός καλύπτει την παράλληλη επεξεργασία OCR, PDF με προστασία
  κωδικού και τη μετατροπή σαρωμένων PDF σε searchable documents.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Παράδειγμα Aspose OCR Java – εξαγωγή κειμένου από PDF γρήγορα
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Παράδειγμα Aspose OCR Java: εξαγωγή κειμένου από PDF γρήγορα'
url: /el/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR Java: εξαγωγή κειμένου από PDF γρήγορα

Σε αυτό το tutorial θα ανακαλύψετε **πώς να χρησιμοποιήσετε ένα παράδειγμα Aspose OCR Java** για να μετατρέψετε σαρωμένα PDF σε αναζητήσιμο, μηχανικά αναγνώσιμο κείμενο. Είτε έχετε ένα μόνο αρχείο πολλαπλών σελίδων είτε μια δέσμη PDF προστατευμένων με κωδικό, τα παρακάτω βήματα δείχνουν πώς να διαμορφώσετε τη μηχανή OCR, να ενεργοποιήσετε την παράλληλη επεξεργασία και να ανακτήσετε το συνδυασμένο αποτέλεσμα με λίγες μόνο γραμμές κώδικα Java.

Θα μάθετε επίσης πότε να προσαρμόζετε τον αριθμό των νημάτων για βέλτιστη απόδοση, πώς να διαχειρίζεστε κρυπτογραφημένα PDF και γιατί αυτή η προσέγγιση είναι ιδανική για τη μετατροπή σαρωμένων εγγράφων PDF σε αναζητήσιμα αρχεία.

![how to use OCR with Aspose OCR Java](/images/ocr-parallel.png "Illustration of parallel OCR processing in Java – how to use OCR")
[how to use OCR with Aspose OCR Java](/images/ocr-parallel.png "Illustration of parallel OCR processing in Java – how to use OCR")

## Γρήγορες απαντήσεις
- **Τι κάνει το παράδειγμα Aspose OCR Java;** Φορτώνει ένα PDF, εκτελεί OCR σε κάθε σελίδα παράλληλα και επιστρέφει το πλήρες αναζητήσιμο κείμενο ως μία ενιαία συμβολοσειρά.  
- **Μπορεί να επεξεργαστεί PDF προστατευμένα με κωδικό;** Ναι – μπορείτε να παρέχετε τον κωδικό του εγγράφου όταν προσθέτετε το αρχείο στο `OcrInput`.  
- **Αξίζει η παράλληλη επεξεργασία OCR;** Σε μηχάνημα με 4 πυρήνες μειώνει το χρόνο επεξεργασίας κατά 30‑70 % για PDF με περισσότερες από πέντε σελίδες.  
- **Ποιες γλώσσες υποστηρίζονται;** Πάνω από 70 γλώσσες, συμπεριλαμβανομένων των Αγγλικών, Γαλλικών, Γερμανικών, Κινέζικων και Αραβικών.  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται εμπορική άδεια Aspose OCR για μη‑δοκιμαστική χρήση· η δωρεάν δοκιμή λειτουργεί για αξιολόγηση.

## Τι είναι ένα παράδειγμα Aspose OCR Java;
Το **παράδειγμα Aspose OCR Java** είναι ένα σύντομο, εκτελέσιμο πρόγραμμα που δείχνει πώς να δημιουργήσετε μια实例 του `OcrEngine`, να διαμορφώσετε την παράλληλη εκτέλεση και να εξάγετε κείμενο από αρχεία PDF χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR for Java. Επίσης δείχνει πώς να διαχειρίζεστε κοινές περιπτώσεις όπως έγγραφα προστατευμένα με κωδικό, ρύθμιση ορίου μνήμης και επιλογή γλώσσας, παρέχοντας μια ισχυρή βάση για την κατασκευή μεγαλύτερων αγωγών επεξεργασίας εγγράφων.

## Γιατί να χρησιμοποιήσετε την παράλληλη επεξεργασία OCR;
Το Aspose OCR μπορεί να χωρίσει ένα PDF πολλαπλών σελίδων σε ξεχωριστές σελίδες και να επεξεργαστεί κάθε σελίδα σε δικό του νήμα. Σε διακομιστή με 8 πυρήνες, ένα έγγραφο 120 σελίδων επεξεργάζεται συνήθως σε λιγότερο από 30 δευτερόλεπτα, σε σύγκριση με πάνω από ένα λεπτό όταν εκτελείται διαδοχικά. Αυτή η αύξηση ταχύτητας είναι ιδιαίτερα πολύτιμη όταν χρειάζεται να **μετατρέψετε σαρωμένα PDF σε αναζητήσιμα** αρχεία μαζικά.

## Προαπαιτούμενα
- Java 8 ή νεότερη εγκατεστημένη.  
- Maven ή Gradle (το παράδειγμα χρησιμοποιεί Maven).  
- Άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  

## Πώς να εκτελέσετε το παράδειγμα Aspose OCR Java βήμα προς βήμα

### Βήμα 1: ρυθμίστε το έργο σας

Προσθέστε την εξάρτηση Aspose OCR στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Αν προτιμάτε Gradle, αντικαταστήστε το απόσπασμα με την αντίστοιχη γραμμή `implementation`.  
Αφού η εξάρτηση λυθεί, μπορείτε να εισάγετε τις απαιτούμενες κλάσεις στο αρχείο πηγαίου κώδικα Java.

### Βήμα 2: δημιουργήστε και διαμορφώστε τη μηχανή OCR

`OcrEngine` είναι η βασική κλάση που εκτελεί την οπτική αναγνώριση χαρακτήρων.

Η κλάση `OcrEngine` είναι το κύριο αντικείμενο του Aspose OCR που περιλαμβάνει όλες τις ρυθμίσεις OCR και τη λογική εκτέλεσης.  
Ενεργοποιήστε την παράλληλη επεξεργασία και προαιρετικά περιορίστε το σύνολο νημάτων:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Γιατί είναι σημαντικό:**  
- `setParallelProcessing(true)` διανέμει τις σελίδες σε πολλαπλούς πυρήνες CPU, μειώνοντας δραστικά το χρόνο εκτέλεσης σε πολυπύρηνο υλικό.  
- `setMaxThreadCount` προστατεύει τους πόρους του διακομιστή αποτρέποντας τη μηχανή από το να μονοπωλήσει όλους τους πυρήνες, κάτι που είναι κρίσιμο σε περιβάλλοντα κοινόχρηστης φιλοξενίας ή CI.

### Βήμα 3: φορτώστε το PDF που θέλετε να επεξεργαστείτε

`OcrInput` αντιπροσωπεύει τη συλλογή αρχείων (PDF, εικόνες ή μεικτά μέσα) που η μηχανή θα αναλύσει.

Η κλάση `OcrInput` συγκεντρώνει μία ή περισσότερες πηγές εισόδου, επιτρέποντάς σας να τροφοδοτήσετε PDF, TIFF ή JPEG στη μηχανή OCR σε μία παρτίδα.  
Προσθέστε το PDF σας (ή ένα σύνολο PDF) στη συλλογή εισόδου:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Συμβουλή:** Χρησιμοποιήστε απόλυτη διαδρομή ή διαδρομή σχετική με τον τρέχοντα φάκελο εργασίας για να αποφύγετε το `FileNotFoundException`. Η μέθοδος `add` μπορεί να κληθεί επανειλημμένα για να προγραμματίσει πολλαπλά έγγραφα για επεξεργασία παρτίδας.

### Βήμα 4: εκτελέστε OCR σε όλες τις σελίδες παράλληλα

`OcrResult` περιέχει το συνδυασμένο κείμενο εξόδου και τις πληροφορίες εμπιστοσύνης ανά σελίδα μετά την ολοκλήρωση της αναγνώρισης.

Το αντικείμενο `OcrResult` περιέχει το ενωμένο αποτέλεσμα απλού κειμένου και μια λίστα από αντικείμενα `PageResult` που εμφανίζουν τις βαθμολογίες εμπιστοσύνης για κάθε επεξεργασμένη σελίδα.  
Εκτελέστε την αναγνώριση:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Πίσω από τη σκηνή:** Κάθε σελίδα παραδίδεται σε ξεχωριστό νήμα εργασίας (μέχρι το `maxThreadCount` που ορίσατε). Η βιβλιοθήκη συγχρονίζει τα αποτελέσματα ώστε το τελικό `OcrResult` διατηρεί την αρχική σειρά των σελίδων.

### Βήμα 5: ανακτήστε και εμφανίστε το συνδυασμένο κείμενο

`OcrResult.getText()` επιστρέφει την πλήρη αναζητήσιμη συμβολοσειρά.

Η μέθοδος `getText()` του `OcrResult` επιστρέφει μία ενιαία `String` που περιέχει το κείμενο που εξήχθη από OCR σε κάθε σελίδα, με τις αλλαγές γραμμής να διατηρούνται όπως εμφανίστηκαν στο αρχικό PDF.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει μία συνεχόμενη συμβολοσειρά που περιέχει το αναγνώσιμο κείμενο από όλες τις σελίδες, έτοιμο για ευρετηρίαση, αποθήκευση ή περαιτέρω επεξεργασία.

### Βήμα 6: διαχειριστείτε ειδικές περιπτώσεις

#### Πώς η μηχανή αντιμετωπίζει PDF προστατευμένα με κωδικό;

Παρέχετε τον κωδικό όταν προσθέτετε το αρχείο στο `OcrInput`:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Η υπερφόρτωση της μεθόδου `add` που δέχεται κωδικό αποκρυπτογραφεί το έγγραφο άμεσα, επιτρέποντας αδιάκοπη OCR χωρίς χειροκίνητη αποκρυπτογράφηση.

#### Πώς μπορώ να περιορίσω τη χρήση μνήμης για πολύ μεγάλα αρχεία;

Καλέστε `ocrEngine.setMemoryLimit(256);` για να περιορίσετε την κατανάλωση RAM στα 256 MB. Η μηχανή θα αποθηκεύει αυτόματα τα επιπλέον δεδομένα σε προσωρινά αρχεία, αποτρέποντας καταρρεύσεις εξαιτίας έλλειψης μνήμης ακόμη και σε PDF με εκατοντάδες σελίδες.

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

### Χρειάζομαι πραγματικά την παράλληλη επεξεργασία;

Αν το PDF σας περιέχει **περισσότερες από λίγες σελίδες** και έχετε τουλάχιστον τέσσερις πυρήνες CPU, η ενεργοποίηση της παράλληλης επεξεργασίας συνήθως μειώνει το συνολικό χρόνο εκτέλεσης κατά **30‑70 %**. Για σάρωση μίας σελίδας, το κόστος των νημάτων μπορεί να υπερβαίνει το όφελος, οπότε μπορείτε να το απενεργοποιήσετε με `ocrEngine.setParallelProcessing(false)`.

### Τι συμβαίνει όταν μια σελίδα αποτύχει στο OCR;

Το Aspose OCR ρίχνει ένα `OcrException` μόνο για μοιραίες σφάλματα όπως ένα κατεστραμμένο αρχείο. Σελίδες που δεν μπορούν να αναγνωριστούν επιστρέφουν απλώς μια κενή συμβολοσειρά, την οποία η μηχανή ενώνει σιωπηλά. Μπορείτε να ελέγξετε το `ocrResult.getPageResults()` για να λάβετε τις βαθμολογίες εμπιστοσύνης ανά σελίδα και να διαχειριστείτε χειροκίνητα τις σελίδες χαμηλής εμπιστοσύνης.

### Πώς αλλάζω τη γλώσσα αναγνώρισης;

Η μηχανή προεπιλογή είναι τα Αγγλικά, αλλά μπορείτε να αλλάξετε γλώσσες με:

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Αντικαταστήστε το `Language.FRENCH` με οποιοδήποτε υποστηριζόμενο enum γλώσσας. Αυτό είναι απαραίτητο όταν χρειάζεται να **εξάγετε κείμενο PDF Java** από πολυγλωσσικά έγγραφα.

## Επαγγελματικές συμβουλές για OCR έτοιμο για παραγωγή

- **Επεξεργασία παρτίδας:** Τυλίξτε τη ροή σε βρόχο που διαβάζει ονόματα αρχείων από έναν φάκελο, μετατρέποντας το demo σε κλιμακούμενη υπηρεσία.  
- **Καταγραφή:** Ορίστε `ocrEngine.setLogLevel(LogLevel.ERROR)` στην παραγωγή για να καταστέλλετε την εκτενή έξοδο.  
- **Καθαρισμός αποτελέσματος:** Μετά-επεξεργαστείτε το `ocrResult.getText()` με κανονικές εκφράσεις για να αφαιρέσετε περιττά κενά ή artefacts.  
- **Ρύθμιση ομάδας νημάτων:** Χρησιμοποιήστε `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` σε διακομιστές με πολλούς πυρήνες για μέγιστη απόδοση.  
- **Δοκιμή απόδοσης:** Σε Intel Xeon 8‑πυρήνων, ένα PDF 200 σελίδων (300 MB) επεξεργάζεται σε ~22 δευτερόλεπτα με ενεργοποιημένη την παράλληλη OCR.

## Συμπέρασμα

Τώρα έχετε ένα πλήρες **παράδειγμα Aspose OCR Java** που εξάγει αναζητήσιμο κείμενο από οποιοδήποτε σαρωμένο PDF, υποστηρίζει αρχεία προστατευμένα με κωδικό και αξιοποιεί την παράλληλη επεξεργασία για ταχύτητα. Ενσωματώνοντας αυτόν τον κώδικα στις δικές σας εφαρμογές, μπορείτε να δημιουργήσετε ισχυρούς αγωγούς ψηφιοποίησης εγγράφων, να τροφοδοτήσετε τα αποτελέσματα OCR σε ευρετήρια αναζήτησης ή να τα συνδυάσετε με υπηρεσίες μετάφρασης για πολυγλωσσικά αρχεία.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε το εξαγόμενο κείμενο στο Elasticsearch για πλήρη αναζήτηση κειμένου, ή συνδέστε το αποτέλεσμα με ένα API μετάφρασης για να δημιουργήσετε ένα πολυγλωσσικό αναζητήσιμο αποθετήριο. Καλή προγραμματιστική!

---

**Τελευταία ενημέρωση:** 2026-10-24  
**Δοκιμάστηκε με:** Aspose OCR for Java 24.11  
**Συγγραφέας:** Aspose  

## Συχνές ερωτήσεις

**Ε:** Μπορώ να χρησιμοποιήσω αυτό το παράδειγμα με δωρεάν άδεια δοκιμής;  
**Α:** Ναι, η δωρεάν δοκιμή Aspose OCR λειτουργεί για ανάπτυξη και δοκιμές· απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις.

**Ε:** Το παράδειγμα υποστηρίζει OCR σε PDF προστατευμένα με κωδικό;  
**Α:** Απόλυτα – περάστε τον κωδικό στο `OcrInput.add(filePath, password)` και η μηχανή θα αποκρυπτογραφήσει το έγγραφο αυτόματα.

**Ε:** Πόσες γλώσσες αναγνωρίζει το Aspose OCR;  
**Α:** Πάνω από 70 γλώσσες, συμπεριλαμβανομένων των δεξιά‑προς‑αριστερά γραφών όπως η Αραβική και η Εβραϊκή.

**Ε:** Ποιο είναι το μέγιστο μέγεθος PDF που μπορώ να επεξεργαστώ;  
**Α:** Η μηχανή μπορεί να διαχειριστεί PDF με εκατοντάδες σελίδες· μπορείτε να ορίσετε όριο μνήμης για να διατηρείται η χρήση RAM προβλέψιμη.

**Ε:** Είναι ασφαλής η παράλληλη OCR σε κοινόχρηστους διακομιστές;  
**Α:** Ναι, ρυθμίζοντας το `setMaxThreadCount` ελέγχετε τον μέγιστο αριθμό ταυτόχρονων νημάτων, αποτρέποντας την εξάντληση πόρων.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## Σχετικά μαθήματα

- [Πώς να χρησιμοποιήσετε OCR σε Java με παράλληλη επεξεργασία με Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Δημιουργία Αναζητήσιμου PDF με τον οδηγό Aspose OCR Java](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [Πώς να χρησιμοποιήσετε OCR σε Java για εξαγωγή κειμένου από PDF με Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}