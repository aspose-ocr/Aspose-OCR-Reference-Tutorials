---
category: general
date: 2026-03-21
description: Μάθετε πώς να ευθυγραμμίζετε τα αρχεία εικόνας και να αναγνωρίζετε κείμενο
  σε εικόνα με το Aspose OCR. Μετατρέψτε jpg σε κείμενο και διορθώστε την περιστροφή
  της εικόνας με λίγες γραμμές κώδικα C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: el
og_description: Πώς να αφαιρέσετε την κλίση μιας εικόνας και να εξάγετε κείμενο από
  JPEG χρησιμοποιώντας το Aspose OCR. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να
  μετατρέψετε jpg σε κείμενο και να διορθώσετε την περιστροφή της εικόνας.
og_title: Πώς να διορθώσετε την κλίση μιας εικόνας σε C# – Γρήγορο σεμινάριο Aspose
  OCR
tags:
- OCR
- C#
- Aspose
title: Πώς να διορθώσετε την κλίση μιας εικόνας σε C# – Πλήρης οδηγός με χρήση του
  Aspose OCR
url: /el/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση μιας εικόνας σε C# – Πλήρης οδηγός με χρήση Aspose OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση μιας εικόνας** που βγήκε από σαρωτή κεκλιμένη σε περίεργη γωνία; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να εξάγουν κείμενο από αποδείξεις, τιμολόγια ή χειρόγραφα σημειώματα. Τα καλά νέα είναι ότι με το Aspose OCR μπορείτε να διορθώσετε την περιστροφή της εικόνας και να εξάγετε καθαρό, αναζητήσιμο κείμενο με λίγες μόνο γραμμές.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την εγκατάσταση της βιβλιοθήκης, την ενεργοποίηση της αυτόματης διόρθωσης κλίσης, την αναγνώριση κειμένου στην εικόνα και τελικά τη μετατροπή ενός JPG σε κείμενο. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση εφαρμογή console που **αναγνωρίζει κείμενο jpg** αρχεία χωρίς να τα περιστρέφετε χειροκίνητα πρώτα.

## Τι θα χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework)  
- **Aspose.OCR for .NET** πακέτο NuGet – συνιστάται η έκδοση 23.12 ή νεότερη  
- Ένα δείγμα **skewed JPEG** (π.χ., `skewed_receipt.jpg`) τοποθετημένο κάπου που η εφαρμογή σας μπορεί να το διαβάσει  
- Visual Studio, VS Code, ή οποιονδήποτε επεξεργαστή C# προτιμάτε  

Δεν απαιτούνται άλλα εργαλεία τρίτων. Η βιβλιοθήκη διαχειρίζεται τη διόρθωση κλίσης, το OCR και ακόμη και την ανίχνευση γλώσσας εσωτερικά.

![παράδειγμα διόρθωσης κλίσης εικόνας](/images/deskew-example.png "πώς να διορθώσετε την κλίση μιας εικόνας χρησιμοποιώντας Aspose OCR")

## Βήμα 1: Ρύθμιση του έργου και εγκατάσταση του Aspose.OCR

Για να διατηρήσετε τα πράγματα οργανωμένα, ξεκινήστε ένα νέο έργο console:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

Η γραμμή `dotnet add package` φέρνει τα δυαδικά αρχεία **Aspose.OCR** μαζί με όλες τις εγγενείς εξαρτήσεις. Αν είστε σε Windows, θα λάβετε αυτόματα τα εγγενή DLLs· σε Linux/macOS μπορεί να χρειαστεί το πακέτο `libgdiplus`, αλλά είναι μια εφάπαξ εγκατάσταση.

## Βήμα 2: Ενεργοποίηση αυτόματης διόρθωσης κλίσης (Διόρθωση περιστροφής εικόνας)

Τώρα ανοίξτε το `Program.cs` και αντικαταστήστε το περιεχόμενό του με τον κώδικα παρακάτω. Η βασική γραμμή εδώ είναι `ocrEngine.Settings.Deskew = true;` – αυτό είναι το σήμα που λέει στη μηχανή **πώς να διορθώσει την κλίση μιας εικόνας** αυτόματα.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Γιατί να ενεργοποιήσετε τη διόρθωση κλίσης;

Όταν ένας σαρωτής τροφοδοτεί μια σελίδα με γωνία, η βάση του κειμένου είναι κεκλιμένη. Τα παραδοσιακά OCR engines θα διάβαζαν κάθε χαρακτήρα ως μια κεκλιμένη έκδοση, μειώνοντας δραστικά την ακρίβεια. Ορίζοντας `Deskew = true`, το Aspose OCR εκτελεί μια γρήγορη μεταστροφή Hough στο παρασκήνιο, περιστρέφει το bitmap πίσω σε οριζόντια θέση και στη συνέχεια πραγματοποιεί την αναγνώριση. Το αποτέλεσμα είναι το ίδιο όπως αν είχατε περιστρέψει χειροκίνητα την εικόνα στο Photoshop—μόνο πιο γρήγορο και πλήρως αυτοματοποιημένο.

## Βήμα 3: Αναγνώριση κειμένου στην εικόνα και μετατροπή JPG σε κείμενο

Η κλήση `Recognize` κάνει δύο πράγματα ταυτόχρονα:

1. **Διορθώνει** την κλίση της εικόνας (επειδή ενεργοποιήσαμε τη σημαία).  
2. **Εξάγει** το κειμενικό περιεχόμενο, επιστρέφοντάς το σε ένα αντικείμενο `OcrResult`.

Μπορείτε να θεωρήσετε το `ocrResult.Text` ως μια απλή συμβολοσειρά, να το γράψετε σε αρχείο ή να το περάσετε σε επεξεργαστικές αλυσίδες. Αν χρειάζεστε τις ακατέργαστες βαθμολογίες εμπιστοσύνης ανά λέξη, το `ocrResult.Words` σας δίνει μια συλλογή με τιμές `Confidence`.

### Παράδειγμα εξόδου

Υποθέτοντας ότι το `skewed_receipt.jpg` περιέχει μια απλή απόδειξη, μπορεί να δείτε κάτι όπως:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Παρατηρήστε πώς οι αριθμοί ευθυγραμμίζονται όμορφα παρά την αρχική εικόνα που ήταν περιστραμμένη περίπου 7°. Αυτό είναι το μαγικό αποτέλεσμα της **διόρθωσης περιστροφής εικόνας** που είναι ενσωματωμένο στη βιβλιοθήκη.

## Βήμα 4: Εκτέλεση του παραδείγματος και επαλήθευση αποτελεσμάτων

Συγκεντρώστε (compile) και εκτελέστε:

```bash
dotnet run
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα. Αν λάβετε μια εξαίρεση όπως `FileNotFoundException`, ελέγξτε ξανά τη διαδρομή προς το JPEG σας και βεβαιωθείτε ότι το αρχείο είναι αναγνώσιμο.

### Συνηθισμένα προβλήματα & επαγγελματικές συμβουλές

- **Large Images** – Η χρήση μνήμης του OCR αυξάνεται με τις διαστάσεις της εικόνας. Αλλάξτε το μέγεθος των υπερβολικά μεγάλων αρχείων (π.χ., > 3000 px πλάτος) πριν τα δώσετε στη μηχανή.  
- **Non‑Latin Scripts** – Από προεπιλογή η μηχανή υποθέτει Αγγλικά. Ορίστε `ocrEngine.Settings.Language = OcrLanguage.French;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) αν χρειάζεστε **να αναγνωρίσετε κείμενο στην εικόνα** σε άλλα αλφάβητα.  
- **Batch Processing** – Για πολλά αρχεία, επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`; η δημιουργία νέας μηχανής ανά αρχείο προκαλεί περιττό κόστος.  
- **Quality Check** – Μετά τη διόρθωση κλίσης μπορείτε να εξάγετε το διορθωμένο bitmap μέσω `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` για να επαληθεύσετε οπτικά τη διόρθωση της περιστροφής.

## Πλήρες λειτουργικό παράδειγμα (Όλα μαζί)

Παρακάτω είναι το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει σχόλια, διαχείριση σφαλμάτων και ένα προαιρετικό βήμα για αποθήκευση της διορθωμένης εικόνας.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Η εκτέλεση του προγράμματος θα **αναγνωρίζει κείμενο jpg** αρχεία, θα διορθώνει αυτόματα οποιαδήποτε κλίση και θα εκτυπώνει καθαρό, αναζητήσιμο κείμενο στην κονσόλα.

## Συμπεράσματα

Τώρα έχετε ένα στιβαρό, έτοιμο για παραγωγή απόσπασμα κώδικα που δείχνει **πώς να διορθώσετε την κλίση μιας εικόνας** και να εξάγετε τα περιεχόμενά της χρησιμοποιώντας το Aspose OCR. Η προσέγγιση λειτουργεί για αποδείξεις, τιμολόγια, σαρωμένα συμβόλαια ή οποιοδήποτε JPEG όπου το κείμενο δεν είναι τέλεια οριζόντιο.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- **Batch processing** ενός φακέλου JPEG και εγγραφή κάθε αποτελέσματος σε αρχείο `.txt` (σχετίζεται με *convert jpg to text*).  
- Ενσωμάτωση του βήματος OCR σε ένα ASP.NET Core API ώστε οι πελάτες να μπορούν να ανεβάζουν εικόνες και να λαμβάνουν κείμενο μορφοποιημένο σε JSON.  
- Πειραματισμός με διαφορετικές ρυθμίσεις OCR όπως `ocrEngine.Settings.Language` ή `ocrEngine.Settings.RecognitionMode` για βελτίωση της ακρίβειας σε έγγραφα μη‑Αγγλικής γλώσσας.

Δοκιμάστε το, προσαρμόστε τις ρυθμίσεις και αφήστε τη μηχανή να κάνει το δύσκολο έργο. Όπως πάντα, αν συναντήσετε κάποιο πρόβλημα ή έχετε μια έξυπνη βελτιστοποίηση να μοιραστείτε, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}