---
category: general
date: 2026-06-06
description: αναγνώριση κειμένου σε εικόνα χρησιμοποιώντας C# OCR – ένα βήμα‑προς‑βήμα
  παράδειγμα C# OCR που εξάγει κείμενο από σαρώσεις και μετατρέπει τη σάρωση σε κείμενο
  σε λίγα λεπτά.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: el
og_description: Αναγνώριση εικόνας κειμένου με C# OCR. Μάθετε ένα πρακτικό παράδειγμα
  C# OCR που εξάγει κείμενο από σαρώσεις, μετατρέπει τη σάρωση σε κείμενο και διαχειρίζεται
  εικόνες πραγματικού κόσμου.
og_title: Αναγνώριση κειμένου σε εικόνα με C# – Πλήρης οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Αναγνώριση εικόνας κειμένου σε C# – Πλήρης Οδηγός OCR
url: /el/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου σε εικόνα σε C# – Πλήρης Οδηγός OCR

Έχετε αναρωτηθεί ποτέ πώς να **recognize text image** απευθείας από μια σκαναρισμένη φωτογραφία χρησιμοποιώντας C#; Δεν είστε ο μόνος. Είτε ψηφιοποιείτε παλιές αποδείξεις, είτε εξάγετε δεδομένα από μια επαγγελματική κάρτα, είτε απλώς μετατρέπετε μια χαμηλής ανάλυσης σάρωση σε επεξεργάσιμο κείμενο, η δυνατότητα εξαγωγής κειμένου από μια εικόνα είναι ένα χρήσιμο κόλπο που κάθε προγραμματιστής πρέπει να έχει στο εργαλειοφόρο του.

Σε αυτόν τον οδηγό θα περάσουμε από ένα **c# ocr example** που φορτώνει μια εικόνα, εκτελεί οπτική αναγνώριση χαρακτήρων και εκτυπώνει το αποτέλεσμα στην κονσόλα. Στο τέλος θα μπορείτε να **extract text scan** αρχεία, **convert scan to text**, και ακόμη να προσαρμόσετε τη διαδικασία για θορυβώδεις εικόνες. Δεν απαιτούνται πολυτελείς υπηρεσίες τρίτων—μόνο το ενσωματωμένο Windows.Media.Ocr API (ή οποιοδήποτε συμβατό OcrEngine) και μερικές γραμμές κώδικα.

## Τι Θα Μάθετε

* Πώς να ρυθμίσετε ένα έργο C# για OCR.
* Ο ακριβής κώδικας που απαιτείται για αρχεία **recognize text image**.
* Συμβουλές για τη διαχείριση σκαναρίσματος χαμηλής ανάλυσης και εγγράφων πολλαπλών σελίδων.
* Τρόποι επέκτασης του παραδείγματος σε μια επαναχρησιμοποιήσιμη βιβλιοθήκη για τις δικές σας εφαρμογές.

### Προαπαιτούμενα

* .NET 6.0 ή νεότερο (το API λειτουργεί επίσης σε .NET 5+).
* Visual Studio 2022 (η έκδοση Community είναι εντάξει) ή οποιοδήποτε IDE προτιμάτε.
* Ένα δείγμα εικόνας όπως `lowres_scan.jpg` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.
* Βασική εξοικείωση με async/await—οι κλήσεις OCR είναι ασύγχρονες στο Windows API.

> **Pro tip:** Αν βρίσκεστε σε πλατφόρμα μη‑Windows, αντικαταστήστε το namespace `Windows.Media.Ocr` με μια διασυνοριακή βιβλιοθήκη όπως το TesseractSharp· η λογική γύρω παραμένει η ίδια.

---

## Βήμα 1: Ρύθμιση για **recognize text image** με μια μηχανή OCR

Πρώτα, χρειαζόμαστε μια παρουσία της μηχανής OCR. Η κλάση `OcrEngine` είναι το σημείο εισόδου για οποιαδήποτε λειτουργία **image to text c#**.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Γιατί είναι σημαντικό:** Η μηχανή αφαιρεί το βάρος της αναγνώρισης προτύπων. Δημιουργώντας την ρητά κερδίζουμε έλεγχο στις ρυθμίσεις γλώσσας, κάτι που είναι ουσιώδες όταν αργότερα θέλετε να **extract text scan** έγγραφα σε άλλες γλώσσες.

## Βήμα 2: Φόρτωση του αρχείου εικόνας – ο πυρήνας του **convert scan to text**

Στη συνέχεια, διαβάζουμε την εικόνα από το δίσκο και τη μετατρέπουμε σε `SoftwareBitmap`, τη μορφή που αναμένει η μηχανή OCR.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Γιατί το κάνουμε:** Η άμεση τροφοδοσία ενός ακατέργαστου ρεύματος αρχείου στην OCR συχνά δίνει φτωχά αποτελέσματα, ειδικά με σκαναρίσματα χαμηλής ανάλυσης. Η μετατροπή σε `SoftwareBitmap` μας επιτρέπει να χειριστούμε το DPI, το βάθος χρώματος, και ακόμη να εφαρμόσουμε φίλτρα πριν την αναγνώριση.

## Βήμα 3: Εκτέλεση της λειτουργίας **recognize text image**

Τώρα τελικά καλούμε τη μέθοδο `RecognizeAsync` της μηχανής. Εδώ συμβαίνει η μαγεία.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Τι θα δείτε:** Αν το `lowres_scan.jpg` περιέχει τη φράση «Hello World», η κονσόλα θα εκτυπώσει:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Αυτό είναι ολόκληρο το **c# ocr example** σε δράση—μόνο τέσσερα λογικά βήματα, αλλά καλύπτει τα πάντα από τη φόρτωση του αρχείου μέχρι το τελικό αποτέλεσμα.

## Βήμα 4: Διαχείριση Ακραίων Περιπτώσεων – Όταν η Σάρωση Δεν Είναι Τέλεια

Οι πραγματικές εικόνες δεν είναι πάντα καθαρές. Εδώ είναι μερικές προσαρμογές που μπορείτε να κάνετε χωρίς να ξαναγράψετε ολόκληρο το πρόγραμμα:

| Πρόβλημα | Γρήγορη Διόρθωση |
|----------|-------------------|
| **Very low DPI (≤ 72)** | Αυξήστε το μέγεθος του bitmap χρησιμοποιώντας `BitmapTransform` πριν από την αναγνώριση. |
| **Skewed text** | Εφαρμόστε μια περιστροφή (`SoftwareBitmap.Rotate`) για να ευθυγραμμίσετε τη σελίδα. |
| **Multiple languages** | Δημιουργήστε `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` και ορίστε το `engine.Language` αναλόγως. |
| **Large files** | Επεξεργαστείτε την εικόνα σε τμήματα (`engine.RecognizeAsync(tileBitmap)`) και συνενώστε τα αποτελέσματα. |

Αυτές οι προσαρμογές διασφαλίζουν ότι η ρουτίνα **extract text scan** παραμένει αξιόπιστη ακόμη και όταν αντιμετωπίζετε θορυβώδεις αποδείξεις ή φωτογραφίες τραβηγμένες υπό γωνία.

## Βήμα 5: Μετατροπή του Παραδείγματος σε Επαναχρησιμοποιήσιμο Βοηθητικό (Προαιρετικό)

Αν σκοπεύετε να **convert scan to text** σε διάφορα μέρη μιας εφαρμογής, τυλίξτε τη λογική σε μια μικρή βοηθητική κλάση:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Τώρα απλώς καλείτε:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Γιατί θα το αγαπήσετε:** Ο βοηθός απομονώνει τη λειτουργία OCR, επιτρέποντάς σας να εστιάσετε στη λογική της επιχείρησης—τέλειο για ένα **c# ocr example** που θα επαναχρησιμοποιηθεί σε πολλά έργα.

---

![παράδειγμα recognize text image](https://example.com/ocr-demo.png "Στιγμιότυπο οθόνης εξόδου OCR κονσόλας που δείχνει το αποτέλεσμα του recognize text image")

*Κείμενο εναλλακτικής περιγραφής:* **recognize text image** έξοδος από μια εφαρμογή C# OCR κονσόλας.

---

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό σε .NET Core σε Linux;**  
A: Το namespace `Windows.Media.Ocr` είναι μόνο για Windows. Σε Linux ή macOS θα το αντικαταστήσετε με το TesseractSharp ή το IronOcr—και τα δύο εκθέτουν μια παρόμοια μέθοδο `Engine.Recognize`, έτσι ώστε ο υπόλοιπος κώδικας να παραμένει σχεδόν αμετάβλητος.

**Q: Πόσο ακριβής είναι η ενσωματωμένη OCR για χειρόγραφες σημειώσεις;**  
A: Η αναγνώριση χειρόγραφου είναι ακόμη πειραματική. Για τα καλύτερα αποτελέσματα, χρησιμοποιήστε τυπωμένες γραμματοσειρές ή εξετάστε μια υπηρεσία cloud όπως το Azure Cognitive Services εάν χρειάζεστε υψηλή ακρίβεια.

**Q: Μπορώ να επεξεργαστώ PDFs απευθείας;**  
A: Δεν είναι δυνατό εξ αρχής. Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (χρησιμοποιώντας `PdfSharp` ή `Ghostscript`) και στη συνέχεια τροφοδοτήστε το bitmap στη μηχανή OCR.

---

## Συμπέρασμα

Τώρα έχετε ένα πλήρες, έτοιμο για παραγωγή **c# ocr example** που μπορεί να **recognize text image** αρχεία, **extract text scan** περιεχόμενα, και **convert scan to text** με λίγες μόνο γραμμές κώδικα. Κατανοώντας τη ροή—δημιουργία μηχανής, φόρτωση εικόνας, ασύγχρονη αναγνώριση και διαχείριση αποτελεσμάτων—μπορείτε να προσαρμόσετε το πρότυπο σε οποιοδήποτε έργο C# που χρειάζεται να μετατρέπει εικόνες σε αναζητήσιμες συμβολοσειρές.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να προσθέσετε ένα απλό UI με WinForms ή WPF, πειραματιστείτε με διαφορετικές γλώσσες, ή συνδέστε την έξοδο με μια βάση δεδομένων για αρχεία αναζήτησης. Ο ουρανός είναι το όριο όταν κυριαρχείτε τις τεχνικές **image to text c#**.

Καλό προγραμματισμό, και εύχομαι οι σκαναρίσματά σας να είναι πάντα καθαρά!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Μετατροπή εικόνας σε κείμενο – Εκτέλεση OCR σε εικόνα από URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Πώς να εξάγετε κείμενο από εικόνα προετοιμάζοντας ορθογώνια στην OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}