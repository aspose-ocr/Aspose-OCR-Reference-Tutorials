---
category: general
date: 2026-02-14
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Java. Μάθετε
  πώς να εξάγετε κείμενο από πεδία φόρμας με περιοχές ενδιαφέροντος για ακριβή αποτελέσματα.
draft: false
keywords:
- extract text from image
- extract text from form
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε Java.
  Αυτό το σεμινάριο δείχνει πώς να εξάγετε κείμενο από πεδία φόρμας μέσω περιοχών
  ενδιαφέροντος.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός Java
url: /el/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR – Οδηγός Java

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά καταλήξατε να αναλύετε ολόκληρη τη φωτογραφία, σπαταλώντας πόρους CPU και λαμβάνοντας θορυβώδη αποτελέσματα; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές—σκεφτείτε σαρωτές τιμολογίων, αναγνώστες διαβατηρίων ή φόρμες εισαγωγής δεδομένων—σας ενδιαφέρουν μόνο μερικά πεδία, όχι ολόκληρος ο καμβάς.  

Το καλό νέο είναι ότι το Aspose OCR σας επιτρέπει να **εξάγετε κείμενο από εικόνα** *και* από συγκεκριμένες περιοχές φόρμας ορίζοντας πολύγωνα. Σε αυτό το tutorial θα δείτε ακριβώς πώς να **εξάγετε κείμενο από πεδία φόρμας** χρησιμοποιώντας Java, γιατί η προσέγγιση είναι σημαντική και τι να ρυθμίσετε όταν κάτι πάει στραβά.

Παρακάτω θα καλύψουμε τα πάντα, από τη ρύθμιση της βιβλιοθήκης μέχρι την αντιμετώπιση δύσκολων περιπτώσεων, ώστε στο τέλος να έχετε ένα έτοιμο προς εκτέλεση απόσπασμα κώδικα που εξάγει μόνο τα δεδομένα που χρειάζεστε.

## Τι Θα Χρειαστεί

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) – οι νεότερες εκδόσεις έχουν καλύτερη υποστήριξη Unicode.  
- Aspose.OCR for Java 23.10 (ή η πιο πρόσφατη έκδοση τη στιγμή της ανάγνωσης).  
- Ένα δείγμα εικόνας με όνομα `form.png` που περιέχει σαφώς ορισμένα πεδία.  
- Ένα IDE ή απλός επεξεργαστής κειμένου—IntelliJ IDEA, VS Code, ή ακόμη και Notepad.

Δεν απαιτείται μαγεία Maven/Gradle για το βασικό demo· απλώς προσθέστε το Aspose OCR JAR στο classpath σας.

---

## Βήμα 1 – Αρχικοποίηση της Μηχανής OCR και Φόρτωση της Εικόνας

Το πρώτο που χρειάζεται η μηχανή είναι ένα bitmap για επεξεργασία. Θα το κατευθύνουμε στο `form.png`, το οποίο βρίσκεται στον ίδιο φάκελο με το αρχείο πηγαίου κώδικα.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Γιατί είναι σημαντικό:*  
Δημιουργώντας ένα νέο `OcrEngine` έχετε ένα καθαρό ξεκίνημα, εξασφαλίζοντας ότι δεν υπάρχουν παλιές ρυθμίσεις που να επηρεάζουν την εκτέλεση. Η πρόωρη φόρτωση της εικόνας επίσης επαληθεύει ότι το αρχείο υπάρχει, ώστε να λάβετε μια χρήσιμη εξαίρεση πριν σπαταλήσετε χρόνο σε επόμενα βήματα.

> **Συμβουλή:** Αν η εικόνα σας είναι τεράστια (πάνω από 5 MB), σκεφτείτε να την αλλάξετε μέγεθος πρώτα. Το Aspose OCR λειτουργεί πιο γρήγορα σε εικόνες κάτω από 2000 px σε οποιαδήποτε διάσταση.

---

## Βήμα 2 – Ορισμός Πολυγώνων για τα Πεδία που Θέλετε να Διαβάσετε

Μια *Περιοχή Ενδιαφέροντος* (ROI) είναι απλώς ένα πολύγωνο που λέει στη μηχανή πού να κοιτάξει. Παρακάτω δημιουργούμε δύο ορθογώνια—ένα για το “First Name” και ένα άλλο για το “Date of Birth”. Προσαρμόστε τις συντεταγμένες ώστε να ταιριάζουν στη δική σας φόρμα.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Γιατί πολύγωνα αντί για ορθογώνια;*  
Τα πολύγωνα σας δίνουν την ευελιξία να χειρίζεστε λοξά ή μη‑ορθογώνια κουτιά—συνηθισμένο όταν σκανάρετε έντυπες φόρμες που δεν είναι τέλεια ευθυγραμμισμένες.

---

## Βήμα 3 – Εντοπίστε στο Aspose OCR να Επικεντρωθεί Μόνο σε Αυτές τις Περιοχές

Τώρα συνδέουμε τα πολύγωνα με τη μηχανή. Η μέθοδος `setRegionsOfInterest` δέχεται μια λίστα, ώστε να μπορείτε να προσθέσετε όσα πεδία θέλετε.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Τι συμβαίνει στο παρασκήνιο;*  
Το Aspose OCR περικόπτει κάθε πολύγωνο σε ξεχωριστό bitmap, εκτελεί τον αλγόριθμο αναγνώρισης και στη συνέχεια ενώνει τα αποτελέσματα. Αυτό μειώνει δραστικά τα ψευδώς θετικά από τα γύρω γραφικά.

---

## Βήμα 4 – Εκτέλεση της Διαδικασίας OCR

Με όλα ρυθμισμένα, ξεκινάμε το OCR. Η κλήση `process()` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και τις βαθμολογίες εμπιστοσύνης.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Αν χρειάζεστε εμπιστοσύνη ανά πεδίο, μπορείτε να ελέγξετε το `ocrResult.getRegions()`—κάθε περιοχή φέρει τη δική της βαθμολογία. Για τις περισσότερες απλές φόρμες, το συνολικό κείμενο είναι επαρκές.

---

## Βήμα 5 – Εμφάνιση (ή Αποθήκευση) του Εξαγόμενου Κειμένου

Τέλος, εκτυπώνουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να γράψετε σε βάση δεδομένων, αρχείο JSON ή να το στείλετε μέσω API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Οι δύο γραμμές αντιστοιχούν στα δύο πολύγωνα που ορίσαμε. Αν δείτε επιπλέον κενά, αφαιρέστε τα με `String.trim()`.

---

## Πώς να Εξάγετε Κείμενο από Φόρμα όταν Έχετε Πολλά Πεδία

Όταν μια φόρμα περιέχει δεκάδες εισόδους, η χειροκίνητη πληκτρολόγηση των συντεταγμένων γίνεται κουραστική. Εδώ είναι ένα γρήγορο μοτίβο που μπορείτε να υιοθετήσετε:

1. **Δημιουργήστε ένα CSV** όπου κάθε γραμμή περιέχει `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Φορτώστε το CSV** κατά την εκτέλεση, κάντε βρόχο σε κάθε γραμμή, δημιουργήστε ένα `Polygon` και προσθέστε το στη λίστα ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Γιατί να ασχοληθείτε;*  
Η αυτοματοποίηση της δημιουργίας ROI σας επιτρέπει να επαναχρησιμοποιήσετε τον ίδιο κώδικα Java σε πολλαπλές διατάξεις φόρμας, διατηρώντας το project σας DRY (Don’t Repeat Yourself).

---

## Περιπτώσεις Άκρων & Συμβουλές που Μπορεί να Μην Έχετε Σκεφτεί

- **Περιστροφές σκαναρίσματος:** Αν ολόκληρη η εικόνα είναι περιστραμμένη, καλέστε `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Χαμηλή αντίθεση:** Ορίστε `ocrEngine.getEngineOptions().setContrast(1.5f)` για να βελτιώσετε την αναγνωσιμότητα.  
- **Μη‑λατινικά scripts:** Αλλάξτε τη γλώσσα με `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (ή οποιαδήποτε υποστηριζόμενη γλώσσα).  
- **Μερικές αποτυχίες OCR:** Πάντα ελέγχετε το `ocrResult.getConfidence()`· αν πέσει κάτω από 80 %, σκεφτείτε να ζητήσετε από τον χρήστη επαλήθευση χειροκίνητα.  

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση και εκτέλεση. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Μεταγλώττιση με:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Θα πρέπει να δείτε τις δύο γραμμές κειμένου που ανήκουν στις ορισμένες ROI.

---

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με PDFs;**  
A: Όχι άμεσα. Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ., χρησιμοποιώντας Aspose PDF) και μετά δώστε την εικόνα στη μηχανή OCR.

**Q: Τι γίνεται αν η φόρμα μου έχει κουτάκια ελέγχου;**  
A: Το OCR δεν μπορεί να διαβάσει boolean καταστάσεις, αλλά μπορείτε να θεωρήσετε την περιοχή του κουτιού ως ROI και να ελέγξετε την πυκνότητα των pixel για να καταλάβετε αν υπάρχει σημάδι.

**Q: Μπορώ να εξάγω κείμενο από μια πολύπλευρη φόρμα σε μία εκτέλεση;**  
A: Κάντε βρόχο σε κάθε εικόνα σελίδας, επαναχρησιμοποιήστε την ίδια λίστα ROI και συνενώστε τα αποτελέσματα.

---

## Συμπέρασμα

Διασχίσαμε μια πλήρη, ολοκληρωμένη λύση για **εξαγωγή κειμένου από εικόνα** χρησιμοποιώντας Aspose OCR, και δείξαμε πώς η ίδια τεχνική σας επιτρέπει να **εξάγετε κείμενο από πεδία φόρμας** με ακρίβεια. Ορίζοντας πολύγωνα, περιορίζοντας την εστίαση της μηχανής και αντιμετωπίζοντας κοινές παγίδες, λαμβάνετε γρήγορα, καθαρά δεδομένα χωρίς το βάρος της επεξεργασίας ολόκληρης της εικόνας.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδέσετε το αποτέλεσμα OCR σε ένα payload JSON, ή να το δώσετε σε μοντέλο μηχανικής μάθησης για επικύρωση. Ο ουρανός είναι το όριο, και τώρα εσείς

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}