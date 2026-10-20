---
category: general
date: 2026-01-13
description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα, να φορτώσετε
  εικόνα για OCR και να μορφοποιήσετε την έξοδο JSON χρησιμοποιώντας το Aspose OCR.
  Μάθετε πώς να σειριοποιήσετε ένα αντικείμενο σε JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: el
og_description: c# OCR οδηγός που σας καθοδηγεί στη εξαγωγή κειμένου από εικόνα, τη
  φόρτωση εικόνας για OCR και τη μορφοποίηση της εξόδου JSON με το Aspose OCR.
og_title: c# OCR tutorial – Εξαγωγή κειμένου & μορφοποίηση JSON
tags:
- OCR
- C#
- JSON
title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνα και λήψη μορφοποιημένου JSON
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνα και Μορφοποίηση JSON Εξόδου

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από αρχεία εικόνας** σε ένα έργο C# χωρίς να ασχοληθείτε με χαμηλού επιπέδου επεξεργασία εικονοστοιχείων; Αυτό είναι το πρόβλημα που λύνει αυτό το *c# ocr tutorial*. Σε λίγα μόνο λεπτά θα δείτε πώς να **φορτώσετε εικόνα για OCR**, να εκτελέσετε το Aspose OCR, και να **μορφοποιήσετε την έξοδο JSON** ώστε να τροφοδοτήσετε τα δεδομένα απευθείας στο API ή στη βάση δεδομένων σας.

Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε γιατί κάθε κομμάτι είναι σημαντικό, και ακόμη θα σας δείξουμε το ακριβές JSON που θα πρέπει να περιμένετε. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που μετατρέπει ένα PNG τιμολόγου σε καθαρό, εσοχή JSON. Χωρίς περιττά, μόνο μια πρακτική λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET 6+.

## Τι Καλύπτει αυτό το c# ocr tutorial

- Εγκατάσταση του πακέτου NuGet Aspose.OCR  
- Φόρτωση αρχείου εικόνας για επεξεργασία OCR  
- Αναγνώριση αγγλικού κειμένου (ή οποιασδήποτε υποστηριζόμενης γλώσσας)  
- **Σειριοποίηση του αποτελέσματος OCR σε JSON** με όμορφη εκτύπωση  
- Εμφάνιση του JSON στην κονσόλα και αποθήκευση του εάν το επιθυμείτε  

Απαιτείται μόνο μια βασική κατανόηση του C# και ένα πρόσφατο .NET SDK. Τίποτα άλλο. Αν σας ενδιαφέρει πώς να **εξάγετε κείμενο από εικόνα** για τιμολόγια, αποδείξεις ή σαρωμένες φόρμες, συνεχίστε την ανάγνωση.

---

## Βήμα 1: Ρύθμιση του Περιβάλλοντος του c# ocr tutorial

Πριν γράψετε κώδικα, βεβαιωθείτε ότι έχετε τα σωστά εργαλεία:

1. **.NET 6 SDK ή νεότερο** – μπορείτε να το κατεβάσετε από την ιστοσελίδα της Microsoft.  
2. **Visual Studio 2022** (η έκδοση Community λειτουργεί άψογα) ή οποιονδήποτε επεξεργαστή προτιμάτε.  
3. **Πακέτο NuGet Aspose.OCR** – εκτελέστε `dotnet add package Aspose.OCR` στο φάκελο του έργου σας.

> **Pro tip:** Αν χρησιμοποιείτε CI pipeline, προσθέστε την αναφορά του πακέτου στο `.csproj` ώστε η κατασκευή να το επαναφέρει αυτόματα.

---

## Βήμα 2: Φόρτωση Εικόνας για OCR

Το πρώτο πραγματικό βήμα στο tutorial μας είναι να πάρουμε την εικόνα που θέλουμε να επεξεργαστούμε. Το Aspose OCR λειτουργεί με κοινές μορφές όπως PNG, JPEG και TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας ως `OcrImage` δίνει στη μηχανή πρόσβαση στα δεδομένα bitmap και σε τυχόν πληροφορίες DPI, κάτι που βελτιώνει την ακρίβεια αναγνώρισης. Η παράλειψη αυτού του βήματος ή η χρήση κατεστραμμένου αρχείου θα προκαλέσει εξαίρεση χρόνου εκτέλεσης.

---

## Βήμα 3: Εξαγωγή Κειμένου από Εικόνα

Τώρα εκτελούμε πραγματικά τη μηχανή OCR. Η μέθοδος `Recognize` επιστρέφει ένα πλούσιο αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και λεπτομέρειες διάταξης.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Edge case:** Αν χρειάζεται να επεξεργαστείτε ένα έγγραφο πολλαπλών γλωσσών, καλέστε το `Recognize` δύο φορές με διαφορετικές τιμές `OcrLanguage` και συνδυάστε τα αποτελέσματα. Η μηχανή είναι thread‑safe, οπότε μπορείτε ακόμη και να παραλληλοποιήσετε μεγάλες παρτίδες.

---

## Βήμα 4: Σειριοποίηση Αντικειμένου σε JSON – Μορφοποίηση JSON Εξόδου

Το αντικείμενο `OcrResult` είναι μια απλή κλάση C#, που σημαίνει ότι μπορούμε να το περάσουμε στο `System.Text.Json`. Ενεργοποιώντας το `WriteIndented`, η έξοδος γίνεται αναγνώσιμη από άνθρωπο.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Τι παίρνετε:** Μια ωραία εσοχή JSON string που περιλαμβάνει το αναγνωρισμένο κείμενο, την εμπιστοσύνη και τη διάταξη της σελίδας. Είναι τέλειο για logging, αποστολή σε web service ή αποθήκευση σε NoSQL βάση δεδομένων.

---

## Βήμα 5: Εμφάνιση και (Προαιρετικά) Αποθήκευση του Μορφοποιημένου JSON

Τέλος, εκτυπώνουμε το JSON στην κονσόλα. Μπορείτε επίσης να το γράψετε σε αρχείο με `File.WriteAllText` αν προτιμάτε.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Αναμενόμενη έξοδος κονσόλας (κομμένη για συντομία):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Αν η μηχανή OCR δεν βρει κανένα κείμενο, το πεδίο `Text` θα είναι κενή συμβολοσειρά και το `Confidence` θα είναι `0`. Αυτό είναι ένα καλό σήμα για να ελέγξετε ξανά την ποιότητα της εικόνας.

---

## Βήμα 6: Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια νέα εφαρμογή console:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` από το φάκελο του έργου) και παρακολουθήστε την κονσόλα να εκτυπώνει μια ωραία μορφοποιημένη αναπαράσταση JSON της σαρωμένης απόδειξης σας.

---

## Συνηθισμένα Προβλήματα & Συμβουλές (c# ocr tutorial Extras)

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Κενό πεδίο `Text`** | Η εικόνα έχει χαμηλή αντίθεση ή είναι περιστρεφόμενη. | Προεπεξεργασία της εικόνας (αύξηση αντίθεσης, διόρθωση κλίσης) ή χρήση `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Λείπουν τα εγγενή binaries του Aspose OCR. | Βεβαιωθείτε ότι το πακέτο NuGet επαναφέρθηκε σωστά και ότι η αρχιτεκτονική χρόνου εκτέλεσης (x64/x86) ταιριάζει με το OS σας. |
| **Καθυστέρηση απόδοσης σε μεγάλα PDFs** | Το OCR επεξεργάζεται κάθε σελίδα διαδοχικά. | Παραλληλοποιήστε δημιουργώντας ξεχωριστές `OcrEngine` εμφανίσεις ανά σελίδα (η μηχανή είναι thread‑safe). |
| **JSON πολύ μεγάλο** | Σειριοποιείτε κάθε λεπτομέρεια, συμπεριλαμβανομένων των bounding boxes. | Χρησιμοποιήστε DTO που περιέχει μόνο `Text` και `Confidence` πριν τη σειριοποίηση. |

> **Θυμηθείτε:** Ο στόχος αυτού του tutorial είναι να δείξει μια καθαρή, end‑to‑end ροή. Μπορείτε πάντα να περικόψετε το JSON ή να προσθέσετε περισσότερα μεταδεδομένα αργότερα.

---

## Συμπέρασμα

Μόλις ολοκληρώσατε ένα **c# ocr tutorial** που φορτώνει μια εικόνα, **εξάγει κείμενο από εικόνα**, και παράγει ένα **μορφοποιημένο json output** με **σειριοποίηση αντικειμένου σε json**. Τα βήματα είναι απλά, ο κώδικας είναι έτοιμος για εκτέλεση, και το JSON είναι τέλεια εσοχή για downstream κατανάλωση.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `OcrLanguage.English` με `OcrLanguage.French` ή να τροφοδοτήσετε έναν φάκελο αποδείξεων σε βρόχο. Μπορείτε επίσης να εξερευνήσετε την αποθήκευση του JSON απευθείας σε Azure Blob Storage ή τη χρήση του σε μοντέλο μηχανικής μάθησης.

Αν αντιμετωπίσετε προβλήματα, ελέγξτε ξανά ότι η διαδρομή της εικόνας είναι σωστή και ότι η άδεια Aspose OCR (αν έχετε) έχει φορτωθεί πριν καλέσετε το `Recognize`. Καλή προγραμματιστική δουλειά, και οι OCR αποτελέσματά σας να είναι πάντα καθαρά!

*Εικόνα που απεικονίζει τη ροή OCR (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}