---
date: 2026-02-12
description: Μάθετε πώς να κάνετε OCR κειμένου εικόνας με επιλογή γλώσσας χρησιμοποιώντας
  το Aspose.OCR για Java. Αυτός ο οδηγός βήμα‑προς‑βήμα καλύπτει την εξαγωγή κειμένου
  σε Java, τη διόρθωση κλίσης OCR και πολλά άλλα.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας το Aspose.OCR
url: /el/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας το Aspose.OCR

## Εισαγωγή

Η εξαγωγή κειμένου από αρχεία εικόνας είναι μια συχνή απαίτηση, είτε ψηφιοποιείτε σαρωμένα έγγραφα, επεξεργάζεστε αποδείξεις ή δημιουργείτε αρχεία αναζήτησης. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, πρακτικό παράδειγμα που δείχνει **πώς να κάνετε OCR κειμένου εικόνας** με συγκεκριμένη ρύθμιση γλώσσας, ώστε να ενσωματώσετε αξιόπιστο OCR στις Java εφαρμογές σας σήμερα. Θα δείτε επίσης πώς να διαχειριστείτε τη διόρθωση κλίσης OCR και την αναγνώριση βάσει περιοχής για βέλτιστη ακρίβεια.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR σε Java;** Aspose.OCR for Java  
- **Ποια ρύθμιση επιλέγει τη γλώσσα;** `settings.setLanguage(Language.Eng)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα)  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν άδεια αξιολόγησης λειτουργεί για δοκιμές· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να περιορίσω το OCR σε μια περιοχή της εικόνας;** Ναι, χρησιμοποιήστε `RecognitionSettings.setRecognitionAreas()` με ορθογώνια.  
- **Ποιος είναι ο τυπικός χρόνος εκτέλεσης;** Μερικά δευτερόλεπτα ανά σελίδα σε ένα τυπικό laptop, ανάλογα με το μέγεθος της εικόνας και την πολυπλοκότητα της γλώσσας.

## Πώς να κάνετε OCR κειμένου εικόνας με επιλογή γλώσσας
Σε αυτήν την ενότητα απαντάμε στην κεντρική ερώτηση **πώς να κάνετε OCR** μια εικόνα όταν γνωρίζετε τη γλώσσα του κειμένου. Η επιλογή της σωστής γλώσσας βελτιώνει δραστικά την ακρίβεια αναγνώρισης, επειδή η μηχανή OCR μπορεί να εφαρμόσει λεξικά και μοντέλα χαρακτήρων ειδικά για τη γλώσσα.

### Γιατί είναι σημαντικό
- **Υψηλότερη ακρίβεια** – μοντέλα ειδικά για τη γλώσσα μειώνουν τις λανθασμένες αναγνώσεις.  
- **Βελτίωση απόδοσης** – η μηχανή παραλείπει περιττούς ελέγχους γλώσσας.  
- **Καλύτερη διαχείριση διακριτικών** – τα γαλλικά, ισπανικά, γερμανικά κ.λπ., αναγνωρίζονται σωστά όταν χρησιμοποιείται το αντίστοιχο `Language` enum.

## Τι είναι η «εξαγωγή κειμένου από εικόνα»;
Η εξαγωγή κειμένου από εικόνα (OCR) μετατρέπει την οπτική αναπαράσταση χαρακτήρων σε μηχανικά αναγνώσιμες συμβολοσειρές. Αυτό επιτρέπει την αναζήτηση, την ανάλυση και τις ροές εργασίας εξαγωγής δεδομένων που διαφορετικά θα απαιτούσαν χειροκίνητη μεταγραφή.

## Γιατί να χρησιμοποιήσετε το Aspose.OCR με επιλογή γλώσσας;
- **Πολυγλωσσική υποστήριξη** – Επιλέξτε την ακριβή γλώσσα(ες) που εμφανίζονται στην εικόνα σας για να αυξήσετε την ακρίβεια.  
- **Λεπτομερής έλεγχος** – Ρυθμίστε την κλίση, ορίστε περιοχές αναγνώρισης και ορίστε τη συμπεριφορά αυτόματης κλίσης.  
- **Καθαρό Java API** – Χωρίς εγγενείς εξαρτήσεις, εύκολο στην ενσωμάτωση σε οποιοδήποτε Java project.  
- **Πλούσια δεδομένα αποτελέσματος** – Λάβετε απλό κείμενο, JSON, ορθογώνια περιγράμματα και προειδοποιήσεις σε μία κλήση.

## Προαπαιτούμενα

- **Java Development Kit (JDK)** εγκατεστημένο (JDK 8 ή νεότερο).  
- **Aspose.OCR for Java** βιβλιοθήκη – κατεβάστε την από την επίσημη ιστοσελίδα [εδώ](https://reference.aspose.com/ocr/java/).  
- Ένα αρχείο εικόνας που περιέχει το κείμενο που θέλετε να εξάγετε, π.χ., `p3.png`.

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

## Οδηγός βήμα‑βήμα

### Βήμα 1: Ρυθμίστε τον Κατάλογο Εγγράφων σας

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Αντικαταστήστε το `"Your Document Directory"` με την απόλυτη διαδρομή όπου βρίσκεται το `p3.png`.

### Βήμα 2: Ορίστε τη Διαδρομή της Εικόνας

```java
// The image path
String file = dataDir + "p3.png";
```

Βεβαιωθείτε ότι η μεταβλητή `file` δείχνει στην ακριβή εικόνα που θέλετε να επεξεργαστείτε.

### Βήμα 3: Δημιουργήστε ένα Αντικείμενο Aspose.OCR API

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
2. Ορίζουμε μια ορθογώνια περιοχή (`RecognitionAreas`) για να περιορίσουμε το OCR στο τμήμα της εικόνας που περιέχει πραγματικό κείμενο.  
3. Ορίζουμε τη **γλώσσα** στα Αγγλικά (`Language.Eng`). Αλλάξτε το σε `Language.Fra`, `Language.Spa`, κ.λπ., ανάλογα με την πηγή εικόνας.

### Βήμα 5: Εκτελέστε OCR και Ανακτήστε τα Αποτελέσματα

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

Η έξοδος της κονσόλας εμφανίζει:

- Το πλήρες εξαγόμενο κείμενο (`recognitionText`).  
- Κείμενο για κάθε ορθογώνιο (`recognitionAreasText`).  
- Συντεταγμένες του ορθογωνίου περιγράμματος.  
- Μια αναπαράσταση JSON για εύκολη επεξεργασία downstream.  
- Την ανιχνευμένη γωνία κλίσης και τυχόν προειδοποιήσεις.

Μπορείτε τώρα να περάσετε το `result.recognitionText` στη λογική της επιχείρησής σας — να το αποθηκεύσετε, να το ευρετηριάσετε ή να το στείλετε σε άλλη υπηρεσία.

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Λύση |
|----------|-------|------|
| **Garbage characters** | Wrong language selected | Set the correct `Language` enum (e.g., `Language.Fra` for French). |
| **No text returned** | Recognition area does not cover the text | Adjust the `Rectangle` coordinates or remove `RecognitionAreas` to process the whole image. |
| **Slow performance** | Very large image or high resolution | Downscale the image before OCR or increase memory allocation for the JVM. |
| **Warnings about unsupported format** | Image format not recognized | Convert the image to PNG, JPEG, or TIFF before processing. |

## Συχνές Ερωτήσεις

**Ε: Μπορώ να αναγνωρίσω πολλαπλές γλώσσες σε μία κλήση OCR;**  
Α: Ναι. Χρησιμοποιήστε `settings.setLanguage(Language.Eng | Language.Fra)` για να ενεργοποιήσετε την πολυγλωσσική αναγνώριση.

**Ε: Ποιες μορφές εικόνας υποστηρίζει το Aspose.OCR;**  
Α: PNG, JPEG, BMP, TIFF, GIF και αρκετές άλλες. Απλώς δώστε τη σωστή διαδρομή αρχείου.

**Ε: Υπάρχει όριο μεγέθους για την εικόνα;**  
Α: Δεν υπάρχει σκληρό όριο, αλλά πολύ μεγάλες εικόνες αυξάνουν τη χρήση μνήμης και τον χρόνο επεξεργασίας. Σκεφτείτε να αλλάξετε το μέγεθος των μεγάλων αρχείων.

**Ε: Πώς αποκτώ άδεια παραγωγής;**  
Α: Αγοράστε άδεια από την ιστοσελίδα της Aspose και εφαρμόστε την μέσω της κλάσης `License` όπως φαίνεται στην τεκμηρίωση της Aspose.

**Ε: Μπορώ να εξάγω κείμενο απευθείας από σελίδα PDF;**  
Α: Δεν είναι δυνατόν απευθείας με το Aspose.OCR. Μετατρέψτε πρώτα τη σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας το Aspose.PDF) και έπειτα εκτελέστε OCR.

## Συμπέρασμα

Τώρα έχετε δει πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose.OCR για Java, επιλέγοντας την κατάλληλη γλώσσα και περιορίζοντας την αναγνώριση σε συγκεκριμένες περιοχές. Αυτή η προσέγγιση παρέχει ακριβές, υψηλής απόδοσης OCR που μπορεί να ενσωματωθεί σε οποιαδήποτε ροή εργασίας βασισμένη σε Java — από συστήματα διαχείρισης εγγράφων μέχρι pipelines καταγραφής δεδομένων. Έτοιμοι να προχωρήσετε; Δοκιμάστε να αλλάξετε το enum της γλώσσας, πειραματιστείτε με διαφορετικές περιοχές αναγνώρισης και ενσωματώστε τα αποτελέσματα στην δική σας λογική εφαρμογής.

---

**Τελευταία ενημέρωση:** 2026-02-12  
**Δοκιμή με:** Aspose.OCR 24.11 for Java  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}