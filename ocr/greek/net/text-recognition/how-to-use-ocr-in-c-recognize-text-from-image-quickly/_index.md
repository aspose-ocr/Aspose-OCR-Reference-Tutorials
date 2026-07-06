---
category: general
date: 2026-02-16
description: Πώς να χρησιμοποιήσετε OCR σε C# για να αναγνωρίσετε κείμενο από εικόνα,
  να εξάγετε κείμενο από JPEG και να μετατρέψετε την εικόνα σε κείμενο με το Aspose
  OCR. Οδηγός βήμα‑προς‑βήμα.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from jpeg
- convert image to text
- how to extract text
language: el
og_description: Μάθετε πώς να χρησιμοποιείτε OCR σε C# για να αναγνωρίζετε κείμενο
  από εικόνα, να εξάγετε κείμενο από JPEG και να μετατρέπετε την εικόνα σε κείμενο.
  Περιλαμβάνονται πλήρης κώδικας και συμβουλές.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνώριση κειμένου από εικόνα
tags:
- C#
- Aspose OCR
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνωρίστε κείμενο από εικόνα γρήγορα
url: /el/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνωρίστε κείμενο από εικόνα γρήγορα

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** σε ένα έργο .NET για να εξάγετε κείμενο από μια εικόνα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζεται να *αναγνωρίσουν κείμενο από εικόνα* αρχεία, ειδικά JPEG, και καταλήγουν να ψάχνουν για ένα “μαγικό” απόσπασμα που λειτουργεί.

Το θέμα είναι—το Aspose OCR κάνει όλη τη διαδικασία παιχνιδάκι. Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε για **να μετατρέψετε εικόνα σε κείμενο**, να εξάγετε αυτό το κείμενο από ένα JPEG, και—ναι—θα δείτε την ακριβή έξοδο στην κονσόλα σας. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα.

## Τι θα μάθετε

- Εγκαταστήστε το πακέτο NuGet Aspose OCR.
- Αρχικοποιήστε τη μηχανή OCR σε **online mode** ώστε τα ελλιπή πακέτα γλώσσας να ληφθούν αυτόματα.
- Φορτώστε το μοντέλο γλώσσας Κυριλλικό (ή οποιαδήποτε άλλη γλώσσα χρειάζεστε).
- Παρέχετε μια JPEG εικόνα στη μηχανή και **αναγνωρίστε κείμενο από εικόνα**.
- Αντιμετωπίστε κοινά προβλήματα όπως ελλιπή αρχεία ή μη υποστηριζόμενες μορφές.
- Δείτε τον πλήρη κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio σήμερα.

> **Συμβουλή:** Αν εργάζεστε με σαρωμένα PDF, μπορείτε να εξάγετε κάθε σελίδα ως εικόνα και να τη δώσετε στην ίδια μηχανή—δεν αλλάζει τίποτα στον κώδικα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Το Aspose OCR στοχεύει σε σύγχρονα runtime. |
| Visual Studio 2022 (or any IDE you like) | Χρήσιμα για debugging και IntelliSense. |
| A JPEG image containing text (e.g., `cyrillic_sample.jpg`) | Θα **εξάγουμε κείμενο από JPEG** στην επίδειξη. |
| Internet connection (for the first run) | Η μηχανή κατεβάζει πακέτα γλώσσας σε **online mode**. |

Αν κάποιο από αυτά λείπει, το tutorial θα εξακολουθεί να μεταγλωττίζεται, αλλά η μηχανή OCR μπορεί να ρίξει εξαίρεση όταν δεν βρει το μοντέλο γλώσσας.

## Βήμα 1 – Εγκατάσταση του πακέτου NuGet Aspose OCR

Το πρώτο που χρειάζεστε είναι η ίδια η βιβλιοθήκη. Ανοίξτε το **Package Manager Console** και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Ή, αν προτιμάτε το UI, αναζητήστε το “Aspose.OCR” στο NuGet Package Manager και πατήστε **Install**. Αυτό θα κατεβάσει όλα τα απαιτούμενα DLL, συμπεριλαμβανομένης της βασικής μηχανής OCR και των μοντέλων γλώσσας που μπορούν να ληφθούν κατά απαίτηση.

> **Γιατί αυτό το βήμα είναι σημαντικό:** Χωρίς το πακέτο, καμία κλάση όπως `OcrEngine` ή `LanguageModel` δεν υπάρχει, έτσι ο κώδικάς σας δεν θα μεταγλωττιστεί.

## Βήμα 2 – Αρχικοποίηση της μηχανής OCR (Primary Keyword)

Τώρα που η βιβλιοθήκη είναι έτοιμη, μπορούμε να **χρησιμοποιήσουμε OCR** δημιουργώντας μια παρουσία `OcrEngine`. Η χρήση του `ResourceMode.Online` λέει στο Aspose να κατεβάσει αυτόματα τυχόν ελλιπή πακέτα γλώσσας, κάτι που είναι ιδανικό για γρήγορη δημιουργία πρωτοτύπων.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine in online mode.
// This will download language packs if they aren’t already present.
OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);
```

> **Τι συμβαίνει στο παρασκήνιο;** Η μηχανή επικοινωνεί με το CDN του Aspose, ελέγχει ποια μοντέλα γλώσσας έχετε ζητήσει και κατεβάζει τα απαραίτητα αρχεία σε τοπική κρυφή μνήμη. Οι επόμενες εκτελέσεις είναι offline, επιταχύνοντας την επεξεργασία.

## Βήμα 3 – Φόρτωση του επιθυμητού μοντέλου γλώσσας

Αν δουλεύετε με αγγλικό κείμενο, το `LanguageModel.English` είναι το προεπιλεγμένο. Στο παράδειγμά μας θα φορτώσουμε **Cyrillic**, αλλά μπορείτε να το αντικαταστήσετε με οποιαδήποτε υποστηριζόμενη γλώσσα.

```csharp
// Load the Cyrillic language model so the engine knows which characters to look for.
ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
```

> **Ακραία περίπτωση:** Αν προσπαθήσετε να φορτώσετε μια γλώσσα που δεν υποστηρίζεται (π.χ., `LanguageModel.Klingon`), θα ριχτεί `UnsupportedLanguageException`. Τυλίξτε την κλήση σε μπλοκ try‑catch αν δημιουργείτε UI που επιτρέπει στους χρήστες να επιλέγουν γλώσσες σε πραγματικό χρόνο.

## Βήμα 4 – Παροχή της εικόνας (Secondary Keyword: extract text from jpeg)

Εδώ δείχνουμε τη μηχανή στο αρχείο JPEG που περιέχει το κείμενο που θέλουμε να διαβάσουμε. Η `ImageStream.FromFile` δέχεται οποιαδήποτε μορφή εικόνας μπορεί να αποκωδικοποιήσει το Aspose, αλλά το JPEG είναι το πιο κοινό για φωτογραφίες και στιγμιότυπα οθόνης.

```csharp
// Replace the path with the actual location of your JPEG image.
string imagePath = @"C:\Images\cyrillic_sample.jpg";

if (!File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Load the image into the OCR engine.
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Γιατί είναι σημαντικό:** Η παροχή μιας μη υπάρχουσας διαδρομής θα προκαλέσει `FileNotFoundException`. Η παραπάνω guard clause αποτρέπει το πρόγραμμα από το να καταρρεύσει και δίνει στον χρήστη ένα σαφές μήνυμα.

## Βήμα 5 – Αναγνώριση κειμένου από εικόνα και εμφάνιση αποτελέσματος

Ο πυρήνας του **πώς να χρησιμοποιήσετε OCR** είναι η μέθοδος `Recognize`. Επιστρέφει μια απλή συμβολοσειρά με όλους τους ανιχνευμένους χαρακτήρες, διατηρώντας τις αλλαγές γραμμής όπου είναι δυνατόν.

```csharp
try
{
    // Perform the OCR operation.
    string recognizedText = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("📝 Recognized Text:");
    Console.WriteLine(recognizedText);
}
catch (Exception ex)
{
    Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
}
```

### Αναμενόμενη έξοδος στην κονσόλα

Αν το JPEG περιέχει τη φράση “Привет мир” (Hello world στα Ρωσικά), θα δείτε κάτι όπως:

```
📝 Recognized Text:
Привет мир
```

Αν η εικόνα είναι θολή, η έξοδος μπορεί να περιέχει ακατάλληλους χαρακτήρες—εδώ η προεπεξεργασία (π.χ., αύξηση αντίθεσης) μπορεί να βοηθήσει, κάτι που θα αναφέρουμε αργότερα.

## Βήμα 6 – Πλήρες λειτουργικό παράδειγμα (Όλα τα βήματα συνδυασμένα)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε ένα νέο έργο **Console App**. Περιλαμβάνει όλα από την εγκατάσταση του πακέτου μέχρι τη διαχείριση σφαλμάτων, ώστε να το τρέξετε αμέσως.

```csharp
// ------------------------------------------------------------
// Complete OCR Example – How to use OCR in C#
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine (online mode auto‑downloads language packs)
            OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);

            // 2️⃣ Load the language model you need (Cyrillic in this demo)
            try
            {
                ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
            }
            catch (Exception langEx)
            {
                Console.WriteLine($"❌ Language load error: {langEx.Message}");
                return;
            }

            // 3️⃣ Provide the image – this is where we **extract text from jpeg**
            string imagePath = @"YOUR_DIRECTORY\cyrillic_sample.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Cannot find image at {imagePath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Recognize text – the heart of **how to use OCR**
            try
            {
                string recognizedText = ocrEngine.Recognize();

                // 5️⃣ Output – **convert image to text** and display it
                Console.WriteLine("📝 Recognized Text:");
                Console.WriteLine(recognizedText);
            }
            catch (Exception ocrEx)
            {
                Console.WriteLine($"⚠️ OCR operation failed: {ocrEx.Message}");
            }
        }
    }
}
```

> **Γρήγορη δοκιμή:** Αντικαταστήστε το `YOUR_DIRECTORY\cyrillic_sample.jpg` με την πραγματική διαδρομή σε ένα JPEG που περιέχει καθαρό κείμενο. Εκτελέστε το έργο (F5) και παρακολουθήστε την κονσόλα να εμφανίζει τη εξαγόμενη συμβολοσειρά.

## Βήμα 7 – Συμβουλές, Ακραίες περιπτώσεις και Συχνές ερωτήσεις

### Πώς μπορώ να **αναγνωρίσω κείμενο από εικόνα** αρχεία εκτός του JPEG;

Το Aspose OCR υποστηρίζει PNG, BMP, TIFF και ακόμη σελίδες PDF (όταν τις μετατρέψετε πρώτα σε εικόνες). Απλώς αλλάξτε την επέκταση αρχείου στη `ImageStream.FromFile`. Ο ίδιος κώδικας λειτουργεί—χωρίς επιπλέον ρυθμίσεις.

### Τι γίνεται αν η εικόνα είναι χαμηλής ανάλυσης;

Η ακρίβεια του OCR μειώνεται δραματικά κάτω από 300 dpi. Μπορείτε να βελτιώσετε τα αποτελέσματα με:

1. Αύξηση της ανάλυσης της εικόνας με μια βιβλιοθήκη όπως **ImageSharp**.
2. Εφαρμογή δυαδικού κατωφλίου για αύξηση της αντίθεσης.
3. Χρήση `ocrEngine.Settings.Deskew = true` για ευθυγράμμιση κεκλιμένου κειμένου.

```csharp
ocrEngine.Settings.Deskew = true; // Auto‑corrects rotated text
```

### Μπορώ να **μετατρέψω εικόνα σε κείμενο** μαζικά;

Απολύτως. Τυλίξτε τη λογική αναγνώρισης σε βρόχο `foreach` πάνω από έναν φάκελο εικόνων. Θυμηθείτε να επαναχρησιμοποιήσετε την ίδια παρουσία `OcrEngine`—αποθηκεύει στην κρυφή μνήμη τα πακέτα γλώσσας και επιταχύνει την επεξεργασία σε παρτίδες.

```csharp
string[] files = Directory.GetFiles(@"C:\Images", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string txt = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), txt);
}
```

### Λειτουργεί αυτό σε Linux/macOS;

Ναι. Το Aspose OCR είναι δια‑πλατφόρμα όσο έχετε εγκατεστημένο το .NET runtime. Το μόνο πρόβλημα είναι οι εγγενείς εξαρτήσεις για αποκωδικοποίηση εικόνας, που περιλαμβάνονται στο πακέτο NuGet.

### Πώς μπορώ να **εξάγω κείμενο από jpeg** διατηρώντας τη διάταξη;

Ορίστε `ocrEngine.Settings.PreserveFormatting = true`. Αυτό διατηρεί τις αλλαγές γραμμής και απλούς πίνακες, κάνοντας την έξοδο πιο ευανάγνωστη.

```csharp
ocrEngine.Settings.PreserveFormatting = true;
```

---

## Συμπέρασμα

Σε λίγα βήματα δείξαμε **πώς να χρησιμοποιήσετε OCR** σε C# για **να αναγνωρίσετε κείμενο από εικόνα**, **να εξάγετε κείμενο από JPEG**, και **να μετατρέψετε εικόνα σε κείμενο** με το Aspose OCR. Το πλήρες παράδειγμα λειτουργεί αμέσως, διαχειρίζεται ελλιπή αρχεία και σας δίνει άμεση ανατροφοδότηση στην κονσόλα.

Από εδώ μπορείτε:

- Αντικαταστήστε το `LanguageModel.Cyrillic` με οποιαδήποτε άλλη γλώσσα (English, Arabic, Chinese, κ.λπ.).
- Επεξεργαστείτε κατά παρτίδες φακέλους εικόνων για αυτοματοποίηση εισαγωγής δεδομένων.
- Συνδυάστε OCR με επεξεργασία φυσικής γλώσσας για ευρετηρίαση σαρωμένων εγγράφων.

Λοιπόν, προχωρήστε—δοκιμάστε τον κώδικα, πειραματιστείτε με διαφορετικές ποιότητες εικόνας, και αφήστε τη μηχανή να κάνει το σκληρό έργο. Αν αντιμετωπίσετε πρόβλημα, η κοινότητα (και η τεκμηρίωση του Aspose) είναι μόνο μια αναζήτηση μακριά. Καλή προγραμματιστική!

---

![παράδειγμα στιγμιότυπο χρήσης OCR](placeholder-image.png "πώς να χρησιμοποιήσετε OCR σε C# παράδειγμα")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}