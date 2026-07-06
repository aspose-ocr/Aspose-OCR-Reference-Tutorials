---
category: general
date: 2026-04-03
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέψετε σαρωμένη εικόνα, να φορτώσετε αρχείο εικόνας σε C# και να αναγνωρίσετε
  κείμενο από TIF ασύγχρονα.
draft: false
keywords:
- extract text from image
- convert scanned image
- how to ocr image
- load image file c#
- recognize text from tif
language: el
og_description: Εξαγωγή κειμένου από εικόνα με το Aspose OCR σε C#. Αυτός ο οδηγός
  δείχνει πώς να μετατρέψετε σαρωμένη εικόνα, να φορτώσετε αρχείο εικόνας σε C# και
  να αναγνωρίσετε κείμενο από TIF χρησιμοποιώντας ασύγχρονες κλήσεις.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Async OCR οδηγός
tags:
- OCR
- C#
- Aspose
- Async
title: Εξαγωγή κειμένου από εικόνα σε C# – Async OCR Tutorial
url: /el/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Async OCR Tutorial

Need to **extract text from image** quickly? With Aspose OCR you can do it in C# using async calls, and the whole process finishes before you’ve even finished your coffee.  
If you’re also wondering how to **convert scanned image** files or load an image file in C# without breaking a sweat, you’re in the right place.

In this guide we’ll walk through every step—from pulling a TIF off disk to getting clean, searchable text back. By the end you’ll be able to **recognize text from TIF** files, understand the nuances of loading different image formats, and have a solid async pattern you can reuse in any .NET project.

## Τι Θα Μάθετε

* Πώς να ρυθμίσετε τη μηχανή Aspose OCR για ασύγχρονη χρήση.  
* Ο ακριβής κώδικας που χρειάζεστε για **load image file C#**‑style, συμπεριλαμβανομένου του χειρισμού σφαλμάτων για ελλιπή αρχεία.  
* Τρόποι για **convert scanned image** PDF ή TIFF σε bitmap που μπορεί να διαβάσει το Aspose.  
* Γιατί το async OCR (`RecognizeAsync`) είναι πιο γρήγορο και πιο κλιμακώσιμο από το συγχρονισμένο του.  
* Αναμενόμενη έξοδος κονσόλας και πώς να επαληθεύσετε ότι το εξαγόμενο κείμενο ταιριάζει με την πηγή.

> **Pro tip:** Αν επεξεργάζεστε δεκάδες σελίδες, κρατήστε τη μηχανή OCR ενεργή μεταξύ κλήσεων—η δημιουργία νέας παρουσίας κάθε φορά προσθέτει περιττό κόστος.

---

## Εξαγωγή Κειμένου από Εικόνα Ασύγχρονα

The heart of the solution lives in an async `Main` method. Using `await` keeps the UI thread free (or, in a console app, frees up the thread pool) while the OCR engine does its heavy lifting.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // 1️⃣ Create an instance of the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        Image inputImage = Image.FromFile(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Run asynchronous OCR recognition (returns a Task<string>)
        string recognizedText = await ocrEngine.RecognizeAsync(inputImage);

        // 4️⃣ Display the OCR result
        Console.WriteLine("Async OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**Why async?** Η λειτουργία OCR μπορεί να περιλαμβάνει δικτυακή I/O (αν η μηχανή χρησιμοποιεί υπηρεσίες cloud) ή εντατική εργασία CPU. Το `RecognizeAsync` ελευθερώνει το νήμα που το κάλεσε, επιτρέποντας σε άλλες εργασίες—όπως η διαχείριση περισσότερων αρχείων—να συνεχίσουν.

### Αναμενόμενη Έξοδος

```
Async OCR result:
The quick brown fox jumps over the lazy dog.
```

Αν η εικόνα περιέχει πολλαπλές γραμμές, κάθε γραμμή θα εμφανίζεται χωρισμένη με χαρακτήρες νέας γραμμής. Μπορείτε να αποθηκεύσετε το αποτέλεσμα σε αρχείο με `File.WriteAllText("output.txt", recognizedText);` αν χρειάζεστε μόνιμη αποθήκευση.

---

## Convert Scanned Image to a Usable Format

Sometimes you receive a scanned PDF or a multi‑page TIFF. Aspose OCR works best with a `System.Drawing.Image`, so you may need to convert first.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.Drawing.Imaging;

// Load a multi‑page TIFF and pick the first frame
Image tiff = Image.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
tiff.SelectActiveFrame(FrameDimension.Page, 0); // Grab page 0

// Optionally, change DPI for better accuracy
var bitmap = new Bitmap(tiff);
bitmap.SetResolution(300, 300); // 300 DPI is a sweet spot for OCR
```

> **Why change DPI?** Η υψηλότερη ανάλυση δίνει στη μηχανή OCR περισσότερες λεπτομέρειες, μειώνοντας τις λανθασμένες αναγνώσεις σε θολές σαρώσεις. Απλώς μην ξεπεράσετε τα 600 DPI—οι περισσότερες μηχανές δεν κερδίζουν επιπλέον ακρίβεια αλλά θα χρησιμοποιήσουν περισσότερη μνήμη.

---

## Φόρτωση Αρχείου Εικόνας C# – Διαχείριση Διαφορετικών Μορφών

You might be tempted to hard‑code a `.tif` path, but a robust utility should accept **any** image type (`.png`, `.jpg`, `.bmp`). Here’s a tiny helper that abstracts the loading logic:

```csharp
static Image LoadImage(string path)
{
    if (!File.Exists(path))
        throw new FileNotFoundException($"Image not found: {path}");

    // Let .NET decide the correct decoder based on file header
    using (var stream = File.OpenRead(path))
    {
        return Image.FromStream(stream);
    }
}
```

Use it like:

```csharp
Image img = LoadImage(@"YOUR_DIRECTORY/input.tif");
string text = await ocrEngine.RecognizeAsync(img);
```

Now you’ve covered the **load image file C#** scenario without worrying about the exact extension.

---

## Αναγνώριση Κειμένου από TIF – Τι Πρέπει να Ξέρετε

TIF files often store multiple pages or use compression that confuses some libraries. Two things help you get reliable results:

1. Επιλέξτε το σωστό πλαίσιο – όπως φαίνεται νωρίτερα με `SelectActiveFrame`.  
2. Κανονικοποιήστε τα χρώματα – η μετατροπή σε bitmap 24‑bit RGB μπορεί να εξαλείψει περίεργες παλέτες.

```csharp
static Image PrepareTif(string tifPath, int pageIndex = 0)
{
    Image tif = Image.FromFile(tifPath);
    tif.SelectActiveFrame(FrameDimension.Page, pageIndex);
    // Convert to 24‑bit RGB to avoid palette issues
    Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
    using (Graphics g = Graphics.FromImage(rgb))
    {
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
    }
    return rgb;
}
```

Feed the returned `Image` straight into `RecognizeAsync` and you’ll reliably **recognize text from TIF** even when the source uses CCITT Group 4 compression.

---

## Πλήρες Παράδειγμα Από Αρχή έως Τέλος

Putting everything together gives you a single file you can drop into a console project and run.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        try
        {
            // Step 1 – Initialize OCR engine (reuse if processing many files)
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2 – Load and prepare the image (handles TIF, PNG, JPG, etc.)
            Image img = PrepareImage(@"YOUR_DIRECTORY/input.tif");

            // Step 3 – Run async recognition
            string result = await ocrEngine.RecognizeAsync(img);

            // Step 4 – Output the result
            Console.WriteLine("Async OCR result:");
            Console.WriteLine(result);

            // Optional: Save to a text file
            File.WriteAllText("ocr-output.txt", result);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // Helper that decides how to load based on extension
    static Image PrepareImage(string path)
    {
        string ext = Path.GetExtension(path).ToLowerInvariant();
        return ext switch
        {
            ".tif" or ".tiff" => PrepareTif(path),
            _ => LoadImage(path)
        };
    }

    static Image LoadImage(string path)
    {
        if (!File.Exists(path))
            throw new FileNotFoundException($"Image not found: {path}");

        using var stream = File.OpenRead(path);
        return Image.FromStream(stream);
    }

    static Image PrepareTif(string tifPath, int page = 0)
    {
        Image tif = Image.FromFile(tifPath);
        tif.SelectActiveFrame(FrameDimension.Page, page);
        Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
        using var g = Graphics.FromImage(rgb);
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
        return rgb;
    }
}
```

**What you should see:** Η κονσόλα εκτυπώνει το εξαγόμενο κείμενο, και ένα αρχείο με όνομα `ocr-output.txt` εμφανίζεται δίπλα στο εκτελέσιμο περιέχοντας το ίδιο κείμενο.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Question | Answer |
|----------|--------|
| *Μπορώ να κάνω OCR ένα PDF απευθείας;* | Το Aspose OCR λειτουργεί σε εικόνες, επομένως πρέπει πρώτα να μετατρέψετε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας Aspose.PDF ή `PdfRenderer`). |
| *Τι γίνεται αν η εικόνα είναι τεράστια;* | Μειώστε την ανάλυση σε μέγιστο 2500 px πλάτος/ύψος πριν το OCR· το Aspose θα αλλάξει το μέγεθος εσωτερικά αυτόματα, αλλά εσείς εξοικονομείτε μνήμη. |
| *Είναι η async μέθοδος thread‑safe;* | Ναι, αλλά επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` μόνο αν δεν καλείτε το `RecognizeAsync` ταυτόχρονα. Για παράλληλη επεξεργασία, δημιουργήστε ξεχωριστές μηχανές ανά εργασία. |
| *Χρειάζομαι άδεια;* | Το Aspose OCR προσφέρει δωρεάν αξιολόγηση με υδατογραφήματα. Για παραγωγή, αγοράστε άδεια και ορίστε την μέσω `License license = new License(); license.SetLicense("Aspose.OCR.lic");`. |

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **extract text from image** αρχεία σε C# χρησιμοποιώντας το ασύγχρονο API του Aspose OCR. Με τη διαχείριση της φόρτωσης εικόνας, την προαιρετική μετατροπή σαρωμένων εικόνων και τις ιδιαιτερότητες των αρχείων TIF, η λύση είναι τόσο αξιόπιστη όσο και έτοιμη για παραγωγή.  

Από εδώ μπορείτε:

* **Convert scanned image** PDF σε PNG πριν το OCR για καλύτερη ακρίβεια.  
* Εξερευνήστε **how to ocr image** ροές απευθείας από ένα web API, εξαλείφοντας την ανάγκη για προσωρινά αρχεία.  
* Επεξεργαστείτε κατά παρτίδες δεκάδες αρχεία επαναχρησιμοποιώντας την παρουσία `OcrEngine` μέσα σε βρόχο `Parallel.ForEach`.  

Δοκιμάστε αυτές τις παραλλαγές και θα δείτε γρήγορα γιατί το asynchronous OCR είναι ένας μετασχηματιστής για εφαρμογές με πολλά έγγραφα. Καλή προγραμματιστική, και μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε προβλήματα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}