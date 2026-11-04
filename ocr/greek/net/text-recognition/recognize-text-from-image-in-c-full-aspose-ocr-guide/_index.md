---
category: general
date: 2026-04-03
description: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να εξάγετε κείμενο από την εικόνα, να γράφετε αρχείο
  JSON σε C# και να εκτελείτε OCR σε PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: el
og_description: αναγνωρίστε κείμενο από εικόνα με Aspose OCR σε C#. Οδηγός βήμα‑βήμα
  για τη φόρτωση εικόνας για OCR, την εξαγωγή κειμένου από την εικόνα, τη δημιουργία
  αρχείου JSON σε C# και την εκτέλεση OCR σε PNG.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρες Μάθημα Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρης Οδηγός Aspose OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε C# – Πλήρες Μάθημα Aspose OCR

Ποτέ χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερες ποια βιβλιοθήκη να επιλέξεις; Ίσως έχεις μια σειρά από σαρωμένες αποδείξεις, ένα στιγμιότυπο PNG ή ένα χειρόγραφο σημείωμα που θέλεις να μετατρέψεις σε αναζητήσιμα δεδομένα. Τα καλά νέα: με το Aspose.OCR μπορείς να το κάνεις με λίγες γραμμές κώδικα C#, και θα πάρεις ακόμη και ένα τακτοποιημένο αρχείο JSON που μπορείς να τροφοδοτήσεις σε άλλα συστήματα.

Σε αυτό το μάθημα θα δούμε πώς να φορτώνουμε μια εικόνα για OCR, να εξάγουμε κείμενο από την εικόνα, να σειριοποιήσουμε το αποτέλεσμα σε αρχείο JSON και, τέλος, πώς να χειριζόμαστε αρχεία PNG χωρίς προβλήματα. Στο τέλος θα έχεις μια έτοιμη εφαρμογή κονσόλας που **αναγνωρίζει κείμενο από εικόνα** και γράφει το αποτέλεσμα στο *output.json*.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και με .NET Framework)
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Ένα PNG (ή οποιαδήποτε υποστηριζόμενη μορφή) που θέλετε να επεξεργαστείτε
- Visual Studio, VS Code ή οποιονδήποτε επεξεργαστή C# προτιμάτε

Δεν απαιτούνται πρόσθετες βιβλιοθήκες τρίτων—μόνο η μηχανή Aspose OCR και ο ενσωματωμένος σειριοποιητής `System.Text.Json`.

## Βήμα 1: Αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο κάνει το βαριά δουλειά στο παρασκήνιο.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Γιατί είναι σημαντικό:** Η δημιουργία ενός `OcrEngine` μία φορά και η επαναχρησιμοποίησή του είναι πιο αποδοτική από το να δημιουργείτε νέο engine για κάθε αρχείο. Η κλήση `RecognizeToResult` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει ήδη το εξαγόμενο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα πλαίσια περιορισμού—τέλειο για επεξεργασία downstream.

## Βήμα 2: Φορτώστε εικόνα για OCR – διαχείριση διαφορετικών μορφών

Το Aspose OCR μπορεί να διαβάσει PNG, JPEG, BMP και πολλές άλλες μορφές. Αν δουλεύετε με PNG που περιέχει διαφάνεια, ίσως θελήσετε να το «ισοπεδώσετε» πρώτα για να αποφύγετε απρόσμενα κενά.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Συμβουλή:** Πάντα ελέγχετε ότι οι διαστάσεις της εικόνας είναι λογικές (π.χ., πλάτος > 50 px). Πολύ μικρές εικόνες μπορούν να κάνουν το OCR engine να χάσει χαρακτήρες, οδηγώντας σε χαμηλές βαθμολογίες εμπιστοσύνης.

## Βήμα 3: Γράψτε αρχείο JSON C# – κάντε το αποτέλεσμα καταναλώσιμο

Ο σειριοποιητής `System.Text.Json` είναι γρήγορος και ενσωματωμένος, αλλά μπορείτε να τον αντικαταστήσετε με `Newtonsoft.Json` αν χρειάζεστε προσαρμοσμένους μετατροπείς. Το παραπάνω παράδειγμα χρησιμοποιεί ήδη `WriteIndented = true` ώστε το αρχείο να είναι αναγνώσιμο από άνθρωπο.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Το να έχετε τα δεδομένα OCR σε JSON σας επιτρέπει να τα εισάγετε εύκολα σε βάσεις δεδομένων, να τα στείλετε μέσω HTTP ή να τα τροφοδοτήσετε σε pipelines μηχανικής μάθησης.

## Βήμα 4: Επαληθεύστε το αποτέλεσμα – γρήγορος έλεγχος λογικής

Αφού τρέξει το πρόγραμμα, ανοίξτε το `output.json` και ψάξτε για το πεδίο `"Text"`. Αν περιέχει το αναμενόμενο κείμενο, έχετε **εξάγει κείμενο από εικόνα** επιτυχώς. Αν η εμπιστοσύνη είναι χαμηλή, σκεφτείτε προεπεξεργασία της εικόνας (π.χ., αύξηση αντίθεσης ή εφαρμογή δυαδικού κατωφλίου).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

Η εκτέλεση της κονσόλας θα εμφανίσει κάτι όπως:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Αυτό είναι ένα σαφές σημάδι ότι το OCR λειτούργησε όπως αναμενόταν.

## Συνηθισμένα Προβλήματα & Ακραίες Περιπτώσεις

| Πρόβλημα | Γιατί συμβαίνει | Πώς να διορθώσετε |
|----------|----------------|-------------------|
| **Κενό αποτέλεσμα** | Η εικόνα είναι πολύ σκοτεινή ή έχει μη υποστηριζόμενο χρωματικό χώρο | Μετατρέψτε σε γκρι, αυξήστε τη φωτεινότητα ή ισοπεδώστε το PNG (δείτε το Βήμα 2) |
| **Ασχετοί χαρακτήρες** | Χαμηλό DPI (< 72) ή έντονος θόρυβος | Μεγαλώστε την εικόνα ή εφαρμόστε φίλτρο αποθορυβοποίησης πριν την περάσετε στο `RecognizeToResult` |
| **Μεγάλα αρχεία προκαλούν πίεση μνήμης** | Η φόρτωση ενός PNG πολλαπλών megapixel σε `Bitmap` καταναλώνει RAM | Επεξεργαστείτε τις εικόνες σε τμήματα ή μειώστε την ανάλυση διατηρώντας την αναγνωσιμότητα |
| **Σφάλμα σειριοποίησης JSON** | Το `OcrResult` περιέχει κυκλικές αναφορές (σπάνιο) | Χρησιμοποιήστε `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Bonus: Εκτέλεση OCR σε PNG σε βρόχο παρτίδας

Αν έχετε έναν φάκελο γεμάτο PNG αρχεία, μπορείτε να επεκτείνετε το demo ώστε να τα επεξεργάζεται όλα:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Τώρα το πρόγραμμα **εκτελεί OCR σε PNG** μαζικά, γράφοντας ένα αντίστοιχο αρχείο JSON για κάθε εικόνα.

## Συμπέρασμα

Μόλις μάθατε πώς να **αναγνωρίζετε κείμενο από εικόνα** σε C# με Aspose OCR, **φορτώνετε εικόνα για OCR**, **εξάγετε κείμενο από εικόνα**, και **γράφετε αρχείο JSON C#** για αποθήκευση των αποτελεσμάτων. Το πλήρες, εκτελέσιμο παράδειγμα καλύπτει τα βασικά βήματα, εξηγεί γιατί κάθε μέρος είναι σημαντικό και δείχνει πώς να χειρίζεστε ειδικές ιδιαιτερότητες του PNG.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να τροφοδοτήσετε το JSON σε ευρετήριο αναζήτησης, να το συνδυάσετε με ανίχνευση γλώσσας ή να το ενσωματώσετε σε web API που επεξεργάζεται μεταφορτώσεις σε πραγματικό χρόνο. Μπορείτε επίσης να εξερευνήσετε την υποστήριξη του Aspose για αναγνώριση χειρογράφου αν η περίπτωση χρήσης σας το απαιτεί.

Έχετε ερωτήσεις σχετικά με ακραίες περιπτώσεις ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική! 

![επίδειξη αναγνώρισης κειμένου από εικόνα](/images/ocr-demo.png "Diagram showing how Aspose OCR recognizes text from image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}