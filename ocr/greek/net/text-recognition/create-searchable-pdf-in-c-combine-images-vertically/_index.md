---
category: general
date: 2026-02-28
description: Δημιουργήστε αναζητήσιμο PDF σε C# συνδυάζοντας εικόνες κάθετα. Μάθετε
  πώς να στοιβάζετε εικόνες κάθετα και να μετατρέπετε σαρωμένες σελίδες PDF με το
  Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF σε C# συνδυάζοντας εικόνες κάθετα. Αυτός
  ο οδηγός δείχνει πώς να στοιβάζετε εικόνες κάθετα και να μετατρέπετε σαρωμένες σελίδες
  PDF χρησιμοποιώντας το Aspose OCR.
og_title: Δημιουργία Αναζητήσιμου PDF σε C# – Συνδυασμός Εικόνων Κατακόρυφα
tags:
- Aspose OCR
- C#
- PDF generation
title: Δημιουργία Αναζητήσιμου PDF σε C# – Κατακόρυφος Συνδυασμός Εικόνων
url: /el/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF σε C# – Συνδυασμός Εικόνων Κατακόρυφα

Σας χρειάστηκε ποτέ να **create searchable PDF** από μερικές σαρωμένες PNG αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης εγγράφων το μεγαλύτερο πρόβλημα είναι η μετατροπή μιας στοίβας αρχείων εικόνας σε ένα τακτοποιημένο, αναζητήσιμο PDF που μπορείτε να ευρετηριάσετε και να μοιραστείτε.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **stack images vertically**, **combine images vertically**, και τέλος **convert scanned pages PDF** σε ένα ενιαίο αναζητήσιμο έγγραφο χρησιμοποιώντας τη μηχανή GPU‑accelerated του Aspose.OCR. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιαδήποτε λύση .NET.

> **Τι θα μάθετε**
> - Αρχικοποίηση μιας μηχανής OCR με υποστήριξη GPU.
> - Επεξεργασία παρτίδας εικόνων παράλληλα.
> - **Combine images vertically** για να μιμηθείτε μια σάρωση πολλαπλών σελίδων.
> - Εξαγωγή αναζητήσιμου PDF και λεπτομερούς αναφοράς JSON για downstream ανάλυση.

## Προαπαιτούμενα

- .NET 6+ (ο κώδικας μεταγλωττίζεται με .NET 6, .NET 7 ή .NET 8)
- Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Μηχανή με GPU αν θέλετε να διατηρήσετε τη ρύθμιση `ProcessingMode.Gpu` (λειτουργεί και fallback σε CPU)
- Ένας φάκελος με μερικά σαρωμένα αρχεία PNG/JPEG (το demo χρησιμοποιεί `page1.png`, `page2.png`, `page3.png`)

Καμία εξωτερική υπηρεσία, κανένα κρυφό αρχείο ρυθμίσεων — μόνο καθαρό C#.

## Βήμα 1 – Ρύθμιση του OCR Engine για **Create Searchable PDF**

Πρώτα δημιουργούμε ένα `OcrEngine`, ενεργοποιούμε την επιτάχυνση GPU, επιλέγουμε τα Αγγλικά ως γλώσσα και προσθέτουμε μερικά φίλτρα προεπεξεργασίας. Αυτά τα φίλτρα βελτιώνουν την ακρίβεια ευθυγραμμίζοντας κεκλιμένες σελίδες (`DeskewFilter`) και αφαιρώντας θόρυβο (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Γιατί είναι σημαντικό:** Η μηχανή OCR κάνει το σκληρό κομμάτι της αναγνώρισης κειμένου. Η ενεργοποίηση του `ProcessingMode.Gpu` μπορεί να μειώσει τον χρόνο αναγνώρισης στο μισό σε μια σύγχρονη κάρτα γραφικών, ενώ τα φίλτρα μειώνουν κοινά σφάλματα σάρωσης που διαφορετικά θα παρήγαγαν ακατάλληλο αποτέλεσμα.

## Βήμα 2 – Διαμόρφωση Batch Processor για **Convert Scanned Pages PDF** Αποτελεσματικά

Η επεξεργασία κάθε σελίδας μία‑με‑μία είναι αποδεκτή για λίγες εικόνες, αλλά στα πραγματικά έργα συχνά υπάρχουν δεκάδες ή εκατοντάδες σελίδες. Το `OcrBatchProcessor` του Aspose.OCR μας επιτρέπει να τρέχουμε αναγνώριση παράλληλα, επιταχύνοντας δραματικά το βήμα **convert scanned pages pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro tip:** Αν έχετε μόνο CPU, ορίστε `ProcessingMode = ProcessingMode.Cpu`. Ο batch processor θα σεβαστεί ακόμα το `MaxDegreeOfParallelism`, ώστε να μπορείτε να το ρυθμίσετε ώστε να μην υπερφορτώνει τη μηχανή.

## Βήμα 3 – Εκτέλεση OCR στην Παρτίδα και Συλλογή Αποτελεσμάτων

Τώρα πραγματοποιούμε την πραγματική αναγνώριση κειμένου. Η μέθοδος `Recognize` επιστρέφει μια λίστα από αντικείμενα `OcrResult`, το καθένα περιέχει τόσο την αρχική εικόνα όσο και το εξαγόμενο κείμενο.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Σε αυτό το σημείο έχετε όλα όσα χρειάζεστε για **create searchable PDF**: τις εικόνες (ακόμη στη μνήμη) και τα αντίστοιχα επίπεδα κειμένου.

## Βήμα 4 – **Combine Images Vertically** και Δημιουργία του Αναζητήσιμου PDF

Τα περισσότερα σαρωμένα έγγραφα είναι PDF πολλαπλών σελίδων, οπότε πρέπει να ενώσουμε τις μεμονωμένες εικόνες σε μια μακριά εικόνα που αντικατοπτρίζει μια φυσική στοίβα. Το Aspose.OCR παρέχει τη μέθοδο `Image.CombineVertical` ακριβώς γι’ αυτό το σκοπό.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Το παραγόμενο αρχείο (`combined_searchable.pdf`) περιέχει επιλέξιμο, αναζητήσιμο κείμενο κάτω από κάθε εικόνα σελίδας — ακριβώς ό,τι χρειάζεστε για **create searchable PDF** από σαρωμένες πηγές.

![Create searchable PDF example](/images/create-searchable-pdf.png "create searchable pdf example")

*Κείμενο alt εικόνας: παράδειγμα δημιουργίας αναζητήσιμου PDF που δείχνει ένα συνδυασμένο PDF με αναζητήσιμο κείμενο.*

**Γιατί η κατακόρυφη στοίβαξη;** Πολλές βιβλιοθήκες OCR αντιμετωπίζουν κάθε εικόνα ως ξεχωριστή σελίδα. Στοίβαζοντάς τες, διατηρούμε τη σωστή σειρά σελίδων του PDF ενώ εκμεταλλευόμαστε ένα μόνο πέρασμα OCR για ολόκληρο το έγγραφο.

## Βήμα 5 – Εξαγωγή Λεπτομερούς JSON για την Πρώτη Σελίδα (Ιδανικό για Downstream Workflows)

Μερικές φορές χρειάζεστε κάτι παραπάνω από ένα PDF· ίσως θέλετε να τροφοδοτήσετε τα δεδομένα OCR σε μια βάση δεδομένων ή σε μια αλυσίδα μηχανικής μάθησης. Το Aspose.OCR σας επιτρέπει να σειριοποιήσετε κάθε `OcrResult` σε JSON, διατηρώντας τα πλαίσια οριοθέτησης, τα σκορ εμπιστοσύνης και άλλα.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Αναμενόμενο απόσπασμα JSON (περιορισμένο):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Τώρα μπορείτε να τροφοδοτήσετε αυτό το JSON σε οποιοδήποτε downstream σύστημα — είτε ευρετηριάζετε το κείμενο στο Elasticsearch είτε το στέλνετε σε έναν προσαρμοσμένο πίνακα αναλύσεων.

---

## Πώς να **Stack Images Vertically** – Σύντομη Επανάληψη

Αν αναρωτιέστε **how to stack images vertically** χωρίς το Aspose, μπορείτε να χρησιμοποιήσετε το `System.Drawing` για να δημιουργήσετε ένα νέο bitmap και να σχεδιάσετε κάθε σελίδα η μία μετά την άλλη. Ωστόσο, η ενσωματωμένη μέθοδος `Image.CombineVertical` του Aspose διαχειρίζεται DPI, μορφή pixel και διαχείριση μνήμης για εσάς, καθιστώντας την την πιο αξιόπιστη επιλογή για παραγωγικό κώδικα.

### Εναλλακτική: Χρήση `System.Drawing` (μόνο για περιέργεια)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Η χειροκίνητη προσέγγιση λειτουργεί, αλλά χάνετε την ευκολία του αυτόματου χειρισμού DPI και τη δυνατότητα να τροφοδοτήσετε άμεσα το αποτέλεσμα στην `RecognizeToPdf`. Παραμείνετε στη `CombineVertical` εκτός αν έχετε πολύ εξειδικευμένη απαίτηση.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Out‑of‑memory errors** όταν επεξεργάζεστε δεκάδες υψηλής ανάλυσης σαρώσεις | Κάθε εικόνα παραμένει στη μνήμη μέχρι να γραφτεί το PDF | Αποδεσμεύστε τα αντικείμενα `Image` αμέσως μόλις τελειώσετε (`using` blocks) ή μειώστε την ανάλυση πριν το συνδυασμό |
| **Garbage text** μετά το OCR | Κεκλιμένες σαρώσεις ή χαμηλή αντίθεση | Διατηρήστε το `DeskewFilter` και το `DenoiseFilter`; σκεφτείτε να προσθέσετε `ContrastFilter` αν χρειάζεται |
| **Missing searchable layer** | Χρησιμοποιήθηκε `Recognize` αντί για `RecognizeToPdf` | Βεβαιωθείτε ότι καλείτε `ocrEngine.RecognizeToPdf` στην ενωμένη εικόνα |
| **GPU fallback fails** σε μηχανές χωρίς κατάλληλους οδηγούς | `ProcessingMode.Gpu` ρίχνει εξαίρεση | Τυλίξτε τη δημιουργία της μηχανής σε try/catch και επιστρέψτε σε `ProcessingMode.Cpu` |

## Επόμενα Βήματα – Επέκταση της Ροής Εργασίας

Τώρα που ξέρετε πώς να **create searchable PDF**, μπορείτε να:

- **Batch‑process ολόκληρους φακέλους** χρησιμοποιώντας `Directory.GetFiles` και βρόχο `foreach`.
- **Προσθέσετε υδατογραφήματα** σε κάθε σελίδα πριν το συνδυασμό (χρησιμοποιήστε `ImageProcessor` από Aspose.Imaging).
- **Διαχωρίσετε το αναζητήσιμο PDF πίσω σε μεμονωμένες σελίδες** αν χρειάζεστε PDF ανά σελίδα αργότερα (`PdfDocument.Split` από Aspose.PDF).
- **Ενσωματώσετε με Azure Blob Storage** για λήψη εικόνων από το cloud και αποθήκευση του τελικού PDF πίσω στο cloud.

Όλες αυτές οι επεκτάσεις βασίζονται στα ίδια βασικά concepts: ρύθμιση OCR, διαχείριση εικόνων και εξαγωγή PDF.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **create searchable PDF** από μια συλλογή σαρωμένων εικόνων σε C#. Αρχικοποιώντας ένα `OcrEngine` με GPU, τρέχοντας batch παράλληλα με `OcrBatchProcessor`, **combining images vertically**, και τελικά καλώντας `RecognizeToPdf`, παίρνετε ένα τακτοποιημένο, αναζητήσιμο έγγραφο έτοιμο για αρχειοθέτηση ή ευρετηρίαση. Η επιπλέον εξαγωγή JSON σας δίνει πλήρη διαφάνεια στα αποτελέσματα OCR, ανοίγοντας δρόμους για analytics ή προσαρμοσμένες ροές εργασίας.

Δοκιμάστε το, πειραματιστείτε με διαφορετικά φίλτρα, και δείτε τη γραμμή αυτοματοποίησης εγγράφων σας να γίνεται πιο ομαλή. Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο — καλή προγραμματιστική!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}