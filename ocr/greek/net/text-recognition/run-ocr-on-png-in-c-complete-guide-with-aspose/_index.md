---
category: general
date: 2026-02-16
description: Εκτελέστε OCR σε PNG γρήγορα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο, να διαβάζετε κείμενο PNG και να αναγνωρίζετε κείμενο PNG
  με έναν βήμα‑βήμα οδηγό.
draft: false
keywords:
- run OCR on PNG
- how to extract text
- read text png
- recognize text png
- ocr tutorial c#
language: el
og_description: Εκτελέστε OCR σε PNG με το Aspose OCR σε C#. Αυτό το σεμινάριο σας
  δείχνει πώς να εξάγετε κείμενο, να διαβάζετε κείμενο PNG και να αναγνωρίζετε κείμενο
  PNG βήμα προς βήμα.
og_title: Εκτέλεση OCR σε PNG με C# – Πλήρης Οδηγός
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Εκτέλεση OCR σε PNG σε C# – Πλήρης Οδηγός με το Aspose
url: /el/net/text-recognition/run-ocr-on-png-in-c-complete-guide-with-aspose/
---

as is. Good.

Now produce final output with all translated content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε PNG με C# – Πλήρης Οδηγός με Aspose

Έχετε χρειαστεί ποτέ να **run OCR on PNG** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—οι προγραμματιστές ρωτούν συνεχώς *how to extract text* από υψηλής ανάλυσης στιγμιότυπα, αποδείξεις ή σαρωμένα διαγράμματα. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πρακτική, ολοκληρωμένη λύση που σας επιτρέπει να **run OCR on PNG** χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR, όλα σε απλό C#.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου NuGet μέχρι την ενεργοποίηση της επιτάχυνσης GPU, τη φόρτωση του μοντέλου αγγλικής γλώσσας, και τελικά την εκτύπωση της αναγνωρισμένης συμβολοσειράς στην κονσόλα. Στο τέλος θα γνωρίζετε ακριβώς **how to extract text** από οποιοδήποτε PNG, πώς να **read text PNG** αποδοτικά, και θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα **OCR tutorial C#** που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Τι Θα Μάθετε

- Εγκατάσταση και διαμόρφωση του Aspose.OCR για .NET.
- Ενεργοποίηση της επιτάχυνσης υλικού για ταχύτερη επεξεργασία.
- Φόρτωση μοντέλων γλώσσας και παροχή μιας εικόνας PNG στη μηχανή.
- Καταγραφή και εμφάνιση του αποτελέσματος, αντιμετωπίζοντας κοινά προβλήματα.
- Επέκταση του παραδείγματος σε άλλες γλώσσες ή μορφές εικόνας.

**Prerequisites:** .NET 6 ή νεότερο, Visual Studio 2022 (ή το αγαπημένο σας IDE), και μια συμβατή GPU αν θέλετε την προαιρετική επιτάχυνση. Δεν απαιτείται προηγούμενη εμπειρία OCR.

---

## Εκτέλεση OCR σε PNG – Ρύθμιση του Περιβάλλοντος

Πριν βουτήξουμε στον κώδικα, ας βεβαιωθούμε ότι το περιβάλλον ανάπτυξης είναι έτοιμο. Αυτό το βήμα είναι κρίσιμο· ένα ελλιπές πακέτο ή ασυμφωνία χρόνου εκτέλεσης θα κάνει ολόκληρο το tutorial να καταρρεύσει.

1. **Δημιουργήστε ένα νέο έργο console**  
   ```bash
   dotnet new console -n OcrPngDemo
   cd OcrPngDemo
   ```

2. **Προσθέστε το πακέτο NuGet Aspose.OCR**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **(Optional) Verify GPU support** – Εάν διαθέτετε GPU NVIDIA ή AMD που υποστηρίζει CUDA/OpenCL, εγκαταστήστε τους κατάλληλους οδηγούς. Η βιβλιοθήκη θα ανιχνεύσει αυτόματα το υλικό όταν ορίσετε `HardwareAcceleration.Gpu`.

Αυτό είναι όλο. Ένα νέο έργο με τη βιβλιοθήκη OCR είναι τώρα έτοιμο να **run OCR on PNG** αρχεία.

## Πώς να Εξάγετε Κείμενο – Αρχικοποίηση της Μηχανής OCR

Η πρώτη πραγματική γραμμή κώδικα δημιουργεί μια παρουσία `OcrEngine`. Σκεφτείτε τη μηχανή ως τον εγκέφαλο πίσω από τη λειτουργία· διατηρεί τις ρυθμίσεις, τα μοντέλα γλώσσας και τις ρυθμίσεις υλικού.

```csharp
using Aspose.OCR;

// Step 1: Initialize the OCR engine (default CPU mode)
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί το δημιουργούμε χειροκίνητα αντί να χρησιμοποιήσουμε έναν static βοηθό;  
Επειδή μας δίνει πλήρη έλεγχο πάνω στο **how to extract text**—μπορούμε να ενεργοποιήσουμε/απενεργοποιήσουμε το GPU, να αλλάξουμε τη γλώσσα ή να ανταλλάξουμε την πηγή εικόνας σε πραγματικό χρόνο. Σε μεγαλύτερες εφαρμογές μπορεί να διατηρείτε μια singleton μηχανή για να αποφύγετε την επαναφόρτωση μοντέλων.

## Ανάγνωση PNG Κειμένου με Επιτάχυνση GPU

Εάν επεξεργάζεστε υψηλής ανάλυσης στιγμιότυπα, το OCR μόνο με CPU μπορεί να είναι αργό. Η ενεργοποίηση της επιτάχυνσης GPU μειώνει δευτερόλεπτα από κάθε εκτέλεση.

```csharp
// Step 2: Enable GPU acceleration for faster processing (requires compatible GPU)
ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;
```

*Pro tip:* Εάν το μηχάνημά σας δεν διαθέτει συμβατή GPU, η παραπάνω γραμμή θα επιστρέψει ήρεμα σε λειτουργία CPU. Δεν θα ριχτεί εξαίρεση, ώστε να διατηρήσετε τον κώδικα αμετάβλητο σε διαφορετικά περιβάλλοντα.

## Φόρτωση Μοντέλου Γλώσσας – Παράδειγμα “English”

Το Aspose περιλαμβάνει ένα μοντέλο English από προεπιλογή, αλλά μπορείτε να φορτώσετε άλλα (French, German, κλ.) με μία κλήση. Η φόρτωση του μοντέλου είναι προαπαιτούμενο για **recognize text PNG**· χωρίς αυτό η μηχανή δεν θα ξέρει ποιο σύνολο χαρακτήρων να περιμένει.

```csharp
// Step 3: Load the language model you need (English is included by default)
ocrEngine.LoadLanguage(LanguageModel.English);
```

Εάν χρειαστεί ποτέ να **read text PNG** σε άλλη γλώσσα, αντικαταστήστε το `LanguageModel.English` με την κατάλληλη τιμή enum.

## Παροχή της Εικόνας – Από Αρχείο σε Stream

Τώρα παραδίδουμε το αρχείο PNG στη μηχανή. Η βοηθητική μέθοδος `ImageStream.FromFile` διαβάζει το αρχείο στη μνήμη και υποστηρίζει πολλές μορφές, αλλά το PNG είναι η εστία μας.

```csharp
// Step 4: Provide the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/high_res_image.png");
```

Βεβαιωθείτε ότι η διαδρομή δείχνει σε ένα πραγματικό PNG· διαφορετικά θα λάβετε `FileNotFoundException`. Για γρήγορη δοκιμή, τοποθετήστε ένα στιγμιότυπο οθόνης από ένα τυπωμένο τιμολόγιο στον φάκελο και αναφέρετέ το εδώ.

## Αναγνώριση Text PNG – Εκτέλεση της Λειτουργίας OCR

Με όλα συνδεδεμένα, η πραγματική κλήση OCR είναι μια ενιαία μέθοδος. Η μέθοδος επιστρέφει μια συμβολοσειρά που περιέχει όλους τους εξαγόμενους χαρακτήρες, διατηρώντας τις αλλαγές γραμμής όπου είναι δυνατόν.

```csharp
// Step 5: Run the OCR operation and capture the recognized text
string recognizedText = ocrEngine.Recognize();
```

Γιατί λειτουργεί αυτή η ενιαία κλήση;  
Πίσω από τις σκηνές η μηχανή εκτελεί μια σειρά σταδίων: προεπεξεργασία (αφαίρεση θορύβου, δυαδικοποίηση), τμηματοποίηση (διαχωρισμός σε γραμμές και χαρακτήρες) και τέλος ταξινόμηση χρησιμοποιώντας ένα μοντέλο deep‑learning. Όλα αυτά τα βαριά βήματα είναι κρυμμένα από εσάς, γι' αυτό το API φαίνεται τόσο ελαφρύ.

## Εμφάνιση του Αποτελέσματος – Επαλήθευση του Output

Τέλος, εκτυπώνουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να γράψετε σε βάση δεδομένων, να τροφοδοτήσετε έναν δείκτη αναζήτησης ή να περάσετε τη συμβολοσειρά σε άλλη υπηρεσία.

```csharp
// Step 6: Display the OCR result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

Όταν εκτελέσετε το πρόγραμμα θα πρέπει να δείτε κάτι όπως:

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Εάν το output φαίνεται ακατάστατο, ελέγξτε ξανά την ποιότητα της εικόνας (αντίθεση, προσανατολισμός) και σκεφτείτε να ενεργοποιήσετε το `ocrEngine.PreprocessOptions` για πρόσθετες ρυθμίσεις.

## Πλήρης OCR Tutorial C# – Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι ο **πλήρης, εκτελέσιμος** κώδικας που συνδυάζει όλα τα κομμάτια. Αντιγράψτε‑επικολλήστε το στο `Program.cs`, αντικαταστήστε τη διαδρομή της εικόνας και πατήστε **F5**.

```csharp
using System;
using Aspose.OCR;

namespace OcrPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize the OCR engine (CPU by default)
            OcrEngine ocrEngine = new OcrEngine();

            // Enable GPU acceleration if a compatible GPU is present
            ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;

            // Load the English language model (default)
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Specify the PNG image to process
            string imagePath = "YOUR_DIRECTORY/high_res_image.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR and retrieve the recognized text
            string recognizedText = ocrEngine.Recognize();

            // Output the result to the console
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**Expected output:** Η κονσόλα εκτυπώνει τους ακριβείς χαρακτήρες που βρέθηκαν στο PNG, διατηρώντας τις αλλαγές γραμμής. Εάν η εικόνα περιέχει μόνο αριθμούς, θα δείτε μια σειρά ψηφίων· εάν περιέχει μεικτή γλώσσα, θα λάβετε τους κατάλληλους χαρακτήρες Unicode.

> **Note:** Το παραπάνω πρόγραμμα λειτουργεί με οποιοδήποτε PNG, JPEG ή BMP εφόσον η διαδρομή του αρχείου είναι σωστή. Για **read text PNG** από stream (π.χ., από web API), αντικαταστήστε το `ImageStream.FromFile` με `ImageStream.FromBytes(byteArray)`.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το PNG μου είναι περιστραμμένο;

Το Aspose.OCR μπορεί να περιστρέφει αυτόματα τις εικόνες. Προσθέστε:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.ImageOrientation = ImageOrientation.AutoDetect;
```

### Πώς να διαχειριστώ μεγάλες παρτίδες;

Τυλίξτε τη μηχανή σε ένα μπλοκ `using` και επαναχρησιμοποιήστε την σε πολλά αρχεία:

```csharp
using (var engine = new OcrEngine())
{
    engine.LoadLanguage(LanguageModel.English);
    foreach (var file in Directory.GetFiles(folder, "*.png"))
    {
        engine.Image = ImageStream.FromFile(file);
        string text = engine.Recognize();
        // Process text...
    }
}
```

### Μπορώ να εξάγω κείμενο από εικόνα χαμηλής αντίθεσης;

Ενεργοποιήστε την προεπεξεργασία:

```csharp
ocrEngine.PreprocessOptions = PreprocessOptions.EnhanceContrast | PreprocessOptions.Denoise;
```

### Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;

Ναι—`ocrEngine.RecognizeWithDetails()` επιστρέφει μια συλλογή από αντικείμενα `OcrResult`, το καθένα περιέχει μια ιδιότητα `Confidence`.

## Οπτικό Παράδειγμα

<img src="https://example.com/ocr-output.png" alt="Παράδειγμα εξόδου Run OCR on PNG που δείχνει το εξαγόμενο κείμενο τιμολογίου">

*Το κείμενο alt περιλαμβάνει τη βασική λέξη‑κλειδί, ικανοποιώντας τις απαιτήσεις SEO.*

## Συμπέρασμα

Τώρα έχετε μια ισχυρή ροή εργασίας **run OCR on PNG** που λειτουργεί αμέσως με το Aspose.OCR. Ακολουθώντας αυτό το **OCR tutorial C#**, μπορείτε να **how to extract text**, **read text PNG**, και **recognize text PNG** σε λίγες μόνο γραμμές κώδικα. Η υποστήριξη GPU της μηχανής, η φόρτωση γλώσσας και το απλό API την καθιστούν λύση‑πρώτο για κάθε προγραμματιστή .NET που χρειάζεται να μετατρέπει εικόνες σε αναζητήσιμο κείμενο.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `LanguageModel.English` με άλλη γλώσσα, πειραματιστείτε με το `PreprocessOptions` για θορυβώδεις σαρώσεις, ή ενσωματώστε το αποτέλεσμα σε έναν δείκτη πλήρους κειμένου. Οι δυνατότητες είναι απεριόριστες, και ο κώδικας που μόλις γράψατε είναι μια επαναχρησιμοποιήσιμη βάση για όλες αυτές τις περιπέτειες.

Εάν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose για πιο προχωρημένες επιλογές διαμόρφωσης. Καλή προγραμματιστική, και απολαύστε τη μετατροπή αυτών των επίμονων PNG σε επεξεργάσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}