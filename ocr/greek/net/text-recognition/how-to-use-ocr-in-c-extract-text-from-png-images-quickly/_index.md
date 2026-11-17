---
category: general
date: 2026-03-29
description: Πώς να χρησιμοποιήσετε OCR με το Aspose για την εξαγωγή κειμένου από
  αρχεία PNG και τη μετατροπή εικόνων σε κείμενο. Μάθετε βήμα‑βήμα ασύγχρονο OCR σε
  C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: el
og_description: Πώς να χρησιμοποιήσετε OCR με το Aspose σε C# για την εξαγωγή κειμένου
  από αρχεία PNG. Αυτός ο οδηγός σας καθοδηγεί μέσω του ασύγχρονου OCR, του κώδικα
  και των συμβουλών.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από εικόνες PNG
tags:
- OCR
- C#
- Aspose
title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή κειμένου από εικόνες PNG γρήγορα
url: /el/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε C# – Εξαγωγή Κειμένου από Εικόνες PNG Γρήγορα

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να εξάγετε κείμενο από μερικά στιγμιότυπα PNG; Ίσως έχετε σαρωμένες αποδείξεις, τιμολόγια ή προεπισκοπήσεις UI και χρειάζεστε αυτό το κείμενο σε μορφή που μπορεί να αναζητηθεί. Τα καλά νέα; Με το Aspose.OCR μπορείτε να μετατρέψετε εικόνες σε κείμενο με λίγες μόνο γραμμές ασύγχρονου κώδικα C#.

Σε αυτό το tutorial θα σας δείξουμε ακριβώς πώς να εξάγετε κείμενο από αρχεία PNG, θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό και θα σας δώσουμε ένα έτοιμο προς εκτέλεση πρόγραμμα που εκτυπώνει το αναγνωρισμένο κείμενο για κάθε σελίδα. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από εικόνες** χωρίς να ψάχνετε στην τεκμηρίωση.

## Τι Θα Μάθετε

- Εγκαταστήστε και αναφέρετε το πακέτο NuGet Aspose.OCR.  
- Αρχικοποιήστε τη μηχανή OCR και ορίστε τη γλώσσα (Αγγλικά σε αυτό το παράδειγμα).  
- Παρέχετε έναν πίνακα PNG αρχείων στη μέθοδο `RecognizeImagesAsync` για γρήγορη, μη‑αποκλειστική επεξεργασία.  
- Διατρέξτε τα αντικείμενα `OcrResult` και εξάγετε τις συμβολοσειρές.  

Καμία εξωτερική υπηρεσία, χωρίς περίπλοκα callbacks—απλός, ασύγχρονος C# που λειτουργεί σε .NET 6+.

---

## Προαπαιτούμενα

| Requirement | Reason |
|-------------|--------|
| .NET 6 SDK (or later) | Μοντέρνα χαρακτηριστικά της γλώσσας όπως το `async Main`. |
| Visual Studio 2022 or VS Code | IDE για τη μεταγλώττιση και εκτέλεση του κώδικα. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Παρέχει την κλάση `OcrEngine` που χρησιμοποιείται στο παράδειγμα. |
| A few PNG images (`page1.png`, `page2.png`, …) | Αρχεία εισόδου για τη διαδικασία OCR. |

Αν έχετε ήδη ένα .NET project, απλώς εκτελέστε `dotnet add package Aspose.OCR`. Διαφορετικά, δημιουργήστε μια νέα εφαρμογή κονσόλας με `dotnet new console -n OcrDemo`.

## Βήμα 1: Εγκατάσταση Aspose.OCR και Ρύθμιση του Έργου

Πρώτα, προσθέστε τη βιβλιοθήκη OCR στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

Γιατί είναι σημαντικό: Το Aspose.OCR περιλαμβάνει τη φυσική μηχανή OCR, τα πακέτα γλωσσών και ένα απλό API. Με την προσθήκη του μέσω NuGet εξασφαλίζετε συμβατότητα εκδόσεων και αυτόματες ενημερώσεις.

---

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR και Επιλογή Γλώσσας

Η μηχανή πρέπει να γνωρίζει ποια γλώσσα θα αναζητήσει. Τα Αγγλικά είναι τα πιο κοινά, αλλά μπορείτε να αλλάξετε σε `Language.Spanish`, `Language.French`, κλπ.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Συμβουλή:** Πάντα ορίζετε ρητά τη γλώσσα· η χρήση της προεπιλογής μπορεί να μειώσει την ακρίβεια και να αυξήσει το χρόνο επεξεργασίας.

---

## Βήμα 3: Προετοιμασία της Λίστας Αρχείων PNG

Μπορείτε να δώσετε ένα μόνο αρχείο ή έναν πίνακα. Η παροχή ενός πίνακα επιτρέπει στη μηχανή να τα επεξεργάζεται σε παρτίδες ασύγχρονα, κάτι που είναι ιδανικό για μερικές σελίδες.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Αν οι εικόνες σας βρίσκονται σε υποφάκελο, απλώς προσθέστε το σχετικό μονοπάτι (`"images/page1.png"`). Η μηχανή θα ρίξει ένα σαφές `FileNotFoundException` αν το μονοπάτι είναι λάθος—για αυτό ελέγξτε ξανά τα ονόματα αρχείων.

---

## Βήμα 4: Εκτέλεση Ασύγχρονης OCR σε Όλες τις Εικόνες

Η μέθοδος `RecognizeImagesAsync` επιστρέφει έναν πίνακα `OcrResult`. Επειδή είναι async, το UI (ή η κονσόλα) παραμένει ανταποκριτικό ενώ το OCR εκτελείται στο παρασκήνιο.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Γιατί async;**  
Αν ενσωματώνετε OCR σε web API ή εφαρμογή desktop, δεν θέλετε το νήμα να μπλοκάρει ενώ η μηχανή σαρώνει κάθε pixel. Το `await` απελευθερώνει το νήμα πίσω στην ομάδα νημάτων, βελτιώνοντας την κλιμακωσιμότητα.

---

## Βήμα 5: Εμφάνιση του Εξαγόμενου Κειμένου για Κάθε Σελίδα

Τώρα που έχουμε τα αποτελέσματα, διατρέξτε τα και εκτυπώστε το αναγνωρισμένο κείμενο. Η ιδιότητα `Text` περιέχει το απλό κείμενο εξόδου, έτοιμο για περαιτέρω επεξεργασία (π.χ., αποθήκευση σε βάση δεδομένων).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Αναμενόμενη Έξοδος

Υποθέτοντας ότι το `page1.png` περιέχει “Invoice #12345” και το `page2.png` περιέχει “Total: $89.99”, θα δείτε κάτι όπως:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Αν το OCR δεν εντοπίσει κείμενο, η ιδιότητα `Text` θα είναι κενή συμβολοσειρά—χειριστείτε αυτήν την περίπτωση στον κώδικα παραγωγής ελέγχοντας `string.IsNullOrWhiteSpace`.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει όλες τις οδηγίες using, το async `Main`, και σχόλια που διευκρινίζουν κάθε βήμα.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Αποθηκεύστε το αρχείο, τοποθετήστε τα PNG δίπλα στο εκτελέσιμο (ή προσαρμόστε τα μονοπάτια), και εκτελέστε:

```bash
dotnet run
```

Θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι έχετε μετατρέψει επιτυχώς **εικόνες σε κείμενο**.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

| Situation | What to Do |
|-----------|------------|
| **PNG χαμηλής ανάλυσης** | Αυξήστε το `ocrEngine.ImageProcessingOptions.Dpi` πριν από την αναγνώριση. |
| **Πολλαπλές γλώσσες** | Ορίστε `ocrEngine.Language = Language.English | Language.Spanish;` (bitwise OR). |
| **Μεγάλη παρτίδα (εκατοντάδες αρχεία)** | Επεξεργαστείτε σε τμήματα (π.χ., 20 αρχεία ανά κλήση `RecognizeImagesAsync`) για να αποφύγετε αυξήσεις μνήμης. |
| **Απαιτείται το σκορ εμπιστοσύνης** | Χρησιμοποιήστε `ocrResults[i].Confidence` (float μεταξύ 0 και 1) για να φιλτράρετε αποτελέσματα χαμηλής ποιότητας. |

Αυτές οι ρυθμίσεις κρατούν την αλυσίδα OCR σας ανθεκτική, ειδικά όταν μεταβαίνετε από μια demo σε παραγωγή.

---

## Μπόνους: Αποθήκευση των Αποτελεσμάτων σε Αρχείο Κειμένου

Αν προτιμάτε ένα μόνιμο αντίγραφο αντί για έξοδο στην κονσόλα, προσθέστε έναν μικρό βοηθό:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Τώρα έχετε ένα μόνο αρχείο που **εξάγει κείμενο από εικόνες** για επεξεργασία downstream—ιδανικό για ευρετηρίαση, αναζήτηση ή τροφοδοσία σε μοντέλο γλώσσας.

---

## Συμπέρασμα

Διασχίσαμε **πώς να χρησιμοποιήσετε OCR** σε C# με το Aspose για **εξαγωγή κειμένου από αρχεία PNG** και **μετατροπή εικόνων σε κείμενο** αποδοτικά. Η ασύγχρονη προσέγγιση εξασφαλίζει ότι η εφαρμογή σας παραμένει ανταποκριτική, ενώ το απλό API διατηρεί τον κώδικα ευανάγνωστο και συντηρήσιμο.

Δοκιμάστε το με τα δικά σας έγγραφα, πειραματιστείτε με διαφορετικές γλώσσες και ίσως ακόμη συνδέσετε το αποτέλεσμα με ευρετήριο αναζήτησης ή υπηρεσία περίληψης. Ο ουρανός είναι το όριο όταν μπορείτε αξιόπιστα να μετατρέψετε εικόνες σε αναζητήσιμες συμβολοσειρές.

### Επόμενα Βήματα & Σχετικά Θέματα

- **Εξαγωγή κειμένου από εικόνες** σε άλλες μορφές (JPEG, TIFF) – απλώς αλλάξτε τις επεκτάσεις αρχείων.  
- **Επεξεργασία σε παρτίδες με Parallel.ForEach** για τεράστιες εργασίες.  
- **Καθαρισμός μετά το OCR** χρησιμοποιώντας κανονικές εκφράσεις για την κανονικοποίηση ημερομηνιών, ποσών ή ταυτοτήτων.  
- **Ενσωμάτωση με Azure Cognitive Services** αν χρειάζεστε OCR βασισμένο στο cloud με επιπλέον δυνατότητες.  

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε προβλήματα, ή να μοιραστείτε πώς επεκτείνατε αυτή τη βασική ροή. Καλή προγραμματιστική!   (Image: ![Στιγμιότυπο αποτελέσματος OCR που δείχνει το εξαγόμενο κείμενο](/images/ocr-result.png){.align-center alt="παράδειγμα εξόδου OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}