---
category: general
date: 2026-06-22
description: 'Πώς να διορθώσετε την κλίση μιας εικόνας για OCR: μάθετε τα βήματα προεπεξεργασίας
  εικόνας για OCR, αφαιρέστε τον θόρυβο αλατιού‑πιπεριού και αυξήστε την ακρίβεια.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας για OCR, να αφαιρέσετε τον
  θόρυβο άλατος και πιπεριού και να εφαρμόσετε τεχνικές προεπεξεργασίας εικόνων OCR
  σε ένα πλήρες παράδειγμα Java.
og_title: Πώς να αφαιρέσετε την κλίση της εικόνας – Οδηγός προεπεξεργασίας εικόνας
  για OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Πώς να διορθώσετε την κλίση της εικόνας – Οδηγός προεπεξεργασίας εικόνας για
  OCR
url: /el/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση εικόνας – Οδηγός Προεπεξεργασίας Εικόνας OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση μιας εικόνας** ώστε η μηχανή OCR σας να διαβάζει πραγματικά το κείμενο; Δεν είστε οι μόνοι. Μια κεκλιμένη σάρωση μπορεί να μετατρέψει ένα τέλειο έγγραφο σε ακατάστατο μπερδεμένο κείμενο, και οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα τουλάχιστον μία φορά.

Σε αυτό το tutorial θα περάσουμε από μια πλήρη **image preprocessing OCR** αλυσίδα που όχι μόνο διορθώνει την περιστροφή αλλά επίσης **αφαιρεί αλάτι‑πιπέρι** τεχνάσματα και ενισχύει την αντίθεση — ουσιαστικά όλα όσα χρειάζεστε για **preprocess images OCR**‑στυλ πριν τα δώσετε στη μηχανή. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση Java snippet και ένα σαφές νοητικό μοντέλο για το γιατί κάθε βήμα είναι σημαντικό.

## Πώς να διορθώσετε την κλίση εικόνας – Δημιουργία της Αλυσίδας Προεπεξεργασίας

Η καρδιά κάθε ροής εργασίας φιλικής προς OCR είναι ένα αντικείμενο **preprocess options** που συνδέει μια σειρά φίλτρων. Σκεφτείτε το ως έναν διαδρόμιο: κάθε φίλτρο κάνει μία εργασία, μετά περνάει την εικόνα στο επόμενο. Παρακάτω υπάρχει ένα ελάχιστο αλλά πλήρες παράδειγμα που χρησιμοποιεί μια υποθετική βιβλιοθήκη OCR με `DeskewFilter`, `DenoiseFilter` και `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Γιατί λειτουργεί αυτό

* **DeskewFilter** αναλύει τις κυρίαρχες γραμμές κειμένου της εικόνας, εκτιμά τη γωνία και περιστρέφει το bitmap πίσω στην οριζόντια θέση. Οι περισσότερες βιβλιοθήκες περιορίζουν τη διόρθωση στα ±15° επειδή μεγαλύτερες γωνίες συνήθως υποδεικνύουν μια κακώς σαρωμένη σελίδα που χρειάζεται χειροκίνητη παρέμβαση.
* **DenoiseFilter** στοχεύει στο κλασικό μοτίβο *αλάτι‑πιπέρι* — εκείνα τα απομονωμένα μαύρα ή λευκά pixel που μοιάζουν με θόρυβο σε τηλεόραση. Η αφαίρεσή τους αποτρέπει τη μηχανή OCR από το να συγχέει τον θόρυβο με χαρακτήρες.
* **ContrastBoostFilter** τεντώνει το ιστόγραμμα, κάνοντας τα αδύναμα στίγματα να ξεχωρίζουν. Ένας πολλαπλασιαστής `1.5f` είναι μια ασφαλής προεπιλογή· μπορείτε να τον αυξήσετε αν οι σαρώσεις σας είναι ιδιαίτερα ξεθωριασμένες.

> **Pro tip:** Αν γνωρίζετε ότι τα έγγραφά σας δεν υπερβαίνουν ποτέ κλίση 10°, περάστε αυτό το μικρότερο όριο στο `DeskewFilter` — ο αλγόριθμος τρέχει πιο γρήγορα και είναι λιγότερο πιθανό να υπερδιορθώσει.

## Image Preprocessing OCR: Προσθήκη Φίλτρων στη Σωστή Σειρά

Η σειρά έχει σημασία. Φανταστείτε ότι αφαιρείτε τον θόρυβο *πριν* την ευθυγράμμιση· ο θόρυβος μπορεί να διαταράξει την ανίχνευση γωνίας, οδηγώντας σε αποτέλεσμα με λανθασμένη ευθυγράμμιση. Αντίστροφα, η εφαρμογή ενίσχυσης αντίθεσης *μετά* την ευθυγράμμιση εξασφαλίζει ότι η περιστροφή δεν εισάγει νέα τεχνάσματα.

Παρακάτω είναι μια γρήγορη λίστα ελέγχου που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε οποιοδήποτε έργο:

| Βήμα | Φίλτρο | Αιτία |
|------|--------|--------|
| 1 | `DeskewFilter` | Ευθυγραμμίζει τη γραμμή βάσης του κειμένου |
| 2 | `DenoiseFilter` | Αφαιρεί τον απομονωμένο θόρυβο pixel |
| 3 | `ContrastBoostFilter` | Βελτιώνει την αναγνωσιμότητα για OCR |

Αν χρειαστεί να προσθέσετε επιπλέον βήματα — π.χ., ένα φίλτρο **binarization** για δυαδικό OCR — θα το τοποθετήσετε **μετά** την ενίσχυση αντίθεσης, επειδή μια καθαρή, υψηλής αντίθεσης εικόνα δυαδικοποιείται πιο ακριβώς.

## Αφαίρεση Θορύβου Αλάτι‑Πιπέρι με DenoiseFilter

Ο θόρυβος αλάτι‑πιπέρι είναι διάσημος σε σαρώσεις χαμηλής ποιότητας, ειδικά εκείνες που προέρχονται από φθηνές κάμερες τηλεφώνου. Το `DenoiseFilter` στη βιβλιοθήκη μας υλοποιεί έναν πυρήνα median‑filter, ο οποίος αντικαθιστά κάθε pixel με τη διάμεσο του περιβάλλοντος γειτονικού του. Το αποτέλεσμα; Τα στίγματα αυτά εξαφανίζονται χωρίς να θολώνουν τους πραγματικούς χαρακτήρες.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Πότε να αυξήσετε το μέγεθος του πυρήνα;* Αν οι πηγαίες εικόνες σας είναι γεμάτες με μεγάλα στίγματα, ένας μεγαλύτερος πυρήνας θα τα καθαρίσει, αλλά προσέξτε: πολύ μεγάλος και μπορεί να αρχίσετε να σβήνετε λεπτές γραμμές σε μικρές γραμματοσειρές.

## Preprocess Images OCR – Εφαρμογή της Αλυσίδας

Μόλις έχετε συναρμολογήσει τη σειρά φίλτρων, η προσάρτησή της στη μηχανή είναι μια γραμμή κώδικα (`engine.setPreprocessOptions`). Από εκείνη τη στιγμή, κάθε κλήση στο `recognizeText` εκτελείται αυτόματα μέσω της αλυσίδας. Δεν χρειάζεται να καλέσετε χειροκίνητα κάθε φίλτρο — ο κώδικάς σας παραμένει καθαρός, και οι μελλοντικές αλλαγές (προσθήκη νέου φίλτρου, ρύθμιση παραμέτρων) είναι κεντρικές.

Ακολουθεί ένα παράδειγμα επιτυχημένης εκτέλεσης με μια δείγμα σάρωσης που αρχικά είχε κλίση 12° και εμφανή θόρυβο pepper:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Παρατηρήστε πώς το κείμενο είναι καθαρό, σωστά προσανατολισμένο, και χωρίς αχρησιμοποίητους χαρακτήρες που διαφορετικά θα εμφανίζονταν ως “I n v o i c e” ή “$‑‑‑”.

## Περιπτώσεις Άκρων & Συνηθισμένα Παγίδες

| Κατάσταση | Τι να προσέξετε | Προτεινόμενη λύση |
|-----------|-------------------|---------------|
| Rotation > 15° | Το DeskewFilter μπορεί να αποτύχει | Προ‑περιστρέψτε χειροκίνητα ή χρησιμοποιήστε φίλτρο μεγαλύτερης εμβέλειας |
| Extremely low resolution ( < 100 dpi ) | Η ενίσχυση αντίθεσης δεν μπορεί να ανακτήσει λεπτομέρειες | Αναδειγματοληψία (resample) της εικόνας πρώτα (π.χ., `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | Το DenoiseFilter μόνο του δεν είναι αρκετό | Συνδέστε ένα `GaussianBlurFilter` πριν το `DenoiseFilter` |
| Color scans with colored text | Απαιτείται μετατροπή σε κλίμακα του γκρι | Εισάγετε `GrayscaleFilter` πριν την ενίσχυση αντίθεσης |

Αν προβλέψετε αυτές τις καταστάσεις, εξοικονομείτε ώρες εντοπισμού σφαλμάτων αργότερα.

## Πλήρες Παράδειγμα Εργασίας (All‑in‑One)

Παρακάτω υπάρχει μια αυτόνομη κλάση Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle που περιλαμβάνει την εξάρτηση `com.example.ocr`. Δείχνει **πώς να διορθώσετε την κλίση εικόνας**, **να αφαιρέσετε θόρυβο αλάτι‑πιπέρι**, και **preprocess images OCR**‑στυλ.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `scanned-document.png` περιέχει ένα σαφές τιμολόγιο):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Αν αντικαταστήσετε την εικόνα με μία που είναι ήδη τέλεια ευθυγραμμισμένη, θα παρατηρήσετε ότι η αλυσίδα εξακολουθεί να λειτουργεί — δεν σπάει τίποτα, και η ακρίβεια του OCR παραμένει υψηλή.

## Συμπέρασμα

Τώρα έχετε μια στέρεη κατανόηση του **πώς να διορθώσετε την κλίση εικόνας** και γιατί κάθε βήμα προεπεξεργασίας — **image preprocessing OCR**, **remove salt pepper**, και **preprocess images OCR** — παίζει κρίσιμο ρόλο στην παροχή καθαρού, αναζητήσιμου κειμένου. Το παραπάνω παράδειγμα είναι πλήρες,

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}