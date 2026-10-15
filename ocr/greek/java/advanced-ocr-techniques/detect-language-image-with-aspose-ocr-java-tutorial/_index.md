---
category: general
date: 2026-02-14
description: Ανίχνευση γλώσσας εικόνας με χρήση Aspose OCR σε Java – μάθετε πώς να
  εξάγετε κείμενο από εικόνα, να μετατρέψετε εικόνα OCR σε κείμενο και να διαβάσετε
  κείμενο PNG ενώ λαμβάνετε τη ανιχνευμένη γλώσσα.
draft: false
keywords:
- detect language image
- extract text image
- ocr image to text
- read text png
- get detected language
language: el
og_description: Ανίχνευση γλώσσας εικόνας χρησιμοποιώντας Aspose OCR σε Java. Μάθετε
  πώς να εξάγετε κείμενο από εικόνα, OCR εικόνας σε κείμενο, να διαβάζετε κείμενο
  PNG και να λαμβάνετε τη ανιχνευμένη γλώσσα σε λίγα λεπτά.
og_title: Ανίχνευση γλώσσας σε εικόνα με Aspose OCR – Java Tutorial
tags:
- OCR
- Java
- Aspose
title: Ανίχνευση γλώσσας εικόνας με Aspose OCR – Εγχειρίδιο Java
url: /el/java/advanced-ocr-techniques/detect-language-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ανίχνευση γλώσσας εικόνας με Aspose OCR – Java Tutorial

Ποτέ χρειάστηκε να **ανιχνεύσετε τη γλώσσα εικόνας** αλλά δεν ήξερες ποια βιβλιοθήκη μπορεί να το κάνει αυτόματα; Δεν είσαι μόνος—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν μια μόνο εικόνα περιέχει κείμενο σε πολλές γλώσσες.  

Σε αυτόν τον οδηγό θα δείξουμε, βήμα‑βήμα, πώς να χρησιμοποιήσετε το Aspose OCR για Java για **ανίχνευση γλώσσας εικόνας**, **εξαγωγή κειμένου από εικόνα**, και πώς να μετατρέψετε το PNG σε αναζητήσιμο κείμενο. Στο τέλος θα μπορείτε να **ocr image to text**, **read text png**, και ακόμη **get detected language** χωρίς να γράψετε προσαρμοσμένο μοντέλο ML.

## Τι θα μάθετε

- Πώς να δημιουργήσετε και να διαμορφώσετε μια παρουσία `OcrEngine`.
- Ενεργοποίηση αυτόματης ανίχνευσης γλώσσας ώστε η μηχανή να επιλέγει το σωστό σύστημα γραφής.
- Εξαγωγή του κειμένου από ένα PNG πολλαπλών γλωσσών.
- Ανάκτηση του κωδικού γλώσσας που εντόπισε το Aspose.
- Συνηθισμένα προβλήματα (π.χ. θολές εικόνες) και συμβουλές για βελτίωση της ακρίβειας.

**Προαπαιτούμενα**  
Ένα JDK Java 17+ , Maven ή Gradle, και άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για demos). Δεν απαιτούνται άλλα τρίτα εργαλεία OCR.

---

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή του Aspose OCR

Πρώτα, προσθέστε την εξάρτηση Aspose OCR στο `pom.xml` (Maven) ή στο `build.gradle` (Gradle). Ακολουθεί το απόσπασμα Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

Αν προτιμάτε Gradle:

```gradle
// build.gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** Κρατήστε τη βιβλιοθήκη ενημερωμένη· οι νεότερες εκδόσεις βελτιώνουν την πολυγλωσσική ανίχνευση.

Τώρα δημιουργήστε μια απλή κλάση Java με όνομα `AutoLangDemo`. Αυτό το αρχείο θα περιέχει το πλήρες εκτελέσιμο παράδειγμα.

---

## Βήμα 2: Αρχικοποίηση της μηχανής OCR (ανίχνευση γλώσσας εικόνας)

Το πρώτο που κάνετε είναι να δημιουργήσετε ένα αντικείμενο `OcrEngine`. Αυτό το αντικείμενο είναι η καρδιά της λειτουργίας **ανίχνευση γλώσσας εικόνας**.

```java
import com.aspose.ocr.*;

public class AutoLangDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the image that contains multiple languages
        String imagePath = "YOUR_DIRECTORY/multilang.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 2.3: Enable automatic language detection
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 2.4: Perform OCR processing on the image
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the detected language and extracted text
        System.out.println("Detected language: " + ocrResult.getDetectedLanguage());
        System.out.println(ocrResult.getText());
    }
}
```

Παρατηρήστε πώς το σχόλιο `// Step 2.3` αναφέρει *automatic language detection*—αυτή είναι η γραμμή που κάνει τη μηχανή **detect language image** χωρίς να χρειάζεται να καθορίσετε κωδικό γλώσσας χειροκίνητα.

---

## Βήμα 3: Εκτέλεση του demo και επαλήθευση του αποτελέσματος (εξαγωγή κειμένου από εικόνα)

Συγκεντρώστε και εκτελέστε το πρόγραμμα:

```bash
mvn compile exec:java -Dexec.mainClass=AutoLangDemo
```

Αν όλα είναι ρυθμισμένα σωστά, θα δείτε κάτι όπως:

```
Detected language: en
Hello World!
Bonjour le monde!
Hola Mundo!
```

Η κονσόλα εκτυπώνει τη **detected language** (`en` για Αγγλικά) ακολουθούμενη από το αποτέλεσμα **extract text image**. Στην πράξη, ο κωδικός γλώσσας μπορεί να είναι `fr`, `es`, `de`, κ.λπ., ανάλογα με το κυρίαρχο σύστημα γραφής.

> **Γιατί λειτουργεί:** Το Aspose OCR σαρώνει το bitmap, αξιολογεί τα σύνολα χαρακτήρων, και επιλέγει τη πιο πιθανή γλώσσα από το ενσωματωμένο λεξικό του. Ορίζοντας `OcrLanguage.AUTO_DETECT`, αφήνετε τη μηχανή να κάνει το δύσκολο έργο.

---

## Βήμα 4: Διαχείριση ειδικών περιπτώσεων – Όταν η ανίχνευση αποτυγχάνει

Ακόμη και οι καλύτερες μηχανές OCR δυσκολεύονται με εικόνες χαμηλής ανάλυσης ή θορυβώδεις PNG. Εδώ είναι μερικά κόλπα για βελτίωση της αξιοπιστίας:

| Πρόβλημα | Διόρθωση |
|----------|----------|
| **Θολή εικόνα** | Προεπεξεργασία με `java.awt` για μεγέθυνση (`BufferedImage.getScaledInstance`) ή εφαρμογή φίλτρου ακονισμού. |
| **Μικτές γλώσσες στην ίδια σελίδα** | Καλείτε `ocrEngine.process()` σε κάθε περιοχή ξεχωριστά χρησιμοποιώντας `ocrEngine.setRegion(Rectangle)`. |
| **Μη υποστηριζόμενο σύστημα γραφής** | Ορίστε ρητά `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.<YOUR_LANG>)` ως εναλλακτική. |

Αυτές οι προτάσεις διατηρούν το **ocr image to text** pipeline σας αξιόπιστο, ειδικά όταν χρειάζεται να **read text png** αρχεία που προέρχονται από σαρωμένες αποδείξεις ή στιγμιότυπα οθόνης.

---

## Βήμα 5: Αποθήκευση του εξαγόμενου κειμένου (read text png)  

Συχνά θέλετε να αποθηκεύσετε το αποτέλεσμα OCR σε αρχείο για μετέπειτα επεξεργασία. Το παρακάτω απόσπασμα γράφει την έξοδο στο `output.txt`:

```java
import java.nio.file.*;

Path outPath = Paths.get("output.txt");
Files.writeString(outPath, ocrResult.getText(), StandardOpenOption.CREATE);
System.out.println("Text saved to " + outPath.toAbsolutePath());
```

Τώρα όχι μόνο **detect language image** και **extract text image**, αλλά έχετε και ένα μόνιμο αντίγραφο που μπορείτε να τροφοδοτήσετε σε ευρετήρια αναζήτησης, APIs μετάφρασης ή pipelines δεδομένων.

---

## Πλήρες λειτουργικό παράδειγμα (Όλα τα βήματα συνδυασμένα)

Παρακάτω είναι ο πλήρης, έτοιμος‑για‑εκτέλεση κώδικας. Αντιγράψτε‑και‑επικολλήστε το στο `src/main/java/AutoLangDemo.java` και εκτελέστε.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class AutoLangDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load multi‑language PNG (replace with your actual path)
        String imagePath = "YOUR_DIRECTORY/multilang.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // 3️⃣ Auto‑detect language – this is the heart of detect language image
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.AUTO_DETECT);

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // 5️⃣ Show detected language and extracted text
        System.out.println("Detected language: " + ocrResult.getDetectedLanguage());
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());

        // 6️⃣ Persist the text (optional)
        Path outPath = Paths.get("output.txt");
        Files.writeString(outPath, ocrResult.getText(), StandardOpenOption.CREATE);
        System.out.println("Saved extracted text to " + outPath.toAbsolutePath());
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Detected language: fr
=== Extracted Text ===
Bonjour le monde!
Hello World!
¡Hola Mundo!
```

Ο ακριβής κωδικός γλώσσας θα διαφέρει ανάλογα με το περιεχόμενο της εικόνας, αλλά το μοτίβο παραμένει το ίδιο.

---

## Συχνές ερωτήσεις

**Ε: Λειτουργεί αυτό με αρχεία JPEG ή BMP;**  
Α: Απόλυτα. Το Aspose OCR υποστηρίζει PNG, JPEG, BMP, TIFF, και GIF. Απλώς αλλάξτε την επέκταση αρχείου στο `imagePath`.

**Ε: Μπορώ να ανιχνεύσω περισσότερες από μία γλώσσες στην ίδια εικόνα;**  
Α: Ναι. Η μηχανή επιστρέφει τη *πρωτεύουσα* γλώσσα, αλλά μπορείτε να καλέσετε `ocrEngine.process()` σε ξεχωριστές περιοχές για να καταγράψετε κάθε σύστημα γραφής ξεχωριστά.

**Ε: Τι γίνεται αν η εικόνα περιέχει χειρόγραφο κείμενο;**  
Α: Η τρέχουσα μηχανή Aspose OCR διαπρέπει με τυπωμένες γραμματοσειρές. Το χειρόγραφο κείμενο μπορεί να απαιτεί εξειδικευμένο μοντέλο (π.χ., Azure Cognitive Services) – αυτό είναι διαφορετική περίπτωση χρήσης.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, ολοκληρωμένη συνταγή για **detect language image**, **extract text image**, και **ocr image to text** χρησιμοποιώντας το Aspose OCR για Java. Ενεργοποιώντας το `OcrLanguage.AUTO_DETECT` αφήνετε τη βιβλιοθήκη να **get detected language** αυτόματα, και με λίγες επιπλέον γραμμές μπορείτε να **read text png**, να αποθηκεύσετε το αποτέλεσμα και να αντιμετωπίσετε κοινές ειδικές περιπτώσεις.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε το εξαγόμενο κείμενο στο API του Google Translate, ή να το ευρετηριάσετε με Elasticsearch για αναζητήσιμα PDF. Μπορείτε επίσης να πειραματιστείτε με επεξεργασία παρτίδας—να κάνετε βρόχο πάνω σε έναν φάκελο PNG και να γράφετε κάθε αποτέλεσμα σε δικό του αρχείο `.txt`.

Καλό κώδικα, και να είναι πάντα ακριβή τα OCR pipelines σας!  

---

![detect language image example](detect-language-image.png "παράδειγμα ανίχνευσης γλώσσας εικόνας")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}