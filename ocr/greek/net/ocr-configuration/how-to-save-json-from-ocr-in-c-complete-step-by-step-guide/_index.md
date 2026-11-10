---
category: general
date: 2026-03-02
description: Μάθετε πώς να αποθηκεύετε JSON ενώ εξάγετε κείμενο από εικόνα χρησιμοποιώντας
  το Aspose OCR. Περιλαμβάνει κώδικα για εγγραφή αρχείου JSON, συμβουλές φόρτωσης
  bitmap εικόνας και πλήρες παράδειγμα C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: el
og_description: Ανακαλύψτε πώς να αποθηκεύετε JSON ενώ εξάγετε κείμενο από εικόνα
  με το Aspose OCR. Πλήρης κώδικας C#, βήματα για τη δημιουργία αρχείου JSON και πρακτικές
  συμβουλές.
og_title: Πώς να αποθηκεύσετε JSON από OCR σε C# – Πλήρης οδηγός προγραμματισμού
tags:
- C#
- OCR
- Aspose
- JSON
title: Πώς να αποθηκεύσετε JSON από OCR σε C# – Πλήρης Οδηγός βήμα‑προς‑βήμα
url: /el/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αποθηκεύσετε JSON από OCR σε C# – Ολοκληρωμένος Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να αποθηκεύσετε JSON** που περιέχει το κείμενο που μόλις εξάγατε από μια εικόνα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να *εξάγουν κείμενο από εικόνα* και στη συνέχεια να διατηρήσουν αυτές τις πληροφορίες ως ένα καλαίσθητα μορφοποιημένο αρχείο JSON. Τα καλά νέα; Η λύση είναι αρκετά απλή μόλις έχετε τα σωστά στοιχεία στη θέση τους.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: χρήση του Aspose.OCR για **εξαγωγή κειμένου από εικόνα**, στη συνέχεια **εγγραφή αρχείου JSON**, και τέλος **πώς να αποθηκεύσετε JSON** στο δίσκο. Καθ' όλη τη διάρκεια θα σας δείξουμε επίσης πώς να **φορτώνετε αντικείμενα bitmap image** σωστά, και θα καλύψουμε μερικές περιπτώσεις άκρων που μπορεί να συναντήσετε. Στο τέλος θα έχετε μια αυτόνομη εφαρμογή C# console που κάνει τα πάντα, από τη φόρτωση της εικόνας μέχρι την παραγωγή ενός έτοιμου προς χρήση εγγράφου JSON.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί με .NET Core και .NET Framework επίσης)
- Aspose.OCR for .NET (μπορείτε να κατεβάσετε ένα δωρεάν trial πακέτο NuGet)
- Ένα δείγμα εικόνας PNG ή JPG που περιέχει αγγλικό κείμενο
- Visual Studio, VS Code ή οποιοδήποτε IDE συμβατό με C#

Δεν απαιτούνται πρόσθετες βιβλιοθήκες — μόνο το τυπικό namespace `System.Drawing` για διαχείριση bitmap και το `System.Text.Json` για σειριοποίηση.

---

## Βήμα 1 – Φόρτωση της Εικόνας Bitmap (το τμήμα “load bitmap image”)

Πριν μπορέσει να γίνει οποιοδήποτε OCR, πρέπει να φορτώσετε την εικόνα στη μνήμη ως `Bitmap`. Σκεφτείτε το σαν το άνοιγμα ενός βιβλίου πριν αρχίσετε να διαβάζετε τις σελίδες του.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Pro tip:** Αν η εικόνα είναι μεγάλη, σκεφτείτε να την αλλάξετε μέγεθος πρώτα για να βελτιώσετε την απόδοση. Η μηχανή OCR λειτουργεί πιο γρήγορα σε εικόνες κάτω των 2 MB.

---

## Βήμα 2 – Διαμόρφωση της Μηχανής Aspose OCR

Τώρα που το bitmap είναι έτοιμο, χρειαζόμαστε ένα `OcrEngine`. Αυτό το αντικείμενο ξέρει πώς να **εξάγει κείμενο από εικόνα** και προαιρετικά να μας δώσει γεωμετρικά δεδομένα όπως τα πλαίσια περιγράμματος.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Γιατί να ενεργοποιήσετε το `ExportBoundingBoxes`; Αν ποτέ χρειαστεί να επισημάνετε λέξεις σε UI, αυτές οι συντεταγμένες είναι πολύτιμες. Αν δεν τις χρειάζεστε, μπορείτε να θέσετε τη σημαία σε `false` και το JSON θα είναι λίγο πιο ελαφρύ.

---

## Βήμα 3 – Εκτέλεση OCR και Λήψη Δομημένου Αποτελέσματος

Με τη μηχανή διαμορφωμένη, το επόμενο βήμα είναι η πραγματική **εξαγωγή κειμένου** λειτουργία. Η μέθοδος `RecognizeToOcrResult` επιστρέφει ένα πλούσιο αντικείμενο που περιέχει το αναγνωρισμένο κείμενο, βαθμολογίες εμπιστοσύνης και προαιρετικά δεδομένα διάταξης.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

Η μεταβλητή `ocrResult` τώρα κρατά όλα όσα χρειάζεστε. Αν την εξετάσετε στον debugger, θα δείτε μια ιεραρχία αντικειμένων `Page`, `Paragraph`, `Line` και `Word`, το καθένα με τη δική του ιδιότητα `Text`.

---

## Βήμα 4 – Σειριοποίηση του Αποτελέσματος σε Μορφοποιημένο Στίγμα JSON

Εδώ αρχίζει πραγματικά η **μαγεία του πώς να αποθηκεύσετε json**. Θα χρησιμοποιήσουμε το `System.Text.Json` επειδή είναι ενσωματωμένο, γρήγορο και υποστηρίζει αυτόματα όμορφη εκτύπωση.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Αν χρειάζεστε διαφορετική σύμβαση ονομασίας (π.χ. camelCase), απλώς προσθέστε `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` στις επιλογές.

---

## Βήμα 5 – Εγγραφή του JSON στο Δίσκο (το βήμα “write json file”)

Τέλος, πραγματικά **εγγράφουμε το αρχείο JSON** στο σύστημα αρχείων. Αυτή είναι η συγκεκριμένη απάντηση στο **πώς να αποθηκεύσετε json** σε περιβάλλον C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Μετά την εκτέλεση αυτής της γραμμής, θα βρείτε ένα όμορφα εσοχισμένο `sample-page.json` δίπλα στην αρχική σας εικόνα. Ανοίξτε το με οποιονδήποτε επεξεργαστή κειμένου ή δώστε το σε άλλη υπηρεσία — τα δεδομένα OCR είναι τώρα φορητά.

---

## Βήμα 6 – Επαλήθευση του Αποτελέσματος (Τι Πρέπει να Δείτε;)

Η εκτέλεση του προγράμματος θα πρέπει να εκτυπώσει μια σύντομη επιβεβαίωση στην κονσόλα:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Ανοίξτε το παραγόμενο αρχείο JSON και θα δείτε κάτι σαν:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Αν η σημαία `ExportBoundingBoxes` ήταν `true`, κάθε λέξη θα περιέχει επίσης συντεταγμένες `Rectangle`. Αυτό είναι χρήσιμο για επόμενη εργασία UI.

---

## Συχνές Ερωτήσεις & Περιπτώσεις Άκρων

### Τι γίνεται αν η διαδρομή της εικόνας είναι άκυρη;

Τυλίξτε τη φόρτωση του bitmap σε ένα μπλοκ `try/catch` και εμφανίστε ένα σαφές σφάλμα:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Πώς να χειριστώ μη‑αγγλικές γλώσσες;

Απλώς αλλάξτε την ιδιότητα `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Το Aspose υποστηρίζει πάνω από 50 γλώσσες, οπότε επιλέξτε αυτή που ταιριάζει στο υλικό σας.

### Χρειάζεται να απελευθερώσω τα αντικείμενα `Bitmap`;

Ναι. Το `Bitmap` υλοποιεί το `IDisposable`, οπότε τυλίξτε το σε δήλωση `using` για να ελευθερώσετε άμεσα τους εγγενείς πόρους.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Τι κάνω αν θέλω ένα συμπαγές JSON χωρίς εσοχές;

Αντικαταστήστε τις `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Αυτό μειώνει το μέγεθος του αρχείου — χρήσιμο για σενάρια με περιορισμένο εύρος ζώνης.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που ενσωματώνει όλα τα βήματα, τον χειρισμό σφαλμάτων και τις καλύτερες πρακτικές που συζητήθηκαν παραπάνω. Αποθηκεύστε το ως `Program.cs` και τρέξτε το από τη γραμμή εντολών ή το IDE σας.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Τι κάνει αυτό:**  
1. Ελέγχει αν η εικόνα υπάρχει.  
2. Την φορτώνει με ασφάλεια μέσα σε μπλοκ `using`.  
3. Εκτελεί OCR για **εξαγωγή κειμένου από εικόνα**.  
4. Σειριοποιεί το αποτέλεσμα σε ένα όμορφα εσοχισμένο στίγμα JSON.  
5. Αποθηκεύει αυτό το στίγμα στο δίσκο, απαντώντας στην κεντρική ερώτηση **πώς να αποθηκεύσετε json**.

Τρέξτε `dotnet run` (ή πατήστε F5 στο Visual Studio) και θα δείτε το μήνυμα επιβεβαίωσης μόλις το αρχείο γραφτεί.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή συνταγή για **πώς να αποθηκεύσετε JSON** που προέρχεται από εξαγωγή κειμένου με OCR. Από τη φόρτωση μιας εικόνας bitmap μέχρι την εγγραφή ενός καθαρού αρχείου JSON, κάθε βήμα εξηγείται με το «γιατί» πίσω από τον κώδικα, ώστε να μπορείτε να προσαρμόσετε τη λύση στα δικά σας έργα.  

Αν θέλετε να εξερευνήσετε το επόμενο βήμα, σκεφτείτε:

- **Πώς να εξάγετε κείμενο** από PDF μετατρέποντας κάθε σελίδα σε εικόνα πρώτα.  
- Χρήση των δεδομένων πλαισίου για επισήμανση λέξεων σε UI WPF ή WinForms.  
- Ροή του JSON απευθείας σε web API αντί για εγγραφή αρχείου (χρήση `HttpClient`).

Δοκιμάστε το, προσαρμόστε τις επιλογές, και αφήστε τα δεδομένα OCR να τροφοδοτήσουν ό,τι εφαρμογή χτίζετε. Έχετε ερωτήσεις; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}