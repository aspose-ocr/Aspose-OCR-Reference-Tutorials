---
category: general
date: 2026-03-17
description: c# OCR οδηγός – ανακαλύψτε πώς να εξάγετε κείμενο από αρχεία εικόνας,
  διαβάστε κείμενο από φωτογραφίες WebP και μετατρέψτε εικόνα σε κείμενο χρησιμοποιώντας
  ένα απλό OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: el
og_description: Το σεμινάριο C# OCR σας δείχνει πώς να εξάγετε κείμενο από αρχεία
  εικόνας, να διαβάζετε κείμενο από φωτογραφίες WebP και να μετατρέπετε εικόνα σε
  κείμενο με λίγες γραμμές κώδικα.
og_title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνες σε λίγα λεπτά
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR tutorial: Εξαγωγή κειμένου από εικόνες (WebP, Φωτογραφία) – Σύντομος
  οδηγός'
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Εξαγωγή Κειμένου από Εικόνες (WebP, Φωτογραφία)

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις σε C#; Ίσως έχετε ένα στιγμιότυπο WebP, ένα JPEG από απόδειξη, ή μια σαρωμένη σελίδα PDF και θέλετε απλώς τις λέξεις μέσα. Σε αυτό το **c# OCR tutorial** θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που διαβάζει κείμενο από μια φωτογραφία, διαχειρίζεται WebP και άλλες σύγχρονες μορφές, και μετατρέπει την εικόνα σε απλό κείμενο—όλα σε λίγες γραμμές.

**Ποιο είναι το όφελος;** Θα μπορείτε να μετατρέψετε οποιαδήποτε εικόνα κειμένου σε αναζητήσιμες συμβολοσειρές, να τις εισάγετε σε βάσεις δεδομένων ή να τις δώσετε σε επόμενα AI pipelines. Χωρίς μαγεία, μόνο μια αξιόπιστη μηχανή OCR, μερικά .NET APIs, και σαφείς εξηγήσεις του “γιατί” πίσω από κάθε βήμα.

## Τι Θα Χρειαστείτε

- **.NET 6 SDK** (ή νεότερο). Ο κώδικας παρακάτω μεταγλωττίζεται με .NET 6+ και εκτελείται σε Windows, Linux ή macOS.
- **Visual Studio 2022** ή οποιονδήποτε επεξεργαστή προτιμάτε (VS Code λειτουργεί καλά).
- Το πακέτο NuGet **`Microsoft.Windows.SDK.Contracts`** (παρέχει `Windows.Media.Ocr`). Εγκαταστήστε το με:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε – για αυτό το tutorial θα χρησιμοποιήσουμε μια **WebP** φωτογραφία με όνομα `photo.webp` τοποθετημένη σε φάκελο που ονομάζεται `YOUR_DIRECTORY`.

> Συμβουλή: Αν βρίσκεστε σε μη‑Windows πλατφόρμα, μπορείτε να αντικαταστήσετε το `OcrEngine` με μια cross‑platform βιβλιοθήκη όπως **Tesseract**. Ο υπόλοιπος κώδικας παραμένει σχεδόν αμετάβλητος.

## Βήμα 1: Ρύθμιση ενός C# OCR Tutorial Project

Πρώτα, δημιουργήστε μια νέα console εφαρμογή. Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Προσθέστε το απαιτούμενο πακέτο (όπως φαίνεται παραπάνω) και ανοίξτε το έργο στο IDE σας. Αυτή η δομή μας δίνει ένα καθαρό ξεκίνημα για το **c# OCR tutorial**.

## Βήμα 2: Εισαγωγή Namespaces και Προετοιμασία της Εικόνας

Χρειαζόμαστε μερικές οδηγίες `using` ώστε ο μεταγλωττιστής να ξέρει πού να βρει το `OcrEngine`, το `SoftwareBitmap` και τα βοηθήματα φόρτωσης εικόνας.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Γιατί αυτά τα namespaces;**  
> `Windows.Media.Ocr` φιλοξενεί την κλάση `OcrEngine` που πραγματικά εκτελεί την αναγνώριση. `Windows.Graphics.Imaging` μας επιτρέπει να αποκωδικοποιήσουμε την εικόνα (συμπεριλαμβανομένου του WebP) σε ένα `SoftwareBitmap` που η μηχανή μπορεί να καταλάβει. Τα βοηθήματα `System.IO` και `Windows.Storage.Streams` κάνουν τη φόρτωση αρχείων εύκολη.

Τώρα, φορτώστε την εικόνα. Ο ενσωματωμένος αποκωδικοποιητής μπορεί να διαχειριστεί WebP, HEIF, PNG, JPEG, και άλλα, ώστε να μπορείτε να **διαβάσετε κείμενο από WebP** χωρίς πρόσθετα plugins.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Edge case:** Αν η εικόνα σας είναι ήδη ασπρόμαυρη, μπορείτε να παραλείψετε το βήμα μετατροπής. Η μετατροπή σε γκρι κλίμακα είναι μια μικρή βελτίωση απόδοσης και συχνά βελτιώνει την αναγνώριση σε θορυβώδεις φωτογραφίες.

## Βήμα 3: Εκτέλεση του OCR Engine – Αναγνώριση Κειμένου από Φωτογραφία

Αυτή είναι η καρδιά του **c# OCR tutorial**. Δημιουργούμε μια παρουσία του `OcrEngine`, την τροφοδοτούμε με το bitmap, και εξάγουμε το αναγνωρισμένο κείμενο.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Τι συμβαίνει;**  
- `TryCreateFromUserProfileLanguages()` επιλέγει τη γλώσσα(ες) που έχει οριστεί στο προφίλ χρήστη των Windows, που συνήθως καλύπτει Αγγλικά, Ισπανικά κλπ. Αν χρειάζεστε συγκεκριμένη γλώσσα, χρησιμοποιήστε `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` εκτελεί το βαρέως βάρους σε νήμα παρασκηνίου, επιστρέφοντας ένα `OcrResult` που περιέχει τη ακατέργαστη συμβολοσειρά, τα πλαίσια των λέξεων και τις βαθμολογίες εμπιστοσύνης.  
- Τέλος, εκτυπώνουμε το `ocrResult.Text`, δίνοντάς σας το αποτέλεσμα **convert image to text** που μπορείτε να μεταβιβάσετε αλλού.

## Βήμα 4: Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Μεταγλωττίζεται, εκτελείται, και εκτυπώνει το κείμενο που εξήχθη από το `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Αναμενόμενη Έξοδος

Αν το `photo.webp` περιέχει την πρόταση “Hello, world! This is a test.” θα δείτε κάτι σαν:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Οι ακριβείς αλλαγές γραμμής εξαρτώνται από τη διάταξη της πηγαίας εικόνας, αλλά το αποτέλεσμα **extract text from image** θα είναι πάντα μια απλή συμβολοσειρά που μπορείτε να επεξεργαστείτε περαιτέρω.

## Συχνές Ερωτήσεις & Edge Cases

### Λειτουργεί αυτό με άλλες μορφές εικόνας;

Απολύτως. Ο αποκωδικοποιητής που χρησιμοποιείται (`BitmapDecoder`) εντοπίζει αυτόματα JPEG, PNG, BMP, GIF, **WebP**, HEIF, και άλλα. Έτσι μπορείτε να **διαβάσετε κείμενο από WebP**, JPEG, ή ακόμη και TIFF χωρίς να αλλάξετε τον κώδικα.

### Τι γίνεται αν η μηχανή OCR επιστρέψει χαμηλή εμπιστοσύνη;

Μπορείτε να ελέγξετε το `ocrResult.Lines` και κάθε `OcrWord` για `ConfidenceScore`. Αν η βαθμολογία είναι κάτω από ένα όριο (π.χ., 0.6), σκεφτείτε:
- Προεπεξεργασία της εικόνας (αύξηση αντίθεσης, ευκρίνιση, διόρθωση κλίσης).
- Χρήση εικόνας υψηλότερης ανάλυσης.
- Μετάβαση σε εξειδικευμένη βιβλιοθήκη όπως **Tesseract** για πολυγλωσσική υποστήριξη.

### Πώς να διαχειριστείτε πολλές γλώσσες στην ίδια εικόνα;

Δημιουργήστε ξεχωριστές παρουσίες `OcrEngine` για κάθε γλώσσα και τρέξτε τις διαδοχικά, ή χρησιμοποιήστε βιβλιοθήκη που υποστηρίζει ανίχνευση μικτής γλώσσας. Για την ενσωματωμένη μηχανή, μπορείτε να περάσετε ένα αντικείμενο `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Μπορώ να το τρέξω σε Linux/macOS;

Το API `Windows.Media.Ocr` είναι μόνο για Windows. Σε μη‑Windows πλατφόρμες, αντικαταστήστε το τμήμα OCR με **Tesseract** (μέσω `Tesseract.Net.SDK`). Ο κώδικας φόρτωσης και προεπεξεργασίας παραμένει ίδιος, έτσι το υπόλοιπο αυτού του **c# OCR tutorial** εξακολουθεί να ισχύει.

## Pro Tips για Καλύτερη Ακρίβεια

- **Resize** μεγάλες εικόνες σε μέγιστο 2000 px στην μεγαλύτερη πλευρά – οι μηχανές OCR λειτουργούν γρηγορότερα σε μέτρια μεγέθη.
- **Denoise** χρησιμοποιώντας απλό Gaussian blur αν η φωτογραφία είναι θολή.
- **Deskew** το bitmap αν το κείμενο δεν είναι τέλεια οριζόντιο· το `SoftwareBitmap` μπορεί να περιστραφεί πριν περάσει στο `OcrEngine`.
- **Cache** την παρουσία `OcrEngine` αν επεξεργάζεστε πολλές εικόνες σε παρτίδα· η επαναλαμβανόμενη δημιουργία προσθέτει επιβάρυνση.

## Σχετικά Θέματα για Εξερεύνηση

- **Convert image to text** χρησιμοποιώντας **Tesseract** για cross‑platform έργα.
- **Extract text from PDF** με απόδοση κάθε σελίδας σε εικόνα πρώτα.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}