---
category: general
date: 2026-02-28
description: πώς να εκτελέσετε OCR σε C# χρησιμοποιώντας το Aspose OCR – μάθετε πώς
  να εξάγετε κείμενο από εικόνα, να μετατρέψετε την εικόνα σε JSON ή XML σε λίγα μόνο
  βήματα.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: el
og_description: πώς να εκτελέσετε OCR σε C# χρησιμοποιώντας το Aspose OCR – ανακαλύψτε
  πώς να εξάγετε κείμενο από εικόνα και να μετατρέψετε την εικόνα σε JSON ή XML με
  ένα έτοιμο παράδειγμα προς εκτέλεση.
og_title: πώς να εκτελέσετε OCR με το Aspose OCR σε C# – Πλήρης Οδηγός
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να εκτελέσετε OCR με το Aspose OCR σε C# – Πλήρης Οδηγός
url: /el/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να εκτελέσετε OCR με Aspose OCR σε C# – Πλήρης Οδηγός

Αν αναρωτιέστε **πώς να εκτελέσετε OCR** σε εικόνα απόδειξης χρησιμοποιώντας C#, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από το **εξαγωγή κειμένου από εικόνα** και στη συνέχεια το **μετατροπή εικόνας σε JSON** ή το **μετατροπή εικόνας σε XML** με το Aspose OCR—όλα σε ένα ενιαίο, αυτόνομο πρόγραμμα.

Φανταστείτε ότι δημιουργείτε μια εφαρμογή παρακολούθησης εξόδων και χρειάζεστε να εξάγετε τις γραμμές από φωτογραφημένες αποδείξεις. Η χειροκίνητη πληκτρολόγηση κάθε εγγραφής είναι κουραστική, σωστά; Στο τέλος αυτού του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο snippet που διαβάζει οποιαδήποτε εικόνα, επιστρέφει δομημένο κείμενο και παρέχει τόσο JSON όσο και XML αναπαραστάσεις έτοιμες για επεξεργασία downstream.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.8)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)
- Ένα ενεργό πακέτο **Aspose.OCR** NuGet (`Install-Package Aspose.OCR`)
- Μια δείγμα εικόνας (π.χ., `receipt.png`) τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε

Δεν απαιτείται πρόσθετη ρύθμιση· η βιβλιοθήκη περιλαμβάνει όλα τα απαραίτητα μοντέλα OCR.

![Receipt image for OCR processing – how to run OCR](receipt.png)

> *Alt text: Εικόνα απόδειξης για επεξεργασία OCR – πώς να εκτελέσετε OCR*

## Υλοποίηση βήμα‑βήμα

Παρακάτω χωρίζουμε τη λύση σε λογικά τμήματα. Κάθε βήμα εξηγεί **γιατί** το κάνουμε, όχι μόνο **τι** είναι ο κώδικας.

### 1️⃣ Αρχικοποίηση του OCR Engine – η βάση του **πώς να εκτελέσετε OCR**

Η κλάση `OcrEngine` είναι το σημείο εισόδου. Η δημιουργία της φορτώνει τα εσωτερικά μοντέλα γλώσσας και προετοιμάζει τη μηχανή για αναγνώριση.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Συμβουλή:** Η επαναχρησιμοποίηση του ίδιου `OcrEngine` για πολλαπλές εικόνες μειώνει την κατανάλωση μνήμης και επιταχύνει την επεξεργασία παρτίδας.

### 2️⃣ Φόρτωση της εικόνας – ο πυρήνας του **εξαγωγή κειμένου από εικόνα**

Το Aspose OCR λειτουργεί με το δικό του wrapper `Image`. Η χρήση της δήλωσης `using` εγγυάται ότι το αρχείο κλείνει άμεσα.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Αν η εικόνα είναι σε διαφορετική μορφή (BMP, TIFF, PDF), η ίδια μέθοδος `Load` τη διαχειρίζεται—χωρίς επιπλέον μετατροπές.

### 3️⃣ Εκτέλεση OCR Recognition – η καρδιά του **πώς να εκτελέσετε OCR**

Η κλήση `Recognize` εκτελεί το βαρέως φορτίου έργο: ανάλυση διάταξης, τμηματοποίηση χαρακτήρων και ταξινόμηση ανά γλώσσα.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

Το επιστρεφόμενο `OcrResult` περιέχει ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης και ένα λεπτομερές δέντρο διάταξης που μπορεί να σειριοποιηθεί.

### 4️⃣ Μετατροπή εικόνας σε JSON – ο απλός τρόπος για **μετατροπή εικόνας σε json**

Το JSON είναι ιδανικό για web APIs ή NoSQL αποθηκευτικούς χώρους. Η μέθοδος `ToJson` σας δίνει μια όμορφα μορφοποιημένη συμβολοσειρά, κάνοντας το debugging παιχνιδάκι.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Τυπική έξοδος JSON μοιάζει με αυτή (περιορισμένη για συντομία):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Τώρα μπορείτε να στείλετε αυτό το JSON απευθείας σε ένα REST endpoint ή να το αποθηκεύσετε σε Azure Cosmos DB.

### 5️⃣ Μετατροπή εικόνας σε XML – όταν απαιτείται **μετατροπή εικόνας σε xml**

Κάποια παλαιά συστήματα εξακολουθούν να καταναλώνουν XML. Το Aspose παρέχει τη μέθοδο `ToXml` για μια καθαρή, συμβατή με σχήμα αναπαράσταση.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Δείγμα XML:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Και οι δύο μορφές διατηρούν τα ίδια ιεραρχικά δεδομένα, ώστε να διαλέξετε ό,τι ταιριάζει καλύτερα στην αλυσίδα επεξεργασίας σας.

## Συνηθισμένα προβλήματα & Πώς να εξάγετε κείμενο αξιόπιστα

Ακόμα και με μια ισχυρή βιβλιοθήκη, οι πραγματικές εικόνες ρίχνουν απρόοπτα. Εδώ είναι τρία ζητήματα που μπορεί να συναντήσετε και οι αντίστοιχες λύσεις.

### 📏 Εικόνες χαμηλής ανάλυσης

**Γιατί έχει σημασία:** Μικρά γράμματα συγχωνεύονται, μειώνοντας τις βαθμολογίες εμπιστοσύνης.  
**Λύση:** Προεπεξεργαστείτε την εικόνα—αυξήστε την ανάλυση με `Image.Resize` ή εφαρμόστε φίλτρο ενίσχυσης πριν τη δώσετε στο `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Κακή αντίθεση

**Γιατί έχει σημασία:** Ανοιχτό κείμενο σε σκούρο φόντο μπερδεύει τον αλγόριθμο τμηματοποίησης.  
**Λύση:** Αντιστρέψτε τα χρώματα ή ρυθμίστε τη φωτεινότητα/αντίθεση μέσω `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Πολυγλωσσικά έγγραφα

**Γιατί έχει σημασία:** Το προεπιλεγμένο μοντέλο γλώσσας είναι τα Αγγλικά· μεικτές γλώσσες οδηγούν σε ακατάλληλη έξοδο.  
**Λύση:** Ορίστε `ocrEngine.Language = OcrLanguage.Multilingual;` πριν από την αναγνώριση.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Η αντιμετώπιση αυτών των περιπτώσεων εξασφαλίζει ότι το **εξαγωγή κειμένου** από οποιαδήποτε εικόνα γίνεται αξιόπιστη διαδικασία και όχι τυχαία.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση και εκτέλεση. Απλώς αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή της εικόνας σας και πατήστε F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Αναμενόμενη έξοδος κονσόλας** (μορφοποιημένη για ευκρίνεια) εμφανίζει τόσο τις δομές JSON όσο και XML που περιέχουν το εξαγόμενο κείμενο και τα πλαίσια περιορισμού.

## Ανακεφαλαίωση – Τι καλύψαμε

- **πώς να εκτελέσετε OCR** με Aspose OCR σε C#
- Η διαδικασία βήμα‑βήμα για **εξαγωγή κειμένου από εικόνα**
- Δύο επιλογές σειριοποίησης: **μετατροπή εικόνας σε json** και **μετατροπή εικόνας σε xml**
- Συμβουλές για αντιμετώπιση χαμηλής ανάλυσης, χαμηλής αντίθεσης και πολυγλωσσικών σεναρίων
- Ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση δείγμα κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET

## Τι ακολουθεί;

Τώρα που μπορείτε να **εξάγετε κείμενο** και να λάβετε δομημένα δεδομένα, σκεφτείτε τις παρακάτω ιδέες:

- Στείλτε το JSON σε μια Azure Function που αποθηκεύει τις αποδείξεις σε Cosmos DB.
- Χρησιμοποιήστε την έξοδο XML για να γεμίσετε ένα υπάρχον σύστημα λογιστικής βασισμένο σε SOAP.
- Συνδυάστε το Aspose OCR με ένα μοντέλο μηχανικής μάθησης για αυτόματη κατηγοριοποίηση τύπων εξόδων.

Πειραματιστείτε ελεύθερα—αντικαταστήστε το `receipt.png` με τιμολόγια, επαγγελματικές κάρτες ή χειρόγραφα σημειώματα. Το ίδιο μοτίβο λειτουργεί σε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}