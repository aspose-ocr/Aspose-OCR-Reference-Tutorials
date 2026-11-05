---
category: general
date: 2026-02-28
description: Δημιουργήστε αναζητήσιμο PDF από ένα πολυ‑σελίδες TIFF σε C#. Αυτός ο
  οδηγός δείχνει πώς να μετατρέψετε εικόνα σε αναζητήσιμο PDF με ένα πλήρες παράδειγμα
  OCR σε C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από αρχείο TIFF χρησιμοποιώντας
  το Aspose.OCR. Ακολουθήστε αυτό το βήμα‑προς‑βήμα παράδειγμα OCR σε C# για να μετατρέψετε
  εικόνες σε PDF με δυνατότητα αναζήτησης.
og_title: Δημιουργία Αναζητήσιμου PDF σε C# – OCR εικόνας σε PDF
tags:
- OCR
- PDF
- C#
- Aspose
title: Δημιουργία Αναζητήσιμου PDF σε C# – Εικόνα σε PDF OCR
url: /el/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF σε C# – Εικόνα σε PDF OCR

Ποτέ χρειάστηκε να **δημιουργήσετε αναζητήσιμο PDF** από ένα σαρωμένο έγγραφο αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι. Σε πολλές ροές εργασίας γραφείου, ένα αναζητήσιμο PDF είναι η διαφορά μεταξύ ενός αδύνατου αρχείου και ενός αναζητήσιμου αρχείου.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες **c# ocr example** που μετατρέπει ένα πολυ‑σελίδων TIFF σε αναζητήσιμο PDF, όλα με το Aspose.OCR. Στο τέλος θα ξέρετε ακριβώς πώς να **image to searchable pdf**, πώς να **convert tiff to pdf**, και θα έχετε ένα έτοιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Μάθετε

* Πώς να εγκαταστήσετε και να αναφερθείτε στο Aspose.OCR σε ένα C# project.  
* Τα ακριβή βήματα για τη φόρτωση ενός TIFF, τον ορισμό της γλώσσας και την κλήση του `RecognizeToPdf`.  
* Γιατί κάθε βήμα είναι σημαντικό – από τη διαχείριση μνήμης μέχρι την επιλογή γλώσσας.  
* Συμβουλές για τη διαχείριση μεγάλων εγγράφων, αντιμετώπιση κοινών προβλημάτων OCR και επέκταση της λύσης σε άλλες μορφές εικόνας.

**Προαπαιτούμενα** – ένα πρόσφατο .NET SDK (4.6+ ή .NET Core 3.1+), Visual Studio (ή το αγαπημένο σας IDE) και μια άδεια Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για δοκιμές). Δεν απαιτούνται άλλες εξωτερικές βιβλιοθήκες.

---

## Δημιουργία Αναζητήσιμου PDF – Επισκόπηση

Σε υψηλό επίπεδο η διαδικασία είναι η εξής:

1. **Initialize** το `OcrEngine`.  
2. **Load** την πηγαία εικόνα (ένα TIFF στην περίπτωσή μας).  
3. **Configure** τις ρυθμίσεις γλώσσας για καλύτερη ακρίβεια.  
4. **Run** OCR και **save** το αποτέλεσμα απευθείας ως αναζητήσιμο PDF.  

Αυτό είναι όλο. Το Aspose API κάνει το βαριά δουλειά, ώστε να μην χρειάζεται να συνδυάσετε ξεχωριστές βιβλιοθήκες OCR και PDF.

---

## Βήμα 1: Εγκατάσταση Aspose.OCR και Ρύθμιση του Project σας

Πρώτα, προσθέστε το πακέτο NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

Ή, αν προτιμάτε το Package Manager Console στο Visual Studio:

```powershell
Install-Package Aspose.OCR
```

Μετά την επαναφορά του πακέτου, ανοίξτε το αρχείο του project και ελέγξτε την αναφορά:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση (ελέγξτε τον ιστότοπο της Aspose) για να λάβετε διορθώσεις σφαλμάτων και τα πιο πρόσφατα language packs.

---

## Βήμα 2: Μετατροπή TIFF σε PDF – Φόρτωση της Εικόνας

Τώρα θα φορτώσουμε το TIFF που θέλετε να κάνετε αναζητήσιμο. Η μέθοδος `Image.Load` της Aspose υποστηρίζει πολυ‑σελίδων TIFF εκτός κουτιού.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Why this matters:** Η φόρτωση της εικόνας μέσα σε ένα `using` block εγγυάται ότι οι μη διαχειριζόμενοι πόροι απελευθερώνονται άμεσα—σημαντικό όταν επεξεργάζεστε μεγάλα έγγραφα.

---

## Βήμα 3: Image to Searchable PDF – Ρύθμιση του OCR Engine

Πριν τρέξουμε το OCR, θα πούμε στη μηχανή ποια γλώσσα να περιμένει. Τα Αγγλικά λειτουργούν για τις περισσότερες περιπτώσεις, αλλά μπορείτε να αντικαταστήσετε με οποιαδήποτε τιμή του enum `OcrLanguage`.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Expert note:** Η επιλογή της σωστής γλώσσας μειώνει δραστικά τις λανθασμένες αναγνώσεις. Αν έχετε μικτές γλώσσες, μπορείτε να τις συνδυάσετε με τον τελεστή `|`, π.χ. `OcrLanguage.English | OcrLanguage.French`.

---

## Βήμα 4: C# OCR Example – Recognize and Save

Με τη μηχανή έτοιμη, καλέστε το `RecognizeToPdf`. Η μέθοδος γράφει το αναζητήσιμο PDF απευθείας στο δίσκο, ενσωματώνοντας ένα αόρατο επίπεδο κειμένου πίσω από την αρχική εικόνα.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Μετά την εκτέλεση αυτής της γραμμής, το `output.pdf` θα περιέχει τις αρχικές σελίδες TIFF συν ένα κρυφό κείμενο που οποιοσδήποτε PDF reader μπορεί να αναζητήσει.

---

## Βήμα 5: C# Image to PDF – Επαλήθευση του Αποτελέσματος

Ας επιβεβαιώσουμε ότι όλα λειτούργησαν. Ανοίξτε το παραγόμενο PDF στο Adobe Reader (ή σε οποιονδήποτε viewer) και δοκιμάστε να ψάξετε για μια λέξη που γνωρίζετε ότι υπάρχει στο αρχικό TIFF.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Αν η αναζήτηση επιστρέψει αποτελέσματα, έχετε δημιουργήσει επιτυχώς **create searchable pdf** από μια εικόνα. Αν όχι, ελέγξτε ξανά τη ρύθμιση γλώσσας ή την ποιότητα του πηγαίου TIFF.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι μια αυτόνομη εφαρμογή console που μπορείτε να μεταγλωττίσετε και να τρέξετε:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Αναμενόμενη έξοδος** (στην κονσόλα):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Ανοίξτε το `output.pdf` και θα πρέπει να μπορείτε να πληκτρολογήσετε οποιαδήποτε λέξη από το αρχικό TIFF στο πεδίο αναζήτησης του viewer και να δείτε τα αποτελέσματα επισημασμένα.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="παράδειγμα δημιουργίας αναζητήσιμου pdf"}

*Το παραπάνω στιγμιότυπο δείχνει ένα αναζητήσιμο PDF ανοιγμένο σε έναν viewer με ενεργό το κρυφό επίπεδο κειμένου.*

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το TIFF μου είναι τεράστιο (εκατοντάδες σελίδες);

Το Aspose.OCR μεταδίδει τις σελίδες μία‑μία, αλλά μπορεί να αντιμετωπίσετε όρια μνήμης. Σκεφτείτε την επεξεργασία του TIFF σε παρτίδες:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Αργότερα, συγχωνεύστε τα PDF ανά‑σελίδα με μια βιβλιοθήκη PDF (π.χ. Aspose.PDF).

### Μπορώ να εξάγω σε διαφορετική μορφή, όπως αναζητήσιμο DOCX;

Ναι—χρησιμοποιήστε το `RecognizeToDocument` αντί για `RecognizeToPdf`. Το API είναι παρόμοιο με τη μέθοδο PDF, απλώς αλλάξτε την επέκταση του αρχείου προορισμού.

### Πώς διαχειρίζομαι γλώσσες εκτός των Αγγλικών;

Αντικαταστήστε το `OcrLanguage.English` με το κατάλληλο enum, π.χ. `OcrLanguage.Spanish`. Μπορείτε επίσης να συνδυάσετε γλώσσες:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### Τι γίνεται με PDF που είναι προστατευμένα με κωδικό;

Μετά το βήμα OCR, μπορείτε να ανοίξετε το παραγόμενο PDF με το Aspose.PDF και να εφαρμόσετε κρυπτογράφηση:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Συνοψίζοντας

Καλύψαμε όλα όσα χρειάζεστε για να **create searchable PDF** αρχεία από εικόνες TIFF χρησιμοποιώντας C#. Από την εγκατάσταση του Aspose.OCR, τη φόρτωση της εικόνας, τη ρύθμιση γλώσσας, την εκτέλεση OCR, μέχρι την επαλήθευση του αναζητήσιμου αποτελέσματος, έχετε τώρα ένα σταθερό **c# ocr example** που μπορείτε να προσαρμόσετε σε άλλες μορφές.  

Αν είστε έτοιμοι να προχωρήσετε, δοκιμάστε:

* **Convert TIFF to PDF** για μη‑αναζητήσιμα αρχεία (απλώς παραλείψτε το βήμα OCR).  
* Πειραματιστείτε με **image to searchable pdf**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}