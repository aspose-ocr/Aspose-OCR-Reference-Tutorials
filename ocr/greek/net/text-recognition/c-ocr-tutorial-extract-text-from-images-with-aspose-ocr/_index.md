---
category: general
date: 2026-02-20
description: c# OCR tutorial που δείχνει πώς να εξάγετε κείμενο από εικόνα, να αναγνωρίζετε
  κείμενο από PNG και να μετατρέπετε την εικόνα σε κείμενο με λίγες μόνο γραμμές κώδικα.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: el
og_description: c# OCR tutorial που σας καθοδηγεί στη εξαγωγή κειμένου από αρχεία
  εικόνας, στην αναγνώριση κειμένου από PNG και στη μετατροπή εικόνων σε κείμενο χρησιμοποιώντας
  το Aspose.OCR.
og_title: c# OCR tutorial – Γρήγορος οδηγός για την εξαγωγή κειμένου από εικόνες
tags:
- OCR
- C#
- Aspose
title: c# OCR οδηγός – Εξαγωγή κειμένου από εικόνες με το Aspose.OCR
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνες με Aspose.OCR

Ποτέ χρειάστηκε ένα **c# ocr tutorial** που να λειτουργεί σε πραγματικό αρχείο PNG; Δεν είστε ο μόνος. Σε πολλά έργα—σκεφτείτε σάρωση τιμολογίων, αρχειοθέτηση αποδείξεων ή απλή ανάλυση στιγμιότυπων—οι προγραμματιστές συναντούν εμπόδιο όταν προσπαθούν να **extract text from image** αρχεία χωρίς αξιόπιστη βιβλιοθήκη.  

Τα καλά νέα είναι ότι το Aspose.OCR κάνει όλη τη διαδικασία παιδικό παιχνίδι. Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **how to extract text** από ένα PNG, εξηγεί *γιατί* κάθε γραμμή είναι σημαντική, και ακόμη αγγίζει περιπτώσεις όπως η αδειοδότηση και η προεπεξεργασία εικόνας. Στο τέλος θα μπορείτε να **recognize text from png** αρχεία και να **convert image to text** με λίγες μόνο δηλώσεις C#.

## What This Tutorial Covers

- Ρύθμιση του κινητήρα Aspose.OCR σε μια .NET console εφαρμογή.  
- Φόρτωση ενός PNG (ή οποιουδήποτε υποστηριζόμενου bitmap) από το δίσκο.  
- Εκτέλεση OCR και εκτύπωση του αποτελέσματος στην κονσόλα.  
- Προαιρετική αδειοδότηση, διαχείριση σφαλμάτων και συμβουλές απόδοσης.  

Καμία εξωτερική υπηρεσία, καμία κρυφή μαγεία—απλός κώδικας C# που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε. Αν ποτέ αναρωτηθήκατε **how to extract text** από ένα σαρωμένο έγγραφο, μείνετε μαζί μας· θα απαντήσουμε σε αυτό και σε μερικές ερωτήσεις “τι θα γίνει αν…”.

## Prerequisites

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε).  
- Ένα δωρεάν ή επί πληρωμή πακέτο Aspose.OCR for .NET από το NuGet.  
- Ένα αρχείο εικόνας με όνομα `sample.png` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.  

Αυτό είναι όλο—δεν απαιτούνται άλλα εργαλεία τρίτων.

## c# OCR Tutorial: Setting Up Aspose.OCR

Πρώτα απ’ όλα: χρειάζεστε τη βιβλιοθήκη Aspose.OCR. Ανοίξτε το τερματικό σας στον φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτό κατεβάζει την πιο πρόσφατη σταθερή έκδοση και προσθέτει τις απαραίτητες αναφορές DLL. Αν έχετε αρχείο άδειας (`Aspose.OCR.lic`), κρατήστε το κοντά· διαφορετικά η δωρεάν δοκιμή θα λειτουργήσει, αλλά με υδατογράφημα στο αποτέλεσμα του OCR.

### Why a License Matters

Χωρίς άδεια η μηχανή λειτουργεί σε λειτουργία αξιολόγησης, η οποία προσθέτει τη γραμμή “Powered by Aspose” στο αποτέλεσμα για ορισμένες γλώσσες. Για κώδικα παραγωγής θα θέλετε να καλέσετε το `SetLicense` νωρίς, όπως φαίνεται στον κώδικα παρακάτω. Είναι μια κλήση μίας γραμμής, αλλά αφαιρεί το υδατογράφημα και ξεκλειδώνει την πλήρη ταχύτητα επεξεργασίας.

## Extract Text from Image Using Aspose.OCR

Τώρα ας βουτήξουμε στον πραγματικό κώδικα OCR. Παρακάτω υπάρχει ένα **complete, self‑contained** πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως.

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**What’s happening here?**  

1. **Engine creation** – `OcrEngine` είναι το κύριο σημείο εισόδου· φορτώνει τα δεδομένα γλώσσας εσωτερικά.  
2. **License loading** – προαιρετικό αλλά συνιστάται· απλώς δείχνετε στο αρχείο `.lic`.  
3. **Image loading** – `Image.FromFile` λειτουργεί για οποιαδήποτε μορφή bitmap· χρησιμοποιούμε PNG επειδή διατηρεί την απώλεια‑απώλειας ποιότητα, κάτι κρίσιμο για την ακρίβεια του OCR.  
4. **Recognition** – `ocrEngine.Recognize` κάνει όλη τη βαριά δουλειά, επιστρέφοντας μια συμβολοσειρά που περιέχει τους ανιχνευμένους χαρακτήρες.  
5. **Output** – γράφουμε το αποτέλεσμα στην κονσόλα, αλλά μπορείτε εύκολα να το αποθηκεύσετε σε αρχείο, βάση δεδομένων ή στοιχείο UI.

### Expected Output

Αν το `sample.png` περιέχει το κείμενο “Hello World”, η κονσόλα θα εμφανίσει:

```
=== OCR Result ===
Hello World
```

Αν η εικόνα είναι θολή ή περιέχει μη‑λατινικούς χαρακτήρες, το αποτέλεσμα μπορεί να περιλαμβάνει ακατάλληλα σύμβολα. Εκεί έρχεται η προεπεξεργασία (ρύθμιση αντίθεσης, δυαδικοποίηση) — καλυμμένη στην επόμενη ενότητα.

## Recognize Text from PNG Files – Tips & Tricks

Το PNG είναι δημοφιλής μορφή επειδή αποθηκεύει εικονοστοιχεία χωρίς συμπιεστικά artefacts. Παρόλα αυτά, δεν είναι όλα τα PNG ίσα. Εδώ είναι μερικές πρακτικές συμβουλές που μπορεί να βρείτε χρήσιμες:

- **Resolution matters** – Στοχεύστε τουλάχιστον 300 dpi. Οτιδήποτε χαμηλότερο μπορεί να προκαλέσει χαμένα χαρακτήρες.  
- **Color vs. Grayscale** – Η μετατροπή ενός έγχρωμου PNG σε γκρι κλίμακα πριν το OCR μπορεί να βελτιώσει την ταχύτητα χωρίς να βλάψει την ακρίβεια.  
- **Noise removal** – Μικρές κηλίδες συχνά μπερδεύουν τη μηχανή· ένα απλό median filter μπορεί να βοηθήσει.

Παρακάτω υπάρχει ένα γρήγορο απόσπασμα που δείχνει πώς να προεπεξεργαστείτε μια εικόνα πριν τη δώσετε στο Aspose.OCR:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro tip:** Αν επεξεργάζεστε δεκάδες εικόνες, δημιουργήστε ένα μόνο `OcrEngine` και επαναχρησιμοποιήστε το. Η δημιουργία νέας μηχανής ανά εικόνα προσθέτει περιττό κόστος.

## Convert Image to Text – Advanced Options

Το Aspose.OCR δεν περιορίζεται στην απλή εξαγωγή κειμένου. Μπορείτε να του ζητήσετε να επιστρέψει **structured data** (όπως τα πλαίσια των λέξεων) ή να ορίσετε **language hints** για βελτιωμένη ακρίβεια σε πολυγλωσσικά έγγραφα.

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

Το αντικείμενο `OcrResult` σας δίνει τις συντεταγμένες κάθε λέξης, κάτι χρήσιμο για επισήμανση κειμένου σε UI ή για μετα‑επεξεργασία (π.χ., διαγραφή ευαίσθητων πληροφοριών).

## How to Extract Text in Real‑World Scenarios

Ας αντιμετωπίσουμε μερικές ερωτήσεις “τι θα γίνει αν…” που συχνά εμφανίζονται σε περιβάλλον παραγωγής.

### What if the image is a PDF page?

Το Aspose.OCR μπορεί να διαβάσει PDF απευθείας, αλλά θα χρειαστείτε τη βιβλιοθήκη Aspose.PDF για να rasterize κάθε σελίδα σε εικόνα πρώτα. Η ροή εργασίας είναι:

1. Φόρτωση PDF με `Aspose.Pdf.Document`.  
2. Μετατροπή μιας σελίδας σε bitmap (`PdfConverter`).  
3. Παροχή του bitmap στο `OcrEngine.Recognize`.

### What if the OCR result contains garbage characters?

Τυπικές αιτίες είναι χαμηλή ανάλυση, υπερβολικός θόρυβος ή μη υποστηριζόμενες γραμματοσειρές. Δοκιμάστε:

- Αύξηση της ανάλυσης της εικόνας (`Bitmap` resizing).  
- Εφαρμογή φίλτρου sharpening.  
- Καθορισμός της σωστής γλώσσας (όπως φαίνεται παραπάνω).  

### What if I need to process images in parallel?

Επειδή το `OcrEngine` δεν είναι thread‑safe, δημιουργήστε μια **ξεχωριστή παρουσία ανά νήμα** ή χρησιμοποιήστε μια thread‑local πισίνα. Παράδειγμα με `Parallel.ForEach`:

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## Complete Working Example

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια συμπαγής έκδοση που μπορείτε να τοποθετήσετε σε ένα νέο console project:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

Μεταγλωττίστε με `dotnet run` και παρακολουθήστε την κονσόλα να εκτυπώνει το εξαγόμενο κείμενο. Απλό, έτσι; Αυτή είναι η ομορφιά ενός καλά σχεδιασμένου...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}