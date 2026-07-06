---
category: general
date: 2026-02-13
description: Μάθετε πώς να εκτελείτε OCR σε αραβικές εικόνες και να εξάγετε αραβικό
  κείμενο από ένα αρχείο JPG. Αυτός ο οδηγός βήμα‑βήμα σας δείχνει πώς να διαβάζετε
  το κείμενο της εικόνας και να μετατρέπετε την εικόνα σε κείμενο χρησιμοποιώντας
  C#.
draft: false
keywords:
- how to perform OCR
- extract arabic text
- read image text
- extract text jpg
- convert image to text
language: el
og_description: Πώς να πραγματοποιήσετε OCR σε αραβικές εικόνες και να εξάγετε αραβικό
  κείμενο. Ακολουθήστε αυτόν τον πλήρη οδηγό για να διαβάσετε κείμενο από εικόνες
  JPG και να μετατρέψετε την εικόνα σε κείμενο σε C#.
og_title: Πώς να εκτελέσετε OCR σε αραβικές εικόνες – Εξαγωγή κειμένου σε C#
tags:
- OCR
- C#
- Image Processing
title: Πώς να εκτελέσετε OCR σε αραβικές εικόνες – Εξαγωγή κειμένου σε C#
url: /el/net/text-recognition/how-to-perform-ocr-on-arabic-images-extract-text-in-c/
---

Greek translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε Αραβικές Εικόνες – Εξαγωγή Κειμένου σε C#  

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε αραβικές εικόνες χωρίς να τσαλακώνετε τα μαλλιά σας; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν εμπόδια όταν πρέπει να διαβάσουν κείμενο εικόνας γραμμένο σε δεξιά‑προς‑αριστερά σενάρια.  

Σε αυτό το tutorial θα δείτε μια πλήρη, εκτελέσιμη λύση που **εξάγει αραβικό κείμενο** από ένα JPEG, σας δείχνει πώς να **διαβάσετε κείμενο εικόνας**, και τελικά **μετατρέπει την εικόνα σε κείμενο** που μπορείτε να χρησιμοποιήσετε στην εφαρμογή σας. Χωρίς ασαφείς αναφορές, μόνο συγκεκριμένος κώδικας και η λογική πίσω από κάθε γραμμή.

> **Pro tip:** Αν εργάζεστε με σαρωμένες αποδείξεις, πινακίδες δρόμου ή ιστορικά έγγραφα, τα παρακάτω βήματα θα σας εξοικονομήσουν ώρες δοκιμών‑και‑σφαλμάτων.

## Τι Θα Χρειαστείτε  

- .NET 6 ή νεότερο (το παράδειγμα χρησιμοποιεί μια εφαρμογή κονσόλας).  
- Μια βιβλιοθήκη OCR που υποστηρίζει Αραβικά. Για παράδειγμα, θα χρησιμοποιήσουμε το φανταστικό πακέτο NuGet `SimpleOcr`, αλλά το μοτίβο λειτουργεί και με Tesseract, IronOCR ή Microsoft Computer Vision.  
- Ένα αρχείο εικόνας με όνομα `arabic_sign.jpg` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε (π.χ., `./Images/`).  

Αυτό είναι όλο. Χωρίς βαριές SDKs, χωρίς κλειδιά cloud, μόνο μερικές γραμμές C#.

![πώς να εκτελέσετε OCR σε αραβική πινακίδα](/images/arabic_sign.jpg)

*Κείμενο alt εικόνας: πώς να εκτελέσετε OCR σε αραβική πινακίδα*

## Πώς να Εκτελέσετε OCR σε Αραβικές Εικόνες  

Παρακάτω χωρίζουμε τη διαδικασία σε τρία λογικά βήματα. Κάθε βήμα εξηγεί **τι** κάνουμε, **γιατί** είναι σημαντικό, και **πώς** ο κώδικας εντάσσεται.

### Βήμα 1: Εγκατάσταση και Αρχικοποίηση της Μηχανής OCR  

Πρώτα, προσθέστε το πακέτο OCR στο πρότζεκτ σας:

```bash
dotnet add package SimpleOcr
```

Τώρα δημιουργήστε μια παρουσία της μηχανής και πείτε της να χρησιμοποιήσει το μοντέλο γλώσσας Αραβικά. Η προημεροληπτική ρύθμιση της γλώσσας είναι κρίσιμη· διαφορετικά η μηχανή θα αντιμετωπίζει τους αραβικούς χαρακτήρες ως άγνωστα σύμβολα.

```csharp
using System;
using SimpleOcr;   // <-- fictional namespace for illustration

// Step 1: Create an OCR engine configured for Arabic
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic   // Enables right‑to‑left processing
};
```

**Γιατί είναι σημαντικό:** Τα Αραβικά χρησιμοποιούν διαφορετική κατεύθυνση γραφής και έχουν σχήματα χαρακτήρων που εξαρτώνται από το πλαίσιο. Επιλέγοντας ρητά `OcrLanguage.Arabic`, η μηχανή εφαρμόζει τους σωστούς κανόνες σχήματος και βελτιώνει δραματικά την ακρίβεια.

### Βήμα 2: Φόρτωση του JPEG και Εκτέλεση Αναγνώρισης  

Στη συνέχεια τροφοδοτούμε την εικόνα στη μηχανή. Η μέθοδος `RecognizeImage` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης και προαιρετικά πλαίσια οριοθέτησης.

```csharp
// Step 2: Recognize text from the input image
string imagePath = @"./Images/arabic_sign.jpg";

OcrResult ocrResult;
try
{
    ocrResult = ocrEngine.RecognizeImage(imagePath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to process '{imagePath}': {ex.Message}");
    return;
}
```

**Σημείωση περί περιπτώσεων άκρων:** Αν το αρχείο δεν βρεθεί ή η μορφή δεν υποστηρίζεται, το μπλοκ `catch` θα σας δώσει ένα σαφές σφάλμα αντί για σιωπηλή κατάρρευση. Αυτό είναι ιδιαίτερα χρήσιμο όταν **εξάγετε κείμενο από JPG** αρχεία σε εργασίες παρτίδας.

### Βήμα 3: Εξαγωγή του Κειμένου και Χρήση του  

Τέλος, εξάγουμε τη αναγνωρισμένη συμβολοσειρά από το `ocrResult` και την εμφανίζουμε. Μπορείτε επίσης να τη γράψετε σε αρχείο, να τη στείλετε μέσω API ή να τη δώσετε σε επόμενες διεργασίες NLP.

```csharp
// Step 3: Display the extracted Arabic text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);

// Optional: Save to a .txt file for later processing
System.IO.File.WriteAllText("./output/extracted_text.txt", ocrResult.Text);
```

**Αναμενόμενη έξοδος:**  
Αν το `arabic_sign.jpg` περιέχει τη φράση “مكتبة المدينة” (City Library), η κονσόλα θα εκτυπώσει κάτι σαν:

```
=== Extracted Arabic Text ===
مكتبة المدينة
```

Το αποτέλεσμα μπορεί να περιέχει επιπλέον κενά· μπορείτε να τα καθαρίσετε με `String.Trim()` ή κανονικές εκφράσεις αν χρειαστεί.

## Συνηθισμένες Παραλλαγές & Συμβουλές  

### Ανάγνωση Κειμένου Εικόνας από Διαφορετικές Μορφές  

Ο ίδιος κώδικας λειτουργεί για PNG, BMP ή ακόμη και σελίδες PDF (αν η βιβλιοθήκη τα υποστηρίζει). Απλώς αλλάξτε την επέκταση αρχείου στο `imagePath`. Θυμηθείτε να διατηρείτε τη **κύρια λέξη‑κλειδί** στο μυαλό: κάθε φορά που αλλάζετε μορφή, εξακολουθείτε να *εκτελείτε OCR* σε μια νέα πηγή.

### Βελτίωση Ακρίβειας Κατά την **Εξαγωγή Αραβικού Κειμένου**  

- **Προ‑επεξεργασία της εικόνας**: αυξήστε την αντίθεση, διορθώστε την κλίση ή εφαρμόστε ένα δυαδικό κατώφλι.  
- **Ορίστε υψηλότερο DPI**: πολλές μηχανές OCR απαιτούν τουλάχιστον 300 dpi για καθαρούς χαρακτήρες.  
- **Χρησιμοποιήστε πακέτα γλώσσας**: κάποιες βιβλιοθήκες επιτρέπουν τη φόρτωση προσαρμοσμένου αραβικού λεξικού για ειδικούς όρους.

### Διαχείριση Μεγάλων Παρτίδων (Εξαγωγή Κειμένου JPG σε Βρόχους)  

Αν έχετε φάκελο γεμάτο JPEGs, τυλίξτε το βήμα αναγνώρισης σε έναν βρόχο `foreach`:

```csharp
foreach (var file in Directory.GetFiles("./Images", "*.jpg"))
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

Αυτό το μοτίβο σας επιτρέπει να **μετατρέψετε εικόνα σε κείμενο** σε κλίμακα χωρίς να ξαναγράψετε κώδικα.

### Όταν η Μηχανή Επιστρέφει Κενά Αποτελέσματα  

- Επαληθεύστε ότι η εικόνα δεν είναι πολύ σκοτεινή ή θολή.  
- Ελέγξτε ότι το μοντέλο γλώσσας Αραβικά έχει φορτωθεί σωστά (ορισμένα πακέτα απαιτούν ξεχωριστή λήψη).  
- Δοκιμάστε διαφορετικό πάροχο OCR· ο Tesseract, για παράδειγμα, συχνά διαχειρίζεται καλύτερα εικόνες χαμηλής ανάλυσης.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα  

Αντιγράψτε το παρακάτω απόσπασμα σε ένα νέο έργο κονσόλας (`dotnet new console -n ArabicOcrDemo`). Περιλαμβάνει όλες τις απαραίτητες δηλώσεις `using`, διαχείριση σφαλμάτων και μια σύντομη επικεφαλίδα σχολίου.

```csharp
// ArabicOcrDemo.csproj
// <Project Sdk="Microsoft.NET.Sdk">
//   <PropertyGroup>
//     <OutputType>Exe</OutputType>
//     <TargetFramework>net6.0</TargetFramework>
//   </PropertyGroup>
//   <ItemGroup>
//     <PackageReference Include="SimpleOcr" Version="1.2.3" />
//   </ItemGroup>
// </Project>

using System;
using SimpleOcr;   // Replace with your actual OCR library namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic
        };

        // 2️⃣ Path to the JPEG containing Arabic text
        string imagePath = @"./Images/arabic_sign.jpg";

        // 3️⃣ Run recognition with graceful error handling
        OcrResult result;
        try
        {
            result = ocrEngine.RecognizeImage(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
            return;
        }

        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(result.Text);

        // 5️⃣ Optional: persist the text for later use
        System.IO.Directory.CreateDirectory("./output");
        System.IO.File.WriteAllText("./output/extracted_text.txt", result.Text);
    }
}
```

Τρέξτε το με:

```bash
dotnet run --project ArabicOcrDemo.csproj
```

Θα πρέπει να δείτε τη φράση στα Αραβικά να εκτυπώνεται στην κονσόλα και να αποθηκεύεται στο `./output/extracted_text.txt`.

## Συμπέρασμα  

Τώρα γνωρίζετε **πώς να εκτελείτε OCR** σε αραβικές εικόνες, πώς να **εξάγετε αραβικό κείμενο**, και πώς να **διαβάσετε κείμενο εικόνας** από ένα JPEG και **να μετατρέψετε εικόνα σε κείμενο** σε μια καθαρή, παραγωγικά‑έτοιμη εφαρμογή C# κονσόλας. Η τρι-βήμα ροή—ρύθμιση μηχανής, αναγνώριση εικόνας, και διαχείριση αποτελεσμάτων—καλύπτει τον πυρήνα κάθε εργασίας OCR, ανεξάρτητα από τη γλώσσα ή τον τύπο αρχείου.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αλλάξετε τη γλώσσα σε Αγγλικά, να τροφοδοτήσετε ένα PDF, ή να ενσωματώσετε το αποτέλεσμα με ένα API μετάφρασης. Μπορείτε επίσης να εξερευνήσετε **εξαγωγή κειμένου jpg** αρχείων παράλληλα χρησιμοποιώντας `Parallel.ForEach` για τεράστιες βάσεις δεδομένων.

Έχετε ερωτήσεις σχετικά με περιπτώσεις άκρων, βελτιστοποίηση απόδοσης ή εναλλακτικές βιβλιοθήκες; Αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}