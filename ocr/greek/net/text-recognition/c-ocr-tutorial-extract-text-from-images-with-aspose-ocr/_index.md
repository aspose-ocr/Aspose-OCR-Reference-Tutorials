---
category: general
date: 2026-01-09
description: c# OCR οδηγός που δείχνει πώς να εξάγετε κείμενο από αρχεία εικόνας,
  να αναγνωρίζετε κείμενο από PNG, να μετατρέπετε την εικόνα σε συμβολοσειρά και να
  ανιχνεύετε τη γλώσσα αυτόματα χρησιμοποιώντας το Aspose.OCR.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to string
- detect language automatically
language: el
og_description: c# OCR tutorial που σας καθοδηγεί στην εξαγωγή κειμένου από εικόνες,
  στην αναγνώριση κειμένου από αρχεία png, στη μετατροπή εικόνων σε συμβολοσειρές
  και στην αυτόματη ανίχνευση γλώσσας χρησιμοποιώντας το Aspose OCR.
og_title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνες
tags:
- C#
- OCR
- Aspose
- Image Processing
title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνες με το Aspose OCR
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνες με το Aspose OCR

Ποτέ χρειάστηκε ένα **c# ocr tutorial** που να λειτουργεί πραγματικά σε ένα πραγματικό αρχείο PNG; Ίσως να δημιουργείτε έναν σαρωτή αποδείξεων, έναν πολυγλωσσικό επεξεργαστή φορμών, ή απλώς να θέλετε να μάθετε πώς να μετατρέψετε μια φωτογραφία κειμένου σε μια αναζητήσιμη συμβολοσειρά. Ό,τι και να είναι, βρίσκεστε στο σωστό μέρος.

Σε αυτόν τον οδηγό θα σας δείξουμε βήμα‑βήμα πώς να **εξάγετε κείμενο από εικόνα** αρχεία, **αναγνωρίσετε κείμενο από png**, **μετατρέψετε την εικόνα σε συμβολοσειρά**, και ακόμη **ανιχνεύσετε τη γλώσσα αυτόματα**—όλα με τη βιβλιοθήκη Aspose.OCR. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)  
- Μια αναφορά NuGet στο `Aspose.OCR` (έκδοση 23.9 ή νεότερη)  
- Ένα αρχείο εικόνας (`mixed‑script.png` σε αυτό το παράδειγμα) τοποθετημένο κάπου που η εφαρμογή μπορεί να το διαβάσει  
- Βασική κατανόηση της C# (αν έχετε γράψει ένα “Hello World”, είστε εντάξει)

> **Pro tip:** Αν δεν έχετε ήδη άδεια, η Aspose προσφέρει δωρεάν προσωρινή άδεια για δοκιμές. Απλώς τοποθετήστε το αρχείο `.lic` δίπλα στο εκτελέσιμο σας.

## Βήμα 1 – Εγκατάσταση του Πακέτου NuGet Aspose.OCR

Πρώτα, προσθέστε τη βιβλιοθήκη στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Ή, αν προτιμάτε το UI, κάντε δεξί‑κλικ *Dependencies → Manage NuGet Packages* και αναζητήστε **Aspose.OCR**.

## Βήμα 2 – Προετοιμασία της Μηχανής OCR (c# ocr tutorial core)

Τώρα θα δημιουργήσουμε ένα στιγμιότυπο `OcrEngine`, θα του πούμε να ανιχνεύσει αυτόματα τη γλώσσα, και θα το κατευθύνουμε στο αρχείο PNG μας.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 2.1: Initialise the OCR engine – this is the heart of the c# ocr tutorial
        var ocrEngine = new OcrEngine();

        // Step 2.2: Let the engine decide which language(s) are present.
        // AutoDetect is the default, but we set it explicitly for clarity.
        ocrEngine.Language = OcrLanguage.AutoDetect;

        // Step 2.3: Path to the image you want to process.
        // Replace with your own path if needed.
        string imagePath = @"C:\Images\mixed-script.png";

        // Step 2.4: Run the recognition.
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Step 2.5: Output the result – this is where we **convert image to string**.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### Γιατί ορίζουμε `Language = OcrLanguage.AutoDetect`

Η αυτόματη ανίχνευση γλώσσας σας εξοικονομεί το μαντεύω αν η εικόνα περιέχει Αγγλικά, Ρώσικα, Αραβικά ή ένα μείγμα. Είναι η πιο ευέλικτη επιλογή για σενάριο **detect language automatically**, και λειτουργεί αμέσως για τις περισσότερες γραφές που υποστηρίζει η Aspose.

## Βήμα 3 – Εκτέλεση της Εφαρμογής και Επαλήθευση του Αποτελέσματος

Συγκεντρώστε και εκτελέστε το πρόγραμμα (`dotnet run` ή πατήστε **F5** στο Visual Studio). Αν όλα είναι σωστά συνδεδεμένα, θα δείτε κάτι όπως:

```
=== Recognized Text ===
Hello World!
Привет мир!
مرحبا بالعالم!
```

Αυτό το αποτέλεσμα αποδεικνύει ότι εξάγαμε επιτυχώς **κείμενο από εικόνα**, **αναγνωρίσαμε κείμενο από png**, και **μετατρέψαμε την εικόνα σε συμβολοσειρά** – όλα σε ένα μόνο, συνοπτικό απόσπασμα.

## Βήμα 4 – Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Διαχείριση Πολλαπλών Εικόνων

Αν χρειάζεται να επεξεργαστείτε έναν φάκελο PNG, τυλίξτε την κλήση αναγνώρισης σε έναν βρόχο `foreach`:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Images", "*.png"))
{
    string text = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"[{Path.GetFileName(file)}] => {text}");
}
```

### Καθορισμός Σταθερής Γλώσσας

Μερικές φορές γνωρίζετε τη γλώσσα εκ των προτέρων (π.χ., μόνο Αγγλικά). Μπορείτε να αντικαταστήσετε το `AutoDetect` με `OcrLanguage.English` για να επιταχύνετε την επεξεργασία:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### Αντιμετώπιση Σαρωμάτων Χαμηλής Ποιότητας

Η Aspose.OCR προσφέρει επιλογές προεπεξεργασίας (μείωση θορύβου, διόρθωση κλίσης). Για μια γρήγορη λύση:

```csharp
ocrEngine.ImagePreprocessingOptions.Deskew = true;
ocrEngine.ImagePreprocessingOptions.RemoveNoise = true;
```

### Αποθήκευση του Αποτελέσματος σε Αρχείο

Αντί να εκτυπώνετε στην κονσόλα, ίσως θέλετε να γράψετε το εξαγόμενο κείμενο σε αρχείο `.txt`:

```csharp
File.WriteAllText(@"C:\Output\recognized.txt", recognizedText);
```

## Βήμα 5 – Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το **πλήρες πρόγραμμα** συμπεριλαμβανομένης της προαιρετικής προεπεξεργασίας και της λογικής εξόδου σε αρχείο. Μη διστάσετε να προσαρμόσετε τις διαδρομές.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class OcrDemo
{
    static void Main()
    {
        // Initialise engine
        var ocrEngine = new OcrEngine
        {
            // Auto‑detect language (detect language automatically)
            Language = OcrLanguage.AutoDetect,

            // Optional: improve accuracy on noisy scans
            ImagePreprocessingOptions = {
                Deskew = true,
                RemoveNoise = true
            }
        };

        // Input image – change to your own file
        string inputPath = @"C:\Images\mixed-script.png";

        // Perform OCR
        string extractedText = ocrEngine.RecognizeImage(inputPath);

        // Display on console (convert image to string)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);

        // Save to a text file for later use
        string outputPath = Path.ChangeExtension(inputPath, ".txt");
        File.WriteAllText(outputPath, extractedText);
        Console.WriteLine($"\nText saved to: {outputPath}");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος σε ένα PNG που περιέχει Αγγλικά, Ρώσικα και Αραβικά δίνει:

```
=== OCR Result ===
Hello World!
Привет мир!
مرحبا بالعالم!

Text saved to: C:\Images\mixed-script.txt
```

Αν η εικόνα είναι κενή ή μη αναγνώσιμη, η μηχανή επιστρέφει μια κενή συμβολοσειρά—χειριστείτε αυτήν την περίπτωση ελέγχοντας `string.IsNullOrWhiteSpace(extractedText)` πριν προχωρήσετε.

## Συχνές Ερωτήσεις (FAQs)

**Q: Υποστηρίζει η Aspose.OCR χειρόγραφο κείμενο;**  
A: Επικεντρώνεται σε τυπωμένο OCR. Για χειρόγραφο κείμενο θα χρειαστείτε ένα εξειδικευμένο μοντέλο ML ή μια υπηρεσία όπως το Azure Computer Vision.

**Q: Μπορώ να το τρέξω σε Linux/macOS;**  
A: Απόλυτα. Η Aspose.OCR είναι cross‑platform· απλώς εγκαταστήστε το .NET runtime για το λειτουργικό σας σύστημα.

**Q: Τι γίνεται αν χρειαστεί να επεξεργαστώ PDFs αντί για PNGs;**  
A: Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας το `Aspose.PDF`) και μετά δώστε την εικόνα στη μηχανή OCR.

## Συμπέρασμα

Μόλις ολοκληρώσαμε ένα **c# ocr tutorial** που σας οδηγεί μέσα από **εξαγωγή κειμένου από εικόνα** αρχείων, **αναγνώριση κειμένου από png**, **μετατροπή της εικόνας σε συμβολοσειρά**, και **αυτόματη ανίχνευση γλώσσας** χρησιμοποιώντας το Aspose.OCR. Ο κώδικας είναι σύντομος, οι έννοιες σαφείς, και μπορείτε να τον επεκτείνετε για επεξεργασία παρτίδων, προσαρμοσμένες ρυθμίσεις γλώσσας, ή ακόμη και ενσωμάτωση σε web API.

Τι επόμενα; Δοκιμάστε να τροφοδοτήσετε το αποτέλεσμα OCR σε ευρετήριο αναζήτησης, σε υπηρεσία μετάφρασης, ή συνδυάστε το με το Azure Cognitive Services για ακόμη πιο πλούσιες ροές δεδομένων. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά της μετατροπής εικόνας‑σε‑κείμενο σε C#.

Καλή προγραμματιστική, και μην ξεχάσετε να πειραματιστείτε με διαφορετικές ποιότητες εικόνας—η μηχανή OCR σας θα το εκτιμήσει! 

![c# ocr tutorial – παράδειγμα αποτελέσματος OCR σε PNG με μεικτό κείμενο](placeholder-image.png "c# ocr tutorial – Στιγμιότυπο αποτελέσματος OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}