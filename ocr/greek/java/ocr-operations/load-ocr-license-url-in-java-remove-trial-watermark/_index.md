---
category: general
date: 2026-06-28
description: Φορτώστε τη διεύθυνση URL της άδειας OCR σε Java και αφαιρέστε το υδατογράφημα
  δοκιμής με ένα απλό παράδειγμα κώδικα. Μάθετε βήμα‑βήμα πώς να εφαρμόσετε μια απομακρυσμένη
  άδεια Aspose OCR.
draft: false
keywords:
- load OCR license URL
- remove trial watermark
- Aspose OCR Java
- remote license loading
- Java OCR setup
language: el
og_description: Φορτώστε τη διεύθυνση URL της άδειας OCR σε Java για να αφαιρέσετε
  το υδατογράφημα δοκιμής. Ακολουθήστε αυτόν τον πλήρη οδηγό για την αδειοδότηση του
  Aspose OCR.
og_title: Φόρτωση URL άδειας OCR σε Java – Αφαίρεση υδατογραφήματος δοκιμής
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Load OCR license URL in Java and remove trial watermark with a simple
    code example. Learn step‑by‑step how to apply a remote Aspose OCR license.
  headline: Load OCR License URL in Java – Remove Trial Watermark
  type: TechArticle
- description: Load OCR license URL in Java and remove trial watermark with a simple
    code example. Learn step‑by‑step how to apply a remote Aspose OCR license.
  name: Load OCR License URL in Java – Remove Trial Watermark
  steps:
  - name: Setting up the Aspose OCR library in a Maven/Gradle project.
    text: Setting up the Aspose OCR library in a Maven/Gradle project.
  - name: Loading the OCR license from a remote URL (the **load OCR license URL**
      part).
    text: Loading the OCR license from a remote URL (the **load OCR license URL**
      part).
  - name: Disabling trial mode to **remove trial watermark**.
    text: Disabling trial mode to **remove trial watermark**.
  - name: Instantiating the `OcrEngine` and performing a quick test scan.
    text: Instantiating the `OcrEngine` and performing a quick test scan.
  - name: The URL is correct and returns the exact `.lic` file (no redirects to an
      HTML page).
    text: The URL is correct and returns the exact `.lic` file (no redirects to an
      HTML page).
  - name: The license file matches the product version you’re using.
    text: The license file matches the product version you’re using.
  - name: '`setTrialMode(false)` was called *after* `fromUrl`.'
    text: '`setTrialMode(false)` was called *after* `fromUrl`.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Φόρτωση URL άδειας OCR σε Java – Αφαίρεση υδατογραφήματος δοκιμής
url: /el/java/ocr-operations/load-ocr-license-url-in-java-remove-trial-watermark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση URL Άδειας OCR σε Java – Αφαίρεση Υδατογράφησης Δοκιμής

Έχετε ποτέ χρειαστεί να **φορτώσετε το URL άδειας OCR** σε ένα έργο Java, αλλά συνεχίζετε να βλέπετε εκείνη την ενοχλητική υδατογράφημα δοκιμής σε κάθε έξοδο; Δεν είστε ο μόνος. Σε πολλές επιχειρηματικές περιπτώσεις η υδατογράφημα δεν φαίνεται μόνο μη επαγγελματική—μπορεί ακόμη και να διακόψει τις επόμενες διαδικασίες.

Τα καλά νέα; Με λίγες γραμμές κώδικα μπορείτε να κατεβάσετε την άδεια Aspose OCR από ένα ασφαλές HTTPS endpoint και να **αφαιρέσετε την υδατογράφημα δοκιμής** μια και για πάντα. Παρακάτω θα βρείτε ένα έτοιμο‑για‑εκτέλεση παράδειγμα, καθώς και το «γιατί» πίσω από κάθε βήμα, ώστε να μην μείνετε με απορίες αργότερα.

## Τι Καλύπτει Αυτό το Σεμινάριο

Θα περάσουμε από:

1. Ρύθμιση της βιβλιοθήκης Aspose OCR σε έργο Maven/Gradle.  
2. Φόρτωση της άδειας OCR από απομακρυσμένο URL (το τμήμα **load OCR license URL**).  
3. Απενεργοποίηση της λειτουργίας δοκιμής για **remove trial watermark**.  
4. Δημιουργία ενός αντικειμένου `OcrEngine` και εκτέλεση γρήγορης δοκιμαστικής σάρωσης.  

Δεν απαιτείται εξωτερική τεκμηρίωση—όλα όσα χρειάζεστε είναι εδώ. Στο τέλος θα έχετε μια καθαρή, χωρίς υδατογράφημα, γραμμή OCR που μπορείτε να ενσωματώσετε σε οποιαδήποτε υπηρεσία Java.  

*Προαπαιτούμενα*: Java 8+, περιβάλλον κατασκευής Maven ή Gradle, και ένα έγκυρο αρχείο άδειας Aspose OCR που φιλοξενείται σε διακομιστή HTTPS (π.χ., `https://yourcompany.com/licenses/asp-ocr.lic`). Αν δεν έχετε ακόμη άδεια, μπορείτε να ζητήσετε δοκιμαστική από την ιστοσελίδα της Aspose—απλώς θυμηθείτε να την αντικαταστήσετε με την παραγωγική άδεια αργότερα.

---

## Βήμα 1: Προσθήκη Εξάρτησης Aspose OCR

Πρώτα, βεβαιωθείτε ότι το JAR της Aspose OCR βρίσκεται στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Για Gradle, έχει ως εξής:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Συμβουλή:** Παρακολουθήστε τον αριθμό έκδοσης· οι νεότερες εκδόσεις συχνά περιλαμβάνουν διορθώσεις σφαλμάτων για τη διαχείριση αδειών.

---

## Βήμα 2: **Load OCR License URL** – Λήψη της Άδειας από το Cloud

Τώρα έρχεται ο πυρήνας του σεμιναρίου. Θα δημιουργήσουμε ένα αντικείμενο `License` και θα του δώσουμε ένα απομακρυσμένο URL. Αυτό είναι το ακριβές σημείο όπου εκτελείται η ενέργεια **load OCR license URL**.

```java
import com.aspose.ocr.*;

public class CloudLicenseDemo {
    public static void main(String[] args) throws Exception {
        // 2.1: Initialize the License object
        License license = new License();

        // 2.2: Load the license from a secure HTTPS location
        // Replace the URL with the actual path to your .lic file
        license.fromUrl("https://yourcompany.com/licenses/asp-ocr.lic");

        // 2.3: Turn off trial mode – this is what actually **remove trial watermark**
        license.setTrialMode(false);

        // 2.4: Create the OCR engine – ready for real work
        OcrEngine ocrEngine = new OcrEngine();

        // 2.5: Quick sanity check – run OCR on a sample image
        ocrEngine.setImage("sample.png");
        if (ocrEngine.process()) {
            System.out.println("OCR succeeded, output:");
            System.out.println(ocrEngine.getText());
        } else {
            System.err.println("OCR failed – check the license and image path.");
        }
    }
}
```

### Γιατί Λειτουργεί Αυτό

* `License.fromUrl(...)` επικοινωνεί με τον απομακρυσμένο διακομιστή, κατεβάζει το αρχείο `.lic` και το επικυρώνει με το δημόσιο κλειδί του προϊόντος. Εφόσον το URL είναι προσβάσιμο μέσω **HTTPS**, η σύνδεση είναι κρυπτογραφημένη και ασφαλής από επιθέσεις man‑in‑the‑middle.  
* `setTrialMode(false)` λέει στην Aspose να αντιμετωπίζει την άδεια ως πλήρη. Αν παραλείψετε αυτήν την κλήση, η βιβλιοθήκη υποθέτει ότι είναι δοκιμαστική και προσθέτει αυτόματα τη λογική **remove trial watermark**—δηλαδή θα συνεχίσετε να βλέπετε την υδατογράφημα παρόλο που το αρχείο άδειας υπάρχει.

> **Περίπτωση άκρης:** Ορισμένα εταιρικά τείχη προστασίας (firewalls) μπλοκάρουν εξωτερικές κλήσεις HTTPS. Αν αντιμετωπίσετε `java.net.ConnectException`, σκεφτείτε να φιλοξενήσετε την άδεια σε εσωτερικό διακομιστή ή να την ενσωματώσετε στο JAR σας και να χρησιμοποιήσετε `license.setLicense("aspose.lic")` αντί αυτού.

---

## Βήμα 3: Επαλήθευση ότι η Υδατογράφημα Έχει Απενεργοποιηθεί

Μια γρήγορη δοκιμή είναι ο καλύτερος τρόπος να επιβεβαιώσετε ότι έχετε πράγματι **remove trial watermark**. Εκτελέστε το πρόγραμμα με μια γνωστή εικόνα που περιέχει ορατό κείμενο. Αν η άδεια είναι ενεργή, η έξοδος θα είναι καθαρή και δεν θα εμφανιστεί το κείμενο “Aspose OCR – Trial Version” στην εικόνα ή στην κονσόλα.

**Αναμενόμενη έξοδος κονσόλας (όταν είναι επιτυχές):**

```
OCR succeeded, output:
Hello, World!
```

Αν εξακολουθείτε να βλέπετε υδατογράφημα, ελέγξτε ξανά:

1. Το URL είναι σωστό και επιστρέφει το ακριβές αρχείο `.lic` (χωρίς ανακατευθύνσεις σε σελίδα HTML).  
2. Το αρχείο άδειας ταιριάζει με την έκδοση του προϊόντος που χρησιμοποιείτε.  
3. `setTrialMode(false)` κλήθηκε *μετά* το `fromUrl`.  

---

## Βήμα 4: Συμβουλές για Παραγωγική Χρήση & Συχνά Προβλήματα

| Κατάσταση | Τι να κάνετε |
|-----------|------------|
| **License expires** | Παρακολουθήστε την ημερομηνία λήξης της `License` (διαθέσιμη μέσω `license.getExpirationDate()`) και αυτοματοποιήστε τις ειδοποιήσεις ανανέωσης. |
| **Network latency** | Αποθηκεύστε την άδεια τοπικά μετά την πρώτη λήψη για να αποφύγετε επαναλαμβανόμενες κλήσεις HTTP. |
| **Multiple JVMs** | Φορτώστε την άδεια μία φορά ανά JVM· οι επόμενες κλήσεις είναι φθηνές αλλά περιττές. |
| **Running in Docker** | Βεβαιωθείτε ότι το κοντέινερ μπορεί να φτάσει στο HTTPS endpoint· προσθέστε το εταιρικό CA στο Java trust store αν χρειάζεται. |
| **File not found** | Χρησιμοποιήστε απόλυτα URLs και βεβαιωθείτε ότι ο διακομιστής επιστρέφει `200 OK` με `application/octet-stream`. |

---

## Βήμα 5: Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Ακολουθεί το τελικό, έτοιμο για αντιγραφή‑επικόλληση πρόγραμμα που ενσωματώνει όλες τις συστάσεις από αυτόν τον οδηγό:

```java
import com.aspose.ocr.*;

public class CloudLicenseDemo {
    public static void main(String[] args) {
        try {
            // ---------- Load OCR license from a remote URL ----------
            License license = new License();
            // Make sure the URL points directly to the .lic file and uses HTTPS
            license.fromUrl("https://yourcompany.com/licenses/asp-ocr.lic");
            // Disable trial mode – this is the key to **remove trial watermark**
            license.setTrialMode(false);

            // ---------- Initialize OCR engine ----------
            OcrEngine ocrEngine = new OcrEngine();

            // ---------- Optional: set language, DPI, etc. ----------
            ocrEngine.getLanguage().setLanguage(Language.English);
            ocrEngine.getImageProperties().setResolution(300);

            // ---------- Perform a quick OCR test ----------
            ocrEngine.setImage("sample.png"); // replace with your image path
            if (ocrEngine.process()) {
                System.out.println("OCR succeeded, output:");
                System.out.println(ocrEngine.getText());
            } else {
                System.err.println("OCR failed – verify the license and image.");
            }
        } catch (Exception e) {
            // ---------- Robust error handling ----------
            System.err.println("An error occurred while loading the OCR license or processing the image:");
            e.printStackTrace();
        }
    }
}
```

**Τρέξτε το:** `mvn compile exec:java -Dexec.mainClass=CloudLicenseDemo` (ή την αντίστοιχη εντολή Gradle). Αν όλα έχουν ρυθμιστεί σωστά, θα δείτε το κείμενο OCR να εκτυπώνεται χωρίς καμία υδατογράφημα δοκιμής να εμφανίζεται.

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **load OCR license URL** σε Java και να **remove trial watermark** με λίγες μόνο γραμμές κώδικα. Με τη λήψη της άδειας από μια ασφαλή απομακρυσμένη θέση, την απενεργοποίηση της λειτουργίας δοκιμής και την αρχικοποίηση του `OcrEngine`, αποκτάτε μια γραμμή OCR επιπέδου παραγωγής έτοιμη για ενσωμάτωση σε μικρο‑υπηρεσίες, εργασίες batch ή εφαρμογές επιφάνειας εργασίας.

Επόμενα βήματα; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με PDFs μέσω `PdfInput`, πειραματιστείτε με διαφορετικά πακέτα γλωσσών, ή δημιουργήστε ένα REST endpoint που δέχεται εικόνες και επιστρέφει απλό κείμενο—όπως προτιμάτε. Και θυμηθείτε, η διατήρηση της άδειας ενημερωμένης και η ομαλή διαχείριση των προβλημάτων δικτύου θα σας εξοικονομήσει προβλήματα στο μέλλον.

Καλή προγραμματιστική δουλειά, και εύχομαι τα αποτελέσματα OCR σας να παραμένουν καθαρά και χωρίς υδατογράφημα!

## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Ορίσετε Άδεια και να Επαληθεύσετε την Άδεια Aspose.OCR σε Java](/ocr/english/java/ocr-basics/set-license/)
- [Πώς να εξάγετε κείμενο από εικόνα μέσω URL χρησιμοποιώντας Aspose.OCR για Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)
- [Υπολογισμός κλίσης με Aspose OCR Java – Πλήρης οδηγός](/ocr/swedish/java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}