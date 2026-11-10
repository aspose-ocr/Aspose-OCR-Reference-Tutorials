---
category: general
date: 2026-08-22
description: Πώς να ενεργοποιήσετε το OCR γρήγορα και να εξάγετε κείμενο από εικόνες
  τιμολογίων σε Java. Μάθετε να αναγνωρίζετε κείμενο από εικόνα και να μετατρέπετε
  μια εικόνα Java σε κείμενο με Aspose.
keywords:
- how to enable OCR
- recognize text from image
- extract text from invoice
- aspose ocr java
- java ocr tutorial
lastmod: 2026-08-22
og_description: Πώς να ενεργοποιήσετε το OCR σε Java και να εξάγετε κείμενο από εικόνες
  τιμολογίων. Αυτός ο οδηγός σας δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα και
  να μετατρέπετε μια εικόνα Java σε κείμενο με Aspose OCR, καλύπτοντας τη spell‑correction
  και το batch processing.
og_image_alt: Screenshot of Java OCR code extracting text from a scanned invoice using
  Aspose OCR
og_title: Πώς να ενεργοποιήσετε το OCR σε Java – Πλήρης οδηγός για την επεξεργασία
  τιμολογίων
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable OCR quickly and extract text from invoice images in Java.
    Learn to recognize text from image and convert a java image to text with Aspose.
  headline: How to enable OCR in Java – Complete tutorial
  type: TechArticle
- questions:
  - answer: The free trial is limited to evaluation; a commercial license is required
      for production deployments.
    question: Can I use Aspose OCR with a free trial in production?
  - answer: Yes, it supports over 30 languages, including English, German, Spanish,
      Chinese, and Arabic.
    question: Does Aspose OCR support languages beyond French?
  - answer: Convert each page to an image using Aspose PDF or PDFBox, then feed each
      image to the OCR flow in a loop.
    question: How do I process a multi‑page PDF?
  - answer: PNG, JPEG, BMP, TIFF, and GIF are all supported out of the box.
    question: What image formats are accepted?
  - answer: The engine can handle images up to 20 MB; larger files should be split
      or down‑scaled before processing.
    question: Is there a maximum file size?
  type: FAQPage
tags:
- OCR
- Java
- Aspose OCR
- invoice processing
- image to text
title: Πώς να ενεργοποιήσετε το OCR σε Java – Πλήρης οδηγός
url: /el/java/ocr-basics/how-to-enable-ocr-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε το OCR σε Java – Πλήρης οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε το OCR** σε ένα έργο Java χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε μόνοι. Οι προγραμματιστές που δημιουργούν pipelines επεξεργασίας τιμολογίων ή εφαρμογές σάρωσης αντιμετωπίζουν συνεχώς το ίδιο πρόβλημα: η μηχανή OCR λειτουργεί, αλλά το κείμενο είναι γεμάτο τυπογραφικά λάθη, ειδικά για μη‑αγγλικές γλώσσες.  

Σε αυτόν τον οδηγό θα περάσουμε από μια πρακτική λύση που όχι μόνο δείχνει **πώς να ενεργοποιήσετε το OCR**, αλλά επίσης επιδεικνύει **αναγνώριση κειμένου από εικόνα** αρχείων, **εξαγωγή κειμένου από τιμολόγιο** PDF, και ακόμη μετατρέπει μια **java εικόνα σε κείμενο** με λίγες μόνο γραμμές κώδικα. Στο τέλος θα έχετε ένα εκτελέσιμο παράδειγμα, μια σαφή κατανόηση του γιατί κάθε βήμα είναι σημαντικό, και μερικές επαγγελματικές συμβουλές για να διατηρείτε τα αποτελέσματα OCR καθαρά.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR σε Java;** Aspose OCR for Java παρέχει μια πλήρη μηχανή με λεξικά ειδικά για κάθε γλώσσα.  
- **Πόσες γραμμές κώδικα χρειάζονται;** Περίπου δέκα γραμμές για τη ρύθμιση της μηχανής, την ενεργοποίηση της διόρθωσης ορθογραφίας και την ανάγνωση μιας εικόνας.  
- **Ποια έκδοση της Java απαιτείται;** Συνιστάται Java 17 ή νεότερη για βέλτιστη απόδοση.  
- **Μπορώ να επεξεργαστώ PDF πολλαπλών σελίδων;** Ναι—μετατρέψτε κάθε σελίδα σε εικόνα και εκτελέστε την ίδια ροή OCR σε βρόχο.  
- **Χρειάζομαι πληρωμένη άδεια για παραγωγή;** Απαιτείται εμπορική άδεια για παραγωγή· μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση.

## Προαπαιτούμενα — τι θα χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας συντάσσεται με παλαιότερες εκδόσεις, αλλά η Java 17 είναι το ιδανικό σημείο).  
- Άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  
- Ένα δείγμα εικόνας τιμολογίου (π.χ., `french_invoice.png`).  
- Το αγαπημένο σας IDE (IntelliJ, Eclipse, VS Code – όποιο και αν είναι).  

Αυτό είναι όλο. Χωρίς βαριές πλατφόρμες, χωρίς εξωτερικές υπηρεσίες, μόνο απλή Java και Aspose.

![how to enable OCR example](/images/ocr-example.png "Illustration showing how to enable OCR in Java")  
[how to enable OCR example](/images/ocr-example.png "Illustration showing how to enable OCR in Java")

## Κλάση AsposeOCR

`AsposeOCR` είναι η κεντρική κλάση μηχανής OCR της Aspose που ενσωματώνει μοντέλα νευρωνικών δικτύων για αναγνώριση κειμένου και μετα‑επεξεργασία. Όλες οι επόμενες λειτουργίες OCR περνούν μέσω ενός αντικειμένου αυτής της κλάσης.

## Βήμα 1: ρυθμίστε τη μηχανή Aspose OCR – ο πυρήνας του **πώς να ενεργοποιήσετε το OCR**

Πριν μπορέσουμε να μιλήσουμε για **αναγνώριση κειμένου από εικόνα**, χρειαζόμαστε μια παρουσία της μηχανής OCR. Η Aspose OCR παρέχει ένα καθαρό, αντικειμενοστραφές API που αφαιρεί τη χαμηλού επιπέδου διαχείριση εικόνων.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.SpellCorrectionOptions;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine – this is the first thing you do when learning how to enable OCR
        AsposeOCR ocrEngine = new AsposeOCR();
```

**Γιατί είναι σημαντικό:** Η δημιουργία ενός αντικειμένου `AsposeOCR` εκχωρεί τα εσωτερικά μοντέλα νευρωνικού δικτύου και προετοιμάζει τη μηχανή για επόμενες κλήσεις. Η παράλειψη αυτού του βήματος θα προκαλέσει `NullPointerException` τη στιγμή που θα προσπαθήσετε να αναγνωρίσετε μια εικόνα.

## Καταμέτρηση RecognitionLanguage

`RecognitionLanguage` είναι μια απαρίθμηση που ενημερώνει τη μηχανή OCR ποιο λεξικό γλώσσας να χρησιμοποιήσει για διόρθωση ορθογραφίας και επιλογή συνόλου χαρακτήρων.

## Βήμα 2: ενεργοποιήστε τη διόρθωση ορθογραφίας – ένα κρίσιμο μέρος του **πώς να ενεργοποιήσετε το OCR** για πραγματικό κείμενο

Οι περισσότερες βιβλιοθήκες OCR επιστρέφουν ακατέργαστους χαρακτήρες, πράγμα που σημαίνει ότι τα γαλλικά τιμολόγια (ή οποιαδήποτε γλώσσα με τόνους) συχνά περιέχουν λανθασμένες λέξεις. Η Aspose μας επιτρέπει να ενεργοποιήσουμε τη διόρθωση ορθογραφίας με ένα ειδικό αντικείμενο επιλογών.

```java
        // Configure spell‑correction – this dramatically improves accuracy for invoices
        SpellCorrectionOptions spellOptions = new SpellCorrectionOptions();
        spellOptions.setEnable(true);                         // Turn the feature on
        spellOptions.setLanguage(RecognitionLanguage.FRENCH); // Choose the dictionary that matches your invoice
        ocrEngine.setSpellCorrectionOptions(spellOptions);
```

**Γιατί αυτό το βήμα είναι ουσιώδες:** Η ενεργοποίηση της διόρθωσης ορθογραφίας λέει στη μηχανή OCR να μετα‑επεξεργαστεί το ακατέργαστο αποτέλεσμα χρησιμοποιώντας ένα λεξικό ειδικό για τη γλώσσα. Αν εξάγετε κείμενο από ένα αγγλικό ή γερμανικό τιμολόγιο, απλώς αντικαταστήστε το `RecognitionLanguage.FRENCH` με το κατάλληλο enum. Αυτό είναι το «μαγικό κουμπί» που πολλοί προγραμματιστές παραβλέπουν όταν ρωτούν **πώς να ενεργοποιήσετε το OCR** για μια συγκεκριμένη γλώσσα.

## Μέθοδος αναγνώρισης μηχανής

Η μέθοδος `recognizeImage` φορτώνει το bitmap, εκτελεί το νευρωνικό μοντέλο, εφαρμόζει τη διόρθωση ορθογραφίας και επιστρέφει μια καθαρή συμβολοσειρά. Αυτή η ενιαία κλήση κάνει το σκληρό έργο για σενάρια **αναγνώριση κειμένου από εικόνα**.

```java
        // Path to the invoice image – replace with your own file location
        String imagePath = "YOUR_DIRECTORY/french_invoice.png";

        // Perform OCR – this is where we actually recognize text from image
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.FRENCH);

        // Output the corrected text
        System.out.println("Corrected text:\n" + ocrResult.getText());
    }
}
```

**Τι θα δείτε:** Η κονσόλα εκτυπώνει το διορθωμένο κείμενο του τιμολογίου, χωρίς τα περισσότερα σφάλματα που προκαλεί το OCR. Για ένα τυπικό γαλλικό τιμολόγιο μπορεί να εμφανιστεί κάτι όπως:

```
Facture Nº 12345
Date: 01/12/2025
Montant TTC: 1 250,00 €
```

Αν η έξοδος εξακολουθεί να περιέχει ανεπιθύμητους χαρακτήρες, ελέγξτε ξανά την ποιότητα της εικόνας (υψηλή αντίθεση, 300 dpi είναι ιδανικό) και βεβαιωθείτε ότι το enum γλώσσας ταιριάζει με τη γλώσσα του τιμολογίου.

## Βοηθητική κλάση InvoiceOcrProcessor

`InvoiceOcrProcessor` είναι μια βοηθητική κλάση που περιβάλλει τη ρύθμιση της μηχανής και τη λογική αναγνώρισης σε ένα επαναχρησιμοποιήσιμο στοιχείο για επεξεργασία παρτίδων.

## Βήμα 5: ενσωμάτωση της ροής OCR σε μεγαλύτερη εφαρμογή

Αν δημιουργείτε έναν επεξεργαστή παρτίδων που διαβάζει δεκάδες τιμολόγια κάθε βράδυ, τυλίξτε τη λογική παραπάνω σε μια επαναχρησιμοποιήσιμη μέθοδο:

```java
public class InvoiceOcrProcessor {
    private final AsposeOCR engine;

    public InvoiceOcrProcessor() throws Exception {
        engine = new AsposeOCR();
        SpellCorrectionOptions opts = new SpellCorrectionOptions();
        opts.setEnable(true);
        opts.setLanguage(RecognitionLanguage.FRENCH);
        engine.setSpellCorrectionOptions(opts);
    }

    public String extractText(String imagePath) throws Exception {
        OcrResult result = engine.recognizeImage(imagePath, RecognitionLanguage.FRENCH);
        return result.getText();
    }
}
```

Τώρα μπορείτε να δημιουργήσετε ένα αντικείμενο `InvoiceOcrProcessor` μία φορά και να καλέσετε `extractText` για κάθε αρχείο—ιδανικό για εργασίες **εξαγωγής κειμένου από τιμολόγιο**.

## Διαχείριση ακραίων περιπτώσεων – όταν η **εξαγωγή κειμένου από τιμολόγιο** γίνεται δύσκολη

Τα πραγματικά τιμολόγια δεν είναι πάντα τέλειες σάρωση. Εδώ είναι μερικά σενάρια που μπορεί να συναντήσετε, μαζί με γρήγορες λύσεις:

| Κατάσταση | Προτεινόμενη λύση |
|-----------|-------------------|
| Εικόνα χαμηλής ανάλυσης ( < 200 dpi ) | Αυξήστε την εικόνα με μια βιβλιοθήκη όπως `java‑image‑scaling` πριν τη δώσετε στην Aspose. |
| Μικτές γλώσσες (π.χ., Γαλλικά + Αγγλικά) | Εκτελέστε δύο ξεχωριστές διεργασίες OCR, μία ανά γλώσσα, και στη συνέχεια συγχωνεύστε τα αποτελέσματα. |
| Χειρόγραφα σημειώματα στο τιμολόγιο | Η Aspose OCR εστιάζει σε τυπωμένο κείμενο· για χειρόγραφο εξετάστε μια εξειδικευμένη υπηρεσία όπως το Google Vision. |
| Μεγάλα PDF με πολλές σελίδες | Μετατρέψτε κάθε σελίδα σε εικόνα (χρησιμοποιώντας Aspose PDF ή PDFBox) και επαναλάβετε τα βήματα OCR. |

Αυτές οι συμβουλές διατηρούν την αλυσίδα **java εικόνα σε κείμενο** αξιόπιστη, ακόμη και όταν το υλικό προέλευσης δεν είναι ιδανικό.

## Επαγγελματικές συμβουλές & κοινά λάθη

- **Συμβουλή:** Ενεργοποιήστε την καταγραφή (`engine.setLogLevel(LogLevel.DEBUG)`) κατά την ανάπτυξη για να δείτε γιατί ορισμένοι χαρακτήρες αναγνωρίζονται λανθασμένα.  
- **Προσοχή:** Αν ξεχάσετε να ορίσετε το σωστό enum γλώσσας· η μηχανή θα επιστρέψει προεπιλογές Αγγλικών, παράγοντας ακατάλληλους τόνους.  
- **Σημείωση απόδοσης:** Η διόρθωση ορθογραφίας προσθέτει περίπου 15 % επιπλέον φόρτο. Αν επεξεργάζεστε μεγάλους όγκους, σκεφτείτε να την απενεργοποιήσετε για γλώσσες όπου το OCR είναι ήδη αξιόπιστο.  
- **Διαχείριση μνήμης:** Αποδεσμεύστε το αντικείμενο `AsposeOCR` μετά από μια μεγάλη παρτίδα (`engine.dispose()`) για να ελευθερώσετε τους εγγενείς πόρους.

## Αναμενόμενη έξοδος & επαλήθευση

Η εκτέλεση του πλήρους προγράμματος με ένα καθαρό γαλλικό τιμολόγιο παράγει:

```
Corrected text:
Facture Nº 12345
Date: 01/12/2025
Montant TTC: 1 250,00 €
```

Επαληθεύστε την έξοδο συγκρίνοντάς την με το αρχικό PDF ή τη σαρωμένη εικόνα. Αν οι διαφορές υπερβαίνουν μερικούς χαρακτήρες, επανεξετάστε τα βήματα προεπεξεργασίας της εικόνας.

## Συχνές ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω το Aspose OCR με δωρεάν δοκιμή σε παραγωγή;**  
Α: Η δωρεάν δοκιμή περιορίζεται στην αξιολόγηση· απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις.

**Ε: Υποστηρίζει το Aspose OCR γλώσσες πέρα από τα Γαλλικά;**  
Α: Ναι, υποστηρίζει πάνω από 30 γλώσσες, συμπεριλαμβανομένων των Αγγλικών, Γερμανικών, Ισπανικών, Κινέζικων και Αραβικών.

**Ε: Πώς επεξεργάζομαι ένα PDF πολλαπλών σελίδων;**  
Α: Μετατρέψτε κάθε σελίδα σε εικόνα χρησιμοποιώντας Aspose PDF ή PDFBox, και στη συνέχεια δώστε κάθε εικόνα στη ροή OCR σε βρόχο.

**Ε: Ποιοι τύποι εικόνας γίνονται αποδεκτοί;**  
Α: PNG, JPEG, BMP, TIFF και GIF υποστηρίζονται εξ ορισμού.

**Ε: Υπάρχει μέγιστο μέγεθος αρχείου;**  
Α: Η μηχανή μπορεί να επεξεργαστεί εικόνες έως 20 MB· μεγαλύτερα αρχεία πρέπει να χωριστούν ή να μειωθεί η ανάλυση πριν την επεξεργασία.

## Συμπέρασμα – τώρα ξέρετε **πώς να ενεργοποιήσετε το OCR** σε Java

Καλύψαμε όλα όσα χρειάζεστε για να απαντήσετε στην ερώτηση **πώς να ενεργοποιήσετε το OCR** για εφαρμογές Java: δημιουργήστε τη μηχανή, ενεργοποιήστε τη διόρθωση ορθογραφίας, εκτελέστε την αναγνώριση και αντιμετωπίστε τις ιδιαιτερότητες των πραγματικών τιμολογίων. Το παράδειγμα σας δείχνει πώς να **αναγνωρίζετε κείμενο από εικόνα**, **εξάγετε κείμενο από τιμολόγιο**, και να μετατρέψετε μια **java εικόνα σε κείμενο**—όλα σε ένα ενιαίο, αυτόνομο απόσπασμα.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `RecognitionLanguage.FRENCH` με άλλη γλώσσα, πειραματιστείτε με PDF πολλαπλών σελίδων, ή δώστε την έξοδο OCR σε έναν επόμενο αναλυτή που εξάγει πίνακες στοιχείων. Ο ουρανός είναι το όριο, και με το Aspose OCR έχετε μια σταθερή βάση.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τις δικές σας προσαρμογές; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

**Τελευταία ενημέρωση:** 2026-08-22  
**Δοκιμή με:** Aspose OCR for Java 24.9  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Αναγνώριση κειμένου εικόνας με Aspose OCR πλήρης οδηγός Java OCR](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Ανάγνωση κειμένου από εικόνα σε Java πλήρης οδηγός Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Πώς να ενεργοποιήσετε GPU για OCR σε Java Αναγνώριση κειμένου από εικόνα](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}