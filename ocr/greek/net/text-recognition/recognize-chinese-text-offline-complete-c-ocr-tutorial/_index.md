---
category: general
date: 2026-01-02
description: Μάθετε πώς να αναγνωρίζετε κινεζικό κείμενο και να εξάγετε κείμενο από
  αρχεία PNG με offline αναγνώριση κειμένου χρησιμοποιώντας το Aspose.OCR. Δεν απαιτείται
  internet – εκτελέστε OCR στην εικόνα σε λίγα μόνο βήματα.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: el
og_description: Αναγνωρίστε κινέζικο κείμενο χωρίς internet. Αυτό το σεμινάριο δείχνει
  πώς να εξάγετε κείμενο από PNG χρησιμοποιώντας αναγνώριση κειμένου εκτός σύνδεσης
  και να εκτελέσετε OCR σε εικόνα σε C#.
og_title: Αναγνώριση κινεζικού κειμένου εκτός σύνδεσης – Οδηγός βήμα‑βήμα C#
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κινέζικου κειμένου εκτός σύνδεσης – Πλήρες σεμινάριο OCR σε C#
url: /el/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κινεζικού κειμένου offline – Πλήρης Οδηγός OCR C#

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κινεζικό κείμενο** από ένα σκαναρισμένο PNG αλλά η εφαρμογή σας τρέχει σε μηχάνημα χωρίς internet; Δεν είστε μόνοι. Σε πολλές επιχειρηματικές καταστάσεις—σκεφτείτε διακοπές δικτύου ή συσκευές πεδίου—η εξάρτηση από υπηρεσίες cloud απλώς δεν είναι εφικτή.  

Σε αυτόν τον οδηγό θα περάσουμε από μια αυτόνομη λύση που σας επιτρέπει να **εξάγετε κείμενο από αρχεία png**, να εκτελέσετε **αναγνώριση κειμένου offline** και να **εκτελέσετε OCR σε εικόνες** χρησιμοποιώντας το Aspose.OCR. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα C# console που εκτυπώνει τους Κινεζικούς χαρακτήρες κατευθείαν στην κονσόλα.

## Προαπαιτούμενα

- .NET 6 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένο τοπικά.  
- Visual Studio 2022 ή VS Code – όποιο προτιμάτε.  
- Ένα αντίγραφο του πακέτου NuGet Aspose.OCR for .NET (`Aspose.OCR`).  
- Τα αρχεία πόρων γλώσσας για Αγγλικά και Απλοποιημένα Κινεζικά (το tutorial δείχνει πώς να τα κατεβάσετε αυτόματα).  
- Μια εικόνα με όνομα `chinese_doc.png` τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε (σύμβολο placeholder `YOUR_DIRECTORY`).

Δεν απαιτούνται πρόσθετες υπηρεσίες, κλειδιά API—μόνο ένα τοπικό DLL και μερικά αρχεία πόρων.

---

## Βήμα 1 – Λήψη των απαιτούμενων πόρων γλώσσας (μία φορά)

Το Aspose.OCR αποθηκεύει τα language packs στο δίσκο. Την πρώτη φορά που τρέχετε την εφαρμογή πρέπει να τα κατεβάσετε. Η κλήση `ResourceManager.DownloadResources` κάνει ακριβώς αυτό, και επειδή περνάμε τόσο τα Αγγλικά όσο και τα Απλοποιημένα Κινεζικά, η μηχανή μπορεί αργότερα να εναλλάσσεται μεταξύ τους χωρίς επιπλέον δικτυακή κίνηση.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Pro tip:** Κρατήστε τον ληφθέντα φάκελο (`Aspose.OCR.Resources`) υπό έλεγχο πηγαίου κώδικα αν χρειάζεστε επαναληπτικές κατασκευές σε πολλαπλές μηχανές.

## Βήμα 2 – Αρχικοποίηση της μηχανής OCR σε offline λειτουργία

Ορίζοντας `OfflineMode = true` λέτε στη βιβλιοθήκη να αποφεύγει οποιεσδήποτε κλήσεις HTTP. Αυτό είναι το κλειδί για αληθινή **αναγνώριση κειμένου offline**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Why this matters:** Ορισμένες βιβλιοθήκες OCR επιστρέφουν σε υπηρεσίες cloud όταν λείπει ένα language pack. Με την εξαναγκασμένη offline λειτουργία εγγυόμαστε προβλέψιμη απόδοση και συμμόρφωση με πολιτικές ιδιωτικότητας δεδομένων.

## Βήμα 3 – Φόρτωση του PNG που θέλετε να επεξεργαστείτε

Θα χρησιμοποιήσουμε το `System.Drawing.Bitmap` για να διαβάσουμε την εικόνα. Αν το έργο σας στοχεύει .NET 6+ σε πλατφόρμες εκτός των Windows, σκεφτείτε το `SkiaSharp` ως εναλλακτική, αλλά για τις περισσότερες εγκαταστάσεις που επικεντρώνονται στα Windows το `Bitmap` λειτουργεί καλά.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Edge case:** Αν το PNG είναι πολύ μεγάλο (πάνω από 5 MP) ίσως θελήσετε να το μειώσετε πρώτα για να επιταχύνετε την αναγνώριση και να μειώσετε τη χρήση μνήμης:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Βήμα 4 – Εκτέλεση της αναγνώρισης με γλώσσα Απλοποιημένα Κινεζικά

Εδώ λέμε στη μηχανή ακριβώς ποια γλώσσα να χρησιμοποιήσει. Το αντικείμενο `RecognitionOptions` σας επιτρέπει επίσης να ρυθμίσετε παραμέτρους όπως `DetectOrientation` ή `PreserveFormatting`, αλλά οι προεπιλογές λειτουργούν καλά για τα περισσότερα τυπωμένα έγγραφα.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Βήμα 5 – Εμφάνιση (ή περαιτέρω επεξεργασία) του εξαγόμενου κειμένου

Η ιδιότητα `OcrResult.Text` περιέχει την αναπαράσταση plain‑text. Μπορείτε να την γράψετε στην κονσόλα, σε αρχείο ή να τη δώσετε σε μια επόμενη διαδικασία NLP.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Αναμενόμενη έξοδος

Αν το `chinese_doc.png` περιέχει τη φράση “你好，世界！”, η κονσόλα θα εμφανίσει:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Note:** Η ακρίβεια του OCR εξαρτάται από την ποιότητα της εικόνας, την καθαρότητα της γραμματοσειράς και το αντίθεση. Για τα καλύτερα αποτελέσματα, χρησιμοποιήστε σαρωτικές εικόνες υψηλής ανάλυσης (300 dpi ή περισσότερο) και βεβαιωθείτε ότι το κείμενο δεν είναι παραμορφωμένο.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα. Αποθηκεύστε το ως `Program.cs` μέσα σε ένα νέο console project και τρέξτε `dotnet run`. Όλα τα βήματα είναι ενσωματωμένα, ώστε να δείτε τη ροή από τη λήψη των πόρων μέχρι την τελική έξοδο.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Tip:** Τυλίξτε την κλήση `ResourceManager.DownloadResources` σε ένα μπλοκ `try/catch` αν θέλετε να χειρίζεστε ευγενικά την περίπτωση που το internet είναι πραγματικά μη διαθέσιμο. Η μέθοδος θα ρίξει `NetworkException` διαφορετικά.

---

## Συχνές Ερωτήσεις (FAQ)

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να αναγνωρίσω Παραδοσιακά Κινεζικά;** | Ναι—αντικαταστήστε το `Language.ChineseSimplified` με `Language.ChineseTraditional` και κατεβάστε το αντίστοιχο πακέτο. |
| **Τι γίνεται αν χρειαστεί να εξάγω κείμενο από JPEG αντί για PNG;** | Ο ίδιος κώδικας λειτουργεί· απλώς αλλάξτε την επέκταση του αρχείου. Το `Bitmap` υποστηρίζει τις περισσότερες κοινές μορφές raster. |
| **Υπάρχει τρόπος να λάβω τα πλαίσια περιορισμού (bounding boxes) για κάθε χαρακτήρα;** | Ορίστε `RecognitionOptions.DetectRegions = true`. Το `OcrResult` θα περιέχει τότε αντικείμενα `Region` με συντεταγμένες. |
| **Πώς τρέχω αυτό σε Linux;** | Χρησιμοποιήστε το πακέτο `System.Drawing.Common` (1.0+). Σε Linux χωρίς γραφικό περιβάλλον ίσως χρειαστεί η εγγενής εξάρτηση `libgdiplus`. |
| **Μπορώ να επεξεργαστώ μαζικά έναν φάκελο εικόνων;** | Απόλυτα—τυλίξτε τη λογική αναγνώρισης σε έναν βρόχο `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Βελτίωση ακρίβειας**: πειραματιστείτε με `RecognitionOptions.PreprocessImage = true` ώστε η μηχανή αυτόματα ενισχύσει την αντίθεση.  
- **Συνδυασμός γλωσσών**: μπορείτε να περάσετε έναν πίνακα γλωσσών στη `ResourceManager.DownloadResources` και να αφήσετε τη μηχανή να εντοπίσει αυτόματα.  
- **Ενσωμάτωση UI**: ενσωματώστε τον κώδικα console σε μια εφαρμογή WinForms ή WPF και εμφανίστε το αποτέλεσμα OCR σε ένα textbox.  
- **Εξερεύνηση άλλων βιβλιοθηκών Aspose**: `Aspose.PDF` για δημιουργία PDF, `Aspose.Slides` για αυτοματοποίηση διαφανειών κ.λπ.  

Αν σας ενδιαφέρει η εξαγωγή κειμένου από άλλες μορφές εικόνας, το ίδιο μοτίβο ισχύει—απλώς αλλάξτε τη διαδρομή του αρχείου και, αν χρειάζεται, προσαρμόστε τις επιλογές προεπεξεργασίας. Καλός κώδικας!

---

![παράδειγμα αναγνώρισης κινεζικού κειμένου](/images/recognize-chinese-text.png "Στιγμιότυπο οθόνης που δείχνει την έξοδο της αναγνώρισης κινεζικού κειμένου στην κονσόλα")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}