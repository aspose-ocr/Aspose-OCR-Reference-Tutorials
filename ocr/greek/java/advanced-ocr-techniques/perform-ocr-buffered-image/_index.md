---
date: 2026-05-04
description: Μάθετε πώς να πραγματοποιήσετε μετατροπή εικόνας σε κείμενο με Java χρησιμοποιώντας
  το Aspose.OCR για Java. Αυτός ο βήμα‑βήμα οδηγός σας δείχνει πώς να εξάγετε κείμενο
  από εικόνα με BufferedImage.
keywords:
- image to text java
- extract text from image
- recognize text from png
linktitle: 'Εξαγωγή κειμένου από εικόνα Java: OCR σε BufferedImage με Aspose.OCR'
second_title: Aspose.OCR Java API
title: 'εικόνα σε κείμενο java: Μετατροπή εικόνας σε κείμενο με το Aspose.OCR'
url: /el/java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Εικόνας σε Κείμενο σε Java: OCR σε BufferedImage με Aspose.OCR

## Εισαγωγή

Σε αυτό το **Aspose OCR Java tutorial** θα ανακαλύψετε πώς να **convert image to text** χρησιμοποιώντας τη δυνατή βιβλιοθήκη Aspose.OCR. **This guide walks you through image to text java** χρησιμοποιώντας την υποστήριξη BufferedImage του Aspose.OCR, είτε χρειάζεται να επεξεργαστείτε σαρωμένα έγγραφα, να διαβάσετε αποδείξεις ή να εξάγετε κείμενο από στιγμιότυπα οθόνης. Θα περάσουμε από τη ρύθμιση, τις απαιτούμενες εισαγωγές και τον ακριβή κώδικα που χρειάζεστε για γρήγορα αποτελέσματα.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη είναι η καλύτερη για Java OCR;** Aspose.OCR for Java.  
- **Μπορώ να επεξεργαστώ ένα BufferedImage απευθείας;** Yes – the `RecognizePage` method accepts `BufferedImage`.  
- **Χρειάζομαι άδεια για δοκιμή;** A free trial works for development; a license is required for production.  
- **Ποια φορμά εικόνας υποστηρίζονται;** PNG, JPEG, BMP, TIFF, and more.  
- **Πόσο χρόνο χρειάζεται μια τυπική εικόνα για επεξεργασία;** Usually under a second for standard‑size images.

## Τι είναι η μετατροπή εικόνας σε κείμενο σε Java;

Η Optical Character Recognition (OCR) αναλύει οπτικά μοτίβα σε μια εικόνα και τα μετατρέπει σε επεξεργάσιμο κείμενο. Σε Java, το OCR σας επιτρέπει να **extract text from image** αρχεία προγραμματιστικά, ανοίγοντας το δρόμο για αυτοματοποιημένη εισαγωγή δεδομένων, αρχεία αναζήτησης και ροές εργασίας με AI χωρίς χειροκίνητη μεταγραφή.

## Γιατί να επιλέξετε Aspose.OCR για Java;

- **High accuracy** across multiple languages and fonts.  
- **Simple API** – one line of code can recognize an entire page.  
- **No external dependencies** – works with plain `BufferedImage`.  
- **Comprehensive documentation** and regular updates (see the trust signals at the bottom).  

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Kit (JDK)** – version 8 ή νεότερο. Κατεβάστε το από [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.OCR for Java** – obtain the latest JAR from the Aspose website [here](https://releases.aspose.com/ocr/java/).  
3. **A folder with images** – create a directory on your machine and place the images you want to process. Update the `dataDir` variable in the code to point to this folder.

## Εισαγωγή Πακέτων

Ξεκινήστε εισάγοντας τις βασικές κλάσεις. Η κλάση `AsposeOCR` παρέχει τη μηχανή OCR, ενώ οι `ImageIO` και `BufferedImage` διαχειρίζονται τη φόρτωση της εικόνας.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
```

## Πώς να **Convert Image to Text** σε Java – Οδηγός Βήμα‑βήμα

### Βήμα 1: Ορίστε τον φάκελο εγγράφου και τη διαδρομή εικόνας  

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

Αντικαταστήστε `"Your Document Directory"` με την απόλυτη διαδρομή όπου βρίσκονται τα αρχεία PNG/JPEG σας. Αυτός είναι ο φάκελος από τον οποίο η διαδικασία **image to text java** θα διαβάσει.

### Βήμα 2: Δημιουργήστε ένα αντικείμενο AsposeOCR  

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Το αντικείμενο `AsposeOCR` σας δίνει πρόσβαση σε όλες τις μεθόδους OCR, συμπεριλαμβανομένης της επιλογής γλώσσας και των προχωρημένων ρυθμίσεων αν τις χρειαστείτε αργότερα.

### Βήμα 3: Φορτώστε την εικόνα και αναγνωρίστε το κείμενο  

```java
// Recognize page from BufferedImage
try {
    BufferedImage loaded = ImageIO.read(new File(imagePath));
    String result = api.RecognizePage(loaded);
    System.out.println("Result BufferedImage: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

Εδώ:

1. Φορτώνουμε το αρχείο εικόνας σε ένα `BufferedImage`.  
2. Καλούμε `api.RecognizePage(loaded)` – αυτή είναι η κεντρική κλήση **extract text java**.  
3. Εκτυπώνουμε το αναγνωρισμένο κείμενο στην κονσόλα.

> **Pro tip:** Μπορείτε επίσης να **recognize text from png** αρχεία με την ίδια μέθοδο· απλώς δείξτε το `imagePath` σε μια PNG εικόνα.

Επαναλάβετε τα τρία βήματα για κάθε εικόνα που χρειάζεται επεξεργασία, απλώς προσαρμόζοντας το `imagePath`.

## Συχνές Περιπτώσεις Χρήσης

- **Invoice processing:** Extract line‑item details from scanned PDFs or PNG receipts.  
- **Document archiving:** Turn scanned contracts into searchable text for quick retrieval.  
- **Automation bots:** Pull text from screenshots of web pages or desktop applications.

## Συχνά Προβλήματα & Επίλυση

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|----------|
| `null` output | Το αρχείο εικόνας δεν βρέθηκε ή δεν μπορεί να διαβαστεί | Επαληθεύστε το `dataDir` και το όνομα αρχείου· βεβαιωθείτε ότι η εικόνα είναι σε υποστηριζόμενο φορμά |
| Garbled characters | Wrong language settings | Use `api.setLanguage(Language.<desired>)` before `RecognizePage` |
| Slow performance on large images | Image resolution too high | Resize the image or pass a scaled `BufferedImage` to the API |

## Συχνές Ερωτήσεις (Πρόσθετες)

**Q1: Μπορεί το Aspose.OCR να διαχειριστεί πολλές γλώσσες;**  
A: Yes – it supports dozens of languages out of the box. You can set the target language with `api.setLanguage(Language.English)` (or any other supported language).

**Q2: Είναι το Aspose.OCR συμβατό με διαφορετικά φορμά εικόνας;**  
A: Absolutely. PNG, JPEG, BMP, TIFF, and GIF are all supported.

**Q3: Πόσο συχνά ενημερώνεται το Aspose.OCR;**  
A: Aspose releases regular updates. Check the latest release notes on the [documentation page](https://reference.aspose.com/ocr/java/).

**Q4: Μπορώ να δοκιμάσω το Aspose.OCR πριν το αγοράσω;**  
A: Yes – a free trial is available [here](https://releases.aspose.com/).

**Q5: Πού μπορώ να βρω υποστήριξη κοινότητας για το Aspose.OCR;**  
A: Join the discussion on the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

## FAQ – Γρήγορη Αναφορά για το Java OCR Tutorial

**Q: Ποιος είναι ο πιο εύκολος τρόπος για να ξεκινήσετε ένα **java ocr tutorial**;**  
A: Install the JDK, add the Aspose.OCR JAR to your project, and follow the three‑step code pattern shown above.

**Q: Μπορώ να χρησιμοποιήσω αυτή τη μέθοδο για **process scanned documents** μαζικά;**  
A: Yes. Loop over files in a directory, reuse the same `AsposeOCR` instance, and collect each result.

**Q: Πρέπει να ορίσω γλώσσα για κείμενο στα Αγγλικά;**  
A: English is the default, but you can explicitly set it with `api.setLanguage(Language.English)` for clarity.

**Q: Υπάρχει κάποιος αντίκτυπος στην απόδοση όταν τρέχει σε διακομιστή;**  
A: The engine is lightweight; typical images (<2 MB) are processed in under a second. For high‑throughput scenarios, consider image pre‑scaling or multi‑threading.

**Q: Πώς διαχειρίζομαι την άδεια παραγωγής;**  
A: Load your license file with `License license = new License(); license.setLicense("Aspose.OCR.lic");` before creating the `AsposeOCR` instance.

**Last Updated:** 2026-05-04  
**Tested With:** Aspose.OCR for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}