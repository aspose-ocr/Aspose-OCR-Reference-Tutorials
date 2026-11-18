---
category: general
date: 2026-08-15
description: Αναγνωρίστε κείμενο σε εικόνες από φωτογραφίες χρησιμοποιώντας Aspose
  OCR σε C#. Ακολουθήστε έναν πλήρη οδηγό μετατροπής εικόνας σε κείμενο C#, μάθετε
  πώς να φορτώνετε εικόνα OCR και να εξάγετε το κείμενο από την εικόνα αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text image
- image to text c#
- aspose ocr example
- load image ocr
- extract text image
language: el
lastmod: 2026-08-15
og_description: Αναγνωρίστε γρήγορα κείμενο σε εικόνα χρησιμοποιώντας το Aspose OCR
  σε C#. Αυτό το σεμινάριο δείχνει πώς να φορτώσετε OCR εικόνας, να μετατρέψετε την
  εικόνα σε κείμενο με C# και να εξάγετε κείμενο από εικόνα για πραγματικές εφαρμογές.
og_image_alt: Screenshot of C# code that recognizes text image with Aspose OCR
og_title: Αναγνώριση κειμένου σε εικόνα με το Aspose OCR – βήμα‑βήμα οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: recognize text image from photos using Aspose OCR in C#. Follow a complete
    image to text C# guide, learn how to load image OCR and extract text image efficiently.
  headline: recognize text image with Aspose OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image processing
title: Αναγνώριση κειμένου σε εικόνα με Aspose OCR σε C#
url: /el/net/text-recognition/recognize-text-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου σε εικόνα με Aspose OCR σε C#

Αν χρειάζεστε **αναγνώριση κειμένου σε εικόνα** σε μια εφαρμογή .NET, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.OCR. Είτε δημιουργείτε έναν σαρωτή εγγράφων, μια υπηρεσία επεξεργασίας αποδείξεων ή ένα πολύγλωσσο chatbot, τα παρακάτω βήματα σας επιτρέπουν να φορτώσετε μια εικόνα, να εκτελέσετε OCR και να εξάγετε το προκύπτον κείμενο—όλα σε καθαρό C#.

Θα δείτε επίσης μια **ροή εργασίας image to text C#**, ένα έτοιμο προς εκτέλεση **παράδειγμα Aspose OCR**, και συμβουλές για την αντιμετώπιση κοινών περιπτώσεων όπως η έλλειψη γλωσσικών μονάδων ή εικόνες χαμηλής ανάλυσης.

## Τι θα μάθετε

* Πώς να εγκαταστήσετε το πακέτο NuGet Aspose.OCR.  
* Πώς να **φορτώσετε εικόνα OCR** με μία μόνο γραμμή κώδικα.  
* Πώς να **αναγνωρίσετε κείμενο σε εικόνα** και να ανακτήσετε το αποτέλεσμα ως απλό κείμενο.  
* Τρόπους για **αποκτήσετε κείμενο από εικόνα** με ασφάλεια και διαχείριση σφαλμάτων.  
* Συστάσεις βέλτιστων πρακτικών για απόδοση και ακρίβεια.

### Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε.  
* Ένα αρχείο εικόνας που περιέχει αναγνώσιμο κείμενο (το παράδειγμα χρησιμοποιεί δείγμα κυριλλικού, αλλά λειτουργεί με οποιοδήποτε αλφάβητο).  

Δεν απαιτούνται πρόσθετες μηχανές OCR ή εγγενείς DLL—το Aspose.OCR διαχειρίζεται τα πάντα εσωτερικά.

## Αναγνώριση κειμένου σε εικόνα χρησιμοποιώντας Aspose OCR

Ο πυρήνας της λύσης είναι η κλάση `OcrEngine`. Η δημιουργία ενός αντικειμένου προετοιμάζει τη μηχανή, μετά μπορείτε να ορίσετε τη γλώσσα, να τροφοδοτήσετε μια εικόνα και να καλέσετε `Recognize()`.

```csharp
using System;
using System.Drawing;               // For Image
using Aspose.OCR;                    // Aspose OCR namespace

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Choose the language model (Cyrillic in this example)
        // The first call automatically downloads the language pack if needed.
        engine.Language = OcrLanguage.Cyrillic;

        // Step 3: Load the image you want to process
        // This demonstrates the “load image OCR” step.
        engine.Image = Image.FromFile(@"C:\Samples\cyrillic_sample.jpg");

        // Step 4: Perform the recognition
        engine.Recognize();

        // Step 5: Output the recognized text
        // This is the “extract text image” stage.
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(engine.Text);
    }
}
```

**Γιατί είναι σημαντικά αυτά τα βήματα**

* **Δημιουργία μηχανής**: εκχωρεί εσωτερικές μνήμες και προετοιμάζει τη γραμμή OCR.  
* **Επιλογή γλώσσας**: ενημερώνει τη μηχανή για το σύνολο χαρακτήρων που αναμένεται· η χρήση του σωστού μοντέλου βελτιώνει δραστικά την ακρίβεια.  
* **Φόρτωση εικόνας**: είναι η μόνη λειτουργία I/O· η κλήση `Image.FromFile` υποστηρίζει μορφές BMP, JPEG, PNG, TIFF και GIF.  
* **Recognize()**: εκτελεί το νευρωνικό μοντέλο πάνω στο bitmap και γεμίζει το `engine.Text`.  
* **Εξαγωγή κειμένου** μέσω `engine.Text` σας δίνει μια απλή συμβολοσειρά που μπορείτε να αποθηκεύσετε, να αναζητήσετε ή να εμφανίσετε.

### Αναμενόμενο αποτέλεσμα

Αν η δείγμα εικόνας περιέχει τη κυριλλική φράση “Привет мир”, η κονσόλα θα εκτυπώσει:

```
=== OCR Result ===
Привет мир
```

Το αποτέλεσμα θα ταιριάζει ακριβώς με τους χαρακτήρες Unicode που εμφανίζονται στην εικόνα, εφόσον το πακέτο γλώσσας έχει επιλεγεί σωστά.

## Φόρτωση εικόνας OCR – διαχείριση διαφορετικών πηγών

Το Aspose.OCR μπορεί να δεχτεί εικόνες από ροές, byte arrays ή `System.Drawing.Image`. Παρακάτω φαίνονται δύο κοινές εναλλακτικές που ικανοποιούν ακόμη και την απαίτηση **load image OCR**.

```csharp
// Load from a memory stream (useful for uploaded files)
using (var stream = File.OpenRead(@"C:\Samples\cyrillic_sample.jpg"))
{
    engine.Image = Image.FromStream(stream);
}

// Load from a byte array (e.g., when the image comes from a database)
byte[] imageBytes = File.ReadAllBytes(@"C:\Samples\cyrillic_sample.jpg");
using (var ms = new MemoryStream(imageBytes))
{
    engine.Image = Image.FromStream(ms);
}
```

Η σωστή επιλογή πηγής αποφεύγει προσωρινά αρχεία και μπορεί να βελτιώσει την απόδοση σε web APIs.

## Μετατροπή image to text C# – βελτιστοποίηση ακρίβειας

Αν και η βασική κλήση λειτουργεί αμέσως, μπορείτε να ρυθμίσετε τη μηχανή για καλύτερα αποτελέσματα:

| Ιδιότητα | Τυπική χρήση | Παράδειγμα |
|----------|--------------|------------|
| `engine.Config.Dpi` | Προσαρμόζει το υποτιθέμενο DPI για εικόνες χαμηλής ανάλυσης | `engine.Config.Dpi = 300;` |
| `engine.Config.SegmentationMode` | Ελέγχει πώς η μηχανή χωρίζει τις γραμμές κειμένου | `engine.Config.SegmentationMode = SegmentationMode.Word;` |
| `engine.Config.EnableNoiseFilter` | Αφαιρεί σπινθήρες φόντου | `engine.Config.EnableNoiseFilter = true;` |

```csharp
engine.Config.Dpi = 300;                     // Improves recognition on 72‑dpi scans
engine.Config.EnableNoiseFilter = true;     // Reduces artifacts
engine.Config.SegmentationMode = SegmentationMode.Line;
```

Αυτές οι ρυθμίσεις αποτελούν μέρος της βελτιστοποίησης **image to text C#** και συχνά μετατρέπουν ένα ασαφές αποτέλεσμα σε καθαρή συμβολοσειρά.

## Εξαγωγή κειμένου από εικόνα – συμβουλές μετα-επεξεργασίας

Αφού λάβετε το `engine.Text`, ίσως χρειαστεί να:

* **Καθαρίσετε λευκούς χαρακτήρες** – το OCR μπορεί να προσθέσει αρχικά/τελικά line breaks.  
* **Κανονικοποιήσετε τα τέλη γραμμής** – Μετατρέψτε `\r\n` σε `\n` για συνέπεια.  
* **Ανιχνεύσετε τη γλώσσα** – Αν υποστηρίζετε πολλαπλά αλφάβητα, ελέγξτε το εύρος του πρώτου χαρακτήρα.

```csharp
string raw = engine.Text;
string cleaned = raw.Trim();                     // Remove surrounding whitespace
cleaned = cleaned.Replace("\r\n", "\n");          // Standardize line breaks
Console.WriteLine(cleaned);
```

Το βήμα **extract text image** είναι εκεί όπου ενσωματώνετε το αποτέλεσμα OCR στη λογική της επιχείρησής σας (π.χ., αποθήκευση σε βάση δεδομένων, τροφοδοσία ευρετηρίου αναζήτησης ή μετάφραση).

## Συνηθισμένα προβλήματα και βέλτιστες πρακτικές

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Έλλειψη γλωσσικού μοντέλου | Την πρώτη φορά που χρησιμοποιείται μια γλώσσα, το Aspose το κατεβάζει. Αν η μηχανή δεν έχει internet, η κλήση αποτυγχάνει. | Προκατεβάστε το μοντέλο σε συνδεδεμένο υπολογιστή ή ορίστε `engine.Language = OcrLanguage.English` ως εναλλακτική. |
| Εικόνα χαμηλής ανάλυσης | Τα μοντέλα OCR υποθέτουν τουλάχιστον 300 DPI για καθαρούς χαρακτήρες. | Μεγαλώστε την εικόνα ή ορίστε `engine.Config.Dpi` όπως φαίνεται παραπάνω. |
| Μη υποστηριζόμενη μορφή εικόνας | Ορισμένες μορφές (π.χ., WebP) δεν αναγνωρίζονται από το `System.Drawing`. | Μετατρέψτε σε PNG/JPEG πριν τη δώσετε στη μηχανή. |
| Μεγάλες εικόνες που καταναλώνουν πολύ μνήμη | Τα bitmap πλήρους ανάλυσης μπορούν να καταναλώσουν εκατοντάδες MB. | Μειώστε το μέγεθος με `engine.Config.MaxImageSize = 2000;` ή αλλάξτε το μέγεθος χειροκίνητα. |

**Συμβουλή:** Τυλίξτε την κλήση OCR σε μπλοκ `try / catch` και καταγράψτε το `engine.LastError` για διαγνωστικές λεπτομέρειες.

```csharp
try
{
    engine.Recognize();
    Console.WriteLine(engine.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## Πλήρες λειτουργικό παράδειγμα

Ακολουθεί το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο console. Περιλαμβάνει όλες τις προαιρετικές ρυθμίσεις που συζητήθηκαν παραπάνω.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;

class OcrDemo
{
    static void Main()
    {
        // Create engine
        OcrEngine engine = new OcrEngine();

        // Select language (Cyrillic used for demo; change as needed)
        engine.Language = OcrLanguage.Cyrillic;

        // Optional: improve accuracy for low‑res images
        engine.Config.Dpi = 300;
        engine.Config.EnableNoiseFilter = true;
        engine.Config.SegmentationMode = SegmentationMode.Line;

        // Load image – replace with your path
        string path = @"C:\Samples\cyrillic_sample.jpg";
        if (!File.Exists(path))
        {
            Console.Error.WriteLine($"File not found: {path}");
            return;
        }

        // Load from file (demonstrates “load image OCR”)
        engine.Image = Image.FromFile(path);

        // Recognize
        try
        {
            engine.Recognize();
            string result = engine.Text.Trim().Replace("\r\n", "\n");
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result);
        }
        catch (Exception e)
        {
            Console.Error.WriteLine($"Error during OCR: {e.Message}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα με `dotnet run`. Αν όλα είναι ρυθμισμένα σωστά, η κονσόλα θα εκτυπώσει το εξαγόμενο κείμενο.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή λύση **recognize text image** χτισμένη με Aspose OCR σε C#. Ο οδηγός κάλυψε τη **ροή image to text C#**, έδειξε πώς να **φορτώσετε εικόνα OCR**, παρουσίασε τρόπους **εξαγωγής κειμένου από εικόνα**, και τόνισε τις βέλτιστες πρακτικές για αποφυγή κοινών προβλημάτων.

Από εδώ μπορείτε:

* Να αντικαταστήσετε το `OcrLanguage.Cyrillic` με άλλες γλώσσες (Arabic, Hindi, κ.λπ.).  
* Να ενσωματώσετε το βήμα OCR σε ένα ASP.NET Core API που δέχεται ανεβασμένες φωτογραφίες.  
* Να συνδυάσετε το αποτέλεσμα με το Azure Cognitive Services Translator για πολυγλωσσικές εφαρμογές.

Καλή προγραμματιστική δουλειά, και θυμηθείτε ότι η ακριβής OCR ξεκινά με μια καθαρή εικόνα και το σωστό μοντέλο γλώσσας!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίησή σας.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}