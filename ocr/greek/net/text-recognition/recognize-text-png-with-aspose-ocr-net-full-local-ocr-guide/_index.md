---
category: general
date: 2025-12-30
description: Μάθετε πώς να αναγνωρίζετε αρχεία PNG κειμένου εκτός σύνδεσης χρησιμοποιώντας
  το Aspose OCR .NET. Εξάγετε κείμενο από εικόνα, εκτελέστε OCR τοπικά και διαχειριστείτε
  κινέζους χαρακτήρες σε λίγα λεπτά.
draft: false
keywords:
- recognize text png
- extract text from image
- run ocr locally
- extract chinese characters
- aspose ocr .net
language: el
og_description: Οδηγός βήμα‑βήμα για την αναγνώριση κειμένου σε αρχεία png εκτός σύνδεσης
  χρησιμοποιώντας το Aspose OCR .NET. Εξαγωγή κειμένου από εικόνα, εκτέλεση OCR τοπικά
  και υποστήριξη κινεζικών χαρακτήρων.
og_title: Αναγνώριση κειμένου PNG με το Aspose OCR – Πλήρης .NET οδηγός
tags:
- OCR
- .NET
- Aspose
- Image Processing
title: Αναγνώριση κειμένου PNG με Aspose OCR .NET – Πλήρης Οδηγός Τοπικής OCR
url: /el/net/text-recognition/recognize-text-png-with-aspose-ocr-net-full-local-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text png – Πλήρης Οδηγός Aspose OCR .NET

Ποτέ χρειάστηκε να **recognize text png** αρχεία αλλά ήσασταν κολλημένοι σε υπηρεσίες μόνο‑cloud; Δεν είστε ο μόνος. Σε πολλά ρυθμιζόμενα περιβάλλοντα δεν μπορείτε να στείλετε εικόνες σε εξωτερικό API, έτσι η εκτέλεση OCR τοπικά γίνεται απαραίτητη δεξιότητα.  

Σε αυτόν τον οδηγό θα σας δείξουμε ακριβώς πώς να **recognize text png** εικόνες σε μηχανή Windows χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR για .NET. Καθ' όλη τη διάρκεια θα μάθετε επίσης πώς να **extract text from image** αρχεία, **run OCR locally**, και ακόμη **extract Chinese characters** χωρίς σύνδεση στο διαδίκτυο.  

Στο τέλος του οδηγού θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που εκτυπώνει το αποτέλεσμα OCR στην κονσόλα, και θα καταλάβετε το γιατί πίσω από κάθε βήμα ρύθμισης. Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφή μαγεία—μόνο καθαρός κώδικας .NET.

---

## Τι Θα Χρειαστείτε

- **.NET 6.0 SDK** ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET 5+).  
- **Visual Studio 2022** (η έκδοση Community είναι εντάξει) ή οποιονδήποτε επεξεργαστή που μπορεί να μεταγλωττίσει C#.  
- **Aspose.OCR for .NET** πακέτο NuGet (έκδοση 23.12 τη στιγμή της συγγραφής).  
- Ένας φάκελος που περιέχει τα αρχεία δεδομένων γλώσσας που απαιτεί το Aspose OCR για επεξεργασία εκτός σύνδεσης.  
- Ένα δείγμα εικόνας PNG με κινέζικο κείμενο (ή οποιαδήποτε γλώσσα θέλετε να δοκιμάσετε).

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—η εγκατάσταση του SDK και η προσθήκη ενός πακέτου NuGet είναι δουλειά δύο κλικ στο Visual Studio.

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose OCR

### Δημιουργία νέου έργου console

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

### Προσθήκη του πακέτου Aspose OCR NuGet

```bash
dotnet add package Aspose.OCR --version 23.12.0
```

Αυτό είναι όλο. Το πακέτο φέρνει το namespace `Aspose.OCR` που θα χρησιμοποιήσουμε για **recognize text png** αρχεία.

## Βήμα 2: Προετοιμασία Πόρων Γλώσσας Εκτός Σύνδεσης

Το Aspose OCR μπορεί να λειτουργεί πλήρως εκτός σύνδεσης, αλλά πρέπει να δείξετε στη μηχανή έναν φάκελο που περιέχει τα αρχεία μοντέλων γλώσσας (`*.dat`). Κατεβάστε το πακέτο γλώσσας από το portal του Aspose και εξάγετε το σε μια τοποθεσία που ελέγχετε, για παράδειγμα:

```
C:\Aspose\OCR\Resources
```

> **Pro tip:** Διατηρήστε τη δομή του φακέλου επίπεδη· κάθε αρχείο μοντέλου πρέπει να βρίσκεται απευθείας κάτω από `Resources`.

## Βήμα 3: Γράψτε τον Κώδικα OCR (Πλήρες Παράδειγμα)

Δημιουργήστε ένα αρχείο με όνομα `Program.cs` (αντικαταστήστε το προεπιλεγμένο) και επικολλήστε τον παρακάτω κώδικα. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε γιατί είναι σημαντική.

```csharp
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ------------------------------------------------------------------
            // 1️⃣ Initialize the OCR engine and force offline mode.
            //    This prevents any accidental web calls – perfect for secure
            //    environments where you must **run OCR locally**.
            // ------------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                OfflineMode = true               // No internet required
            };

            // ------------------------------------------------------------------
            // 2️⃣ Tell the engine where to find the language data files.
            //    Replace the path with the folder you created in Step 2.
            // ------------------------------------------------------------------
            ocrEngine.ResourcesPath = @"C:\Aspose\OCR\Resources";

            // ------------------------------------------------------------------
            // 3️⃣ Load the specific language model you need.
            //    Here we load Simplified Chinese because our sample image
            //    contains Chinese characters. Change this to LanguageModel.English
            //    (or another enum) if you work with other scripts.
            // ------------------------------------------------------------------
            ocrEngine.LoadLanguage(LanguageModel.ChineseSimplified);

            // ------------------------------------------------------------------
            // 4️⃣ Perform OCR on a PNG image.
            //    The Recognize method returns an OcrResult object that holds
            //    the extracted text, confidence scores, etc.
            // ------------------------------------------------------------------
            string imagePath = @"C:\Aspose\OCR\Samples\chinese_doc.png";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // ------------------------------------------------------------------
            // 5️⃣ Output the recognized text to the console.
            //    This is the simplest way to **extract text from image** files.
            // ------------------------------------------------------------------
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("==================");

            // Optional: Show confidence (useful for debugging)
            Console.WriteLine($"Confidence: {ocrResult.Confidence:P2}");
        }
    }
}
```

### Γιατί κάθε βήμα είναι σημαντικό

- **OfflineMode = true** – Εξασφαλίζει ότι η βιβλιοθήκη δεν θα προσπαθήσει ποτέ να επικοινωνήσει με το cloud του Aspose, ικανοποιώντας την απαίτηση “run OCR locally”.  
- **ResourcesPath** – Η μηχανή χρειάζεται τα αρχεία δεδομένων για την αποκωδικοποίηση χαρακτήρων. Χωρίς αυτά θα λάβετε `FileNotFoundException`.  
- **LoadLanguage** – Η φόρτωση μόνο της απαιτούμενης γλώσσας μειώνει την κατανάλωση μνήμης και επιταχύνει την αναγνώριση.  
- **Recognize** – Δέχεται οποιαδήποτε μορφή εικόνας υποστηρίζεται από .NET (`png`, `jpeg`, `bmp`). Για αυτόν τον οδηγό εστιάζουμε στο **recognize text png** επειδή το PNG διατηρεί την απώλεια‑ποιότητας ποιότητα, η οποία είναι ιδανική για OCR.  
- **Confidence** – Έλεγχος λογικής γρήγορης αξιολόγησης· τιμές πάνω από 80 % συνήθως σημαίνουν ότι η εξαγωγή είναι αξιόπιστη.

## Βήμα 4: Κατασκευή και Εκτέλεση της Εφαρμογής

Από τη ρίζα του έργου, εκτελέστε:

```bash
dotnet run
```

Αν όλα έχουν ρυθμιστεί σωστά, θα δείτε κάτι σαν:

```
=== OCR RESULT ===
中华人民共和国成立了
==================
Confidence: 93.45%
```

Αυτή η έξοδος επιβεβαιώνει ότι έχετε εξάγει με επιτυχία **extracted Chinese characters** από μια εικόνα PNG χωρίς να έχετε αγγίξει ποτέ το διαδίκτυο.

## Βήμα 5: Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Εξαγωγή Αγγλικού ή Πολυ‑γλωσσικού Κειμένου

Αν χρειάζεστε **extract text from image** αρχεία που περιέχουν τόσο Αγγλικά όσο και Κινέζικα, μπορείτε να φορτώσετε πολλαπλές γλώσσες:

```csharp
ocrEngine.LoadLanguages(LanguageModel.ChineseSimplified, LanguageModel.English);
```

Η μηχανή θα αλλάζει αυτόματα μεταξύ των γραφών κατά την αναγνώριση.

### Διαχείριση Μεγάλων Εικόνων

Για PNG με πολύ υψηλή ανάλυση, μπορεί να αντιμετωπίσετε πίεση μνήμης. Μια απλή λύση είναι να μειώσετε την κλίμακα της εικόνας πριν τη δώσετε στη μηχανή:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load, resize, and save a temporary copy
using (var original = new Bitmap(imagePath))
{
    int maxDim = 2000; // max width or height
    float scale = Math.Min((float)maxDim / original.Width, (float)maxDim / original.Height);
    int newW = (int)(original.Width * scale);
    int newH = (int)(original.Height * scale);

    using (var resized = new Bitmap(original, newW, newH))
    {
        string tempPath = Path.Combine(Path.GetTempPath(), "resized.png");
        resized.Save(tempPath, ImageFormat.Png);
        ocrResult = ocrEngine.Recognize(tempPath);
    }
}
```

### Αντιμετώπιση Σαρώσεων Χαμηλής Ποιότητας

Αν η τιμή confidence πέσει κάτω από 70 %, σκεφτείτε να εφαρμόσετε φίλτρα προεπεξεργασίας (π.χ., δυαδικοποίηση, αφαίρεση θορύβου). Το Aspose OCR εκθέτει μια μέθοδο `Preprocess` που μπορεί να συνδεθεί πριν από το `Recognize`.

## Pro Tips για Χρήση σε Παραγωγή

- **Cache the OcrEngine** – Η δημιουργία νέας μηχανής για κάθε αίτηση προσθέτει επιβάρυνση. Διατηρήστε μια singleton παρουσία αν χτίζετε μια web υπηρεσία.  
- **Secure the ResourcesPath** – Αποθηκεύστε τα αρχεία γλώσσας σε κατάλογο με περιορισμένα δικαιώματα για να αποφύγετε τυχόν παραβίαση.  
- **Log the Confidence** – Διατηρήστε την τιμή confidence μαζί με το εξαγόμενο κείμενο· είναι ανεκτίμητη όταν χρειάζεται να ελέγξετε την ακρίβεια του OCR.  
- **Version Lock** – Το API είναι σταθερό, αλλά κλειδώστε την έκδοση NuGet (`23.12.0`) στο `csproj` σας για να αποφύγετε απρόσμενες αλλαγές.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, αυτόνομη λύση που μπορεί να **recognize text png** αρχεία χρησιμοποιώντας το Aspose OCR .NET, **extract text from image** περιουσιακά στοιχεία, **run OCR locally**, και **extract Chinese characters** χωρίς εξωτερικές εξαρτήσεις. Ο κώδικας είναι έτοιμος να ενσωματωθεί σε μεγαλύτερη εφαρμογή, και οι εξηγήσεις σας δίνουν το πλαίσιο για να το προσαρμόσετε σε άλλες γλώσσες ή μορφές εικόνας.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να ενσωματώσετε τη μηχανή OCR σε ένα απλό ASP.NET Core API ώστε να μπορείτε να ανεβάζετε PNG μέσω HTTP και να λαμβάνετε αμέσως το εξαγόμενο κείμενο. Ή πειραματιστείτε με επεξεργασία παρτίδας—περιηγηθείτε σε έναν φάκελο εικόνων και γράψτε κάθε αποτέλεσμα σε αρχείο CSV. Ο ουρανός είναι το όριο, και έχετε τα θεμέλια για να προχωρήσετε μακριά.

Καλό προγραμματισμό, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα κρυστάλλινα! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}