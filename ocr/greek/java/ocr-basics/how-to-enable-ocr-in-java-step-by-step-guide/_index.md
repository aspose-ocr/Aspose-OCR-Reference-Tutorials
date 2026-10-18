---
category: general
date: 2026-01-02
description: Πώς να ενεργοποιήσετε γρήγορα το OCR και να εξάγετε κείμενο από εικόνες
  τιμολογίων σε Java. Μάθετε να αναγνωρίζετε κείμενο από εικόνα και να μετατρέπετε
  μια εικόνα Java σε κείμενο με το Aspose.
draft: false
keywords:
- how to enable OCR
- recognize text from image
- extract text from invoice
- java image to text
- Aspose OCR
- spell correction
language: el
og_description: Πώς να ενεργοποιήσετε το OCR στη Java και να εξάγετε κείμενο από εικόνες
  τιμολογίων. Αυτός ο οδηγός σας δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα και
  να μετατρέψετε μια εικόνα Java σε κείμενο με το Aspose.
og_title: Πώς να ενεργοποιήσετε το OCR στη Java – Πλήρης οδηγός
tags:
- Java
- OCR
- Image Processing
title: Πώς να ενεργοποιήσετε το OCR στη Java – Οδηγός βήμα‑προς‑βήμα
url: /el/java/ocr-basics/how-to-enable-ocr-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενεργοποιήσετε το OCR σε Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε το OCR** σε ένα έργο Java χωρίς να τρελαίνεστε; Δεν είστε οι μόνοι. Οι προγραμματιστές που δημιουργούν pipelines επεξεργασίας τιμολογίων ή εφαρμογές σάρωσης συναντούν συνεχώς το ίδιο πρόβλημα: η μηχανή OCR λειτουργεί, αλλά το κείμενο είναι γεμάτο τυπογραφικά λάθη, ειδικά για μη‑αγγλικές γλώσσες.  

Σε αυτόν τον οδηγό θα περάσουμε από μια πρακτική λύση που όχι μόνο δείχνει **πώς να ενεργοποιήσετε το OCR**, αλλά επίσης επιδεικνύει **αναγνώριση κειμένου από εικόνα**, **εξαγωγή κειμένου από τιμολόγιο** PDF, και ακόμη τη μετατροπή **java image to text** με λίγες μόνο γραμμές κώδικα. Στο τέλος θα έχετε ένα εκτελέσιμο παράδειγμα, καλή κατανόηση του γιατί κάθε βήμα είναι σημαντικό, και μερικές επαγγελματικές συμβουλές για καθαρά αποτελέσματα OCR.

## Προαπαιτούμενα — Τι Θα Χρειαστεί

- Java 17 ή νεότερη (ο κώδικας μπορεί να συνταχθεί και με παλαιότερες εκδόσεις, αλλά η Java 17 είναι η ιδανική).  
- Άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  
- Ένα δείγμα εικόνας τιμολογίου (π.χ., `french_invoice.png`).  
- Το αγαπημένο σας IDE (IntelliJ, Eclipse, VS Code – όποιο προτιμάτε).  

Αυτό είναι όλο. Χωρίς βαριές βιβλιοθήκες, χωρίς εξωτερικές υπηρεσίες, μόνο καθαρή Java και Aspose.

![παράδειγμα ενεργοποίησης OCR](/images/ocr-example.png "Εικονογράφηση που δείχνει πώς να ενεργοποιήσετε το OCR σε Java")

## Βήμα 1: Ρύθμιση της Μηχανής Aspose OCR – Ο Πυρήνας του **How to Enable OCR**

Πριν μπούμε στην **recognize text from image**, χρειάζεται μια παρουσία της μηχανής OCR. Η Aspose OCR παρέχει ένα καθαρό, αντικειμενοστραφές API που αφαιρεί την πολυπλοκότητα της χαμηλού επιπέδου διαχείρισης εικόνας.

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

**Γιατί είναι σημαντικό:** Η δημιουργία του `AsposeOCR` φορτώνει τα εσωτερικά μοντέλα νευρωνικών δικτύων και προετοιμάζει τη μηχανή για τις επόμενες κλήσεις. Αν παραλείψετε αυτό το βήμα, θα πάθετε `NullPointerException` τη στιγμή που θα προσπαθήσετε να αναγνωρίσετε μια εικόνα.

## Βήμα 2: Ενεργοποίηση Διόρθωσης Ορθογραφίας – Κρίσιμο Στοιχείο του **How to Enable OCR** για Πραγματικό Κείμενο

Οι περισσότερες βιβλιοθήκες OCR επιστρέφουν ακατέργαστους χαρακτήρες, πράγμα που σημαίνει ότι τα γαλλικά τιμολόγια (ή οποιαδήποτε γλώσσα με τόνους) συχνά περιέχουν λανθασμένες λέξεις. Η Aspose μας επιτρέπει να ενεργοποιήσουμε τη διόρθωση ορθογραφίας με ένα ειδικό αντικείμενο επιλογών.

```java
        // Configure spell‑correction – this dramatically improves accuracy for invoices
        SpellCorrectionOptions spellOptions = new SpellCorrectionOptions();
        spellOptions.setEnable(true);                         // Turn the feature on
        spellOptions.setLanguage(RecognitionLanguage.FRENCH); // Choose the dictionary that matches your invoice
        ocrEngine.setSpellCorrectionOptions(spellOptions);
```

**Γιατί αυτό το βήμα είναι απαραίτητο:** Η ενεργοποίηση της διόρθωσης ορθογραφίας λέει στη μηχανή OCR να επεξεργαστεί το ακατέργαστο αποτέλεσμα χρησιμοποιώντας λεξικό συγκεκριμένης γλώσσας. Αν εξάγετε κείμενο από αγγλικό ή γερμανικό τιμολόγιο, απλώς αντικαταστήστε το `RecognitionLanguage.FRENCH` με το αντίστοιχο enum. Αυτό είναι το “μαγικό κουμπί” που πολλοί προγραμματιστές παραβλέπουν όταν ρωτούν **how to enable OCR** για μια συγκεκριμένη γλώσσα.

## Βήμα 3: Αναγνώριση της Εικόνας – Η Καρδιά του **Recognize Text from Image**

Τώρα που η μηχανή είναι έτοιμη, της δίνουμε τη διαδρομή προς το τιμολόγιό μας. Η μέθοδος `recognizeImage` κάνει το σκληρό έργο: φορτώνει το bitmap, τρέχει το νευρωνικό μοντέλο, εφαρμόζει τη διόρθωση ορθογραφίας και επιστρέφει μια καθαρή συμβολοσειρά.

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

Αν η έξοδος περιέχει ακόμη άσχετους χαρακτήρες, ελέγξτε την ποιότητα της εικόνας (υψηλή αντίθεση, 300 dpi είναι ιδανικό) και βεβαιωθείτε ότι το enum γλώσσας ταιριάζει με τη γλώσσα του τιμολογίου.

## Βήμα 4: Διαχείριση Ακραίων Περιπτώσεων – Όταν το **Extract Text from Invoice** Γίνεται Δύσκολο

Στην πραγματική ζωή τα τιμολόγια δεν είναι πάντα τέλειες σαρώσεις. Εδώ είναι μερικά σενάρια που μπορεί να συναντήσετε, μαζί με γρήγορες λύσεις:

| Κατάσταση | Προτεινόμενη Λύση |
|-----------|-------------------|
| Εικόνα χαμηλής ανάλυσης ( < 200 dpi ) | Ανεβάστε την ανάλυση της εικόνας με βιβλιοθήκη όπως `java‑image‑scaling` πριν τη δώσετε στην Aspose. |
| Μικτές γλώσσες (π.χ., French + English) | Εκτελέστε δύο ξεχωριστές διεργασίες OCR, μία ανά γλώσσα, και συγχωνεύστε τα αποτελέσματα. |
| Χειρόγραφα σημειώματα στο τιμολόγιο | Η Aspose OCR εστιάζει σε τυπωμένο κείμενο· για χειρόγραφα σκεφτείτε μια εξειδικευμένη υπηρεσία όπως Google Vision. |
| Μεγάλα PDF με πολλές σελίδες | Μετατρέψτε κάθε σελίδα σε εικόνα (χρησιμοποιώντας Aspose PDF ή PDFBox) και επαναλάβετε τα βήματα OCR. |

Αυτές οι συμβουλές κρατούν το pipeline **java image to text** ανθεκτικό, ακόμη και όταν το υλικό προέλευσης δεν είναι ιδανικό.

## Βήμα 5: Ενσωμάτωση της Ροής OCR σε Μεγαλύτερη Εφαρμογή

Αν χτίζετε έναν batch επεξεργαστή που διαβάζει δεκάδες τιμολόγια κάθε νύχτα, τυλίξτε τη λογική παραπάνω σε μια επαναχρησιμοποιήσιμη μέθοδο:

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

Τώρα μπορείτε να δημιουργήσετε ένα αντικείμενο `InvoiceOcrProcessor` μία φορά και να καλέσετε `extractText` για κάθε αρχείο — ιδανικό για εργασίες **extract text from invoice**.

## Pro Tips & Συνηθισμένα Πιθανά Σφάλματα

- **Pro tip:** Ενεργοποιήστε την καταγραφή (`engine.setLogLevel(LogLevel.DEBUG)`) κατά την ανάπτυξη για να δείτε γιατί ορισμένοι χαρακτήρες παρερμηνεύονται.  
- **Προσοχή:** Μην ξεχάσετε να ορίσετε το σωστό enum γλώσσας· η μηχανή θα επιστρέψει προεπιλογή Αγγλικών, παράγοντας ακατάλληλους τόνους.  
- **Σημείωση απόδοσης:** Η διόρθωση ορθογραφίας προσθέτει ~15 % επιβάρυνση. Αν επεξεργάζεστε μεγάλα ρεύματα, σκεφτείτε να την απενεργοποιήσετε για γλώσσες όπου το OCR είναι ήδη αξιόπιστο.  
- **Διαχείριση μνήμης:** Αποδεσμεύστε το αντικείμενο `AsposeOCR` μετά από μεγάλο batch (`engine.dispose()`) για να ελευθερώσετε εγγενείς πόρους.

## Αναμενόμενη Έξοδος & Επαλήθευση

Εκτελώντας το πλήρες πρόγραμμα με ένα καθαρό γαλλικό τιμολόγιο λαμβάνετε:

```
Corrected text:
Facture Nº 12345
Date: 01/12/2025
Montant TTC: 1 250,00 €
```

Επαληθεύστε την έξοδο συγκρίνοντάς την με το αρχικό PDF ή τη σαρωμένη εικόνα. Αν οι αποκλίσεις υπερβαίνουν μερικούς χαρακτήρες, επανεξετάστε τα βήματα προεπεξεργασίας εικόνας.

## Συμπέρασμα – Τώρα Ξέρετε **How to Enable OCR** σε Java

Καλύψαμε όλα όσα χρειάζεστε για να απαντήσετε στην ερώτηση **how to enable OCR** για εφαρμογές Java: δημιουργία της μηχανής, ενεργοποίηση διόρθωσης ορθογραφίας, εκτέλεση της αναγνώρισης και αντιμετώπιση των ιδιαιτεροτήτων των πραγματικών τιμολογίων. Το παράδειγμα δείχνει πώς να **recognize text from image**, **extract text from invoice**, και να μετατρέψετε μια **java image to text** — όλα σε ένα αυτόνομο snippet.

Τι ακολουθεί; Δοκιμάστε να αλλάξετε το `RecognitionLanguage.FRENCH` με άλλη γλώσσα, πειραματιστείτε με PDF πολλαπλών σελίδων, ή δώστε το αποτέλεσμα OCR σε έναν επόμενο parser που εξάγει πίνακες γραμμών. Οι δυνατότητες είναι απεριόριστες, και με την Aspose OCR έχετε μια σταθερή βάση.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τις δικές σας βελτιώσεις; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}