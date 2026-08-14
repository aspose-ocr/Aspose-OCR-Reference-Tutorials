---
category: general
date: 2026-02-28
description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose.OCR χωρίς σύνδεση
  στο διαδίκτυο. Μάθετε πώς να αναγνωρίζετε κείμενο από PNG, να διαβάζετε κείμενο
  από σάρωση, να μετατρέπετε εικόνα σε κείμενο και να φορτώνετε εικόνα για OCR.
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from scan
- convert image to text
- load image for OCR
language: el
og_description: Εξάγετε κείμενο από εικόνα εκτός σύνδεσης με το Aspose.OCR. Αυτό το
  εκπαιδευτικό δείχνει πώς να αναγνωρίζετε κείμενο από PNG, να διαβάζετε κείμενο από
  σάρωση, να μετατρέπετε την εικόνα σε κείμενο και να φορτώνετε εικόνα για OCR.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Οδηγός για offline OCR
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε C# – Οδηγός βήμα‑βήμα για offline OCR
url: /el/net/text-recognition/extract-text-from-image-in-c-offline-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα σε C# – Οδηγός βήμα‑βήμα για Offline OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά η εφαρμογή σας δεν μπορεί να βασιστεί σε σύνδεση στο διαδίκτυο; Ίσως δημιουργείτε έναν ασφαλή σαρωτή που τρέχει σε περιβάλλον sandbox, ή απλώς θέλετε να αποφύγετε τις καθυστερήσεις. Σε κάθε περίπτωση, το καλό νέο είναι ότι το Aspose.OCR σας επιτρέπει να **αναγνωρίζετε κείμενο από png** αρχεία εντελώς offline.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **διαβάσετε κείμενο από scan** αρχεία, **μετατρέψετε εικόνα σε κείμενο**, και **φορτώσετε εικόνα για OCR** χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR. Στο τέλος θα έχετε μια αυτόνομη εφαρμογή console που εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα — χωρίς υπηρεσίες cloud.

## Τι θα χρειαστείτε

- **.NET 6.0** (ή οποιαδήποτε πρόσφατη έκδοση .NET). Η σύνταξη που φαίνεται λειτουργεί με .NET 6+ αλλά οι ίδιες έννοιες ισχύουν για .NET Framework 4.7+.
- **Aspose.OCR for .NET** πακέτο NuGet. Εγκαταστήστε το με `dotnet add package Aspose.OCR`.
- Ένα αρχείο εικόνας (png, jpg, bmp, κ.λπ.) που περιέχει καθαρό, ευανάγνωστο κείμενο. Για αυτόν τον οδηγό θα το ονομάσουμε `offline_test.png` και θα το τοποθετήσουμε σε φάκελο με όνομα `YOUR_DIRECTORY`.
- Ένα αγαπημένο IDE (Visual Studio, VS Code, Rider — ό,τι προτιμάτε).

> **Pro tip:** Κρατήστε το language pack που χρειάζεστε (English στο παράδειγμα) στον ίδιο υπολογιστή με την εφαρμογή· αυτό εξασφαλίζει πραγματική offline λειτουργία.

## Βήμα 1 – Δημιουργία έργου και εγκατάσταση Aspose.OCR

Δημιουργήστε ένα νέο project console και προσθέστε τη βιβλιοθήκη OCR.

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
dotnet add package Aspose.OCR
```

> **Why this matters:** Η προσθήκη του πακέτου NuGet επαναφέρει όλα τα απαιτούμενα DLL, ώστε να μην λάβετε σφάλμα “missing reference” κατά τη μεταγλώττιση.

## Βήμα 2 – Διαμόρφωση του OCR Engine για offline χρήση

Η καρδιά της λύσης είναι η κλάση `OcrEngine`. Ορίζοντας το `OfflineMode` σε `true` εξασφαλίζετε ότι η μηχανή δεν κάνει ποτέ κλήση δικτύου. Επίσης, καθορίζετε το language pack που βρίσκεται τοπικά.

```csharp
using Aspose.OCR;
using System.Drawing;   // For Image.Load

// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    OfflineMode = true,               // Prevent any network calls
    Language = OcrLanguage.English    // Use the locally‑installed English pack
};
```

> **Explanation:** Το `OfflineMode` είναι ένα μέτρο ασφαλείας. Αν το ξεχάσετε, το Aspose μπορεί σιωπηρά να επικοινωνήσει με την υπηρεσία cloud του για να κατεβάσει ελλιπή δεδομένα γλώσσας, κάτι που αναιρεί το σκοπό ενός offline σαρωτή.

## Βήμα 3 – Φόρτωση της εικόνας που θέλετε να επεξεργαστείτε

Η φόρτωση της εικόνας είναι απλή, αλλά προσέξτε τη χρήση του `using var` που εξασφαλίζει την αυτόματη απελευθέρωση του bitmap.

```csharp
// Adjust the path to point at your image file
using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

// Quick sanity check – you can inspect image.Width / image.Height if needed
Console.WriteLine($"Loaded image with dimensions: {image.Width}x{image.Height}");
```

> **Edge case:** Αν το αρχείο δεν βρεθεί, το `Image.Load` ρίχνει `FileNotFoundException`. Τυλίξτε την κλήση σε μπλοκ try‑catch για κώδικα παραγωγής.

## Βήμα 4 – Εκτέλεση OCR και ανάκτηση του κειμένου

Τώρα πραγματοποιούμε την αναγνώριση. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο string και τα confidence scores.

```csharp
// Perform OCR
var ocrResult = ocrEngine.Recognize(image);

// The Text property holds the plain‑text extraction
string extractedText = ocrResult.Text;

// Show the result
Console.WriteLine("\n--- OCR Output ---");
Console.WriteLine(extractedText);
```

> **What you’re seeing:** Το `ocrResult.Text` είναι ήδη ένα καθαρό string — δεν χρειάζεται να αφαιρέσετε line breaks εκτός αν η επόμενη λογική σας το απαιτεί.

## Βήμα 5 – Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες `Program.cs` που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο project σας. Συγκομποιείται και εκτελείται ακριβώς όπως είναι (απλώς αντικαταστήστε τη διαδρομή της εικόνας).

```csharp
using Aspose.OCR;
using System.Drawing;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine for offline use
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true,               // Prevent any network calls
            Language = OcrLanguage.English    // Use a locally‑available language pack
        };

        // Step 2: Load the image you want to process
        using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

        // Step 3: Run OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Display the extracted text
        System.Console.WriteLine("\n--- Extracted Text ---");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Αναμενόμενη έξοδος

Αν το `offline_test.png` περιέχει τη φράση “Hello, world!”, η κονσόλα θα εκτυπώσει:

```
--- Extracted Text ---
Hello, world!
```

Για μεγαλύτερα έγγραφα θα δείτε ολόκληρη την παράγραφο, τις αλλαγές γραμμής και την στίξη όπως τις ερμηνεύει η μηχανή OCR.

## Συχνές ερωτήσεις & Πιθανά προβλήματα

### 1. *Μπορώ να αναγνωρίσω κείμενο από png αρχεία που έχουν χρωματικό φόντο;*  
Ναι. Το Aspose.OCR εφαρμόζει αυτόματα ένα βήμα προεπεξεργασίας που ομαλοποιεί την αντίθεση. Αν το φόντο είναι πολύ θορυβώδες, σκεφτείτε να μετατρέψετε την εικόνα σε grayscale πρώτα:

```csharp
image = image.ConvertToGrayscale();
```

### 2. *Τι γίνεται αν χρειαστεί να διαβάσω κείμενο από scan PDF αντί για PNG;*  
Εξάγετε κάθε σελίδα ως εικόνα (χρησιμοποιώντας μια βιβλιοθήκη PDF όπως το Aspose.PDF) και περάστε αυτές τις εικόνες στην ίδια pipeline OCR. Η ροή εργασίας παραμένει η ίδια αφού έχετε το bitmap.

### 3. *Πώς διαχειρίζομαι αποτελέσματα χαμηλής εμπιστοσύνης;*  
Το `OcrResult` περιλαμβάνει ιδιότητα `Confidence` ανά χαρακτήρα. Μπορείτε να διατρέξετε το `ocrResult.Characters` και να σημαδέψετε οποιονδήποτε χαρακτήρα με confidence < 0.75 για χειροκίνητη επανεξέταση.

### 4. *Είναι το English language pack το μοναδικό που λειτουργεί offline;*  
Όχι. Οποιοδήποτε language pack εγκαταστήσετε τοπικά (π.χ. `OcrLanguage.Spanish`) λειτουργεί με τον ίδιο τρόπο — απλώς ορίστε `Language = OcrLanguage.Spanish`.

### 5. *Μπορώ να επεξεργαστώ παρτίδες εικόνων από φάκελο;*  
Απόλυτα. Τυλίξτε τη λογική φόρτωσης και αναγνώρισης σε βρόχο `foreach (var file in Directory.GetFiles(folder, "*.png"))`. Θυμηθείτε να απελευθερώνετε κάθε εικόνα μετά την επεξεργασία.

## Συμβουλές απόδοσης

- **Επαναχρησιμοποιήστε το αντικείμενο `OcrEngine`** για πολλές εικόνες. Η δημιουργία νέας μηχανής για κάθε αρχείο προσθέτει επιπλέον κόστος.
- **Αλλάξτε το μέγεθος μεγάλων εικόνων** σε μέγιστο 2000 px στην μεγαλύτερη πλευρά· μεγαλύτερες διαστάσεις δεν βελτιώνουν την ακρίβεια αλλά επιβραδύνουν την επεξεργασία.
- **Ενεργοποιήστε πολυνηματική εκτέλεση** αν έχετε πολλές εικόνες — απλώς βεβαιωθείτε ότι κάθε νήμα έχει το δικό του `OcrEngine` ή προστατέψτε το κοινόχρηστο με κλείδωμα.

## Οπτική επισκόπηση

![Διάγραμμα που δείχνει τη ροή offline OCR – εξαγωγή κειμένου από εικόνα → φόρτωση εικόνας για OCR → αναγνώριση κειμένου από png → έξοδο κειμένου](https://example.com/ocr-flow.png "Ροή εργασίας εξαγωγής κειμένου από εικόνα")

*Η εικονογράφηση επισημαίνει τα τέσσερα κύρια στάδια που καλύπτονται σε αυτόν τον οδηγό.*

## Συμπέρασμα

Τώρα ξέρετε πώς να **εξάγετε κείμενο από εικόνα** εντελώς offline χρησιμοποιώντας το Aspose.OCR. Το tutorial κάλυψε όλα, από τη δημιουργία του project, τη διαμόρφωση του engine για offline λειτουργία, τη φόρτωση εικόνας, και τέλος την **αναγνώριση κειμένου από png** και την **ανάγνωση κειμένου από scan** έγγραφα. Με τον πλήρη κώδικα στα χέρια, μπορείτε γρήγορα να προσαρμόσετε τη λύση για **μετατροπή εικόνας σε κείμενο** σε batch jobs, να την ενσωματώσετε σε desktop utilities, ή να την ενσωματώσετε σε server‑side υπηρεσίες που πρέπει να παραμείνουν on‑premises.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το English language pack με άλλη γλώσσα, πειραματιστείτε με προεπεξεργασία εικόνας (thresholding, deskew), ή τροφοδοτήστε το OCR output σε pipeline φυσικής γλώσσας για ανάλυση συναισθήματος. Οι δυνατότητες είναι απεριόριστες όταν συνδυάζετε offline OCR με σύγχρονα εργαλεία .NET.

Καλή προγραμματιστική, και εύχομαι τα scans σας να είναι πάντα crystal clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}