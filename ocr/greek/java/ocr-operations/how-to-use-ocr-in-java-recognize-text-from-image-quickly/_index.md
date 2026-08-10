---
category: general
date: 2026-02-17
description: Μάθετε πώς να χρησιμοποιείτε OCR στην Java για να αναγνωρίζετε κείμενο
  από αρχεία εικόνας, να εξάγετε κείμενο από αποδείξεις PNG και να μετατρέπετε την
  απόδειξη σε JSON με το Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: el
og_description: Οδηγός βήμα‑προς‑βήμα για το πώς να χρησιμοποιήσετε OCR σε Java για
  την αναγνώριση κειμένου από εικόνα, την εξαγωγή κειμένου από αποδείξεις PNG και
  τη μετατροπή της απόδειξης σε JSON.
og_title: Πώς να χρησιμοποιήσετε OCR στη Java – Αναγνωρίστε κείμενο από εικόνα
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR στη Java – Αναγνωρίστε κείμενο από εικόνα γρήγορα
url: /el/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε Java – Αναγνώριση Κειμένου από Εικόνα Γρήγορα

Έχετε αναρωτηθεί **πώς να χρησιμοποιήσετε OCR** για να εξάγετε κείμενο από μια φωτογραφία απόδειξης; Ίσως έχετε δοκιμάσει μερικά διαδικτυακά εργαλεία, μόνο για να καταλήξετε με ακατάληπτους χαρακτήρες ή μορφή που δεν μπορείτε να επεξεργαστείτε. Τα καλά νέα είναι ότι με λίγες γραμμές κώδικα Java μπορείτε **να αναγνωρίσετε κείμενο από εικόνα**, **να εξάγετε κείμενο από PNG** αποδείξεις, και ακόμη **να μετατρέψετε την απόδειξη σε JSON** για επεξεργασία downstream.  

Σε αυτό το tutorial θα περάσουμε από την πλήρη ροή εργασίας — από την αδειοδότηση της βιβλιοθήκης Aspose OCR μέχρι την απόκτηση ενός καθαρού JSON payload που μπορείτε να τροφοδοτήσετε σε μια βάση δεδομένων ή σε ένα μοντέλο μηχανικής μάθησης. Χωρίς περιττές πληροφορίες, μόνο ένα πρακτικό, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που παίρνει το `receipt.png` και παράγει ένα έτοιμο‑για‑χρήση JSON string.

## Τι Θα Χρειαστεί

- **Java Development Kit (JDK) 8+** — οποιαδήποτε πρόσφατη έκδοση λειτουργεί.
- **Aspose OCR for Java** βιβλιοθήκη (το Maven artifact είναι `com.aspose:aspose-ocr`).
- Ένα **έγκυρο αρχείο άδειας Aspose OCR** (`Aspose.OCR.lic`). Η δωρεάν δοκιμή λειτουργεί για δοκιμές, αλλά μια πλήρης άδεια αφαιρεί τους περιορισμούς αξιολόγησης.
- Ένα αρχείο εικόνας (PNG, JPEG, κλπ.) που περιέχει το κείμενο που θέλετε να διαβάσετε — ας το ονομάσουμε `receipt.png` και τοποθετήστε το σε γνωστό φάκελο.
- Το αγαπημένο σας IDE (IntelliJ IDEA, Eclipse, VS Code…) — εσείς διαλέγετε.

> **Pro tip:** Κρατήστε το αρχείο άδειας εκτός του φακέλου πηγαίου κώδικα και αναφέρετέ το μέσω απόλυτης ή σχετικής διαδρομής για να αποφύγετε την καταχώρηση του σε σύστημα ελέγχου εκδόσεων.

Τώρα που τα προαπαιτούμενα είναι ξεκάθαρα, ας βουτήξουμε στον πραγματικό κώδικα.

## Πώς να Χρησιμοποιήσετε OCR – Κύρια Βήματα

Παρακάτω είναι μια υψηλού επιπέδου επισκόπηση των ενεργειών που θα εκτελέσουμε:

1. **Φορτώστε τη βιβλιοθήκη Aspose OCR** και εφαρμόστε την άδειά σας.  
2. **Δημιουργήστε ένα αντικείμενο `OcrEngine`** — αυτό είναι το μηχάνημα που κάνει το σκληρό έργο.  
3. **Προετοιμάστε ένα αντικείμενο `OcrInput`** που δείχνει στην εικόνα που θέλετε να επεξεργαστείτε.  
4. **Καλέστε `recognize` με `ResultFormat.JSON`** για να λάβετε μια JSON αναπαράσταση του εξαγόμενου κειμένου.  
5. **Διαχειριστείτε το JSON output** — εκτυπώστε το, γράψτε το σε αρχείο ή επεξεργαστείτε το περαιτέρω.

Κάθε βήμα εξηγείται λεπτομερώς στις ενότητες που ακολουθούν.

## Βήμα 1 – Εγκατάσταση Aspose OCR και Εφαρμογή Άδειας

Πρώτα, προσθέστε την εξάρτηση Aspose OCR στο `pom.xml` αν χρησιμοποιείτε Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Τώρα, στον κώδικα Java, φορτώστε την άδεια. Αυτό το βήμα είναι κρίσιμο· χωρίς αυτό η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης και μπορεί να ενσωματώνει υδατογραφήματα στο αποτέλεσμα.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Γιατί είναι σημαντικό:** Το αντικείμενο `License` ενημερώνει τη μηχανή OCR ότι έχετε εξουσιοδότηση για χρήση του πλήρους συνόλου λειτουργιών, που περιλαμβάνει υψηλής ακρίβειας αναγνώριση και εξαγωγή JSON. Παραλείποντας αυτό το βήμα θα μπορείτε ακόμα **να αναγνωρίσετε κείμενο από εικόνα**, αλλά τα αποτελέσματα μπορεί να είναι περιορισμένα.

## Βήμα 2 – Δημιουργία του Αντικειμένου OCR Engine

Η κλάση `OcrEngine` είναι το σημείο εισόδου για όλες τις λειτουργίες OCR. Σκεφτείτε το ως το «εγκέφαλο» που διαβάζει τα pixel και αποφασίζει ποιοι χαρακτήρες αντιστοιχούν.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Μπορείτε να προσαρμόσετε τη μηχανή (π.χ., να ορίσετε γλώσσα, να ενεργοποιήσετε deskew) αργότερα αν οι αποδείξεις σας περιέχουν μη‑λατινικά σενάρια ή είναι σαρωμένες με κλίση. Για τις περισσότερες αποδείξεις των ΗΠΑ, οι προεπιλογές λειτουργούν τέλεια.

## Βήμα 3 – Φόρτωση της Εικόνας που Θέλετε να Επεξεργαστείτε

Τώρα θα κατευθύνουμε τη μηχανή OCR στο αρχείο που περιέχει την απόδειξη. Η κλάση `OcrInput` μπορεί να δεχτεί πολλαπλές εικόνες, αλλά για αυτό το tutorial θα το κρατήσουμε απλό με ένα μόνο PNG.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Αν ποτέ χρειαστεί να **εξάγετε κείμενο από PNG** σε μαζική κλίμακα, απλώς καλέστε επανειλημμένα `input.add()` ή περάστε μια λίστα διαδρομών αρχείων.

## Βήμα 4 – Αναγνώριση Κειμένου και Μετατροπή Απόδειξης σε JSON

Αυτή είναι η καρδιά του tutorial. Ζητάμε από τη μηχανή να αναγνωρίσει το κείμενο και ζητάμε το αποτέλεσμα σε μορφή JSON. Η σημαία `ResultFormat.JSON` κάνει όλη τη σκληρή δουλειά για εμάς.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Το JSON payload περιλαμβάνει κάθε αναγνωρισμένη γραμμή, το bounding box της, το confidence score και το ακατέργαστο κείμενο. Αυτή η δομή το καθιστά εξαιρετικά εύκολο να **μετατρέψετε την απόδειξη σε JSON** και να το τροφοδοτήσετε σε οποιοδήποτε downstream API.

## Βήμα 5 – Συνδυάστε Όλα και Εκτελέστε το Πρόγραμμα

Παρακάτω είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java που ενώνει όλα τα παραπάνω. Αποθηκεύστε την ως `JsonExportDemo.java` (ή όποιο όνομα θέλετε) και τρέξτε την από το IDE ή τη γραμμή εντολών.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει ένα JSON string παρόμοιο με το παρακάτω (το ακριβές περιεχόμενο εξαρτάται από την απόδειξή σας):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Τώρα μπορείτε να τροφοδοτήσετε αυτό το JSON σε μια βάση δεδομένων, ένα REST endpoint ή μια pipeline ανάλυσης δεδομένων. Το βήμα **μετατροπής απόδειξης σε JSON** είναι ήδη ολοκληρωμένο.

## Συχνές Ερωτήσεις και Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα είναι περιστραμμένη;

Το Aspose OCR ανιχνεύει αυτόματα και διορθώνει ήπιες περιστροφές. Για σοβαρά παραμορφωμένες εικόνες, καλέστε `engine.getImagePreprocessingOptions().setDeskew(true)` πριν από την αναγνώριση.

### Πώς διαχειρίζομαι πολλαπλές γλώσσες;

Χρησιμοποιήστε `engine.getLanguage()` για να ορίσετε τη γλώσσα, π.χ., `engine.setLanguage(Language.FRENCH)`. Αυτό είναι χρήσιμο όταν πρέπει να **αναγνωρίσετε κείμενο από εικόνα** που περιέχει πολύγλωσσες αποδείξεις.

### Μπορώ να εξάγω απλό κείμενο αντί για JSON;

Απολύτως. Αντικαταστήστε το `ResultFormat.JSON` με `ResultFormat.TEXT` και καλέστε `result.getText()`.

### Υπάρχει τρόπος να περιορίσω το OCR σε συγκεκριμένη περιοχή;

Ναι — χρησιμοποιήστε `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` για να εστιάσετε στην περιοχή της απόδειξης, κάτι που μπορεί να βελτιώσει την ταχύτητα και την ακρίβεια.

## Pro Tips για Παραγωγική OCR

- **Cache το αντικείμενο άδειας** αν επεξεργάζεστε πολλά αρχεία σε βρόχο· η δημιουργία του επανειλημμένα προσθέτει overhead.
- **Batch processing**: φορτώστε όλες τις διαδρομές αποδείξεων σε ένα `OcrInput` και καλέστε `recognize` μία φορά. Το JSON θα περιέχει έναν πίνακα σελίδων, η κάθε μία με τις δικές της γραμμές.
- **Επαληθεύστε το JSON**: μετά τη λήψη του string, αναλύστε το με βιβλιοθήκη όπως η Jackson για να βεβαιωθείτε ότι είναι καλά σχηματισμένο πριν το αποθηκεύσετε.
- **Παρακολουθήστε το confidence**: το JSON περιλαμβάνει πεδίο `confidence` ανά γραμμή. Φιλτράρετε γραμμές κάτω από ένα όριο (π.χ., 0.85) για να αποφύγετε ακατάλληλα δεδομένα.
- **Ασφαλίστε την άδειά σας**: αποθηκεύστε το `Aspose.OCR.lic` σε ασφαλές vault ή μεταβλητή περιβάλλοντος, ειδικά σε cloud deployments.

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε OCR** σε Java για **αναγνώριση κειμένου από εικόνα**, **εξαγωγή κειμένου από PNG** αποδείξεις, και **μετατροπή απόδειξης σε JSON** — όλα με ένα σύντομο, ολοκληρωμένο παράδειγμα. Τα βήματα είναι απλά, ο κώδικας εκτελέσιμος, και το JSON output σας δίνει μια δομημένη αναπαράσταση έτοιμη για οποιοδήποτε downstream σύστημα.

Στη συνέχεια, μπορείτε να εξερευνήσετε πιο προχωρημένα σενάρια: τροφοδοσία του JSON σε Apache Kafka για real‑time επεξεργασία, εφαρμογή regex για εξαγωγή συνολικών τιμών, ή ενσωμάτωση με cloud OCR υπηρεσία για κλιμακωσιμότητα. Ό,τι και αν επιλέξετε, τα θεμέλια που μόλις μάθατε θα παραμείνουν τα ίδια.

Έχετε ερωτήσεις ή αντιμετωπίσατε κάποιο πρόβλημα κατά την υλοποίηση; Αφήστε ένα σχόλιο παρακάτω και ας το λύσουμε μαζί. Καλό coding, και απολαύστε τη μετατροπή των ακατάστατων εικόνων αποδείξεων σε καθαρά, αναζητήσιμα δεδομένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}