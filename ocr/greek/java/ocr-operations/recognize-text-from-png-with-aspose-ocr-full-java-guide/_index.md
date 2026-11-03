---
category: general
date: 2026-03-28
description: Μάθετε πώς να αναγνωρίζετε κείμενο από PNG χρησιμοποιώντας το Aspose
  OCR σε Java. Περιλαμβάνει εξαγωγή κειμένου από εικόνα και ενεργοποίηση αυτόματης
  ανίχνευσης γλώσσας για μεικτές γλώσσες.
draft: false
keywords:
- recognize text from png
- extract text from image
- enable auto language detection
language: el
og_description: αναγνωρίστε κείμενο από png άμεσα. Αυτός ο οδηγός δείχνει πώς να εξάγετε
  κείμενο από εικόνα και να ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας για PDF
  με μεικτές γλώσσες.
og_title: Αναγνώριση κειμένου από PNG με το Aspose OCR – Πλήρης οδηγός Java
tags:
- Aspose OCR
- Java
- Image Processing
title: Αναγνώριση κειμένου από PNG με Aspose OCR – Πλήρης Οδηγός Java
url: /el/java/ocr-operations/recognize-text-from-png-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από PNG με Aspose OCR – Πλήρης Java Tutorial

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από PNG** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα διαχειριστεί πολυγλωσσικά κείμενα με ευκολία; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν οι εφαρμογές τους πρέπει να διαβάζουν αποδείξεις, διαβατήρια ή πολυγλωσσική σήμανση.  

Τα καλά νέα είναι ότι το Aspose OCR το κάνει παιχνιδάκι: με λίγες μόνο γραμμές μπορείτε να **εξάγετε κείμενο από εικόνα**, να μετατρέψετε ένα PNG σε αναζητήσιμα δεδομένα, και ακόμη να **ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας** ώστε η μηχανή να επιλέγει το σωστό σύστημα γραφής αυτόματα.  

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε για να ξεκινήσετε: προαπαιτούμενα, κώδικα βήμα‑βήμα, γιατί κάθε ρύθμιση είναι σημαντική και πώς να επαληθεύσετε το αποτέλεσμα. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα Java που μπορεί να διαβάσει ένα PNG που περιέχει κείμενο στα Αγγλικά, Ρωσικά και Κινέζικα—χωρίς να χρειάζεται να αλλάζετε χειροκίνητα πακέτα γλώσσας.

---

## Τι Θα Χρειαστεί

- **Java Development Kit (JDK) 8+** – ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK.  
- **Aspose.OCR for Java** library (η πιο πρόσφατη έκδοση μέχρι το 2026). Μπορείτε να το κατεβάσετε από το Maven Central ή τον ιστότοπο Aspose.  
- Ένα αρχείο εικόνας (π.χ., `mixed-lang.png`) που περιέχει κείμενο σε πολλές γλώσσες.  
- Ένα καλό IDE (IntelliJ IDEA, Eclipse, ή ακόμη VS Code) – αλλά λειτουργεί και ένας απλός επεξεργαστής κειμένου.  

> **Pro tip:** Εάν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση παρακάτω· διαφορετικά κατεβάστε το JAR και προσθέστε το στο classpath σας.  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the newest version -->
</dependency>
```

---

## Βήμα 1: Αρχικοποίηση του OCR Engine για αναγνώριση κειμένου από PNG

Πριν η μηχανή μπορέσει να κάνει οτιδήποτε, χρειάζεστε μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο κρατά όλες τις επιλογές διαμόρφωσης και εκτελεί τις βαριές εργασίες.  

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine – this is the entry point for all operations
        OcrEngine ocrEngine = new OcrEngine();

        // --------------------------------------------------------------
        // Step 2 and 3 are configured here (see next sections)
        // --------------------------------------------------------------

        // Recognize the image and get the result object
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Why this matters:** Το `OcrEngine` αφαιρεί την πολυπλοκότητα του υποκείμενου αλγορίθμου OCR. Η δημιουργία του μία φορά και η επαναχρησιμοποίησή του σε πολλές εικόνες είναι πιο αποδοτική από το να δημιουργείτε νέο engine για κάθε αρχείο.  

---

## Βήμα 2: Ενεργοποίηση αυτόματης ανίχνευσης γλώσσας

Αν παραλείψετε αυτό το βήμα, η μηχανή θα υποθέσει μια ενιαία προεπιλεγμένη γλώσσα (συνήθως Αγγλικά), κάτι που οδηγεί σε ακατανόητους χαρακτήρες για κυριλλικά ή κινέζικα σύμβολα. Η ενεργοποίηση της αυτόματης ανίχνευσης επιτρέπει στο Aspose να σαρώσει την εικόνα και να επιλέξει αυτόματα το καλύτερο μοντέλο γλώσσας.  

```java
// Enable automatic language detection – the engine will sniff the script
ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);
```

> **What’s happening under the hood?** Το Aspose OCR εκτελεί μια ελαφριά προ‑ανάλυση που ελέγχει τη συχνότητα χαρακτήρων και τις περιοχές Unicode. Όταν εντοπίζει μια κυρίαρχη γλώσσα, αντικαθιστά το αντίστοιχο μοντέλο γλώσσας πριν από το βαρέως βάρους OCR πέρασμα.  

---

## Βήμα 3: (Προαιρετικό) Περιορισμός της ανίχνευσης σε πιθανές γλώσσες – βελτίωση ταχύτητας

Όταν γνωρίζετε το σύνολο των γλωσσών που αναμένετε, μπορείτε να δώσετε ένα στοιχείο στην μηχανή. Αυτό περιορίζει το χώρο αναζήτησης, μειώνει τη χρήση CPU και συχνά δίνει πιο γρήγορα αποτελέσματα.  

```java
// Suggest candidate languages – only English, Russian, and Chinese will be considered
ocrEngine.getRecognitionSettings()
         .setCandidateLanguages(new String[] { "en", "ru", "zh" });
```

> **Tip:** Αν παραλείψετε αυτό το βήμα, η μηχανή θα λειτουργήσει ακόμα, αλλά θα αξιολογήσει όλες τις υποστηριζόμενες γλώσσες, κάτι που μπορεί να προσθέσει μερικά δευτερόλεπτα σε μεγάλες παρτίδες.  

---

## Βήμα 4: Αναγνώριση του PNG και εξαγωγή κειμένου από την εικόνα

Τώρα που η μηχανή είναι διαμορφωμένη, καλέστε το `recognizeImage`. Η μέθοδος δέχεται διαδρομή αρχείου, ένα `java.io.File`, ή ακόμη ένα `java.io.InputStream`, προσφέροντάς σας ευελιξία για μεταφορτώσεις web ή αποθήκευση στο cloud.  

```java
// Perform OCR on the specified PNG file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

// The result object holds the raw text, confidence scores, and layout info
String extractedText = ocrResult.getText();
```

> **Edge case:** Αν η εικόνα είναι περιστραμμένη, το Aspose OCR μπορεί να την περιστρέψει αυτόματα. Μπορείτε επίσης να ορίσετε χειροκίνητα `setDetectOrientation(true)` αν παρατηρήσετε μη ευθυγραμμισμένο αποτέλεσμα.  

---

## Βήμα 5: Εμφάνιση του αποτελέσματος – επαλήθευση του output

Η εκτύπωση στην κονσόλα είναι εντάξει για μια γρήγορη επίδειξη, αλλά σε μια πραγματική εφαρμογή μπορεί να αποθηκεύσετε το κείμενο σε βάση δεδομένων, να το τροφοδοτήσετε σε ευρετήριο αναζήτησης ή να το επιστρέψετε μέσω REST API. Παρακάτω υπάρχει ένα ελάχιστο απόσπασμα επαλήθευσης.  

```java
System.out.println("=== Recognized Text ===");
System.out.println(extractedText);
```

### Αναμενόμενη έξοδος στην κονσόλα

Υποθέτοντας ότι το `mixed-lang.png` περιέχει τις τρεις γραμμές:  

```
Hello world!
Привет мир!
你好，世界！
```

Θα πρέπει να δείτε κάτι όπως:  

```
=== Recognized Text ===
Hello world!
Привет мир!
你好，世界！
```

Αν το αποτέλεσμα φαίνεται ακατάστατο, ελέγξτε ξανά ότι το `setAutoDetectLanguage(true)` είναι ενεργοποιημένο και ότι η λίστα των υποψήφιων γλωσσών περιλαμβάνει τα σύμβολα που χρειάζεστε.  

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);

        // Step 3: (Optional) Limit detection to likely languages
        ocrEngine.getRecognitionSettings()
                 .setCandidateLanguages(new String[] { "en", "ru", "zh" });

        // Step 4: Recognize the PNG image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Run it:** Συγκεντρώστε με `javac MixedLangExample.java` και εκτελέστε `java MixedLangExample`. Βεβαιωθείτε ότι το Aspose OCR JAR βρίσκεται στο classpath σας (π.χ., `-cp aspose-ocr-23.12.jar;.` στα Windows ή `-cp aspose-ocr-23.12.jar:.` σε Linux/macOS).  

---

## Συχνές Ερωτήσεις & Προβλήματα

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η εικόνα μου είναι JPEG αντί για PNG;** | Η ίδια μέθοδος `recognizeImage` λειτουργεί για JPEG, BMP, TIFF κ.λπ. Απλώς αλλάξτε την επέκταση του αρχείου. |
| **Μπορώ να επεξεργαστώ ένα stream από ένα HTTP αίτημα;** | Απολύτως. Χρησιμοποιήστε `recognizeImage(InputStream)` και περάστε απευθείας το input stream του αιτήματος. |
| **Πόσο ακριβής είναι η αυτόματη ανίχνευση γλώσσας για παρόμοια συστήματα γραφής (π.χ., Σέρβικα Κυριλλικά vs Ρωσικά);** | Συνήθως είναι ακριβής, αλλά μπορείτε να εξαναγκάσετε μια γλώσσα προσθέτοντάς την στο `candidateLanguages` και αφαιρώντας τις άλλες. |
| **Χρειάζομαι άδεια για το Aspose OCR;** | Μια δωρεάν άδεια αξιολόγησης λειτουργεί για δοκιμές, αλλά η παραγωγική χρήση απαιτεί πληρωμένη άδεια για την αφαίρεση του υδατογράμματος και την ενεργοποίηση όλων των λειτουργιών. |
| **Τι γίνεται με την απόδοση σε μεγάλες παρτίδες;** | Επαναχρησιμοποιήστε μια μόνο παρουσία του `OcrEngine` και επεξεργαστείτε τις εικόνες διαδοχικά ή σε thread pool. Η μηχανή είναι thread‑safe για λειτουργίες μόνο ανάγνωσης. |

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Εξαγωγή κειμένου από εικόνα** σε αρχεία PDF – συνδυάστε το Aspose PDF με OCR για σαρωμένα έγγραφα.  
- **Επεξεργασία παρτίδας** – χρησιμοποιήστε το `ExecutorService` της Java για να παράλληλοποιήσετε χιλιάδες PNG.  
- **Μεταεπεξεργασία** – εφαρμόστε ορθογραφικό έλεγχο ή γλωσσο‑συγκεκριμένη τοκενοποίηση μετά την εξαγωγή.  
- **Ενσωμάτωση με αποθήκευση cloud** – διαβάστε PNG απευθείας από AWS S3 ή Azure Blob Storage χρησιμοποιώντας streams.  

Μη διστάσετε να πειραματιστείτε: δοκιμάστε να προσθέσετε `setDetectOrientation(true)` αν έχετε περιστρεφόμενες σκαναρίσματα, ή αντικαταστήστε τη λίστα υποψήφιων γλωσσών ώστε να περιλαμβάνει Ιαπωνικά (`"ja"`) ή Αραβικά (`"ar"`). Το API είναι αρκετά ευέλικτο για τα περισσότερα έργα που εστιάζουν στο OCR.  

---

## Συμπέρασμα

Τώρα έχετε ένα ολοκληρωμένο παράδειγμα που δείχνει πώς να **αναγνωρίζετε κείμενο από PNG** χρησιμοποιώντας το Aspose OCR, **εξάγετε κείμενο από εικόνα**, και **ενεργοποιήσετε την αυτόματη ανίχνευση γλώσσας** για περιεχόμενο πολλαπλών γλωσσών. Ο κώδικας είναι πλήρης, οι εξηγήσεις καλύπτουν τόσο το “πώς” όσο και το “γιατί”, και έχετε δει το αναμενόμενο αποτέλεσμα ώστε να επαληθεύσετε ότι όλα λειτουργούν στη μηχανή σας.  

Έχετε διαφορετική περίπτωση χρήσης; Αφήστε ένα σχόλιο, μοιραστείτε τα ευρήματά σας, ή εξερευνήστε τα επόμενα βήματα παραπάνω. Καλή προγραμματιστική!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}