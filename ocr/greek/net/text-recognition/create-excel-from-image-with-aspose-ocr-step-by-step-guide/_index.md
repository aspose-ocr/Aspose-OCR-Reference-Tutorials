---
category: general
date: 2026-03-04
description: Δημιουργήστε Excel από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέπετε την εικόνα σε Excel, να εξάγετε πίνακα από την εικόνα και να
  χρησιμοποιείτε το Aspose για OCR εικόνας σε XLSX.
draft: false
keywords:
- create excel from image
- convert image to excel
- extract table from image
- how to use aspose
- ocr image to xlsx
language: el
og_description: Δημιουργήστε Excel από εικόνα γρήγορα. Αυτός ο οδηγός δείχνει πώς
  να μετατρέψετε την εικόνα σε Excel, να εξάγετε πίνακα από την εικόνα και να χρησιμοποιήσετε
  το Aspose OCR για OCR εικόνας σε XLSX.
og_title: Δημιουργία Excel από εικόνα με το Aspose OCR – Πλήρης οδηγός
tags:
- Aspose
- OCR
- Excel
- C#
title: Δημιουργία Excel από εικόνα με το Aspose OCR – Οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/create-excel-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Excel από Εικόνα με Aspose OCR – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **δημιουργήσετε Excel από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να χειριστεί πίνακες αξιόπιστα; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν εμπόδια όταν προσπαθούν να μετατρέψουν μια σαρωμένη απόδειξη ή ένα διάγραμμα εξαγόμενο από PDF σε ένα τακτοποιημένο υπολογιστικό φύλλο.  

Το καλό νέο είναι ότι το Aspose OCR κάνει αυτό παιχνιδάκι. Σε αυτόν τον οδηγό θα **μετατρέψουμε εικόνα σε Excel**, θα εξάγουμε τη δομή του πίνακα και θα καταλήξουμε με ένα έτοιμο προς χρήση αρχείο XLSX—όλα σε λίγες γραμμές C#. Στο τέλος θα γνωρίζετε επίσης **πώς να χρησιμοποιήσετε το Aspose** για το κλασικό σενάριο *ocr image to xlsx*.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR σε ένα έργο .NET.  
- Ο ακριβής κώδικας που χρειάζεται για **εξαγωγή πίνακα από εικόνα** και αποθήκευση ως βιβλίο εργασίας Excel.  
- Συμβουλές για τη διαχείριση εικόνων πολλαπλών σελίδων, διαφορετικών γλωσσών και κοινών προβλημάτων όπως θολές σαρώσεις.  

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το API λειτουργεί με .NET Core, .NET Framework και .NET 5+).  
- Ένα έγκυρο άδεια Aspose OCR (ή μπορείτε να χρησιμοποιήσετε τη δωρεάν δοκιμή).  
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#.  

Αν τα έχετε, ας βουτήξουμε.

---

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose OCR

Πριν γράψετε οποιονδήποτε κώδικα, χρειάζεστε τη βιβλιοθήκη στον υπολογιστή σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

> **Συμβουλή:** Αν χρησιμοποιείτε το .NET CLI, η ισοδύναμη εντολή είναι `dotnet add package Aspose.OCR`. Αυτό εξασφαλίζει ότι έχετε την πιο πρόσφατη έκδοση (από τον Μάρτιο 2026 είναι η 23.12).

---

## Βήμα 2: Αρχικοποίηση του OCR Engine – Ορισμός της Γλώσσας

Η δημιουργία του engine είναι απλή, αλλά αξίζει να εξηγήσουμε **γιατί** ορίζουμε τη γλώσσα. Το Aspose OCR υποστηρίζει πάνω από 60 γλώσσες· η επιλογή της σωστής βελτιώνει δραματικά την ακρίβεια, ειδικά για πίνακες που περιέχουν αριθμούς και σύμβολα.

```csharp
using Aspose.OCR;

// Step 2: Create an OCR engine and specify English (or your target language)
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English   // Change to Language.French, etc., if needed
};
```

Αν η πηγαία εικόνα περιέχει μεικτές γλώσσες, μπορείτε να αφήσετε το `Language` ακαθορισμένο και να αφήσετε το Aspose να εντοπίσει αυτόματα, αλλά αυτό προσθέτει μια μικρή επίπτωση στην απόδοση.

---

## Βήμα 3: Φόρτωση της Πηγαίας Εικόνας που Περιέχει τον Πίνακα

Το Aspose OCR λειτουργεί με οποιαδήποτε μορφή raster (PNG, JPEG, BMP, TIFF). Για τα καλύτερα αποτελέσματα, χρησιμοποιήστε μια μορφή χωρίς απώλειες όπως PNG. Παρακάτω φορτώνουμε ένα αρχείο που ονομάζεται `table.png`.  

```csharp
using Aspose.OCR;
using System.IO;

// Step 3: Load the image that holds the table you want to extract
ImageInfo sourceImage = ImageInfo.Load(@"C:\Images\table.png");
```

> **Ακραία περίπτωση:** Αν η εικόνα σας είναι ένα multi‑page TIFF, καλέστε `ImageInfo.LoadMultiple` και επαναλάβετε για κάθε σελίδα, τροφοδοτώντας την κάθε μία στο OCR engine ξεχωριστά.

---

## Βήμα 4: Εκτέλεση OCR και Λήψη Δομημένων Αποτελεσμάτων

Η μέθοδος `Recognize` κάνει το σκληρό έργο. Επιστρέφει ένα αντικείμενο `OcrResult` που ήδη περιέχει γραμμές, στήλες και βαθμολογίες εμπιστοσύνης κελιών—ιδανικό για άμεση μετατροπή σε Excel.

```csharp
// Step 4: Perform OCR and get a structured result (tables, text blocks, etc.)
OcrResult ocrResult = ocrEngine.Recognize(sourceImage);
```

Γιατί να μην καλέσετε απλώς το `Recognize` και να πάρετε ακατέργαστο κείμενο; Επειδή το δομημένο αποτέλεσμα διατηρεί τη διάταξη του πίνακα, κάτι που είναι απαραίτητο όταν αργότερα **μετατρέψετε εικόνα σε Excel**. Το API εντοπίζει αυτόματα τα σύνορα του πίνακα και συγχωνεύει κελιά όπου είναι κατάλληλο.

---

## Βήμα 5: Μετατροπή του OCR Αποτελέσματος σε Byte Array XLSX

Το Aspose OCR περιλαμβάνει έναν ενσωματωμένο μετατροπέα που παράγει ένα πλήρες βιβλίο εργασίας Excel. Αυτό εξαλείφει την ανάγκη για ξεχωριστή βιβλιοθήκη όπως EPPlus ή ClosedXML.

```csharp
// Step 5: Convert the structured OCR result directly into an Excel workbook (XLSX)
byte[] xlsxData = ocrResult.ToXlsx();
```

Αν χρειάζεται να προσαρμόσετε το βιβλίο εργασίας—π.χ., να εφαρμόσετε προσαρμοσμένο στυλ—μπορείτε να φορτώσετε το byte array σε ένα `System.IO.MemoryStream` και στη συνέχεια να το επεξεργαστείτε με `Aspose.Cells` (άλλο προϊόν της Aspose). Για τις περισσότερες περιπτώσεις, η προεπιλεγμένη έξοδος είναι αρκετά καθαρή.

---

## Βήμα 6: Αποθήκευση του Αρχείου XLSX στον Δίσκο

Τέλος, γράψτε το byte array σε ένα αρχείο. Χρησιμοποιήστε `File.WriteAllBytes` για απλότητα, αλλά μπορείτε επίσης να το στείλετε ως ροή σε μια απάντηση web αν δημιουργείτε ένα API.

```csharp
// Step 6: Persist the generated XLSX file
File.WriteAllBytes(@"C:\Output\table.xlsx", xlsxData);
Console.WriteLine("XLSX saved successfully.");
```

Όταν ανοίξετε το `table.xlsx` θα πρέπει να δείτε μια πιστή αναπαραγωγή του αρχικού πίνακα, με αριθμητικές τιμές να αναγνωρίζονται ως αριθμοί (έτοιμοι για τύπους).

---

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι μια αυτόνομη εφαρμογή console που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο C#. Συγκεντρώνεται και εκτελείται αμέσως (υπό την προϋπόθεση ότι έχετε εγκαταστήσει το πακέτο NuGet και τοποθετήσει μια εικόνα στη συγκεκριμένη διαδρομή).

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine and set language
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the image containing the table
        string inputPath = @"C:\Images\table.png";
        ImageInfo sourceImage = ImageInfo.Load(inputPath);

        // 3️⃣ Perform OCR – we get a structured result with tables
        OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

        // 4️⃣ Convert result to Excel (XLSX) bytes
        byte[] xlsxData = ocrResult.ToXlsx();

        // 5️⃣ Save the XLSX file
        string outputPath = @"C:\Output\table.xlsx";
        File.WriteAllBytes(outputPath, xlsxData);

        Console.WriteLine($"✅ Excel file created at: {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος:** Η κονσόλα εκτυπώνει `✅ Excel file created at: C:\Output\table.xlsx`. Ανοίγοντας το αρχείο εμφανίζεται ένα φύλλο εργασίας με τις ίδιες γραμμές και στήλες όπως η αρχική εικόνα, και τα αριθμητικά κελιά αναγνωρίζονται ως αριθμοί (ώστε να τα αθροίσετε αμέσως).

---

## Συχνές Ερωτήσεις & Προβλήματα

### Τι γίνεται αν το OCR χάσει ένα κελί;

- **Ρύθμιση DPI:** Εικόνες υψηλότερης ανάλυσης (300 dpi ή περισσότερο) βελτιώνουν την ανίχνευση.  
- **Προεπεξεργασία της εικόνας:** Χρησιμοποιήστε μια βιβλιοθήκη όπως `ImageSharp` για να αυξήσετε την αντίθεση ή να αφαιρέσετε τον θόρυβο φόντου πριν τη δώσετε στο Aspose OCR.

### Μπορώ να επεξεργαστώ PDF απευθείας;

Το Aspose OCR λειτουργεί μόνο με raster εικόνες. Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (π.χ., με `Aspose.PDF` ή `PdfiumViewer`), έπειτα εκτελέστε τα παραπάνω βήματα. Αυτό είναι μια τυπική ροή εργασίας για το σενάριο **ocr image to xlsx**.

### Πώς να διαχειριστώ πίνακες πολλαπλών γλωσσών;

Ορίστε `ocrEngine.Language = Language.Multilingual` ή καλέστε `ocrEngine.DetectLanguage = true`. Το engine θα προσπαθήσει να εντοπίσει αυτόματα ανά κελί, κάτι που είναι χρήσιμο όταν έχετε διγλωσσική απόδειξη.

### Απαιτείται άδεια για παραγωγή;

Η δωρεάν δοκιμή λειτουργεί έως 30 ημέρες και προσθέτει υδατογράφημα στο αρχείο Excel. Για παραγωγή, αγοράστε άδεια και καταχωρίστε την με:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Τοποθετήστε αυτό πριν από οποιεσδήποτε κλήσεις OCR.

---

## Μπόνους: Επέκταση του Αποτελέσματος με Aspose.Cells

Αν χρειάζεστε προσαρμοσμένη μορφοποίηση (χρώματα κεφαλίδας, παγωμένα πλαίσια κ.λπ.), μπορείτε να περάσετε το `xlsxData` στο Aspose Cells:

```csharp
using Aspose.Cells;

// Load the generated workbook
Workbook wb = new Workbook(new MemoryStream(xlsxData));

// Apply a style to the first row (header)
Style headerStyle = wb.Worksheets[0].Cells.Rows[0].Style;
headerStyle.ForegroundColor = System.Drawing.Color.LightBlue;
headerStyle.Pattern = BackgroundType.Solid;

// Save the styled workbook
wb.Save(@"C:\Output\styled_table.xlsx");
```

Τώρα δεν έχετε μόνο **μετατρέψει εικόνα σε Excel**, αλλά έχετε επίσης προσθέσει μια επαγγελματική εμφάνιση—ιδανική για πίνακες αναφοράς.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, ολοκληρωμένη λύση για **δημιουργία excel από εικόνα** χρησιμοποιώντας το Aspose OCR. Από την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση σαρώσεων πολλαπλών σελίδων, ο οδηγός σας οδηγεί σε κάθε λεπτομέρεια του **extract table from image** και **ocr image to xlsx**.  

Δοκιμάστε το με μερικά δείγματα στιγμιότυπων—ίσως μια απόδειξη πώλησης ή μια εργαστηριακή αναφορά—και θα δείτε πόσο γρήγορα μια ακατάστατη εικόνα μετατρέπεται σε καθαρό υπολογιστικό φύλλο έτοιμο για ανάλυση.  

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αλυσίδετε αυτή τη ροή εργασίας με έναν αυτοματοποιημένο επεξεργαστή συνημμένων email, ή πειραματιστείτε με το Aspose PDF για να εξάγετε πίνακες απευθείας από PDF. Ο ουρανός είναι το όριο.

---

![Create Excel from Image example](image.png "Create Excel from image - Aspose OCR output")

*Λεζάντα εικόνας: Το παραγόμενο αρχείο Excel αντικατοπτρίζει τον αρχικό πίνακα που καταγράφηκε στο PNG.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}