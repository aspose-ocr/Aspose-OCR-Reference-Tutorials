---
category: general
date: 2026-02-24
description: Επεξεργαστείτε μαζικά εικόνες OCR γρήγορα με το Aspose.OCR σε C#. Μάθετε
  πώς να διαβάζετε αρχεία από φάκελο, να αναγνωρίζετε κείμενο από εικόνα και να μετατρέπετε
  την εικόνα σε κείμενο σε λίγα βήματα.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: el
og_description: Ομαδική OCR εικόνων σε C# χρησιμοποιώντας το Aspose.OCR. Αυτό το σεμινάριο
  δείχνει πώς να διαβάζετε αρχεία από φάκελο, να αναγνωρίζετε κείμενο από εικόνα και
  να μετατρέπετε την εικόνα σε κείμενο αποδοτικά.
og_title: Ομαδική OCR Εικόνων σε C# – Πλήρης Οδηγός Βήμα‑Βήμα
tags:
- C#
- OCR
- Aspose
title: Ομαδική OCR Εικόνων σε C# – Πλήρης Οδηγός για την Εξαγωγή Κειμένου
url: /el/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ομαδική OCR Εικόνων σε C# – Πλήρης Οδηγός για Εξαγωγή Κειμένου

Έχετε ποτέ χρειαστεί να **ομαδική OCR εικόνων** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν για πρώτη φορά να **εξαγωγή κειμένου από εικόνες** μαζικά. Τα καλά νέα είναι ότι με λίγες γραμμές C# και Aspose.OCR μπορείτε να μετατρέψετε έναν φάκελο γεμάτο εικόνες σε τακτικά αρχεία `.txt` σε ελάχιστο χρόνο.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: ανάγνωση αρχείων από έναν φάκελο, τροφοδότηση κάθε εικόνας στη μηχανή OCR, και τελικά **μετατροπή εικόνας σε κείμενο** αρχεία που μπορείτε να ευρετηριάσετε, να αναζητήσετε ή να τροφοδοτήσετε σε επόμενα pipelines. Στο τέλος θα έχετε μια αυτόνομη εφαρμογή console που μπορείτε να ενσωματώσετε σε οποιαδήποτε λύση .NET.

## Τι Θα Χρειαστεί

- **.NET 6+** (το παράδειγμα μεταγλωττίζεται με .NET 6, αλλά οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- **Aspose.OCR** πακέτο NuGet (`Install-Package Aspose.OCR`)
- Ένας φάκελος με αρχεία εικόνας (`.png`, `.jpg`, κλπ.) που θέλετε να επεξεργαστείτε
- Visual Studio, Rider ή τον αγαπημένο σας επεξεργαστή

Δεν απαιτούνται πρόσθετα αρχεία ρυθμίσεων, καμία εξωτερική υπηρεσία—απλώς καθαρός κώδικας C# που εκτελείται τοπικά.

## Ομαδική OCR Εικόνων – Ρύθμιση του Έργου

Πρώτα, δημιουργήστε ένα νέο έργο console:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

### Ανάγνωση Αρχείων από Κατάλογο

Πρέπει να πούμε στην εφαρμογή μας πού βρίσκονται οι εικόνες προέλευσης και πού πρέπει να αποθηκευτούν τα παραγόμενα αρχεία κειμένου. Η χρήση του `System.IO` το κάνει εύκολο.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Γιατί είναι σημαντικό αυτό το βήμα:** Αν ο φάκελος εξόδου δεν υπάρχει, το πρόγραμμα θα πετάξει εξαίρεση όταν προσπαθήσει να γράψει ένα αρχείο `.txt`. Η `CreateDirectory` είναι ιδεομετρική—δεν κάνει τίποτα αν ο φάκελος υπάρχει ήδη, έτσι είναι ασφαλές να την καλέσετε σε κάθε εκτέλεση.

### Αναγνώριση Κειμένου από Εικόνα και Μετατροπή Εικόνας σε Κείμενο

Τώρα εκκινούμε τη μηχανή OCR και επαναλαμβάνουμε για κάθε αρχείο που βρήκαμε. Η επανάληψη χρησιμοποιεί το `Directory.GetFiles` με μπαλαντέρ (`*.*`) ώστε να πιάσει *όλα* τα αρχεία, αλλά μπορείτε να περιορίσετε το φίλτρο σε `*.png` ή `*.jpg` αν προτιμάτε.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**Τι συμβαίνει εδώ;**  
- `ocrEngine.RecognizeImage(imagePath)` διαβάζει το bitmap, εκτελεί τον αλγόριθμο OCR και επιστρέφει ένα αντικείμενο `OcrResult`.  
- `ocrResult.Text` περιέχει την αναπαράσταση plain‑text όλων όσων η μηχανή μπόρεσε να διαβάσει.  
- `File.WriteAllText` δημιουργεί ένα νέο αρχείο (ή αντικαθιστά υπάρχον) με το εξαγόμενο κείμενο.

Αυτή είναι ολόκληρη η διαδικασία **ομαδικής OCR εικόνων** σε λιγότερο από 30 γραμμές κώδικα.

## Pro Συμβουλές & Ακραίες Περιπτώσεις

| Κατάσταση | Σύσταση |
|-----------|----------------|
| Οι εικόνες είναι μεγάλες ( > 5 MB ) | Κάντε προ‑κλιμάκωση σε πλάτος ~1500 px για να επιταχύνετε την αναγνώριση χωρίς να χάσετε ακρίβεια. |
| Χρειάζεστε υποστήριξη PDF | Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (π.χ., χρησιμοποιώντας `Aspose.PDF`) και μετά τη δώστε στην ίδια επανάληψη. |
| Κάποια αρχεία δεν είναι εικόνες (π.χ., `.txt`) | Προσθέστε ένα απλό φίλτρο: `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| Θέλετε πολυγλωσσική υποστήριξη | Ορίστε `ocrEngine.Language = Language.English | Language.Spanish;` πριν την επανάληψη. |
| Χρειάζεστε αναφορά προόδου | Γράψτε `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` μέσα στο foreach. |

> **Pro tip:** Τυλίξτε την κλήση OCR σε `try/catch`. Περιστασιακά μια κατεστραμμένη εικόνα μπορεί να προκαλέσει εξαίρεση στο `RecognizeImage`; η διαχείρισή της αποτρέπει τη διακοπή ολόκληρης της ομαδικής επεξεργασίας.

## Αναμενόμενο Αποτέλεσμα

Μετά το τέλος του προγράμματος, το `outputFolder` θα περιέχει ένα αρχείο `.txt` για κάθε αρχική εικόνα:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

Κάθε αρχείο περιέχει το ακατέργαστο κείμενο που εξήγαγε η μηχανή, για παράδειγμα:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

Τώρα μπορείτε να τροφοδοτήσετε αυτά τα αρχεία σε ευρετήριο αναζήτησης, να εκτελέσετε ανάλυση συναισθήματος, ή απλώς να τα αρχειοθετήσετε για συμμόρφωση.

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό σε Linux;**  
A: Απόλυτα. Η Aspose.OCR είναι cross‑platform, και τα APIs `System.IO` που χρησιμοποιούνται εδώ είναι OS‑agnostic. Απλώς προσαρμόστε τις διαδρομές φακέλων (`/home/user/images`).

**Q: Τι γίνεται αν χρειαστεί να **διαβάσω αρχεία από κατάλογο** επαναληπτικά;**  
A: Αλλάξτε το `SearchOption.TopDirectoryOnly` σε `SearchOption.AllDirectories`. Να είστε προσεκτικοί με ζητήματα δικαιωμάτων σε πιο βαθιούς φακέλους.

**Q: Πόσο ακριβής είναι η OCR;**  
A: Η ακρίβεια εξαρτάται από την ποιότητα της εικόνας, τη γραμματοσειρά και τη γλώσσα. Για καλύτερα αποτελέσματα, χρησιμοποιήστε σαρώσεις υψηλής ανάλυσης και καθαρά φόντα. Μπορείτε επίσης να ρυθμίσετε το `ocrEngine.Config` για ενεργοποίηση διόρθωσης κλίσης ή μείωσης θορύβου.

## Συμπέρασμα

Μόλις μάθατε πώς να **ομαδοποιήσετε OCR εικόνων** σε C# χρησιμοποιώντας Aspose.OCR, από την ανάγνωση αρχείων από κατάλογο μέχρι την **αναγνώριση κειμένου από εικόνα** και τελικά την **μετατροπή εικόνας σε κείμενο** αρχεία που μπορείτε να αποθηκεύσετε ή να επεξεργαστείτε περαιτέρω. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω πρέπει να λειτουργεί αμέσως, και η ενότητα συμβουλών σας δίνει ένα roadmap για κλιμάκωση ή προσαρμογή της λύσης.

Επόμενα βήματα; Δοκιμάστε να προσθέσετε ένα απλό UI με WinForms ή WPF, να ενσωματώσετε το αποτέλεσμα με Azure Cognitive Search, ή να πειραματιστείτε με άλλες γλώσσες που υποστηρίζει η Aspose.OCR. Ο ουρανός είναι το όριο μόλις κατακτήσετε τον βασικό βρόχο.

Καλό κώδικα, και εύχομαι τα OCR batch σας να είναι χωρίς σφάλματα!  

![Διάγραμμα της διαδικασίας ομαδικής OCR εικόνων](batch-ocr-images-diagram.png "Ροή εργασίας ομαδικής OCR εικόνων")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}