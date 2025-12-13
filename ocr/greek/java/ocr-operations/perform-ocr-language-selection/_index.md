---
date: 2025-12-13
description: Μάθετε πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose.OCR
  για Java με επιλογή γλώσσας. Αυτό το βήμα‑βήμα σεμινάριο Aspose OCR Java δείχνει
  ακριβή διαμόρφωση OCR.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Πώς να εξάγετε κείμενο από εικόνα με επιλογή γλώσσας χρησιμοποιώντας το Aspose.OCR
url: /el/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Κείμενο από Εικόνα με Επιλογή Γλώσσας Χρησιμοποιώντας το Aspose.OCR

## Εισαγωγή

Η εξαγωγή κειμένου από αρχεία εικόνας είναι μια κοινή ανάγκη, είτε ψηφιοποιείτε σαρωμένα έγγραφα, επεξεργάζεστε αποδείξεις ή δημιουργείτε αρχεία με δυνατότητα αναζήτησης. Το Aspose.OCR για Java κάνει αυτή τη διαδικασία απλή και προσφέρει λεπτομερή έλεγχο της επιλογής γλώσσας, της διόρθωσης κλίσης και των περιοχών αναγνώρισης. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, πρακτικό παράδειγμα που δείχνει **πώς να εξάγετε κείμενο από εικόνα** με συγκεκριμένη ρύθμιση γλώσσας, ώστε να ενσωματώσετε αξιόπιστο OCR στις Java εφαρμογές σας σήμερα.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη χειρίζεται OCR σε Java;** Aspose.OCR για Java  
- **Ποια ρύθμιση επιλέγει τη γλώσσα;** `settings.setLanguage(Language.Eng)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα)  
- **Χρειάζεται άδεια για ανάπτυξη;** Μια δωρεάν άδεια αξιολόγησης λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να περιορίσω το OCR σε περιοχή της εικόνας;** Ναι, χρησιμοποιήστε `RecognitionSettings.setRecognitionAreas()` με ορθογώνια.  
- **Ποιος είναι ο τυπικός χρόνος εκτέλεσης;** Μερικά δευτερόλεπτα ανά σελίδα σε τυπικό laptop, ανάλογα με το μέγεθος της εικόνας και την πολυπλοκότητα της γλώσσας.

## Τι είναι η “εξαγωγή κειμένου από εικόνα”;
Η εξαγωγή κειμένου από εικόνα (OCR) μετατρέπει την οπτική αναπαράσταση χαρακτήρων σε μη‑αξιόπιστες συμβολοσειρές. Αυτό επιτρέπει αναζήτηση, αναλύσεις και ροές εξαγωγής δεδομένων που διαφορετικά θα απαιτούσαν χειροκίνητη μεταγραφή.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR με επιλογή γλώσσας;
- **Υποστήριξη πολλαπλών γλωσσών** – Επιλέξτε την ακριβή γλώσσα(ες) που εμφανίζονται στην εικόνα σας για μεγαλύτερη ακρίβεια.  
- **Λεπτομερής έλεγχος** – Ρυθμίστε την κλίση, ορίστε περιοχές αναγνώρισης και καθορίστε τη συμπεριφορά αυτόματης κλίσης.  
- **Καθαρό Java API** – Χωρίς εξαρτήσεις native, εύκολο στην ενσωμάτωση σε οποιοδήποτε Java project.  
- **Πλούσια δεδομένα αποτελέσματος** – Λάβετε απλό κείμενο, JSON, ορθογώνια περιθώρια και προειδοποιήσεις με μία κλήση.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **Java Development Kit (JDK)** εγκατεστημένο (JDK 8 ή νεότερο).  
- **Aspose.OCR για Java** βιβλιοθήκη – κατεβάστε την από την επίσημη ιστοσελίδα [εδώ](https://reference.aspose.com/ocr/java/).  
- Ένα αρχείο εικόνας που περιέχει το κείμενο που θέλετε να εξάγετε, π.χ. `p3.png`.

## Εισαγωγή Πακέτων

Στο αρχείο πηγαίου κώδικα Java, συμπεριλάβετε τις απαιτούμενες κλάσεις Aspose.OCR και τις τυπικές βοηθητικές κλάσεις Java:

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

## Οδηγός Βήμα‑Βήμα

### Βήμα 1: Ρυθμίστε τον Κατάλογο Εγγράφων σας

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Αντικαταστήστε το `"Your Document Directory"` με το απόλυτο μονοπάτι όπου βρίσκεται το `p3.png`.

### Βήμα 2: Ορίστε τη Διαδρομή της Εικόνας

```java
// The image path
String file = dataDir + "p3.png";
```

Βεβαιωθείτε ότι η μεταβλητή `file` δείχνει στην ακριβή εικόνα που θέλετε να επεξεργαστείτε.

### Βήμα 3: Δημιουργήστε Παράδειγμα του Aspose.OCR API

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Το αντικείμενο `AsposeOCR` σας δίνει πρόσβαση σε όλες τις λειτουργίες OCR.

### Βήμα 4: Ορίστε τις Επιλογές Αναγνώρισης (Επιλογή Γλώσσας)

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
2. Ορίζουμε μια ορθογώνια περιοχή (`RecognitionAreas`) για να περιορίσουμε το OCR στο τμήμα της εικόνας που περιέχει κείμενο.  
3. Ορίζουμε τη **γλώσσα** στα Αγγλικά (`Language.Eng`). Αλλάξτε το σε `Language.Fra`, `Language.Spa` κ.λπ., ανάλογα με την πηγή εικόνας.

### Βήμα 5: Εκτελέστε το OCR και Λάβετε τα Αποτελέσματα

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

### Βήμα 6: Εκτυπώστε και Χρησιμοποιήστε τα Αποτελέσματα

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

Η έξοδος στην κονσόλα εμφανίζει:

- Το πλήρες εξαγόμενο κείμενο (`recognitionText`).  
- Κείμενο για κάθε ορθογώνιο (`recognitionAreasText`).  
- Συντεταγμένες των ορθογωνίων περιθωρίων.  
- Μια αναπαράσταση JSON για εύκολη επεξεργασία downstream.  
- Την ανιχνευμένη γωνία κλίσης και τυχόν προειδοποιήσεις.

Τώρα μπορείτε να τροφοδοτήσετε το `result.recognitionText` στη λογική της επιχείρησής σας — να το αποθηκεύσετε, να το ευρετηριάσετε ή να το περάσετε σε άλλη υπηρεσία.

## Συνηθισμένα Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Ακατάλληλοι χαρακτήρες** | Λάθος γλώσσα επιλεγμένη | Ορίστε το σωστό enum `Language` (π.χ., `Language.Fra` για γαλλικά). |
| **Δεν επιστρέφεται κείμενο** | Η περιοχή αναγνώρισης δεν καλύπτει το κείμενο | Προσαρμόστε τις συντεταγμένες του `Rectangle` ή αφαιρέστε το `RecognitionAreas` για επεξεργασία ολόκληρης της εικόνας. |
| **Αργή απόδοση** | Πολύ μεγάλη ή υψηλής ανάλυσης εικόνα | Μειώστε την ανάλυση της εικόνας πριν το OCR ή αυξήστε τη μνήμη που διατίθεται στη JVM. |
| **Προειδοποιήσεις για μη υποστηριζόμενη μορφή** | Μορφή εικόνας δεν αναγνωρίζεται | Μετατρέψτε την εικόνα σε PNG, JPEG ή TIFF πριν την επεξεργασία. |

## Συχνές Ερωτήσεις

**Ε: Μπορώ να αναγνωρίσω πολλαπλές γλώσσες σε μία κλήση OCR;**  
Α: Ναι. Χρησιμοποιήστε `settings.setLanguage(Language.Eng | Language.Fra)` για ενεργοποίηση πολυγλωσσικής αναγνώρισης.

**Ε: Ποιες μορφές εικόνας υποστηρίζει το Aspose.OCR;**  
Α: PNG, JPEG, BMP, TIFF, GIF και αρκετές άλλες. Απλώς δώστε το σωστό μονοπάτι αρχείου.

**Ε: Υπάρχει όριο μεγέθους για την εικόνα;**  
Α: Δεν υπάρχει σκληρό όριο, αλλά πολύ μεγάλες εικόνες αυξάνουν τη χρήση μνήμης και τον χρόνο επεξεργασίας. Σκεφτείτε να αλλάξετε το μέγεθος των μεγάλων αρχείων.

**Ε: Πώς αποκτώ άδεια παραγωγής;**  
Α: Αγοράστε άδεια από την ιστοσελίδα της Aspose και εφαρμόστε την μέσω της κλάσης `License` όπως φαίνεται στην τεκμηρίωση του Aspose.

**Ε: Μπορώ να εξάγω κείμενο απευθείας από σελίδα PDF;**  
Α: Δεν απευθείας με το Aspose.OCR. Μετατρέψτε πρώτα τη σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας το Aspose.PDF) και έπειτα τρέξτε το OCR.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose.OCR για Java, επιλέγοντας τη σωστή γλώσσα και περιορίζοντας την αναγνώριση σε συγκεκριμένες περιοχές. Αυτή η προσέγγιση προσφέρει ακριβές, υψηλής απόδοσης OCR που μπορεί να ενσωματωθεί σε οποιαδήποτε Java‑βασισμένη ροή εργασίας — από συστήματα διαχείρισης εγγράφων μέχρι pipelines καταγραφής δεδομένων.

---

**Τελευταία ενημέρωση:** 2025-12-13  
**Δοκιμασμένο με:** Aspose.OCR 24.11 για Java  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}