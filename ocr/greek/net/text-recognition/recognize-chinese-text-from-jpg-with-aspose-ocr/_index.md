---
category: general
date: 2026-04-08
description: Μάθετε πώς να αναγνωρίζετε κινεζικό κείμενο από εικόνες JPG χρησιμοποιώντας
  το Aspose OCR. Αυτός ο οδηγός βήμα‑βήμα σας δείχνει επίσης πώς να εξάγετε κείμενο
  από την εικόνα γρήγορα.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: el
og_description: Αναγνωρίστε κινέζικο κείμενο από εικόνες JPG χρησιμοποιώντας το Aspose
  OCR. Ακολουθήστε αυτόν τον πλήρη οδηγό για να εξάγετε κείμενο από την εικόνα εκτός
  σύνδεσης.
og_title: αναγνώριση κινεζικού κειμένου από JPG με Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κινεζικού κειμένου από JPG με Aspose OCR
url: /el/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κινεζικού κειμένου από JPG με Aspose OCR

Κάποτε χρειάστηκε να **αναγνωρίσετε κινεζικό κείμενο** από ένα αρχείο JPG αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν δημιουργούν εφαρμογές σάρωσης πολυγλωσσικού περιεχομένου. Τα καλά νέα είναι ότι το Aspose OCR το κάνει παιχνιδάκι, ακόμη και όταν πρέπει να λειτουργήσετε εκτός σύνδεσης.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα όλη τη διαδικασία εξαγωγής κειμένου από μια εικόνα, **extract text from image**, και θα σας δείξουμε ακριβώς πώς να **recognize text from jpg** χρησιμοποιώντας C#. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που διαβάζει μια εικόνα στα κινέζικα και εκτυπώνει τους αναγνωρισμένους χαρακτήρες στην κονσόλα.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερη (οποιαδήποτε πρόσφατη έκδοση)
- Το πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Ένα αρχείο πόρων γλώσσας Κινέζικα (το tutorial δείχνει πώς να το φορτώσετε εκτός σύνδεσης)
- Ένα αρχείο εικόνας με όνομα `chinese_sample.jpg` τοποθετημένο σε φάκελο που ελέγχετε

Δεν απαιτούνται περίπλοκες τεχνικές IDE—Visual Studio, Rider ή ακόμη και VS Code αρκούν.

## Βήμα 1: Δημιουργία Έργου και Εγκατάσταση Aspose OCR

Πρώτα, δημιουργήστε ένα νέο console project και προσθέστε τη βιβλιοθήκη Aspose OCR.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν βρίσκεστε πίσω από εταιρικό proxy, προσθέστε τη σημαία `--no-cache` για να εξαναγκάσετε μια φρέσκια λήψη.

## Βήμα 2: Απενεργοποίηση Αυτόματης Λήψης Πόρων

Το Aspose OCR μπορεί να κατεβάσει πακέτα γλώσσας αυτόματα, αλλά για παραγωγή συνήθως θέλετε να συμπεριλάβετε τα αρχεία με την εφαρμογή σας. Η απενεργοποίηση της αυτόματης λήψης αποτρέπει ανεπιθύμητες κλήσεις δικτύου.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

Γιατί το κάνουμε αυτό; Η τοπική διατήρηση των πόρων εγγυάται σταθερή απόδοση και σας επιτρέπει να τρέξετε την εφαρμογή σε μηχανήματα χωρίς πρόσβαση στο internet.

## Βήμα 3: Φόρτωση Πόρων Κινέζικης Γλώσσας Εκτός Σύνδεσης

Το Aspose παρέχει τα δεδομένα γλώσσας ως ξεχωριστά αρχεία. Υποθέτοντας ότι έχετε τοποθετήσει το κινεζικό πακέτο (`zh`) σε φάκελο `Resources` δίπλα στο εκτελέσιμο, φορτώστε το ως εξής:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **Watch out:** Αν η διαδρομή είναι λανθασμένη, θα λάβετε `FileNotFoundException`. Ελέγξτε ξανά το όνομα του φακέλου και την ευαισθησία πεζών‑κεφαλαίων σε Linux.

## Βήμα 4: Ορισμός Γλώσσας Μηχανής σε Κινέζικα

Τώρα που τα δεδομένα έχουν φορτωθεί, ορίστε τον κωδικό γλώσσας στην μηχανή.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

Ο ρητός ορισμός της γλώσσας βελτιώνει την ακρίβεια, επειδή το OCR δεν θα χάνει χρόνο προσπαθώντας να μαντέψει το σύστημα γραφής.

## Βήμα 5: Αναγνώριση Κειμένου από Εικόνα JPG

Αυτή είναι η καρδιά του tutorial—παραδίδοντας ένα JPG στη μηχανή και εξάγοντας το κείμενο.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

Αν όλα πήγαν καλά, η κονσόλα θα εμφανίσει τους κινεζικούς χαρακτήρες που περιέχονται στο `chinese_sample.jpg`. Μπορείτε επίσης να προσπελάσετε το `ocrResult.Confidence` για ένα μέτρο ποιότητας.

## Βήμα 6: Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα κομμάτια παίρνετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα. Αποθηκεύστε το ως `Program.cs` μέσα στο φάκελο του έργου σας.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

Το ακριβές αποτέλεσμα θα διαφέρει ανάλογα με την πηγή εικόνας, αλλά θα πρέπει να δείτε ένα μπλοκ κινεζικών χαρακτήρων ακολουθούμενο από ποσοστό εμπιστοσύνης.

## Βήμα 7: Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Αναγνώριση Κειμένου από PNG ή BMP

Η μέθοδος `RecognizeImage` δέχεται οποιαδήποτε μορφή υποστηρίζεται από το `System.Drawing` του .NET. Απλώς αλλάξτε την επέκταση του αρχείου:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### Διαχείριση Πολλαπλών Γλωσσών

Αν χρειάζεται να **extract text from image** που συνδυάζει Αγγλικά και Κινέζικα, φορτώστε και τα δύο πακέτα γλώσσας και ορίστε `ocrEngine.Language = "zh,en";`. Η μηχανή θα εναλλάσσει αυτόματα τα συστήματα γραφής.

### Αντιμετώπιση Εικόνων Χαμηλής Ανάλυσης

Χαμηλό DPI μπορεί να μειώσει δραστικά την ακρίβεια του OCR. Πριν καλέσετε το `RecognizeImage`, μπορείτε να αυξήσετε την ανάλυση της εικόνας:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

Θυμηθείτε, η αύξηση της ανάλυσης δεν προσθέτει μαγικά λεπτομέρειες, αλλά μπορεί να δώσει στο αλγόριθμο περισσότερα pixel για επεξεργασία.

## Βήμα 8: Δοκιμή & Επαλήθευση

Μια γρήγορη επιβεβαίωση είναι να συγκρίνετε το αποτέλεσμα του OCR με μια γνωστή αλυσίδα αναφοράς.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

Αν το `matches` είναι `false`, σκεφτείτε να τροποποιήσετε την εικόνα (π.χ., να αυξήσετε την αντίθεση) ή να ενεργοποιήσετε `ocrEngine.Options.UseAdvancedPreprocessing = true`.

## Συμπέρασμα

Μόλις μάθατε πώς να **recognize chinese text** από ένα αρχείο JPG χρησιμοποιώντας Aspose OCR, και τώρα ξέρετε πώς να **extract text from image** σε πλήρως offline σενάριο. Η ολοκληρωμένη λύση—αρχικοποίηση, φόρτωση πόρων, επιλογή γλώσσας και επεξεργασία εικόνας—συμπεριλαμβάνεται σε μια απλή, εύκολη στην εκτέλεση console εφαρμογή.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε μια δέσμη εικόνων στην ίδια μηχανή, πειραματιστείτε με διαφορετικά πακέτα γλώσσας, ή ενσωματώστε το βήμα OCR σε ένα ASP .NET Web API ώστε οι χρήστες να μπορούν να ανεβάζουν εικόνες και να λαμβάνουν μεταφρασμένο κείμενο άμεσα. Ο ουρανός είναι το όριο όταν συνδυάζετε αξιόπιστο OCR με σύγχρονα εργαλεία .NET.

Καλή προγραμματιστική, και μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}