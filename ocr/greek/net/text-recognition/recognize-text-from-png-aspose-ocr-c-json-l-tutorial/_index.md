---
category: general
date: 2026-03-26
description: Αναγνωρίστε κείμενο από PNG και εξάγετε δεδομένα από απόδειξη χρησιμοποιώντας
  Aspose OCR σε C#. Μετατρέψτε την εικόνα σε JSON‑L και επεξεργαστείτε την απόδειξη
  με OCR σε ένα πλήρες παράδειγμα.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: el
og_description: αναγνωρίστε κείμενο από png και μετατρέψτε τις αποδείξεις σε JSON‑L
  με το Aspose OCR σε C#. Πλήρης κώδικας βήμα‑βήμα και συμβουλές.
og_title: αναγνώριση κειμένου από png – Οδηγός Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Αναγνώριση κειμένου από PNG – Οδηγός Aspose OCR C# JSON‑L
url: /el/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από png – Πλήρης Οδηγός Aspose OCR C# 

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από png** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας έδινε καθαρά, γραμμή‑με‑γραμμή αποτελέσματα; Δεν είστε μόνοι. Σε πολλές εφαρμογές μικρών επιχειρήσεων η απόδειξη είναι αποθηκευμένη ως εικόνα PNG, και η εξαγωγή του ποσού, της ημερομηνίας ή του ονόματος του εμπόρου αποτελεί καθημερινό πρόβλημα.  

Τα καλά νέα; Με μερικές γραμμές C# και τη βιβλιοθήκη **Aspose OCR** μπορείτε να **εξάγετε κείμενο από απόδειξη**, στη συνέχεια **μετατρέψετε την εικόνα σε jsonl** για downstream analytics. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία — φόρτωση ενός PNG, εκτέλεση OCR, και εγγραφή κάθε γραμμής σε αρχείο JSON‑L — ώστε να μπορείτε να **επεξεργαστείτε την απόδειξη με OCR** αμέσως.

Θα καλύψουμε όλα όσα χρειάζεστε: τα απαιτούμενα πακέτα NuGet, ένα πλήρες εκτελέσιμο πρόγραμμα, εξηγήσεις για το γιατί κάθε βήμα είναι σημαντικό, και μια σειρά πρακτικών συμβουλών που θα εκτιμήσετε όταν οι αποδείξεις γίνονται ακατάστατες. Δεν απαιτείται εξωτερική τεκμηρίωση· απλώς αντιγράψτε‑επικολλήστε, εκτελέστε και προσαρμόστε.

---

## Τι Θα Μάθετε

- Πώς να **αναγνωρίσετε κείμενο από png** χρησιμοποιώντας `Aspose.OCR`.
- Πώς να **εξάγετε κείμενο από απόδειξη** από αντικείμενα γραμμής και να καταγράψετε τα confidence scores.
- Πώς να **μετατρέψετε την εικόνα σε jsonl** ώστε κάθε γραμμή OCR να γίνεται ξεχωριστό αντικείμενο JSON.
- Πώς να **επεξεργαστείτε την απόδειξη με OCR** από άκρη σε άκρη, αντιμετωπίζοντας ειδικές περιπτώσεις όπως κενές εικόνες ή γραμμές χαμηλής εμπιστοσύνης.
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων OCR και τη βελτίωση της ακρίβειας.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).
- Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε.
- Ένα έγκυρο άδεια Aspose OCR (μπορείτε να ξεκινήσετε με δωρεάν προσωρινή άδεια από το Aspose.com).
- Ένα δείγμα απόδειξης αποθηκευμένο ως `receipt.png` σε φάκελο που ελέγχετε.

---

## Βήμα 1: Αναγνώριση κειμένου από png με Aspose OCR

Το πρώτο που χρειαζόμαστε είναι ένα αρχικοποιημένο `OcrEngine`. Αυτό το αντικείμενο περιέχει τις ρυθμίσεις της μηχανής OCR (γλώσσα, λειτουργία ανίχνευσης κ.λπ.). Από προεπιλογή χρησιμοποιεί την Αγγλική και ανιχνεύει αυτόματα τη διάταξη της σελίδας, κάτι που λειτουργεί καλά για τις περισσότερες αποδείξεις.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Γιατί είναι σημαντικό:**  
`OcrEngine` είναι το κύριο στοιχείο που κάνει τη δουλειά· η δημιουργία του μία φορά και η επαναχρησιμοποίησή του σε πολλές εικόνες μειώνει την κατανάλωση μνήμης. Εάν χρειάζεστε διαφορετική γλώσσα (π.χ., αποδείξεις στα Ισπανικά), μπορείτε να ορίσετε `ocrEngine.Language = OcrLanguage.Spanish;` πριν καλέσετε το `Recognize`.

---

## Βήμα 2: Εξαγωγή κειμένου από γραμμές απόδειξης

`OcrResult` περιέχει μια συλλογή που ονομάζεται `Lines`. Κάθε γραμμή περιέχει το ακατέργαστο κείμενο και ένα confidence score (0‑100). Η εξαγωγή τους σας δίνει λεπτομερή έλεγχο — μπορείτε να απορρίψετε γραμμές χαμηλής εμπιστοσύνης ή να τις επισημάνετε για χειροκίνητη ανασκόπηση.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Γιατί κάνουμε escape το JSON:**  
Το κείμενο της απόδειξης μπορεί να περιέχει εισαγωγικά (`"`) ή ανάστροφες καθέτους (`\`) που θα σπάσουν μια αφελή συμβολοσειρά JSON. Η μέθοδος `EscapeJson` εγγυάται μια έγκυρη γραμμή JSON.

**Πώς φαίνεται η έξοδος:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Κάθε γραμμή είναι ξεχωριστή εγγραφή, ιδανική για ροή σε data lake ή για τροφοδότηση μοντέλου μηχανικής μάθησης.

---

## Βήμα 3: Μετατροπή εικόνας σε JSONL – διαχείριση ειδικών περιπτώσεων

Όταν επεξεργάζεστε μια παρτίδα αποδείξεων, μερικές εικόνες μπορεί να είναι κενές, κατεστραμμένες ή να έχουν εξαιρετικά χαμηλά confidence scores. Ας κάνουμε τη ροή πιο ανθεκτική.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Γιατί φιλτράρουμε:**  
Αποδείξεις εκτυπωμένες σε ξεθωριασμένο χαρτί μπορούν να παράγουν αχρείαστους χαρακτήρες με χαμηλή εμπιστοσύνη. Η αφαίρεση όλων κάτω από 80 % συνήθως αφαιρεί το θόρυβο ενώ διατηρεί τα χρήσιμα δεδομένα.

---

## Βήμα 4: Επεξεργασία απόδειξης με OCR – παράδειγμα από άκρη σε άκρη

Συνδυάζοντας όλα, εδώ είναι το **πλήρες, έτοιμο‑για‑εκτέλεση** πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το αρχείο PNG σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Εκτέλεση του κώδικα:**  
1. Ανοίξτε ένα τερματικό στο φάκελο του έργου.  
2. `dotnet add package Aspose.OCR` – εγκαθιστά τη βιβλιοθήκη.  
3. `dotnet run` – θα πρέπει να δείτε το μήνυμα επιτυχίας και να εμφανιστεί ένα αρχείο `receipt.jsonl`.

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο JSON διαχωρισμένο ανά γραμμή, όπου κάθε γραμμή αντιστοιχεί σε μια γραμμή απόδειξης, πλήρης με confidence scores. Τώρα μπορείτε να διοχετεύσετε αυτό το αρχείο σε Power BI, Elastic ή οποιοδήποτε εργαλείο analytics που καταλαβαίνει JSON‑L.

---

## Συνηθισμένα Προβλήματα & Επαγγελματικές Συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Γρήγορη λύση |
|----------|------------------|--------------|
| **Κενή έξοδος** | Λάθος διαδρομή εικόνας ή το αρχείο δεν είναι PNG. | Ελέγξτε ξανά τη διαδρομή, χρησιμοποιήστε `File.Exists(imagePath)`. |
| **Αχρείες χαρακτήρες** | Χαμηλό DPI ή πολύ συμπιεσμένο PNG. | Χρησιμοποιήστε σάρωση τουλάχιστον 300 dpi· αποφύγετε την έντονη συμπίεση JPEG. |
| **Πάρα πολλές γραμμές χαμηλής εμπιστοσύνης** | Απόδειξη εκτυπωμένη σε θερμικό χαρτί με ξεθώριασμα. | Αυξήστε το όριο `minConfidence` ή προεπεξεργαστείτε την εικόνα (αντίθεση/κατώφλι). |
| **Σφάλματα ανάλυσης JSON** | Μη escaped εισαγωγικά στο κείμενο της απόδειξης. | Διατηρήστε τη βοηθητική `EscapeJson` ή μεταβείτε σε `System.Text.Json` για αξιόπιστη σειριοποίηση. |

**Συμβουλή επαγγελματία:** Εάν χρειάζεται να εξάγετε συγκεκριμένα πεδία (π.χ., το συνολικό ποσό), εκτελέστε ένα απλό regex σε κάθε `line.Text` αφού έχετε το αρχείο JSON‑L. Αυτό διατηρεί το OCR ξεχωριστό από τη λογική της επιχείρησης και κάνει τον εντοπισμό σφαλμάτων πιο εύκολο.

---

## Επέκταση της Λύσης

- **Επεξεργασία παρτίδας:** Τυλίξτε τη λογική `Main` σε ένα `foreach` πάνω σε όλα τα αρχεία PNG σε έναν φάκελο.
- **Υποστήριξη πολλαπλών γλωσσών:** Ορίστε `ocrEngine.Language = OcrLanguage.Spanish;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν το `Recognize`.
- **Δομημένη έξοδος:** Αντί για JSON γραμμή‑με‑γραμμή, δημιουργήστε ένα αντικείμενο `Receipt` με ιδιότητες `Date`, `Merchant`, `Total`, και στη συνέχεια σειριοποιήστε το μία φορά.

Όλες αυτές οι παραλλαγές εξακολουθούν να **μετατρέπουν την εικόνα σε jsonl** στον πυρήνα, ώστε να μπορείτε να αλλάξετε τον downstream καταναλωτή χωρίς να επηρεάσετε το τμήμα OCR.

---

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **αναγνωρίζετε κείμενο από png** αρχεία χρησιμοποιώντας Aspose OCR, **εξάγετε κείμενο από απόδειξη**, και **μετατρέψετε την εικόνα σε jsonl** για εύκολη downstream επεξεργασία. Το πλήρες, αυτόνομο πρόγραμμα C# παρουσιάζει όλη τη ροή εργασίας — από τη φόρτωση ενός PNG, τη διαχείριση ειδικών περιπτώσεων, μέχρι τη δημιουργία ενός καθαρού αρχείου JSON‑L — ώστε να μπορείτε άμεσα να **επεξεργαστείτε την απόδειξη με OCR** στα δικά σας έργα.

Δοκιμάστε το με μερικά δείγματα αποδείξεων, ρυθμίστε το όριο εμπιστοσύνης, και θα δείτε πόσο γρήγορα μια θορυβώδης στοίβα εικόνων μετατρέπεται σε δομημένα δεδομένα έτοιμα για analytics. Όταν νιώσετε άνετα, εξερευνήστε την επεξεργασία παρτίδας ή προσθέστε ένα μικρό μοντέλο ML για αυτόματη ταξινόμηση κατηγοριών εξόδων.

Έχετε ερωτήσεις ή βρήκατε μια έξυπνη βελτίωση; Αφήστε ένα σχόλιο παρακάτω — καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}