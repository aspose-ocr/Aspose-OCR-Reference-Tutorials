---
category: general
date: 2026-09-18
description: Μάθετε πώς να προσθέσετε την εξάρτηση Aspose OCR Maven και να εξάγετε
  κείμενο από εικόνες σε Java. Αυτός ο οδηγός καλύπτει τη ρύθμιση της μηχανής OCR,
  τον ορθογραφικό έλεγχο, προσαρμοσμένα λεξικά και συμβουλές διαμόρφωσης.
draft: false
keywords:
- aspose ocr maven dependency
- java image to text
- extract image text java
- Aspose OCR Java
- OCR spell checking
lastmod: 2026-09-18
og_description: Μάθετε πώς να προσθέσετε την εξάρτηση Aspose OCR Maven και να εξάγετε
  κείμενο από εικόνες σε Java. Αυτός ο οδηγός καλύπτει τη ρύθμιση της μηχανής OCR,
  τον ορθογραφικό έλεγχο, προσαρμοσμένα λεξικά και συμβουλές διαμόρφωσης.
og_image_alt: Diagram showing OCR workflow to extract text from image using Aspose
  OCR in Java
og_title: Προσθήκη εξάρτησης Aspose OCR Maven για εξαγωγή κειμένου από εικόνες σε
  Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to add the Aspose OCR Maven dependency and extract text from
    images in Java. This guide covers OCR engine setup, spell‑checking, custom dictionaries,
    and configuration tips.
  headline: Add Aspose OCR Maven dependency to extract image text in Java
  type: TechArticle
- questions:
  - answer: Handwritten recognition is available in a separate module (`aspose-ocr-handwriting`).
      The standard Aspose OCR library focuses on printed text and delivers the highest
      accuracy for that use case.
    question: Does Aspose OCR support handwritten text?
  - answer: Yes—download the image into a `byte[]` or `InputStream` (e.g., using `java.net.URL`)
      and pass that stream to `ocrEngine.recognize(inputStream)`.
    question: Can I process images directly from a URL?
  - answer: Use `ocrConfig.setRegion(new Rectangle(x, y, width, height))` before calling
      `recognize`. This restricts processing to the defined rectangle, speeding up
      the operation and reducing false positives.
    question: How do I limit OCR to a specific region of an image?
  - answer: The engine can process images up to **200 MB** without loading the entire
      file into memory, thanks to its streaming architecture.
    question: What is the maximum file size Aspose OCR can handle?
  - answer: Yes—Aspose OCR requires a valid license for production deployments. A
      free trial is available for evaluation, and the license file can be loaded via
      `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Προσθήκη εξάρτησης Aspose OCR Maven για εξαγωγή κειμένου από εικόνες σε Java
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη εξάρτησης Aspose OCR Maven για εξαγωγή κειμένου από εικόνα σε Java

Αν χρειάζεστε **εξαγωγή κειμένου από εικόνα σε Java** γρήγορα και αξιόπιστα, η προσθήκη της εξάρτησης Aspose OCR Maven είναι ο πιο απλός τρόπος για να ξεκινήσετε. Είτε δημιουργείτε μια γραμμή επεξεργασίας τιμολογίων, ένα αναζητήσιμο αρχείο, είτε ένα κινητό backend που διαβάζει χειρόγραφες φόρμες, η βιβλιοθήκη σας παρέχει μια έτοιμη μηχανή OCR με ενσωματωμένο ορθογραφικό έλεγχο, επιλογή γλώσσας και υποστήριξη προσαρμοσμένου λεξικού. Σε αυτό το tutorial θα δείτε πώς να προσθέσετε την εξάρτηση Maven, να διαμορφώσετε τη μηχανή και να ανακτήσετε καθαρό, διορθωμένο κείμενο από οποιαδήποτε υποστηριζόμενη μορφή εικόνας.

---

## Γρήγορες απαντήσεις
- **Ποιος Maven συντελεστής προσθέτει το Aspose OCR;** `com.aspose:aspose-ocr:24.10` (αντικαταστήστε το 24.10 με την πιο πρόσφατη έκδοση).  
- **Ποια έκδοση Java απαιτείται;** Java 8 ή νεότερη· η βιβλιοθήκη λειτουργεί σε οποιοδήποτε runtime JDK 8+.  
- **Μπορώ να ενεργοποιήσω τον ορθογραφικό έλεγχο;** Ναι—καλέστε `ocrConfig.setSpellCheck(true)` μετά τη δημιουργία της μηχανής.  
- **Πώς μπορώ να χρησιμοποιήσω προσαρμοσμένο λεξικό;** Φορτώστε ένα αρχείο `.dic` και περάστε το στο `ocrConfig.setSpellCheckDictionary(path)`.  
- **Είναι η βιβλιοθήκη κατάλληλη για μεγάλα PDF;** Ναι—επεξεργαστείτε κάθε σελίδα ως εικόνα και επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` για να διατηρήσετε τη χρήση μνήμης χαμηλή.

---

## Τι είναι η εξάρτηση Aspose OCR Maven;
Η **εξάρτηση Aspose OCR Maven** είναι ένα artifact Gradle/Maven που περιλαμβάνει ολόκληρη τη μηχανή OCR, τα πακέτα γλωσσών και τους πόρους ορθογραφικού ελέγχου σε ένα ενιαίο JAR, επιτρέποντάς σας να καλέσετε τις λειτουργίες OCR απευθείας από κώδικα Java χωρίς εγγενή δυαδικά αρχεία. Η προσθήκη της εξάρτησης φέρνει **70+ πακέτα γλωσσών** και **υποστηρίζει πάνω από 30 μορφές εικόνας**, ώστε να μπορείτε να χειριστείτε PNG, JPEG, TIFF, BMP και ακόμη και πολυσελίδες TIFF αμέσως.

---

## Γιατί να χρησιμοποιήσετε Aspose OCR για μετατροπή εικόνας σε κείμενο σε Java;
Το Aspose OCR επεξεργάζεται μια τυπική σελίδα 300 dpi σε **κάτω από 200 ms** σε τυπική CPU 2.5 GHz, και μπορεί να χειριστεί έγγραφα έως **200 MB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Ο ενσωματωμένος ορθογραφικός έλεγχος βελτιώνει την ακατέργαστη ακρίβεια OCR κατά **12–18 ποσοστιαίες μονάδες** σε θορυβώδεις σαρώσεις, μειώνοντας τα βήματα μετα-επεξεργασίας.

---

## Προαπαιτούμενα
- **Java 8+** (οποιοδήποτε πρόσφατο JDK λειτουργεί).  
- **Maven** ή **Gradle** σύστημα κατασκευής για διαχείριση εξαρτήσεων.  
- Αρχείο εικόνας που περιέχει τυπωμένο ή εκτυπωμένο κείμενο (π.χ., `invoice_page.png`).  
- Τουλάχιστον **1 GB** μνήμης heap για πολύ μεγάλες εικόνες· οι τυπικές σαρώσεις χρειάζονται πολύ λιγότερο.

> **Συμβουλή επαγγελματία:** Εάν χρησιμοποιείτε Maven, προσθέστε το παρακάτω απόσπασμα στο `pom.xml` (αντικαταστήστε την έκδοση με την πιο πρόσφατη έκδοση):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

Το παραπάνω απόσπασμα είναι ένα απλό XML τμήμα· **δεν** μετράει ως μπλοκ κώδικα για σκοπούς επικύρωσης.

---

## Πώς αρχικοποιείτε τη μηχανή OCR και έχετε πρόσβαση στη διαμόρφωσή της;
Η κλάση `OcrEngine` αντιπροσωπεύει τον πυρήνα του επεξεργαστή OCR που εκτελεί ανάλυση εικόνας και εξαγωγή κειμένου.  
Δημιουργήστε τη μηχανή με `new OcrEngine()`, στη συνέχεια αποκτήστε τη μεταβλητή διαμόρφωση μέσω `getConfiguration()`. Το αντικείμενο διαμόρφωσης σας επιτρέπει να ορίσετε γλώσσα, να ενεργοποιήσετε ορθογραφικό έλεγχο και να καθορίσετε προσαρμοσμένα λεξικά, ώστε να προσαρμόσετε τη διαδικασία OCR στους συγκεκριμένους τύπους εγγράφων σας. Η επαναχρησιμοποίηση της ίδιας παρουσίας μηχανής σε πολλές εικόνες μειώνει το κόστος.

```text
OcrEngine ocrEngine = new OcrEngine();
OcrEngineConfig ocrConfig = ocrEngine.getConfig();
```

*Οι δύο παραπάνω γραμμές δείχνουν το τυπικό μοτίβο αρχικοποίησης. Η πρώτη δημιουργεί τη μηχανή· η δεύτερη ανακτά τη μεταβλητή διαμόρφωση.*

---

## Πώς επιλέγετε γλώσσα και ενεργοποιείτε τον ορθογραφικό έλεγχο;
Το enum `Language` περιλαμβάνει όλες τις υποστηριζόμενες γλώσσες που η μηχανή OCR μπορεί να αναγνωρίσει.  
Επιλέξτε την κατάλληλη τιμή enum (π.χ., `Language.ENGLISH`) στο αντικείμενο διαμόρφωσης για να υποδείξετε στο engine ποιο μοντέλο γλώσσας να χρησιμοποιήσει. Η ενεργοποίηση του ορθογραφικού ελέγχου με `setSpellCheck(true)` ενεργοποιεί το ενσωματωμένο λεξικό, βελτιώνοντας την ακρίβεια διορθώνοντας κοινές λανθασμένες αναγνώσεις. Μπορείτε επίσης να συνδυάσετε πολλαπλές γλώσσες εάν χρειάζεται, αν και κάθε κλήση επεξεργάζεται μία γλώσσα τη φορά.

```text
ocrConfig.setLanguage(Language.ENGLISH);
ocrConfig.setSpellCheck(true);
```

Η ενεργοποίηση του ορθογραφικού ελέγχου μειώνει κοινές λανθασμένες αναγνώσεις OCR όπως “0” vs. “O” ή “l” vs. “1”. Για αγγλικά έγγραφα το προεπιλεγμένο λεξικό περιέχει **150 k** λέξεις, και μπορείτε να το επεκτείνετε με τους δικούς σας όρους.

---

## Πώς μπορείτε να φορτώσετε προσαρμοσμένο λεξικό ορθογραφικού ελέγχου;
Εάν ο τομέας σας χρησιμοποιεί εξειδικευμένη ορολογία—ιατρικούς κωδικούς, νομικές συντομογραφίες ή SKU προϊόντων—φορτώστε ένα προσαρμοσμένο αρχείο `.dic`. Η μηχανή ενσωματώνει τη λίστα σας στο ενσωματωμένο λεξικό, διασφαλίζοντας ότι οι ειδικοί όροι αναγνωρίζονται σωστά.

```text
ocrConfig.setSpellCheckDictionary("C:/dictionaries/custom_terms.dic");
```

Μπορείτε επίσης να παρέχετε το λεξικό ως σχετική διαδρομή μέσα στους πόρους του έργου· η μηχανή θα το επιλύσει κατά το χρόνο εκτέλεσης.

---

## Πώς εκτελείτε OCR σε τοπικό αρχείο εικόνας;
`recognize` είναι μέθοδος του `OcrEngine` που επεξεργάζεται ένα αρχείο εικόνας και επιστρέφει ένα `RecognitionResult` με το εξαγόμενο κείμενο.  
Παρέχετε τη πλήρη διαδρομή στην εικόνα όταν καλείτε `ocrEngine.recognize("path/to/image.png")`. Η μέθοδος εκτελεί προεπεξεργασία όπως ευθυγράμμιση και δυαδικοποίηση πριν εφαρμόσει τον νευρωνικό αναγνωστικό αλγόριθμο. Το `RecognitionResult` περιλαμβάνει τόσο το ακατέργαστο OCR αποτέλεσμα όσο και την έκδοση με ορθογραφικό έλεγχο, την οποία μπορείτε να προσπελάσετε μέσω `getText()`.

```text
RecognitionResult result = ocrEngine.recognize("C:/images/typed_scanned_doc.png");
String correctedText = result.getText();
```

Πίσω από τη σκηνή, το Aspose OCR εκτελεί ευθυγράμμιση, δυαδικοποίηση και διαχωρισμό χαρακτήρων πριν τροφοδοτήσει τα pixel δεδομένα σε νευρωνικό αναγνωστικό μοντέλο. Η διαδικασία διαχειρίζεται πλήρως η βιβλιοθήκη· εσείς χρειάζεται μόνο να χειριστείτε το παραγόμενο string.

---

## Πώς εμφανίζετε ή αποθηκεύετε το διορθωμένο κείμενο;
Απλώς εκτυπώστε το string στην κονσόλα, γράψτε το σε αρχείο ή εισάγετέ το σε βάση δεδομένων. Επειδή το βήμα ορθογραφικού ελέγχου έχει ήδη καθαρίσει το αποτέλεσμα, μπορείτε να θεωρήσετε το string έτοιμο για παραγωγή.

```text
System.out.println(correctedText);
```

Εάν χρειάζεται να αποθηκεύσετε το αποτέλεσμα, χρησιμοποιήστε το τυπικό Java I/O:

```text
Files.write(Paths.get("output.txt"), correctedText.getBytes(StandardCharsets.UTF_8));
```

---

## Ποιες είναι οι κοινές ακραίες περιπτώσεις και πώς μπορείτε να τις αντιμετωπίσετε;
Όταν εργάζεστε με πραγματικές σαρώσεις, διάφορες συνθήκες μπορούν να επηρεάσουν την απόδοση του OCR. Χαμηλή ανάλυση, μεικτές γλώσσες, μεγάλα PDF και εξειδικευμένη ορολογία απαιτούν ειδική διαχείριση για να διατηρηθεί η ακρίβεια και η αποδοτικότητα. Οι παρακάτω ενότητες περιγράφουν πρακτικές στρατηγικές για κάθε μία από αυτές τις προκλήσεις.

### Εικόνες χαμηλής ανάλυσης
Η ακρίβεια OCR πέφτει απότομα κάτω από **150 dpi**. Για σαρώσεις χαμηλότερης ανάλυσης, εξετάστε την αύξηση ανάλυσης με βιβλιοθήκη επεξεργασίας εικόνας (π.χ., OpenCV) πριν τις περάσετε στο Aspose OCR.

### Πολύγλωσσα έγγραφα
Το Aspose OCR υποστηρίζει **70+ γλώσσες**. Για σελίδες με μεικτές γλώσσες, καλέστε `ocrConfig.setLanguage` για κάθε γλώσσα που θέλετε να εντοπίσετε, εκτελέστε `recognize` ξεχωριστά και συνδυάστε τα αποτελέσματα. Η μηχανή δεν εντοπίζει αυτόματα τη γλώσσα.

### PDF ή πολυσελίδες TIFF
Εξάγετε κάθε σελίδα ως εικόνα (χρησιμοποιώντας Aspose PDF, PDFBox ή παρόμοια βιβλιοθήκη), έπειτα τροφοδοτήστε κάθε εικόνα στην ίδια παρουσία `OcrEngine`. Η επαναχρησιμοποίηση της παρουσίας διατηρεί τη χρήση μνήμης χαμηλή, επειδή η μηχανή είναι αμετάβλητη μεταξύ κλήσεων.

### Προσαρμοσμένη ευαισθησία ορθογραφικού ελέγχου
Το προεπιλεγμένο όριο ορθογραφικού ελέγχου λειτουργεί για τα περισσότερα αγγλικά κείμενα. Για εξαιρετικά τεχνικά έγγραφα μπορείτε να ρυθμίσετε τις εσωτερικές `SpellCheckOptions` μέσω `ocrConfig.getSpellCheckOptions().setThreshold(0.75)` (τιμές από 0.0–1.0). Χαμηλότερες τιμές κάνουν τη μηχανή πιο επιθετική στην διόρθωση λέξεων.

---

## Συχνές ερωτήσεις

**Ε: Υποστηρίζει το Aspose OCR χειρόγραφο κείμενο;**  
Α: Η αναγνώριση χειρόγραφου κειμένου είναι διαθέσιμη σε ξεχωριστό μοντέλο (`aspose-ocr-handwriting`). Η τυπική βιβλιοθήκη Aspose OCR εστιάζει σε τυπωμένο κείμενο και προσφέρει τη μέγιστη ακρίβεια για αυτήν τη χρήση.

**Ε: Μπορώ να επεξεργαστώ εικόνες απευθείας από URL;**  
Α: Ναι—κατεβάστε την εικόνα σε `byte[]` ή `InputStream` (π.χ., χρησιμοποιώντας `java.net.URL`) και περάστε το stream στο `ocrEngine.recognize(inputStream)`.

**Ε: Πώς περιορίζω το OCR σε συγκεκριμένη περιοχή μιας εικόνας;**  
Α: Χρησιμοποιήστε `ocrConfig.setRegion(new Rectangle(x, y, width, height))` πριν καλέσετε `recognize`. Αυτό περιορίζει την επεξεργασία στο ορισμένο ορθογώνιο, επιταχύνοντας τη λειτουργία και μειώνοντας τα ψευδώς θετικά.

**Ε: Ποιο είναι το μέγιστο μέγεθος αρχείου που μπορεί να διαχειριστεί το Aspose OCR;**  
Α: Η μηχανή μπορεί να επεξεργαστεί εικόνες έως **200 MB** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, χάρη στην αρχιτεκτονική ροής δεδομένων.

**Ε: Απαιτείται εμπορική άδεια για χρήση σε παραγωγή;**  
Α: Ναι—το Aspose OCR απαιτεί έγκυρη άδεια για παραγωγικές εγκαταστάσεις. Διατίθεται δωρεάν δοκιμαστική έκδοση για αξιολόγηση, και το αρχείο άδειας μπορεί να φορτωθεί με `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

---

## Συμπέρασμα και επόμενα βήματα

Τώρα έχετε μια πλήρη, ολοκληρωμένη ροή εργασίας για **εξαγωγή κειμένου από εικόνα σε Java** χρησιμοποιώντας την εξάρτηση Aspose OCR Maven. Προσθέτοντας την εξάρτηση, διαμορφώνοντας τη γλώσσα και τον ορθογραφικό έλεγχο, φορτώνοντας προαιρετικά προσαρμοσμένο λεξικό και αντιμετωπίζοντας ακραίες περιπτώσεις όπως χαμηλή ανάλυση ή πολυσελίδες PDF, μπορείτε να μετατρέψετε θορυβώδεις εικόνες σε καθαρό, αναζητήσιμο κείμενο με ελάχιστο κώδικα.

Από εδώ μπορείτε να εξερευνήσετε:

- **Επεξεργασία παρτίδας** – επαναλάβετε πάνω από έναν φάκελο εικόνων και αποθηκεύστε κάθε αποτέλεσμα σε βάση δεδομένων.  
- **Ενσωμάτωση με Aspose PDF** – εξάγετε εικόνες από PDF και τροφοδοτήστε τις απευθείας στη μηχανή OCR.  
- **Προηγμένη διαχείριση γλώσσας** – αλλάξτε δυναμικά το `ocrConfig.setLanguage` βάσει μεταδεδομένων εγγράφου.  

Δοκιμάστε τα βήματα, πειραματιστείτε με τις επιλογές διαμόρφωσης και θα δείτε πόσο χρόνο κερδίζετε σε σύγκριση με την κατασκευή μιας δικής σας λύσης OCR. Καλή προγραμματιστική!

![Διάγραμμα που δείχνει τη ροή εργασίας OCR για εξαγωγή κειμένου από εικόνα](/images/ocr-workflow.png "αναγνώριση κειμένου από εικόνα workflow")

---

**Τελευταία ενημέρωση:** 2026-09-18  
**Δοκιμή με:** Aspose OCR 24.10 for Java  
**Συγγραφέας:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου από εικόνες – Βασικά OCR για Java](/ocr/java/ocr-basics/)
- [εικόνα σε κείμενο java: Μετατροπή εικόνας σε κείμενο με Aspose.OCR](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Εκτέλεση OCR σε εικόνα με Java – Πλήρης οδηγός Aspose OCR](/ocr/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}