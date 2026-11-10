---
category: general
date: 2026-06-25
description: Οδηγός OCR εικόνας σε Excel που δείχνει πώς να εξάγετε πίνακα από εικόνα
  και να μετατρέψετε σκαναρισμένο πίνακα σε Excel χρησιμοποιώντας το Aspose.OCR. Περιλαμβάνεται
  παράδειγμα κώδικα βήμα‑βήμα.
draft: false
keywords:
- ocr image to excel
- extract table from image
- how to convert scanned table to excel
- convert image to excel
language: el
og_description: Μάθετε πώς να μετατρέπετε εικόνα σε OCR για Excel, να εξάγετε πίνακα
  από εικόνα και να μετατρέψετε σαρωμένο πίνακα σε Excel με ένα πλήρες παράδειγμα
  C# χρησιμοποιώντας το Aspose.OCR.
og_title: OCR εικόνα σε Excel – Οδηγός μετατροπής βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: OCR image to Excel tutorial that shows how to extract table from image
    and convert scanned table to Excel using Aspose.OCR. Step‑by‑step code example
    included.
  headline: OCR Image to Excel – Complete Guide to Convert Scanned Tables to Excel
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- Excel automation
title: OCR εικόνα σε Excel – Πλήρης οδηγός για τη μετατροπή σαρωμένων πινάκων σε Excel
url: /el/net/image-and-drawing-recognition/ocr-image-to-excel-complete-guide-to-convert-scanned-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Image to Excel – Πλήρης Οδηγός για τη Μετατροπή Σαρωμένων Πινάκων σε Excel

Έχετε αναρωτηθεί ποτέ πώς να **OCR image to Excel** χωρίς να περνάτε ώρες πληκτρολογώντας δεδομένα με το χέρι; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν ένας πελάτης παραδίδει έναν σαρωμένο πίνακα και περιμένει ένα τακτοποιημένο φύλλο εργασίας. Τα καλά νέα; Με λίγες γραμμές C# και Aspose.OCR μπορείτε να μετατρέψετε αυτήν την εικόνα σε ένα καθαρό βιβλίο εργασίας Excel σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **extract table from image**, θα σας δείξουμε **how to convert scanned table to Excel**, και θα σας δώσουμε ένα έτοιμο προς εκτέλεση δείγμα κώδικα. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET και να αρχίσετε αμέσως τη μετατροπή εικόνων σε Excel.

## Τι Θα Χρειαστείτε

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί τόσο με .NET Core όσο και με .NET Framework)  
* Άδεια Aspose.OCR ή δωρεάν κλειδί αξιολόγησης (η βιβλιοθήκη είναι διαθέσιμη μέσω NuGet)  
* Μια σαρωμένη εικόνα που περιέχει έναν καθαρό πίνακα (JPEG ή PNG είναι τα καλύτερα)  
* Visual Studio, Rider ή οποιονδήποτε επεξεργαστή προτιμάτε  

Αυτό είναι όλο—χωρίς επιπλέον υπηρεσίες, χωρίς κλήσεις OCR στο cloud, μόνο καθαρή τοπική επεξεργασία.

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose.OCR

Για να ξεκινήσετε, δημιουργήστε μια νέα εφαρμογή console:

```bash
dotnet new console -n OcrToExcelDemo
cd OcrToExcelDemo
```

Στη συνέχεια προσθέστε το πακέτο Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Αν βρίσκεστε σε εταιρικό δίκτυο, εκτελέστε την εντολή με `--no-cache` για να αποφύγετε παλαιά πακέτα.

## Βήμα 2: Αρχικοποίηση του OCR Engine (Η Καρδιά του OCR Image to Excel)

Το πρώτο κομμάτι κώδικα δημιουργεί μια παρουσία `OcrEngine`. Σκεφτείτε το ως τη μηχανή που διαβάζει τα pixel και αποφασίζει ποιος χαρακτήρας είναι.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class ExcelOutputExample
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var engine = new OcrEngine();
```

Γιατί χωρίζουμε την αρχικοποίηση της μηχανής από τη φόρτωση της εικόνας; Επειδή η μηχανή μπορεί να επαναχρησιμοποιηθεί για πολλές εικόνες, εξοικονομώντας μνήμη και χρόνο εκκίνησης—ιδιαίτερα χρήσιμο όταν χρειάζεται να **convert image to Excel** σε εργασία δέσμης.

## Βήμα 3: Φόρτωση της Εικόνας που Περιέχει τον Πίνακα

Στη συνέχεια κατευθύνουμε το OCR engine στο αρχείο που περιέχει τον σαρωμένο πίνακα. Η `OcrImage.FromFile` υποστηρίζει πολλές μορφές, αλλά για τα καλύτερα αποτελέσματα χρησιμοποιήστε σαρώσεις υψηλής ανάλυσης (300 dpi ή υψηλότερα).

```csharp
        // Step 2: Load the image containing the table to be recognized
        var image = OcrImage.FromFile("YOUR_DIRECTORY/table_scan.jpg");
```

> **Εξαίρεση:** Αν η εικόνα είναι περιστραμμένη, καλέστε `image.Rotate(90)` πριν από την αναγνώριση. Η μηχανή μπορεί να χειριστεί την περιστροφή, αλλά η παροχή σωστά προσανατολισμένων δεδομένων βελτιώνει την ακρίβεια.

## Βήμα 4: Εκτέλεση της Αναγνώρισης

Τώρα η μηχανή κάνει τη βαριά δουλειά. Η `engine.Recognize(image)` επιστρέφει ένα αντικείμενο `OcrResult` που ήδη ξέρει πώς να χωρίσει τις γραμμές σε σειρές και τις λέξεις σε κελιά.

```csharp
        // Step 3: Perform OCR recognition on the image
        var ocrResult = engine.Recognize(image);
```

Το `OcrResult` είναι περισσότερο από απλό κείμενο—περιέχει μια δομή που γνωρίζει πίνακες. Γι' αυτό αυτή η μέθοδος είναι ιδανική για το σενάριο **extract table from image**.

## Βήμα 5: Προετοιμασία Memory Stream για το Excel Workbook

Αντί να γράψουμε αμέσως στο δίσκο, κρατάμε αρχικά το αρχείο Excel στη μνήμη. Αυτό μας δίνει ευελιξία να το στείλουμε μέσω HTTP, να το επισυνάψουμε σε email, ή να το επεξεργαστούμε περαιτέρω πριν την αποθήκευση.

```csharp
        // Step 4: Prepare a memory stream to hold the Excel output
        using (var excelStream = new MemoryStream())
        {
```

## Βήμα 6: Αποθήκευση του OCR Result Απευθείας ως Αρχείο Excel

Αυτή είναι η μαγική γραμμή που μετατρέπει το αποτέλεσμα OCR σε ένα σωστό βιβλίο εργασίας `.xlsx`. Κάθε αναγνωρισμένη γραμμή γίνεται σειρά, κάθε λέξη κελί—ακριβώς ό,τι χρειάζεστε όταν **convert image to Excel**.

```csharp
            // Step 5: Save the OCR result as an Excel workbook 
            // (each line becomes a row, each word becomes a cell)
            ocrResult.SaveAsExcel(excelStream);
```

Αν χρειάζεστε περισσότερο έλεγχο (π.χ., συγχώνευση κελιών για επικεφαλίδες πολλαπλών στηλών), μπορείτε να επεξεργαστείτε το stream με μια βιβλιοθήκη όπως EPPlus—αλλά για τις περισσότερες γρήγορες εργασίες μετατροπής αυτή η έτοιμη μέθοδος είναι επαρκής.

## Βήμα 7: Εγγραφή του Αρχείου Excel στον Δίσκο

Τέλος αποθηκεύουμε το βιβλίο εργασίας σε αρχείο. Μπορείτε επίσης να επιστρέψετε `excelStream.ToArray()` από ένα endpoint Web API αν χτίζετε μια υπηρεσία.

```csharp
            // Step 6: Write the Excel file to disk
            File.WriteAllBytes("YOUR_DIRECTORY/table.xlsx", excelStream.ToArray());
        }
```

## Βήμα 8: Ειδοποίηση του Χρήστη

Ένα απλό μήνυμα console επιβεβαιώνει την επιτυχία. Σε μια πραγματική εφαρμογή θα το αντικαταστήσετε με κατάλληλη καταγραφή.

```csharp
        // Step 7: Inform the user that the Excel file has been created
        Console.WriteLine("Excel file created.");
    }
}
```

### Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs`, προσαρμόστε τις διαδρομές αρχείων και πατήστε **F5**.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class ExcelOutputExample
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var engine = new OcrEngine();

        // Step 2: Load the image containing the table to be recognized
        var image = OcrImage.FromFile("YOUR_DIRECTORY/table_scan.jpg");

        // Step 3: Perform OCR recognition on the image
        var ocrResult = engine.Recognize(image);

        // Step 4: Prepare a memory stream to hold the Excel output
        using (var excelStream = new MemoryStream())
        {
            // Step 5: Save the OCR result as an Excel workbook 
            // (each line becomes a row, each word becomes a cell)
            ocrResult.SaveAsExcel(excelStream);

            // Step 6: Write the Excel file to disk
            File.WriteAllBytes("YOUR_DIRECTORY/table.xlsx", excelStream.ToArray());
        }

        // Step 7: Inform the user that the Excel file has been created
        Console.WriteLine("Excel file created.");
    }
}
```

> **Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση, θα βρείτε το `table.xlsx` στον καθορισμένο φάκελο. Ανοίξτε το στο Excel και θα δείτε κάθε κελί να περιέχει το κείμενο που ανίχνευσε η μηχανή OCR από την αρχική εικόνα.

## Συνηθισμένα Προβλήματα και Πώς να τα Διορθώσετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|-------|----------------|-----|
| **Garbage characters** | Χαμηλής ανάλυσης εικόνα ή θορυβώδες φόντο | Προεπεξεργασία της εικόνας (αύξηση DPI, εφαρμογή δυαδικοποίησης) πριν την περάσετε στο `OcrEngine`. |
| **Merged cells** | Η μηχανή θεωρεί τα κενά ως διαχωριστές, αλλά η ευθυγράμμιση των στηλών είναι λανθασμένη | Χρησιμοποιήστε `ocrResult.SaveAsExcel(excelStream, new ExcelSaveOptions { UseTabularStructure = true })` για να επιβάλετε πιο αυστηρή διάταξη πίνακα. |
| **Missing rows** | Ο πίνακας έχει λεπτές γραμμές που το OCR θεωρεί ως φόντο | Αυξήστε την αντίθεση ή χρησιμοποιήστε `engine.ImagePreprocessingOptions.ApplyDeskew = true`. |
| **Large file size** | Αποθηκεύσατε το βιβλίο εργασίας σε παλαιό μορφότυπο XLS | Βεβαιωθείτε ότι χρησιμοποιείτε την προεπιλεγμένη έξοδο XLSX (OpenXML); η μέθοδος `SaveAsExcel` το κάνει ήδη. |

## Επέκταση της Λύσης – Τι Ακολουθεί;

Τώρα που έχετε κατακτήσει τα βασικά του **ocr image to Excel**, σκεφτείτε τα επόμενα βήματα:

* **Batch processing** – Επανάληψη σε φάκελο εικόνων, συγχώνευση αποτελεσμάτων σε ένα ενιαίο βιβλίο εργασίας, ή δημιουργία αρχείου zip με πολλά αρχεία Excel.  
* **Cloud integration** – Ενσωμάτωση του κώδικα σε ASP.NET Core API ώστε οι χρήστες να μπορούν να ανεβάζουν εικόνες και να λαμβάνουν άμεσα αρχεία Excel.  
* **Data validation** – Μετά τη μετατροπή, εκτελέστε έναν γρήγορο έλεγχο λογικής (π.χ., βεβαιωθείτε ότι οι αριθμητικές στήλες περιέχουν αριθμούς) χρησιμοποιώντας βιβλιοθήκη όπως `ClosedXML`.  
* **Styling** – Χρησιμοποιήστε EPPlus ή NPOI για να προσθέσετε μορφοποίηση κεφαλίδων, αυτόματη προσαρμογή στηλών, ή να εφαρμόσετε conditional formatting βάσει βαθμών εμπιστοσύνης OCR.  

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στο βασικό μοτίβο που καλύψαμε: **extract table from image**, τροφοδοτήστε το αποτέλεσμα σε ένα Excel stream, και παραδώστε ένα χρήσιμο αρχείο.

## Συμπέρασμα

Αυτά είναι—ένας απλός, ολοκληρωμένος οδηγός για **how to convert scanned table to Excel** χρησιμοποιώντας Aspose.OCR και C#. Ξεκινήσαμε με το πρόβλημα της μετατροπής μιας εικόνας πίνακα σε ένα χρήσιμο φύλλο εργασίας, περάσαμε από κάθε γραμμή κώδικα, εξηγήσαμε γιατί κάθε βήμα είναι σημαντικό, και ακόμη επισημάναμε κοινά προβλήματα που μπορεί να αντιμετωπίσετε.

Τώρα μπορείτε με σιγουριά να πείτε ότι ξέρετε πώς να **ocr image to excel**, και έχετε μια σταθερή βάση για να επεκτείνετε σε εργασίες δέσμης, web services, ή πιο πλούσιες αναφορές Excel. Δοκιμάστε το με τις δικές σας σαρώσεις, προσαρμόστε τις επιλογές προεπεξεργασίας, και δείτε τον χρόνο που εξοικονομείται να αυξάνεται.

Έχετε ερωτήσεις σχετικά με εξαιρέσεις ή θέλετε να μοιραστείτε μια επιτυχημένη ιστορία; Αφήστε ένα σχόλιο παρακάτω—ας συνεχίσουμε τη συζήτηση. Καλό κώδικα!  

![Διάγραμμα που δείχνει τη ροή εργασίας OCR Image to Excel – η σαρωμένη εικόνα πίνακα επεξεργάζεται και μετατρέπεται σε αρχείο Excel](/images/ocr-image-to-excel-workflow.png){: .center alt="διάγραμμα ροής ocr image to excel"}

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικότατα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εξάγετε πίνακα από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Πώς να εξάγετε κείμενο από εικόνα προετοιμάζοντας ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}