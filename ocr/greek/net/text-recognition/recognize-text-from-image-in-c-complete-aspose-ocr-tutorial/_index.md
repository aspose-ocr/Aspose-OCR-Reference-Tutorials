---
category: general
date: 2026-05-06
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα χρησιμοποιώντας το Aspose
  OCR σε C#. Εξάγετε κείμενο από απόδειξη, φορτώστε εικόνα για OCR και δείτε ένα πλήρες
  παράδειγμα Aspose OCR.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: el
og_description: Μάθετε να αναγνωρίζετε κείμενο από εικόνα με το Aspose OCR, να εξάγετε
  κείμενο από απόδειξη και να φορτώνετε εικόνα για OCR σε έναν σύντομο, βήμα‑βήμα
  οδηγό.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρες Μάθημα Aspose OCR
tags:
- C#
- OCR
- Aspose
title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρης οδηγός Aspose OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα σε C# – Πλήρες Aspose OCR Tutorial

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε οι μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να εξάγουν αριθμούς από μια απόδειξη ή να σαρώσουν μια φόρμα. Τα καλά νέα είναι ότι το Aspose OCR κάνει όλη τη διαδικασία παιχνιδάκι, και σε αυτό το tutorial θα σας καθοδηγήσουμε μέσα από ένα **πλήρες παράδειγμα Aspose OCR** που σας επιτρέπει να **εξάγετε κείμενο από απόδειξη** εικόνες με λίγες μόνο γραμμές C#.

Στα επόμενα λεπτά θα μάθετε πώς να **φορτώνετε εικόνα για OCR**, να ορίζετε την ακριβή περιοχή που περιέχει το συνολικό ποσό, να εκτελείτε τη μηχανή και, τέλος, να εμφανίζετε το αποτέλεσμα. Καμία ασαφής αναφορά σε εξωτερικά έγγραφα, καμία ελλιπής πληροφορία—ό,τι χρειάζεστε για copy‑paste και εκτέλεση είναι εδώ. Λίγες ρυθμίσεις, μερικά βήματα, και θα μπορείτε να αναγνωρίζετε κείμενο από αρχεία εικόνας άμεσα.

> **Τι θα αποκομίσετε**  
> * Μια εκτελέσιμη εφαρμογή C# console που αναγνωρίζει κείμενο από αρχεία εικόνας.  
> * Κατανόηση του γιατί μπορεί να θέλετε να περιορίσετε το OCR σε συγκεκριμένο ορθογώνιο (ταχύτητα και ακρίβεια).  
> * Συμβουλές για την αντιμετώπιση κοινών edge cases όπως θολές αποδείξεις ή περιστρεφόμενες σαρώσεις.  

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντική |
|-------------|----------------|
| .NET 6.0 SDK (ή νεότερο) | Το Aspose OCR διανέμεται ως βιβλιοθήκη .NET Standard 2.0 / .NET 5+, οπότε οποιοδήποτε πρόσφατο runtime λειτουργεί. |
| Visual Studio 2022 (ή VS Code) | Ένα άνετο IDE επιταχύνει το debugging, αλλά οποιοσδήποτε επεξεργαστής που μπορεί να μεταγλωττίσει C# αρκεί. |
| **Aspose.OCR for .NET** NuGet package | Αυτή είναι η κύρια βιβλιοθήκη που πραγματικά αναγνωρίζει κείμενο από εικόνα. |
| Ένα δείγμα εικόνας απόδειξης (`receipt.jpg`) | Θα χρησιμοποιήσουμε αυτό το αρχείο για να δείξουμε **εξαγωγή κειμένου από απόδειξη**. |

Μπορείτε να εγκαταστήσετε το πακέτο NuGet με την ακόλουθη εντολή:

```bash
dotnet add package Aspose.OCR
```

Μόλις ολοκληρωθεί, είστε έτοιμοι να ξεκινήσετε τη φόρτωση της εικόνας για OCR.

---

## Βήμα 1: Φορτώστε την εικόνα για OCR

Το πρώτο που πρέπει να κάνετε είναι να κατευθύνετε τη μηχανή στο αρχείο που θέλετε να αναλύσετε. Εδώ εμφανίζεται φυσικά η δευτερεύουσα λέξη-κλειδί **load image for OCR**.

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **Pro tip:** Αν η εικόνα σας βρίσκεται στο φάκελο του έργου, μπορείτε να χρησιμοποιήσετε σχετική διαδρομή όπως `ocrEngine.SetImage("receipt.jpg");`. Βεβαιωθείτε μόνο ότι το αρχείο αντιγράφεται στον φάκελο εξόδου (`Copy to Output Directory = PreserveNewest`).

Η μέθοδος `SetImage` δέχεται οποιαδήποτε μορφή μπορεί να αποκωδικοποιήσει το System.Drawing (JPEG, PNG, BMP κ.λπ.), οπότε δεν περιορίζεστε σε έναν μόνο τύπο αρχείου.

---

## Βήμα 2: Ορίστε την περιοχή ενδιαφέροντος – **extract text from receipt**

Η σάρωση ολόκληρης της εικόνας σπαταλά CPU cycles και μπορεί να εισάγει θόρυβο. Καθορίζοντας στο Aspose OCR ακριβώς πού βρίσκεται το συνολικό ποσό, βελτιώνετε τόσο την ταχύτητα όσο και την ακρίβεια. Εδώ είναι το σημείο όπου **extract text from receipt**.

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **Γιατί ένα ορθογώνιο;**  
> Η μηχανή OCR λειτουργεί πάνω σε πλέγμα pixel. Όταν το περιορίζετε σε μια περιοχή, αγνοεί τα υπόλοιπα—δεν θα εμφανίζονται πια τυχαίοι χαρακτήρες από το λογότυπο του καταστήματος ή τη γραμμή κεφαλίδας.

Αν δεν γνωρίζετε ακριβώς τις συντεταγμένες, μπορείτε να χρησιμοποιήσετε οποιονδήποτε προβολέα εικόνας που εμφανίζει θέσεις pixel (π.χ., Paint.NET) για να εντοπίσετε τα νούμερα.

---

## Βήμα 3: Εκτελέστε τη μηχανή – **recognize text from image** (κύρια λέξη-κλειδί)

Τώρα συμβαίνει η μαγεία. Λέτε στο Aspose να διαβάσει πραγματικά τα pixel μέσα στο ορθογώνιο που ορίσατε.

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

Το `OcrResult` περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη τα bounding boxes για κάθε λέξη. Για μια γρήγορη επίδειξη θα εκτυπώσουμε μόνο το απλό κείμενο.

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Total amount detected: $23.45
```

Αν η έξοδος φαίνεται παραμορφωμένη, ελέγξτε ξανά τις συντεταγμένες ROI ή δοκιμάστε να αυξήσετε την ανάλυση της εικόνας.

---

## Βήμα 4: Διαχείριση του αποτελέσματος – βελτιώνοντας το **Aspose OCR example**

Μια αξιόπιστη λύση κάνει περισσότερα από το να ρίχνει τη συμβολοσειρά στην κονσόλα. Παρακάτω υπάρχει ένας μικρός βοηθός που αφαιρεί κενά, αφαιρεί περιττές αλλαγές γραμμής και επαληθεύει ότι η εξαγόμενη τιμή μοιάζει με χρηματικό ποσό.

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

Ο βοηθός δείχνει ένα ρεαλιστικό **Aspose OCR example** που μπορείτε να ενσωματώσετε σε οποιοδήποτε μεγαλύτερο σύστημα τιμολόγησης.

---

## Βήμα 5: Πλήρες εκτελέσιμο πρόγραμμα – η απόλυτη **extract text from receipt** επίδειξη

Συνδυάζοντας όλα τα παραπάνω παίρνετε ένα ενιαίο, αντιγράψτε‑και‑επικολλήστε αρχείο. Αποθηκεύστε το ως `Program.cs` και τρέξτε `dotnet run`.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**Αναμενόμενη έξοδος**

```
Total amount detected: $23.45
```

Αν η εικόνα της απόδειξης είναι πιο σκοτεινή ή το κείμενο είναι κεκλιμένο, μπορεί να δείτε κάτι όπως `Total amount detected: 23,45`. Η μέθοδος `CleanAmount` το κανονικοποιεί σε τυπική μορφή δεκαδικού.

---

## Συνηθισμένα προβλήματα όταν **recognize text from image**

### 1. Λανθασμένες συντεταγμένες ROI
Αν το ορθογώνιο είναι πολύ μικρό, η μηχανή θα κόψει χαρακτήρες· αν είναι πολύ μεγάλο, επαναφέρετε θόρυβο. Χρησιμοποιήστε ένα οπτικό εργαλείο για να ρυθμίσετε τα νούμερα, ή ανιχνεύστε προγραμματιστικά τα όρια της απόδειξης με μια απλή βιβλιοθήκη επεξεργασίας εικόνας (π.χ., OpenCV).

### 2. Σαρώσεις χαμηλής ανάλυσης
Η ακρίβεια του OCR πέφτει δραματικά κάτω από 150 dpi. Αν ελέγχετε τη διαδικασία σάρωσης, στοχεύστε τουλάχιστον 300 dpi. Αν έχετε αρχείο χαμηλής ανάλυσης, δοκιμάστε `ocrEngine.SetResolution(300);` πριν καλέσετε `Recognize()`.

### 3. Παραμορφωμένες ή περιστρεφόμενες αποδείξεις
Το Aspose OCR μπορεί να περιστρέψει αυτόματα, αλλά πρέπει να το ενεργοποιήσετε:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. Ρυθμίσεις γλώσσας
Η προεπιλεγμένη γλώσσα είναι τα Αγγλικά. Αν η απόδειξή σας περιέχει άλλα αλφάβητα, ορίστε τη γλώσσα ρητά:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## Edge cases & variations – επέκταση του **Aspose OCR example**

* **Πολλαπλά πεδία:** Θέλετε επίσης να εξάγετε την ημερομηνία και το ποσό φόρου; Απλώς επαναλάβετε το βήμα ROI με νέο ορθογώνιο και καλέστε ξανά `Recognize()` (ή χρησιμοποιήστε την ίδια μηχανή μετά την επαναφορά του ROI).  
* **Επεξεργασία παρτίδας:** Τυλίξτε τη λογική σε βρόχο `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` για να διαχειριστείτε δεκάδες αρχεία αυτόματα.  
* **Ασύγχρονη εκτέλεση:** Η μέθοδος `Recognize` είναι συγχρονική, αλλά μπορείτε να τη μεταφέρετε σε νήμα παρασκηνίου με `Task.Run` αν χτίζετε εφαρμογή UI.

---

## Οπτική αναφορά

![παράδειγμα αναγνώρισης κειμένου από εικόνα](/images/ocr-demo.png "Στιγμιότυπο που δείχνει το αποτέλεσμα του Aspose OCR – recognize text from image")

*Το στιγμιότυπο δείχνει την έξοδο της κονσόλας μετά την εκτέλεση του πλήρους προγράμματος.*

---

## Συμπέρασμα

Μόλις **recognize text from image** χρησιμοποιώντας το Aspose OCR, περάσαμε από το **load image for OCR**, και χτίσαμε μια πρακτική ροή **extract text from receipt** που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET. Το πλήρες **Aspose OCR example** αποτελεί μόνο λίγες γραμμές, αλλά καλύπτει τα πιο κοινά σενάρια: επιλογή ROI, καθαρισμό αποτελέσματος και διαχείριση τυπικών παγίδων.

Τι επόμενα; Δοκιμάστε να αντικαταστήσετε το ορθογώνιο με δυναμική ανίχνευση, πειραματιστείτε με διαφορετικές γλώσσες, ή ενσωματώστε το αποτέλεσμα σε βάση δεδομένων για αυτόματη παρακολούθηση εξόδων. Ο ουρανός είναι το όριο, και με τη βάση που έχετε τώρα, θα είναι εύκολο να επεκτείνετε.

Έχετε ερωτήσεις ή μια δύσκολη απόδειξη που δεν συνεργάζεται;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}