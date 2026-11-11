---
category: general
date: 2026-09-10
description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κυριλλικού κειμένου,
  την προεπεξεργασία εικόνων και τη μετατροπή τους σε αρχεία PDF ή HTML σε ένα ενιαίο,
  εκτελέσιμο παράδειγμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: el
lastmod: 2026-09-10
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κυριλλικού κειμένου,
  την προεπεξεργασία εικόνων και την εξαγωγή των αποτελεσμάτων ως PDF ή HTML. Ακολουθήστε
  αυτόν τον βήμα‑βήμα οδηγό.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – εξαγωγή κυριλλικού κειμένου και μετατροπή
  εικόνων
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή κυριλλικού κειμένου
url: /el/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε C# για εξαγωγή κυριλλικού κειμένου

Αν χρειάζεστε **πώς να χρησιμοποιήσετε OCR** σε C# για την εξαγωγή κυριλλικού κειμένου από σαρωμένα έγγραφα, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα μάθετε επίσης πώς να **προεπεξεργαστείτε εικόνα για OCR**, και πώς να **μετατρέψετε εικόνα σε PDF** ή **μετατρέψετε εικόνα σε HTML** μόλις το κείμενο αναγνωριστεί.

Τα έργα ψηφιοποίησης εγγράφων συχνά αντιμετωπίζουν δύο προβλήματα: σαρώσεις χαμηλής ποιότητας και την ανάγκη αποθήκευσης των αποτελεσμάτων σε πολλαπλές μορφές. Αυτό το tutorial λύνει και τα δύο χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR, η οποία κατεβάζει αυτόματα τα ελλιπή πακέτα γλωσσών, προσφέρει ενσωματωμένα βοηθήματα επεξεργασίας εικόνας και μπορεί να εξάγει το αποτέλεσμα OCR σε PDF ή HTML με μία κλήση.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή που υποστηρίζει έργα C#.
* Το πακέτο NuGet **Aspose.OCR**. Εγκαταστήστε το με:

```bash
dotnet add package Aspose.OCR
```

* Ένα αρχείο εικόνας που περιέχει κυριλλικούς χαρακτήρες (π.χ., `sample_cyrillic.jpg`).  
  Τοποθετήστε το αρχείο σε φάκελο που μπορείτε να αναφέρετε ως `YOUR_DIRECTORY`.

Η βιβλιοθήκη θα κατεβάσει το πακέτο γλώσσας Cyrillic την πρώτη φορά που ορίζετε `ocrEngine.Language = Language.Cyrillic;`, έτσι δεν απαιτείται χειροκίνητη λήψη.

## Βήμα 1 – Αρχικοποίηση της μηχανής OCR (πώς να χρησιμοποιήσετε OCR)

Η δημιουργία μιας παρουσίας `OcrEngine` προετοιμάζει τη μηχανή για όλες τις επόμενες λειτουργίες.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Γιατί είναι σημαντικό:** Η μηχανή κρατά τις ρυθμίσεις όπως η γλώσσα, οι ρυθμίσεις επεξεργασίας εικόνας και οι επιλογές εξόδου. Η αρχικοποίηση της μία φορά διατηρεί τον υπόλοιπο κώδικα καθαρό και ασφαλή ως προς τα νήματα.

## Βήμα 2 – Επιλογή της κυριλλικής γλώσσας (εξαγωγή κυριλλικού κειμένου)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Γιατί είναι σημαντικό:** Η ακρίβεια του OCR εξαρτάται σε μεγάλο βαθμό από το σωστό μοντέλο γλώσσας. Επιλέγοντας ρητά `Language.Cyrillic`, η μηχανή εφαρμόζει πίνακες συχνότητας χαρακτήρων κατάλληλους για Ρωσικά, Ουκρανικά, Βουλγαρικά κ.λπ.

## Βήμα 3 – Προεπεξεργασία της εικόνας για OCR

Οι σαρώσεις χαμηλής ποιότητας περιέχουν κλίση, στίγματα ή άνισο φωτισμό. Ο ενσωματωμένος `ImageProcessor` μπορεί να βελτιώσει τα ποσοστά αναγνώρισης με μόνο δύο κλήσεις.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Γιατί είναι σημαντικό:** Η προεπεξεργασία μειώνει τους ψευδείς χαρακτήρες και αυξάνει το σκορ εμπιστοσύνης. Το κεκλιμένο κείμενο συχνά παράγει ακατάστατο αποτέλεσμα· η ευθυγράμμιση το διορθώνει. Η αφαίρεση στίγματος εξαλείφει μικρά τεχνουργήματα που η μηχανή OCR θα μπορούσε να ερμηνεύσει ως γράμματα.

> **Συμβουλή:** Αν οι πηγαίες εικόνες σας είναι ήδη καθαρές, μπορείτε να παραλείψετε αυτές τις κλήσεις. Για πολύ κατεστραμμένες σαρώσεις, σκεφτείτε επιπλέον βήματα όπως `Binarize()` ή `ContrastStretch()`.

## Βήμα 4 – Εκτέλεση OCR στην είσοδο εικόνας

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Γιατί είναι σημαντικό:** Η `Process` εκτελεί τη διαδικασία αναγνώρισης στο παρεχόμενο bitmap. Επιστρέφει `void`; το αναγνωρισμένο κείμενο γίνεται διαθέσιμο μέσω της ιδιότητας `Text`.

## Βήμα 5 – Ανάκτηση του αναγνωρισμένου κειμένου και αποθήκευση σε αρχείο

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Γιατί είναι σημαντικό:** Η αποθήκευση του ακατέργαστου κειμένου επιτρέπει επεξεργασία σε επόμενα στάδια όπως αναζήτηση, ευρετηρίαση ή τροφοδοσία σε υπηρεσίες μετάφρασης.

## Βήμα 6 – Εξαγωγή του αποτελέσματος OCR σε άλλες μορφές (μετατροπή εικόνας σε PDF & μετατροπή εικόνας σε HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Γιατί είναι σημαντικό:** Η μετατροπή του αποτελέσματος OCR σε PDF ή HTML σας επιτρέπει να διατηρήσετε το οπτικό περιεχόμενο της αρχικής εικόνας ενώ παρέχετε δυνατότητα αναζήτησης κειμένου. Αυτό είναι ιδιαίτερα χρήσιμο για νομικές ή αρχειακές διαδικασίες.

### Αναμενόμενη έξοδος

Η εκτέλεση του προγράμματος με μια καθαρή κυριλλική σάρωση παράγει τρία αρχεία:

* `result.txt` – απλό κείμενο Unicode, π.χ., `Пример текста на кириллице`.
* `result.pdf` – PDF που περιέχει την εικόνα με ένα αόρατο στρώμα κειμένου για αναζήτηση.
* `result.html` – σελίδα HTML που εμφανίζει την εικόνα και το κείμενο που μπορεί να επιλεγεί.

Ανοίξτε οποιοδήποτε από τα αρχεία για να επαληθεύσετε ότι οι κυριλλικοί χαρακτήρες έχουν εξαχθεί σωστά.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το πακέτο γλώσσας δεν κατέβει;** | Βεβαιωθείτε ότι ο υπολογιστής έχει πρόσβαση στο διαδίκτυο. Μπορείτε επίσης να προ‑κατεβάσετε το πακέτο από τον ιστότοπο της Aspose και να το τοποθετήσετε στο φάκελο `bin`. |
| **Μπορώ να αναγνωρίσω άλλα αλφάβητα στην ίδια εκτέλεση;** | Ναι. Καλέστε `ocrEngine.Language = Language.English;` (ή οποιοδήποτε υποστηριζόμενο enum) πριν από τη `Process`. Ενδέχεται να χρειαστεί να εκτελέσετε τη `Process` ξεχωριστά για κάθε γλώσσα εάν η εικόνα περιέχει ανάμεικτα σενάρια. |
| **Η εικόνα μου είναι multi‑page TIFF – λειτουργεί αυτό;** | Η `OcrEngine` επεξεργάζεται ένα bitmap τη φορά. Φορτώστε κάθε σελίδα σε ένα `Bitmap` και καλέστε τη `Process` σε βρόχο, συνενώνοντας τα αποτελέσματα. |
| **Πώς μπορώ να αυξήσω την απόδοση για μεγάλες παρτίδες;** | Ξαναχρησιμοποιήστε μία μόνο παρουσία `OcrEngine` και ορίστε `ocrEngine.OptimizeMemory = true;`. Επίσης, σκεφτείτε παράλληλη επεξεργασία με ξεχωριστές παρουσίες μηχανής ανά νήμα. |

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε OCR** σε C# για **εξαγωγή κυριλλικού κειμένου**, **προεπεξεργασία εικόνας για OCR**, και **μετατροπή εικόνας σε PDF** ή **μετατροπή εικόνας σε HTML** σε λίγα σύντομα βήματα. Το πλήρες παράδειγμα δείχνει μια παραγωγική‑

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε AspOCR: Φίλτρα προεπεξεργασίας εικόνας OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Πώς να εξάγετε κείμενο OCR σε C# – Πλήρης οδηγός βήμα‑βήμα](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Πώς να χρησιμοποιήσετε Aspose OCR για αποτέλεσμα JSON στην αναγνώριση εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}