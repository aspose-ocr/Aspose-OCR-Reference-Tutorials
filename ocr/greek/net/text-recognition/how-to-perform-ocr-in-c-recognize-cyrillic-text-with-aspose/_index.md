---
category: general
date: 2025-12-30
description: Πώς να εκτελέσετε OCR γρήγορα σε C#. Μάθετε πώς να εξάγετε κείμενο από
  εικόνα, να μετατρέπετε την εικόνα σε κείμενο και να αναγνωρίζετε κυριλλικό κείμενο
  χρησιμοποιώντας το Aspose OCR.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize cyrillic text
- process image with OCR
language: el
og_description: Πώς να εκτελέσετε OCR σε C# με το Aspose. Αυτό το σεμινάριο δείχνει
  πώς να εξάγετε κείμενο από εικόνα, να μετατρέψετε την εικόνα σε κείμενο και να αναγνωρίσετε
  κυριλλικούς χαρακτήρες.
og_title: Πώς να εκτελέσετε OCR σε C# – Πλήρης Οδηγός
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR σε C# – Αναγνώριση κυριλλικού κειμένου με το Aspose
url: /el/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε C# – Αναγνώριση κυριλλικού κειμένου με Aspose

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε μια εικόνα που περιέχει κυριλλικά γράμματα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να εξάγουν κείμενο από αρχεία εικόνας, ειδικά όταν η γλώσσα δεν είναι βασισμένη στο λατινικό αλφάβητο. Τα καλά νέα; Με το Aspose OCR μπορείτε να **process image with OCR** με λίγες μόνο γραμμές κώδικα C#, και θα λάβετε καθαρό, αναζητήσιμο κείμενο.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη ροή εργασίας: από την εγκατάσταση της βιβλιοθήκης Aspose OCR, στη φόρτωση του μοντέλου γλώσσας Κυριλλικού, και τέλος **extracting text from image** και την εκτύπωση του στην κονσόλα. Στο τέλος θα μπορείτε να **convert image to text** και **recognize cyrillic text** χωρίς καμία δυσκολία.

## Τι θα χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Core και .NET Framework)
- Έγκυρη άδεια Aspose OCR ή δωρεάν δοκιμή (η δωρεάν έκδοση είναι πλήρως λειτουργική για ανάπτυξη)
- Ένα αρχείο εικόνας που περιέχει κυριλλικούς χαρακτήρες (π.χ., `cyrillic_sample.png`)
- Ένας φάκελος που περιέχει τα language modules που παρέχει η Aspose (θα υποδείξετε στη μηχανή αυτόν τον φάκελο)

Αυτό είναι—χωρίς επιπλέον πακέτα NuGet εκτός από το Aspose OCR, και χωρίς βαρύς εξαρτήσεις.

## Βήμα 1 – Εγκατάσταση Aspose OCR και Προετοιμασία Πόρων

Το πρώτο που πρέπει να κάνετε είναι να προσθέσετε το πακέτο Aspose OCR στο έργο σας. Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Μετά την εγκατάσταση του πακέτου, κατεβάστε τα **OCR language modules** από τον ιστότοπο της Aspose και αποσυμπιέστε τα σε έναν φάκελο της επιλογής σας, π.χ. `C:\Aspose\ocr-modules`. Αυτός ο φάκελος θα αναφερθεί αργότερα όταν υποδείξουμε στη μηχανή πού βρίσκεται το μοντέλο Κυριλλικού.

> **Pro tip:** Κρατήστε το φάκελο των modules εκτός του καταλόγου της λύσης σας για να αποφύγετε την τυχαία καταχώρηση μεγάλων δυαδικών αρχείων στον έλεγχο πηγαίου κώδικα.

## Βήμα 2 – Δημιουργία Ελάχιστης Εφαρμογής Κονσόλας

Τώρα ας ρυθμίσουμε μια μικρή εφαρμογή κονσόλας που θα **process image with OCR**. Δημιουργήστε ένα νέο έργο αν δεν έχετε ήδη:

```bash
dotnet new console -n CyrillicOcrDemo
cd CyrillicOcrDemo
```

Ανοίξτε το `Program.cs` και αντικαταστήστε το περιεχόμενό του με το πλήρες, εκτελέσιμο παράδειγμα παρακάτω. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε ακριβώς γιατί υπάρχει.

```csharp
// ------------------------------------------------------------
// How to Perform OCR – Complete C# Example using Aspose OCR
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language modules live.
        //    Replace the path with the actual location on your machine.
        ocrEngine.ResourcesPath = @"C:\Aspose\ocr-modules";

        // 3️⃣ Load the Cyrillic language model explicitly.
        //    This ensures the engine knows how to read Cyrillic glyphs.
        ocrEngine.LoadLanguage(LanguageModel.Cyrillic);

        // 4️⃣ Perform OCR on the target image.
        //    The method returns an OcrResult object that holds the text.
        var ocrResult = ocrEngine.Recognize(@"C:\Aspose\cyrillic_sample.png");

        // 5️⃣ Output the recognized text to the console.
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Γιατί κάθε βήμα είναι σημαντικό**

- **Initialize the OCR engine** – Δημιουργεί το βασικό αντικείμενο που θα διαχειρίζεται όλη την ανάλυση εικόνας.
- **ResourcesPath** – Η Aspose διαχωρίζει τα δεδομένα γλώσσας από το κεντρικό DLL· η αναφορά στον φάκελο επιτρέπει στη μηχανή να φορτώσει τα σωστά λεξικά.
- **LoadLanguage(Cyrillic)** – Χωρίς αυτήν την κλήση η μηχανή προεπιλέγει τα Αγγλικά, κάτι που θα αλλοιώσει τους κυριλλικούς χαρακτήρες.
- **Recognize(...)** – Αυτή είναι η πραγματική λειτουργία **convert image to text**. Διαβάζει το bitmap, εκτελεί το νευρωνικό δίκτυο και επιστρέφει ένα αποτέλεσμα.
- **Console.WriteLine** – Τέλος, κάνουμε **extract text from image** και το εμφανίζουμε, αποδεικνύοντας ότι το OCR πέτυχε.

## Βήμα 3 – Εκτέλεση της Εφαρμογής και Επαλήθευση του Αποτελέσματος

Συγκεντρώστε και εκτελέστε το πρόγραμμα:

```bash
dotnet run
```

Αν όλα έχουν ρυθμιστεί σωστά, θα πρέπει να δείτε κάτι σαν:

```
=== Recognized Cyrillic Text ===
Привет, мир! Это пример текста на кириллице.
```

Αυτή η γραμμή είναι το ακριβές κείμενο που εξήχθη από το OCR engine από το `cyrillic_sample.png`. Σε πραγματικό σενάριο, μπορείτε τώρα να αποθηκεύσετε αυτήν τη συμβολοσειρά σε μια βάση δεδομένων, να τη δώσετε σε ευρετήριο αναζήτησης ή να τη μεταφράσετε άμεσα.

### Συνηθισμένα Προβλήματα και Πώς να τα Αποφύγετε

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Empty output** | Δεν βρέθηκαν τα modules γλώσσας ή λανθασμένο `ResourcesPath`. | Ελέγξτε ξανά τη διαδρομή του φακέλου και βεβαιωθείτε ότι το αρχείο `.bin` του Κυριλλικού υπάρχει. |
| **Garbage characters** | Λάθος μοντέλο γλώσσας (προεπιλογή στα Αγγλικά). | Καλέστε `LoadLanguage(LanguageModel.Cyrillic)` πριν το `Recognize`. |
| **File not found** | Λάθος στη διαδρομή της εικόνας. | Χρησιμοποιήστε απόλυτες διαδρομές ή `Path.Combine` με `AppContext.BaseDirectory`. |
| **Performance lag** | Μεγάλες εικόνες επεξεργάζονται σε πλήρη ανάλυση. | Αλλάξτε το μέγεθος της εικόνας σε ≤ 1024 px πλάτος πριν το OCR· η Aspose προσφέρει μεθόδους `Resize`. |

## Βήμα 4 – Επέκταση του Παραδείγματος: Επεξεργασία σε Παρτίδες

Συχνά θα χρειαστείτε να **process image with OCR** σε πολλά αρχεία. Εδώ είναι ένα γρήγορο απόσπασμα που διασχίζει έναν φάκελο, εκτελεί OCR σε κάθε PNG και γράφει τα αποτελέσματα σε ένα αρχείο κειμένου.

```csharp
using System.IO;

// Assume ocrEngine is already configured as in the previous example.
string inputFolder = @"C:\Aspose\Samples";
string outputFolder = @"C:\Aspose\Results";

foreach (var filePath in Directory.GetFiles(inputFolder, "*.png"))
{
    var result = ocrEngine.Recognize(filePath);
    string fileName = Path.GetFileNameWithoutExtension(filePath);
    string outPath = Path.Combine(outputFolder, $"{fileName}.txt");
    File.WriteAllText(outPath, result.Text);
    Console.WriteLine($"Processed {fileName} → {outPath}");
}
```

Αυτό το μοτίβο σας επιτρέπει να **extract text from image** αρχεία μαζικά, μια συχνή απαίτηση για έργα ψηφιοποίησης εγγράφων.

## Βήμα 5 – Όταν Χρειάζεστε Περισσότερο από το Κυριλλικό

Το Aspose OCR υποστηρίζει δεκάδες γλώσσες (Αραβικά, Χίντι, Κινέζικα κ.λπ.). Για να αλλάξετε γλώσσες, απλώς αντικαταστήστε την τιμή του enum:

```csharp
ocrEngine.LoadLanguage(LanguageModel.Arabic);
```

Μπορείτε ακόμη και να φορτώσετε πολλαπλές γλώσσες ταυτόχρονα:

```csharp
ocrEngine.LoadLanguages(LanguageModel.Cyrillic, LanguageModel.English);
```

Αυτή η ευελιξία σημαίνει ότι η ίδια βάση κώδικα μπορεί να **convert image to text** για πολυγλωσσικά αρχεία.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο να τοποθετηθεί στο `Program.cs`. Δεν λείπουν τμήματα—απλώς αντικαταστήστε τις διαδρομές placeholder με τις δικές σας.

```csharp
// ------------------------------------------------------------
// How to Perform OCR – Full End‑to‑End Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // Point to the folder containing language modules.
        ocrEngine.ResourcesPath = @"C:\Aspose\ocr-modules";

        // Load Cyrillic language model.
        ocrEngine.LoadLanguage(LanguageModel.Cyrillic);

        // Recognize text from a Cyrillic image.
        var ocrResult = ocrEngine.Recognize(@"C:\Aspose\cyrillic_sample.png");

        // Output the result.
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Τρέξτε το, και θα δείτε την ακριβή κυριλλική συμβολοσειρά να εκτυπώνεται στην κονσόλα—απόδειξη ότι τώρα ξέρετε **how to perform OCR** σε C#.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **how to perform OCR** σε εικόνες που περιέχουν κυριλλικούς χαρακτήρες χρησιμοποιώντας το Aspose OCR. Από την εγκατάσταση της βιβλιοθήκης, τη φόρτωση του σωστού μοντέλου γλώσσας, μέχρι το **extract text from image** τόσο μεμονωμένα όσο και σε παρτίδες, έχετε τώρα μια σταθερή βάση για οποιοδήποτε έργο εξαγωγής κειμένου.

Επόμενα βήματα; Δοκιμάστε να αλλάξετε το μοντέλο γλώσσας σε **recognize cyrillic text** μαζί με τα Αγγλικά, πειραματιστείτε με διαφορετικές μορφές εικόνας, ή προωθήστε το αποτέλεσμα σε ένα API μετάφρασης. Ο ουρανός είναι το όριο όταν μπορείτε αξιόπιστα να **convert image to text**.

Έχετε ερωτήσεις για ειδικές περιπτώσεις—όπως σάρωση χαμηλής ανάλυσης ή θορυβώδη φόντο; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}