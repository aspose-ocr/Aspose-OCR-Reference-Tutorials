---
category: general
date: 2026-06-03
description: Εκπαιδευτικό βίντεο OCR υποτίτλων που δείχνει πώς να εξάγετε καρέ από
  βίντεο και να διαβάζετε κείμενο από αρχεία βίντεο όπως MP4 χρησιμοποιώντας το Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: el
og_description: Μάθετε OCR υποτίτλων βίντεο με το Aspose.OCR. Εξάγετε καρέ από βίντεο,
  διαβάστε κείμενο από βίντεο και εξάγετε κείμενο από MP4 σε λίγα λεπτά.
og_title: OCR Υπότιτλων Βίντεο σε C# – Οδηγός Βήμα‑Βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR Υπότιτλων Βίντεο σε C# – Πλήρης Οδηγός
url: /el/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Υπότιτλων Βίντεο σε C# – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί **video subtitle ocr** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Είτε ψηφιοποιείτε ηχογραφήσεις διαλέξεων, είτε εξάγετε υπότιτλους από εκπαιδευτικά βίντεο, είτε απλώς θέλετε να **διαβάσετε κείμενο από βίντεο** αρχεία—συμπεριλαμβανομένου του MP4—χωρίς να ψάχνετε για τρίτα εργαλεία.

## Τι Θα Δημιουργήσετε

1. Αποκωδικοποιεί ένα MP4 (ή οποιαδήποτε υποστηριζόμενη μορφή) σε μεμονωμένα `Bitmap` καρέ.  
2. Περιορίζει την περιοχή OCR στη ζώνη των υποτίτλων ώστε η μηχανή να μην αποσπάται από ολόκληρη την εικόνα.  
3. Επεξεργάζεται κάθε καρέ με το `VideoOcrProcessor` της Aspose.  
4. Εκτυπώνει το αναγνωρισμένο κείμενο υποτίτλων στην κονσόλα.

Χωρίς περιττά, μόνο ένα λειτουργικό παράδειγμα end‑to‑end που μπορείτε να ενσωματώσετε σε ένα πραγματικό έργο.

## Προαπαιτούμενα

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – εγκαταστήστε μέσω NuGet: `Install-Package Aspose.OCR`.  
- Ένα αρχείο βίντεο (το MP4 λειτουργεί άψογα).  
- Ένας τρόπος για την αποκωδικοποίηση των καρέ του βίντεο – η demo χρησιμοποιεί μια placeholder μέθοδο, αλλά μπορείτε να ενσωματώσετε FFmpeg, OpenCV ή οποιαδήποτε βιβλιοθήκη που επιστρέφει αντικείμενα `Bitmap`.  

> Συμβουλή: Αν χρησιμοποιείτε Windows, το πακέτο `System.Drawing.Common` λειτουργεί καλά για `Bitmap`. Σε Linux/macOS θα χρειαστείτε την εγγενή εξάρτηση `libgdiplus`.

## Βήμα 1 – Εξαγωγή Καρέ από Βίντεο

Το πρώτο εμπόδιο είναι η μετατροπή μιας κινούσας εικόνας σε στατικές εικόνες. Η μέθοδος `GetVideoFrames` παρακάτω είναι σκόπιμα κενή· αντικαταστήστε την με τον αγαπημένο σας αποκωδικοποιητή. Εδώ είναι ένα γρήγορο σκίτσο χρησιμοποιώντας FFmpeg‑Core (απλώς για να δείξει τη δομή των δεδομένων):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Γιατί είναι σημαντικό:** Η εξαγωγή καρέ παρέχει στη μηχανή OCR μια στατική εικόνα για επεξεργασία, κάτι που βελτιώνει δραματικά την ακρίβεια σε σύγκριση με την προσπάθεια ανάγνωσης απευθείας από ροή βίντεο.

## Βήμα 2 – Ρύθμιση του VideoOcrProcessor

Τώρα που έχουμε μια ακολουθία αντικειμένων `Bitmap`, μπορούμε να τα περάσουμε στο Aspose.OCR. Το `VideoOcrProcessor` μας επιτρέπει να ορίσουμε μια **Region of Interest (ROI)** – ιδανική για υπότιτλους που συνήθως βρίσκονται στην κορυφή ή στο κάτω μέρος του καρέ.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Γιατί να περιορίσουμε το ROI;** Αγνοώντας το υπόλοιπο της εικόνας μειώνουμε τον θόρυβο, μειώνουμε το χρόνο επεξεργασίας και αποφεύγουμε ψευδώς θετικά αποτελέσματα από γραφικά φόντου.

## Βήμα 3 – Εκτέλεση OCR στην Ακολουθία Καρέ

Με τον επεξεργαστή έτοιμο, η τροφοδοσία των καρέ γίνεται με μία γραμμή κώδικα. Η μέθοδος `Process` επιστρέφει ένα enumerable από αντικείμενα `OcrResult`, το καθένα περιέχει το αναγνωρισμένο κείμενο για το αντίστοιχο καρέ.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Τι συμβαίνει εσωτερικά;** Το Aspose.OCR κανονικοποιεί εσωτερικά κάθε bitmap, εκτελεί έναν αναγνωριστή βασισμένο σε νευρωνικό δίκτυο και στη συνέχεια επεξεργάζεται το αποτέλεσμα για να βελτιώσει την στίξη και τις αλλαγές γραμμής.

## Βήμα 4 – Εμφάνιση του Εξαγόμενου Κειμένου

Τέλος, επαναλαμβάνουμε τα αποτελέσματα και εκτυπώνουμε κάθε γραμμή υποτίτλου. Μπορείτε επίσης να τα γράψετε σε αρχείο SRT, σε βάση δεδομένων ή να τα στείλετε σε υπηρεσία μετάφρασης.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω προκύπτει ένα αυτόνομο πρόγραμμα κονσόλας:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Αν το OCR αντιμετωπίζει δυσκολίες με κάποιο συγκεκριμένο καρέ, θα δείτε μια κενή συμβολοσειρά – αυτό είναι ένδειξη να προσαρμόσετε το ROI ή να αυξήσετε το ρυθμό εξαγωγής καρέ.

## Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Διορθώσετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Αχρείαστοι χαρακτήρες** | Καρέ χαμηλής ανάλυσης ή έντονη συμπίεση | Εξάγετε καρέ με υψηλότερο bitrate, ή αυξήστε την ανάλυση του bitmap πριν το OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **Δεν επιστράφηκε κείμενο** | Το ROI δεν καλύπτει πραγματικά τη ζώνη των υποτίτλων | Επαληθεύστε τις συντεταγμένες του ορθογωνίου (χρησιμοποιήστε εργαλείο στιγμιότυπου για μέτρηση). |
| **Σημείο συμφόρησης απόδοσης** | Η επεξεργασία κάθε καρέ στα 30 fps είναι υπερβολική | Μειώστε το δείγμα σε 1‑2 fps για τις περισσότερες ροές υποτίτλων· μπορείτε ακόμα να καταγράψετε κάθε αλλαγή υποτίτλου. |
| **FFmpeg δεν βρέθηκε** | `ffmpeg.exe` δεν βρίσκεται στο `PATH` | Παρέχετε το πλήρες μονοπάτι στο `ProcessStartInfo.FileName` ή εγκαταστήστε το FFmpeg παγκοσμίως. |

## Επέκταση της Λύσης

- **Export to SRT** – συνδέστε τα χρονικά σημεία με το κείμενο OCR και γράψτε ένα αρχείο SubRip.  
- **Multi‑language support** – ορίστε `ocrProcessor.Language = OcrLanguage.Spanish` (ή οποιαδήποτε υποστηριζόμενη γλώσσα).  
- **Real‑time processing** – διοχετεύστε τα καρέ απευθείας από ζωντανή ροή αντί για ανάγνωση από δίσκο.  

Όλες αυτές οι παραλλαγές περιστρέφονται γύρω από τις βασικές ιδέες του **extract frames from video**, **read text from video**, και **extract text from mp4**.

## Συμπέρασμα

Μόλις περάσαμε από μια πλήρη ροή εργασίας **video subtitle ocr** σε C#. Με την εξαγωγή καρέ από το βίντεο, εστιάζοντας το OCR στη ζώνη των υποτίτλων και επαναλαμβάνοντας τα αποτελέσματα, μπορείτε αξιόπιστα να **read text from video** αρχεία όπως MP4. Ο κώδικας είναι έτοιμος για αντιγραφή‑επικόλληση, και ο μοντέλο σχεδίασης σας επιτρέπει να αντικαταστήσετε οποιονδήποτε αποκωδικοποιητή καρέ προτιμάτε.

Επόμενα βήματα; Δοκιμάστε να εξάγετε τα αποτελέσματα σε αρχείο SRT, πειραματιστείτε με διαφορετικά μεγέθη ROI, ή στείλτε τους υπότιτλους σε API μετάφρασης για πολυγλωσσικούς υπότιτλους. Ο ουρανός είναι το όριο μόλις κατακτήσετε τα βασικά της εξαγωγής κειμένου από βίντεο.

Καλό κώδικα, και οι υπότιτλοί σας να είναι πάντα κρυστάλλινοι!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}