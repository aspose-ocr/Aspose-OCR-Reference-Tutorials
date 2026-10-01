---
category: general
date: 2026-01-07
description: Αποκτήστε κείμενο OCR από μια εικόνα χρησιμοποιώντας το Aspose OCR Java.
  Μάθετε πώς να εξάγετε κείμενο από εικόνα, να φορτώσετε εικόνα OCR και να εκτελέσετε
  ένα παράδειγμα Java OCR σε λίγα λεπτά.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: el
og_description: Λάβετε κείμενο OCR από εικόνες με το Aspose OCR Java. Αυτός ο οδηγός
  παρουσιάζει ένα παράδειγμα OCR σε Java, πώς να εξάγετε κείμενο από εικόνα και πώς
  να φορτώνετε OCR εικόνας αποδοτικά.
og_title: Λάβετε κείμενο OCR σε Java – Πλήρης οδηγός Aspose OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Λήψη κειμένου OCR σε Java – Πλήρες παράδειγμα Aspose OCR
url: /el/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λήψη κειμένου OCR σε Java – Πλήρες Παράδειγμα Aspose OCR

Έχετε χρειαστεί ποτέ να **λάβετε κείμενο OCR** από ένα σαρωμένο έγγραφο αλλά δεν ήξερατε ποια βιβλιοθήκη να επιλέξετε; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα—π.χ. αυτοματοποίηση τιμολογίων, επεξεργασία αποδείξεων ή ψηφιοποίηση πολυγλωσσικών φορμών—η εξαγωγή κειμένου από εικόνες είναι το πρώτο βήμα προς την αυτοματοποίηση.

Σε αυτό το tutorial θα περάσουμε από ένα **java OCR example** που χρησιμοποιεί τη βιβλιοθήκη Aspose OCR for Java. Στο τέλος θα ξέρετε πώς να **φορτώσετε εικόνα OCR**, να εκτελέσετε τη μηχανή και να **εξάγετε κείμενο εικόνας** με λίγες μόνο γραμμές κώδικα. Χωρίς περιττές πληροφορίες, μόνο μια πρακτική λύση που μπορείτε να αντιγράψετε‑επικολλήσετε στο δικό σας έργο.

## Τι θα μάθετε

- Πώς να ρυθμίσετε το Aspose OCR for Java (συμπεριλαμβανομένων των συντεταγμένων Maven).  
- Τα ακριβή βήματα για **φόρτωση εικόνας OCR** και ορισμό γλώσσας.  
- Πώς να **λάβείμενο OCR** ως απλό string και να το εκτυπώσετε στην κονσόλα.  
- Συμβουλές για διαχείριση πολυγλωσσικών εικόνων και αυτόματη ανίχνευση γλωσσών.  

*Προαπαιτούμενα*: Java 8 ή νεότερη, IDE συμβατό με Maven (IntelliJ IDEA, Eclipse ή VS Code) και έγκυρη άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση).

---

![Διάγραμμα ροής που δείχνει πώς να λάβετε κείμενο OCR από μια εικόνα χρησιμοποιώντας το Aspose OCR Java](https://example.com/ocr-flowchart.png "Διάγραμμα ροής λήψης κειμένου OCR")

## Βήμα 1 – Προσθήκη εξάρτησης Aspose OCR (Φόρτωση εικόνας OCR)

Πρώτα, πείτε στο Maven να κατεβάσει τη βιβλιοθήκη Aspose OCR. Ανοίξτε το `pom.xml` και προσθέστε το παρακάτω μπλοκ `<dependency>` μέσα στο `<dependencies>`:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip**: Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι `implementation 'com.aspose:aspose-ocr:23.9'`. Η προσθήκη της εξάρτησης είναι ο πιο οικονομικός τρόπος για **φόρτωση εικόνας OCR** στο έργο σας.

## Βήμα 2 – Δημιουργία της μηχανής OCR και φόρτωση της εικόνας σας

Τώρα θα γράψουμε μια μικρή κλάση Java που δημιουργεί ένα αντικείμενο `OcrEngine`, το κατευθύνει σε ένα αρχείο εικόνας και ορίζει τη γλώσσα που θα αναγνωριστεί. Η γλώσσα προσδιορίζεται με τον κωδικό ISO‑639‑2 (π.χ. `"tam"` για ταμίλ).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Γιατί να ορίσετε ρητά τη γλώσσα;

Ο καθορισμός της γλώσσας μειώνει τα ψευδώς θετικά και επιταχύνει την αναγνώριση. Για πολυγλωσσικά PDF μπορείτε να κάνετε βρόχο πάνω σε έναν πίνακα κωδικών γλώσσας ή να ενεργοποιήσετε την αυτόματη ανίχνευση για ευκολία.

## Βήμα 3 – Εκτέλεση της διαδικασίας OCR και **Λήψη κειμένου OCR**

Με τη μηχανή ρυθμισμένη, η επόμενη γραμμή εκτελεί πραγματικά την αναγνώριση. Το αντικείμενο αποτελέσματος περιέχει το εξαγόμενο string και πρόσθετα μεταδεδομένα.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Όταν τρέξετε το `LanguageExample`, θα δείτε κάτι σαν:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

Αν χρησιμοποιήσατε `setAutoDetectLanguage(true)`, η μηχανή θα προσπαθήσει να μαντέψει τη γλώσσα για εσάς, κάτι που είναι χρήσιμο όταν αντιμετωπίζετε άγνωστα έγγραφα.

## Βήμα 4 – Διαχείριση Συνηθισμένων Περιπτώσεων (Διαφορετικές Παραλλαγές Εξαγωγής Κειμένου Εικόνας)

### Αντιμετώπιση εικόνων χαμηλής ανάλυσης

Η ακρίβεια του OCR πέφτει δραματικά κάτω από 300 dpi. Αν η πηγή σας είναι χαμηλής ανάλυσης, σκεφτείτε να την αυξήσετε πρώτα:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Αφαίρεση θορύβου φόντου

Μερικές φορές τα σαρωμένα έντυπα έχουν στίγματα που μπερδεύουν τη μηχανή. Μπορείτε να ενεργοποιήσετε προεπεξεργασία:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Εξαγωγή κειμένου από συγκεκριμένες περιοχές

Αν χρειάζεστε κείμενο μόνο από ένα συγκεκριμένο ορθογώνιο (π.χ. ένα κελί πίνακα), ορίστε ένα `Rectangle` πριν καλέσετε το `recognize()`:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Αυτές οι προσαρμογές κάνουν το **java OCR example** σας ανθεκτικό για παραγωγικά φορτία.

## Βήμα 5 – Επαλήθευση του αποτελέσματος (Τι πρέπει να περιμένετε;)

Μια επιτυχής εκτέλεση θα εκτυπώσει την απλή κειμενική έκδοση της εικόνας. Για πολυγλωσσικές εικόνες μπορεί να δείτε μεικτά αλφάβητα:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Αν το αποτέλεσμα είναι κενό ή ακατανόητο, ελέγξτε:

1. Το μονοπάτι αρχείου στο `setImage` (είναι σωστό;).  
2. Ο κωδικός γλώσσας ταιριάζει με το αλφάβητο της εικόνας.  
3. Η ποιότητα της εικόνας (αντίθεση, DPI) είναι επαρκής.

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το αρχείο, έτοιμο για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY/multilingual.png` με το πραγματικό μονοπάτι της δοκιμαστικής σας εικόνας.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Τώρα θα δείτε το εξαγόμενο περιεχόμενο στην κονσόλα σας.

---

## Συμπέρασμα

Σας δείξαμε πώς να **λάβετε κείμενο OCR** από μια εικόνα χρησιμοποιώντας το Aspose OCR for Java. Ακολουθώντας αυτό το **java OCR example**, μπορείτε να **εξάγετε κείμενο εικόνας**, **φορτώσετε εικόνα OCR** και ακόμη να ρυθμίσετε τη μηχανή για πολυγλωσσικές ή θορυβώδεις εισόδους.  

Από εδώ μπορείτε:

- Να ενσωματώσετε το βήμα OCR σε μεγαλύτερη ροή εργασίας (π.χ. αποθήκευση του κειμένου σε βάση δεδομένων).  
- Να το συνδυάσετε με API μετάφρασης για να μετατρέψετε πολυγλωσσικές σάρωση σε μία γλώσσα.  
- Να πειραματιστείτε με άλλες δυνατότητες του Aspose OCR όπως μετατροπή PDF ή ανίχνευση barcode.

Δοκιμάστε το, σπάστε μερικά πράγματα και στη συνέχεια βελτιώστε τις ρυθμίσεις μέχρι το αποτέλεσμα να είναι τέλειο. Καλή προγραμματιστική, και εύχομαι το OCR σας πάντα να είναι crystal clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}