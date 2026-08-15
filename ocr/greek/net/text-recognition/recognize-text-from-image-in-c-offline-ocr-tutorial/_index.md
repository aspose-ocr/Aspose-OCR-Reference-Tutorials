---
category: general
date: 2026-04-29
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα εκτός σύνδεσης χρησιμοποιώντας
  το Aspose OCR. Περιλαμβάνει βήματα για την εξαγωγή κειμένου από PNG και τη φόρτωση
  της εικόνας για OCR σε μια ενιαία εφαρμογή C#.
draft: false
keywords:
- recognize text from image
- extract text from png
- load image for ocr
- Aspose OCR offline
- C# OCR example
language: el
og_description: Αναγνώριση κειμένου από εικόνα εκτός σύνδεσης με το Aspose OCR σε
  C#. Οδηγός βήμα‑βήμα για την εξαγωγή κειμένου από PNG και τη φόρτωση της εικόνας
  για OCR.
og_title: Αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός OCR Εκτός Σύνδεσης
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Αναγνώριση κειμένου από εικόνα σε C# – Εκμάθηση OCR εκτός σύνδεσης
url: /el/net/text-recognition/recognize-text-from-image-in-c-offline-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα – Πλήρης Οδηγός Offline OCR

Κάποτε χρειάστηκε να **recognize text from image** ενώ η εφαρμογή σας τρέχει σε μηχάνημα χωρίς πρόσβαση στο διαδίκτυο; Ίσως να δημιουργείτε έναν σαρωτή για εξωτερικές συσκευές, ένα ασφαλές περίπτερο, ή απλώς θέλετε να αποφύγετε την καθυστέρηση των υπηρεσιών cloud. Σε αυτό το tutorial θα περάσουμε από ένα αυτόνομο πρόγραμμα C# που **recognize text from image** χρησιμοποιώντας Aspose OCR, και θα σας δείξουμε επίσης πώς να **extract text from png** και σωστά **load image for ocr** όταν οι πόροι βρίσκονται στον δίσκο.

Θα καλύψουμε όλα όσα χρειάζεστε: το ακριβές πακέτο NuGet, τη δομή φακέλων για τα προ‑κατεβασμένα OCR modules, και μερικές συμβουλές που κρατούν τον κώδικά σας ανθεκτικό όταν τα πράγματα δεν πάνε όπως πρέπει. Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή console που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα — χωρίς κλήσεις δικτύου.

## Προαπαιτούμενα

- .NET 6 (ή οποιοδήποτε πρόσφατο .NET runtime) εγκατεστημένο τοπικά.  
- Visual Studio 2022 ή VS Code — όποιο IDE προτιμάτε.  
- Πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
- Τα offline OCR αρχεία πόρων που κατεβάσατε από το portal της Aspose (είναι μόνο λίγα MB).  
- Μια εικόνα PNG (`offline_test.png`) που θέλετε να επεξεργαστείτε.

> **Pro tip:** Κρατήστε το φάκελο πόρων δίπλα στο εκτελέσιμο σας· έτσι η σχετική ανάλυση διαδρομής γίνεται παιχνιδάκι.

## Βήμα 1 – Δημιουργία του OCR Engine Instance

Το πρώτο που κάνουμε είναι η δημιουργία ενός `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα αναλύσει αργότερα τα pixel.

```csharp
using Aspose.OCR;
using System;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε μια νέα παρουσία σε κάθε εκτέλεση; Εγγυάται καθαρή κατάσταση, ειδικά όταν εναλλάσσετε επιλογές όπως η αυτόματη λήψη πόρων. Σε μια υπηρεσία που τρέχει πολύ ώρα μπορεί να επαναχρησιμοποιήσετε το engine, αλλά για μια απλή demo αυτή η προσέγγιση είναι η πιο ασφαλής.

## Βήμα 2 – Καθορισμός των Offline Πόρων για το Engine

Το Aspose OCR κανονικά κατεβάζει language packs από το cloud. Επειδή θέλουμε να **recognize text from image** offline, πρέπει να πούμε στο engine πού βρίσκονται τα αρχεία.

```csharp
        // Step 2: Point the engine to the folder containing the pre‑downloaded OCR modules
        ocrEngine.Config.ResourcesPath = @"YOUR_DIRECTORY";
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή που περιέχει το φάκελο `ocrdata` που εξαγάγατε από το download της Aspose. Αν η διαδρομή είναι λανθασμένη, το engine θα ρίξει `FileNotFoundException` — γι’ αυτό ελέγξτε προσεκτικά την ορθογραφία.

## Βήμα 3 – Απενεργοποίηση Αυτόματης Λήψης Πόρων

Από προεπιλογή το Aspose προσπαθεί να κατεβάσει τα ελλιπή modules on the fly. Για ένα offline σενάριο απενεργοποιούμε ρητά αυτή τη λειτουργία.

```csharp
        // Step 3: Disable automatic resource download to enforce offline operation
        ocrEngine.Config.AllowAutomaticResourceDownload = false;
```

Αν ξεχάσετε αυτή τη γραμμή, το engine θα προσπαθήσει μια κλήση δικτύου, η οποία αποτυγχάνει σιωπηλά σε πολλά εταιρικά firewalls και σας αφήνει με κενό αποτέλεσμα. Η απενεργοποίηση επίσης επιταχύνει την πρώτη αναγνώριση επειδή το engine παραλείπει τον έλεγχο λήψης.

## Βήμα 4 – Φόρτωση της Εικόνας και Εκτέλεση OCR

Τώρα τελικά **load image for ocr**. Η στατική βοηθητική μέθοδος `LoadImage` δέχεται μια διαδρομή αρχείου και επιστρέφει ένα αντικείμενο `Image` που το engine μπορεί να καταναλώσει.

```csharp
        // Step 4: Load the image to be processed and run OCR
        var ocrResult = ocrEngine.Recognize(
            OcrEngine.LoadImage(@"YOUR_DIRECTORY/offline_test.png"));
```

Παρατηρήστε ότι χρησιμοποιούμε αρχείο PNG — ιδανικό για lossless εξαγωγή κειμένου. Αν έχετε JPEG, η ίδια κλήση λειτουργεί, αλλά το PNG συνήθως δίνει πιο καθαρά αποτελέσματα επειδή δεν υπάρχει compression artefact.

## Βήμα 5 – Εμφάνιση του Αναγνωρισμένου Κειμένου

Η μέθοδος `Recognize` επιστρέφει ένα `OcrResult` που περιέχει την ιδιότητα `Text`. Απλώς το γράφουμε στην κονσόλα.

```csharp
        // Step 5: Display the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Hello, Aspose OCR!
This is an offline test.
```

Αν η έξοδος είναι κενή, ελέγξτε ξανά το `ResourcesPath` και βεβαιωθείτε ότι το language module (π.χ. `English`) είναι παρόν.

![αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR](/images/offline_ocr_demo.png "αναγνώριση κειμένου από εικόνα")

*Το screenshot παραπάνω δείχνει την έξοδο της κονσόλας μετά την εξαγωγή κειμένου από png.*

## Συνηθισμένες Περιπτώσεις Άκρων & Πώς να τις Διαχειριστείτε

### 1. Η Εικόνα Είναι Πολύ Μεγάλη

Πολύ υψηλής ανάλυσης PNGs μπορούν να προκαλέσουν πίεση μνήμης. Σμικρύνετε την εικόνα πριν τη δώσετε στο engine:

```csharp
using System.Drawing;

// Load, resize, then pass to OCR
var original = (Bitmap)Image.FromFile(@"YOUR_DIRECTORY/offline_test.png");
var resized = new Bitmap(original, new Size(original.Width / 2, original.Height / 2));
var tempPath = Path.Combine(Path.GetTempPath(), "temp_resized.png");
resized.Save(tempPath);
var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(tempPath));
```

### 2. Δεν Εντοπίστηκε Η Γλώσσα

Αν προσπαθείτε να **extract text from png** που περιέχει γλώσσα διαφορετική από τα Αγγλικά, ορίστε ρητά τη γλώσσα:

```csharp
ocrEngine.Config.Language = Language.French; // or Language.Spanish, etc.
```

Βεβαιωθείτε ότι το αντίστοιχο language pack υπάρχει στον offline φάκελο πόρων.

### 3. Κενές ή Χαμηλής Αντίθεσης Εικόνες

Το OCR δυσκολεύεται με χαμηλή αντίθεση. Προεπεξεργαστείτε την εικόνα με ένα απλό threshold:

```csharp
using System.Drawing.Imaging;

var bitmap = new Bitmap(@"YOUR_DIRECTORY/offline_test.png");
for (int y = 0; y < bitmap.Height; y++)
{
    for (int x = 0; x < bitmap.Width; x++)
    {
        var pixel = bitmap.GetPixel(x, y);
        var gray = (pixel.R + pixel.G + pixel.B) / 3;
        var bw = gray > 128 ? Color.White : Color.Black;
        bitmap.SetPixel(x, y, bw);
    }
}
bitmap.Save(@"YOUR_DIRECTORY/processed.png");
```

Στη συνέχεια δείξτε στο OCR engine το `processed.png`. Αυτή η μικρή ρύθμιση συχνά μετατρέπει ένα 30 % ποσοστό επιτυχίας σε σχεδόν τέλεια εξαγωγή.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το *ολόκληρο* πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο μηχάνημά σας.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set offline resources folder
        ocrEngine.Config.ResourcesPath = @"C:\OCRResources";

        // 3️⃣ Prevent any network calls
        ocrEngine.Config.AllowAutomaticResourceDownload = false;

        // 4️⃣ Load PNG and recognize
        string imagePath = @"C:\OCRResources\offline_test.png";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(imagePath));

        // 5️⃣ Output the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το PNG περιέχει “Hello World!”):

```
=== OCR Output ===
Hello World!
```

Τρέξτε το με `dotnet run` από το φάκελο του project και παρακολουθήστε την κονσόλα να εκτυπώνει το εξαγόμενο κείμενο.

## Ανακεφαλαίωση – Τι Καταφέραμε

- **recognize text from image** πλήρως offline χρησιμοποιώντας Aspose OCR.  
- Επιδείξαμε πώς να **extract text from png** χωρίς καμία εξωτερική υπηρεσία.  
- Δείξαμε τον σωστό τρόπο **load image for ocr** και τη διαμόρφωση του engine για offline λειτουργία.  

Όλα αυτά ταιριάζουν σε μια μόνο, αυτόνομη εφαρμογή C# console.

## Επόμενα Βήματα & Σχετικά Θέματα

- **Batch processing** – επανάληψη πάνω σε έναν φάκελο PNGs και εγγραφή κάθε αποτελέσματος σε αρχείο `.txt`.  
- **Διαφορετικές μορφές αρχείων** – δοκιμάστε `LoadImage` με TIFF ή BMP για υψηλότερη πιστότητα σάρωσης.  
- **Βελτιστοποίηση απόδοσης** – ενεργοποιήστε multi‑threaded recognition αν έχετε πολλούς πυρήνες.  
- **Ενσωμάτωση με ASP.NET Core** – εκθέστε ένα API endpoint που δέχεται ανεβασμένη εικόνα και επιστρέφει το OCR αποτέλεσμα, παραμένοντας offline.

Αν σας ενδιαφέρει η διαχείριση PDF, δείτε τον οδηγό μας “recognize text from PDF using Aspose PDF”. Για πιο προχωρημένη προεπεξεργασία εικόνας, ρίξτε μια ματιά στα C# bindings του OpenCV.

---

*Καλή κωδικοποίηση! Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω — θα προσπαθήσω να σας βοηθήσω να εξάγετε το κείμενο από οποιαδήποτε εικόνα, ό,τι και αν είναι η σκληρότητά της.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}