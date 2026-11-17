---
category: general
date: 2026-03-29
description: Μάθετε πώς να ελέγχετε τη σημαία άδειας στο Aspose OCR και πώς να ερωτάτε
  την κατάσταση της άδειας προγραμματιστικά. Ένα απλό παράδειγμα C# δείχνει την ανίχνευση
  της λειτουργίας αξιολόγησης.
draft: false
keywords:
- check license flag
- how to query license
- Aspose OCR license status
- OcrEngine.IsLicensed
- evaluation mode detection
language: el
og_description: Ελέγξτε τη σημαία άδειας στο Aspose OCR με ευκολία. Ανακαλύψτε πώς
  να ερωτάτε την κατάσταση της άδειας με το OcrEngine.IsLicensed και να διαχειρίζεστε
  τη λειτουργία αξιολόγησης.
og_title: Έλεγχος σημαίας άδειας στο Aspose OCR – Επαλήθευση άδειας σε C#
tags:
- Aspose OCR
- C#
- Licensing
title: Έλεγχος σημαίας άδειας στο Aspose OCR – Σύντομος οδηγός για την επαλήθευση
  της άδειας
url: /el/net/ocr-configuration/check-license-flag-in-aspose-ocr-quick-guide-to-verify-licen/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# έλεγχος σημαίας άδειας – Επαλήθευση αδειοδότησης Aspose OCR σε C#

Έχετε αναρωτηθεί ποτέ πώς να **ελέγξετε τη σημαία άδειας** για το Aspose OCR χωρίς να σκάβετε μέσα σε ατελείωτα έγγραφα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδιο προσπαθώντας να καταλάβουν αν η εφαρμογή τους εκτελείται με πλήρη άδεια ή είναι κολλημένη σε λειτουργία αξιολόγησης. Τα καλά νέα; Είναι μια μιά γραμμή κώδικα σε C# και θα δείτε το αποτέλεσμα αμέσως.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα **πώς να ερωτήσετε την άδεια** χρησιμοποιώντας την ιδιότητα `OcrEngine.IsLicensed`, θα εξηγήσουμε γιατί είναι σημαντικό, και θα σας δώσουμε ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Στο τέλος θα ξέρετε ακριβώς πότε ο κώδικάς σας είναι αδειοδοτημένος, πώς φαίνεται η έξοδος, και πώς να αντιδράσετε αν βρίσκεστε σε λειτουργία αξιολόγησης.

Θα καλύψουμε:
- Προαπαιτούμενα (πακέτο Aspose OCR NuGet, .NET 6+)
- Ανάλυση κώδικα βήμα‑βήμα
- Αναμενόμενη έξοδος κονσόλας
- Συνηθισμένα προβλήματα και επαγγελματικές συμβουλές

Χωρίς περιττές πληροφορίες, μόνο μια πρακτική λύση που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο Visual Studio σήμερα.

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio 2022 ή VS Code με την επέκταση C#)
- Το **Aspose.OCR** πακέτο NuGet εγκατεστημένο (`dotnet add package Aspose.OCR`)
- Είτε ένα έγκυρο αρχείο άδειας Aspose OCR είτε να είστε άνετοι να δουλέψετε σε λειτουργία αξιολόγησης για δοκιμές

Αν λείπει κάποιο από αυτά, κατεβάστε πρώτα το πακέτο NuGet—`dotnet add package Aspose.OCR`—και θα είστε έτοιμοι.

## Βήμα 1 – Εισαγωγή του Namespace του Aspose OCR

Το πρώτο που χρειάζεστε είναι η σωστή οδηγία `using` ώστε ο μεταγλωττιστής να ξέρει πού βρίσκεται το `OcrEngine`.

```csharp
using Aspose.OCR;   // <-- brings OcrEngine into scope
```

> **Γιατί;**  
> Χωρίς αυτήν την εισαγωγή θα λάβετε σφάλμα “type or namespace name could not be found”. Το namespace ομαδοποιεί όλες τις κλάσεις σχετικές με OCR, και το `OcrEngine` είναι το σημείο εισόδου για ελέγχους αδειοδότησης.

## Βήμα 2 – Δημιουργία μιας Ελάχιστης Εφαρμογής Console

Θα τυλίξουμε τον έλεγχο αδειοδότησης μέσα σε μια μικρή εφαρμογή console. Αυτό κρατά το παράδειγμα αυτόνομο και εύκολο στη δοκιμή.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2a: Retrieve the license flag
        bool isLicensed = OcrEngine.IsLicensed;

        // Step 2b: Display the current mode
        Console.WriteLine(isLicensed ? "Licensed" : "Running in evaluation mode");
    }
}
```

### Εξήγηση

- Το `OcrEngine.IsLicensed` είναι μια **στατική Boolean ιδιότητα** που επιστρέφει `true` όταν έχει φορτωθεί μια έγκυρη άδεια στην κλάση `OcrEngine`.  
- Αποθηκεύουμε αυτήν την τιμή στο `isLicensed` για ευκρίνεια.  
- Ο τελεστής τριπλού (`? :`) εκτυπώνει ένα φιλικό μήνυμα. Αν έχετε φορτώσει αρχείο άδειας νωρίτερα (π.χ. `OcrEngine.SetLicense("Aspose.OCR.lic")`), η έξοδος θα είναι **Licensed**· διαφορετικά θα δείτε **Running in evaluation mode**.

## Βήμα 3 – Φόρτωση Άδειας (Προαιρετικό αλλά Συνιστάται)

Αν *έχετε* αρχείο άδειας, φορτώστε το πριν ελέγξετε τη σημαία. Αυτό το βήμα δεν απαιτείται για τη σημαία αυτή καθαυτή—`IsLicensed` θα είναι `false` μέχρι να οριστεί άδεια—αλλά δείχνει τη πλήρη ροή εργασίας.

```csharp
// Load the license file (adjust the path as needed)
try
{
    OcrEngine.SetLicense("Aspose.OCR.lic");
    Console.WriteLine("License file loaded successfully.");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load license: {ex.Message}");
}
```

Τοποθετήστε το παραπάνω μπλοκ **πριν** τη γραμμή `bool isLicensed = OcrEngine.IsLicensed;`. Αν το αρχείο λείπει ή είναι κατεστραμμένο, το block `catch` θα σας ενημερώσει και το `IsLicensed` θα παραμείνει `false`.

## Βήμα 4 – Εκτέλεση και Επαλήθευση του Αποτελέσματος

Δομήστε και εκτελέστε το πρόγραμμα:

```bash
dotnet run
```

Τυπική έξοδος κονσόλας όταν υπάρχει άδεια **υπάρχει**:

```
License file loaded successfully.
Licensed
```

Και όταν βρίσκεστε σε **λειτουργία αξιολόγησης**:

```
Failed to load license: File not found.
Running in evaluation mode
```

Η ακριβής διατύπωση σας επιτρέπει να κατευθύνετε λογικά το πρόγραμμα—ίσως να απενεργοποιήσετε premium λειτουργίες OCR ή να προτρέψετε τον χρήστη να αγοράσει άδεια.

## Βήμα 5 – Διαχείριση της Λειτουργίας Αξιολόγησης με Ευγένεια

Σε πραγματικές εφαρμογές πιθανότατα δεν θέλετε να καταρρεύσετε ή να υποβαθμίσετε σιωπηλά. Εδώ είναι ένα γρήγορο μοτίβο για να προστατεύσετε premium λειτουργικότητα:

```csharp
if (!OcrEngine.IsLicensed)
{
    Console.WriteLine("Warning: Running in evaluation mode. Some features may be limited.");
    // Optionally, disable high‑resolution OCR or watermarks
}
else
{
    // Proceed with full‑feature OCR processing
}
```

> **Pro tip:** Η έκδοση αξιολόγησης προσθέτει υδατογράφημα σε κάθε επεξεργασμένη εικόνα. Ο έλεγχος της σημαίας νωρίς σας βοηθά να αποφασίσετε αν θα ενημερώσετε τον χρήστη ή θα κρύψετε τα UI στοιχεία που σχετίζονται με το υδατογράφημα.

## Βήμα 6 – Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

| Πιθανό Σφάλμα | Γιατί Συμβαίνει | Διόρθωση |
|---------------|------------------|----------|
| Ξέχνατε να καλέσετε `SetLicense` | Το `IsLicensed` παραμένει `false` ακόμη και με έγκυρο αρχείο | Φορτώστε πάντα την άδεια κατά την εκκίνηση της εφαρμογής |
| Χρήση σχετικού μονοπατιού που δείχνει σε λάθος φάκελο | Το runtime δεν μπορεί να εντοπίσει το `Aspose.OCR.lic` | Χρησιμοποιήστε απόλυτο μονοπάτι ή ενσωματώστε την άδεια ως ενσωματωμένο πόρο |
| Εκτέλεση σε πλατφόρμα όπου το αρχείο άδειας είναι μπλοκαρισμένο (π.χ. read‑only container) | Το `SetLicense` ρίχνει εξαίρεση | Βεβαιωθείτε ότι το αρχείο έχει δικαιώματα ανάγνωσης, ή αντιγράψτε το σε φάκελο temp με δικαιώματα εγγραφής |
| Υπόθεση ότι το `IsLicensed` αλλάζει μετά την επεξεργασία OCR | Η ιδιότητα αντικατοπτρίζει μόνο την κατάσταση φόρτωσης της άδειας, όχι ανά λειτουργία | Φορτώστε την άδεια μία φορά· μην ελέγχετε ξανά μετά από κάθε κλήση OCR εκτός αν την αποφορτώσετε (που δεν είναι τυπικό) |

## Παράδειγμα Πλήρους Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο έργο console (`dotnet new console`) και να εκτελέσετε χωρίς τροποποίηση (απλώς τοποθετήστε το `.lic` αρχείο δίπλα στο `Program.cs`).

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Attempt to load the license (optional)
        try
        {
            OcrEngine.SetLicense("Aspose.OCR.lic");
            Console.WriteLine("License file loaded successfully.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load license: {ex.Message}");
        }

        // Query the license flag
        bool isLicensed = OcrEngine.IsLicensed;

        // Inform the user of the current mode
        Console.WriteLine(isLicensed ? "Licensed" : "Running in evaluation mode");

        // Example of graceful handling
        if (!isLicensed)
        {
            Console.WriteLine("Warning: Some OCR features may be restricted in evaluation mode.");
        }

        // Keep the console window open when debugging
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

**Αναμενόμενη έξοδος** (με άδεια):

```
License file loaded successfully.
Licensed
Press any key to exit...
```

**Αναμενόμενη έξοδος** (χωρίς άδεια):

```
Failed to load license: File not found.
Running in evaluation mode
Warning: Some OCR features may be restricted in evaluation mode.
Press any key to exit...
```

## Συμπέρασμα

Τώρα ξέρετε ακριβώς **πώς να ελέγξετε τη σημαία άδειας** για το Aspose OCR και **πώς να ερωτήσετε την κατάσταση της άδειας** με το `OcrEngine.IsLicensed`. Φορτώνοντας την άδεια νωρίς, ελέγχοντας τη Boolean σημαία, και διαχειριζόμενοι την κατάσταση αξιολόγησης με ευγένεια, διατηρείτε την εφαρμογή σας ανθεκτική και φιλική προς τον χρήστη.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να ενσωματώσετε αυτόν τον έλεγχο σε μια μεγαλύτερη αλυσίδα OCR, ίσως ενεργοποιώντας επεξεργασία υψηλής ανάλυσης μόνο όταν υπάρχει πλήρης άδεια. Μπορείτε επίσης να εξερευνήσετε άλλες δυνατότητες του Aspose OCR—ανίχνευση γλώσσας, προεπεξεργασία εικόνας ή επεξεργασία δέσμης—διατηρώντας τη λογική αδειοδότησης καθαρή και κεντρική.

Αν αντιμετωπίσατε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα, και εύχομαι οι επεξεργασίες OCR σας να παραμείνουν πλήρως αδειοδοτημένες! 

![check license flag screenshot](/images/check-license-flag.png "check license flag in Aspose OCR console output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}