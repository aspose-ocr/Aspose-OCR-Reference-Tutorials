---
category: general
date: 2026-05-25
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης σε Java χρησιμοποιώντας το
  Aspose OCR. Μάθετε πώς να μετατρέπετε PDF σε PDF με δυνατότητα αναζήτησης, να φορτώνετε
  PDF για OCR και να επιταχύνετε με GPU.
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF σε Java χρησιμοποιώντας το Aspose OCR.
  Αυτό το σεμινάριο δείχνει πώς να μετατρέψετε PDF σε αναζητήσιμο PDF, να φορτώσετε
  PDF για OCR και να χρησιμοποιήσετε επιτάχυνση GPU.
og_title: Δημιουργία Αναζητήσιμου PDF με Java OCR – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: Δημιουργία Αναζητήσιμου PDF με Java OCR – Πλήρης Οδηγός
url: /el/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Java OCR – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από σαρωμένα έγγραφα αλλά δεν ήξερτε από πού να ξεκινήσετε; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να μετατρέψουν PDF μόνο με εικόνες σε περιουσιακά στοιχεία με δυνατότητα αναζήτησης κειμένου, ειδικά όταν η απόδοση μετρά.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που **δημιουργεί αναζητήσιμο PDF** χρησιμοποιώντας το Aspose OCR για Java. Θα σας δείξουμε επίσης πώς να **μετατρέψετε PDF σε αναζητήσιμο PDF**, **φορτώσετε PDF για OCR**, και ακόμη **OCR PDF με επιτάχυνση GPU** — όλα σε ένα ενιαίο, εύκολο‑ανάγνωστο script. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα και μια σαφή κατανόηση του γιατί κάθε βήμα είναι σημαντικό.

> **Τι θα αποκτήσετε**  
> * Ένα πλήρες Java project που διαβάζει ένα PDF πολλαπλών γλωσσών  
> * OCR με υποστήριξη GPU που επιταχύνει την επεξεργασία σε σύγχρονο υλικό  
> * Έξοδο αναζητήσιμου PDF που μπορείτε να ενσωματώσετε σε οποιοδήποτε σύστημα διαχείρισης εγγράφων  

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 17 (ή νεότερη) εγκατεστημένη – οι παλαιότερες εκδόσεις μπορεί να λείπουν απαιτούμενα APIs.  
* Maven ή Gradle για διαχείριση εξαρτήσεων – θα χρησιμοποιήσουμε Maven στα παραδείγματα.  
* Άδεια Aspose OCR for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  
* Ένα αρχείο PDF που περιέχει σαρωμένες σελίδες (το demo χρησιμοποιεί `mixed_lang.pdf`).  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε – τα παρακάτω βήματα περιλαμβάνουν τις ακριβείς εντολές για να ξεκινήσετε.

![Create searchable PDF using Aspose OCR Java](https://example.com/images/create-searchable-pdf.png "Create searchable PDF using Aspose OCR Java")

## Βήμα 1: Ρύθμιση του Project και **Create Searchable PDF** – Αρχικοποίηση Project

Πρώτα, δημιουργήστε ένα Maven project. Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Μεταβείτε στον φάκελο:

```bash
cd SearchablePdfDemo
```

Προσθέστε την εξάρτηση Aspose OCR στο `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **Γιατί είναι σημαντικό:** Η διαδικασία **create searchable pdf** εξαρτάται από την κλάση `OcrEngine`, η οποία βρίσκεται μέσα στη βιβλιοθήκη Aspose OCR. Χωρίς τη σωστή έκδοση θα λάβετε σφάλματα μεταγλώττισης ή θα λείπουν λειτουργίες.

Τώρα δημιουργήστε την κύρια κλάση Java `QuickDemo.java` στο `src/main/java/com/example/ocr/`.

## Βήμα 2: Ενεργοποίηση Επιτάχυνσης GPU – **OCR PDF with GPU**

Η επιτάχυνση GPU μπορεί να μειώσει λεπτά από μια εργασία OCR πολλαπλών σελίδων. Το Aspose OCR σας επιτρέπει να το ενεργοποιήσετε με μια μόνο γραμμή:

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

Αν το μηχάνημά σας διαθέτει συμβατό GPU NVIDIA ή AMD και οι κατάλληλοι οδηγοί είναι εγκατεστημένοι, η μηχανή OCR θα μεταβιβάσει το βαρέως βάρους στην κάρτα γραφικών. Διαφορετικά, η κλήση επιστρέφει με ασφάλεια στην επεξεργασία CPU — χωρίς κατάρρευση, απλώς πιο αργή εκτέλεση.

> **Pro tip:** Σε Linux, ίσως χρειαστεί να ορίσετε το `LD_LIBRARY_PATH` ώστε να δείχνει στις βιβλιοθήκες CUDA πριν ξεκινήσετε το JVM.

## Βήμα 3: **Load PDF for OCR** και Διαμόρφωση Υποστήριξης Γλώσσας

Τώρα πραγματικά **load pdf for ocr**. Το Aspose OCR αντιμετωπίζει τις σελίδες PDF ως εικόνες εσωτερικά, οπότε απλώς δείχνετε τη μηχανή στο αρχείο:

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

Στη συνέχεια, ενημερώστε τη μηχανή για τη γλώσσα που αναμένετε. Στο demo μας εστιάζουμε στα Ταϊλανδικά, αλλά μπορείτε να περάσετε έναν πίνακα γλωσσών αν το έγγραφο περιέχει πολλαπλά σενάρια:

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

Αν έχετε προσαρμοσμένο λεξικό (π.χ. όρους ειδικού τομέα), ενσωματώστε το:

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **Γιατί να ορίσετε γλώσσα;** Η ακρίβεια του OCR εξαρτάται από το μοντέλο γλώσσας. Η παροχή του σωστού `OcrLanguage` μειώνει δραστικά τις λανθασμένες αναγνώσεις, ειδικά για μη‑λατινικά σενάρια.

## Βήμα 4: **Convert PDF to Searchable PDF** με Μία Κλήση

Το Aspose OCR ξεχωρίζει επειδή μπορεί να **convert pdf to searchable pdf** με μία μόνο κλήση μεθόδου — χωρίς ανάγκη χειροκίνητης συγχώνευσης εικόνων και επιπέδων κειμένου.

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

Πίσω από τη σκηνή, η μηχανή:

1. Εκτελεί OCR σε κάθε εικόνα σελίδας.  
2. Δημιουργεί ένα αόρατο στρώμα κειμένου που ταιριάζει με το οπτικό περιεχόμενο.  
3. Ενσωματώνει αυτό το στρώμα σε νέο PDF, διατηρώντας την αρχική εμφάνιση.

Το αποτέλεσμα είναι ένα αρχείο που φαίνεται ταυτόσημο με το εισαγόμενο, αλλά μπορεί να ευρετηριαστεί από οποιονδήποτε προβολέα PDF.

## Βήμα 5: Ανάκτηση Αναγνωρισμένου Κειμένου και Επαλήθευση Εξόδου

Ακόμη και αν έχουμε ήδη αποθηκεύσει ένα αναζητήσιμο PDF, μπορεί να θέλετε το ακατέργαστο κείμενο για καταγραφή ή περαιτέρω επεξεργασία:

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

Όταν εκτελέσετε το πρόγραμμα, θα δείτε το εξαγόμενο Ταϊλανδικό κείμενο στην κονσόλα, ακολουθούμενο από ένα νέο `mixed_lang_searchable.pdf` στον φάκελό σας.

### Αναμενόμενη Έξοδος Κονσόλας (κομμένη)

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

Ανοίξτε το παραγόμενο PDF σε Adobe Reader ή οποιονδήποτε προβολέα, πατήστε **Ctrl + F**, και θα μπορείτε να αναζητήσετε τις λέξεις που μόλις εμφανίστηκαν στην κονσόλα. Αυτό αποδεικνύει ότι δημιουργήσαμε επιτυχώς **create searchable pdf** αρχεία.

## Βήμα 6: Συνηθισμένα Προβλήματα και **Pro Tips** για OCR Υψηλής Απόδοσης

| Πρόβλημα | Σύμπτωμα | Διόρθωση |
|----------|----------|----------|
| **GPU not detected** | No speed boost, engine falls back to CPU | Ensure CUDA drivers are installed and `java.library.path` includes the GPU libs. |
| **Missing fonts** | Text layer shows garbled characters | Install the appropriate language fonts on the host OS or embed them via `engine.getEngineOptions().setEmbedFonts(true)`. |
| **Large PDFs (> 500 pages)** | Out‑of‑memory errors | Increase the JVM heap (`-Xmx4g`) and set `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` to spread work across cores. |
| **Custom dictionary not applied** | Spell‑corrector seems ignored | Verify the path is absolute and the file uses UTF‑8 encoding. |

> **Θυμηθείτε:** Η γραμμή `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());` είναι κρίσιμη όταν θέλετε να **ocr pdf with gpu** *και* να αξιοποιήσετε πλήρως τους πολυπύρηνους επεξεργαστές. Εντοπίζει τη μηχανή να δημιουργεί έναν worker ανά πυρήνα, κρατώντας το GPU απασχολημένο ενώ η CPU διαχειρίζεται την προ‑ και μετα‑επεξεργασία.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που ενσωματώνει κάθε βήμα που συζητήσαμε. Αντικαταστήστε τις διαδρομές placeholder με τις δικές σας.

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

Συμπιέστε και τρέξτε:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε το εξαγόμενο κείμενο στην κονσόλα και ένα νέο αναζητήσιμο PDF δίπλα στο αρχικό αρχείο.

## Συμπέρασμα

Δείξαμε πώς να **create searchable pdf** αρχεία σε Java χρησιμοποιώντας το Aspose OCR, καλύπτοντας όλα από τη ρύθμιση του project μέχρι την επιτάχυνση GPU. Με το **load pdf for OCR**, τη διαμόρφωση υποστήριξης γλώσσας, και την κλήση της μίας‑γραμμής **convert pdf to searchable pdf**, παίρνετε ένα πλήρως ευρετηριασμένο έγγραφο έτοιμο για μηχανές αναζήτησης ή εσωτερικά συστήματα ανάκτησης.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `OcrLanguage.THAI` με `OcrLanguage.ENGLISH` ή συνδυάστε πολλαπλές γλώσσες για πολύγλωσσα PDFs. Πειραματιστείτε με τη ρύθμιση `engine.getEngineOptions().setResolution(300)` για να δείτε πώς η DPI επηρεάζει την ακρίβεια, ή ενσωματώστε προσαρμοσμένες γραμματοσειρές για καλύτερη απόδοση σε παλαιότερους προβολείς.

Έχετε ερωτήσεις σχετικά με τη βελτιστοποίηση της απόδοσης, την αδειοδότηση, ή την ενσωμάτωση αυτής της ροής εργασίας σε υπηρεσία Spring Boot; Αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση Aspose OCR Java για πιο βαθιές πληροφορίες. Καλή προγραμματιστική, και απολαύστε τη μετατροπή των στατικών σαρώσεων σε αναζητήσιμους θησαυρούς!

## Σχετικά Μαθήματα

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}