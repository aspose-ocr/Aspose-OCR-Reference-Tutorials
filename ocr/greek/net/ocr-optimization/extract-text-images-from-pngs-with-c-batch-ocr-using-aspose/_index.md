---
category: general
date: 2026-02-09
description: Εξάγετε κείμενο από εικόνες γρήγορα με C# ορίζοντας το μέγιστο επίπεδο
  παραλληλισμού για batch OCR – μάθετε να μετατρέπετε σαρωμένες σελίδες, να διαχειρίζεστε
  OCR πολλαπλών εικόνων και να διαβάζετε κείμενο PNG αποδοτικά.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: el
og_description: Εξαγωγή κειμένου από εικόνες σε C# ορίζοντας μέγιστο παράλληλο επίπεδο.
  Αυτό το σεμινάριο δείχνει πώς να μετατρέψετε σαρωμένες σελίδες, να εκτελέσετε πολλαπλή
  OCR εικόνων και να διαβάσετε κείμενο PNG με το Aspose OCR.
og_title: Εξαγωγή κειμένου από εικόνες PNG με C# – Πλήρης Οδηγός Batch OCR
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Εξαγωγή κειμένου από εικόνες PNG με C# – Μαζική OCR χρησιμοποιώντας Aspose
  OCR
url: /el/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εξαγωγή κειμένου από εικόνες PNG με C# – Batch OCR χρησιμοποιώντας Aspose OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνες** από έναν φάκελο σαρωμένων PNG αλλά να έχετε κολλήσει στο ερώτημα «πώς θα το κάνω γρήγορα;»; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα, οι προγραμματιστές πρέπει να **ορίσουν το μέγιστο παράλληλο** ώστε δεκάδες σελίδες να επεξεργάζονται σε δευτερόλεπτα αντί για λεπτά.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που **μετατρέπει σαρωμένες σελίδες**, εκτελεί **πολλαπλό OCR εικόνας**, και τελικά **διαβάζει κείμενο png** χωρίς κανένα πρόβλημα. Χωρίς αόριστους συνδέσμους «δείτε την τεκμηρίωση»—απλώς κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε, εξηγήσεις για το γιατί κάθε γραμμή είναι σημαντική, και συμβουλές για να αποφύγετε τα συνηθισμένα προβλήματα.

> **Pro tip:** Αν ήδη χρησιμοποιείτε το Aspose OCR σε άλλο μέρος, θα παρατηρήσετε ότι η ίδια κλάση `OcrEngine` εμφανίζεται εδώ, αλλά θα ρυθμίσουμε τη διαμόρφωσή της για πραγματική παράλληλη επεξεργασία.

---

## Τι Θα Χρειαστεί

- **.NET 6+** (ή .NET Framework 4.6+). Το API λειτουργεί το ίδιο, αλλά τα νεότερα runtime παρέχουν καλύτερη διαχείριση νημάτων.  
- **Aspose.OCR for .NET** – εγκατάσταση μέσω NuGet: `Install-Package Aspose.OCR`.  
- Ένας φάκελος που περιέχει μερικές σαρώσεις PNG (`page1.png`, `page2.png`, …).  
- Ένα IDE ή επεξεργαστή με τον οποίο αισθάνεστε άνετα (Visual Studio, Rider, VS Code…).

Αυτό είναι όλο. Χωρίς επιπλέον υπηρεσίες, χωρίς κλειδιά cloud, μόνο καθαρή τοπική επεξεργασία.

---

## εξαγωγή κειμένου από εικόνες – Ορισμός Μέγιστης Παράλληλης Επεξεργασίας για Batch OCR

Όταν εκκινείτε OCR σε πολλά αρχεία, η μηχανή, από προεπιλογή, χρησιμοποιεί ένα μόνο νήμα. Είναι ασφαλές αλλά εξαιρετικά αργό. Ρυθμίζοντας το `MaxDegreeOfParallelism` λέτε στη μηχανή πόσα νήματα μπορεί να δημιουργήσει ταυτόχρονα.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Γιατί 4;**  
Τα τέσσερα είναι ένα ιδανικό σημείο στα περισσότερα σύγχρονα laptops—αρκετοί πυρήνες για να κρατούν την CPU απασχολημένη, αλλά όχι τόσο πολλοί ώστε να πνίγουν τις άλλες διεργασίες. Αν τρέχετε αυτό σε διακομιστή με 16 πυρήνες, αυξήστε τον αριθμό στα 12 ή 14 για αισθητή επιτάχυνση.

---

## Μετατροπή σαρωμένων σελίδων – Δημιουργία Συλλογής Image Stream

Το Aspose αναμένει κάθε εικόνα ως `ImageStream`. Η βοηθητική μέθοδος `FromFile` διαβάζει το αρχείο, το κρατά στη μνήμη, και το παραδίδει στη μηχανή OCR. Μπορείτε επίσης να περάσετε ένα `MemoryStream` αν οι εικόνες προέρχονται από βάση δεδομένων ή από HTTP response.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Edge case:** Αν κάποιο αρχείο λείπει ή είναι κατεστραμμένο, το `FromFile` θα ρίξει `FileNotFoundException`. Τυλίξτε τη δημιουργία σε `try/catch` αν περιμένετε ασταθή είσοδο.

---

## πολλαπλό OCR εικόνας – Εκτέλεση Batch OCR

Τώρα γίνεται η βαριά δουλειά. Η `RecognizeBatch` δημιουργεί έως τον αριθμό νημάτων που ορίσατε νωρίτερα, επεξεργάζεται κάθε εικόνα, και επιστρέφει μια λίστα αντικειμένων `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Στο παρασκήνιο, κάθε νήμα φορτώνει την εικόνα του, τρέχει το νευρωνικό δίκτυο, και εξάγει απλό κείμενο. Η σειρά των αποτελεσμάτων ταιριάζει με τη σειρά της λίστας εισόδου, ώστε να μπορείτε με ασφάλεια να αντιστοιχίσετε σελίδα 1 → αποτέλεσμα 0, κ.ο.κ.

---

## ανάγνωση κειμένου png – Εμφάνιση του Εξαγόμενου Περιεχομένου

Τέλος, διατρέχουμε τα αποτελέσματα και εκτυπώνουμε το απλό κείμενο στην κονσόλα. Εδώ μπορείτε να κατευθύνετε την έξοδο σε αρχείο, βάση δεδομένων, ή ακόμη και σε downstream υπηρεσία NLP.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Αναμενόμενη Έξοδος Κονσόλας

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Αν δείτε κενές ενότητες, ελέγξτε ξανά ότι τα PNG δεν είναι καθαρά λευκά—το OCR χρειάζεται αντίθεση.

---

## Πρακτικές Συμβουλές & Συνηθισμένα Πιθανά Προβλήματα

| Κατάσταση | Τι να κάνετε |
|-----------|--------------|
| **Πίεση μνήμης** σε μεγάλα batch | Επεξεργαστείτε τις εικόνες σε τμήματα των 10‑20 αρχείων, και καλέστε `GC.Collect()` αν παρατηρήσετε αυξήσεις. |
| **Λανθασμένος εντοπισμός γλώσσας** | Ορίστε `ocrEngine.Configuration.Language = OcrLanguage.English;` (ή τη γλώσσα‑στόχο) πριν καλέσετε `RecognizeBatch`. |
| **Αργή απόδοση παρά την παράλληλη επεξεργασία** | Βεβαιωθείτε ότι το SSD σας δεν περιορίζει το I/O· διαβάστε όλα τα αρχεία στη μνήμη πρώτα (όπως κάνουμε με `ImageStream.FromFile`). |
| **Απουσία χαρακτήρων** | Αυξήστε το `ocrEngine.Configuration.DPI = 300;` για επεξεργασία υψηλότερης ανάλυσης. |

---

## Επέκταση του Παραδείγματος – Από PNG σε PDF ή DOCX

Αν τελικά χρειαστεί να **μετατρέψετε σαρωμένες σελίδες** σε αναζητήσιμα PDFs, απλώς περάστε το ίδιο `ocrResults[i].PlainText` σε βιβλιοθήκη PDF (π.χ., Aspose.PDF) και επικάψτε το κείμενο ως αόρατο στρώμα. Η ίδια τεχνική παράλληλης επεξεργασίας λειτουργεί και εκεί.

---

## Πλήρης Πηγαίος Κώδικας (Έτοιμος για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Αποθηκεύστε το ως `BatchExample.cs`, τρέξτε `dotnet run`, και παρακολουθήστε την κονσόλα σας να γεμίζει με το κείμενο που κρυβόταν μέσα σε αυτές τις PNG σαρώσεις.

---

## Οπτική Σύνοψη

![παράδειγμα εξαγωγής κειμένου από εικόνες](images/ocr-batch.png){alt="παράδειγμα εξαγωγής κειμένου από εικόνες"}

Το διάγραμμα δείχνει τη ροή: **Αρχεία PNG → Συλλογή ImageStream → OcrEngine (max parallelism) → Αποτελέσματα OCR → Κονσόλα / downstream αποθήκευση**.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, end‑to‑end συνταγή για το πώς να **εξάγετε κείμενο από εικόνες** σε C# ενώ **ορίζετε μέγιστη παράλληλη επεξεργασία**, **μετατρέπετε σαρωμένες σελίδες**, διαχειρίζεστε **πολλαπλό OCR εικόνας**, και **διαβάζετε κείμενο png** αποδοτικά. Ο κώδικας είναι αυτόνομος, οι εξηγήσεις καλύπτουν τόσο το “πώς” όσο και το “γιατί”, και οι συμβουλές σας κρατούν μακριά από κοινά προβλήματα.

Τι έπεται; Δοκιμάστε να αντικαταστήσετε τη λίστα PNG με έναν δυναμικό βρόχο `Directory.GetFiles`, πειραματιστείτε με διαφορετικούς αριθμούς νημάτων, ή τροφοδοτήστε την έξοδο σε αναζητήσιμο PDF. Το ίδιο μοτίβο κλιμακώνεται σε εκατοντάδες σελίδες με ελάχιστο επιπλέον κώδικα.

Έχετε ερωτήσεις ή ένα δύσκολο edge case; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}