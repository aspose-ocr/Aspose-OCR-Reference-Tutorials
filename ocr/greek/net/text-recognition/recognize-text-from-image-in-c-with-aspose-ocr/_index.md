---
category: general
date: 2026-02-22
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Οδηγός
  βήμα‑προς‑βήμα για εξαγωγή κειμένου από PNG, μετατροπή εικόνας σε κείμενο και ανάγνωση
  ενσωματωμένου πόρου C# για άδεια.
draft: false
keywords:
- recognize text from image
- extract text from png
- convert image to text
- read embedded resource c#
- perform ocr on image
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα άμεσα με το Aspose OCR. Μάθετε πώς
  να εξάγετε κείμενο από PNG, να μετατρέψετε εικόνα σε κείμενο και να διαβάσετε ενσωματωμένο
  πόρο C# για απρόσκοπτη αδειοδότηση.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρης οδηγός Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Αναγνώριση κειμένου από εικόνα σε C# με Aspose OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε C# με Aspose OCR

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις σε C#; Δεν είσαι μόνος—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο εμπόδιο όταν συναντούν για πρώτη φορά το OCR. Σε αυτό το tutorial θα βουτήξουμε κατευθείαν σε μια λειτουργική λύση που σας επιτρέπει να **εξάγετε κείμενο από png**, **μετατρέψετε εικόνα σε κείμενο**, και ακόμη **διαβάσετε ενσωματωμένο πόρο c#** για άδεια χωρίς καμία δυσκολία.

Θα καλύψουμε τα πάντα, από τη φόρτωση μιας ενσωματωμένης άδειας Aspose OCR μέχρι την εκτύπωση του τελικού string στην κονσόλα. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project και να το τρέξετε άμεσα.

## Τι θα χρειαστείτε

- **.NET 6+** (ο κώδικας μεταγλωττίζεται και σε .NET Framework, αλλά το .NET 6 είναι το τρέχον LTS)
- **Aspose.OCR for .NET** πακέτο NuGet (έκδοση 23.9 ή νεότερη)
- Μια **δείγμα PNG** εικόνα που περιέχει καθαρό, τυπωμένο αγγλικό κείμενο
- Ένα **αρχείο άδειας Aspose OCR** (`Aspose.OCR.lic`) προστεθειμένο στο project σας ως *Embedded Resource*

Αν κάποιο από αυτά σας είναι άγνωστο, μην ανησυχείτε—κάθε βήμα παρακάτω εξηγεί πώς να το ρυθμίσετε.

## Βήμα 1: Ανάγνωση του Ενσωματωμένου Πόρου C# License  

Πριν ο κινητήρας OCR λειτουργήσει, το Aspose χρειάζεται μια έγκυρη άδεια. Η αποθήκευση του αρχείου `.lic` ως ενσωματωμένου πόρου το κρατά εκτός του δέντρου πηγαίου κώδικα και κάνει την ανάπτυξη άνετη.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Load the embedded Aspose OCR license
        // ------------------------------------------------------------
        var assembly = Assembly.GetExecutingAssembly();

        // The resource name follows the folder hierarchy in the project.
        // Adjust "MyApp.Resources.Aspose.OCR.lic" if yours differs.
        using (var licenseStream = assembly.GetManifestResourceStream(
               "MyApp.Resources.Aspose.OCR.lic"))
        {
            if (licenseStream == null)
            {
                Console.Error.WriteLine(
                    "License file not found. Make sure it's marked as Embedded Resource.");
                return;
            }

            var license = new License();
            license.SetLicenseFromStream(licenseStream);
        }

        // Continue with OCR steps...
```

**Γιατί είναι σημαντικό:**  
Η ενσωμάτωση της άδειας αποτρέπει τυχαία έκθεση στο source control και εγγυάται ότι το αρχείο μεταφέρεται μαζί με το μεταγλωττισμένο DLL. Αν η ροή είναι `null`, το πρόγραμμα τερματίζεται νωρίς—αυτή είναι η πρώτη μας αμυντική έλεγχος.

## Βήμα 2: Αρχικοποίηση του OCR Engine (Εκτέλεση OCR στην Εικόνα)  

Τώρα που η άδεια φορτώθηκε, μπορούμε να δημιουργήσουμε ένα αντικείμενο `OcrEngine`. Θα ορίσουμε τη γλώσσα στα Αγγλικά επειδή το δείγμα PNG μας χρησιμοποιεί αυτή τη γλώσσα.

```csharp
        // ------------------------------------------------------------
        // 2️⃣ Initialise the OCR engine – this is where we perform OCR on image
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // change to Language.French etc. if needed
        };
```

**Συμβουλή:** Το enum `Language` υποστηρίζει πάνω από 30 γλώσσες. Η αλλαγή είναι τόσο απλή όσο `Language.Spanish`. Αν χρειαστείτε ανίχνευση πολλαπλών γλωσσών, δημιουργήστε ξεχωριστούς κινητήρες ή χρησιμοποιήστε `ocrEngine.AutoDetectLanguage = true` (διαθέσιμο σε νεότερες εκδόσεις Aspose).

## Βήμα 3: Φόρτωση της PNG Εικόνας (Εξαγωγή Κειμένου από PNG)  

Το Aspose OCR λειτουργεί με τη δική του κλάση `Image`, όχι με `System.Drawing.Image`. Δείξτε του ένα μονοπάτι αρχείου ή περάστε ένα `Stream` αν προτιμάτε.

```csharp
        // ------------------------------------------------------------
        // 3️⃣ Load the image – this is the step where we extract text from png
        // ------------------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/sample.png";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Image not found at {imagePath}");
            return;
        }

        var image = Image.Load(imagePath);
```

**Ακραία περίπτωση:** Αν το PNG σας περιέχει κανάλι άλφα (διαφανές φόντο), το Aspose μπορεί να ερμηνεύσει λανθασμένα το κενό χώρο. Μια γρήγορη λύση είναι η προεπεξεργασία της εικόνας με `ImageProcessor` για να την ισοπεδώσετε, αλλά για τις περισσότερες σαρωμένες εγγράφους ο προεπιλεγμένος φορτωτής λειτουργεί καλά.

## Βήμα 4: Εκτέλεση της Αναγνώρισης (Μετατροπή Εικόνας σε Κείμενο)  

Με τον κινητήρα και την εικόνα έτοιμα, η πραγματική κλήση OCR είναι μια μόνο γραμμή. Το αντικείμενο αποτελέσματος σας δίνει το ακατέργαστο string και ένα σκορ εμπιστοσύνης.

```csharp
        // ------------------------------------------------------------
        // 4️⃣ Recognise the image – this is where we convert image to text
        // ------------------------------------------------------------
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: check confidence (0‑100)
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**Γιατί να σας ενδιαφέρει η εμπιστοσύνη:**  
Μια χαμηλή εμπιστοσύνη (π.χ. < 70%) συνήθως υποδηλώνει θολή σάρωση ή μη υποστηριζόμενη γραμματοσειρά. Σε παραγωγή θα μπορούσατε να επιστρέψετε σε διαφορετικό OCR engine ή να ζητήσετε από τον χρήστη να ξανασάρωση.

## Βήμα 5: Έξοδος του Αναγνωρισμένου Κειμένου  

Τέλος, εκτυπώστε το εξαγόμενο string. Σε μια πραγματική εφαρμογή μπορεί να το γράψετε σε βάση δεδομένων, σε αρχείο JSON, ή να το τροφοδοτήσετε σε ευρετήριο αναζήτησης.

```csharp
        // ------------------------------------------------------------
        // 5️⃣ Output the recognised text – the final result of recognize text from image
        // ------------------------------------------------------------
        Console.WriteLine("\n--- Recognised Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Αναμενόμενη Έξοδος Κονσόλας

```
Confidence: 96%
--- Recognised Text ---
Hello, world!
This is a sample PNG used for OCR testing.
```

Αν δείτε το κείμενο παραπάνω (ή κάτι παρόμοιο), συγχαρητήρια—έχετε επιτυχώς **αναγνωρίσει κείμενο από εικόνα** με το Aspose OCR!

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε  

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| `License not set` exception | Το αρχείο άδειας δεν είναι ενσωματωμένο ή το όνομα πόρου είναι λανθασμένο | Επαληθεύστε `Build Action = Embedded Resource` και ελέγξτε το πλήρες όνομα |
| Κενή έξοδος | DPI εικόνας πολύ χαμηλό (κάτω από 150) | Επαναδειγματοληψία του PNG σε τουλάχιστον 150 DPI πριν το δώσετε στο Aspose |
| Παραμορφωμένοι χαρακτήρες | Λάθος γλώσσα επιλεγμένη | Ορίστε `ocrEngine.Language` στη σωστή τιμή του enum `Language` |
| `OutOfMemoryException` σε μεγάλες εικόνες | Φόρτωση τεράστιου PNG (10 MB+) απευθείας | Χρησιμοποιήστε `Image.Load(stream, maxWidth: 2000, maxHeight: 2000)` για να μειώσετε το μέγεθος κατά το φορτίο |

## Pro Tip: Επεξεργασία σε Παρτίδες  

Αν χρειάζεται να **αναγνωρίσετε κείμενο από εικόνα** σε μεγάλες ποσότητες, τυλίξτε τη βασική λογική σε έναν βρόχο `foreach` και επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`. Η επαναχρήση του κινητήρα εξοικονομεί μερικά χιλιοστά του δευτερολέπτου ανά αρχείο, επειδή οι υποκείμενες βιβλιοθήκες παραμένουν φορτωμένες.

```csharp
var images = System.IO.Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var path in images)
{
    var img = Image.Load(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path} → {result.Text.Trim()}");
}
```

## Επόμενα Βήματα  

- **Βελτιώστε την προεπεξεργασία** – δοκιμάστε `ImageProcessor` για να αυξήσετε την αντίθεση ή να αφαιρέσετε θόρυβο.  
- **Εξερευνήστε άλλες μορφές εξόδου** – `ocrResult.GetWords()` σας δίνει τα πλαίσια οριοθέτησης, χρήσιμα για επισήμανση κειμένου στο UI.  
- **Συνδυάστε με Azure Cognitive Services** αν χρειάζεστε υποστήριξη χειρόγραφου στο cloud.  

Όλες αυτές οι επεκτάσεις βασίζονται στο ίδιο βασικό μοτίβο: φορτώστε άδεια, δημιουργήστε κινητήρα, δώστε εικόνα, και διαβάστε το κείμενο.

![Screenshot of console showing recognized text from image](/images/ocr-result.png "σcreenshot αποτελέσματος αναγνώρισης κειμένου από εικόνα")

## Συμπέρασμα  

Διασχίσαμε ένα πλήρες, έτοιμο για παραγωγή παράδειγμα που δείχνει πώς να **αναγνωρίσετε κείμενο από εικόνα** σε C# χρησιμοποιώντας Aspose OCR. Από την ανάγνωση ενσωματωμένου πόρου για άδεια, τη φόρτωση PNG, την εκτέλεση OCR, και την εκτύπωση του αποτελέσματος, καλύφθηκε κάθε βήμα.

Τώρα μπορείτε να **εξάγετε κείμενο από png**, **μετατρέψετε εικόνα σε κείμενο**, και ακόμη **διαβάσετε ενσωματωμένο πόρο c#** για άδεια—όλα σε μερικές δεκάδες γραμμές κώδικα. Μη διστάσετε να πειραματιστείτε με διαφορετικές γλώσσες, μεγαλύτερες παρτίδες εικόνων, ή να ενσωματώσετε το αποτέλεσμα στη δική σας αλυσίδα επεξεργασίας εγγράφων. Καλό προγραμματισμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}