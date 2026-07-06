---
category: general
date: 2026-04-06
description: Πώς να χρησιμοποιήσετε OCR σε C# για την εξαγωγή απλού κειμένου από εικόνες
  JPG, συμπεριλαμβανομένων των κυριλλικών χαρακτήρων. Μάθετε πώς να φορτώνετε την
  εικόνα για OCR, να αναγνωρίζετε κείμενο JPG και να λαμβάνετε αξιόπιστα αποτελέσματα.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για εξαγωγή απλού κειμένου από αρχεία
  JPG. Αυτός ο οδηγός δείχνει πώς να φορτώσετε εικόνα για OCR, να αναγνωρίσετε κείμενο
  JPG και να διαχειριστείτε κυριλλικό κείμενο.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή απλού κειμένου από εικόνες
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή απλού κειμένου από εικόνες
url: /el/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε OCR σε C# – Εξαγωγή απλού κειμένου από εικόνες

Έχετε αναρωτηθεί ποτέ **how to use OCR** σε ένα έργο .NET χωρίς να παλεύετε με τις εγγενείς βιβλιοθήκες; Ίσως έχετε έναν φάκελο με σαρωμένες αποδείξεις, μερικές στιγμιότυπες οθόνης με κυριλλικές λεζάντες, ή απλώς χρειάζεστε να εξάγετε το κείμενο από ένα JPEG για γρήγορη ανάλυση. Τα καλά νέα είναι ότι το Aspose OCR κάνει όλη αυτή τη διαδικασία παιχνιδάκι.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **how to use OCR** για **extract plain text** από μια εικόνα JPEG, πώς να **load image for OCR**, και ακόμη πώς να **extract Cyrillic text** όταν η γλώσσα προέλευσης δεν είναι Λατινική. Στο τέλος θα έχετε μια μικρή εφαρμογή console που εκτυπώνει το αναγνωρισμένο κείμενο απευθείας στην κονσόλα — χωρίς επιπλέον αρχεία, χωρίς μυστικά side‑effects.

> **What you’ll get**  
> * Ένας οδηγός βήμα‑βήμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο Visual Studio.  
> * Επεξηγήσεις του *γιατί* κάθε γραμμή είναι σημαντική, όχι μόνο του *τι* κάνει.  
> * Συμβουλές για τη διαχείριση μεγάλων εικόνων, πολλαπλών γλωσσών και κοινών παγίδων.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).  
* Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε).  
* Πρόσβαση στο Internet την πρώτη φορά που τρέχετε το δείγμα — το Aspose OCR κατεβάζει τα language packs κατά απαίτηση.  

Αν σας λείπει το πακέτο NuGet Aspose OCR, θα το καλύψουμε στο πρώτο βήμα.

## Βήμα 1 – Εγκατάσταση Aspose OCR μέσω NuGet (και γιατί έχει σημασία)

Το βήμα **load image for OCR** δεν μπορεί να γίνει μέχρι να είναι η βιβλιοθήκη παρούσα. Η χρήση του NuGet εγγυάται ότι θα λάβετε τα πιο πρόσφατα, ασφαλή binaries και θα φέρει αυτόματα όλες τις απαιτούμενες εξαρτήσεις.

```bash
dotnet add package Aspose.OCR
```

*Γιατί έχει σημασία*: Το Aspose OCR διανέμεται με ένα μικρό core DLL και φορτώνει τα δεδομένα γλώσσας μόνο όταν τα ζητήσετε. Έτσι η εφαρμογή σας παραμένει ελαφριά και αποφεύγετε την ενσωμάτωση μεγάλων αρχείων γλώσσας που δεν χρησιμοποιούνται.

## Βήμα 2 – Αρχικοποίηση του OCR Engine (η καρδιά του **how to use OCR**)

Η δημιουργία ενός αντικειμένου `OcrEngine` είναι η πρώτη πραγματική γραμμή κώδικα που μετρά για το **how to use OCR**. Η μηχανή προεπιλέγει τη λειτουργία “on‑demand”, δηλαδή θα κατεβάσει το language pack την πρώτη φορά που ζητήσετε μια συγκεκριμένη γλώσσα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **Pro tip**: Αν εργάζεστε πίσω από εταιρικό proxy, ορίστε το `OcrEngine.Proxy` πριν από την πρώτη κλήση αναγνώρισης ώστε το download να ολοκληρωθεί.

## Βήμα 3 – Επιλογή Γλώσσας – **Extract Cyrillic Text** όταν χρειάζεται

Το Aspose OCR υποστηρίζει δεκάδες γραφές. Για **extract Cyrillic text**, απλώς ορίστε την ιδιότητα `Language` σε `OcrLanguage.Cyrillic`. Την πρώτη φορά που εκτελεστεί αυτή η γραμμή, το κυριλλικό module (≈ 5 MB) θα ληφθεί από το CDN του Aspose.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Αν η εικόνα σας περιέχει μόνο λατινικούς χαρακτήρες, μπορείτε να αντικαταστήσετε το `Cyrillic` με `English`. Το ίδιο μοτίβο ισχύει για οποιαδήποτε υποστηριζόμενη γλώσσα.

## Βήμα 4 – **Load Image for OCR** – Από Δίσκο ή Stream

Τώρα πραγματικά **load image for OCR**. Η κλάση `System.Drawing.Image` διαχειρίζεται τις πιο κοινές μορφές (JPG, PNG, BMP). Αν βρίσκεστε σε μη‑Windows πλατφόρμα, σκεφτείτε το `ImageSharp`, αλλά για αυτό το tutorial ο ενσωματωμένος τύπος είναι επαρκής.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **Γιατί έχει σημασία**: Η φόρτωση της εικόνας μέσα σε ένα `using` block εγγυάται ότι οι μη‑διαχειριζόμενοι πόροι GDI+ θα απελευθερωθούν άμεσα, αποτρέποντας διαρροές μνήμης σε υπηρεσίες που τρέχουν πολύ χρόνο.

## Βήμα 5 – **Recognize Text JPG** – Εκτέλεση της διαδικασίας OCR

Με τη μηχανή ρυθμισμένη και την εικόνα φορτωμένη, τελικά **recognize text jpg**. Η μέθοδος `Recognize` επιστρέφει ένα `OcrResult` που περιέχει το απλό string, τους δείκτες εμπιστοσύνης, και ακόμη τα bounding boxes αν τα χρειαστείτε αργότερα.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

Αν θέλετε να βελτιώσετε την ακρίβεια, μπορείτε να προσαρμόσετε το `ocrEngine.Config` (π.χ., ενεργοποίηση `AutoRotate` ή ορισμός `TextOrientation`). Για τις περισσότερες απλές περιπτώσεις, οι προεπιλογές λειτουργούν εκπληκτικά καλά.

## Βήμα 6 – **Extract Plain Text** – Εμφάνιση του Αποτελέσματος

Το τελικό κομμάτι του **how to use OCR** είναι να εξάγετε το αναγνωρισμένο string από το `ocrResult` και να κάνετε κάτι με αυτό. Εδώ απλώς το γράφουμε στην κονσόλα, κάτι που επίσης δείχνει πώς να **extract plain text** από το αντικείμενο αποτελέσματος.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### Αναμενόμενο Αποτέλεσμα

Αν το `cyrillic_sample.jpg` περιέχει τη φράση “Привет мир” (Hello world), θα πρέπει να δείτε:

```
=== Recognized Text ===
Привет мир
```

Αν η εικόνα είναι θολή ή το κείμενο πολύ μικρό, η έξοδος μπορεί να περιέχει σφάλματα· μπορείτε να ελέγξετε το `ocrResult.Confidence` για να αποφασίσετε αν θα επαναλάβετε με υψηλότερη ανάλυση πηγής.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα. Αντιγράψτε το σε ένα νέο έργο Console App (`dotnet new console`) και τρέξτε το. Δεν απαιτούνται επιπλέον αρχεία εκτός από την εικόνα που θα δείξετε.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note**: Αντικαταστήστε το `YOUR_DIRECTORY\cyrillic_sample.jpg` με την πραγματική διαδρομή του αρχείου JPEG σας.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστεί να **recognize text jpg** από stream αντί για αρχείο;

Μπορείτε να περάσετε απευθείας ένα `MemoryStream`:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### Πώς διαχειρίζομαι πολλαπλές γλώσσες στην ίδια εικόνα;

Ορίστε το `ocrEngine.Language` σε `OcrLanguage.Multilingual`. Η μηχανή θα προσπαθήσει να εντοπίσει αυτόματα κάθε γραφή, κάτι που είναι χρήσιμο όταν μια απόδειξη συνδυάζει Αγγλικά και Κυριλλικά.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### Η εικόνα μου είναι τεράστια (πάνω από 5 MP). Θα κολλήσει η μηχανή;

Οι μεγάλες εικόνες αυξάνουν τη χρήση μνήμης και μπορούν να επιβραδύνουν την αναγνώριση. Ένα γρήγορο προ‑resize βοηθά:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### Μπορώ να λάβω το score εμπιστοσύνης για κάθε γραμμή;

Ναι — το `ocrResult.Lines` περιέχει `Confidence` ανά γραμμή. Η επανάληψη πάνω σε αυτές σας επιτρέπει να φιλτράρετε αποτελέσματα χαμηλής εμπιστοσύνης.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## Pro Tips για Παραγωγική OCR

* **Cache language packs** — η πρώτη λήψη μπορεί να διαρκέσει μερικά δευτερόλεπτα· αποθηκεύστε τα αρχεία σε γνωστό φάκελο και ορίστε το `ocrEngine.LanguageDataPath` για επαναχρησιμοποίηση.  
* **Batch processing** — επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` για πολλές εικόνες· η δημιουργία νέας μηχανής ανά αρχείο προσθέτει περιττό κόστος.  
* **Error handling** — τυλίξτε την κλήση `Recognize` σε try/catch. Το Aspose ρίχνει `OcrException` για κατεστραμμένες εικόνες ή μη υποστηριζόμενες μορφές.  
* **Logging** — καταγράψτε το `ocrResult.Confidence` ώστε να μπορείτε αργότερα να ελέγξετε ποιες σελίδες χρειάστηκαν χειροκίνητη επανεξέταση.

## Συμπέρασμα

Καλύψαμε πώς να **use OCR** σε C# για **extract plain text** από ένα JPEG, δείξαμε τα βήματα για **load image for OCR**, παρουσιάσαμε πώς να **recognize text jpg**, και ακόμη εξάγαμε **Cyrillic text** από την εικόνα. Το δείγμα είναι πλήρως λειτουργικό, απαιτεί μόνο ένα πακέτο NuGet, και μπορεί να επεκταθεί για πολυγλωσσικά έγγραφα, batch jobs ή σενάρια σε πραγματικό χρόνο.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αλλάξετε τη γλώσσα από Κυριλλική σε Αραβική, πειραματιστείτε με τη σημαία `AutoRotate`, ή ενσωματώστε το αποτέλεσμα σε έναν δείκτη αναζήτησης. Οι δυνατότητες είναι ατελείωτες.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}