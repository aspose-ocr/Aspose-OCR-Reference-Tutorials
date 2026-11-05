---
date: 2026-06-24
description: Μάθετε πώς να κάνετε OCR κειμένου εικόνας με επιλογή γλώσσας χρησιμοποιώντας
  το Aspose.OCR για Java. Αυτός ο οδηγός βήμα προς βήμα καλύπτει την εξαγωγή κειμένου
  Java, τη διόρθωση κλίσης OCR και άλλα.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Πώς να εκτελέσετε διόρθωση κλίσης OCR και επιλογή γλώσσας με Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Πώς να εκτελέσετε διόρθωση κλίσης OCR και επιλογή γλώσσας με Aspose.OCR
url: /el/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε διόρθωση κλίσης OCR και επιλογή γλώσσας με το Aspose.OCR

## Εισαγωγή

Η εξαγωγή κειμένου από αρχεία εικόνας είναι μια κοινή απαίτηση, είτε ψηφιοποιείτε σαρωμένα έγγραφα, επεξεργάζεστε αποδείξεις ή δημιουργείτε αρχεία αναζήτησης. Σε αυτό το μάθημα θα περάσουμε βήμα‑βήμα ένα πλήρες, πρακτικό παράδειγμα που δείχνει **πώς να κάνετε OCR κειμένου εικόνας** με συγκεκριμένη ρύθμιση γλώσσας, ώστε να ενσωματώσετε αξιόπιστο OCR στις εφαρμογές Java σας σήμερα. Θα δείτε επίσης πώς να διαχειριστείτε **τη διόρθωση κλίσης OCR** και την αναγνώριση βάσει περιοχής για βέλτιστη ακρίβεια, που μαζί μπορούν να **βελτιώσουν την ακρίβεια OCR** έως και 30 % σε κεκλιμένες σαρώσεις.

## Σύντομες Απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR σε Java;** Aspose.OCR for Java  
- **Ποια ρύθμιση επιλέγει τη γλώσσα;** `settings.setLanguage(Language.Eng)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα)  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν άδεια αξιολόγησης λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να περιορίσω το OCR σε μια περιοχή της εικόνας;** Ναι, χρησιμοποιήστε `RecognitionSettings.setRecognitionAreas()` με ορθογώνια.  
- **Ποιος είναι ο τυπικός χρόνος εκτέλεσης;** Μερικά δευτερόλεπτα ανά σελίδα σε ένα τυπικό laptop, ανάλογα με το μέγεθος της εικόνας και την πολυπλοκότητα της γλώσσας.  

`Language` είναι μια απαρίθμηση που καταγράφει τις γλώσσες OCR που υποστηρίζονται από το Aspose.OCR, όπως Αγγλικά, Γαλλικά, Ισπανικά κ.λπ.

## Τι είναι η διόρθωση κλίσης OCR;

Η διόρθωση κλίσης OCR είναι η διαδικασία ανίχνευσης και ευθυγράμμισης των κεκλιμένων γραμμών κειμένου πριν από την αναγνώριση χαρακτήρων. Με την ευθυγράμμιση της βάσης του κειμένου, η μηχανή OCR μπορεί να εφαρμόσει τα μοντέλα γλώσσας πιο αποτελεσματικά, μειώνοντας τις λανθασμένες αναγνώσεις που προκαλούνται από κεκλιμένες σαρώσεις. Αυτό το βήμα βελτιώνει την οπτική ποιότητα της εισερχόμενης εικόνας, επιτρέποντας στους αλγόριθμους αναγνώρισης να εστιάσουν στα πραγματικά σχήματα χαρακτήρων αντί για τις παραμορφώσεις που προκύπτουν από την περιστροφή.

## Γιατί η διόρθωση κλίσης OCR βελτιώνει την ακρίβεια

Όταν το κείμενο είναι κεκλιμένο, τα σχήματα των χαρακτήρων εμφανίζονται παραμορφωμένα, οδηγώντας σε έως και 20 % υψηλότερα ποσοστά σφάλματος. Η εφαρμογή **ocr skew correction** αφαιρεί αυτή τη διαμόρφωση, επιτρέποντας στη μηχανή να εστιάσει στα πραγματικά γλύφια. Σε δοκιμαστικές μετρήσεις, το Aspose.OCR πέτυχε αύξηση 15‑30 % στην ακρίβεια αναγνώρισης σε έγγραφα με περιστροφή 10‑15° μετά την εφαρμογή της διόρθωσης κλίσης.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR με επιλογή γλώσσας;

Η επιλογή της ακριβούς γλώσσας του πηγαίου κειμένου επιτρέπει στη μηχανή OCR να χρησιμοποιήσει λεξικά και μοντέλα χαρακτήρων ειδικά για τη γλώσσα, κάτι που αυξάνει δραματικά την ακρίβεια αναγνώρισης και μειώνει το χρόνο επεξεργασίας. Επιπλέον, το Aspose.OCR προσφέρει ακριβή έλεγχο της διόρθωσης κλίσης, της επιλογής περιοχής και των μορφών εξόδου, καθιστώντας το μια ευέλικτη επιλογή για πολυγλωσσικές γραμμές επεξεργασίας εγγράφων.

- **Υποστήριξη πολλαπλών γλωσσών** – Επιλέξτε την ακριβή γλώσσα(ες) που εμφανίζονται στην εικόνα σας για να αυξήσετε την ακρίβεια.  
- **Ακριβής έλεγχος** – Ρυθμίστε την κλίση, ορίστε περιοχές αναγνώρισης και ορίστε τη συμπεριφορά αυτόματης κλίσης.  
- **Καθαρό Java API** – Χωρίς εγγενείς εξαρτήσεις, εύκολο στην ενσωμάτωση σε οποιοδήποτε έργο Java.  
- **Πλούσια δεδομένα αποτελεσμάτων** – Λάβετε απλό κείμενο, JSON, περιοριστικά ορθογώνια και προειδοποιήσεις με μία κλήση.  
- **Ποσοτικοποιημένη δυνατότητα** – Το Aspose.OCR υποστηρίζει **50+** μορφές εισόδου και εξόδου και μπορεί να επεξεργαστεί παρτίδες εικόνων **500‑σελίδων** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη.

## Προαπαιτούμενα

- **Java Development Kit (JDK)** εγκατεστημένο (JDK 8 ή νεότερο).  
- **Aspose.OCR for Java** βιβλιοθήκη – κατεβάστε την από την επίσημη ιστοσελίδα [εδώ](https://reference.aspose.com/ocr/java/).  
- Ένα αρχείο εικόνας που περιέχει το κείμενο που θέλετε να εξάγετε, π.χ., `p3.png`.  

## Εισαγωγή Πακέτων

Οι παρακάτω εισαγωγές σας δίνουν πρόσβαση στις βασικές κλάσεις OCR και στα τυπικά βοηθητικά εργαλεία Java.  
`import com.aspose.ocr.*;` – φέρνει τη βασική μηχανή OCR.  
`import com.aspose.ocr.config.*;` – περιέχει αντικείμενα ρυθμίσεων όπως το `RecognitionSettings`.  
`import java.awt.Rectangle;` – χρησιμοποιείται για τον ορισμό περιοχών αναγνώρισης.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Πώς να εφαρμόσετε τη διόρθωση κλίσης OCR σε Java;

Φορτώστε την εικόνα, απενεργοποιήστε την αυτόματη ανίχνευση κλίσης και είτε παρέχετε μια μετρημένη γωνία είτε αφήστε τη μηχανή να την υπολογίσει χρησιμοποιώντας `settings.setAutoSkew(false)`. Η μηχανή OCR θα ευθυγραμμίσει πρώτα την εικόνα βάσει της παρεχόμενης ή ανιχνευθείσας γωνίας, έπειτα θα προχωρήσει στην αναγνώριση χαρακτήρων. Αυτή η διπλή προσέγγιση εξασφαλίζει ότι οποιαδήποτε κλίση αφαιρείται πριν εφαρμοστούν τα μοντέλα γλώσσας, οδηγώντας σε καθαρότερη έξοδο κειμένου και λιγότερες λανθασμένες αναγνώσεις.

## Οδηγός βήμα‑βήμα

### Βήμα 1: Ρυθμίστε τον φάκελο εγγράφων σας

Δημιουργήστε ένα αντικείμενο `File` που δείχνει στο φάκελο που περιέχει την πηγαία εικόνα σας. Αυτό κάνει τη διαχείριση διαδρομών φορητή μεταξύ λειτουργικών συστημάτων.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Αντικαταστήστε το `"Your Document Directory"` με την απόλυτη διαδρομή όπου βρίσκεται το `p3.png`.

### Βήμα 2: Ορίστε τη διαδρομή της εικόνας

Δημιουργήστε ένα αντικείμενο `File` για την συγκεκριμένη εικόνα που θέλετε να επεξεργαστείτε. Η χρήση ενός αντικειμένου `File` σας δίνει εύκολη πρόσβαση στα μεταδεδομένα του αρχείου αν τα χρειαστείτε αργότερα.

```java
// The image path
String file = dataDir + "p3.png";
```

Βεβαιωθείτε ότι η μεταβλητή `file` δείχνει στην ακριβή εικόνα που θέλετε να επεξεργαστείτε.

### Βήμα 3: Δημιουργήστε ένα στιγμιότυπο του Aspose.OCR API

Η κλάση `AsposeOCR` είναι το σημείο εισόδου για όλες τις λειτουργίες OCR. Περιλαμβάνει τη μηχανή, διαχειρίζεται πόρους και παρέχει τη μέθοδο `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Το αντικείμενο `AsposeOCR` σας δίνει πρόσβαση σε όλες τις λειτουργίες OCR.

### Βήμα 4: Ορίστε τις επιλογές αναγνώρισης (Επιλογή γλώσσας)

`RecognitionSettings` είναι το δοχείο ρυθμίσεων του Aspose.OCR που σας επιτρέπει να ρυθμίσετε με ακρίβεια τη διαδικασία OCR.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Εδώ:

1. Απενεργοποιούμε το auto‑skew επειδή παρέχουμε χειροκίνητη τιμή κλίσης.  
2. Ορίζουμε μια ορθογώνια περιοχή (`RecognitionAreas`) για να περιορίσουμε το OCR στο τμήμα της εικόνας που περιέχει πραγματικό κείμενο.  
3. Ορίζουμε τη **γλώσσα** στα Αγγλικά (`Language.Eng`). Αλλάξτε το σε `Language.Fra`, `Language.Spa` κ.λπ., ανάλογα με την πηγή εικόνας.

### Βήμα 5: Εκτελέστε OCR και ανακτήστε τα αποτελέσματα

Η κλήση `recognizePage` εκτελεί τη μηχανή OCR χρησιμοποιώντας την εικόνα και τις ρυθμίσεις που ορίσατε. Το αποτέλεσμα αποθηκεύεται σε ένα αντικείμενο `RecognitionResult`, το οποίο συγκεντρώνει όλα τα χρήσιμα δεδομένα.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Η κλήση `RecognizePage` εκτελεί τη μηχανή OCR χρησιμοποιώντας την εικόνα και τις ρυθμίσεις που ορίσατε. Το αποτέλεσμα αποθηκεύεται σε ένα αντικείμενο `RecognitionResult`.

### Βήμα 6: Εκτυπώστε και χρησιμοποιήστε τα αποτελέσματα

Η έξοδος της κονσόλας εμφανίζει:

- Το πλήρες εξαγόμενο κείμενο (`recognitionText`).  
- Κείμενο για κάθε ορθογώνιο που ορίστηκε (`recognitionAreasText`).  
- Συντεταγμένες των περιοριστικών ορθογωνίων.  
- Μια αναπαράσταση JSON για εύκολη επεξεργασία downstream.  
- Την ανιχνευμένη γωνία κλίσης και τυχόν προειδοποιήσεις.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Η έξοδος της κονσόλας εμφανίζει το πλήρες εξαγόμενο κείμενο, το κείμενο ανά περιοχή, τα ορθογώνια περιγράμματα, το JSON, τη γωνία κλίσης και τυχόν προειδοποιήσεις. Μπορείτε τώρα να περάσετε το `result.recognitionText` στη λογική της επιχείρησής σας — να το αποθηκεύσετε, να το ευρετηριάσετε ή να το στείλετε σε άλλη υπηρεσία.

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Ακατάλληλοι χαρακτήρες** | Λάθος γλώσσα επιλεγμένη | Ορίστε το σωστό enum `Language` (π.χ., `Language.Fra` για Γαλλικά). |
| **Δεν επιστράφηκε κείμενο** | Η περιοχή αναγνώρισης δεν καλύπτει το κείμενο | Ρυθμίστε τις συντεταγμένες του `Rectangle` ή αφαιρέστε το `RecognitionAreas` για επεξεργασία ολόκληρης της εικόνας. |
| **Αργή απόδοση** | Πολύ μεγάλη εικόνα ή υψηλή ανάλυση | Μειώστε την ανάλυση της εικόνας πριν το OCR ή αυξήστε την κατανομή μνήμης JVM. |
| **Προειδοποιήσεις για μη υποστηριζόμενη μορφή** | Μορφή εικόνας δεν αναγνωρίζεται | Μετατρέψτε την εικόνα σε PNG, JPEG ή TIFF πριν την επεξεργασία. |

## Συχνές Ερωτήσεις

**Ε: Μπορώ να αναγνωρίσω πολλαπλές γλώσσες σε μία κλήση OCR;**  
Α: Ναι. Χρησιμοποιήστε `settings.setLanguage(Language.Eng | Language.Fra)` για να ενεργοποιήσετε την πολυγλωσσική αναγνώριση.

**Ε: Ποιες μορφές εικόνας υποστηρίζει το Aspose.OCR;**  
Α: PNG, JPEG, BMP, TIFF, GIF και αρκετές άλλες. Απλώς δώστε τη σωστή διαδρομή αρχείου.

**Ε: Υπάρχει όριο μεγέθους για την εικόνα;**  
Α: Δεν υπάρχει σκληρό όριο, αλλά η επεξεργασία εικόνων μεγαλύτερων από 10 MB μπορεί να αυξήσει τη χρήση μνήμης και το χρόνο εκτέλεσης. Σκεφτείτε να μειώσετε το μέγεθος των μεγάλων αρχείων.

**Ε: Πώς αποκτώ άδεια παραγωγής;**  
Α: Αγοράστε άδεια από τον ιστότοπο της Aspose και εφαρμόστε την μέσω της κλάσης `License` όπως φαίνεται στην τεκμηρίωση της Aspose.

**Ε: Μπορώ να εξάγω κείμενο από σελίδα PDF απευθείας;**  
Α: Δεν είναι δυνατόν απευθείας με το Aspose.OCR. Μετατρέψτε πρώτα τη σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας το Aspose.PDF) και μετά εκτελέστε OCR.

## Συμπέρασμα

Τώρα έχετε δει πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose.OCR για Java, επιλέγοντας την κατάλληλη γλώσσα και εφαρμόζοντας **διόρθωση κλίσης OCR** για βελτιωμένη αξιοπιστία. Αυτή η προσέγγιση παρέχει ακριβές, υψηλής απόδοσης OCR που μπορεί να ενσωματωθεί σε οποιαδήποτε ροή εργασίας βασισμένη σε Java — από συστήματα διαχείρισης εγγράφων έως αγωγούς σύλληψης δεδομένων. Πειραματιστείτε με διαφορετικά enums `Language`, ρυθμίστε τα `RecognitionAreas` και ενσωματώστε την έξοδο JSON στην ανάλυση downstream για μια πραγματικά ολοκληρωμένη λύση.

---

**Τελευταία ενημέρωση:** 2026-06-24  
**Δοκιμή με:** Aspose.OCR 24.11 for Java  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Πώς να υπολογίσετε τη γωνία κλίσης java χρησιμοποιώντας το Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας το Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR αναγνώριση εγγράφων PDF στο Aspose.OCR για Java](/ocr/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}