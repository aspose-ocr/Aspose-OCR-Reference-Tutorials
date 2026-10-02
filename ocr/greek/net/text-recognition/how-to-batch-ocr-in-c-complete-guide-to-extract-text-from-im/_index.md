---
category: general
date: 2026-02-20
description: Πώς να εκτελέσετε ομαδική OCR με το Aspose OCR σε C#. Μάθετε την ομαδική
  εξαγωγή κειμένου, δημιουργήστε μηχανή OCR και εξάγετε κείμενο από εικόνες αποδοτικά.
draft: false
keywords:
- how to batch OCR
- extract text from images
- c# ocr engine
- batch text extraction
- create OCR engine
language: el
og_description: Πώς να κάνετε ομαδική OCR σε C# εξηγείται. Δημιουργήστε μηχανή OCR,
  εκτελέστε ομαδική εξαγωγή κειμένου και εξάγετε κείμενο από εικόνες με το Aspose.
og_title: Πώς να κάνετε μαζική OCR σε C# – Οδηγός βήμα‑βήμα
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε ομαδική OCR σε C# – Πλήρης οδηγός για την εξαγωγή κειμένου από
  εικόνες
url: /el/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# – Πλήρης Οδηγός για Εξαγωγή Κειμένου από Εικόνες

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε μια δέκαδα σαρωμένων αποδείξεων χωρίς να γράψετε ξεχωριστό πρόγραμμα για κάθε αρχείο; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα η ανάγκη για **εξαγωγή κειμένου από εικόνες** γρήγορα και αξιόπιστα αποτελεί καθημερινό πρόβλημα.  

Τα καλά νέα; Με το `OcrEngine` της Aspose μπορείτε να δημιουργήσετε μια **c# OCR engine** μία φορά, να της δώσετε μια λίστα αρχείων και να αφήσετε τη βιβλιοθήκη να κάνει το σκληρό έργο. Αυτό το tutorial σας δείχνει **πώς να κάνετε batch OCR** βήμα‑βήμα, εξηγεί γιατί κάθε μέρος είναι σημαντικό και καλύπτει ακόμη και μερικές ειδικές περιπτώσεις που μπορεί να συναντήσετε.

Στα επόμενα λεπτά θα μάθετε πώς να:

* **Δημιουργείτε αντικείμενα τύπου OCR engine** σωστά,
* συναρμολογείτε μια συλλογή αρχείων για **batch εξαγωγή κειμένου**,
* εκτελείτε τη δουλειά batch και προεπισκόπηση των πρώτων 50 χαρακτήρων κάθε αποτελέσματος,
* αντιμετωπίζετε κοινά προβλήματα όπως ελλιπή αρχεία ή κενά αποτελέσματα.

Δεν υπάρχουν εξωτερικοί σύνδεσμοι τεκμηρίωσης — όλα όσα χρειάζεστε είναι εδώ. Ας ξεκινήσουμε.

---

## Πώς να κάνετε Batch OCR – Δημιουργία του OCR Engine

Πρώτα απ' όλα: χρειάζεστε μια παρουσία του **c# OCR engine** που θα διαβάσει πραγματικά τα pixel. Σκεφτείτε το ως τον εγκέφαλο πίσω από τη λειτουργία.  

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine – this is the core of how to batch OCR
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the code lives after we’ve created the engine
```

> **Συμβουλή:** Η δημιουργία του engine μία φορά και η επαναχρησιμοποίησή του για πολλά αρχεία είναι πολύ πιο αποδοτική από το να δημιουργείτε νέο αντικείμενο ανά εικόνα. Μειώνει την κατανάλωση μνήμης και επιταχύνει τη συνολική **batch εξαγωγή κειμένου**.

---

## Προετοιμασία της Λίστας Εικόνων για Batch Εξαγωγή Κειμένου

Τώρα που υπάρχει το engine, πρέπει να του πούμε **τι** θα επεξεργαστεί. Η πιο απλή προσέγγιση είναι μια `List<string>` που περιέχει απόλυτες ή σχετικές διαδρομές.  

```csharp
        // Step 2: Build a list of image files – this is where we define the batch
        var imageFiles = new List<string>
        {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        };
```

Αν παίρνετε τα ονόματα αρχείων από έναν φάκελο, μια μιά‑γραμμή όπως `Directory.GetFiles("YOUR_DIRECTORY", "*.*", SearchOption.TopDirectoryOnly)` λειτουργεί εξίσου καλά.  

> **Γιατί είναι σημαντικό:** Η παροχή μιας έτοιμης συλλογής επιτρέπει στο **c# OCR engine** να επαναλαμβάνει εσωτερικά, που αποτελεί την ουσία του **πώς να κάνετε batch OCR** χωρίς χειροκίνητους βρόχους.

---

## Εκτέλεση του Batch Recognition και Προεπισκόπηση Αποτελεσμάτων

Η πραγματική μαγεία συμβαίνει όταν καλείτε το `RecognizeBatch`. Η μέθοδος δέχεται τη συλλογή αρχείων και μια callback που λαμβάνει κάθε `OcrResult`.  

```csharp
        // Step 3: Execute batch recognition – this is the core of how to batch OCR
        ocrEngine.RecognizeBatch(imageFiles, result =>
        {
            // Show the source file name and the first 50 characters of the recognized text
            string preview = result.Text.Length > 50 ? result.Text.Substring(0, 50) + "..." : result.Text;
            Console.WriteLine($"{result.SourceFile}: {preview}");
        });
    }
}
```

### Αναμενόμενη έξοδος στην κονσόλα

```
YOUR_DIRECTORY/doc1.png: Invoice #12345 Date: 2024-01-15 Total: $...
YOUR_DIRECTORY/doc2.jpg: Meeting Notes – 10/02/2024 • Attendees:...
YOUR_DIRECTORY/doc3.tif: Shipping Manifest – Batch 07 – Items:
```

Το παραπάνω απόσπασμα τυπώνει μια σύντομη προεπισκόπηση, χρήσιμη όταν έχετε δεκάδες αρχεία και θέλετε απλώς να επαληθεύσετε ότι το OCR εντοπίζει κείμενο.

![προεπισκόπηση batch OCR](/images/batch-ocr-preview.png "Εικονογράφηση του πώς προβάλλονται τα αποτελέσματα batch OCR στην κονσόλα")

> **Ειδική περίπτωση:** Αν το `result.Text` είναι κενό, η callback εξακολουθεί να εκτελείται. Μπορείτε να καταγράψετε μια προειδοποίηση ή να μετακινήσετε το αρχείο σε φάκελο “needs‑review”. Αυτό εξασφαλίζει ότι δεν χάνετε δεδομένα σιωπηρά κατά τη **batch εξαγωγή κειμένου**.

---

## Βελτιστοποίηση του c# OCR Engine για Καλύτερη Ακρίβεια

Οι προεπιλεγμένες ρυθμίσεις λειτουργούν για πολλές καθαρές σαρώσεις, αλλά μπορείτε να βελτιώσετε τα αποτελέσματα με μερικές προσαρμογές:

| Ρύθμιση | Τι κάνει | Πότε να τη χρησιμοποιήσετε |
|---------|----------|----------------------------|
| `ocrEngine.Language = Language.English;` | Εξαναγκάζει το λεξικό Αγγλικών, μειώνοντας τα ψευδώς θετικά. | Κυρίως αγγλικά έγγραφα. |
| `ocrEngine.Config.PageSegmentationMode = PageSegMode.Auto;` | Αφήνει το engine να μαντέψει τη διάταξη. | Μικτές διατάξεις (πίνακες + παραγράφους). |
| `ocrEngine.Config.Dpi = 300;` | Βελτιώνει την αναγνώριση σε εικόνες χαμηλής ανάλυσης. | Σαρώσεις κάτω από 200 dpi. |

Προσθέστε αυτές τις γραμμές **μετά** τη δημιουργία του engine αλλά **πριν** καλέσετε το `RecognizeBatch`:

```csharp
        ocrEngine.Language = Language.English;
        ocrEngine.Config.PageSegmentationMode = PageSegMode.Auto;
        ocrEngine.Config.Dpi = 300;
```

---

## Διαχείριση Ελλιπών Αρχείων και Καταγραφή (Προαιρετικό αλλά Συνιστώμενο)

Όταν επεξεργάζεστε έναν μεγάλο φάκελο, κάποια αρχεία μπορεί να λείπουν ή να είναι κατεστραμμένα. Τυλίξτε την κλήση batch σε try‑catch και καταγράψτε τις προβληματικές διαδρομές:

```csharp
        try
        {
            ocrEngine.RecognizeBatch(imageFiles, result =>
            {
                // Same preview logic as before
                string preview = result.Text.Length > 50 ? result.Text.Substring(0, 50) + "..." : result.Text;
                Console.WriteLine($"{result.SourceFile}: {preview}");
            });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing batch: {ex.Message}");
        }
```

Αυτό το αμυντικό μοτίβο αποτρέπει το **batch OCR** να καταρρεύσει στη μέση, κάτι που είναι ιδιαίτερα σημαντικό σε παραγωγικές γραμμές.

---

## Ανακεφαλαίωση Ό,τι Καλύψαμε

* **Δημιουργία OCR engine** – μια μοναδική παρουσία `OcrEngine` είναι η ραχοκοκαλιά του **πώς να κάνετε batch OCR**.  
* **Batch εξαγωγή κειμένου** – δώστε μια `List<string>` με διαδρομές εικόνων στο `RecognizeBatch`.  
* **Προεπισκόπηση αποτελεσμάτων** – η callback σας επιτρέπει να δείτε τους πρώτους 50 χαρακτήρες, επιβεβαιώνοντας την επιτυχία.  
* **Βελτιστοποίηση ρυθμίσεων** – γλώσσα, DPI και τμηματοποίηση βελτιώνουν την ακρίβεια για διαφορετικές σαρώσεις.  
* **Διαχείριση σφαλμάτων** – τυλίξτε την κλήση batch για να διατηρήσετε τη διαδικασία ανθεκτική.

---

## Τι Ακολουθεί; Εξερεύνηση Πιο Προχωρημένων Σεναρίων

Τώρα που ξέρετε **πώς να κάνετε batch OCR**, ίσως θέλετε να:

* **Αποθηκεύσετε κάθε αποτέλεσμα σε ξεχωριστό αρχείο `.txt`** – ιδανικό για επόμενη ευρετηρίαση.  
* **Συνδυάσετε OCR με δημιουργία PDF** – μετατρέψτε σαρωμένες σελίδες σε αναζητήσιμα PDF.  
* **Παραλληλοποιήσετε το batch** – για τεράστιους όγκους εργασίας, τρέξτε πολλαπλά `OcrEngine` σε ξεχωριστά νήματα (προσέξτε τα όρια άδειας).  

Όλες αυτές οι επεκτάσεις εξακολουθούν να βασίζονται στο ίδιο **c# OCR engine** που μόλις ρυθμίσατε, οπότε βρίσκεστε ήδη σε σταθερό έδαφος.

---

### TL;DR

Μάθατε **πώς να κάνετε batch OCR** σε C# χρησιμοποιώντας το `OcrEngine` της Aspose. Δημιουργώντας το engine μία φορά, προετοιμάζοντας μια λίστα αρχείων εικόνας και καλώντας το `RecognizeBatch` με μια απλή callback προεπισκόπηση, μπορείτε αποδοτικά να **εξάγετε κείμενο από εικόνες** σε κλίμακα. Ρυθμίστε τις παραμέτρους του engine για μεγαλύτερη ακρίβεια, προσθέστε διαχείριση σφαλμάτων, και έχετε μια παραγωγική γραμμή **batch εξαγωγής κειμένου**.

Καλή προγραμματιστική, και εύχομαι οι OCR εκτελέσεις σας να είναι γρήγορες και χωρίς σφάλματα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}