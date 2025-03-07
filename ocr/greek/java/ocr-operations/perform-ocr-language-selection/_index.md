---
title: Εκτέλεση OCR με επιλογή γλώσσας στο Aspose.OCR
linktitle: Εκτέλεση OCR με επιλογή γλώσσας στο Aspose.OCR
second_title: Aspose.OCR Java API
description: Ξεκλειδώστε την ακριβή εξαγωγή κειμένου από εικόνες με το Aspose.OCR για Java. Ακολουθήστε τον οδηγό βήμα προς βήμα για ακριβή OCR με επιλογή γλώσσας.
weight: 11
url: /el/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR με επιλογή γλώσσας στο Aspose.OCR

## Εισαγωγή

Στο συνεχώς εξελισσόμενο τοπίο της τεχνολογίας, η Οπτική Αναγνώριση Χαρακτήρων (OCR) παίζει καθοριστικό ρόλο στην εξαγωγή ουσιαστικών πληροφοριών από εικόνες. Το Aspose.OCR για Java ξεχωρίζει ως ένα ισχυρό εργαλείο που επιτρέπει στους προγραμματιστές να ενσωματώνουν απρόσκοπτα τις δυνατότητες OCR στις εφαρμογές Java τους. Σε αυτόν τον οδηγό βήμα προς βήμα, θα διερευνήσουμε πώς να εκτελείτε το OCR με την επιλογή γλώσσας χρησιμοποιώντας το Aspose.OCR, ξεκλειδώνοντας τη δυνατότητα επεξεργασίας διαφορετικού περιεχομένου με ακρίβεια.

## Προαπαιτούμενα

Πριν βουτήξετε στο σεμινάριο, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

- Περιβάλλον ανάπτυξης Java: Βεβαιωθείτε ότι έχετε εγκαταστήσει Java στο σύστημά σας και ότι το περιβάλλον ανάπτυξής σας είναι ρυθμισμένο.

-  Aspose.OCR Library: Κάντε λήψη και εγκατάσταση της βιβλιοθήκης Aspose.OCR για Java. Μπορείτε να βρείτε τη βιβλιοθήκη και τη σχετική τεκμηρίωση[εδώ](https://reference.aspose.com/ocr/java/).

- Αρχείο εικόνας: Προετοιμάστε ένα αρχείο εικόνας που περιέχει το κείμενο που θέλετε να εξαγάγετε. Για παράδειγμα, ας χρησιμοποιήσουμε ένα αρχείο με το όνομα "p3.png".

## Εισαγωγή πακέτων

Στο έργο σας Java, εισαγάγετε τα απαραίτητα πακέτα για να αξιοποιήσετε τη λειτουργικότητα Aspose.OCR. Προσθέστε τις ακόλουθες γραμμές στην αρχή του αρχείου σας Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Βήμα 1: Ρυθμίστε τον Κατάλογο Εγγράφων σας

```java
// Η διαδρομή προς τον κατάλογο εγγράφων.
String dataDir = "Your Document Directory";
```

Αντικαταστήστε το "Your Document Directory" με την πραγματική διαδρομή προς τον κατάλογο όπου βρίσκεται το αρχείο εικόνας σας.

## Βήμα 2: Καθορίστε τη διαδρομή εικόνας

```java
// Η διαδρομή της εικόνας
String file = dataDir + "p3.png";
```

Προσαρμόστε τη μεταβλητή αρχείου ώστε να οδηγεί στο συγκεκριμένο αρχείο εικόνας σας.

## Βήμα 3: Δημιουργία παρουσίας API Aspose.OCR

```java
// Δημιουργία παρουσίας API
AsposeOCR api = new AsposeOCR();
```

Αρχικοποιήστε το αντικείμενο AsposeOCR για πρόσβαση στις δυνατότητές του.

## Βήμα 4: Ορίστε τις επιλογές αναγνώρισης

```java
// Ορίστε τις επιλογές αναγνώρισης
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Προσαρμόστε τις ρυθμίσεις αναγνώρισης με βάση τις απαιτήσεις σας. Προσαρμόστε παραμέτρους όπως περιοχές λοξής, γλώσσας και αναγνώρισης.

## Βήμα 5: Εκτελέστε OCR και ανάκτηση αποτελεσμάτων

```java
// Λήψη αντικειμένου αποτελέσματος
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Εκτελέστε τη λειτουργία OCR χρησιμοποιώντας το καθορισμένο αρχείο εικόνας και ρυθμίσεις. Καταγράψτε το αποτέλεσμα στο αντικείμενο RecognitionResult.

## Βήμα 6: Εκτύπωση και χρήση αποτελεσμάτων

```java
// Εκτύπωση αποτελέσματος
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Εκτυπώστε το εξαγόμενο κείμενο, τις περιοχές αναγνώρισης, την αναπαράσταση JSON, τη γωνία κλίσης και τυχόν προειδοποιήσεις. Χρησιμοποιήστε τα αποτελέσματα όπως απαιτείται στην αίτησή σας.

## συμπέρασμα

Σε αυτό το σεμινάριο, έχουμε εμβαθύνει στην απρόσκοπτη ενσωμάτωση του Aspose.OCR για Java για την εκτέλεση OCR με επιλογή γλώσσας. Αυτή η ισχυρή βιβλιοθήκη ανοίγει έναν κόσμο δυνατοτήτων για προγραμματιστές που στοχεύουν να εξάγουν κείμενο από εικόνες με ακρίβεια.

## Συχνές ερωτήσεις

### Ε1: Μπορώ να χρησιμοποιήσω το Aspose.OCR για πολλές γλώσσες σε μία διαδικασία αναγνώρισης;

A1: Ναι, μπορείτε να ορίσετε πολλές γλώσσες στις Ρυθμίσεις αναγνώρισης για να βελτιώσετε την ακρίβεια αναγνώρισης για πολύγλωσσο περιεχόμενο.

### Ε2: Πώς μπορώ να χειριστώ διαφορετικές μορφές εικόνας με το Aspose.OCR;

A2: Το Aspose.OCR υποστηρίζει διάφορες μορφές εικόνας, συμπεριλαμβανομένων των PNG, JPEG και TIFF. Απλώς δώστε τη σωστή διαδρομή αρχείου στη μεταβλητή διαδρομής εικόνας.

### Ε3: Υπάρχει όριο στο μέγεθος της εικόνας που μπορεί να επεξεργαστεί το Aspose.OCR;

A3: Το Aspose.OCR μπορεί να χειριστεί εικόνες διαφορετικών μεγεθών, αλλά οι μεγαλύτερες εικόνες ενδέχεται να απαιτούν περισσότερο χρόνο και πόρους επεξεργασίας.

### Ε4: Μπορώ να προσαρμόσω τις ρυθμίσεις αναγνώρισης για συγκεκριμένες περιοχές μέσα σε μια εικόνα;

Α4: Απολύτως. Χρησιμοποιήστε τη δυνατότητα Recognition Areas για να ορίσετε συγκεκριμένα ορθογώνια μέσα στην εικόνα για στοχευμένη αναγνώριση.

### Ε5: Είναι το Aspose.OCR κατάλληλο τόσο για προσωπικά όσο και για εμπορικά έργα;

A5: Ναι, το Aspose.OCR προσφέρει ευέλικτες επιλογές αδειοδότησης, καθιστώντας το κατάλληλο τόσο για προσωπική όσο και για εμπορική χρήση.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
