---
category: general
date: 2026-06-16
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα χρησιμοποιώντας το Aspose
  OCR Java και ανακαλύψτε πώς να βελτιώσετε την ακρίβεια του OCR με ένα προσαρμοσμένο
  λεξικό. Επεξεργαστείτε εικόνα με OCR σε λίγα λεπτά.
draft: false
keywords:
- recognize text from image
- how to improve OCR accuracy
- process image with OCR
- Aspose OCR Java
- custom dictionary OCR
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR Java.
  Μάθετε πώς να βελτιώσετε την ακρίβεια του OCR και να επεξεργάζεστε την εικόνα με
  OCR αποδοτικά.
og_title: Αναγνώριση κειμένου από εικόνα με Aspose OCR Java – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to recognize text from image using Aspose OCR Java and discover
    how to improve OCR accuracy with a custom dictionary. Process image with OCR in
    minutes.
  headline: recognize text from image with Aspose OCR Java – Complete Guide
  type: TechArticle
- description: Learn how to recognize text from image using Aspose OCR Java and discover
    how to improve OCR accuracy with a custom dictionary. Process image with OCR in
    minutes.
  name: recognize text from image with Aspose OCR Java – Complete Guide
  steps:
  - name: '**Pre‑process the image** – convert to grayscale, increase contrast, or
      binarize.'
    text: '**Pre‑process the image** – convert to grayscale, increase contrast, or
      binarize.'
  - name: '**Resize** – larger images give the engine more pixels per character.'
    text: '**Resize** – larger images give the engine more pixels per character.'
  - name: '**Set correct DPI** – Aspose OCR assumes 300 dpi for optimal results.'
    text: '**Set correct DPI** – Aspose OCR assumes 300 dpi for optimal results.'
  - name: '**Choose the right language** – mis‑matched language settings reduce confidence
      scores.'
    text: '**Choose the right language** – mis‑matched language settings reduce confidence
      scores.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Text Recognition
title: Αναγνώριση κειμένου από εικόνα με Aspose OCR Java – Πλήρης Οδηγός
url: /el/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose OCR Java – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** αλλά τα αποτελέσματα έδειχναν σαν κρυπτογραφικό χάος; Δεν είστε ο μόνος. Σε πολλά έργα—είτε πρόκειται για ψηφιοποίηση χειρόγραφων φορμών είτε για εξαγωγή δεδομένων από αποδείξεις—η λήψη καθαρού κειμένου είναι το πρώτο βήμα προς οποιαδήποτε αυτοματοποίηση.  

Σε αυτό το σεμινάριο θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει ακριβώς **πώς να βελτιώσετε την ακρίβεια του OCR** ενεργοποιώντας τον ενσωματωμένο ορθογραφικό έλεγχο και, αν θέλετε, προσθέτοντας ένα προσαρμοσμένο λεξικό. Στο τέλος θα μπορείτε να **επεξεργαστείτε εικόνα με OCR** με λίγες γραμμές κώδικα Java.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη βιβλιοθήκη Aspose OCR σε έργο Maven ή Gradle.  
- Τα ακριβή βήματα για **αναγνώριση κειμένου από εικόνα** χρησιμοποιώντας το `OcrEngine`.  
- Γιατί η ενεργοποίηση του ορθογραφικού ελέγχου είναι ο πιο γρήγορος τρόπος για **βελτίωση της ακρίβειας του OCR**.  
- Πότε και πώς να **επεξεργαστείτε εικόνα με OCR** χρησιμοποιώντας προσαρμοσμένο λεξικό για ειδικούς όρους.  
- Κοινά προβλήματα, συμβουλές απόδοσης και πώς πρέπει να φαίνεται η έξοδος.

> **Προαπαιτούμενα** – Java 8 ή νεότερη, ένα βασικό περιβάλλον Maven/Gradle, και μια εικόνα (JPEG, PNG, BMP) που θέλετε να σαρώσετε. Δεν απαιτείται προηγούμενη εμπειρία OCR.

![αναγνώριση κειμένου από εικόνα παράδειγμα](/images/ocr-example.png "Παράδειγμα αναγνώρισης κειμένου από εικόνα χρησιμοποιώντας Aspose OCR")

## Αναγνώριση Κειμένου από Εικόνα – Πλήρες Παράδειγμα Java

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα. Αντιγράψτε το σε ένα αρχείο με όνομα `SpellCheckExample.java`, προσαρμόστε τις διαδρομές, και είστε έτοιμοι.

```java
import com.aspose.ocr.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the image to be processed
        OcrEngine engine = new OcrEngine();
        // ImageStream.fromFile reads the image from disk – replace with your own file path
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/handwritten.jpg"));

        // Step 2: Enable the built‑in spell checker to improve recognition accuracy
        // This tiny flag can dramatically boost the quality of the output.
        engine.getRecognitionSettings().setUseSpellChecker(true);

        // Step 3: (Optional) Add a custom dictionary with domain‑specific words
        // Useful when you know the text will contain jargon, product codes, etc.
        engine.getRecognitionSettings()
              .getSpellCheckerSettings()
              .addCustomDictionary("YOUR_DIRECTORY/my_custom_words.txt");

        // Step 4: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        // Step 5: Print the extracted text to the console
        System.out.println("=== OCR Output ===");
        System.out.println(result.getText());
    }
}
```

**Αναμενόμενη έξοδος κονσόλας** (το ακριβές κείμενο εξαρτάται από την εικόνα σας, φυσικά):

```
=== OCR Output ===
Dear John,

Please find attached the invoice #INV-2023-045 for $1,250.00.
Thank you for your business.

Best,
Acme Corp.
```

Αν ο ορθογραφικός έλεγχος είναι απενεργοποιημένος, θα παρατηρήσετε περισσότερες λανθασμένες λέξεις, ειδικά σε χειρόγραφες δειγματοληψίες. Αυτό είναι το βασικό στοιχείο του **πώς να βελτιώσετε την ακρίβεια του OCR**.

## Ρύθμιση Aspose OCR στο Έργο Java Σας

Πριν τρέξει ο κώδικας, χρειάζεστε το αρχείο JAR του Aspose OCR. Ο πιο εύκολος τρόπος είναι μέσω Maven Central:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Ή με Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Μετά την προσθήκη της εξάρτησης, ανανεώστε το έργο σας ώστε οι κλάσεις να είναι διαθέσιμες. Δεν απαιτούνται πρόσθετες εγγενείς βιβλιοθήκες—το Aspose OCR είναι καθαρά Java.

## Ενεργοποίηση Ορθογραφικού Ελέγχου για Βελτίωση της Ακρίβειας του OCR

Γιατί μια απλή λογική σημαία κάνει τόσο μεγάλη διαφορά; Οι μηχανές OCR συχνά ερμηνεύουν λανθασμένα παρόμοιους χαρακτήρες (π.χ. “l” vs. “1” ή “O” vs. “0”). Ο ενσωματωμένος ορθογραφικός έλεγχος εκτελεί ένα γλωσσικό μοντέλο πάνω στην ακατέργαστη έξοδο και διορθώνει πιθανά λάθη.  

Στην πράξη, η εναλλαγή του `setUseSpellChecker(true)` μπορεί να αυξήσει την ακρίβεια σε επίπεδο χαρακτήρων από το υψηλό 70 % στο μεσαίο 90 % σε καθαρό τυπωμένο κείμενο, και εξακολουθεί να βοηθά σε ακατάστατες χειρόγραφες σημειώσεις.  

**Συμβουλή:** Αν επεξεργάζεστε πολυγλωσσικά έγγραφα, ορίστε τη γλώσσα ρητά:

```java
engine.getRecognitionSettings().setLanguage(Language.English);
```

Αυτό ωθεί περαιτέρω τον ορθογραφικό έλεγχο προς το σωστό λεξικό.

## Προσθήκη Προσαρμοσμένου Λεξικού για Λέξεις Ειδικού Τομέα

Μερικές φορές το προεπιλεγμένο λεξικό δεν γνωρίζει τους κωδικούς προϊόντων, ιατρικούς όρους ή συντομογραφίες σας. Εκεί έρχεται στο προσκήνιο το προαιρετικό προσαρμοσμένο λεξικό. Δημιουργήστε ένα αρχείο απλού κειμένου (`my_custom_words.txt`) με μία λέξη ανά γραμμή:

```
AcmeCorp
INV-2023-045
USD
```

Στη συνέχεια καλέστε το `addCustomDictionary(...)` όπως φαίνεται στο παράδειγμα. Η μηχανή OCR θα θεωρήσει αυτές τις καταχωρήσεις έγκυρες, αποτρέποντας την επισήμανσή τους ως σφάλματα.  

**Πότε να χρησιμοποιήσετε:**  
- Σάρωση τιμολογίων με μοναδικούς αριθμούς τιμολογίων.  
- Αναγνώριση επιστημονικών εργασιών με τεχνική ορολογία.  
- Επεξεργασία νομικών συμβάσεων που περιέχουν συγκεκριμένους αναγνωριστικούς όρους.

## Εκτέλεση του OCR και Λήψη Αποτελεσμάτων

Μόλις ρυθμιστεί η μηχανή, η μέθοδος `recognize()` κάνει το σκληρό έργο. Επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει:

- `getText()` – η απλή συμβολοσειρά που εκτυπώσατε νωρίτερα.  
- `getWords()` – μια συλλογή από μεμονωμένα αντικείμενα λέξεων, το καθένα με το δικό του σκορ εμπιστοσύνης.  
- `getPages()` – χρήσιμο αν χρειάζεστε μεταδεδομένα ανά σελίδα.

Μπορείτε να επαναλάβετε το `result.getWords()` για να φιλτράρετε λέξεις χαμηλής εμπιστοσύνης:

```java
for (OcrWord word : result.getWords()) {
    if (word.getConfidence() < 0.70) {
        System.out.println("Low confidence word: " + word.getText());
    }
}
```

Αυτό το μικρό απόσπασμα είναι ένας πρακτικός τρόπος για **επεξεργασία εικόνας με OCR** ενώ διατηρείτε την ποιότητα υπό έλεγχο.

## Συχνά Προβλήματα και Συμβουλές για Καλύτερα Αποτελέσματα

| Πρόβλημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|----------|----------------|--------------|
| Θολές ή χαμηλής ανάλυσης εικόνες | Το OCR χρειάζεται σαφείς άκρες χαρακτήρων | Αυξήστε την ανάλυση τουλάχιστον σε 300 dpi· εφαρμόστε φίλτρα ενίσχυσης |
| Καμπυλωμένες σελίδες | Οι γραμμές κειμένου δεν είναι οριζόντιες | Χρησιμοποιήστε `engine.getRecognitionSettings().setAutoSkewCorrection(true)` |
| Μη λατινικά αλφάβητα | Η προεπιλεγμένη γλώσσα είναι τα Αγγλικά | Ορίστε το κατάλληλο enum `Language` (π.χ., `Language.French`) |
| Το προσαρμοσμένο λεξικό δεν φορτώνεται | Λάθος διαδρομή αρχείου ή κωδικοποίηση | Επαληθεύστε τη διαδρομή, χρησιμοποιήστε UTF‑8 και βεβαιωθείτε ότι υπάρχει μία λέξη ανά γραμμή |

**Pro tip:** Αποθηκεύστε στην κρυφή μνήμη το στιγμιότυπο `OcrEngine` αν επεξεργάζεστε πολλές εικόνες σε παρτίδα. Η δημιουργία νέας μηχανής για κάθε εικόνα προσθέτει περιττό φόρτο.

## Πώς να Βελτιώσετε την Ακρίβεια του OCR – Σύνοψη

Έχουμε ήδη δει το μεγαλύτερο πλεονέκτημα: η ενεργοποίηση του ενσωματωμένου ορθογραφικού ελέγχου. Αλλά υπάρχουν μερικά ακόμη κόλπα:

1. **Προεπεξεργασία της εικόνας** – μετατροπή σε αποχρώσεις του γκρι, αύξηση αντίθεσης ή δυαδικοποίηση.  
2. **Αλλαγή μεγέθους** – μεγαλύτερες εικόνες δίνουν στη μηχανή περισσότερα pixel ανά χαρακτήρα.  
3. **Ορισμός σωστού DPI** – το Aspose OCR υποθέτει 300 dpi για βέλτιστα αποτελέσματα.  
4. **Επιλογή της σωστής γλώσσας** – οι λανθασμένες ρυθμίσεις γλώσσας μειώνουν τα σκορ εμπιστοσύνης.  

Συνδυάστε αυτά με τον ορθογραφικό έλεγχο και ένα προσαρμοσμένο λεξικό, και θα αναγνωρίζετε σταθερά **κείμενο από εικόνα** με υψηλή πιστότητα.

## Πλήρη Δομή Δείγματος Έργου Από‑Αρχή‑Στο‑Τέλος

```
my-ocr-project/
├─ src/
│  └─ main/
│     └─ java/
│        └─ SpellCheckExample.java
├─ resources/
│  ├─ handwritten.jpg
│  └─ my_custom_words.txt
├─ pom.xml   (or build.gradle)
└─ README.md
```

Η εκτέλεση του `mvn compile exec:java -Dexec.mainClass=SpellCheckExample` (ή το ισοδύναμο Gradle) θα εκτυπώσει την έξοδο OCR στην κονσόλα.

## Συμπέρασμα

Τώρα έχετε μια στιβαρή, έτοιμη για παραγωγή συνταγή για **αναγνώριση κειμένου από εικόνα** χρησιμοποιώντας Aspose OCR Java. Με την εναλλαγή του ορθογραφικού ελέγχου μαθαίνετε αμέσως **πώς να βελτιώσετε την ακρίβεια του OCR**, και φορτώνοντας ένα προσαρμοσμένο λεξικό αποκτάτε λεπτομερή έλεγχο όταν **επεξεργάζεστε εικόνα με OCR** για εξειδικευμένους τομείς.  

Τι ακολουθεί; Δοκιμάστε να επεξεργαστείτε ένα πολυσελίδες PDF, πειραματιστείτε με διαφορετικές γλώσσες, ή συνδέστε την έξοδο με μια επόμενη διαδικασία NLP. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά.  

Έχετε ερωτήσεις ή ένα ενδιαφέρον σενάριο χρήσης να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω, και καλή κωδικοποίηση!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να κάνετε OCR κειμένου εικόνας με γλώσσα χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Εξαγωγή κειμένου από εικόνα Java με Aspose.OCR λειτουργία ανίχνευσης περιοχών](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Μετατροπή εικόνας σε κείμενο σε Java χρησιμοποιώντας Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}