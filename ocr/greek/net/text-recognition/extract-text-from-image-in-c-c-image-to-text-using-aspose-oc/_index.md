---
category: general
date: 2026-04-17
description: Εξάγετε κείμενο από εικόνα με το Aspose OCR σε C#. Μάθετε πώς να διαβάζετε
  κείμενο από PNG, να μετατρέπετε εικόνα σε κείμενο και να φορτώνετε εικόνα για OCR
  σε λίγα λεπτά.
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: el
og_description: Εξαγωγή κειμένου από εικόνα με Aspose OCR σε C#. Αυτό το σεμινάριο
  δείχνει πώς να διαβάσετε κείμενο από PNG, να μετατρέψετε την εικόνα σε κείμενο και
  να φορτώσετε την εικόνα για OCR αποδοτικά.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε C# – c# εικόνα σε κείμενο χρησιμοποιώντας Aspose
  OCR
url: /el/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε C# – Πλήρης Οδηγός Aspose OCR

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη να επιλέξετε; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν έχουν ένα στιγμιότυπο PNG, ένα σαρωμένο τιμολόγιο ή μια πολυγλωσσική πινακίδα και θέλουν να μετατρέψουν τα pixel σε αναζητήσιμο κείμενο.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που σας επιτρέπει να **διαβάσετε κείμενο από PNG**, **μετατρέψετε εικόνα σε κείμενο**, και **φορτώσετε εικόνα για OCR** χρησιμοποιώντας το Aspose OCR—όλα σε καθαρό, σύγχρονο C#. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα αρχείο εικόνας για OCR (το βήμα «φόρτωση εικόνας για OCR»)  
- Πώς να διαμορφώσετε το Aspose OCR για μια συγκεκριμένη ομάδα γλωσσών  
- Πώς να εξάγετε τη διαγνωσμένη συμβολοσειρά και να την εμφανίσετε στην κονσόλα  
- Συμβουλές για διαχείριση πολλαπλών γλωσσών, μεγάλων αρχείων και μνήμης  

Δεν απαιτείται εξωτερική τεκμηρίωση· όλα όσα χρειάζεστε βρίσκονται στα παρακάτω αποσπάσματα κώδικα.

## Προαπαιτούμενα

- .NET 6+ SDK (ή .NET Core 3.1+ – το API είναι το ίδιο)  
- Visual Studio 2022, VS Code, ή οποιοδήποτε IDE προτιμάτε  
- Πακέτο NuGet **Aspose.OCR** (εγκατάσταση με `dotnet add package Aspose.OCR`)  

Αν έχετε όλα αυτά, ας ξεκινήσουμε.

![Extract text from image using Aspose OCR in C#](https://example.com/aspsoe-ocr-demo.png "extract text from image using Aspose OCR")

## Βήμα 1 – Φόρτωση της Εικόνας για OCR

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δώσετε κάτι στο OCR engine για ανάγνωση. Το Aspose OCR υποστηρίζει μια ποικιλία μορφών, αλλά το PNG είναι μια κοινή επιλογή για στιγμιότυπα οθόνης και σαρωμένα γραφικά.

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **Γιατί είναι σημαντικό:** Η σωστή φόρτωση της εικόνας διασφαλίζει ότι η μηχανή βλέπει τα ακριβή δεδομένα pixel που περιμένετε. Αν περάσετε ένα κατεστραμμένο stream, η αναγνώριση θα αποτύχει σιωπηλά.

## Βήμα 2 – Δημιουργία και Διαμόρφωση του OCR Engine

Στη συνέχεια, δημιουργήστε ένα στιγμιότυπο του `OcrEngine`. Προαιρετικά, μπορείτε να ορίσετε την ομάδα γλώσσας· για πολλές δυτικές γραφές η προεπιλογή λειτουργεί, αλλά αν δουλεύετε με κυριλλικά, αραβικά ή ασιατικά σύμβολα, θα θέλετε να ενημερώσετε την μηχανή εκ των προτέρων.

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **Pro tip:** Ορίζοντας τη γλώσσα περιορίζετε το σύνολο χαρακτήρων που η μηχανή ψάχνει, κάτι που επιταχύνει την αναγνώριση και βελτιώνει την ακρίβεια.

## Βήμα 3 – Εκτέλεση του OCR και Εξαγωγή Κειμένου

Τώρα γίνεται η βαριά δουλειά. Καλέστε το `Recognize` με την εικόνα που φορτώσατε νωρίτερα, μετά διαβάστε την ιδιότητα `Text` από το αποτέλεσμα.

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### Αναμενόμενο Αποτέλεσμα

Αν το `sample.png` περιέχει τη φράση “Hello, World!” θα δείτε:

```
=== OCR Output ===
Hello, World!
```

Αν η εικόνα είναι πιο σύνθετη (π.χ. μια πολύγραμμη απόδειξη), η μηχανή διατηρεί τις αλλαγές γραμμής, δίνοντάς σας ένα έτοιμο προς επεξεργασία μπλοκ κειμένου.

## Βήμα 4 – Ενσωμάτωση Όλων σε Ένα Πλήρες Πρόγραμμα

Παρακάτω βρίσκεται η πλήρης, αυτόνομη εφαρμογή κονσόλας που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο C#. Περιλαμβάνει διαχείριση σφαλμάτων και σχόλια που εξηγούν κάθε μέρος.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` από το φάκελο του έργου) και παρακολουθήστε την κονσόλα να εκτυπώνει τη διαγνωσμένη συμβολοσειρά. Αυτή είναι ολόκληρη η ροή **εξαγωγής κειμένου από εικόνα** σε λιγότερο από 30 γραμμές κώδικα.

## Βήμα 5 – Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Ανάγνωση Κειμένου από PNG vs. Άλλες Μορφές

Αν και το παράδειγμα χρησιμοποιεί PNG, το Aspose OCR υποστηρίζει επίσης JPEG, BMP, TIFF και GIF. Απλώς αλλάξτε την επέκταση του αρχείου· η ίδια κλήση `OcrImage.FromFile` λειτουργεί χωρίς τροποποίηση.

### Μετατροπή Εικόνας σε Κείμενο σε Web API

Αν χρειάζεται να εκθέσετε αυτή τη λειτουργία μέσω ενός HTTP endpoint, μπορείτε να δεχτείτε ένα ανέβασμα `IFormFile`, να μετατρέψετε το stream σε `OcrImage` με `OcrImage.FromStream`, και να επιστρέψετε τη συμβολοσειρά ως JSON. Η κύρια λογική OCR παραμένει η ίδια.

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### Διαχείριση Μεγάλων Εικόνων

Οι μεγάλες, υψηλής ανάλυσης εικόνες μπορούν να καταναλώσουν πολύ μνήμη. Μια πρακτική προσέγγιση είναι να μειώσετε την κλίμακα της εικόνας πριν τη δώσετε στη μηχανή:

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### Πολυγλωσσικά Έγγραφα

Αν ένα έγγραφο συνδυάζει Αγγλικά και Κυριλλικά, συνδυάστε τις σημαίες γλώσσας:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

Η μηχανή θα προσπαθήσει να αναγνωρίσει χαρακτήρες και από τα δύο σύνολα.

### Αποδέσμευση Πόρων

Η δήλωση `using` γύρω από το `OcrEngine` εγγυάται ότι οι εγγενείς πόροι απελευθερώνονται. Η παράλειψη αυτής της πρακτικής μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

## Pro Tips για Αξιόπιστο OCR

- **Καθαρές Εικόνες Κερδίζουν:** Προεπεξεργαστείτε τις εικόνες (απλοποίηση, αποθόρυβο) με βιβλιοθήκες όπως **ImageSharp** πριν το OCR.  
- **Μέγεθος Γραμματοσειράς:** Κείμενο μικρότερο από 10 px συχνά παραλείπεται· σκεφτείτε να αυξήσετε την κλίμακα της εικόνας.  
- **Ελέγξτε το `ocrResult.Confidence`:** Το αντικείμενο `OcrResult` εκθέτει επίσης βαθμό εμπιστοσύνης ανά λέξη—χρησιμοποιήστε το για να σημαδέψετε τμήματα χαμηλής εμπιστοσύνης για χειροκίνητη επανεξέταση.  
- **Επεξεργασία σε Παρτίδες:** Για δεκάδες αρχεία, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` ώστε να αποφύγετε το επαναλαμβανόμενο κόστος αρχικοποίησης.

## Συμπέρασμα

Μόλις μάθατε πώς να **εξάγετε κείμενο από εικόνα** σε C# χρησιμοποιώντας το Aspose OCR, καλύπτοντας όλα από το **φόρτωση εικόνας για OCR** μέχρι το **μετατροπή εικόνας σε κείμενο** και το **διάβασμα κειμένου από PNG**. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει ακριβώς τον κώδικα που χρειάζεστε, εξηγεί γιατί υπάρχει κάθε βήμα, και προσφέρει πρακτικές παραλλαγές για πραγματικές εφαρμογές.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε τη διαγνωσμένη συμβολοσειρά σε έναν δείκτη αναζήτησης, να τη μεταφράσετε με το Azure Cognitive Services, ή να δημιουργήσετε ένα αναζητήσιμο PDF με το ίδιο επίπεδο κειμένου. Οι δυνατότητες είναι ατελείωτες, και τώρα έχετε μια σταθερή βάση για οποιοδήποτε έργο **c# image to text**.

Πειραματιστείτε, προσαρμόστε τις ρυθμίσεις γλώσσας, ή ενσωματώστε αυτό το απόσπασμα σε μια μεγαλύτερη εφαρμογή. Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}