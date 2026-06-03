---
category: general
date: 2026-06-03
description: Παράδειγμα Aspose OCR σε C# που δείχνει πώς να ορίσετε όριο μνήμης GPU,
  να φορτώσετε εικόνα για OCR και να αναγνωρίσετε κείμενο από αρχεία TIF με πλήρη
  κώδικα και συμβουλές.
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: el
og_description: 'Μάθετε ένα πλήρες παράδειγμα Aspose OCR C#: ενεργοποίηση GPU, ορισμός
  ορίου μνήμης GPU, φόρτωση εικόνας για OCR και αναγνώριση κειμένου από αρχεία TIF.
  Περιλαμβάνεται ο πλήρης κώδικας.'
og_title: Παράδειγμα Aspose OCR C# – Επιτάχυνση GPU, Όριο Μνήμης & Επεξεργασία TIF
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Παράδειγμα Aspose OCR C# – Ενεργοποίηση GPU, Ορισμός ορίου μνήμης & Επεξεργασία
  εικόνων TIF
url: /el/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Παράδειγμα Aspose OCR C# – Ενεργοποίηση GPU, Ορισμός Ορίου Μνήμης & Επεξεργασία Εικόνων TIF

Έχετε αναρωτηθεί ποτέ πώς να εξάγετε την μέγιστη απόδοση από τον κώδικα **Aspose OCR C# example** όταν εργάζεστε με τεράστιες σάρωση TIFF; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—π.χ. ψηφιοποίηση αρχείων ή εξαγωγή δεδομένων από αποδείξεις υψηλής ανάλυσης—το στενό λαιμό δεν είναι ο αλγόριθμος OCR, αλλά η αξιοποίηση του υλικού.

Εδώ είναι το θέμα: το Aspose OCR υποστηρίζει επιτάχυνση GPU, αλλά πρέπει να του πείτε ακριβώς πόση μνήμη μπορεί να χρησιμοποιήσει, να φορτώσετε τον σωστό τύπο εικόνας και, τέλος, να εξάγετε το αναγνωρισμένο κείμενο από ένα αρχείο .tif. Αυτό το tutorial σας καθοδηγεί βήμα‑βήμα, από την εγκατάσταση του SDK μέχρι τη ρύθμιση του GPU, ώστε να τρέχετε OCR με αστραπιαία ταχύτητα χωρίς να εξαντλείτε τη μνήμη της GPU.

Θα προσθέσουμε επίσης μερικά σενάρια “τι γίνεται αν” — όπως η διαχείριση πολυ‑σελίδων TIFF ή η επιστροφή στη CPU όταν δεν υπάρχει GPU — ώστε να καταλήξετε με μια αξιόπιστη λύση, όχι μόνο με ένα αποσπασματικό κομμάτι κώδικα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στη μηχανή σας:

| Προαπαιτούμενο | Γιατί είναι σημαντικό |
|----------------|-----------------------|
| **.NET 6 SDK** (ή νεότερο) | Το Aspose OCR στοχεύει στο .NET Standard 2.0+, επομένως οποιαδήποτε πρόσφατη έκδοση του .NET λειτουργεί. |
| **Aspose.OCR NuGet package** (`Install-Package Aspose.OCR`) | Η κύρια βιβλιοθήκη που παρέχει `OcrEngine`, `GpuSettings`, κ.λπ. |
| **CUDA 11+** (NVIDIA) **ή ROCm 5+** (AMD) | Απαιτείται για επιτάχυνση GPU· το SDK θα ελέγξει για συμβατό οδηγό κατά την εκτέλεση. |
| Μια **GPU με τουλάχιστον 2 GB VRAM** (θα περιορίσουμε στα 2048 MB) | Χωρίς αρκετή μνήμη, η μηχανή μπορεί να επιστρέψει σιωπηλά στη CPU. |
| Μια **υψηλής ανάλυσης εικόνα TIFF** που θέλετε να επεξεργαστείτε | Το Aspose OCR μπορεί να διαβάσει σχεδόν οποιαδήποτε μορφή raster, αλλά το TIF είναι κοινό για σάρωση. |
| Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε) | Για τη δημιουργία και αποσφαλμάτωση του έργου C#. |

Αν λείπει κάποιο από αυτά, ο κώδικας θα μεταγλωττιστεί, αλλά δεν θα δείτε τις επιδόσεις που επιδιώκουμε.

## Βήμα 1: Δημιουργία της Μηχανής Aspose OCR C# Example

Το πρώτο βήμα σε κάθε **Aspose OCR C# example** είναι η δημιουργία μιας στιγμής του OCR engine. Σκεφτείτε το `OcrEngine` ως τον σκηνοθέτη μιας ταινίας — συντονίζει τα πάντα, από τη φόρτωση της εικόνας μέχρι την εξαγωγή του κειμένου.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Pro tip:** Αν σκοπεύετε να επεξεργαστείτε πολλές εικόνες διαδοχικά, κρατήστε ζωντανή μια μόνο `OcrEngine`. Η επανδημιουργία της για κάθε εικόνα προσθέτει επιπλέον φόρτο που μπορεί να υπερκαλύψει τον χρόνο OCR.

## Βήμα 2: Ορισμός Ορίου Μνήμης GPU (και Ενεργοποίηση Επιτάχυνσης)

Τώρα έρχεται το μέρος που συχνά προκαλεί προβλήματα: **ορισμός ορίου μνήμης GPU**. Από προεπιλογή, το Aspose OCR θα προσπαθήσει να χρησιμοποιήσει όλη τη διαθέσιμη VRAM, κάτι που σε κοινόχρηστη σταθμό εργασίας μπορεί να στερήσει άλλες εφαρμογές από πόρους. Το αντικείμενο `GpuSettings` σας επιτρέπει να περιορίσετε αυτήν την εκχώρηση.

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### Γιατί να ορίσετε όριο μνήμης;

- **Stability:** Αποτρέπει καταρρίψεις λόγω έλλειψης μνήμης όταν επεξεργάζεστε τεράστιες εικόνες.  
- **Co‑existence:** Επιτρέπει σε άλλες εφαρμογές βαριάς χρήσης GPU (π.χ. μοντέλα TensorFlow) να λειτουργούν παράλληλα.  
- **Predictability:** Κάνει τις δοκιμές απόδοσης επαναλήψιμες, επειδή η GPU δεν θα ξεκινήσει ανταλλαγή (swapping).

Αν παραλείψετε το `MemoryLimitMb`, το Aspose θα εκχωρήσει ό,τι κρίνει απαραίτητο, κάτι που μπορεί να είναι εντάξει σε dedicated server, αλλά είναι ριψοκίνδυνο σε φορητό υπολογιστή προγραμματιστή.

## Βήμα 3: Φόρτωση Εικόνας για OCR

Η φόρτωση του σωστού τύπου αρχείου είναι το επόμενο κρίσιμο βήμα. Η μέθοδος `OcrImage.FromFile` ανιχνεύει αυτόματα τον τύπο της εικόνας, αλλά θα πρέπει να ελέγξετε ότι το αρχείο υπάρχει και ότι είναι μια υποστηριζόμενη παραλλαγή TIFF (π.χ. LZW‑compressed ή CCITT‑G4).

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### Διαχείριση πολυ‑σελίδων TIFF

Αν το TIFF σας περιέχει πολλές σελίδες, το Aspose OCR θα διαβάσει μόνο την πρώτη από προεπιλογή. Για να επεξεργαστείτε όλες τις σελίδες, μπορείτε να κάνετε βρόχο πάνω στο `image.Pages` (διαθέσιμο σε νεότερες εκδόσεις SDK) και να περάσετε κάθε σελίδα στη μηχανή ξεχωριστά.

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

Το παραπάνω απόσπασμα δείχνει ένα πρότυπο **load image for OCR** που λειτουργεί τόσο για μονο‑ όσο και για πολυ‑σελίδες αρχεία.

## Βήμα 4: Αναγνώριση Κειμένου από TIF (ή οποιοδήποτε raster)

Τώρα που η εικόνα βρίσκεται στη μνήμη, ζητάμε από το Aspose να κάνει τη μαγεία του. Η μέθοδος `Recognize` επιστρέφει ένα `OcrResult` που περιέχει το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη πληροφορίες bounding‑box αν τις χρειάζεστε.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### Γιατί αυτό λειτουργεί καλά με TIF

- **Lossless compression:** Τα TIFF συχνά αποθηκεύουν ακατέργαστα δεδομένα εικονοστοιχείων, παρέχοντας στην μηχανή OCR τη μέγιστη πιστότητα.  
- **Multiple color spaces:** Το Aspose μπορεί να διαχειριστεί grayscale, RGB ή ακόμη και CMYK TIFF χωρίς επιπλέον κώδικα μετατροπής.

Αν χρειάζεται να ρυθμίσετε πακέτα γλώσσας (π.χ. Γαλλικά ή Ιαπωνικά), ορίστε `ocrEngine.Settings.Language = "fr"` πριν καλέσετε το `Recognize`.

## Βήμα 5: Εμφάνιση του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώνουμε το κείμενο στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να γράψετε σε βάση δεδομένων, σε αρχείο JSON ή να περάσετε τη συμβολοσειρά σε επόμενη διαδικασία NLP.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Αναμενόμενη έξοδος

Εκτελώντας το πρόγραμμα σε μια καθαρή σάρωση 300 dpi μιας τυπωμένης σελίδας συνήθως παίρνετε κάτι σαν:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

Αν η εικόνα είναι θολή ή το όριο μνήμης GPU είναι πολύ χαμηλό, μπορεί να δείτε ακατάστατους χαρακτήρες ή κομμένο αποτέλεσμα. Η μείωση του `MemoryLimitMb` κάτω από το αποτύπωμα της εικόνας (συχνά ~1 GB για TIFF 6000×8000 pixel) μπορεί να κάνει τη μηχανή να επιστρέψει αυτόματα στη CPU.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο Console App project, αντικαταστήστε `YOUR_DIRECTORY/large_photo.tif` με τη διαδρομή του δικού σας TIFF και πατήστε **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Γρήγορη λίστα ελέγχου

- ✅ **Aspose OCR C# example** compiled without errors.  
- ✅ **GPU enabled** (`Enable = true`).  
- ✅ **GPU memory limit** set to 2048 MB.  
- ✅ **Image loaded** from a TIF file.  
- ✅ **Text recognized** and printed.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| `System.DllNotFoundException: cudart64_110.dll` | CUDA runtime not installed or version mismatch. | Install CUDA 11.x (or 12.x) matching your driver. |
| OCR returns empty string | Image is too dark or DPI < 150. | Pre‑process with `image.AdjustContrast()` or resample to 300 dpi. |
| Out‑of‑memory crash on GPU | `MemoryLimitMb` too low for the image. | Raise the limit or split the image into tiles via `image.Crop`. |
| `Unsupported image format` error | TIFF uses an exotic compression (e.g., JPEG‑2000). | Convert the TIFF to a supported format with ImageMagick before OCR. |

## Επέκταση της Επίδειξης

Τώρα που έχετε ένα σταθερό **aspose ocr c# example**, ίσως θέλετε να εξερευνήσετε:

- **Batch processing:** Loop over a folder of TIFs, write each result to a `.txt` file.  
- **Language packs:** `ocrEngine.Settings.Language = "es"` for Spanish, or load custom dictionaries.  
- **Bounding boxes:** Use `ocrResult.Regions` to get coordinates for each word—handy for redaction tools.  
- **CPU fallback:** Wrap the GPU block in a try/catch; on failure, set `ocrEngine.Settings.Gpu.Enable = false` and retry.  

These extensions keep the core pattern intact while adding value for specific use‑

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}