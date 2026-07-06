---
category: general
date: 2026-05-21
description: Πραγματοποιήστε OCR σε εικόνα χρησιμοποιώντας C#. Μάθετε πώς να φορτώνετε
  εικόνα για OCR, να εξάγετε κείμενο από PNG και να αναγνωρίζετε κείμενο από εικόνα
  με ένα μικρό παράδειγμα κώδικα.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα σε C# γρήγορα. Αυτός ο οδηγός δείχνει πώς
  να φορτώσετε εικόνα για OCR, να εξάγετε κείμενο από PNG και να αναγνωρίσετε κείμενο
  από εικόνα με έξοδο HTML που διατηρεί τη διάταξη.
og_title: Εκτέλεση OCR σε εικόνα με C# – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Εκτέλεση OCR σε εικόνα με C# – Πλήρης οδηγός βήμα‑βήμα
url: /el/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτελέστε OCR σε εικόνα με C# – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **εκτελέσετε OCR σε εικόνα** αρχεία χωρίς να ασχοληθείτε με βαριές διεπαφές χρήστη; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε αποδείξεις, εξάγετε δεδομένα από σαρωμένες φόρμες, είτε απλώς χρειάζεστε να μετατρέψετε ένα PNG σε αναζητήσιμο κείμενο, με λίγες γραμμές C# μπορείτε να το πετύχετε.

Σε αυτό το tutorial θα περάσουμε από τη φόρτωση μιας εικόνας για OCR, την αναγνώριση κειμένου από εικόνα, και τέλος την εξαγωγή κειμένου από PNG ως καθαρό HTML. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση εφαρμογή κονσόλας που **εκτελεί OCR σε εικόνα** αρχεία και διατηρεί την αρχική διάταξη.

## Τι Θα Δημιουργήσετε

- Ένα ελάχιστο πρόγραμμα κονσόλας που διαβάζει ένα PNG (ή οποιαδήποτε υποστηριζόμενη εικόνα)  
- Χρησιμοποιεί μια μηχανή OCR για **αναγνωρίσετε κείμενο από εικόνα**  
- Αποθηκεύει το αποτέλεσμα ως HTML με διατήρηση διάταξης, ενσωματώνοντας την αρχική εικόνα  
- Δείχνει πώς να **φορτώσετε εικόνα για OCR**, **εξάγετε κείμενο από PNG**, και να διαχειριστείτε κοινές περιπτώσεις άκρων  

> **Προαπαιτούμενα**  
> - .NET 6.0 SDK ή νεότερο (μπορείτε επίσης να στοχεύσετε .NET Framework 4.7+)  
> - Μια βιβλιοθήκη OCR συμβατή με NuGet – το παράδειγμα χρησιμοποιεί *Aspose.OCR* αλλά οποιαδήποτε βιβλιοθήκη με παρόμοιο API θα λειτουργήσει  
> - Βασικές γνώσεις C# (τίποτα περίπλοκο)  

Τα έχετε; Τέλεια—ας βουτήξουμε.

## Εκτελέστε OCR σε εικόνα – Πλήρης Εξήγηση Κώδικα

Παρακάτω είναι το **πλήρες, εκτελέσιμο** πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο κονσόλας (`dotnet new console`) και πατήστε **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Αναμενόμενο αποτέλεσμα**  
> ```
> HTML with layout saved.
> ```  
> Μετά την εκτέλεση θα βρείτε το `form.html` δίπλα στο PNG σας. Ανοίξτε το σε έναν περιηγητή και θα δείτε την ακριβώς ίδια διάταξη, αλλά τώρα το κείμενο είναι επιλέξιμο και αναζητήσιμο.

### Φορτώστε εικόνα για OCR

Η γραμμή `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` είναι εκεί που **φορτώνουμε εικόνα για OCR**. Η βοηθητική κλάση `ImageStream` αφαιρεί τις λεπτομέρειες του μορφότυπου αρχείου, ώστε να μπορείτε να τροφοδοτήσετε JPEG, BMP ή TIFF χωρίς αλλαγή κώδικα.  

**Γιατί να μην περάσουμε απλώς ένα `Bitmap`;**  
Επειδή πολλές SDK OCR αναμένουν ένα stream που μεταφέρει επίσης μεταδεδομένα DPI. Χρησιμοποιώντας τον ενσωματωμένο φορτωτή της βιβλιοθήκης εξασφαλίζουμε ότι η μηχανή βλέπει την εικόνα ακριβώς όπως εμφανίζεται στην οθόνη, κάτι που βελτιώνει την ακρίβεια.

#### Pro tip
Αν επεξεργάζεστε μια παρτίδα αρχείων, τυλίξτε το βήμα φόρτωσης σε ένα `try/catch` και καταγράψτε τυχόν `FileNotFoundException`. Αυτό αποτρέπει το σπάσιμο ολόκληρης της παρτίδας επειδή ένα αρχείο λείπει.

### Εξάγετε κείμενο από PNG

Μόλις ολοκληρωθεί το `engine.Recognize()`, η μηχανή OCR κρατά το αναγνωρισμένο κείμενο εσωτερικά. Μπορείτε να το εξάγετε ως string αν χρειάζεστε μόνο ακατέργαστο κείμενο:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Αυτή είναι η πιο γρήγορη μέθοδος για **εξάγετε κείμενο από PNG** όταν δεν σας ενδιαφέρει η διάταξη. Για τις περισσότερες εργασίες εισαγωγής δεδομένων, το απλό κείμενο αρκεί—απλώς θυμηθείτε να αφαιρέσετε τα line breaks αν σκοπεύετε να το εισάγετε σε CSV.

### Αναγνωρίστε κείμενο από εικόνα

Η κλήση `Recognize()` κάνει τη βαριά δουλειά. Στο παρασκήνιο η μηχανή:

1. Κανονικοποιεί την εικόνα (απλοποιεί κλίση, αφαιρεί θόρυβο)  
2. Την διαχωρίζει σε γραμμές και λέξεις  
3. Εκτελεί έναν νευρωνικό ταξινομητή εκπαιδευμένο σε εκατομμύρια γλύφους  

Επειδή ορίσαμε `Language = OcrLanguage.English`, η μηχανή εφαρμόζει αγγλικά λεξικά, μειώνοντας δραστικά τα ψευδώς θετικά αποτελέσματα. Αν χρειάζεστε πολυγλωσσική υποστήριξη, απλώς περάστε έναν πίνακα γλωσσών:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Διαχείριση εξόδου HTML με διατήρηση διάταξης

Οι περισσότεροι προγραμματιστές σταματούν στο απλό κείμενο, αλλά το `HtmlSaveOptions` που χρησιμοποιήσαμε σας επιτρέπει να **εκτελέσετε OCR σε εικόνα** και να διατηρήσετε την οπτική δομή. Δύο σημαίες έχουν σημασία:

- `PreserveLayout = true` – διατηρεί στήλες, πίνακες και κενά.  
- `EmbedImages = true` – ενσωματώνει το αρχικό PNG ως στοιχείο `<img>` κωδικοποιημένο σε Base64, ώστε το HTML να είναι αυτόνομο.

Αν προτιμάτε ένα ελαφρύτερο αρχείο, ορίστε `EmbedImages = false` και το HTML θα αναφέρεται στο αρχικό PNG στο δίσκο.

#### Edge case: Large files

Για εικόνες μεγαλύτερες από 5 MB, η ενσωμάτωση μπορεί να αυξήσει δραματικά το μέγεθος του HTML. Σε τέτοιες περιπτώσεις, μεταβείτε σε εξωτερικές αναφορές εικόνας και σκεφτείτε να συμπιέσετε το PNG εκ των προτέρων με `ImageProcessor.Compress`.

## Συνηθισμένα προβλήματα και Pro Tips

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|--------|--------------|-----|
| Ακατάληπτοι χαρακτήρες | Λανθασμένη ρύθμιση γλώσσας ή έλλειψη πακέτου γλώσσας | Εγκαταστήστε τα κατάλληλα αρχεία δεδομένων γλώσσας και ορίστε σωστά το `engine.Language` |
| Κανένα κείμενο στην έξοδο | Η εικόνα είναι πολύ σκοτεινή ή χαμηλής ανάλυσης | Προεπεξεργαστείτε με `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Η διάταξη διασπάται στο HTML | `PreserveLayout` αφήθηκε στο προεπιλεγμένο `false` | Ορίστε `PreserveLayout = true` στο `HtmlSaveOptions` |
| Αργή επεξεργασία σε πολλές σελίδες | Η μηχανή επανεκκινείται ανά αρχείο | Επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` και αλλάξτε μόνο το `engine.Image` σε κάθε βρόχο |

### Κλιμάκωση σε Πολλαπλά Αρχεία

Αν χρειάζεται να **εκτελέσετε OCR σε εικόνα** αρχεία σε έναν φάκελο, τυλίξτε τη βασική λογική σε έναν απλό βρόχο:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Παρατηρήστε ότι **φορτώνουμε εικόνα για OCR** μέσα στον βρόχο, αλλά διατηρούμε τα ίδια αντικείμενα `engine` και `htmlOptions`. Αυτό μειώνει την κατανάλωση μνήμης και επιταχύνει τις εργασίες παρτίδας.

## Πέρα από το βασικό: Εξαγωγή σε PDF ή DOCX

Η ίδια `engine` μπορεί να αποθηκεύσει σε άλλες μορφές:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Αν το σύστημα σας απαιτεί αναζητήσιμα PDF, αυτή είναι μια αλλαγή μίας γραμμής—χωρίς ανάγκη ξεχωριστού αγωγού μετατροπής.

## Συμπέρασμα

Σας δείξαμε πώς να **εκτελέσετε OCR σε εικόνα** αρχεία με C#, από τη φόρτωση της εικόνας μέχρι **εξάγετε κείμενο από PNG** και τέλος **αναγνωρίσετε κείμενο από εικόνα** σε ένα HTML αρχείο με διατήρηση διάταξης. Το πλήρες παράδειγμα είναι έτοιμο για εκτέλεση, και τώρα καταλαβαίνετε γιατί κάθε βήμα είναι σημαντικό, πώς να το προσαρμόσετε για διαφορετικές γλώσσες, και ποια προβλήματα να προσέχετε.

Στη συνέχεια, δοκιμάστε να αντικαταστήσετε την αγγλική γλώσσα με άλλη τοπική, πειραματιστείτε με `PreserveLayout = false` για πιο ελαφρύ HTML, ή διοχετεύστε την έξοδο απλού κειμένου σε μια βάση δεδομένων για αναζητήσιμα αρχεία. Ο ουρανός είναι το όριο όταν συνδυάζετε μια ισχυρή μηχανή OCR με λίγες γραμμές C#.

Έχετε ερωτήσεις σχετικά με τη διαχείριση πολυσελίδων TIFF, ή θέλετε να μάθετε πώς να ενσωματώσετε αυτό σε ένα ASP.NET Core API; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Σχετικά Tutorials

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να εξάγετε κείμενο από εικόνα προετοιμάζοντας ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Εξαγωγή κειμένου από εικόνα – Αναγνώριση γραμμής με Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}