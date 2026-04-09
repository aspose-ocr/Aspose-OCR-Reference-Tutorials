---
category: general
date: 2026-04-08
description: Εξαγωγή κειμένου από εικόνα με το Aspose OCR σε C#. Μάθετε πώς να προεπεξεργαστείτε
  την εικόνα για OCR και πώς να προεπεξεργαστείτε την εικόνα ώστε να βελτιώσετε την
  ακρίβεια.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Αυτός
  ο οδηγός δείχνει πώς να προεπεξεργαστείτε την εικόνα για OCR και πώς να προεπεξεργαστείτε
  την εικόνα για τα καλύτερα αποτελέσματα.
og_title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποσυμπίεση Κειμένου από Εικόνα με Aspose OCR – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **αποσπάσετε κείμενο από εικόνα** αλλά τα αποτελέσματα ήταν γεμάτα σφάλματα; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν η πηγή εικόνας είναι λοξή, θορυβώδης ή χαμηλής αντίθεσης. Τα καλά νέα είναι ότι μια σύντομη διαδικασία προεπεξεργασίας μπορεί να μετατρέψει μια ασταθή λήψη σε καθαρή πηγή για OCR, και το Aspose OCR κάνει όλο το έργο παιχνιδάκι.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει **πώς να προεπεξεργαστείτε εικόνα για OCR** χρησιμοποιώντας τα ενσωματωμένα φίλτρα του Aspose OCR, και στη συνέχεια **να αποσπάσετε κείμενο από εικόνα** με λίγες μόνο γραμμές C#. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα, θα καταλάβετε γιατί κάθε φίλτρο είναι σημαντικό, και θα ξέρετε πώς να ρυθμίσετε τη σειρά για τις δικές σας περιπτώσεις.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)
- Το πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Μια δείγμα εικόνας που είναι λοξή, θορυβώδης ή χαμηλής αντίθεσης (π.χ., `skewed_noisy.jpg`)
- Οποιοδήποτε IDE προτιμάτε—Visual Studio, Rider ή VS Code αρκεί

Καμία επιπλέον εγγενής βιβλιοθήκη, καμία υπηρεσία web, μόνο καθαρό C#.

## Βήμα 1: Ρύθμιση του OCR Engine – Το Αφετηριακό Σημείο για την Απόσπαση Κειμένου

Πρώτα απ’ όλα: δημιουργήστε ένα αντικείμενο `OcrEngine` και ορίστε τη γλώσσα που θα αναζητήσει. Τα Αγγλικά είναι τα πιο συχνά, αλλά μπορείτε να αντικαταστήσετε το `"en"` με `"fr"`, `"de"` κ.λπ.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Γιατί είναι σημαντικό:** Η μηχανή διατηρεί εσωτερικά λεξικά και γλωσσικές ευρετικές. Αν παραλείψετε τον ορισμό της γλώσσας, το Aspose προεπιλέγει τα Αγγλικά, αλλά η ρητή δήλωση αποτρέπει εκπλήξεις όταν αλλάξετε τοπικές ρυθμίσεις.

## Βήμα 2: Δημιουργία Αλυσίδας Προεπεξεργασίας – Πώς να Προεπεξεργαστείτε Εικόνα για Βέλτιστα Αποτελέσματα

Τώρα προσθέτουμε φίλτρα. Σκεφτείτε τα ως ένα μικρό σύνολο επεξεργασίας φωτογραφίας που εκτελείται αυτόματα πριν το βήμα OCR. Τα τρία φίλτρα παρακάτω καλύπτουν τα πιο κοινά προβλήματα:

| Φίλτρο | Τι διορθώνει | Πότε να το χρησιμοποιήσετε |
|--------|--------------|----------------------------|
| `DeskewFilter` | Περιστρέφει την εικόνα πίσω στην οριζόντια θέση | Εικόνες που λήφθηκαν υπό γωνία |
| `DenoiseFilter` | Μειώνει τυχαίες κηλίδες και θόρυβο | Φωτογραφίες χαμηλού φωτισμού ή σαρωμένα έγγραφα |
| `ContrastStretchFilter` | Αυξάνει την αντίθεση, κάνοντας το σκοτεινό κείμενο πιο εμφανές | Ασθενείς εκτυπώσεις ή ξεθωριασμένες λήψεις οθόνης |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Pro tip:** Η σειρά έχει σημασία. Πρώτα Deskew, μετά Denoise, και τέλος ContrastStretch. Αν τα αντιστρέψετε, μπορεί να ενισχύσετε τον θόρυβο αντί να τον αφαιρέσετε.

## Βήμα 3: Εκτέλεση του OCR – Τέλος, Απόσπαση Κειμένου από Εικόνα

Με τη σειρά έτοιμη, δώστε στη μηχανή τη διαδρομή της εικόνας σας. Το Aspose θα εφαρμόσει αυτόματα τα φίλτρα και στη συνέχεια θα τρέξει τον αλγόριθμο αναγνώρισης.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Αν το αρχείο δεν βρεθεί, θα λάβετε ένα σαφές `FileNotFoundException`. Γι’ αυτό συνιστούμε τη χρήση απόλυτων διαδρομών κατά την ανάπτυξη, και μετά τη μετάβαση σε σχετικές διαδρομές ή τιμές ρυθμίσεων για παραγωγή.

## Βήμα 4: Εμφάνιση του Αποτελέσματος – Δείτε Τι Παράχθηκε

Το αντικείμενο `OcrResult` περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη τα πλαίσια περιορισμού κάθε λέξης. Για μια γρήγορη επίδειξη θα εκτυπώσουμε απλώς το κείμενο στην κονσόλα.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά την ποιότητα της εικόνας ή πειραματιστείτε με επιπλέον φίλτρα (π.χ., `BinarizationFilter` για δυαδικές εικόνες).

## Πλήρες Παράδειγμα – Αντιγραφή‑Επικόλληση και Εκτέλεση

Παρακάτω είναι το πλήρες, αυτόνομο πρόγραμμα. Απλώς αντικαταστήστε το `YOUR_DIRECTORY/skewed_noisy.jpg` με τη σωστή διαδρομή της δοκιμαστικής σας εικόνας.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Αναμενόμενη έξοδος** – Η κονσόλα θα εκτυπώσει την απλή κειμενική αναπαράσταση του περιεχομένου της εικόνας. Αν η εικόνα περιέχει μια απλή πινακίδα με τη λέξη “OpenAI”, θα δείτε ακριβώς αυτή τη λέξη, χωρίς επιπλέον σύμβολα.

## Περιπτώσεις Ορίων & Πώς να Ρυθμίσετε τη Σειρά

### 1️⃣ Πολύ Σκοτεινές Εικόνες

Αν το φίλτρο αντίθεσης δεν αρκεί, προσθέστε ένα `BrightnessCorrectionFilter`:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Πολυγλωσσικά Έγγραφα

Ορίστε `Language = "en+fr"` (το Aspose υποστηρίζει κωδικούς γλωσσών χωρισμένους με κόμμα) και προσθέστε ένα `LanguageDetectionFilter` αν θέλετε η μηχανή να εντοπίζει αυτόματα τη γλώσσα.

### 3️⃣ Μεγάλα PDF που Μετατρέπονται σε Εικόνες

Η επεξεργασία χιλιετούς PDF μία εικόνα τη φορά μπορεί να είναι αργή. Χρησιμοποιήστε `Parallel.ForEach` για να τρέξετε OCR σε πολλαπλές εικόνες ταυτόχρονα, αλλά θυμηθείτε ότι το `OcrEngine` δεν είναι thread‑safe—δημιουργήστε ξεχωριστό στιγμιότυπο ανά νήμα.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Λήψη Πλαισίων Περιγράμματος

Αν χρειάζεστε τη θέση κάθε λέξης (π.χ., για επισήμανση), εξετάστε το `ocrResult.Regions`. Κάθε περιοχή περιέχει συντεταγμένες `Rectangle` που μπορείτε να χρησιμοποιήσετε σε UI overlay.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Συνηθισμένα Πιθανά Σφάλματα (Και Πώς να τα Αποφύγετε)

- **Παράλειψη του βήματος Deskew** – Ακόμη και μια κλίση 2 μοίρες μπορεί να μειώσει την εμπιστοσύνη κατά 20 %. Προσθέτε πάντα `DeskewFilter` όταν η πηγή δεν είναι τέλεια ευθυγραμμισμένη.
- **Χρήση JPEG με βαριά συμπίεση** – Τα τεχνουργήματα συμπίεσης μοιάζουν με θόρυβο· μεταβείτε σε PNG ή TIFF για καλύτερο OCR.
- **Σκληρός κώδικας διαδρομών** – Οι σχετικές διαδρομές λειτουργούν τοπικά, αλλά σε pipelines CI/CD θα θέλετε να διαβάζετε τη θέση της εικόνας από ρυθμίσεις ή μεταβλητές περιβάλλοντος.

## Δοκιμή της Ρύθμισης Σας

1. Εκτελέστε το πρόγραμμα με μια καθαρή, υψηλής αντίθεσης εικόνα. Θα πρέπει να λάβετε σχεδόν τέλειο κείμενο.  
2. Αντικαταστήστε το με μια θορυβώδη, λοξή φωτογραφία. Επαληθεύστε ότι η έξοδος βελτιώνεται μετά την προσθήκη των τριών φίλτρων.  
3. Πειραματιστείτε αφαιρώντας ένα φίλτρο τη φορά για να δείτε την επίδρασή του—αυτό σας βοηθά να καταλάβετε *γιατί* κάθε βήμα είναι σημαντικό.

## Συμπέρασμα

Δείξαμε πώς να **αποσπάσετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR, και παρουσιάσαμε έναν πρακτικό τρόπο **προεπεξεργασίας εικόνας για OCR** που λειτουργεί στις περισσότερες πραγματικές συνθήκες. Συνδέοντας τα `DeskewFilter`, `DenoiseFilter` και `ContrastStretchFilter` δίνετε στη μηχανή έναν καθαρό καμβά, βελτιώνοντας δραστικά την ακρίβεια.

Από εδώ μπορείτε να εξερευνήσετε πιο προχωρημένα φίλτρα, να διαχειριστείτε πολυσελίδες έγγραφα ή να ενσωματώσετε τα αποτελέσματα OCR σε ευρετήριο αναζήτησης. Ό,τι και αν επιλέξετε, το βασικό μοτίβο—αρχικοποίηση, προεπεξεργασία, αναγνώριση, και χρήση—παραμένει το ίδιο.

Έτοιμοι για επόμενη βήμα; Δοκιμάστε να προσθέσετε ένα `BinarizationFilter` για ασπρόμαυρες σαρώσεις, ή συνδέστε την έξοδο με μια βάση δεδομένων για αναζητήσιμα PDF. Καλό προγραμματισμό, και καλή επιτυχία με τις εικόνες σας στο Aspose!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}