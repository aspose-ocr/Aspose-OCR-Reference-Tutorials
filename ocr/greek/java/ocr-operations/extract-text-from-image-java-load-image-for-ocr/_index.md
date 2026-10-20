---
category: general
date: 2026-04-29
description: Εξαγωγή κειμένου από εικόνα Java χρησιμοποιώντας Aspose OCR – μάθετε
  πώς να φορτώνετε εικόνα για OCR και να αναγνωρίζετε κείμενο από απόδειξη σε μορφή
  JSON.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: el
og_description: Εξαγωγή κειμένου από εικόνα Java με Aspose OCR. Αυτό το σεμινάριο
  δείχνει πώς να φορτώσετε εικόνα για OCR και να αναγνωρίσετε κείμενο από απόδειξη,
  εξάγοντας JSON.
og_title: Εξαγωγή κειμένου από εικόνα Java – Πλήρης Οδηγός
tags:
- Java
- OCR
- Aspose
title: Εξαγωγή κειμένου από εικόνα Java – Φόρτωση εικόνας για OCR
url: /el/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extract text from image java – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **extract text from image java** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν προσπαθούν να **load image for OCR** και στη συνέχεια λαμβάνουν το ακατέργαστο κείμενο σε μορφή που είναι δύσκολο να επεξεργαστεί.

Σε αυτό το tutorial θα περάσουμε από μια καθαρή, ολοκληρωμένη λύση που όχι μόνο **load image for OCR** αλλά και **recognize text from receipt** και θα αποδώσει μια τακτοποιημένη συμβολοσειρά JSON. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση κλάση Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο — χωρίς επιπλέον ρυθμίσεις.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR για Java (η βιβλιοθήκη που κάνει το βαρέως βάρους έργο εύκολο).
- Τα ακριβή βήματα για **load image for OCR** από το δίσκο.
- Πώς να διαμορφώσετε τη μηχανή ώστε να επιστρέφει αποτελέσματα σε JSON, που είναι ιδανικό για επεξεργασία downstream.
- Πώς να **recognize text from receipt** εικόνες και να επαληθεύσετε το αποτέλεσμα.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· χρειάζεστε μόνο ένα λειτουργικό JDK και ένα IDE με το οποίο αισθάνεστε άνετα.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| **Java 17+** (or any recent JDK) | Το Aspose OCR παρέχει προ‑συγκροτημένα binaries για σύγχρονες εκδόσεις Java. |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | Κάνει τη διαχείριση εξαρτήσεων παιχνιδάκι. |
| **A sample receipt image** (e.g., `receipt.png`) | Θα χρησιμοποιήσουμε αυτό το αρχείο για να δείξουμε **recognize text from receipt**. |
| **Internet connection** (once) | Απαιτείται για τη λήψη του Aspose JAR την πρώτη φορά. |

Αν τα έχετε ήδη, τέλεια—ας ξεκινήσουμε.

## Βήμα 1: Προσθέστε το Aspose OCR στο Έργο σας

Το πρώτο που χρειάζεστε είναι η βιβλιοθήκη Aspose OCR. Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Για Gradle, είναι ως εξής:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Συμβουλή:** Κλειδώστε τον αριθμό έκδοσης. Η μετέπειτα αναβάθμιση μπορεί να εισάγει λεπτές αλλαγές στο API που θα σπάσουν τον κώδικά σας.

Μόλις επιλυθεί η εξάρτηση, είστε έτοιμοι να γράψετε κώδικα Java που πραγματικά **extract text from image java**.

## Βήμα 2: Φορτώστε την Εικόνα για OCR

Τώρα θα δείξουμε τη συγκεκριμένη γραμμή που **load image for OCR**. Το Aspose παρέχει ένα βολικό βοηθητικό `ImageStream.fromFile`.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή προς το αρχείο απόδειξης σας. Αν η διαδρομή είναι λανθασμένη, η μηχανή θα ρίξει ένα `FileNotFoundException`, οπότε ελέγξτε ξανά την ορθογραφία.

> **Γιατί είναι σημαντικό:** Η σωστή φόρτωση της εικόνας είναι το θεμέλιο. Αν η εικόνα δεν διαβαστεί, η μηχανή OCR δεν έχει τίποτα να αναγνωρίσει και θα καταλήξετε με ένα κενό αποτέλεσμα JSON.

## Βήμα 3: Ενημερώστε τη Μηχανή να Επιστρέφει JSON

Το Aspose OCR μπορεί να εκδώσει XML, απλό κείμενο ή JSON. Για σύγχρονα APIs το JSON είναι το πιο ευέλικτο, οπότε θα ορίσουμε τη μορφή ρητά.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

Μπορείτε να μεταβείτε σε `OcrResultFormat.XML` με μία μικρή αλλαγή αν το downstream σύστημα σας προτιμά XML. Το API έχει σχεδιαστεί ώστε να είναι εναλλάξιμο.

## Βήμα 4: Εκτελέστε τη Διαδικασία Αναγνώρισης

Με την εικόνα φορτωμένη και τη μορφή ορισμένη, το επόμενο βήμα είναι να **recognize text from receipt**. Εδώ γίνεται η βαριά δουλειά.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

Η κλήση `recognize()` μπλοκάρει μέχρι η μηχανή να ολοκληρώσει την ανάλυση της εικόνας. Για μεγάλες εικόνες ίσως θέλετε να το τρέξετε σε νήμα παρασκηνίου, αλλά για μια τυπική απόδειξη ολοκληρώνεται σε κλάσμα του δευτερολέπτου.

## Βήμα 5: Πάρτε το Αποτέλεσμα JSON

Τέλος, εξάγουμε τη ακατέργαστη συμβολοσειρά JSON και την εκτυπώνουμε. Αυτή η συμβολοσειρά περιέχει κάθε τμήμα του αναγνωρισμένου κειμένου, το πλαίσιο του, τις βαθμολογίες εμπιστοσύνης και άλλα.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του πλήρους προγράμματος σε μια καθαρή απόδειξη δίνει κάτι σαν:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

Παρατηρήστε πώς κάθε γραμμή της απόδειξης είναι ένα ξεχωριστό μπλοκ με βαθμολογία εμπιστοσύνης. Τώρα μπορείτε να τροφοδοτήσετε αυτό το JSON σε οποιοδήποτε downstream σύστημα — να το αποθηκεύσετε σε βάση δεδομένων, να το στείλετε μέσω HTTP ή να το δώσετε σε μοντέλο μηχανικής μάθησης.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι η πλήρης, αυτόνομη κλάση Java που συνδυάζει όλα. Αντιγράψτε‑και‑επικολλήστε την, προσαρμόστε τη διαδρομή της εικόνας και τρέξτε `mvn compile exec:java` (ή την αντίστοιχη εντολή Gradle).

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **Προσοχή:**  
> • **Σφάλματα διαδρομής αρχείου** – ελέγξτε ξανά τις κάθετες γραμμές σε Windows vs. macOS/Linux.  
> • **Έλλειψη μνήμης** – μεγάλες εικόνες μπορεί να χρειάζονται `ocrEngine.setMemoryOptimization(true)`.  
> • **Ρυθμίσεις γλώσσας** – αν η απόδειξή σας περιέχει μη λατινικούς χαρακτήρες, καλέστε `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν το `recognize()`.

## Δοκιμή της Λύσης

1. **Τρέξτε το πρόγραμμα** – θα πρέπει να δείτε ένα JSON blob να εκτυπώνεται στην κονσόλα.  
2. **Επικυρώστε το JSON** – αντιγράψτε το αποτέλεσμα στο <https://jsonlint.com/> για να βεβαιωθείτε ότι είναι σωστά δομημένο.  
3. **Αναλύστε το** – σε ένα πραγματικό έργο θα χρησιμοποιούσατε μια βιβλιοθήκη όπως Jackson ή Gson για να μετατρέψετε το JSON σε POJOs για ευκολότερη διαχείριση.

Αν αντιμετωπίσετε έναν κενό πίνακα `pages`, οι πιο συνηθισμένοι λόγοι είναι: το αρχείο εικόνας δεν βρέθηκε ή η εικόνα είναι πολύ θολή για τις προεπιλεγμένες ρυθμίσεις της μηχανής. Στην τελευταία περίπτωση, δοκιμάστε να αυξήσετε το DPI ή να εφαρμόσετε ένα βήμα προεπεξεργασίας (π.χ., δυαδικοποίηση) πριν το δώσετε στο Aspose.

## Παραλλαγές & Ακραίες Περιπτώσεις

| Σενάριο | Τι να αλλάξετε |
|----------|----------------|
| **Multiple pages** (π.χ., PDF πολλαπλών σελίδων μετατρεπόμενο σε εικόνες) | Επανάληψη σε κάθε εικόνα, κλήση του `ocrEngine.setImage(...)` μέσα στον βρόχο, και συγκέντρωση των αποτελεσμάτων JSON. |
| **Different output format** | Αντικαταστήστε το `OcrResultFormat.JSON` με `OcrResultFormat.XML` ή `OcrResultFormat.PLAIN_TEXT`. |
| **Performance tuning** | Χρησιμοποιήστε `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` για ταχύτητα, ή `OcrRecognitionMode.ACCURATE` για ποιότητα. |
| **Non‑receipt documents** | Ρυθμίστε το `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` αν χρειάζεστε εξαγωγή πινάκων. |

## Συμπέρασμα

Μόλις καλύψαμε έναν σύντομο, έτοιμο για παραγωγή τρόπο να **extract text from image java** χρησιμοποιώντας το Aspose OCR. Ακολουθώντας τα πέντε βήματα — δημιουργήστε τη μηχανή, **load image for OCR**, ορίστε την έξοδο JSON, **recognize text from receipt**, και τέλος διαβάστε το JSON — μπορείτε να ενσωματώσετε OCR σε οποιοδήποτε backend Java με ελάχιστο κόπο.

Από εδώ ίσως θέλετε να:

- Αποθηκεύσετε το JSON σε μια NoSQL βάση δεδομένων για μελλοντική ανάλυση.  
- Στείλετε το αποτέλεσμα σε ένα chatbot που απαντά σε ερωτήσεις σχετικά με αποδείξεις.  
- Συνδυάσετε αυτό με το Apache Tika για να διαχειριστείτε PDF, DOCX και άλλες μορφές.

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις ώστε να ταιριάζουν στα συγκεκριμένα έγγραφά σας, και αφήστε τη μηχανή να κάνει τη βαριά δουλειά ενώ εσείς εστιάζετε στην προσθήκη αξίας.

---

![extract text from image java](placeholder-image.png "extract text from image java")

*Σχήμα: Οπτική αναπαράσταση της διαδικασίας OCR – από το αρχείο εικόνας στο JSON output.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}