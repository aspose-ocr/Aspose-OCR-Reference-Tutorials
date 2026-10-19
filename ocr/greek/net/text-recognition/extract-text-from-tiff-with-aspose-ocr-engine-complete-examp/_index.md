---
category: general
date: 2026-04-04
description: Μάθετε πώς να εξάγετε κείμενο από αρχεία TIFF χρησιμοποιώντας ένα παράδειγμα
  μηχανής OCR σε C#. Οδηγός βήμα‑βήμα με έξοδο JSON και XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: el
og_description: Εξαγωγή κειμένου από αρχεία TIFF χρησιμοποιώντας μηχανή OCR, παράδειγμα
  σε C#. Λεπτομερή βήματα, πλήρης κώδικας και συμβουλές για έξοδο JSON/XML.
og_title: Εξαγωγή κειμένου από TIFF με τη μηχανή OCR της Aspose – Πλήρης οδηγός
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από TIFF με τη μηχανή OCR της Aspose – Πλήρες παράδειγμα
url: /el/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από TIFF – Πλήρες Παράδειγμα Μηχανής OCR σε C#

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από TIFF** εικόνες αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να διαχειριστεί αρχεία πολλαπλών σελίδων χωρίς έναν κύκλο παρακάμψεων; Δεν είστε οι μόνοι. Σε πολλά παλαιά συστήματα, τα έγγραφα φτάνουν ως σάρωση πολλαπλών σελίδων TIFF, και η εξαγωγή του ακατέργαστου κειμένου είναι μια απαραίτητη λειτουργία για αναζήτηση, συμμόρφωση ή αυτοματοποίηση εισαγωγής δεδομένων.

Τα καλά νέα; Με το Aspose OCR μπορείτε να το κάνετε σε λίγες γραμμές—χωρίς να παίζετε με buffers χαμηλού επιπέδου. Αυτό το tutorial σας οδηγεί μέσα από ένα **πλήρες παράδειγμα μηχανής OCR** που φορτώνει ένα πολυσέλιδο TIFF, αναγνωρίζει κάθε σελίδα και παράγει τόσο μορφοποιημένο JSON όσο και προαιρετικό XML. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας C# που εξάγει κείμενο από αρχεία TIFF σε δευτερόλεπτα.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη μηχανή Aspose OCR σε ένα έργο .NET.  
- Ο ακριβής κώδικας που απαιτείται για **εξαγωγή κειμένου από TIFF** αρχεία, συμπεριλαμβανομένης της διαχείρισης πολλαπλών σελίδων.  
- Γιατί μπορεί να θέλετε έξοδο JSON αντί XML και πώς να δημιουργήσετε και τα δύο.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων (π.χ., DPI εικόνας, χρήση μνήμης).  

### Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί με .NET Core και .NET Framework).  
- Ένα έγκυρο άδεια Aspose OCR (ή κλειδί δωρεάν δοκιμής).  
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε.  
- Ένα δείγμα αρχείου πολυσέλιδου TIFF (ονομαζόμενο `multi-page.tiff` στο παράδειγμα).  

> **Pro tip:** Αν έχετε περιορισμένο προϋπολογισμό, η δωρεάν δοκιμή σας επιτρέπει ακόμη να εξάγετε κείμενο από έως 100 σελίδες ανά μήνα—ιδανικό για δοκιμές.

---

## Βήμα 1 – Αρχικοποίηση της Μηχανής OCR (παράδειγμα μηχανής OCR)

Πριν μπορέσουμε να **εξάγουμε κείμενο από TIFF**, χρειαζόμαστε μια παρουσία της μηχανής OCR. Αυτό το αντικείμενο περιέχει όλες τις ρυθμίσεις που μπορεί να τροποποιήσετε αργότερα (γλώσσα, ανάλυση κ.λπ.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Γιατί είναι σημαντικό:* Η κλάση `OcrEngine` αφαιρεί το βαριά έργο. Η δημιουργία μιας στιγμής της μία φορά και η επαναχρησιμοποίησή της για πολλές εικόνες είναι πιο αποδοτική σε μνήμη από το να δημιουργείτε νέα μηχανή ανά σελίδα.

---

## Βήμα 2 – Φόρτωση του Πολυσέλιδου TIFF (εξαγωγή κειμένου από TIFF)

Τώρα κατευθύνουμε τη μηχανή στο αρχείο προέλευσης. Η `ImageStream.FromFile` υποστηρίζει TIFF, JPEG, PNG και πολλά άλλα, αλλά για αυτό το tutorial εστιάζουμε στο TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Σημείωση:** Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου στο μηχάνημά σας.  
> **Συμβουλή:** Αν το TIFF σας έχει χαμηλό DPI (κάτω από 150), σκεφτείτε προεπεξεργασία για να βελτιώσετε την ακρίβεια του OCR.

---

## Βήμα 3 – Αναγνώριση Όλων των Σελίδων

Καλώντας το `Recognize()` εκτελεί τον αλγόριθμο OCR σε **κάθε σελίδα** του TIFF. Το αντικείμενο αποτελέσματος περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και τη διαίρεση ανά σελίδα.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Τι λαμβάνετε:* Το `ocrResult` περιέχει μια συλλογή αντικειμένων `PageResult`. Το κείμενο κάθε σελίδας μπορεί να προσπελαστεί μέσω `ocrResult.Pages[i].Text`. Η μηχανή παρέχει επίσης επίπεδα εμπιστοσύνης, χρήσιμα για ελέγχους ποιότητας.

---

## Βήμα 4 – Αποθήκευση Αποτελεσμάτων ως JSON (και προαιρετικό XML)

Οι περισσότερες σύγχρονες ροές δεδομένων προτιμούν JSON, αλλά τα παλαιά συστήματα εξακολουθούν να χρησιμοποιούν XML. Εδώ είναι πώς να δημιουργήσετε και τα δύο, με ωραία μορφοποίηση.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Παράδειγμα Εξόδου JSON (κομμένο)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

Το JSON είναι αναγνώσιμο από άνθρωπο, καθιστώντας τον εντοπισμό σφαλμάτων εύκολο. Το XML αντικατοπτρίζει την ίδια δομή αν το χρειάζεστε.

---

## Βήμα 5 – Επαλήθευση της Εξαγωγής (εξαγωγή κειμένου από TIFF)

Μετά τη δημιουργία των αρχείων, ένας γρήγορος έλεγχος λογικής βοηθά να διασφαλιστεί ότι δεν συνέβη κάτι λάθος.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Αν δείτε το απόσπασμα εκτυπωμένο, έχετε εξάγει με επιτυχία **κείμενο από TIFF** και το έχετε αποθηκεύσει. Από εδώ μπορείτε να τροφοδοτήσετε το JSON σε έναν δείκτη αναζήτησης, μια βάση δεδομένων ή οποιαδήποτε υπηρεσία downstream.

---

## Γιατί να Χρησιμοποιήσετε το Aspose OCR για εξαγωγή κειμένου από TIFF;

- **Υποστήριξη πολλαπλών σελίδων έτοιμη προς χρήση** – δεν χρειάζεται να χωρίσετε το TIFF χειροκίνητα.  
- **Υψηλή ακρίβεια** χάρη σε ιδιόκτητα μοντέλα νευρωνικών δικτύων.  
- **Διαπλατφορμική** – λειτουργεί σε Windows, Linux και macOS .NET runtime.  
- **Πλούσια μορφότυπα εξόδου** (JSON, XML, απλό κείμενο) που ταιριάζουν τόσο σε σύγχρονες όσο και σε παλαιές υποδομές.  

Αν εξακολουθείτε να διστάζετε, δοκιμάστε τη δωρεάν δοκιμή σε ένα δείγμα εγγράφου. Θα παρατηρήσετε την ταχύτητα και την απλότητα σε σύγκριση με ανοιχτού κώδικα εναλλακτικές λύσεις που συχνά απαιτούν πρόσθετη προεπεξεργασία εικόνας.

---

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Συμπτώματα | Διόρθωση |
|----------|------------|----------|
| Χαμηλή ανάλυση TIFF | Ελλιπή χαρακτήρες, χαμηλή εμπιστοσύνη | Ανεβάστε την ανάλυση της εικόνας σε ≥150 DPI πριν το OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Λάθος γλώσσα | Ακατάληπτες λέξεις, ειδικά για μη‑αγγλικά κείμενα | Ορίστε `ocrEngine.Language = Language.Spanish` (ή την κατάλληλη) πριν το `Recognize()` |
| Έλλειψη μνήμης σε μεγάλα αρχεία | `OutOfMemoryException` | Επεξεργαστείτε τις σελίδες σε παρτίδες: κάντε βρόχο μέσω `ocrEngine.Image.Pages` και καλέστε `RecognizePage(i)` |
| Μη εφαρμοσμένη άδεια | Υδατογράφημα “Evaluation” στην έξοδο | Καταχωρίστε την άδειά σας: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε ένα νέο έργο κονσόλας. Περιλαμβάνει όλα τα τμήματα που συζητήσαμε—αρχικοποίηση, φόρτωση, αναγνώριση και αποθήκευση.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Αποθηκεύστε το αρχείο ως `Program.cs`, εκτελέστε `dotnet run`, και παρακολουθήστε την κονσόλα να σας δείχνει πού αποθηκεύτηκαν το JSON και το XML. Αυτό είναι—μόλις ολοκληρώσατε ένα **παράδειγμα μηχανής OCR** που εξάγει κείμενο από TIFF.

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Επεξεργασία παρτίδας:** Τυλίξτε τη λογική σε βρόχο `foreach` για να διαχειριστείτε αυτόματα δεκάδες αρχεία TIFF.  
- **Ενσωμάτωση αναζήτησης:** Σπρώξτε το JSON στο Elasticsearch ή στο Azure Cognitive Search για να ενεργοποιήσετε πλήρη αναζήτηση κειμένου σε σαρωμένα έγγραφα.  
- **Προεπεξεργασία εικόνας:** Εξερευνήστε το API `ImageProcessing` του Aspose για διόρθωση κλίσης, αφαίρεση θορύβου ή ρύθμιση αντίθεσης πριν το OCR.  
- **Εναλλακτική έξοδος:** Χρησιμοποιήστε `ocrResult.ToPlainText()` αν χρειάζεστε μόνο ακατέργαστες συμβολοσειρές χωρίς μεταδεδομένα.  

Αν σας ενδιαφέρουν άλλες μορφές εικόνας, το ίδιο μοτίβο λειτουργεί για PDFs (απλώς αλλάξτε το αρχείο προέλευσης) ή PNG. Το κύριο συμπέρασμα είναι ότι μόλις ρυθμιστεί η μηχανή, το υπόλοιπο είναι μια επαναλαμβανόμενη ροή.

---

## Συμπέρασμα

Διασχίσαμε ένα **πλήρες παράδειγμα μηχανής OCR** που σας επιτρέπει να **εξάγετε κείμενο από αρχεία TIFF** με το Aspose OCR, παράγοντας καθαρό JSON και προαιρετικό XML για οποιαδήποτε επόμενη ροή εργασίας. Ο κώδικας είναι αυτόνομος, οι εξηγήσεις καλύπτουν το “γιατί” πίσω από κάθε βήμα

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}