---
category: general
date: 2026-09-18
description: Μάθετε image preprocessing για OCR με Aspose σε Java, συμπεριλαμβανομένου
  του πώς να reduce image noise, boost contrast, και correct skew. Ακολουθήστε αυτό
  το Aspose OCR Java tutorial για να extract text image efficiently.
draft: false
keywords:
- image preprocessing for OCR
- extract text image java
- aspose OCR Java tutorial
lastmod: 2026-09-18
og_description: Μάθετε image preprocessing για OCR με Aspose σε Java, συμπεριλαμβανομένου
  του πώς να reduce image noise, boost contrast, και correct skew. Ακολουθήστε αυτό
  το Aspose OCR Java tutorial για να extract text image efficiently.
og_image_alt: Guide showing image preprocessing for OCR using Aspose OCR Java
og_title: Image preprocessing για OCR με Aspose σε Java – οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn image preprocessing for OCR with Aspose in Java, including how
    to reduce image noise, boost contrast, and correct skew. Follow this Aspose OCR
    Java tutorial to extract text image efficiently.
  headline: Image preprocessing for OCR with Aspose in Java – guide
  type: TechArticle
- questions:
  - answer: A radius of 3 works for most scanned documents. Increasing the radius
      beyond 5 can start to blur fine details like punctuation, which may hurt accuracy.
      Test a few values on a representative sample to find the sweet spot.
    question: How much noise reduction is too much?
  - answer: Yes, but order matters. The recommended sequence is **deskew → noise reduction
      → contrast boost**. Applying contrast boost before noise removal can amplify
      speckles, leading to poorer OCR results.
    question: Can I change the order of filters?
  - answer: Absolutely. Aspose OCR can extract each page as an image, run the same
      pipeline on every page, and concatenate the results. Loop over the pages, apply
      the pipeline, and combine the strings.
    question: Does this work on multi‑page PDFs?
  - answer: The built‑in OCR engine focuses on printed text. For handwriting you’ll
      need a specialized model such as Aspose OCR Handwriting or a cloud‑based AI
      service. Pre‑processing still helps, but recognition accuracy will vary.
    question: What if my text is handwritten?
  - answer: Yes. A valid Aspose OCR license removes evaluation limits, enables full‑speed
      processing, and grants access to premium filters. A free trial is available
      for testing.
    question: Is a license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Image processing
- Aspose
title: Image preprocessing για OCR με Aspose σε Java – οδηγός
url: /el/java/advanced-ocr-techniques/reduce-image-noise-in-ocr-with-aspose-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία εικόνας για OCR με Aspose σε Java – οδηγός

Αν έχετε προσπαθήσει ποτέ να εξάγετε κείμενο από μια θορυβώδη σάρωση, ξέρετε πόσο γρήγορα μπορεί να μειωθεί η ακρίβεια του OCR. **Image preprocessing for OCR** είναι το σύνολο των βημάτων που καθαρίζουν μια εικόνα πριν τρέξει η μηχανή αναγνώρισης – αφαιρώντας σπασμένα σημεία, ευθυγραμμίζοντας κλίστές σελίδες και ενισχύοντας την αντίθεση. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα Java που δείχνει ακριβώς πώς να εφαρμόσετε αυτά τα φίλτρα με Aspose OCR, γιατί κάθε φίλτρο είναι σημαντικό και τι αποτελέσματα μπορείτε να περιμένετε.

> **Pro tip:** Για αποδείξεις ή παλιές έντυπες φόρμες, η ταυτόχρονη εφαρμογή deskew + contrast boost συχνά προσφέρει τη μεγαλύτερη άνοδο στην ακρίβεια.

## Γρήγορες απαντήσεις
- **What is the first step?** Δημιουργήστε ένα στιγμιότυπο `OcrEngine` – είναι το κεντρικό αντικείμενο που εκτελεί τη γραμμή αναγνώρισης.  
- **Which filter removes speckles?** `NoiseReductionFilter` με ακτίνα median 3 λειτουργεί για τις περισσότερες σαρωμένες εγγραφές.  
- **How do I straighten a rotated page?** Χρησιμοποιήστε `DeskewFilter`; ανιχνεύει αυτόματα τη γωνία και περιστρέφει την εικόνα.  
- **Can I boost contrast without losing detail?** Ορίστε τον παράγοντα `ContrastBoostFilter` σε 1.2 (20 % ενίσχυση) για καλή ισορροπία.  
- **Do I need a license for production?** Ναι – μια έγκυρη άδεια Aspose OCR αφαιρεί τα όρια αξιολόγησης και ενεργοποιεί πλήρη ταχύτητα επεξεργασίας.

## Τι είναι η προεπεξεργασία εικόνας για OCR;
**Image preprocessing for OCR** είναι η προετοιμασία bitmap εικόνων για τη βελτίωση των αποτελεσμάτων οπτικής αναγνώρισης χαρακτήρων. Συνήθως περιλαμβάνει αφαίρεση θορύβου, ενίσχυση αντίθεσης και γεωμετρικές διορθώσεις όπως το deskewing. Με την παροχή μιας καθαρότερης εικόνας στη μηχανή, μειώνετε τις λανθασμένες αναγνώσεις και αυξάνετε τη συνολική απόδοση.

## Γιατί να χρησιμοποιήσετε το tutorial Aspose OCR Java για αυτήν την εργασία;
Aspose OCR υποστηρίζει **50+ μορφές εισόδου** (PNG, JPEG, TIFF, BMP κ.λπ.) και μπορεί να επεξεργαστεί έγγραφα πολλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, επιτυγχάνοντας έως **2× ταχύτερη** αναγνώριση σε σύγκριση με τις ακατέργαστες κλήσεις OCR. Η βιβλιοθήκη επίσης παρέχει μια εύχρηστη pipeline προεπεξεργασίας, επιτρέποντάς σας να αλυσίδετε φίλτρα σε μια ενιαία, αναγνώσιμη δήλωση.

## Τι θα χρειαστείτε

- **Aspose OCR for Java** (τελευταία έκδοση, π.χ., 23.10). Προσθέστε την εξάρτηση Maven ή κατεβάστε το JAR από τον ιστότοπο Aspose.  
- Java 8 ή νεότερη. Το παράδειγμα χρησιμοποιεί σύνταξη φιλική προς lambda αλλά τρέχει σε οποιοδήποτε runtime Java 8+.  
- Μια δείγμα εικόνας (`input.png`) που παρουσιάζει θόρυβο, χαμηλή αντίθεση ή ελαφρά περιστροφή.  
- Ένα IDE ή έναν απλό επεξεργαστή κειμένου· Maven/Gradle είναι προαιρετικά αλλά απλοποιούν τη διαχείριση εξαρτήσεων.

## Τι είναι η κλάση OcrEngine;
`OcrEngine` είναι το κεντρικό αντικείμενο του Aspose OCR που περιλαμβάνει τον αλγόριθμο αναγνώρισης και διαχειρίζεται τη pipeline προεπεξεργασίας. Αποθηκεύει ρυθμίσεις όπως γλώσσα, τρόπο τμηματοποίησης σελίδας και συνδεδεμένα φίλτρα. Όλες οι ρυθμίσεις εφαρμόζονται σε αυτήν την παρουσία πριν καλέσετε τη μέθοδο `recognize` σε μια εικόνα.

## Πώς να δημιουργήσετε το στιγμιότυπο της μηχανής OCR  

Για να δημιουργήσετε τη μηχανή OCR, δημιουργήστε μια παρουσία της κλάσης `OcrEngine` με τον προεπιλεγμένο κατασκευαστή της. Αυτό το αντικείμενο κρατά όλες τις ρυθμίσεις, συμπεριλαμβανομένου οποιουδήποτε αλυσίδας φίλτρων προσθέσετε αργότερα, και προετοιμάζει τη εσωτερική μηχανή αναγνώρισης για επεξεργασία εικόνων. Μόλις δημιουργηθεί, μπορείτε αμέσως να αρχίσετε να προσθέτετε βήματα προεπεξεργασίας.

```java
import com.aspose.ocr.*;

public class FilterChainExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this object holds configuration and state
        OcrEngine ocrEngine = new OcrEngine();
```

> **Why?** Η μηχανή περιλαμβάνει τον αλγόριθμο αναγνώρισης και σας επιτρέπει να συνδέσετε μια pipeline προεπεξεργασίας. Χωρίς αυτήν, θα πρέπει να καλέσετε χειροκίνητα βιβλιοθήκες εικόνας χαμηλού επιπέδου.

## Τι είναι η κλάση DeskewFilter;
Η `DeskewFilter` εξετάζει τον προσανατολισμό των γραμμών κειμένου στην εικόνα και υπολογίζει τη γωνία που απαιτείται για να τις κάνει οριζόντιες. Στη συνέχεια περιστρέφει το bitmap αναλόγως, διασφαλίζοντας ότι η μηχανή OCR λαμβάνει μια σωστά ευθυγραμμισμένη εικόνα, κάτι που μειώνει σημαντικά τα σφάλματα αναγνώρισης που προκαλούνται από κεκλιμένο κείμενο.

## Τι είναι η κλάση NoiseReductionFilter;
`NoiseReductionFilter` υλοποιεί ένα median φίλτρο που αντικαθιστά κάθε pixel με τη μεσαία τιμή της γύρω γειτονιάς του. Καθορίζοντας μια ακτίνα (συνήθως 3), αφαιρεί απομονωμένα σπασμένα σημεία και κόκκο χωρίς να θολώνει μεγαλύτερες δομές, βοηθώντας τη μηχανή OCR να εστιάσει στους πραγματικούς χαρακτήρες αντί στον θόρυβο.

## Τι είναι η κλάση ContrastBoostFilter;
`ContrastBoostFilter` ενισχύει τη διαφορά μεταξύ φωτεινών και σκοτεινών περιοχών πολλαπλασιάζοντας τις εντάσεις των pixel με έναν ρυθμιζόμενο παράγοντα. Μια τυπική ενίσχυση 1.2 (αύξηση 20 %) κάνει το κείμενο να ξεχωρίζει από το φόντο, βελτιώνοντας την ανίχνευση άκρων και τελικά αυξάνοντας την ακρίβεια του OCR σε σάρωσες χαμηλής αντίθεσης.

## Βήμα 2: δημιουργία pipeline προεπεξεργασίας  

Εδώ **μειώνουμε τον θόρυβο της εικόνας** και **ενισχύουμε την αντίθεση**. Η pipeline είναι μια αλυσίδα φίλτρων που εκτελείται με τη σειρά.

```java
        // Construct a pipeline that will clean up the image before OCR
        PreProcessingPipeline preProcessingPipeline = new PreProcessingPipeline()
                .add(new DeskewFilter())                     // correct image skew
                .add(new NoiseReductionFilter(3))            // add noise reduction (kernel radius = 3)
                .add(new ContrastBoostFilter(1.2f));         // boost image contrast (20% increase)
```

### Γιατί αυτά τα φίλτρα;
| Φίλτρο | Τι κάνει | Γιατί βοηθά |
|--------|----------|--------------|
| **DeskewFilter** | Ανιχνεύει και περιστρέφει την εικόνα ώστε οι γραμμές κειμένου να είναι οριζόντιες. | Οι μηχανές OCR υποθέτουν σχεδόν οριζόντιο κείμενο· μια κεκλιμένη γραμμή μπορεί να προκαλέσει λανθασμένη αναγνώριση. |
| **NoiseReductionFilter** | Εφαρμόζει median φίλτρο με ρυθμιζόμενη ακτίνα (εδώ `3`). | Αφαιρεί σπασμένα σημεία και κόκκο που αλλιώς μοιάζουν με αχρείαστους χαρακτήρες. |
| **ContrastBoostFilter** | Πολλαπλασιάζει την ένταση των pixel με έναν παράγοντα (`1.2f` = 20 % ενίσχυση). | Ενισχύει τη διαφορά μεταξύ του κειμένου και του φόντου, καθιστώντας τις άκρες πιο σαφείς. |

> **Common variation:** Αν οι εικόνες σας είναι πολύ σπογγώδεις, αυξήστε την ακτίνα πυρήνα σε `5` ή `7`. Μεγαλύτερες ακτίνες αφαιρούν περισσότερο θόρυβο αλλά μπορεί επίσης να θολώσουν λεπτομερείς λεπτομέρειες, οπότε δοκιμάστε σε αντιπροσωπευτικό δείγμα.

## Βήμα 3: προσθήκη του pipeline στη μηχανή  

Τώρα λέμε στη μηχανή OCR να χρησιμοποιήσει την pipeline που μόλις δημιουργήσαμε.

```java
        // Plug the pipeline into the OCR engine’s configuration
        ocrEngine.getConfiguration().setPreProcessingPipeline(preProcessingPipeline);
```

> **Edge case:** Η παράλειψη αυτού του βήματος αφήνει τη μηχανή με τις προεπιλογές της (συχνά χωρίς προεπεξεργασία), κάτι που σημαίνει ότι πιθανότατα θα δείτε τα ίδια σφάλματα που προκαλούνται από θόρυβο.

## Βήμα 4: εκτέλεση OCR στην εικόνα σας  

Με όλα έτοιμα, ας αναγνωρίσουμε το κείμενο.

```java
        // Run OCR – replace the path with your own image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/input.png");
```

> **What if the image is colored?** Το Aspose OCR μετατρέπει αυτόματα τις έγχρωμες εικόνες σε γκρι κλίμακα πριν εφαρμόσει τα φίλτρα, αλλά μπορείτε να μετατρέψετε χειροκίνητα πρώτα αν χρειάζεστε συγκεκριμένο κανάλι.

## Βήμα 5: έξοδος του αναγνωρισμένου κειμένου  

Τέλος, εκτυπώστε τη εξαγόμενη συμβολοσειρά. Σε μια πραγματική εφαρμογή ίσως τη γράψετε σε αρχείο ή βάση δεδομένων.

```java
        // Show the result in the console
        System.out.println("=== OCR Output ===");
        System.out.println(recognitionResult.getText());
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
=== OCR Output ===
Invoice #12345
Date: 02/08/2026
Total: $1,234.56
Thank you for your business!
```

Αν η αρχική εικόνα ήταν θορυβώδης, θα παρατηρήσετε πολύ λιγότερους ακατάστατους χαρακτήρες σε σύγκριση με μια εκτέλεση χωρίς την pipeline προεπεξεργασίας.

## Οπτική σύνοψη  

![Δειγματική είσοδος εικόνας που δείχνει θόρυβο πριν την επεξεργασία – παράδειγμα μείωσης θορύβου εικόνας](https://example.com/images/noisy-scan.png "μείωση θορύβου εικόνας")

[Δειγματική είσοδος εικόνας που δείχνει θόρυβο πριν την επεξεργασία – παράδειγμα μείωσης θορύβου εικόνας](https://example.com/images/noisy-scan.png "μείωση θορύβου εικόνας")

Το παραπάνω alt κείμενο περιέχει τη **κύρια λέξη-κλειδί**, ικανοποιώντας το SEO ενώ περιγράφει επίσης την εικόνα για προσβασιμότητα.

## Συχνές ερωτήσεις (FAQs)

**Q: Πόση μείωση θορύβου είναι πολύ;**  
A: Μια ακτίνα 3 λειτουργεί για τις περισσότερες σαρωμένες εγγραφές. Η αύξηση της ακτίνας πάνω από 5 μπορεί να ξεθώρισει λεπτομέρειες όπως σημεία στίξης, κάτι που μπορεί να βλάψει την ακρίβεια. Δοκιμάστε μερικές τιμές σε αντιπροσωπευτικό δείγμα για να βρείτε το ιδανικό σημείο.

**Q: Μπορώ να αλλάξω τη σειρά των φίλτρων;**  
A: Ναι, αλλά η σειρά έχει σημασία. Η συνιστώμενη ακολουθία είναι **deskew → noise reduction → contrast boost**. Η εφαρμογή contrast boost πριν από την αφαίρεση θορύβου μπορεί να ενισχύσει τα σπασμένα σημεία, οδηγώντας σε χειρότερα αποτελέσματα OCR.

**Q: Λειτουργεί αυτό σε πολυ‑σελίδες PDF;**  
A: Απόλυτα. Το Aspose OCR μπορεί να εξάγει κάθε σελίδα ως εικόνα, να τρέξει την ίδια pipeline σε κάθε σελίδα και να συνενώσει τα αποτελέσματα. Επανάληψη πάνω στις σελίδες, εφαρμογή της pipeline και συνένωση των συμβολοσειρών.

**Q: Τι γίνεται αν το κείμενό μου είναι χειρόγραφο;**  
A: Η ενσωματωμένη μηχανή OCR εστιάζει σε τυπωμένο κείμενο. Για χειρόγραφο θα χρειαστείτε ένα εξειδικευμένο μοντέλο όπως Aspose OCR Handwriting ή μια υπηρεσία AI στο cloud. Η προεπεξεργασία βοηθά ακόμη, αλλά η ακρίβεια αναγνώρισης θα διαφέρει.

**Q: Απαιτείται άδεια για παραγωγική χρήση;**  
A: Ναι. Μια έγκυρη άδεια Aspose OCR αφαιρεί τα όρια αξιολόγησης, ενεργοποιεί πλήρη ταχύτητα επεξεργασίας και παρέχει πρόσβαση σε premium φίλτρα. Διατίθεται δωρεάν δοκιμή για δοκιμές.

## Επόμενα βήματα & σχετικά θέματα  

- **Extract text image java** από PDFs ή πολυ‑σελίδες TIFF χρησιμοποιώντας Aspose PDF, έπειτα τροφοδοτήστε τις εικόνες στην ίδια pipeline.  
- Πειραματιστείτε με υψηλότερες τιμές **contrast boost** (`1.5f`, `2.0f`) για φωτογραφίες χαμηλού φωτισμού.  
- Συνδυάστε τα φίλτρα Aspose με προσαρμοσμένες λειτουργίες OpenCV για σπάνιες μορφές θορύβου (π.χ., αλάτι‑και‑πέπερ).  
- Εξερευνήστε **correct image skew** όρια για ακραίες περιστροφές (> 15°) ρυθμίζοντας τις παραμέτρους ανίχνευσης deskew.  

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στην κεντρική ιδέα της **προεπεξεργασίας εικόνας για OCR**, βελτιώνοντας σταθερά την ακρίβεια σε ένα ευρύ φάσμα έργων επεξεργασίας εγγράφων.

## Συμπέρασμα  

Καλύψαμε μια πλήρη, end‑to‑end λύση που **μειώνει τον θόρυβο της εικόνας**, **ενισχύει την αντίθεση**, **προσθέτει μείωση θορύβου**, και **διορθώνει την κλίση** πριν την εξαγωγή κειμένου από μια εικόνα χρησιμοποιώντας Aspose OCR για Java. Ακολουθώντας τα πέντε βήματα παραπάνω, μπορείτε να μετατρέψετε μια σπόρικη, κεκλιμένη σάρωση σε μια καθαρή, μηχανικά αναγνώσιμη συμβολοσειρά με λίγες μόνο γραμμές κώδικα. Δοκιμάστε την pipeline με τις δικές σας εικόνες, προσαρμόστε τις παραμέτρους των φίλτρων και παρακολουθήστε το ποσοστό επιτυχίας του OCR να ανεβαίνει.

---

**Τελευταία ενημέρωση:** 2026-09-18  
**Δοκιμή με:** Aspose OCR for Java 23.10  
**Συγγραφέας:** Aspose

## Σχετικά Tutorials

- [Recognize Text Image With Aspose Ocr Full Java Ocr Tutorial](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Reduce Image Noise In Ocr With Aspose Full Java Guide](/ocr/java/advanced-ocr-techniques/reduce-image-noise-in-ocr-with-aspose-full-java-guide/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}