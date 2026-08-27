---
category: general
date: 2025-12-29
description: Μάθετε πώς να κάνετε OCR σε αρχεία PDF με C# και να εξάγετε κείμενο από
  σελίδες PDF. Αυτό το σεμινάριο καλύπτει επίσης τη μετατροπή PDF σε κείμενο και τις
  τεχνικές ανάγνωσης σελίδων PDF με C#.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: el
og_description: Πώς να κάνετε OCR σε PDF με C# εξηγημένο σε έναν σύντομο οδηγό. Λάβετε
  τον πλήρη κώδικα για εξαγωγή κειμένου από PDF, μετατροπή PDF σε κείμενο και ανάγνωση
  σελίδας PDF με C#.
og_title: Πώς να κάνετε OCR PDF σε C# – Πλήρης Οδηγός Προγραμματισμού
tags:
- OCR
- C#
- PDF processing
title: Πώς να κάνετε OCR PDF σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να OCR PDF σε C# – Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να OCR PDF** αρχεία απευθείας από την εφαρμογή σας C#; Ίσως έχετε μια στοίβα σαρωμένων τιμολογίων και χρειάζεται να εξάγετε το κείμενο χωρίς χειροκίνητη αντιγραφή‑επικόλληση. Αυτό είναι ένα κοινό πρόβλημα, ειδικά όταν τα PDF είναι βασισμένα σε εικόνες και η παραδοσιακή εξαγωγή κειμένου αποτυγχάνει.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που όχι μόνο δείχνει **πώς να OCR PDF**, αλλά επίσης επιδεικνύει πώς να *εξάγετε κείμενο από PDF*, *μετατρέψετε PDF σε κείμενο* και *διαβάσετε σελίδα PDF C#* χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR. Χωρίς ασαφείς αναφορές—μόνο ο κώδικας που μπορείτε να ενσωματώσετε στο Visual Studio και να αρχίσετε να πειραματίζεστε.

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)  
- **Aspose.OCR** πακέτο NuGet – εγκαταστήστε με `dotnet add package Aspose.OCR`  
- Ένα σαρωμένο PDF (π.χ., `invoice.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε  
- Βασική εξοικείωση με εφαρμογές κονσόλας C#  

Αυτό είναι όλο. Αν έχετε ήδη ένα έργο, απλώς προσθέστε το πακέτο και είστε έτοιμοι.

## Βήμα 1: Ρυθμίστε το Έργο και Προσθέστε το Aspose.OCR

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας (ή χρησιμοποιήστε ένα υπάρχον) και προσθέστε τη βιβλιοθήκη OCR.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

Γιατί αυτό το βήμα είναι σημαντικό: το Aspose.OCR διαχειρίζεται τη βαριά δουλειά της ανάλυσης εικόνας, της ανίχνευσης διάταξης και της αναγνώρισης χαρακτήρων. Χωρίς αυτό, θα έπρεπε να συνδυάσετε έναν rasterizer, μια μηχανή Tesseract και πολύ κώδικα ενδιάμεσου.

## Βήμα 2: Εισάγετε τα Namespaces και Προετοιμάστε τη Μηχανή OCR

Τώρα ανοίξτε το `Program.cs` (ή οποιοδήποτε .cs αρχείο προτιμάτε) και προσθέστε τις απαιτούμενες οδηγίες `using`.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

Η δημιουργία της μηχανής είναι απλή, αλλά θα ρυθμίσουμε επίσης μερικές επιλογές που βελτιώνουν την ακρίβεια σε τυπικές σαρώσεις τιμολογίων.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**Συμβουλή:** Αν γνωρίζετε τη γλώσσα εκ των προτέρων, ορίστε το `Language` ρητά· αυτό επιταχύνει τη διαδικασία.

## Βήμα 3: Καθορίστε το Αρχείο PDF Σας

Καθορίστε το απόλυτο ή σχετικό μονοπάτι προς το PDF που θέλετε να επεξεργαστείτε. Για το σκοπό αυτού του παραδείγματος, θα υποθέσουμε ότι το αρχείο βρίσκεται σε φάκελο με όνομα `Samples`.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

Ο έλεγχος της ύπαρξης του αρχείου είναι ένα μικρό βήμα, αλλά σας προστατεύει από ασαφείς εξαιρέσεις αργότερα.

## Βήμα 4: Επιλέξτε τη(ς) Σελίδα(ες) για Ανάγνωση

Ένα PDF μπορεί να έχει δεκάδες σελίδες, αλλά συχνά χρειάζεστε μόνο μια συγκεκριμένη—π.χ., τη δεύτερη σελίδα ενός τιμολογίου όπου εμφανίζεται το συνολικό ποσό. Η μέθοδος `RecognizePdf` σας επιτρέπει να στοχεύσετε σε μία σελίδα ή σε ολόκληρο το έγγραφο.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

Αν θέλετε να *μετατρέψετε PDF σε κείμενο* για ολόκληρο το έγγραφο, απλώς παραλείψτε το όρισμα `pageNumber`:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## Βήμα 5: Εμφανίστε ή Αποθηκεύστε το Εξαγόμενο Κείμενο

Τώρα που η μηχανή OCR έχει ολοκληρώσει τη δουλειά της, μπορείτε είτε να εκτυπώσετε το κείμενο στην κονσόλα, να το γράψετε σε αρχείο `.txt`, είτε να το περάσετε σε άλλο σύστημα (π.χ., μια βάση δεδομένων).

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**Γιατί είναι σημαντικό:** Με την αποθήκευση του αποτελέσματος δημιουργείτε ένα επαναχρησιμοποιήσιμο αντικείμενο—ιδανικό για ανάλυση downstream ή ευρετηρίαση αναζήτησης.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs` και να το τρέξετε αμέσως.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

Αν το PDF περιέχει καθαρές, υψηλής ανάλυσης σαρώσεις, το αποτέλεσμα θα είναι σχεδόν τέλειο. Εικόνες χαμηλότερης ποιότητας μπορεί να χρειάζονται πρόσθετη προεπεξεργασία (π.χ., αύξηση DPI ή εφαρμογή φίλτρων); οι `ImagePreprocessingOptions` του Aspose.OCR μπορούν να ρυθμιστούν για αυτές τις περιπτώσεις.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### 1️⃣ Τι γίνεται αν το PDF είναι προστατευμένο με κωδικό;

Η υπερφόρτωση `RecognizePdf` του Aspose.OCR δέχεται ένα αντικείμενο `PdfLoadOptions` όπου μπορείτε να ορίσετε τον κωδικό πρόσβασης:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ Μπορώ να κάνω OCR ολόκληρο το έγγραφο με μία κλήση;

Ναι—απλώς καλέστε `RecognizePdf(pdfFilePath)` χωρίς να καθορίσετε αριθμό σελίδας. Η μέθοδος επιστρέφει ένα μοναδικό `OcrResult` που περιέχει το ενωμένο κείμενο από όλες τις σελίδες.

### 3️⃣ Πώς διαφέρει αυτό από την “εξαγωγή κειμένου από PDF” χρησιμοποιώντας βιβλιοθήκη κειμένου;

Η καθαρή εξαγωγή κειμένου (π.χ., με χρήση iTextSharp) λειτουργεί μόνο σε PDF που ήδη περιέχουν επιλέξιμο κείμενο. **Πώς να OCR PDF** είναι απαραίτητο όταν το PDF είναι ουσιαστικά μια συλλογή εικόνων, όπως σαρωμένα τιμολόγια. Σε αυτές τις περιπτώσεις, η μηχανή OCR εκτελεί οπτική αναγνώριση χαρακτήρων για να μετατρέψει τις εικόνες σε κείμενο αναζητήσιμο.

### 4️⃣ Πώς είναι η απόδοση σε μεγάλα PDF;

Ο χρόνος επεξεργασίας κλιμακώνεται περίπου γραμμικά με τον αριθμό των σελίδων και την ανάλυση της εικόνας. Για μαζικές εργασίες, σκεφτείτε:

- Εκτέλεση OCR παράλληλα (`Parallel.ForEach`)  
- Μείωση DPI εικόνας πριν το OCR (`Resolution = 150`)  
- Caching του αντικειμένου `OcrEngine` αντί για δημιουργία νέου ανά αρχείο  

### 5️⃣ Υπάρχει τρόπος να λάβετε τα πλαίσια (bounding boxes) κάθε λέξης;

Το `OcrResult` εκθέτει μια συλλογή αντικειμένων `OcrRegion`, το καθένα με συντεταγμένες. Μπορείτε να τα διασχίσετε για να δημιουργήσετε αναζητήσιμα PDF ή να επισημάνετε τα αποτελέσματα σε UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## Συμβουλές για Παραγωγικές Υλοποιήσεις

- **Διαχείριση σφαλμάτων:** Τυλίξτε τις κλήσεις OCR σε μπλοκ try/catch για να αποκαλύψετε εξαιρέσεις ειδικές για τη βιβλιοθήκη.  
- **Καταγραφή (Logging):** Καταγράψτε αριθμούς σελίδων και χρόνους επεξεργασίας· βοηθούν στον εντοπισμό προβληματικών σαρώσεων.  
- **Διαχείριση μνήμης:** Αποδεσμεύστε μεγάλα αντικείμενα `Bitmap` αν μετατρέπετε χειροκίνητα τις σελίδες PDF σε εικόνες πριν το OCR.  
- **Ασφάλεια:** Ποτέ μην αποθηκεύετε ακατέργαστα PDF σε μη ασφαλείς δίσκους· σκεφτείτε τη ροή τους απευθείας στη μηχανή OCR.  

## Συμπέρασμα

Τώρα έχετε μια πλήρη, ολοκληρωμένη απάντηση στο **πώς να OCR PDF** χρησιμοποιώντας C#. Το tutorial κάλυψε τα πάντα, από την εγκατάσταση του Aspose.OCR, την επιλογή συγκεκριμένης σελίδας, την εξαγωγή κειμένου, και τη διαχείριση κοινών ακραίων περιπτώσεων. Με αυτή τη βάση μπορείτε να *εξάγετε κείμενο από PDF*, *μετατρέψετε PDF σε κείμενο* και *διαβάσετε σελίδα PDF C#* για οποιοδήποτε pipeline επεξεργασίας εγγράφων χτίζετε.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να τροφοδοτήσετε το αποτέλεσμα OCR σε μια μηχανή πλήρους κειμένου όπως το Lucene.NET, ή δημιουργήστε αναζητήσιμα PDF επικάλυψη του αναγνωρισμένου κειμένου πάνω στις αρχικές εικόνες. Ο ουρανός είναι το όριο, και μόλις αποκτήσατε τα εργαλεία για να το πετύχετε.

---

![παράδειγμα OCR PDF](image-placeholder.png "Εικονογράφηση της επεξεργασίας OCR σε μια σελίδα PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}