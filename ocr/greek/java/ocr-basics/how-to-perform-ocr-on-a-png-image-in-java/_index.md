---
category: general
date: 2026-10-11
description: Μάθετε πώς να εκτελείτε OCR σε εικόνα PNG με Java, να εξάγετε κείμενο
  από την εικόνα και να μετατρέψετε την εικόνα σε κείμενο με ένα απλό παράδειγμα OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: el
lastmod: 2026-10-11
og_description: Πώς να εκτελέσετε OCR σε εικόνα PNG με Java, να εξάγετε κείμενο από
  την εικόνα και να μετατρέψετε την εικόνα σε κείμενο χρησιμοποιώντας ένα σύντομο,
  έτοιμο προς εκτέλεση παράδειγμα.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Πώς να εκτελέσετε OCR σε εικόνα PNG σε Java – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Πώς να κάνετε OCR σε εικόνα PNG με Java
url: /el/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε εικόνα PNG σε Java

Αν χρειάζεται να **εκτελέσετε OCR** σε ένα αρχείο εικόνας, η εκμάθηση **πώς να εκτελέσετε OCR** σε Java είναι απαραίτητη για πολλές εργασίες αυτοματοποίησης. Είτε ψηφιοποιείτε αποδείξεις, κατατάσσετε σαρωμένα έγγραφα, είτε δημιουργείτε ένα αναζητήσιμο αρχείο φωτογραφιών, η δυνατότητα **εξαγωγής κειμένου από εικόνα** εξοικονομεί αμέτρητες ώρες χειροκίνητης εργασίας.

Αυτό το tutorial σας παρουσιάζει μια πλήρη, εκτελέσιμη λύση που φορτώνει ένα PNG, τρέχει μια μηχανή OCR και **αναγνωρίζει κείμενο από PNG** αρχεία. Θα δείτε επίσης πώς να **μετατρέψετε εικόνα σε κείμενο** και να αντιμετωπίσετε κοινά προβλήματα όπως εικόνες χαμηλής ανάλυσης ή μη‑ASCII χαρακτήρες.

## Τι θα επιτύχετε

Στο τέλος αυτού του οδηγού θα μπορείτε να:

* **φορτώσετε εικόνα java** κώδικα που διαβάζει ένα PNG από το δίσκο,
* αρχικοποιήσετε μια ελαφριά μηχανή OCR,
* **εξάγετε κείμενο από εικόνα** και εκτυπώσετε το αποτέλεσμα στην κονσόλα,
* προσαρμόσετε τη λύση για άλλες μορφές εικόνας ή επεξεργασία σε παρτίδες.

Δεν απαιτούνται εξωτερικές υπηρεσίες—μόνο μια ανοιχτή βιβλιοθήκη OCR (Tess4J) και το Java SE runtime.

---

## Προαπαιτούμενα

* Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με JDK 17).
* Maven ή Gradle για διαχείριση εξαρτήσεων.
* Βασική εξοικείωση με τη γραμμή εντολών και το IDE της επιλογής σας.
* Η βιβλιοθήκη `tess4j` (ένα Java wrapper για το Tesseract). Προσθέστε την ακόλουθη εξάρτηση Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Αν χρησιμοποιείτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Χρειάζεστε επίσης τα αρχεία δεδομένων του Tesseract (`.traineddata`). Κατεβάστε το πακέτο δεδομένων αγγλικής γλώσσας από το επίσημο αποθετήριο και τοποθετήστε το σε φάκελο με όνομα `tessdata` στη ρίζα του έργου.

---

## Βήμα 1: Φορτώστε την εικόνα σε Java

Η φόρτωση ενός PNG είναι απλή με την τυπική κλάση `ImageIO`. Ο παρακάτω κώδικας δείχνει **load image java** με ασφαλή, εξαίρεση‑συνειδητό τρόπο:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Γιατί είναι σημαντικό:** Η `ImageIO.read` ανιχνεύει αυτόματα τη μορφή της εικόνας, αλλά ελέγχουμε ρητά για `null` ώστε να αποφύγουμε σιωπηλές αποτυχίες όταν το PNG είναι κατεστραμμένο. Αυτό το μοτίβο αποτελεί βέλτιστη πρακτική όταν **load image java** για OCR.

---

## Βήμα 2: Αρχικοποιήστε τη μηχανή OCR

Το Tess4J τυλίγει το εγγενές δυαδικό του Tesseract, εκθέτοντας ένα απλό API Java. Η παρακάτω μέθοδος δημιουργεί ένα αντικείμενο `Tesseract`, το κατευθύνει στον φάκελο `tessdata` και ρυθμίζει τη γλώσσα στα Αγγλικά:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Γιατί το κάνουμε:** Η αρχικοποίηση της μηχανής μία φορά και η επαναχρησιμοποίησή της για πολλές εικόνες μειώνει το κόστος εκκίνησης. Η κλήση `setOcrEngineMode` επιλέγει τη προεπιλεγμένη λειτουργία, η οποία λειτουργεί καλά για τα περισσότερα PNG. Αν αντιμετωπίσετε θορυβώδεις σαρώσεις, μπορείτε να πειραματιστείτε με άλλες λειτουργίες (π.χ., `OEM_LSTM_ONLY`).

---

## Βήμα 3: Εκτελέστε OCR και **αναγνωρίστε κείμενο από PNG**

Τώρα συνδυάζουμε τον φορτωτή εικόνας και τη μηχανή OCR. Η παρακάτω μέθοδος εκτελεί OCR σε ένα `BufferedImage` και επιστρέφει το εξαγόμενο κείμενο:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Πλήρες εκτελέσιμο παράδειγμα**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Αναμενόμενο αποτέλεσμα**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Η κονσόλα θα εμφανίσει τους ακριβείς χαρακτήρες που εξήγαγε η μηχανή από το `sample.png`. Αν το PNG περιέχει μόνο μία λέξη, η έξοδος θα είναι αυτή η λέξη ακολουθούμενη από αλλαγή γραμμής.

---

## Βήμα 4: Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### 4.1 Διαχείριση PNG χαμηλής ανάλυσης

Το Tesseract αποδίδει καλύτερα σε εικόνες τουλάχιστον 300 DPI. Αν το PNG προέλευσης είναι μικρότερο, αυξήστε το μέγεθός του πριν το OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Εφαρμόστε `upscale(image, 2)` πριν καλέσετε `extractText` για βελτίωση της ακρίβειας.

### 4.2 Εξαγωγή κειμένου μη‑Αγγλικής γλώσσας

Για **extract text from image** που περιέχει άλλες γλώσσες, κατεβάστε τα αντίστοιχα αρχεία `.traineddata` και ορίστε τον κωδικό γλώσσας:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Επεξεργασία σε παρτίδες πολλαπλών PNG

Αν χρειάζεται να **recognize text from PNG** αρχεία σε φάκελο, επαναλάβετε πάνω στον κατάλογο:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Αντιμετώπιση σφαλμάτων OCR

Τυπικά λάθη OCR περιλαμβάνουν την εσφαλμένη ανάγνωση του `0` (μηδέν) ως `O` ή του `1` ως `l`. Η μετα-επεξεργασία με κανονικές εκφράσεις μπορεί να καθαρίσει το αποτέλεσμα:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Pro tips για αξιόπιστο OCR σε Java

| Συμβουλή | Αιτία |
|-----|--------|
| **Χρησιμοποιήστε PNG χωρίς απώλειες** | Τα τεχνουργήματα συμπίεσης σε JPEG μπορούν να μπερδέψουν τη μηχανή. |
| **Κόψτε τα λευκά περιθώρια** | Η περιττή λευκή περιοχή αυξάνει το χρόνο επεξεργασίας και μπορεί να προκαλέσει ψευδείς θετικές αναγνώσεις. |
| **Ορίστε `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** μόνο όταν η διάταξη είναι άγνωστη· διαφορετικά επιλέξτε συγκεκριμένη λειτουργία (π.χ., `PSM_SINGLE_BLOCK`). |
| **Κρατήστε στην cache το αντικείμενο `ITesseract`** |

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}