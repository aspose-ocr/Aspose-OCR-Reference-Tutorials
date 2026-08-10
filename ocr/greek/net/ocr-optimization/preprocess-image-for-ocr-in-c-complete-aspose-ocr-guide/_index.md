---
category: general
date: 2026-05-31
description: Μάθετε πώς να προετοιμάζετε εικόνα για OCR σε C# με το Aspose OCR – αυτόματη
  διόρθωση κλίσης, μείωση θορύβου και εξαγωγή καθαρού κειμένου σε λίγα μόνο βήματα.
draft: false
keywords:
- preprocess image for OCR
- Aspose OCR library
- C# OCR preprocessing
- image deskew
- noise reduction
language: el
og_description: Προεπεξεργασία εικόνας για OCR σε C# χρησιμοποιώντας το Aspose OCR.
  Αυτόματη διόρθωση κλίσης, μείωση θορύβου και ανάκτηση ακριβούς κειμένου με αυτόν
  τον οδηγό βήμα‑βήμα.
og_title: Προεπεξεργασία εικόνας για OCR σε C# – Πλήρης οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to preprocess image for OCR in C# with Aspose OCR – auto‑deskew,
    denoise, and extract clean text in just a few steps.
  headline: Preprocess Image for OCR in C# – Complete Aspose OCR Guide
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: Προεπεξεργασία εικόνας για OCR σε C# – Πλήρης οδηγός Aspose OCR
url: /el/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR σε C# – Πλήρης Οδηγός Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **προεπεξεργαστείτε εικόνα για OCR** ώστε η μηχανή να διαβάζει κάθε χαρακτήρα άψογα; Δεν είστε ο μόνος. Σε πολλά πραγματικά έργα—σκεφτείτε σαρωμένες αποδείξεις, θολές φωτογραφίες ταυτότητας ή περιστραμμένα τιμολόγια—η ακατέργαστη εικόνα απλώς δεν αρκεί. Το καλό νέο; Με τη βιβλιοθήκη Aspose OCR μπορείτε να καθαρίσετε, διορθώσετε την κλίση και να αφαιρέσετε τον θόρυβο μιας εικόνας σε λίγες γραμμές κώδικα, και μετά να τη δώσετε στη μηχανή OCR για ακριβή αποτελέσματα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα C# που δείχνει ακριβώς πώς να **προεπεξεργαστείτε εικόνα για OCR** χρησιμοποιώντας τη διαδικασία προεπεξεργασίας του Aspose OCR. Στο τέλος θα καταλάβετε γιατί η αυτόματη διόρθωση κλίσης είναι σημαντική, πώς λειτουργεί η υψηλού επιπέδου μείωση θορύβου, και τι να ρυθμίσετε όταν κάτι δεν πάει όπως πρέπει. Χωρίς ασαφείς αναφορές, μόνο συγκεκριμένος κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework)
* Ένα έγκυρο άδεια Aspose OCR ή ένα προσωρινό κλειδί αξιολόγησης
* Ένα αρχείο εικόνας που χρειάζεται καθαρισμό—κατά προτίμηση μια κεκλιμένη, θορυβώδης φωτογραφία όπως *skewed_photo.jpg*
* Visual Studio, Rider ή οποιονδήποτε επεξεργαστή C# προτιμάτε

Αυτό είναι όλο. Δεν χρειάζονται επιπλέον πακέτα NuGet εκτός από **Aspose.OCR**.

## Βήμα 1: Εγκατάσταση και Αναφορά της Βιβλιοθήκης Aspose OCR

Πρώτα, προσθέστε το πακέτο NuGet Aspose OCR στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Αν εργάζεστε στο Visual Studio, μπορείτε επίσης να χρησιμοποιήσετε το UI του NuGet Package Manager. Η βιβλιοθήκη περιλαμβάνει όλες τις κλάσεις προεπεξεργασίας που θα χρειαστούμε, οπότε δεν απαιτούνται πρόσθετες εξαρτήσεις.

## Βήμα 2: Δημιουργία του OCR Engine και Φόρτωση της Εικόνας Σας

Η μηχανή είναι η καρδιά της **Aspose OCR library**. Κρατά την εικόνα, τις ρυθμίσεις και, αργότερα, παράγει το κείμενο. Δείτε πώς τη δημιουργείτε:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine and point it at the source image
OcrEngine engine = new OcrEngine
{
    Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_photo.jpg")
};
```

Παρατηρήστε ότι χρησιμοποιούμε το `ImageStream.FromFile`—αυτή η μέθοδος διαβάζει το αρχείο σε ένα stream που η μηχανή μπορεί να επεξεργαστεί. Αν έχετε ήδη την εικόνα στη μνήμη (π.χ. από ανέβασμα στο web), μπορείτε να περάσετε ένα `MemoryStream` αντί αυτού.

## Βήμα 3: Ενεργοποίηση και Ρύθμιση της Διαδικασίας Προεπεξεργασίας

Τώρα έρχεται η μαγεία που **προεπεξεργάζεται εικόνα για OCR**. Το αντικείμενο `OcrPreprocessingOptions` σας επιτρέπει να ενεργοποιήσετε διάφορα φίλτρα. Για τις περισσότερες σαρωμένες εγγραφές θα θέλετε δύο πράγματα:

| Επιλογή | Τι κάνει | Πότε να τη χρησιμοποιήσετε |
|--------|----------|----------------------------|
| `AutoDeskew` | Ανιχνεύει την περιστροφή και αυτόματα περιστρέφει την εικόνα ώστε οι γραμμές κειμένου να γίνουν οριζόντιες | Κεκλιμένες αποδείξεις, λοξές φωτογραφίες |
| `DenoiseLevel` | Μειώνει τυχαίο θόρυβο εικονοστοιχείων· `High` εφαρμόζει το ισχυρότερο φίλτρο | Σαρώσεις σε χαμηλό φωτισμό, συμπιεσμένα JPEG |

```csharp
engine.Preprocessing = new OcrPreprocessingOptions
{
    AutoDeskew = true,                       // image deskew
    DenoiseLevel = DenoiseLevel.High        // noise reduction
};
```

Γιατί να ενεργοποιήσουμε το **image deskew**; Ακόμη και λίγοι μοίρες κλίσης μπορούν να διαταράξουν τη διαχωριστική διαδικασία χαρακτήρων, οδηγώντας σε ακατάλληλη έξοδο. Ο ενσωματωμένος αλγόριθμος deskew αναλύει τη βάση του κειμένου και περιστρέφει το bitmap αναλόγως—χωρίς να χρειάζεται χειροκίνητος υπολογισμός γωνίας.

Και γιατί να αυξήσουμε τη **μείωση θορύβου**; Οι μηχανές OCR είναι ουσιαστικά συγκριτές προτύπων· τα τυχαία pixel τους μπερδεύουν. Ορίζοντας το `DenoiseLevel` σε `High` εφαρμόζεται ένα median filter που εξομαλύνει τις κηλίδες ενώ διατηρεί τις άκρες, ακριβώς ό,τι χρειάζεται για καθαρές γραμμές χαρακτήρων.

### Ρύθμιση της Διαδικασίας (Προαιρετικό)

Αν οι πηγαίες εικόνες είναι ήδη όρθιες αλλά παραμένουν θορυβώδεις, μπορείτε να απενεργοποιήσετε το `AutoDeskew` και να κρατήσετε μόνο το `DenoiseLevel`. Αντίθετα, για καθαρές, υψηλής ανάλυσης σαρώσεις μπορείτε να μειώσετε το επίπεδο θορύβου σε `Low` για να διατηρήσετε λεπτομέρειες (όπως μικρά διακριτικά).

## Βήμα 4: Εκτέλεση της Αναγνώρισης OCR

Με τη προεπεξεργασία ρυθμισμένη, μπορείτε τέλος να καλέσετε το `Recognize()`. Η μηχανή θα εφαρμόσει πρώτα τα βήματα deskew και denoise, και μετά θα περάσει το καθαρισμένο bitmap στη μηχανή OCR.

```csharp
// Perform OCR on the pre‑processed image
OcrResult result = engine.Recognize();
```

Το `OcrResult` περιέχει πολλές χρήσιμες ιδιότητες, αλλά οι περισσότεροι προγραμματιστές ενδιαφέρονται για το `result.Text`, που κρατά το απλό κείμενο που εξήχθη.

## Βήμα 5: Έξοδος και Επαλήθευση του Αναγνωρισμένου Κειμένου

Ας εκτυπώσουμε το αποτέλεσμα στην κονσόλα και επίσης να δείξουμε έναν γρήγορο έλεγχο λογικής:

```csharp
// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);

// Simple validation: ensure we got at least one character
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine("⚠️ No text detected – double‑check the image quality or preprocessing settings.");
}
else
{
    Console.WriteLine("✅ Text extraction successful!");
}
```

Το μπλοκ `if` είναι ένα μικρό παράδειγμα **C# OCR preprocessing** διαχείρισης σφαλμάτων. Σε παραγωγικό περιβάλλον πιθανότατα θα καταγράφετε τα confidence scores (`result.Confidence`) και ίσως να επιστρέφετε σε διαφορετική μηχανή αν το σκορ είναι χαμηλό.

## Πλήρες Παράδειγμα Εφαρμογής

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη κονσολική εφαρμογή που μπορείτε να τρέξετε αμέσως. Αποθηκεύστε το ως `Program.cs`, επαναφέρετε τα πακέτα NuGet και εκτελέστε.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize engine and load image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_photo.jpg")
        };

        // 2️⃣ Configure preprocessing – the core of how to preprocess image for OCR
        engine.Preprocessing = new OcrPreprocessingOptions
        {
            AutoDeskew = true,               // image deskew
            DenoiseLevel = DenoiseLevel.High // noise reduction
        };

        // 3️⃣ Run OCR on the cleaned bitmap
        OcrResult result = engine.Recognize();

        // 4️⃣ Display the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);

        // 5️⃣ Basic validation
        if (string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("⚠️ No text detected – consider adjusting preprocessing options.");
        }
        else
        {
            Console.WriteLine("✅ Extraction complete.");
        }
    }
}
```

### Αναμενόμενη Έξοδος

Αν το *skewed_photo.jpg* περιέχει τη φράση “Hello World”, θα δείτε κάτι σαν:

```
=== OCR Output ===
Hello World
✅ Extraction complete.
```

Ακόμη και αν η αρχική εικόνα ήταν περιστραμμένη 12° και γεμάτη κηλίδες, η **Aspose OCR library** θα την ευθυγραμμίσει και θα την καθαρίσει πριν από την αναγνώριση, παραδίδοντας το ίδιο καθαρό κείμενο.

## Ακραίες Περιπτώσεις & Πιθανά Προβλήματα

| Σενάριο | Τι να προσέξετε | Προτεινόμενη ρύθμιση |
|----------|-------------------|----------------------|
| **Ακραία περιστροφή (>45°)** | Το AutoDeskew μπορεί να δυσκολευτεί, επιστρέφοντας μερικώς περιστραμμένο αποτέλεσμα | Περιστρέψτε χειροκίνητα την εικόνα πρώτα χρησιμοποιώντας `System.Drawing` ή `ImageSharp` |
| **Πολύ χαμηλή αντίθεση** | Η μόνο μείωση θορύβου δεν βελτιώνει την αναγνωσιμότητα | Αυξήστε την αντίθεση με `engine.Preprocessing.Contrast = 1.5f` (διαθέσιμο σε νεότερες εκδόσεις) |
| **Χρωματικό κείμενο σε χρωματικό φόντο** | Το OCR μπορεί να παρερμηνεύσει τα χρώματα ως θόρυβο | Μετατρέψτε σε γκρι κλίμακα: `engine.Preprocessing.ConvertToGrayscale = true` |
| **Μεγάλα PDF χωρισμένα σε σελίδες** | Η χρήση μνήμης αυξάνεται | Επεξεργαστείτε τις σελίδες μία τη φορά, απελευθερώστε το `engine` μετά από κάθε batch |

Η κατανόηση αυτών των λεπτομερειών σας βοηθά να αποφασίσετε **πότε να προεπεξεργαστείτε εικόνα για OCR** και πότε να προσθέσετε επιπλέον βήματα.

## Συμβουλές Απόδοσης

* **Επαναχρησιμοποιήστε το αντικείμενο `OcrEngine`** εάν επεξεργάζεστε πολλές εικόνες σε βρόχο—το κόστος αρχικοποίησης μειώνεται σημαντικά.
* Ορίστε `engine.Preprocessing.DenoiseLevel = DenoiseLevel.Medium` για ισορροπία ταχύτητας‑ακρίβειας σε φωτογραφίες υψηλής ανάλυσης.
* Για εργασίες σε παρτίδες, εξετάστε το ενδεχόμενο απενεργοποίησης του `AutoDeskew` αν γνωρίζετε ότι όλες οι εικόνες είναι ήδη όρθιες· αυτό μπορεί να εξοικονομήσει μερικά χιλιοστά του δευτερολέπτου ανά αρχείο.

## Σχετικές Έννοιες για Εξερεύνηση

* **Ανίχνευση γραμμών κειμένου** – εμβάθυνση στο πώς λειτουργεί το deskew εσωτερικά.
* **Πακέτα γλωσσών** – το Aspose OCR υποστηρίζει πολλές γλώσσες· φορτώστε το κατάλληλο πακέτο για μη‑Αγγλικό κείμενο.
* **Δομημένη έξοδος** – αντί για απλό κείμενο, ανακτήστε τα bounding boxes (`result.Regions`) για να δημιουργήσετε PDF με επιλέξιμο κείμενο.

## Συμπέρασμα

Μόλις καλύψαμε πώς να **προεπεξεργαστείτε εικόνα για OCR** σε C# χρησιμοποιώντας το Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}