---
category: general
date: 2026-05-06
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέπετε JPG σε κείμενο, να ορίζετε τη γλώσσα OCR και να διαβάζετε κείμενο
  από JPG αποδοτικά.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: el
og_description: Εξαγωγή κειμένου από εικόνα σε C# με Aspose OCR. Αυτός ο οδηγός δείχνει
  πώς να μετατρέψετε JPG σε κείμενο, να ορίσετε τη γλώσσα OCR και να διαβάσετε κείμενο
  από JPG.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός
tags:
- OCR
- C#
- Aspose
title: Εξαγωγή κειμένου από εικόνα σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αλλά δεν ήξερτε ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι—οι προγραμματιστές συχνά ρωτούν, «Πώς μπορώ να μετατρέψω ένα JPG σε κείμενο χωρίς να στέλνω δεδομένα στο cloud;» Τα καλά νέα είναι ότι το Aspose OCR σας παρέχει μια πλήρως offline λύση που λειτουργεί απευθείας μέσα στην .NET εφαρμογή σας.

Σε αυτό το tutorial θα καλύψουμε όλα όσα χρειάζεται να γνωρίζετε: από την εγκατάσταση του πακέτου NuGet Aspose OCR, μέχρι το **ορισμό της γλώσσας OCR** για ρωσικό κείμενο, και τέλος το **διάβασμα κειμένου από αρχεία JPG**. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C# και να αρχίσετε άμεσα να εξάγετε κείμενο από εικόνες.

> **Τι θα αποκομίσετε**  
> • Ένα σαφές, εκτελέσιμο παράδειγμα που **εξάγει κείμενο από εικόνα** αρχεία.  
> • Γνώση για το πώς να **μετατρέψετε JPG σε κείμενο** χρησιμοποιώντας τη μηχανή Aspose OCR.  
> • Συμβουλές για τη διαμόρφωση του **set OCR language** για πολυγλωσσικά σενάρια.  
> • Διαχείριση edge‑case για μη αναγνώσιμες εικόνες και ελλιπείς γλωσσικά πακέτα.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| .NET 6.0 ή νεότερο (οποιοδήποτε πρόσφατο .NET runtime) | Το Aspose OCR στοχεύει στο .NET Standard 2.0+, επομένως τα νεότερα runtimes προσφέρουν την καλύτερη απόδοση. |
| Visual Studio 2022 (ή VS Code με επεκτάσεις C#) | Ένα φιλικό IDE σας βοηθά να εντοπίσετε γρήγορα τη ροή του OCR. |
| Πρόσβαση στο Internet **μία φορά** για λήψη του πακέτου NuGet Aspose OCR | Μετά την πρώτη εγκατάσταση μπορείτε να ενεργοποιήσετε **offline resources** για να αποφύγετε περαιτέρω λήψεις. |
| Ένα δείγμα εικόνας JPG (`input.jpg`) που περιέχει ρωσικό κείμενο (ή οποιαδήποτε γλώσσα σκοπεύετε να χρησιμοποιήσετε) | Το tutorial χρησιμοποιεί ένα ρωσικό παράδειγμα, αλλά μπορείτε να αντικαταστήσετε με οποιοδήποτε γλωσσικό πακέτο έχετε εγκαταστήσει. |

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε. Η εγκατάσταση ενός πακέτου NuGet είναι τόσο απλή όσο η πληκτρολόγηση μιας εντολής, και τα υπόλοιπα βήματα λειτουργούν το ίδιο για κάθε μορφή εικόνας που υποστηρίζει το Aspose.

## Επισκόπηση της Λύσης

Σε υψηλό επίπεδο η διαδικασία φαίνεται ως εξής:

1. **Δημιουργήστε** ένα `OcrEngine` με offline resources ώστε η βιβλιοθήκη να μην προσπαθήσει να κατεβάσει δεδομένα γλώσσας κατά την εκτέλεση.  
2. **Ορίστε** τη ζητούμενη γλώσσα (π.χ., Russian) χρησιμοποιώντας το enum `OcrLanguage`.  
3. **Καλέστε** `RecognizeImage` σε ένα τοπικό αρχείο JPG.  
4. **Εκτυπώστε** τη εξαγόμενη συμβολοσειρά στην κονσόλα ή προωθήστε την στη δική σας ροή εργασίας.

Παρακάτω υπάρχει ένα γρήγορο διάγραμμα που απεικονίζει τη ροή των δεδομένων:

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#"}

*Το διάγραμμα είναι καθαρά εικονογραφικό· ο κώδικας κάνει τη βαριά δουλειά.*

## Εξαγωγή Κειμένου από Εικόνα – Βασικές Έννοιες

Πριν αρχίσουμε να γράφουμε κώδικα, ας αναλύσουμε μερικές έννοιες που συχνά δυσκολεύουν τους προγραμματιστές:

- **OfflineResources** – Όταν είναι `true`, το Aspose OCR αναζητά τα γλωσσικά πακέτα που έχετε προ‑κατεβάσει. Αυτό εξαλείφει το βήμα “auto‑download” που μπορεί να επιβραδύνει την εκκίνηση σε περιβάλλοντα παραγωγής.  
- **OcrLanguage** – Το enum περιέχει δεκάδες αναγνωριστικά γλωσσών (`English`, `Russian`, `Japanese`, …). Η επιλογή του σωστού βελτιώνει δραματικά την ακρίβεια, επειδή η μηχανή μπορεί να εφαρμόσει γλωσσικές ειδικές ευρετικές.  
- **Image quality** – Το OCR λειτουργεί καλύτερα σε εικόνες υψηλής αντίθεσης και χωρίς θόρυβο. Αν λάβετε ακατάλληλα αποτελέσματα, σκεφτείτε προεπεξεργασία (π.χ., δυαδικοποίηση) πριν τροφοδοτήσετε την εικόνα στη μηχανή.

Η κατανόηση αυτών των σημείων θα σας βοηθήσει να αποφασίσετε πότε να **ορίσετε τη γλώσσα OCR** χειροκίνητα αντί να βασίζεστε στην αυτόματη ανίχνευση, και γιατί το **convert JPG to text** δεν είναι απλώς μια γραμμή κώδικα.

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose OCR

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

*Συμβουλή:* Μετά την πρώτη εγκατάσταση, προσθέστε `-v latest` για να εξασφαλίσετε ότι λαμβάνετε πάντα την πιο πρόσφατη σταθερή έκδοση. Το μέγεθος του πακέτου είναι περίπου 15 MB, κάτι λογικό για τις περισσότερες εγκαταστάσεις σε επιτραπέζιους ή διακομιστές.

## Βήμα 2: Convert JPG to Text – Αρχικοποίηση της Μηχανής

Τώρα που η βιβλιοθήκη είναι στον υπολογιστή σας, ας δημιουργήσουμε ένα `OcrEngine` που λειτουργεί offline.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### Γιατί είναι σημαντικό

- **Offline mode** εγγυάται προβλέψιμους χρόνους εκκίνησης—χωρίς απρόσμενες κλήσεις δικτύου όταν αναπτύσσετε σε κλειδωμένο διακομιστή.  
- **Ορισμός της γλώσσας** (`OcrLanguage.Russian`) λέει στη μηχανή να χρησιμοποιήσει το ρωσικό σύνολο χαρακτήρων, βελτιώνοντας την ακρίβεια αναγνώρισης από ~70 % σε >95 % για καθαρές εικόνες.  
- Η μέθοδος `RecognizeImage` δέχεται οποιαδήποτε μορφή εικόνας που υποστηρίζει το Aspose (`.jpg`, `.png`, `.tiff`, …). Γι' αυτό μπορούμε να **διαβάσουμε κείμενο από JPG** χωρίς επιπλέον βήματα μετατροπής.

## Βήμα 3: Set OCR Language – Διαχείριση Πολλαπλών Γλωσσών

Μερικές φορές χρειάζεται να επεξεργαστείτε έγγραφα που περιέχουν μικτές γλώσσες (π.χ., Russian και English). Το Aspose OCR σας επιτρέπει να ορίσετε έναν *fallback* πίνακα γλωσσών:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

Όταν η κύρια γλώσσα αποτύχει να αναγνωρίσει έναν χαρακτήρα, η μηχανή ελέγχει αυτόματα τη συμπληρωματική λίστα. Αυτή η τεχνική είναι ιδιαίτερα χρήσιμη για τιμολόγια που συνδυάζουν κυριλλικά ονόματα εταιρειών με αγγλικούς κωδικούς προϊόντων.

> **Σημείωση:** Τα γλωσσικά πακέτα πρέπει να βρίσκονται στο φάκελο `Resources` του έργου σας. Αν λάβετε `FileNotFoundException`, κατεβάστε το ελλιπές πακέτο από το portal του Aspose και τοποθετήστε το δίπλα στο εκτελέσιμο.

## Βήμα 4: Read Text from JPG – Συνηθισμένα Προβλήματα & Διορθώσεις

Ακόμη και με το σωστό γλωσσικό πακέτο, μπορεί να αντιμετωπίσετε:

| Πρόβλημα | Τυπικό Συμπτωμα | Γρήγορη Διόρθωση |
|----------|------------------|-------------------|
| Χαμηλή αντίθεση | Ακατάλληλη ή κενή έξοδος | Εφαρμόστε ένα απλό φίλτρο ενίσχυσης αντίθεσης χρησιμοποιώντας `System.Drawing` πριν το OCR. |
| Περιστραμμένη εικόνα | Το κείμενο εμφανίζεται πλαγίως | Χρησιμοποιήστε `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (ή 180/270) πριν καλέσετε `RecognizeImage`. |
| Μεγάλο μέγεθος αρχείου | Αργή αναγνώριση, υψηλή χρήση μνήμης | Αλλάξτε το μέγεθος της εικόνας σε μέγιστο 2000 px στην μεγαλύτερη πλευρά· η ποιότητα OCR παραμένει υψηλή. |

Ακολουθεί ένας σύντομος βοηθός που αλλάζει το μέγεθος και βελτιώνει μια εικόνα πριν τη δώσετε στη μηχανή:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

Τώρα μπορείτε να καλέσετε `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` και να λάβετε ένα καθαρότερο αποτέλεσμα.

## Πλήρες Παράδειγμα Εργασίας – Όλα τα Βήματα σε Ένα Αρχείο

Παρακάτω είναι το *πλήρες* πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει σημειώσεις εγκατάστασης, διαμόρφωση γλώσσας, προεπεξεργασία και διαχείριση σφαλμάτων.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}