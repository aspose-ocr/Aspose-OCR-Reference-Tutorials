---
category: general
date: 2026-05-25
description: Πώς να χρησιμοποιήσετε το OCR σε C# για την εξαγωγή κειμένου από αρχεία
  εικόνας. Μάθετε πώς να αναγνωρίζετε κινέζικους χαρακτήρες από ένα JPG χρησιμοποιώντας
  το Aspose.OCR σε λίγα απλά βήματα.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κειμένου από αρχεία
  εικόνας. Αυτός ο οδηγός σας δείχνει πώς να αναγνωρίζετε κινεζικούς χαρακτήρες από
  ένα JPG χρησιμοποιώντας το Aspose.OCR.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνώριση κινεζικού κειμένου από JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνώριση Κινέζικου κειμένου από JPG
url: /el/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε C# – Αναγνώριση Κινέζου Κειμένου από JPG

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε λέξεις από μια φωτογραφία που τραβήξατε με το τηλέφωνό σας; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε σαρωτές αποδείξεων, εφαρμογές μετάφρασης ή αυτοματοποιημένη εισαγωγή δεδομένων—θα χρειαστεί να **εξάγετε κείμενο από εικόνα** αρχεία γρήγορα και αξιόπιστα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που **αναγνωρίζει κείμενο από αρχεία JPG** και ακόμη χειρίζεται την δύσκολη περίπτωση **αναγνώρισης Κινέζων χαρακτήρων** χρησιμοποιώντας το γλωσσικό πακέτο **OCR Chinese Simplified**. Στο τέλος, θα έχετε μια αυτόνομη εφαρμογή κονσόλας που εκτυπώνει τη ανιχνευμένη συμβολοσειρά στην κονσόλα, χωρίς επιπλέον χειροκίνητες λήψεις.

> **Σύντομη σημείωση:** Ο κώδικας λειτουργεί με Aspose.OCR ≥ 23.7, το οποίο αυτόματα κατεβάζει τους γλωσσικούς πόρους στην πρώτη χρήση. Εάν χρησιμοποιείτε παλαιότερη έκδοση, θα πρέπει να προσθέσετε τη γλώσσα χειροκίνητα.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (το παράδειγμα στοχεύει στο .NET 6, αλλά το .NET 5 λειτουργεί επίσης)
- Μια πρόσφατη έκδοση του Visual Studio 2022 ή VS Code με την επέκταση C#
- Σύνδεση στο διαδίκτυο για τη πρώτη λήψη γλώσσας
- Μια εικόνα JPG που περιέχει κείμενο Simplified Chinese (θα την ονομάσουμε `chinese_sign.jpg`)

Αυτό είναι όλο—χωρίς βαριά μηχανήματα OCR, χωρίς χειρισμό εγγενών DLL. Μόνο μερικές εντολές NuGet και μερικές γραμμές κώδικα.

## Βήμα 1: Εγκατάσταση Aspose.OCR μέσω NuGet

Πρώτα απ' όλα: χρειαζόμαστε τη βιβλιοθήκη OCR. Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Ή, αν προτιμάτε το UI του Visual Studio, κάντε δεξί‑κλικ στο **Dependencies → Manage NuGet Packages**, αναζητήστε το “Aspose.OCR” και κάντε κλικ στο **Install**.

> **Συμβουλή:** Διατηρήστε τα πακέτα σας ενημερωμένα. Νέα γλωσσικά πακέτα και βελτιώσεις απόδοσης κυκλοφορούν σε κάθε μικρή έκδοση.

## Βήμα 2: Δημιουργία Νέου Console Project (Αν Δεν Το Έχετε Ήδη)

Αν ξεκινάτε από το μηδέν, δημιουργήστε μια νέα εφαρμογή console:

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

Τώρα έχετε ένα αρχείο `Program.cs` έτοιμο για τον κώδικα OCR.

## Βήμα 3: Γράψτε τον Κώδικα OCR – Αναγνώριση Simplified Chinese από JPG

Ανοίξτε το `Program.cs` και αντικαταστήστε το περιεχόμενό του με το παρακάτω. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε *γιατί* κάνουμε κάθε βήμα, όχι μόνο *τι* κάνουμε.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Τι συμβαίνει υπό το καπό;

- **`OcrEngine.Language`** λέει στο Aspose ποιο λεξικό να χρησιμοποιήσει. Επιλέγοντας το `ChineseSimplified`, καθοδηγούμε τη μηχανή να ψάξει για το γλωσσικό πακέτο Simplified Chinese.
- **Πρώτη λήψη**: Όταν εκτελείται το `Recognize`, το SDK επικοινωνεί με το CDN της Aspose, κατεβάζει το αρχείο γλώσσας ≈6 MB, το αποθηκεύει στην τοπική cache και στη συνέχεια προχωρά στην OCR. Οι επόμενες κλήσεις είναι άμεσες.
- **`Image.FromFile`** λειτουργεί με οποιαδήποτε μορφή raster που μπορεί να αποκωδικοποιήσει το .NET—JPG, PNG, BMP—οπότε μπορείτε να **εξάγετε κείμενο από εικόνα** αρχεία πολλών τύπων, όχι μόνο JPG.

## Βήμα 4: Εκτελέστε την Εφαρμογή και Επαληθεύστε το Αποτέλεσμα

Δομήστε και εκτελέστε:

```bash
dotnet run
```

Θα πρέπει να δείτε κάτι όπως:

```
=== Recognized Text ===
欢迎光临
```

Αν η κονσόλα εμφανίζει ακατανόητο κείμενο ή κενή συμβολοσειρά, ελέγξτε ξανά ότι:

1. Η εικόνα περιέχει πράγματι καθαρούς, υψηλής αντίθεσης κινέζους χαρακτήρες.
2. Η διαδρομή του αρχείου είναι σωστή (χωρίς περιττά κενά ή λείποντες τύπους αρχείων).
3. Η μηχανή σας μπορεί να φτάσει στο `https://download.aspose.com` για το γλωσσικό πακέτο.

## Βήμα 5: Διαχείριση Ακραίων Περιστατικών και Συνηθισμένων Παγίδων

### 5.1 Αντιμετώπιση Εικόνων Χαμηλής Ποιότητας

Η ακρίβεια του OCR μειώνεται όταν η πηγή εικόνας είναι θολή, θορυβώδης ή έχει φτωχή φωτισμό. Μια γρήγορη λύση είναι η προεπεξεργασία της εικόνας:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 Εκτέλεση σε Περιβάλλον Χωρίς GUI

Αν αναπτύσσετε σε κοντέινερ Linux χωρίς GUI, βεβαιωθείτε ότι η βιβλιοθήκη `libgdiplus` (απαιτούμενη για `System.Drawing`) είναι εγκατεστημένη:

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 Εγκατάσταση του Γλωσσικού Πακέτου με Χειροκίνητο Cache

Μπορείτε να κατεβάσετε το αρχείο γλώσσας μία φορά και να το δείξετε στο Aspose μέσω του API `License`, το οποίο εξαλείφει την εφάπαξ κλήση δικτύου. Αυτό είναι χρήσιμο για σενάρια εκτός σύνδεσης.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## Πλήρες Παράδειγμα Εργασίας (All‑In‑One)

Παρακάτω είναι το *πλήρες* πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`. Χωρίς κρυφά κομμάτια, χωρίς εξωτερικά scripts.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Αν το JPG περιέχει τη φράση “欢迎光临”, η κονσόλα θα εκτυπώσει:

```
=== Recognized Text ===
欢迎光临
```

Μπορείτε ελεύθερα να αντικαταστήσετε την εικόνα με οποιοδήποτε άλλο σήμα Simplified Chinese, οδικό όνομα ή ετικέτα προϊόντος—η μηχανή θα κάνει το καλύτερο δυνατό.

## Συμπέρασμα

Μόλις καλύψαμε **πώς να χρησιμοποιήσετε OCR** σε C# για **εξαγωγή κειμένου από εικόνα** αρχεία, αντιμετωπίζοντας συγκεκριμένα την πρόκληση της **αναγνώρισης Κινέζων χαρακτήρων** σε **JPG**. Χρησιμοποιώντας τη δυνατότητα λήψης γλώσσας εν κινήσει του Aspose.OCR, μπορείτε να διατηρήσετε την ανάπτυξή σας ελαφριά ενώ υποστηρίζετε το **OCR Chinese Simplified** έτοιμο προς χρήση.

Τι ακολουθεί; Δοκιμάστε αυτές τις ιδέες:

- **Batch processing**: Επανάληψη σε φάκελο εικόνων και εγγραφή κάθε αποτελέσματος σε CSV.
- **Συνδυασμός με APIs μετάφρασης**: Στείλτε τη αναγνωρισμένη συμβολοσειρά στο Azure Translator για εφαρμογές πολυγλωσσικής πραγματικού χρόνου.
- **Εξερευνήστε άλλες γλώσσες**: Αντικαταστήστε το `OcrLanguage.ChineseSimplified` με `Japanese` ή `Arabic` και δείτε πώς προσαρμόζεται ο ίδιος κώδικας.

Έχετε ερωτήσεις σχετικά με τη βελτιστοποίηση απόδοσης, την άδεια χρήσης ή την ενσωμάτωση OCR σε web service; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

---

![Στιγμιότυπο οθόνης της εξόδου της κονσόλας που δείχνει πώς να χρησιμοποιήσετε OCR σε C# για την αναγνώριση Κινέζου κειμένου από εικόνα JPG](ocr-chinese-demo.png "πώς να χρησιμοποιήσετε την έξοδο της κονσόλας OCR")

## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [αναγνώριση κειμένου εικόνας με Aspose OCR για πολλαπλές γλώσσες](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στην OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}