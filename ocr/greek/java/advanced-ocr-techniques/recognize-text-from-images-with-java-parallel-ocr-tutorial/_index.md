---
category: general
date: 2026-01-12
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνες και να εξάγετε κείμενο
  από αρχεία PNG χρησιμοποιώντας το Aspose OCR σε Java. Η παράλληλη επεξεργασία το
  κάνει γρήγορο.
draft: false
keywords:
- recognize text from images
- extract text from png
language: el
og_description: Ανακαλύψτε τον πιο εύκολο τρόπο για να αναγνωρίζετε κείμενο από εικόνες
  σε Java και να εξάγετε κείμενο από αρχεία png χρησιμοποιώντας το Aspose OCR με παράλληλη
  επεξεργασία.
og_title: Αναγνώριση κειμένου από εικόνες με Java – Οδηγός Παράλληλης OCR
tags:
- OCR
- Java
- Aspose
title: Αναγνώριση κειμένου από εικόνες με Java – Παράλληλο Μάθημα OCR
url: /el/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνες με Java – Parallel OCR Tutorial

Ποτέ χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνες** και νιώσατε κολλημένοι στο “πώς το κάνω αυτό;”; Δεν είστε οι μόνοι. Είτε ψηφιοποιείτε τιμολόγια, εξάγετε δεδομένα από στιγμιότυπα οθόνης, είτε δημιουργείτε ένα αναζητήσιμο αρχείο, η δυνατότητα *αναγνώρισης κειμένου από εικόνες* είναι καθοριστική.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα Java που όχι μόνο **αναγνωρίζει κείμενο από εικόνες** αλλά δείχνει και πώς να **εξάγετε κείμενο από png** αρχεία χρησιμοποιώντας τη ενσωματωμένη παράλληλη μηχανή του Aspose OCR. Χωρίς εξωτερικά scripts, χωρίς ελλείψεις — απλός κώδικας και σαφείς εξηγήσεις.

## Τι θα μάθετε

- Ρύθμιση του Aspose OCR σε έργο Java  
- Ενεργοποίηση παράλληλης επεξεργασίας για επιτάχυνση των batch εργασιών  
- Φόρτωση συλλογής PNG αρχείων και **εξαγωγή κειμένου από png** αποδοτικά  
- Διαχείριση κοινών προβλημάτων (μεγάλα αρχεία, κενά αποτελέσματα, όρια νημάτων)  
- Προβολή του πλήρους, εκτελέσιμου κώδικα στο τέλος του άρθρου  

Μέχρι το τέλος, θα έχετε μια λύση copy‑paste που μπορείτε να προσαρμόσετε σε οποιαδήποτε ροή εργασίας εξαγωγής κειμένου από εικόνες.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντική |
|----------|------------------------|
| Java 8 ή νεότερη | Το Java API του Aspose OCR στοχεύει σε Java 8+ |
| Maven ή Gradle (για διαχείριση εξαρτήσεων) | Απλοποιεί την προσθήκη της βιβλιοθήκης Aspose OCR |
| Μερικά PNG αρχεία που θέλετε να επεξεργαστείτε | Το tutorial χρησιμοποιεί `doc1.png`‑`doc4.png` ως παραδείγματα |
| Βασικές γνώσεις σύνταξης Java | Ο κώδικας είναι απλός, αλλά χρειάζεται να τον μεταγλωττίσετε και να τον τρέξετε |

Αν λείπει κάτι από τα παραπάνω, κατεβάστε το τελευταίο JDK από την Oracle ή το AdoptOpenJDK και στήστε ένα απλό Maven project — δεν χρειάζεται τίποτα περίπλοκο.

![recognize text from images diagram](image.png){alt="διάγραμμα αναγνώρισης κειμένου από εικόνες"}

## Βήμα 1 – Προσθήκη Aspose OCR στο έργο σας

Πρώτα, πείτε στο Maven (ή Gradle) να κατεβάσει τη βιβλιοθήκη Aspose OCR. Σε ένα αρχείο `pom.xml`, προσθέστε:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Ελέγξτε το [Aspose OCR Maven repository](https://repo.aspose.com/repo) για την πιο πρόσφατη έκδοση. Η ενημέρωση της βιβλιοθήκης εξασφαλίζει ότι έχετε τις τελευταίες βελτιώσεις OCR και διορθώσεις σφαλμάτων.

## Βήμα 2 – Ενεργοποίηση παράλληλης επεξεργασίας (η μυστική σάλτσα)

Το Aspose OCR μπορεί να διανείμει το φορτίο σε πολλούς πυρήνες CPU. Έτσι κρατάμε τη λειτουργία **αναγνώρισης κειμένου από εικόνες** γρήγορη, ακόμα και όταν έχετε δεκάδες PNG αρχεία.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

Γιατί να θέσουμε όριο; Η υπερβολική δέσμευση νημάτων μπορεί να αφαιρέσει πόρους από άλλες διεργασίες, ειδικά σε κοινόχρηστους διακομιστές. Τέσσερις πυρήνες είναι μια ασφαλής προεπιλογή για τα περισσότερα desktop· αυξήστε το αν γνωρίζετε ότι το υλικό σας μπορεί να τα αντέξει.

## Βήμα 3 – Προετοιμασία λίστας PNG αρχείων

Το tutorial εστιάζει στην **εξαγωγή κειμένου από png** αρχεία, αλλά ο ίδιος κώδικας λειτουργεί και για JPEG, BMP κ.λπ. Τοποθετήστε τις εικόνες σας σε έναν φάκελο και αναφερθείτε σε αυτές ως εξής:

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Σημείωση:** Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή όπου βρίσκονται τα PNG αρχεία. Αν χρειάζεται να επεξεργαστείτε έναν δυναμικό φάκελο, μπορείτε να χρησιμοποιήσετε `Files.list(Paths.get("YOUR_DIRECTORY"))` για να δημιουργήσετε αυτόματα τον πίνακα.

## Βήμα 4 – Εκτέλεση OCR σε κάθε εικόνα (η μηχανή κάνει το βάρος)

Ακόμη και αν ενεργοποιήσαμε το parallelism, εξακολουθούμε να κάνουμε βρόχο πάνω στον πίνακα αρχείων. Το Aspose OCR εσωτερικά διανέμει το έργο αναγνώρισης στα νήματα που διαμορφώσαμε.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### Γιατί βρόχος και όχι parallel stream;

Το Aspose OCR ήδη χωρίζει την επεξεργασία εικόνας εσωτερικά βάσει `ParallelOptions`. Η περιτύλιξη του κώδικα σε εξωτερικό parallel stream θα δημιουργούσε διπλή παράλληλη εκτέλεση και θα μπορούσε να μειώσει την απόδοση. Εμπιστευτείτε τη βιβλιοθήκη για τη διαχείριση των νημάτων.

## Βήμα 5 – Ακραίες περιπτώσεις & πρακτικές συμβουλές

| Κατάσταση | Τι πρέπει να κάνετε |
|-----------|----------------------|
| **Τεράστιο PNG ( > 10 MB )** | Αυξήστε το heap της JVM (`-Xmx2g`) ή μειώστε το μέγεθος της εικόνας πριν τη δώσετε στη μηχανή. |
| **Μικτά φορμά εικόνων** | Χρησιμοποιήστε `ocrEngine.setImage(new File(imagePath))` — η μηχανή ανιχνεύει αυτόματα το φορμά. |
| **Χρειάζεστε το πλήρες κείμενο, όχι μόνο προεπισκόπηση** | Αποθηκεύστε `result.getText()` σε ένα `StringBuilder` ή γράψτε το σε αρχείο για μεταγενέστερη ανάλυση. |
| **Εκτέλεση σε CI server χωρίς GUI** | Δεν απαιτούνται επιπλέον βήματα — το Aspose OCR λειτουργεί πλήρως headless. |
| **Λήξη άδειας** | Καταχωρίστε προσωρινή άδεια με `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` για να αποφύγετε τα υδατογραφήματα αξιολόγησης. |

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που μπορείτε να αντιγράψετε, να επικολλήσετε και να τρέξετε. Περιλαμβάνει όλα τα στοιχεία που συζητήσαμε, καθώς και μερικά σχόλια για σαφήνεια.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Αν το `doc1.png` περιέχει τη φράση “Invoice #12345 – Total $250.00”, θα δείτε κάτι όπως:

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

Η προεπισκόπηση κόβει στα 50 χαρακτήρες, αλλά η πλήρης συμβολοσειρά βρίσκεται μέσα στο `result.getText()` για οποιαδήποτε επεξεργασία χρειαστείτε.

## Συμπέρασμα

Τώρα έχετε ένα σταθερό, έτοιμο για παραγωγή πρότυπο για **αναγνώριση κειμένου από εικόνες** χρησιμοποιώντας το Aspose OCR σε Java, και έχετε δει ακριβώς πώς να **εξάγετε κείμενο από png** αρχεία με παράλληλη επιτάχυνση. Τα κύρια βήματα — ρύθμιση μηχανής, παραμετροποίηση parallel, προετοιμασία λίστας εικόνων και διαχείριση αποτελεσμάτων — έχουν καλυφθεί, μαζί με μια σειρά πρακτικών συμβουλών για να αποφύγετε κοινά προβλήματα.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε τη λίστα PNG με μια δυναμική σάρωση καταλόγου, να διοχετεύσετε το OCR output σε έναν δείκτη αναζήτησης όπως το Elasticsearch, ή να πειραματιστείτε με ρυθμίσεις OCR ανά γλώσσα (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). Ο ουρανός είναι το όριο μόλις κυριαρχήσετε στη βασική ροή εργασίας.

Αν αντιμετωπίσατε δυσκολίες ή έχετε ιδέες για την επέκταση αυτού του tutorial, αφήστε ένα σχόλιο παρακάτω. Καλό coding, και απολαύστε τη μετατροπή εκείνων των επίμονων εικόνων σε αναζητήσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}