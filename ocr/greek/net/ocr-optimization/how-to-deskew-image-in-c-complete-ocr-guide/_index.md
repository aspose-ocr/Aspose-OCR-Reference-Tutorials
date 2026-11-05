---
category: general
date: 2026-05-06
description: Μάθετε πώς να διορθώνετε την κλίση της εικόνας και να εξάγετε κείμενο
  από την εικόνα χρησιμοποιώντας το Aspose OCR – βήμα‑βήμα οδηγός για τη βελτίωση
  της ακρίβειας του OCR και πώς να αφαιρέσετε τον θόρυβο από την εικόνα.
draft: false
keywords:
- how to deskew image
- extract text from image
- how to use OCR
- improve OCR accuracy
- how to denoise image
language: el
og_description: Μάθετε πώς να διορθώνετε την κλίση μιας εικόνας και να εξάγετε κείμενο
  από εικόνα με το Aspose OCR. Αυτό το σεμινάριο δείχνει πώς να αφαιρείτε τον θόρυβο
  από την εικόνα και να βελτιώνετε την ακρίβεια του OCR.
og_title: Πώς να διορθώσετε την κλίση μιας εικόνας σε C# – Πλήρης οδηγός OCR
tags:
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση εικόνας σε C# – Πλήρης οδηγός OCR
url: /el/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση μιας εικόνας σε C# – Πλήρης Οδηγός OCR

Έχετε χρειαστεί ποτέ να **πώς να διορθώσετε την κλίση μιας εικόνας** πριν τρέξετε OCR, αλλά δεν ήσασταν σίγουροι ποια φίλτρα να εφαρμόσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν η πηγή φωτογραφίας είναι ελαφρώς λοξή ή θορυβώδης. Τα καλά νέα; Με λίγες γραμμές C# και Aspose.OCR μπορείτε να ευθυγραμμίσετε, να καθαρίσετε και τελικά να εξάγετε κείμενο από την εικόνα με εντυπωσιακή ακρίβεια.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: φόρτωση μιας λοξής εικόνας, εφαρμογή φίλτρων deskew και denoise, ενίσχυση της αντίθεσης, και τελικά εξαγωγή του κειμένου. Στο τέλος θα καταλάβετε **how to use OCR**, θα δείτε πώς να **improve OCR accuracy**, και θα έχετε ένα έτοιμο‑για‑εκτέλεση δείγμα κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Χρειαστείτε

- .NET 6 ή νεότερο (το API λειτουργεί με .NET Core και .NET Framework)
- Aspose.OCR για .NET (δωρεάν δοκιμή ή άδεια έκδοση) – μπορείτε να το αποκτήσετε από το NuGet με `Install-Package Aspose.OCR`
- Ένα δείγμα εικόνας που είναι λοξή και λίγο θορυβώδης (π.χ., `skewed_noisy.jpg`)
- Visual Studio, VS Code, ή οποιονδήποτε επεξεργαστή προτιμάτε

Δεν απαιτούνται επιπλέον εγγενείς βιβλιοθήκες· το Aspose διαχειρίζεται τα πάντα εσωτερικά.

## Βήμα 1: Ρυθμίστε το Project και Εγκαταστήστε το Aspose.OCR

### Δημιουργία νέας εφαρμογής console

```bash
dotnet new console -n DeskewOcrDemo
cd DeskewOcrDemo
```

### Προσθήκη του πακέτου Aspose.OCR

```bash
dotnet add package Aspose.OCR
```

Αυτό είναι—το project σας τώρα αναφέρεται στη μηχανή OCR και στα ενσωματωμένα φίλτρα που θα χρειαστούμε.

## Βήμα 2: Φορτώστε την Εικόνα που Θέλετε να Επεξεργαστείτε

Θα ξεκινήσουμε δημιουργώντας μια παρουσία `OcrEngine` και δείχνοντάς της το αρχείο που θέλουμε να καθαρίσουμε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // The rest of the pipeline will be added next…
    }
}
```

> **Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας είναι το πρώτο βήμα για οποιοδήποτε επόμενο φίλτρο. Αν η διαδρομή είναι λανθασμένη, ολόκληρη η αλυσίδα αποτυγχάνει σιωπηρά, οπότε ελέγξτε ξανά τη θέση.

## Βήμα 3: Δημιουργία Αλυσίδας Επεξεργασίας – Deskew, Denoise, Στη συνέχεια Ενίσχυση Αντίθεσης

Εδώ συμβαίνει η μαγεία. Θα προσθέσουμε τρία φίλτρα με τη συγκεκριμένη σειρά που αποδίδει τα καλύτερα αποτελέσματα OCR:

1. **DeskewFilter** – ευθυγραμμίζει την εικόνα.
2. **MedianDenoiseFilter** – αφαιρεί τυχαίες κηλίδες χωρίς να θολώνει τις άκρες.
3. **ContrastStretchFilter** – ενισχύει τη διαφορά μεταξύ κειμένου και φόντου.

```csharp
        // Step 3: Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy
```

> **Συμβουλή:** Η σειρά είναι κρίσιμη. Πρώτα το Deskew, επειδή μια κεκλιμένη εικόνα μπορεί να μπερδέσει το φίλτρο denoise. Αφού η εικόνα είναι όρθια, το median filter μπορεί να καθαρίσει το κόκκο, και τέλος το contrast stretch κάνει τα γράμματα να ξεχωρίζουν.

## Βήμα 4: Εκτέλεση Αναγνώρισης OCR

Τώρα αφήνουμε το Aspose να κάνει τη βαριά δουλειά. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο κείμενο και μερικές μετρικές εμπιστοσύνης.

```csharp
        // Step 4: Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // Optional: check confidence (0‑100). Higher means more reliable.
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

> **Πώς να χρησιμοποιήσετε το OCR:** Η κλήση `Recognize` εφαρμόζει εσωτερικά όλα τα φίλτρα που προσθέσαμε, και στη συνέχεια τρέχει τη μηχανή OCR. Δεν χρειάζεται να καλέσετε κάθε φίλτρο χειροκίνητα· η αλυσίδα το κάνει για εσάς.

## Βήμα 5: Εξαγωγή του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώνουμε το κείμενο στην κονσόλα. Σε πραγματικές εφαρμογές πιθανότατα θα το γράψετε σε αρχείο, βάση δεδομένων ή θα το περάσετε σε άλλη υπηρεσία.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to process
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 3️⃣ Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy

        // 4️⃣ Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Show confidence and extracted text
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Τρέξτε το με:

```bash
dotnet run
```

Θα πρέπει να δείτε ένα σκορ εμπιστοσύνης ακολουθούμενο από την απλή κειμενική έκδοση ό,τι υπήρχε στη αρχική σας φωτογραφία.

## Επαλήθευση του Αποτελέσματος – Τι να Περιμένετε

Αν η πηγή εικόνας περιέχει, για παράδειγμα, μια τυπωμένη γραμμή τιμολόγησης:

```
Invoice #12345
Total: $1,250.00
Date: 2024‑04‑30
```

Μετά την εκτέλεση της αλυσίδας, η κονσόλα θα εμφανίσει κάτι όπως:

```
Confidence: 96%
=== Extracted Text ===
Invoice #12345
Total: $1,250.00
Date: 2024-04-30
```

Μια υψηλή τιμή εμπιστοσύνης (συνήθως πάνω από 90%) υποδεικνύει ότι τα βήματα **how to deskew image** και **how to denoise image** βοήθησαν τη μηχανή OCR να δει τους χαρακτήρες καθαρά.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

### Τι γίνεται αν η εικόνα είναι περιστραμμένη περισσότερο από 45 μοίρες;

`DeskewFilter` ανιχνεύει αυτόματα τη γωνία έως ±45°. Για μεγαλύτερες περιστροφές, προ‑περιστρέψτε την εικόνα χρησιμοποιώντας `ocrEngine.Filters.Add(new RotateFilter(angle))` πριν το deskew.

### Η εμπιστοσύνη μου είναι χαμηλή—τι άλλο μπορώ να δοκιμάσω;

- Προσθέστε ένα **BinarizationFilter** για εξαναγκασμό μετατροπής σε ασπρόμαυρο.
- Αυξήστε την ακτίνα του **MedianDenoiseFilter**: `new MedianDenoiseFilter(3)`.
- Χρησιμοποιήστε πηγή εικόνας υψηλότερης ανάλυσης (300 dpi ή περισσότερο).

### Μπορώ να επεξεργαστώ πολλές εικόνες σε βρόχο;

Απόλυτα. Απλώς μετακινήστε τη δημιουργία του engine έξω από το βρόχο, καλέστε `SetImage` για κάθε αρχείο, και επαναχρησιμοποιήστε την ίδια συλλογή φίλτρων.

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    ocrEngine.SetImage(file);
    var result = ocrEngine.Recognize();
    // handle result...
}
```

### Λειτουργεί αυτό σε PDF;

Το Aspose.OCR μπορεί να διαβάσει σελίδες PDF ως εικόνες, αλλά θα χρειαστείτε τη βιβλιοθήκη Aspose.PDF για να εξάγετε κάθε σελίδα ως bitmap πρώτα.

## Συμβουλές για Μέγιστη Ακρίβεια OCR

1. **Κόψτε τα περιττά περιθώρια** – το επιπλέον κενό μπορεί να μπερδέσει τη μηχανή OCR.
2. **Χρησιμοποιήστε ομοιόμορφο φόντο** – το απλό λευκό ή ανοιχτό γκρι λειτουργεί καλύτερα.
3. **Αποφύγετε ακραίο φωτισμό** – οι σκιές δημιουργούν ψεύτικες άκρες που το φίλτρο denoise μπορεί να μην αφαιρέσει πλήρως.
4. **Δοκιμάστε με πραγματικά δείγματα** – τα συνθετικά δεδομένα φαίνονται καθαρά· οι εικόνες παραγωγής συχνά περιέχουν ελαττώματα.

## Συμπέρασμα

Μόλις καλύψαμε **how to deskew image**, **how to denoise image**, και τη πλήρη ροή του **how to use OCR** με το Aspose για **extract text from image** ενώ **improving OCR accuracy**. Ο κώδικας παραδείγματος είναι πλήρης, εκτελέσιμος, και έτοιμος για να τον προσαρμόσετε σε επεξεργασία παρτίδων, ενσωμάτωση UI ή υπηρεσίες cloud.

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε το `MedianDenoiseFilter` με ένα `GaussianDenoiseFilter` και συγκρίνετε τα σκορ εμπιστοσύνης, ή δώστε το εξαγόμενο κείμενο σε έναν parser φυσικής γλώσσας για αυτόματη συμπλήρωση φορμών. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε την αλυσίδα προεπεξεργασίας.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι κρυστάλλινα καθαρά! 

--- 

![παράδειγμα deskew εικόνας](/images/deskew-example.png "πώς να διορθώσετε την κλίση μιας εικόνας")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}