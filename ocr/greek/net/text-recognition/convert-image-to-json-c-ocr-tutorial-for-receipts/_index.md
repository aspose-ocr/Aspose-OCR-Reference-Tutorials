---
category: general
date: 2026-04-11
description: Μετατρέψτε την εικόνα σε JSON χρησιμοποιώντας το Aspose OCR Cloud σε
  C#. Μάθετε πώς να αναγνωρίζετε κείμενο, να εξάγετε κείμενο από εικόνα και να επεξεργάζεστε
  αποδείξεις με OCR σε λίγα λεπτά.
draft: false
keywords:
- convert image to json
- how to recognize text
- extract text from image
- c# ocr tutorial
- process receipt with ocr
language: el
og_description: Μετατρέψτε την εικόνα σε JSON με το Aspose OCR Cloud σε C#. Αυτός
  ο οδηγός δείχνει πώς να αναγνωρίζετε κείμενο, να εξάγετε κείμενο από εικόνα και
  να επεξεργάζεστε απόδειξη με OCR.
og_title: Μετατροπή εικόνας σε JSON – Εκπαίδευση OCR με C# για αποδείξεις
tags:
- OCR
- C#
- Aspose
- JSON
title: Μετατροπή εικόνας σε JSON – Οδηγός OCR σε C# για αποδείξεις
url: /el/net/text-recognition/convert-image-to-json-c-ocr-tutorial-for-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή εικόνας σε JSON – C# OCR Tutorial για αποδείξεις

Έχετε ποτέ χρειαστεί να **convert image to JSON** αλλά δεν ήξερες από πού να ξεκινήσεις; Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε βήμα‑βήμα σε ένα πλήρες, end‑to‑end C# OCR tutorial που παίρνει μια φωτογραφία από μια απόδειξη, αναγνωρίζει το κείμενο και παράγει ένα καθαρό JSON payload.  

Αν έχετε ποτέ αναρωτηθεί *how to recognize text* σε ένα σαρωμένο έγγραφο, ή ψάχνετε έναν γρήγορο τρόπο να **extract text from image** αρχεία, βρίσκεστε στο σωστό μέρος. Στο τέλος αυτού του άρθρου θα μπορείτε να **process receipt with OCR** και να τροφοδοτήσετε το αποτέλεσμα απευθείας στα downstream APIs σας.

## Τι θα χρειαστείτε

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core)  
- Ένα κλειδί Aspose Cloud API – μπορείτε να πάρετε μια δωρεάν δοκιμή από το portal της Aspose  
- Ένα δείγμα εικόνας απόδειξης (`receipt.jpg`) αποθηκευμένο τοπικά  
- Το αγαπημένο σας IDE (Visual Studio, VS Code, Rider – όποιο και αν είναι)

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από τον επίσημο πελάτη `Aspose.OCR.Cloud`. Αν έχετε ήδη εγκατεστημένο το SDK, είστε έτοιμοι να ξεκινήσετε.

## Βήμα 1 – Convert Image to JSON: Ρύθμιση του OCR Client

Πρώτα απ' όλα, χρειαζόμαστε μια παρουσία του `CloudOcrClient`. Αυτό το αντικείμενο διαχειρίζεται όλη την επικοινωνία με την υπηρεσία OCR της Aspose και θα επιστρέψει το αποτέλεσμα σε μορφή JSON.

```csharp
using Aspose.OCR.Cloud;
using System;
using System.Threading.Tasks;

class CloudDemo
{
    static async Task Main()
    {
        // 👉 Replace with your real API key – keep it secret!
        var ocrClient = new CloudOcrClient("YOUR_API_KEY");

        // The path to the receipt you want to process
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";

        // Send the image for recognition (English language in this example)
        var ocrResultJson = await ocrClient.RecognizeAsync(imagePath, Language.English);

        // Show the raw JSON response
        Console.WriteLine(ocrResultJson);
    }
}
```

**Why this matters:** Η αρχικοποίηση του client είναι η γέφυρα μεταξύ του κώδικα C# και της cloud OCR μηχανής. Η μέθοδος `RecognizeAsync` κάνει τη βαριά δουλειά – ανεβάζει την εικόνα, εκτελεί την OCR μηχανή και επιστρέφει μια JSON συμβολοσειρά που περιέχει το αναγνωρισμένο κείμενο, τις βαθμολογίες εμπιστοσύνης και τις συντεταγμένες του bounding‑box.

> **Pro tip:** Αποθηκεύστε το κλειδί API σε μια μεταβλητή περιβάλλοντος ή σε διαχειριστή μυστικών αντί να το κωδικοποιήσετε σκληρά. Με αυτόν τον τρόπο αποφεύγετε τυχαίες διαρροές.

## Βήμα 2 – How to Recognize Text from the Receipt

Τώρα που ο client είναι έτοιμος, ας εμβαθύνουμε στο *how* πίσω από την αναγνώριση κειμένου. Το Aspose OCR υποστηρίζει πολλές γλώσσες, αλλά για τις περισσότερες αποδείξεις τα Αγγλικά λειτουργούν καλά. Αν χρειάζεστε άλλη γλώσσα, απλώς αντικαταστήστε το `Language.English` με την κατάλληλη τιμή enum.

```csharp
// Example: Recognize a Spanish receipt
var spanishResult = await ocrClient.RecognizeAsync(imagePath, Language.Spanish);
Console.WriteLine(spanishResult);
```

**What’s happening under the hood?** Η υπηρεσία εκτελεί ένα μοντέλο deep‑learning που εντοπίζει χαρακτήρες, τους ομαδοποιεί σε λέξεις και στη συνέχεια συναρμολογεί γραμμές. Το JSON που επιστρέφεται φαίνεται περίπου έτσι:

```json
{
  "text": "Total $12.34\nDate 04/10/2026\n...",
  "confidence": 0.97,
  "regions": [
    { "boundingBox": "10,20,200,30", "text": "Total $12.34" },
    { "boundingBox": "10,60,200,30", "text": "Date 04/10/2026" }
  ]
}
```

Μπορείτε να αναλύσετε αυτό το JSON με `System.Text.Json` ή `Newtonsoft.Json` για να εξάγετε τα πεδία που σας ενδιαφέρουν.

## Βήμα 3 – Extract Text from Image and Build JSON Manually (Optional)

Μερικές φορές δεν θέλετε το ακατέργαστο JSON που σας παρέχει η Aspose· ίσως χρειάζεστε μια προσαρμοσμένη δομή για την downstream υπηρεσία σας. Παρακάτω υπάρχει ένα γρήγορο παράδειγμα που απο‑σειριοποιεί την απάντηση και την ξανασυσκευάζει σε ένα πιο καθαρό αντικείμενο.

```csharp
using System.Text.Json;

// Define a lightweight model for the data you actually need
public class ReceiptData
{
    public string Total { get; set; }
    public string Date { get; set; }
}

// Helper method to parse the Aspose JSON
static ReceiptData ParseReceipt(string rawJson)
{
    using JsonDocument doc = JsonDocument.Parse(rawJson);
    string text = doc.RootElement.GetProperty("text").GetString();

    // Very naive parsing – just for demo purposes
    var lines = text.Split('\n', StringSplitOptions.RemoveEmptyEntries);
    var data = new ReceiptData();

    foreach (var line in lines)
    {
        if (line.Contains("Total"))
            data.Total = line.Split(' ')[1];
        else if (line.Contains("Date"))
            data.Date = line.Split(' ')[1];
    }

    return data;
}

// Inside Main after getting ocrResultJson
var receipt = ParseReceipt(ocrResultJson);
string finalJson = JsonSerializer.Serialize(receipt, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine("Custom JSON output:");
Console.WriteLine(finalJson);
```

**Why re‑format?** Πολλά APIs αναμένουν ένα συγκεκριμένο σχήμα (π.χ., `{ \"total\": \"12.34\", \"date\": \"2026-04-10\" }`). Εξάγοντας μόνο τα πεδία που χρειάζεστε, διατηρείτε το payload ελαφρύ και αποτρέπετε τη διαρροή περιττών OCR μεταδεδομένων.

## Βήμα 4 – Test the C# OCR Tutorial with a Sample Receipt

Εκτελέστε το πρόγραμμα από το τερματικό σας:

```bash
dotnet run
```

Θα πρέπει να δείτε δύο μπλοκ εξόδου:

1. Το ακατέργαστο JSON που επιστρέφει η Aspose (το **convert image to json** αποτέλεσμα απευθείας από το cloud).  
2. Το προσαρμοσμένο JSON που δημιουργήσατε στο προηγούμενο βήμα.

Η τυπική έξοδος μοιάζει με:

```
{
  "text":"Total $12.34\nDate 04/10/2026\n...",
  "confidence":0.97,
  ...
}
Custom JSON output:
{
  "Total": "$12.34",
  "Date": "04/10/2026"
}
```

Αν λάβετε σφάλμα όπως *401 Unauthorized*, ελέγξτε ξανά ότι το κλειδί API είναι έγκυρο και ότι η διαδρομή της εικόνας είναι σωστή.

## Περιπτώσεις Άκρων & Συνηθισμένα Σφάλματα

| Κατάσταση | Τι να προσέξετε | Προτεινόμενη Διόρθωση |
|-----------|------------------|------------------------|
| **Απόδειξη χαμηλής ανάλυσης** | Η εμπιστοσύνη OCR πέφτει κάτω από 0.8 | Προεπεξεργαστείτε την εικόνα (αυξήστε DPI, ενισχύστε την ευκρίνεια) πριν την αποστείλετε |
| **Μη‑Αγγλικοί χαρακτήρες** | Λάθος enum γλώσσας | Χρησιμοποιήστε `Language.AutoDetect` ή καθορίστε τη σωστή γλώσσα |
| **Μεγάλο batch αποδείξεων** | Σφάλματα περιορισμού ταχύτητας | Εφαρμόστε εκθετική καθυστέρηση ή ζητήστε υψηλότερο όριο από την Aspose |
| **Λείπουν πεδία** | Ο προσαρμοσμένος parser επιστρέφει `null` | Προσθέστε λογική fallback ή regex μοτίβα για πιο αξιόπιστη εξαγωγή |

## Οπτική Επισκόπηση

![Διάγραμμα που δείχνει τη ροή από αρχείο εικόνας → OCR client → JSON response → custom parsing → final JSON output](https://example.com/ocr-flow-diagram.png "convert image to json")

*Alt text:* *convert image to json flow diagram illustrating the steps covered in this tutorial.*

## Σύνοψη

Σας δείξαμε πώς να **convert image to JSON** με το Aspose OCR Cloud, εξηγήσαμε *how to recognize text* σε μια απόδειξη, παρουσιάσαμε τρόπους για **extract text from image**, και τυλίξαμε τα πάντα σε ένα καθαρό **C# OCR tutorial** που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.  

Τα βασικά σημεία είναι:

- Ρυθμίστε το `CloudOcrClient` με το κλειδί API σας.  
- Καλέστε το `RecognizeAsync` για να λάβετε ένα JSON payload απευθείας από την υπηρεσία.  
- Προαιρετικά, προσαρμόστε το payload ώστε να ταιριάζει με το δικό σας συμβόλαιο δεδομένων.

## Τι Ακολουθεί;

- **Batch processing:** Επανάληψη σε έναν φάκελο αποδείξεων και συγκέντρωση των αποτελεσμάτων σε έναν ενιαίο πίνακα JSON.  
- **Advanced parsing:** Χρησιμοποιήστε κανονικές εκφράσεις ή ένα μικρό μοντέλο NLP για να εξάγετε στοιχεία γραμμής, φόρους και εκπτώσεις.  
- **Integration:** Σπρώξτε το τελικό JSON σε μια βάση δεδομένων, μια ουρά μηνυμάτων ή μια Azure Function για περαιτέρω αυτοματοποίηση.  

Μη διστάσετε να πειραματιστείτε με διαφορετικές μορφές εικόνας (PNG, TIFF) ή να δοκιμάσετε τη ροή **process receipt with OCR** σε φωτογραφίες που έχουν ληφθεί με κινητό. Ο ουρανός είναι το όριο μόλις έχετε έναν αξιόπιστο τρόπο να **convert image to JSON**.

Έχετε ερωτήσεις ή αντιμετωπίσατε πρόβλημα; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}