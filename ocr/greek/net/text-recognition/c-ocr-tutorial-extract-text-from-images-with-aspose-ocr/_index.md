---
category: general
date: 2026-02-19
description: c# OCR tutorial – μάθετε πώς να εξάγετε κείμενο από εικόνα, να διαβάζετε
  κείμενο εικόνας, να μετατρέπετε εικόνα σε κείμενο και να αναγνωρίζετε κείμενο εικόνας
  χρησιμοποιώντας το Aspose.OCR σε λίγα λεπτά.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- read image text
- convert image to text
- recognize image text
language: el
og_description: Το tutorial C# OCR σας δείχνει πώς να εξάγετε κείμενο από εικόνα,
  να διαβάσετε κείμενο εικόνας, να μετατρέψετε την εικόνα σε κείμενο και να αναγνωρίσετε
  κείμενο εικόνας χρησιμοποιώντας το Aspose OCR.
og_title: c# OCR οδηγός – Εξαγωγή κειμένου από εικόνες με το Aspose OCR
tags:
- OCR
- C#
- Aspose
title: 'c# OCR οδηγός: Εξαγωγή κειμένου από εικόνες με Aspose OCR'
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Εξαγωγή Κειμένου από Εικόνες με Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από εικόνα** αρχεία ενώ παραμένετε σε ένα καθαρό περιβάλλον C#; Αυτό ακριβώς λύνει αυτό το **c# ocr tutorial**. Σε λίγα μόνο βήματα θα μάθετε να διαβάζετε κείμενο από εικόνα, να μετατρέπετε εικόνα σε κείμενο, και ακόμη να αναγνωρίζετε κείμενο εικόνας σε διαφορετικές γλώσσες χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR.

Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεστε: από την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση της άδειας, τη ρύθμιση της γλώσσας και την εκτύπωση των αποτελεσμάτων. Στο τέλος θα έχετε μια έτοιμη‑για‑εκτέλεση εφαρμογή κονσόλας που μετατρέπει οποιαδήποτε εικόνα—όπως ένα σαρωμένο τιμολόγιο ή ένα στιγμιότυπο—σε αναζητήσιμο κείμενο.

## Τι Θα Χρειαστείτε

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)  
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)  
- Ένα αρχείο άδειας Aspose.OCR *προαιρετικό* – η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης, αλλά μια άδεια αφαιρεί τα υδατογραφήματα.  
- Μια δείγμα εικόνας (π.χ., `cyrillic_sample.jpg`) τοποθετημένη κάπου στο δίσκο.

Δεν απαιτούνται άλλα εργαλεία τρίτων· το Aspose.OCR διαχειρίζεται όλη τη βαριά δουλειά στο παρασκήνιο.

---

![c# ocr tutorial δείγμα εικόνας που εμφανίζει κυριλλικό κείμενο](/images/ocr-sample.jpg "c# ocr tutorial – δείγμα εικόνας για OCR")

## c# ocr tutorial – Ρύθμιση Aspose OCR

Πρώτα, προσθέστε το πακέτο Aspose.OCR στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, μπορείτε επίσης να κάνετε δεξί‑κλικ στο έργο → **Manage NuGet Packages** και να ψάξετε για *Aspose.OCR*.

### Γιατί είναι σημαντική η άδεια

Το Aspose.OCR λειτουργεί σε λειτουργία αξιολόγησης 30 ημερών χωρίς άδεια. Η κλάση `License` απλώς δείχνει στο αρχείο `.lic` σας· μόλις οριστεί, η μηχανή σταματά να εισάγει υποσέλιδα αξιολόγησης στην έξοδο.

```csharp
// Optional: apply your Aspose.OCR license to unlock full features
// new License().SetLicense("Aspose.OCR.lic");
```

Αν παραλείψετε αυτή τη γραμμή κατά την ανάπτυξη, το OCR λειτουργεί ακόμα—απλώς θυμηθείτε ότι η ειδοποίηση αξιολόγησης θα εμφανίζεται στο εξαγόμενο κείμενο.

## Εξαγωγή κειμένου από εικόνα – Δημιουργία του OCR Engine

Ο πυρήνας κάθε **c# ocr tutorial** είναι το αντικείμενο `OcrEngine`. Αφηρεί όλη τη διαδικασία αναγνώρισης.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 1: (Optional) Apply your license – see above
        // new License().SetLicense("Aspose.OCR.lic");

        // Step 2: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 3: Choose the language you want to recognize
        // For this demo we use Cyrillic, but you can pick English, Arabic, etc.
        ocrEngine.Language = Language.Cyrillic;

        // Step 4: Run OCR on the target picture
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/cyrillic_sample.jpg");

        // Step 5: Output the recognized text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

### Τι κάνει πραγματικά ο κώδικας

- **Instantiating `OcrEngine`** δημιουργεί ένα νέο πλαίσιο επεξεργασίας.  
- **Setting `Language`** ενημερώνει το Aspose για το σύνολο χαρακτήρων που αναμένεται· αυτό βελτιώνει δραματικά την ακρίβεια επειδή η μηχανή μπορεί να εφαρμόσει γλωσσο‑συγκεκριμένες ευρετικές.  
- **`RecognizeImage`** φορτώνει το αρχείο, εκτελεί μια σειρά βημάτων προεπεξεργασίας εικόνας (ευθυγράμμιση, δυαδικοποίηση, αφαίρεση θορύβου) και τελικά τρέχει τον αναγνωριστή νευρωνικού δικτύου.  
- **`result.Text`** περιέχει την αναπαράσταση απλού κειμένου—ιδανική για σενάρια **convert image to text**.

## Ανάγνωση κειμένου εικόνας – Διαχείριση Διαφορετικών Τύπων Αρχείων

Το Aspose.OCR δεν περιορίζεται μόνο σε JPEG. Υποστηρίζει PNG, BMP, TIFF και ακόμη σελίδες PDF (ως εικόνες). Αν χρειάζεται να επεξεργαστείτε μια δέσμη, τυλίξτε την κλήση σε έναν απλό βρόχο:

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.*", SearchOption.TopDirectoryOnly)
                          .Where(f => f.EndsWith(".jpg") || f.EndsWith(".png") || f.EndsWith(".tif"))
                          .ToArray();

foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(res.Text);
}
```

### Ακραία περίπτωση: Κενές ή κατεστραμμένες εικόνες

Αν το `RecognizeImage` λάβει ένα null ή μη αναγνώσιμο αρχείο, ρίχνει ένα `ArgumentException`. Μια γρήγορη προστασία κρατά το **c# ocr tutorial** σας ανθεκτικό:

```csharp
if (!File.Exists(file))
{
    Console.WriteLine($"File not found: {file}");
    continue;
}
```

## Αναγνώριση κειμένου εικόνας – Λεπτομερής Ρύθμιση για Ακρίβεια

Μερικές φορές οι προεπιλεγμένες ρυθμίσεις χάνουν μερικούς χαρακτήρες, ειδικά σε σαρώσεις χαμηλής αντίθεσης. Το Aspose.OCR εκθέτει μερικές ρυθμίσεις που μπορείτε να προσαρμόσετε:

| Ιδιότητα               | Τι κάνει                              | Τυπική περίπτωση χρήσης |
|------------------------|---------------------------------------|--------------------------|
| `ocrEngine.PreprocessingOptions.Deskew` | Περιστρέφει την εικόνα για να διορθώσει την κλίση | Σαρωμένα έγγραφα |
| `ocrEngine.PreprocessingOptions.NoiseRemoval` | Αφαιρεί στίγματα | Παλιά φωτογραφίες |
| `ocrEngine.Language`   | Μοντέλο γλώσσας (Κυριλλικό, Αγγλικά, κ.λπ.) | Πολυγλωσσικό OCR |

Παράδειγμα ενεργοποίησης deskew:

```csharp
ocrEngine.PreprocessingOptions.Deskew = true;
```

Αυτές οι προσαρμογές σας βοηθούν να **εξάγετε κείμενο από εικόνα** αρχεία που δεν είναι τέλεια ευθυγραμμισμένα, αυξάνοντας το ποσοστό επιτυχίας της λειτουργίας **read image text**.

## Αναμενόμενο Αποτέλεσμα

Εκτελώντας το δείγμα κώδικα εναντίον του `cyrillic_sample.jpg` (που περιέχει τη φράση “Привет мир”) θα λάβετε κάτι όπως:

```
Recognized text:
Привет мир
```

Αν βρίσκεστε σε λειτουργία αξιολόγησης, θα δείτε επίσης μια γραμμή στο τέλος:

```
--- Evaluation version. Use a licensed copy for production. ---
```

Αυτή η γραμμή εξαφανίζεται μόλις παρέχετε ένα έγκυρο αρχείο άδειας.

---

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

1. **Wrong language setting** – Η χρήση του `Language.English` σε κυριλλικό κείμενο θα επιστρέψει ακατανόητο κείμενο. Πάντα ταιριάζετε τη γλώσσα με την πηγή.  
2. **Large images** – Η επεξεργασία μιας φωτογραφίας 10 MP μπορεί να είναι αργή. Μειώστε πρώτα την εικόνα (`Bitmap.Resize`) αν η ταχύτητα είναι πιο σημαντική από την τέλεια ακρίβεια pixel‑perfect.  
3. **Missing dependencies** – Το Aspose.OCR έρχεται με εγγενή δυαδικά αρχεία· βεβαιωθείτε ότι ο φάκελος εξόδου περιέχει το `Aspose.OCR.Native.dll` (το NuGet το διαχειρίζεται, αλλά προσαρμοσμένες αλυσίδες κατασκευής μπορεί να χρειάζονται βήμα αντιγραφής).

## Επόμενα Βήματα – Πέρα από τα Βασικά

- **Batch conversion**: Συνδυάστε τον βρόχο που εμφανίστηκε νωρίτερα με ασύγχρονο `Task.Run` για να επιταχύνετε μεγάλους φακέλους.  
- **Export to PDF**: Αφού **convert image to text**, περάστε τη συμβολοσειρά σε έναν δημιουργό PDF (π.χ., Aspose.PDF) για να δημιουργήσετε PDF με δυνατότητα αναζήτησης.  
- **Integrate with Azure Functions**: Μετατρέψτε τη λογική OCR σε ένα serverless endpoint που επεξεργάζεται ανεβάσματα σε πραγματικό χρόνο.  

Όλες αυτές οι επεκτάσεις συνεχίζουν το θέμα του **extract text from image** και **read image text** σε πραγματικές εφαρμογές.

---

## Συμπέρασμα

Μόλις ολοκληρώσατε ένα **c# ocr tutorial** που δείχνει πώς να διαβάζετε κείμενο εικόνας, να μετατρέπετε εικόνα σε κείμενο και να αναγνωρίζετε κείμενο εικόνας χρησιμοποιώντας το Aspose.OCR. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω παρουσιάζει κάθε βήμα—από την άδεια μέχρι την επιλογή γλώσσας και τη διαχείριση σφαλμάτων—ώστε να μπορείτε να ενσωματώσετε αυτόν τον κώδικα σε οποιοδήποτε έργο .NET και να αρχίσετε να εξάγετε κείμενο αμέσως.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές γλώσσες, να ρυθμίσετε τις επιλογές προεπεξεργασίας ή να συνδέσετε το αποτέλεσμα με μια βάση δεδομένων για αρχεία με δυνατότητα αναζήτησης. Αν αντιμετωπίσετε προβλήματα, η τεκμηρίωση του Aspose είναι μια αξιόπιστη πηγή, αλλά ο κώδικας εδώ θα πρέπει να λειτουργεί αμέσως για τις περισσότερες περιπτώσεις.

Καλή προγραμματιστική, και εύχομαι οι εικόνες σας να είναι πάντα αναγνώσιμες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}