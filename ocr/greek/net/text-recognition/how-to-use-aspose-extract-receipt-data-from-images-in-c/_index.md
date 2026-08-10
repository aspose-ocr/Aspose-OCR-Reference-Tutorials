---
category: general
date: 2026-04-04
description: Μάθετε πώς να χρησιμοποιείτε το Aspose για την εξαγωγή δεδομένων από
  απόδειξη, τη φόρτωση εικόνας απόδειξης και την OCR εικόνας απόδειξης με ένα πλήρες
  παράδειγμα C#. Οδηγός βήμα‑βήμα για προγραμματιστές.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: el
og_description: Πώς να χρησιμοποιήσετε το Aspose για την εξαγωγή δεδομένων από απόδειξη
  από μια σαρωμένη εικόνα απόδειξης. Πλήρης κώδικας C#, εξηγήσεις και συμβουλές για
  την επεξεργασία εικόνας απόδειξης με OCR.
og_title: Πώς να χρησιμοποιήσετε το Aspose – Εξαγωγή δεδομένων από αποδείξεις σε εικόνες
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Πώς να χρησιμοποιήσετε το Aspose – Εξαγωγή δεδομένων από αποδείξεις σε εικόνες
  με C#
url: /el/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το Aspose – Εξαγωγή δεδομένων από απόδειξη από εικόνες σε C#

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το Aspose** για να εξάγετε δομημένες πληροφορίες από μια φωτογραφία απόδειξης; Δεν είστε μόνοι. Είτε δημιουργείτε μια εφαρμογή παρακολούθησης εξόδων είτε αυτοματοποιείτε την εισαγωγή τιμολογίων, το πρόβλημα είναι το ίδιο: έχετε ένα PNG ή JPEG και χρειάζεστε το όνομα του εμπόρου, την ημερομηνία και το συνολικό ποσό χωρίς χειροκίνητη πληκτρολόγηση.

Το θέμα είναι—το Aspose.OCR κάνει όλη αυτή τη διαδικασία παιχνιδάκι. Σε αυτό το tutorial θα περάσουμε από τη φόρτωση μιας εικόνας απόδειξης, την εκτέλεση OCR, και τελικά την εξαγωγή δεδομένων απόδειξης με λίγες γραμμές C#. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα κονσόλας που εκτυπώνει τον έμπορο, την ημερομηνία και το συνολικό ποσό απευθείας στην κονσόλα.

> **Γρήγορη νίκη:** Αν χρειάζεστε μόνο τον κώδικα, μεταβείτε στην ενότητα «Πλήρες λειτουργικό παράδειγμα» στο τέλος και αντιγράψτε‑επικολλήστε.

## Τι θα χρειαστείτε

- **.NET 6.0 ή νεότερο** (το API λειτουργεί με .NET Core και .NET Framework)
- **Aspose.OCR for .NET** πακέτο NuGet (`Install-Package Aspose.OCR`)
- Ένα δείγμα εικόνας απόδειξης (PNG, JPG ή BMP) αποθηκευμένο τοπικά
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή που υποστηρίζει έργα C#

Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων. Η μόνη προϋπόθεση είναι μια βασική κατανόηση των εφαρμογών κονσόλας C#—αν έχετε γράψει το “Hello World”, είστε έτοιμοι.

## Βήμα 1 – Εγκατάσταση και Αναφορά του Aspose.OCR

Για **πώς να χρησιμοποιήσετε το Aspose**, πρώτα χρειάζεστε τη βιβλιοθήκη στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Εναλλακτικά, χρησιμοποιήστε το UI του NuGet και αναζητήστε το “Aspose.OCR”. Μόλις εγκατασταθεί, προσθέστε τα απαιτούμενα namespaces στην αρχή του αρχείου σας:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Συμβουλή:** Κρατήστε τα πακέτα NuGet ενημερωμένα. Από σήμερα (Απρίλιος 2026) η πιο πρόσφατη σταθερή έκδοση είναι η 23.11.0, η οποία περιλαμβάνει βελτιώσεις απόδοσης για OCR σε αποδείξεις υψηλής ανάλυσης.

## Βήμα 2 – Φόρτωση της εικόνας απόδειξης

Όταν **φορτώνετε εικόνα απόδειξης**, έχετε δύο κοινές πηγές: μια τοπική διαδρομή ή ένα stream από αίτημα web. Για αυτό το tutorial θα το κρατήσουμε απλό και θα διαβάσουμε από το δίσκο:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Αντικαταστήστε το `YOUR_DIRECTORY/receipt.png` με την πραγματική διαδρομή του αρχείου απόδειξης. Αν διαχειρίζεστε ανεβάσματα χρηστών, μπορείτε να περάσετε ένα `MemoryStream` στο `ImageStream.FromStream`.

> **Γιατί είναι σημαντικό:** Η καθορισμένη γλώσσα (English) λέει στη μηχανή OCR ποιο σύνολο χαρακτήρων να περιμένει, μειώνοντας τις λανθασμένες αναγνώσεις—ιδιαίτερα σημαντικό όταν **ocr receipt image** που περιέχει αριθμούς και σύμβολα.

## Βήμα 3 – Εκτέλεση OCR και σύλληψη πληροφοριών διάταξης

Το βήμα OCR κάνει περισσότερα από το να εκτυπώνει ακατέργαστο κείμενο· συλλαμβάνει επίσης τη διάταξη, η οποία είναι κρίσιμη για τη δομημένη εξαγωγή αργότερα.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Μετά το τέλος του `Recognize()`, το `ocrEngine` διατηρεί τόσο το απλό κείμενο όσο και τα δεδομένα θέσης κάθε λέξης. Αυτό είναι το θεμέλιο για το επόμενο βήμα όπου θα ζητήσουμε από το Aspose να “**how to extract receipt**” πεδία αυτόματα.

## Βήμα 4 – Αρχικοποίηση του Layout Recognizer

Το Aspose παρέχει μια κλάση `LayoutRecognizer` που γνωρίζει πώς οι αποδείξεις είναι συνήθως οργανωμένες (έμπορος στην κορυφή, γραμμή ημερομηνίας, σύνολο κοντά στο κάτω μέρος). Απλώς περνάτε τη ρυθμισμένη μηχανή OCR:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Στο παρασκήνιο, ο αναγνωριστής εφαρμόζει ένα σύνολο ευριστηρίων—όπως η αναζήτηση συμβόλων νομίσματος ή προτύπων ημερομηνίας—για να αντιστοιχίσει το ακατέργαστο κείμενο σε σημασιολογικά πεδία.

## Βήμα 5 – Εξαγωγή δομημένων δεδομένων απόδειξης

Τώρα έρχεται το γλυκό μέρος: **extract receipt data**. Μια κλήση μεθόδου κάνει το σκληρό έργο:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` είναι ένα αντικείμενο τύπου `ReceiptData` (ορίζεται στο `Aspose.OCR.Structured`). Περιέχει τρεις κύριες ιδιότητες:

- `Merchant` – το όνομα του καταστήματος
- `Date` – η ημερομηνία αγοράς ως `DateTime` (αν εντοπιστεί)
- `TotalAmount` – το συνολικό ποσό ως `decimal`

Αν η μηχανή δεν μπορεί να βρει ένα συγκεκριμένο πεδίο, η ιδιότητα θα είναι `null` ή `0`. Μπορείτε να προσθέσετε λογική εναλλακτικού εάν χρειάζεται (π.χ., να ζητήσετε από τον χρήστη επιβεβαίωση).

## Βήμα 6 – Εμφάνιση των εξαγόμενων πληροφοριών

Τέλος, εμφανίστε τα αποτελέσματα στην κονσόλα. Εδώ βλέπετε τους καρπούς της δουλειάς σας:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Οι μορφοποιημένες συμβολοσειρές (`:d` και `:C`) παράγουν αντίστοιχα μια σύντομη ημερομηνία και μια συμβολοσειρά νομίσματος, κάνοντας την έξοδο ευανάγνωστη.

### Αναμενόμενη έξοδος

Υποθέτοντας ότι η απόδειξη ανήκει στο “Coffee Corner”, ημερομηνίας 2025‑12‑01, με σύνολο $4.75, η κονσόλα θα εμφανίσει:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Αν λείπει κάποιο πεδίο, θα δείτε μια κενή γραμμή ή μια προεπιλεγμένη τιμή—ιδανικό για εντοπισμό σφαλμάτων.

## Περιπτώσεις Άκρων & Συνηθισμένα Πιθανά Σφάλματα

### 1. Εικόνες χαμηλής ανάλυσης

Αν η εικόνα της απόδειξης είναι θολή ή κάτω από 150 dpi, η ακρίβεια του OCR μειώνεται δραματικά. Η αύξηση της ανάλυσης της εικόνας με ένα απλό διγραμμικό φίλτρο πριν τη δώσετε στο Aspose μπορεί να βελτιώσει τα αποτελέσματα.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Μη‑Αγγλικές αποδείξεις

Το κύριο παράδειγμα χρησιμοποιεί το `Language.English`. Για πολυγλωσσικές αποδείξεις, ορίστε το `Language` στο κατάλληλο enum (π.χ., `Language.French`) ή χρησιμοποιήστε το `Language.AutoDetect` αν δεν είστε σίγουροι.

### 3. Πολλαπλές αποδείξεις σε μία εικόνα

Ο αναγνωριστής διάταξης του Aspose αναμένει μία μόνο απόδειξη ανά εικόνα. Αν έχετε μια φωτογραφία με πολλές αποδείξεις δίπλα‑δίπλα, θα χρειαστεί να προεπεξεργαστείτε την εικόνα—κόψτε κάθε απόδειξη σε ξεχωριστό αρχείο πριν εκτελέσετε OCR.

### 4. Έλλειψη συμβόλου νομίσματος

Μερικές φορές το συνολικό ποσό εμφανίζεται χωρίς το σύμβολο `$`. Ο αναγνωριστής εξακολουθεί να εντοπίζει αριθμούς, αλλά ίσως χρειαστεί να επεξεργαστείτε τη συμβολοσειρά μετά την εξαγωγή για να εξασφαλίσετε σωστή τοποθέτηση δεκαδικών.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Συμβουλές για Παραγωγή

- **Cache τη μηχανή OCR** εάν επεξεργάζεστε πολλές αποδείξεις σε παρτίδα· η επαναχρησιμοποίηση της ίδιας στιγμής μειώνει το κόστος κατανομής μνήμης.
- **Καταγράψτε το ακατέργαστο κείμενο OCR** (`ocrEngine.Text`) για αρχεία ελέγχου. Είναι χρήσιμο όταν ένα πεδίο αποτυγχάνει να εξαχθεί.
- **Τυλίξτε όλη τη ροή σε try/catch** και εμφανίστε ένα φιλικό μήνυμα σφάλματος (π.χ., “Αδυναμία ανάγνωσης απόδειξης, παρακαλούμε ανεβάστε μια πιο καθαρή εικόνα”).

## Πλήρες Λειτουργικό Παράδειγμα

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να μεταγλωττίσετε και να εκτελέσετε όπως είναι. Απλώς αντικαταστήστε τη διαδρομή της εικόνας και είστε έτοιμοι.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Εκτέλεση του κώδικα**

1. Δημιουργήστε ένα νέο .NET έργο κονσόλας (`dotnet new console -n ReceiptExtractor`).
2. Προσθέστε το πακέτο Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Αντικαταστήστε το παραγόμενο `Program.cs` με το παραπάνω απόσπασμα.
4. Τοποθετήστε μια εικόνα απόδειξης στη διαδρομή που καθορίσατε.
5. Κατασκευάστε και εκτελέστε (`dotnet run`).

Θα πρέπει να δείτε τον έμπορο, την ημερομηνία και το σύνολο να εκτυπώνονται ακριβώς όπως φαίνεται παραπάνω.

## Συμπεράσματα

Σε αυτόν τον οδηγό καλύψαμε **πώς να χρησιμοποιήσετε το Aspose** για **φόρτωση εικόνας απόδειξης**, εκτέλεση **ocr receipt image**, και τελικά **extract receipt data** με μόνο λίγες γραμμές. Το κύριο συμπέρασμα είναι ότι το Aspose.OCR κάνει το σκληρό έργο—αφού έχετε ρυθμίσει τη μηχανή OCR, ο `LayoutRecognizer` μετατρέπει το ακατέργαστο κείμενο σε ένα δομημένο αντικείμενο στο οποίο μπορείτε να εμπιστευτείτε.

Επόμενα βήματα; Δοκιμάστε να αποθηκεύσετε τις εξαγόμενες τιμές σε μια βάση δεδομένων, να δημιουργήσετε μια σύνοψη απόδειξης PDF, ή ακόμη να τις τροφοδοτήσετε σε μοντέλο μηχανικής μάθησης για ταξινόμηση εξόδων. Μπορείτε επίσης να πειραματιστείτε με άλλους δομημένους τύπους εγγράφων όπως τιμολόγια ή ετικέτες αποστολής—το `ExtractInvoiceData` του Aspose λειτουργεί με πολύ παρόμοιο τρόπο.

Έχετε ερωτήσεις σχετικά με περιπτώσεις άκρων ή θέλετε να δείτε πώς να διαχειριστείτε PDF πολλαπλών σελίδων; Αφήστε ένα σχόλιο ή ελέγξτε την επίσημη τεκμηρίωση του Aspose.OCR για προχωρημένα σενάρια. Καλή προγραμματιστική, και απολαύστε την απλότητα του **how to use Aspose** για αυτοματοποίηση αποδείξεων!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}