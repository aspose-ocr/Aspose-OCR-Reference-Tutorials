---
category: general
date: 2026-06-22
description: αναγνώριση κειμένου από jpg σε Java με Aspose OCR – μάθετε πώς να φορτώνετε
  εικόνα για OCR, να εξάγετε κείμενο από την εικόνα και να μετατρέπετε την εικόνα
  σε κείμενο γρήγορα.
draft: false
keywords:
- recognize text from jpg
- extract text from image
- convert image to text
- read scanned document
- load image for ocr
language: el
og_description: αναγνώριση κειμένου από jpg σε Java – βήμα‑βήμα οδηγός για τη φόρτωση
  εικόνας για OCR, την εξαγωγή κειμένου από την εικόνα και τη μετατροπή της εικόνας
  σε κείμενο.
og_title: αναγνώριση κειμένου από jpg χρησιμοποιώντας Aspose OCR σε Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from jpg in Java with Aspose OCR – learn how to load
    image for OCR, extract text from image, and convert image to text quickly.
  headline: recognize text from jpg using Aspose OCR in Java
  type: TechArticle
- description: recognize text from jpg in Java with Aspose OCR – learn how to load
    image for OCR, extract text from image, and convert image to text quickly.
  name: recognize text from jpg using Aspose OCR in Java
  steps:
  - name: Prerequisites (the bare minimum)
    text: '- Java Development Kit (JDK) 8 or newer installed. - Maven or Gradle (we’ll
      use Maven in the example, but the same JAR works with Gradle). - A JPEG image
      you want to test with (named `sample.jpg` for simplicity). - An Aspose OCR license
      (the free evaluation works fine for this demo).'
  - name: Why each line matters
    text: 1. **`OcrEngine engine = new OcrEngine();`** – Instantiates the engine.
      Think of it as turning on the scanner. 2. **`engine.setImage(...)`** – This
      is where we **load image for OCR**. The method accepts an `ImageStream`, which
      can come from a file, a byte array, or even a network stream. 3. **`engin
  - name: From a byte array (e.g., when the image is stored in a database)
    text: '```java byte[] imageBytes = Files.readAllBytes(Paths.get("YOUR_DIRECTORY/sample.jpg"));
      engine.setImage(ImageStream.fromByteArray(imageBytes)); ```'
  - name: Directly from a URL (useful for web services)
    text: '```java URL imageUrl = new URL("https://example.com/sample.jpg"); engine.setImage(ImageStream.fromUrl(imageUrl));
      ```'
  type: HowTo
tags:
- Java
- Aspose OCR
- Image Processing
title: Αναγνώριση κειμένου από JPG χρησιμοποιώντας Aspose OCR σε Java
url: /el/java/ocr-basics/recognize-text-from-jpg-using-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από jpg χρησιμοποιώντας Aspose OCR σε Java – Πλήρης Οδηγός

Ποτέ χρειάστηκε να **αναγνωρίσετε κείμενο από jpg** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα το έκανε εύκολο; Δεν είστε μόνοι. Είτε ψηφιοποιείτε παλιούς λογαριασμούς, εξάγετε δεδομένα από σαρωμένες φόρμες, είτε απλώς θέλετε να μετατρέψετε εικόνες σε αναζητήσιμες συμβολοσειρές, αυτό το tutorial δείχνει ακριβώς πώς να **φορτώσετε εικόνα για OCR**, **εξάγετε κείμενο από εικόνα**, και **μετατρέψετε εικόνα σε κείμενο** με Aspose OCR σε Java.

Σε λίγα λεπτά θα δημιουργήσουμε ένα μικρό πρόγραμμα Java, θα του δώσουμε ένα JPEG και θα παρακολουθήσουμε τη μηχανή να εκτυπώνει απλό‑κείμενο. Χωρίς μυστικά command‑line, χωρίς εξωτερικές υπηρεσίες — μόνο καθαρός, on‑prem κώδικας που μπορείτε να τρέξετε οπουδήποτε τρέχει Java.

## Τι θα αποκομίσετε

- Ένα λειτουργικό έργο Java που **αναγνωρίζει κείμενο από jpg** αρχεία.  
- Κατανόηση κάθε βήματος: εγκατάσταση της βιβλιοθήκης, φόρτωση της εικόνας, εκτέλεση της μηχανής OCR και διαχείριση του αποτελέσματος.  
- Συμβουλές για ανάγνωση σαρωμένων εγγράφων που περιέχουν πολλαπλές γλώσσες ή εικόνες χαμηλής ποιότητας.  
- Μια βάση που μπορείτε να επεκτείνετε σε PDF, PNG ή ακόμη και σε ροές κάμερας σε πραγματικό χρόνο.  

### Προαπαιτούμενα (το ελάχιστο)

- Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.  
- Maven ή Gradle (θα χρησιμοποιήσουμε Maven στο παράδειγμα, αλλά το ίδιο JAR λειτουργεί και με Gradle).  
- Μια εικόνα JPEG που θέλετε να δοκιμάσετε (ονομασμένη `sample.jpg` για απλότητα).  
- Άδεια Aspose OCR (η δωρεάν αξιολόγηση λειτουργεί άψογα για αυτήν την επίδειξη).  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε — θα σας δείξω τις ακριβείς εντολές που χρειάζεστε.

---

## αναγνώριση κειμένου από jpg – Ρύθμιση Aspose OCR

Πρώτα απ' όλα: χρειάζεται η βιβλιοθήκη Aspose OCR στο classpath σας. Ο πιο εύκολος τρόπος είναι να προσθέσετε την εξάρτηση Maven στο `pom.xml` σας.

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check the latest version on Maven Central -->
</dependency>
```

> **Συμβουλή:** Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι `implementation 'com.aspose:aspose-ocr:23.9'`.  

Μόλις το Maven ολοκληρώσει τη λήψη, είστε έτοιμοι να **φορτώσετε εικόνα για OCR** στον κώδικα Java σας.

---

## εξαγωγή κειμένου από εικόνα – Γράψιμο της Κύριας Κλάσης Java

Παρακάτω υπάρχει μια πλήρως εκτελέσιμη κλάση με όνομα `SimpleOcr`. Ακολουθεί ακριβώς τη ροή του αρχικού δείγματος κώδικα, αλλά με μερικά επιπλέον μέτρα ασφαλείας και σχόλια για να γίνει η λογική crystal clear.

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance – this is the heart of the process.
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image to be recognized.
        // Replace "YOUR_DIRECTORY/sample.jpg" with the real path to your JPEG.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Optional: tweak language or recognition mode if you know the source.
        // engine.setLanguage(OcrLanguage.English);
        // engine.setRecognitionMode(OcrRecognitionMode.Text);

        // Step 3: Perform the OCR operation.
        OcrResult result = engine.recognize();

        // Step 4: Retrieve and display the recognized plain‑text.
        System.out.println("=== OCR Output ===");
        System.out.println(result.getText());
    }
}
```

### Γιατί κάθε γραμμή είναι σημαντική

1. **`OcrEngine engine = new OcrEngine();`** – Δημιουργεί την μηχανή. Σκεφτείτε το σαν να ενεργοποιείτε το σαρωτή.  
2. **`engine.setImage(...)`** – Εδώ **φορτώνουμε εικόνα για OCR**. Η μέθοδος δέχεται ένα `ImageStream`, που μπορεί να προέρχεται από αρχείο, byte array ή ακόμη και από ροή δικτύου.  
3. **`engine.recognize();`** – Εκκινεί την βαριά δουλειά. Στο παρασκήνιο η Aspose εφαρμόζει προεπεξεργασία, τμηματοποίηση και ταξινόμηση χαρακτήρων.  
4. **`result.getText();`** – Επιστρέφει ένα `String` απλού κειμένου. Χωρίς XML, χωρίς PDF — μόνο τους χαρακτήρες που μπορείτε να στείλετε σε βάση δεδομένων ή σε ευρετήριο αναζήτησης.  

Συγκεντρώστε και τρέξτε:

```bash
mvn compile exec:java -Dexec.mainClass=SimpleOcr
```

Θα πρέπει να δείτε κάτι σαν:

```
=== OCR Output ===
Invoice #12345
Date: 2026-06-01
Total: $1,234.56
```

Αν η έξοδος φαίνεται ακατάληπτη, θα καλύψουμε αργότερα τα κόλπα **ανάγνωσης σαρωμένου εγγράφου**.

---

## μετατροπή εικόνας σε κείμενο – Βελτιστοποίηση για Καλύτερη Ακρίβεια

Οι προεπιλεγμένες ρυθμίσεις λειτουργούν για καθαρές, υψηλής ανάλυσης JPEG, αλλά οι πραγματικές σαρώσεις συχνά υποφέρουν από θόρυβο, κλίση ή ασυνήθιστα fonts. Εδώ είναι τρεις προσαρμογές που μπορείτε να κάνετε χωρίς να αγγίξετε τον κεντρικό κώδικα:

| Ρύθμιση | Τι κάνει | Πότε να το χρησιμοποιήσετε |
|---------|----------|----------------------------|
| `engine.setLanguage(OcrLanguage.English);` | Αναγκάζει τη μηχανή να ψάχνει μόνο για αγγλικά γλυφά, μειώνοντας τα ψευδώς θετικά. | Η εικόνα σας περιέχει μία μόνο γλώσσα. |
| `engine.setPreprocessingOptions(OcrPreprocessingOptions.AutoRotate);` | Αυτόματα περιστρέφει την εικόνα αν εντοπίσει κλίση. | Σαρωμένα έγγραφα που δεν είναι τέλεια οριζόντια. |
| `engine.setResolution(300);` | Ανεβάζει την ανάλυση της εικόνας στα 300 dpi πριν την αναγνώριση. | JPEG χαμηλής ανάλυσης (π.χ. στιγμιότυπα οθόνης). |

Προσθέστε οποιαδήποτε από αυτές τις γραμμές μετά τη φόρτωση της εικόνας και πριν το `recognize()`. Για παράδειγμα:

```java
engine.setResolution(300);
engine.setPreprocessingOptions(OcrPreprocessingOptions.AutoRotate);
engine.setLanguage(OcrLanguage.English);
```

Αυτές οι μικρορυθμίσεις βελτιώνουν άμεσα το βήμα **μετατροπής εικόνας σε κείμενο**, ειδικά όταν *διαβάζετε σαρωμένο έγγραφο* PDF που πρώτα αποθηκεύτηκε ως JPEG.

---

## φόρτωση εικόνας για ocr – Διαχείριση Διαφορετικών Πηγών Εισόδου

Μέχρι τώρα δείξαμε μια απλή φόρτωση από αρχείο. Η Aspose OCR, όμως, είναι αρκετά ευέλικτη ώστε να δέχεται ροές από μνήμη, URLs ή ακόμη και Android assets. Παρακάτω δύο κοινές εναλλακτικές:

### Από byte array (π.χ. όταν η εικόνα είναι αποθηκευμένη σε βάση δεδομένων)

```java
byte[] imageBytes = Files.readAllBytes(Paths.get("YOUR_DIRECTORY/sample.jpg"));
engine.setImage(ImageStream.fromByteArray(imageBytes));
```

### Απευθείας από URL (χρήσιμο για web services)

```java
URL imageUrl = new URL("https://example.com/sample.jpg");
engine.setImage(ImageStream.fromUrl(imageUrl));
```

Και οι δύο προσεγγίσεις ικανοποιούν την απαίτηση **φόρτωσης εικόνας για OCR**, επιτρέποντάς σας να ενσωματώσετε OCR σε REST endpoints ή batch jobs χωρίς να αγγίξετε το σύστημα αρχείων.

---

## ανάγνωση σαρωμένου εγγράφου – Διαχείριση Πολυ‑Σελίδων ή Χαμηλής Ποιότητας Αρχείων

Ένα σαρωμένο έγγραφο σπάνια είναι μια μοναδική, τέλεια εικόνα. Να πώς μπορείτε να επεκτείνετε το απλό παράδειγμα:

1. **Loop through pages** – Αν έχετε ένα πολυ‑σελίδες TIFF, χρησιμοποιήστε `ImageStream.fromFile("multi.tif")` και καλέστε `engine.recognize()` για κάθε δείκτη σελίδας.  
2. **Apply binarization** – Για σπασμένες σαρώσεις, καλέστε `engine.setBinarizationMethod(OcrBinarizationMethod.Otsu);` πριν την αναγνώριση.  
3. **Enable spell‑check** – Η Aspose μπορεί να κάνει post‑processing των αποτελεσμάτων με ενσωματωμένο λεξικό: `engine.setUseSpellChecker(true);`.  

Αυτές οι τεχνικές κάνουν τη διαφορά μεταξύ μιας χούφτας ακατανόητων χαρακτήρων και ενός καθαρού, αναζητήσιμου αποσπάσματος.

---

## Πλήρες Παράδειγμα End‑to‑End – Από Ρύθμιση Maven μέχρι Έξοδο Κονσόλας

Παρακάτω είναι η πλήρης δομή του έργου που μπορείτε να αντιγράψετε‑επικολλήσετε σε έναν φρέσκο φάκελο.

```
my-ocr-project/
├─ pom.xml
└─ src/
   └─ main/
      └─ java/
         └─ SimpleOcr.java
```

**pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.9</version>
        </dependency>
    </dependencies>
</project>
```

**SimpleOcr.java** – (ίδιο με το προηγούμενο απόσπασμα, με προαιρετικές βελτιώσεις)



## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [αναγνώριση κειμένου εικόνας με Aspose OCR – Πλήρης Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Πώς να OCR Κείμενο Εικόνας με Γλώσσα Χρησιμοποιώντας Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα Java με Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}