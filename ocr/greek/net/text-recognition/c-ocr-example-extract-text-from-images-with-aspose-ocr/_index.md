---
category: general
date: 2026-03-23
description: Παράδειγμα OCR σε C# που δείχνει πώς να εξάγετε κείμενο από εικόνες C#
  χρησιμοποιώντας το Aspose OCR. Μάθετε πώς να φορτώνετε αρχείο εικόνας σε C# και
  να διαχειρίζεστε πολλαπλές γλώσσες.
draft: false
keywords:
- c# ocr example
- extract text from image c#
- load image file c#
- aspose ocr tutorial c#
language: el
og_description: Παράδειγμα OCR σε C# που σας καθοδηγεί στην εξαγωγή κειμένου από αρχεία
  εικόνας C# χρησιμοποιώντας το Aspose OCR. Περιλαμβάνει φόρτωση αρχείου εικόνας C#,
  υποστήριξη πολλαπλών γλωσσών και πλήρες κώδικα.
og_title: c# OCR παράδειγμα – Πλήρης οδηγός για την εξαγωγή κειμένου από εικόνες
tags:
- OCR
- C#
- Aspose
title: c# OCR παράδειγμα – Εξαγωγή κειμένου από εικόνες με Aspose OCR
url: /el/net/text-recognition/c-ocr-example-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr example – Εξαγωγή Κειμένου από Εικόνες με Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **extract text from image c#** έργα χωρίς να τρελαίνεστε; Ίσως έχετε μια σειρά από σαρωμένες αποδείξεις, πολυγλωσσικά PDF ή μερικά στιγμιότυπα οθόνης που χρειάζονται δυνατότητα αναζήτησης. Τα καλά νέα; Με ένα μόνο **c# ocr example** μπορείτε να μετατρέψετε αυτές τις εικόνες σε επεξεργάσιμες συμβολοσειρές σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από ένα **aspose ocr tutorial c#** που δείχνει ακριβώς πώς να **load image file c#**, να αλλάζετε γλώσσες εν κινήσει και να εκτυπώνετε τα αποτελέσματα στην κονσόλα. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που αναγνωρίζει ρωσικό και χίντι κείμενο – και θα ξέρετε πώς να το επεκτείνετε σε οποιαδήποτε γλώσσα υποστηρίζει η Aspose.

## What You’ll Learn

- Πώς να εγκαταστήσετε και να αναφέρετε το NuGet package Aspose.OCR.  
- Τα ακριβή βήματα για **load image file c#** σε ένα `OcrEngine`.  
- Πώς να ορίσετε τη γλώσσα OCR και να καλέσετε `Recognize()`.  
- Συμβουλές για διαχείριση πολλαπλών γλωσσών σε μία εκτέλεση.  
- Αναμενόμενη έξοδος κονσόλας ώστε να επαληθεύσετε ότι όλα λειτουργούν.

Καμία μαγεία, μόνο ένα σαφές, αναπαραγώγιμο **c# ocr example** που μπορείτε να ενσωματώσετε σε οποιαδήποτε .NET console app.

---

## Prerequisites

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

| Requirement | Why it matters |
|------------|----------------|
| .NET 6.0 SDK (ή νεότερο) | Το Aspose.OCR στοχεύει στο .NET Standard 2.0+, οπότε τα σύγχρονα runtime είναι τα καλύτερα. |
| Visual Studio 2022 (ή VS Code) | Χρήσιμο για γρήγορο debugging, αλλά οποιοδήποτε IDE αρκεί. |
| NuGet package `Aspose.OCR` | Η βιβλιοθήκη που κάνει το “βαρύ” έργο. |
| Δύο δείγμα εικόνων (`russian.png`, `hindi.tif`) | Δείχνει την υποστήριξη πολλαπλών γλωσσών. |

Αν λείπει κάτι από τα παραπάνω, εγκαταστήστε το πρώτα – είναι πιο εύκολο από το να προσπαθήσετε να διορθώσετε προβλήματα αργότερα.

---

## Step 1 – Install Aspose.OCR via NuGet

Ανοίξτε το τερματικό (ή το Package Manager Console) και τρέξτε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή φέρνει την πιο πρόσφατη σταθερή έκδοση του Aspose.OCR στο project σας. Χωρίς χειροκίνητη αναζήτηση DLL, χωρίς επιπλέον ρυθμίσεις – μόνο μια καθαρή έναρξη **aspose ocr tutorial c#**.

---

## Step 2 – Create a New Console Project

Αν δεν έχετε ήδη project, δημιουργήστε ένα:

```bash
dotnet new console -n MultiLangOcrDemo
cd MultiLangOcrDemo
```

Τώρα έχετε ένα φρέσκο `Program.cs` έτοιμο για τον κώδικα **c# ocr example**.

---

## Step 3 – Write the Full OCR Code (Load Image File C#)

Αντικαταστήστε το περιεχόμενο του `Program.cs` με το παρακάτω. Είναι ένα πλήρες, εκτελέσιμο **c# ocr example** που δείχνει πώς να **load image file c#**, να ορίσετε τη γλώσσα και να εκτυπώσετε το εξαγόμενο κείμενο.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;

class MultiLang
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Recognize Russian text from a PNG image
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Set the language to Russian
            ocrEngine.Language = Language.Russian;

            // Load the image – this is the "load image file c#" part
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/russian.png");

            // Perform the recognition
            if (ocrEngine.Recognize())
            {
                Console.WriteLine("Russian: " + ocrEngine.Text);
            }
            else
            {
                Console.WriteLine("Failed to recognize Russian text.");
            }
        }

        // -------------------------------------------------
        // 2️⃣ Recognize Hindi text from a TIFF image
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Switch the language to Hindi
            ocrEngine.Language = Language.Hindi;

            // Load the second image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/hindi.tif");

            // Run OCR again
            if (ocrEngine.Recognize())
            {
                Console.WriteLine("Hindi: " + ocrEngine.Text);
            }
            else
            {
                Console.WriteLine("Failed to recognize Hindi text.");
            }
        }
    }
}
```

**Γιατί λειτουργεί:**  
- Το `using` block εξασφαλίζει ότι το `OcrEngine` απελευθερώνεται μετά από κάθε εκτέλεση, απελευθερώνοντας τους εγγενείς πόρους.  
- Η ρύθμιση `ocrEngine.Language` λέει στην Aspose ποιο μοντέλο γλώσσας να εφαρμόσει – κρίσιμο για ακριβή αποτελέσματα.  
- Το `ImageStream.FromFile` είναι ο κανονικός τρόπος για **load image file c#** στην Aspose· υποστηρίζει PNG, TIFF, JPEG και άλλα.  
- Τέλος, το `ocrEngine.Recognize()` κάνει το “βαρύ” έργο και αποθηκεύει το αποτέλεσμα στο `ocrEngine.Text`.

---

## Step 4 – Run the Program and Verify Output

Συμπιέστε και εκτελέστε:

```bash
dotnet run
```

Αν όλα είναι ρυθμισμένα σωστά, θα δείτε κάτι όπως:

```
Russian: Привет мир!
Hindi: नमस्ते दुनिया!
```

Η κονσόλα σας εκτυπώνει τώρα τις εξαγόμενες συμβολοσειρές – απόδειξη ότι το **c# ocr example** εξάγει επιτυχώς **extract text from image c#** αρχεία.

---

## Step 5 – Extending the Example (More Languages, Better Accuracy)

### Add Another Language

Θέλετε να αναγνωρίζετε και Ιαπωνικά; Απλώς αντιγράψτε το δεύτερο μπλοκ, αλλάξτε το enum της γλώσσας και δείξτε σε μια Ιαπωνική εικόνα:

```csharp
ocrEngine.Language = Language.Japanese;
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/japanese.png");
```

### Improve Accuracy with Settings

Το Aspose OCR προσφέρει προαιρετικές ρυθμίσεις:

| Setting | What it does |
|---------|--------------|
| `ocrEngine.Config.DetectSkew = true;` | Διορθώνει κείμενο που είναι περιστραμμένο. |
| `ocrEngine.Config.RemoveNoise = true;` | Καθαρίζει θορυβώδεις σαρώσεις. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock;` | Βελτιστοποιεί για κείμενο μίας γραμμής. |

Προσθέστε αυτές τις γραμμές **πριν** καλέσετε το `Recognize()` αν αντιμετωπίζετε θορυβώδεις εικόνες.

---

## Common Pitfalls & Pro Tips

- **File Path Issues:** Χρησιμοποιήστε απόλυτες διαδρομές ή τοποθετήστε τις εικόνες στη ρίζα του project και ορίστε `Copy to Output Directory` σε `Copy always`. Έτσι αποφεύγετε το *FileNotFoundException*.  
- **Unsupported Formats:** Το Aspose OCR υποστηρίζει τις περισσότερες raster μορφές, αλλά τα PDF πρέπει πρώτα να μετατραπούν σε εικόνες (π.χ., με `Aspose.PDF`).  
- **Memory Leaks:** Πάντα τυλίξτε το `OcrEngine` σε `using` – η παράλειψη αυτής της πρακτικής μπορεί να κρατήσει τη φυσική μνήμη “κολλημένη”, ειδικά όταν επεξεργάζεστε πολλά αρχεία.  
- **Language Packs:** Το προεπιλεγμένο NuGet περιλαμβάνει τις πιο κοινές γλώσσες. Αν χρειάζεστε σπάνιο σύστημα γραφής, κατεβάστε το επιπλέον language pack από την ιστοσελίδα της Aspose και αναφέρετέ το με `ocrEngine.AdditionalLanguages`.

---

## Full Working Example (All Steps Combined)

Παρακάτω είναι το τελικό, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει τις προαιρετικές βελτιώσεις ακρίβειας και δείχνει πώς να διαχειριστείτε τρεις γλώσσες σε βρόχο.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Collections.Generic;

class MultiLangOcr
{
    static void Main()
    {
        // Map of language → image file
        var tasks = new Dictionary<Language, string>
        {
            { Language.Russian, "YOUR_DIRECTORY/russian.png" },
            { Language.Hindi,    "YOUR_DIRECTORY/hindi.tif" },
            { Language.Japanese, "YOUR_DIRECTORY/japanese.jpg" } // optional extra
        };

        foreach (var kvp in tasks)
        {
            using (OcrEngine engine = new OcrEngine())
            {
                engine.Language = kvp.Key;
                engine.Image = ImageStream.FromFile(kvp.Value);

                // Optional accuracy settings
                engine.Config.DetectSkew = true;
                engine.Config.RemoveNoise = true;

                Console.Write($"{kvp.Key}: ");

                if (engine.Recognize())
                {
                    Console.WriteLine(engine.Text);
                }
                else
                {
                    Console.WriteLine("Recognition failed.");
                }
            }
        }
    }
}
```

Τρέξτε το και θα δείτε το κείμενο κάθε γλώσσας να εκτυπώνεται με τη σειρά. Αυτό είναι ένα **c# ocr example** που μπορείτε να προσαρμόσετε για batch‑processing δεκάδων αρχείων με ένα απλό `foreach`.

---

## Conclusion

Δημιουργήσαμε ένα στιβαρό **c# ocr example** που **extracts text from image c#** αρχεία χρησιμοποιώντας το Aspose OCR, δείξαμε πώς να **load image file c#** και πώς να αλλάζετε γλώσσες εν κινήσει. Ο κώδικας είναι πλήρης, εκτελέσιμος και έτοιμος για παραγωγή – απλώς αντικαταστήστε τις διαδρομές placeholder με τις δικές σας εικόνες.

Αν θέλετε να προχωρήσετε παραπέρα, δοκιμάστε:

- Ενσωμάτωση του OCR output σε μια αναζητήσιμη βάση δεδομένων.  
- Χρήση του `Aspose.PDF` για μετατροπή σελίδων PDF σε εικόνες πριν τα δώσετε σε αυτό το **aspose ocr tutorial c#**.  
- Πειραματισμό με τις ιδιότητες `Config` για βελτιστοποίηση ακρίβειας σε χαμηλής ανάλυσης σαρώσεις.

Καλή προγραμματιστική δουλειά, και εύχομαι τα OCR αποτελέσματά σας να είναι πάντα ακριβή!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}