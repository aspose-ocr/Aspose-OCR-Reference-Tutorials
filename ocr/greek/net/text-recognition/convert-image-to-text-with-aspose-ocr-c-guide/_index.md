---
category: general
date: 2026-02-14
description: Μετατρέψτε εικόνα σε κείμενο χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε αραβικό κείμενο από μια εικόνα, να φορτώσετε την εικόνα για OCR και
  να αναγνωρίζετε αραβικά αποδοτικά.
draft: false
keywords:
- convert image to text
- extract text from picture
- how to extract arabic text
- load image for ocr
- how to recognize arabic
language: el
og_description: Μετατρέψτε την εικόνα σε κείμενο χρησιμοποιώντας το Aspose OCR σε
  C#. Αυτό το σεμινάριο δείχνει πώς να εξάγετε αραβικό κείμενο από μια εικόνα, να
  φορτώσετε την εικόνα για OCR και να αναγνωρίσετε τα αραβικά.
og_title: Μετατροπή εικόνας σε κείμενο με Aspose OCR – Οδηγός C#
tags:
- OCR
- C#
- Aspose
title: Μετατροπή εικόνας σε κείμενο με Aspose OCR – Οδηγός C#
url: /el/net/text-recognition/convert-image-to-text-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# μετατροπή εικόνας σε κείμενο με Aspose OCR – οδηγός C#

Θέλετε να **μετατρέψετε εικόνα σε κείμενο** σε μια εφαρμογή C#; Η μετατροπή εικόνας σε κείμενο είναι μια συνηθισμένη εργασία, ειδικά όταν χρειάζεται να **εξάγετε κείμενο από εικόνα** που περιέχει μη‑λατινικά σενάρια. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **πώς να εξάγετε αραβικό κείμενο**, πώς να **φορτώσετε εικόνα για OCR**, και τα ακριβή βήματα που χρειάζεστε για **να αναγνωρίσετε αραβικούς** χαρακτήρες χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση ειδικών περιπτώσεων όπως ελλιπείς γραμματοσειρές ή σαρώσεις χαμηλής ανάλυσης. Στο τέλος, θα έχετε ένα αυτόνομο πρόγραμμα που εκτυπώνει το αναγνωρισμένο αραβικό κείμενο στην κονσόλα — χωρίς εξωτερικά εργαλεία.

## Τι θα μάθετε

- Πώς να προσθέσετε το Aspose.OCR σε ένα .NET project (η πιο πρόσφατη έκδοση το 2026)
- Τον ακριβή κώδικα που απαιτείται για **μετατροπή εικόνας σε κείμενο** και γιατί κάθε γραμμή είναι σημαντική
- Συμβουλές για βελτίωση της ακρίβειας όταν δουλεύετε με αραβικά γλύφους
- Πώς να **φορτώσετε εικόνα για OCR** από διαδρομή αρχείου ή ροή
- Τρόπους αντιμετώπισης κοινών προβλημάτων (π.χ. λανθασμένη ρύθμιση γλώσσας, μη υποστηριζόμενη μορφή εικόνας)

> **Pro tip:** Αν στοχεύετε σε .NET 6 ή νεότερο, μπορείτε να χρησιμοποιήσετε δηλώσεις top‑level για να κάνετε τον κώδικα ακόμη πιο σύντομο. Το παρακάτω παράδειγμα παραμένει στην κλασική κλάση `Program` για μέγιστη συμβατότητα.

## Προαπαιτούμενα

- .NET 6 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET)
- Visual Studio 2022 ή VS Code με την επέκταση C#
- Πακέτο NuGet `Aspose.OCR` (εγκατάσταση μέσω `dotnet add package Aspose.OCR`)
- Ένα αρχείο εικόνας που περιέχει αραβικό κείμενο (π.χ. `arabic_sign.jpg`)

---

## Μετατροπή εικόνας σε κείμενο – Υλοποίηση βήμα‑βήμα

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο console project. Περιλαμβάνει **όλες τις απαραίτητες `using` δηλώσεις**, μια μέθοδο `Main`, και ενσωματωμένα σχόλια που εξηγούν το *γιατί* κάθε λειτουργία.

```csharp
// ------------------------------------------------------------
// Program.cs – Complete example to convert image to text
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine – this object holds the core logic.
            var ocrEngine = new Engine();

            // 2️⃣ Configure OCR options.
            //    We set the language to Arabic because the picture contains Arabic script.
            //    You can replace Language.Arabic with any other supported language.
            var ocrOptions = new OcrOptions
            {
                Language = Language.Arabic
            };

            // 3️⃣ Load the image you want to process.
            //    ImageStream.FromFile reads the file into a stream that Aspose can handle.
            //    If your image is in a different folder, adjust the path accordingly.
            var inputImage = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

            // 4️⃣ Run OCR – the Recognize method returns an OcrResult object.
            var ocrResult = ocrEngine.Recognize(inputImage, ocrOptions);

            // 5️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Αν το `arabic_sign.jpg` περιέχει τη φράση **"مطار دولي"** (σημαίνει “Διεθνές Αεροδρόμιο”), η κονσόλα θα εμφανίσει κάτι σαν:

```
=== OCR Result ===
مطار دولي
```

Η ακριβής ορθογραφία μπορεί να διαφέρει ελαφρώς ανάλογα με την ποιότητα της εικόνας, αλλά θα πρέπει να δείτε αραβικούς χαρακτήρες αντί για ακατανόητο κείμενο.

---

## Πώς να εξάγετε αραβικό κείμενο – ρύθμιση γλώσσας

Γιατί ορίζουμε ρητά `Language = Language.Arabic`; Το Aspose.OCR υποστηρίζει δεκάδες γλώσσες, αλλά η προεπιλογή είναι τα Αγγλικά. Τα Αραβικά χρησιμοποιούν δεξιά‑προς‑αριστερή γραφή και έχουν σχήμα χαρακτήρων που εξαρτάται από το πλαίσιο. Αναγγέλλοντας στη μηχανή τη σωστή γλώσσα, ενεργοποιείτε:

- **Ανίχνευση συνόδων** – χαρακτήρες που ενώνονται (π.χ. “لا”)
- **Δεξιά‑προς‑αριστερή διάταξη** – η έξοδος θα είναι σωστά προσανατολισμένη
- **Βελτιωμένο έλεγχο λεξικού** – η μηχανή μπορεί να διασταυρώνει αραβικές λίστες λέξεων για μεγαλύτερη ακρίβεια

Αν χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** που περιέχει πολλαπλές γλώσσες, μπορείτε να περάσετε έναν πίνακα `Language` enum στο `OcrOptions.Language` (π.χ. `new[] { Language.Arabic, Language.English }`).

---

## Φόρτωση εικόνας για OCR – ανάγνωση της εικόνας

Η γραμμή `ImageStream.FromFile(...)` είναι ο πιο απλός τρόπος για **φόρτωση εικόνας για OCR**. Ωστόσο, μπορεί να συναντήσετε σενάρια όπου:

- Η εικόνα βρίσκεται σε BLOB βάσης δεδομένων.
- Λαμβάνετε την εικόνα μέσω HTTP αιτήματος.
- Το αρχείο είναι σε μη‑τυπική μορφή (π.χ. TIFF με πολλαπλές σελίδες).

Σε αυτές τις περιπτώσεις, μπορείτε να δημιουργήσετε ένα `ImageStream` από ένα `MemoryStream`:

```csharp
byte[] bytes = System.IO.File.ReadAllBytes("path/to/image.png");
using var memStream = new System.IO.MemoryStream(bytes);
var inputImage = ImageStream.FromStream(memStream);
```

Και οι δύο προσεγγίσεις τροφοδοτούν την ίδια εσωτερική αναπαράσταση στη μηχανή, οπότε η ποιότητα του OCR παραμένει αμετάβλητη.

---

## Πώς να αναγνωρίσετε Αραβικά – εκτέλεση της μηχανής

Όταν καλείτε `ocrEngine.Recognize(inputImage, ocrOptions)`, η μηχανή εκτελεί αρκετά εσωτερικά στάδια:

1. **Προεπεξεργασία** – μείωση θορύβου, δυαδικοποίηση και διόρθωση κλίσης.
2. **Κατανομή** – διάσπαση της εικόνας σε γραμμές, λέξεις και χαρακτήρες.
3. **Ταξινόμηση** – αντιστοίχιση κάθε τμήματος με γνωστά αραβικά γλύφα.
4. **Μεταεπεξεργασία** – εφαρμογή κανόνων γλώσσας και ορίων εμπιστοσύνης.

Αν παρατηρήσετε χαμηλές τιμές εμπιστοσύνης, σκεφτείτε:

- **Αύξηση ανάλυσης εικόνας** (συνιστάται τουλάχιστον 300 dpi για Αραβικά).
- **Ρύθμιση αντίθεσης** πριν τη μεταφορά της εικόνας (χρησιμοποιήστε μια απλή βιβλιοθήκη επεξεργασίας εικόνας όπως `System.Drawing` ή `ImageSharp`).
- **Ενεργοποίηση `ocrOptions.UseLanguageDictionary = true`** για πιο αυστηρούς ελέγχους λεξικού.

---

## Συνηθισμένα προβλήματα & πώς να τα αποφύγετε

| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|----------|
| Κενή έξοδος | Λάθος διαδρομή αρχείου ή μη υποστηριζόμενη μορφή | Επαληθεύστε τη διαδρομή, χρησιμοποιήστε `File.Exists`, και βεβαιωθείτε ότι η εικόνα είναι PNG/JPEG/BMP |
| Παραμορφωμένοι χαρακτήρες | Η γλώσσα δεν έχει οριστεί στα Αραβικά | Ορίστε `Language = Language.Arabic` στο `OcrOptions` |
| Χαμηλή ακρίβεια | Η εικόνα είναι θολή ή χαμηλής ανάλυσης | Χρησιμοποιήστε πηγή υψηλότερης ανάλυσης ή εφαρμόστε φίλτρα ακονισμού |
| Εξαίρεση `ArgumentNullException` | `inputImage` είναι null | Βεβαιωθείτε ότι το αρχείο υπάρχει και η ροή ανοίγεται σωστά |

---

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή)

Αν προτιμάτε ένα μόνο αρχείο χωρίς namespaces, εδώ είναι μια συμπαγής έκδοση που εξακολουθεί να ακολουθεί τις βέλτιστες πρακτικές:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class ConvertImageToText
{
    static void Main()
    {
        // Engine creation
        var engine = new Engine();

        // Set OCR options – Arabic language
        var options = new OcrOptions { Language = Language.Arabic };

        // Load image – change the path to your actual file
        var image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

        // Perform recognition
        var result = engine.Recognize(image, options);

        // Show result
        Console.WriteLine("=== Recognized Arabic Text ===");
        Console.WriteLine(result.Text);
    }
}
```

Τρέξτε το πρόγραμμα με `dotnet run` και θα δείτε το αραβικό κείμενο να εκτυπώνεται στην κονσόλα.

---

## Οπτική ανασκόπηση

Παρακάτω υπάρχει μια εικονική λήψη οθόνης που απεικονίζει το αποτέλεσμα στην κονσόλα. Το **alt text** περιλαμβάνει τη βασική λέξη‑κλειδί για συμμόρφωση SEO.

![convert image to text example – console showing Arabic OCR result](convert-image-to-text-example.png)

---

## Συμπέρασμα

Δείξαμε πώς να **μετατρέψετε εικόνα σε κείμενο** χρησιμοποιώντας το Aspose OCR σε C#. Το tutorial κάλυψε τα πάντα, από την εγκατάσταση της βιβλιοθήκης, τη ρύθμιση της γλώσσας για **εξαγωγή αραβικού κειμένου**, τη φόρτωση της εικόνας, και τέλος **πώς να αναγνωρίσετε Αραβικούς** χαρακτήρες με μία μόνο κλήση μεθόδου.  

Με αυτή τη γνώση, μπορείτε τώρα να ενσωματώσετε OCR σε οποιοδήποτε .NET project — είτε είναι ένα desktop εργαλείο, ένα web API, ή μια υπηρεσία παρασκηνίου που επεξεργάζεται παρτίδες σαρωμένων εγγράφων.

### Τι ακολουθεί;

- Πειραματιστείτε με άλλες γλώσσες αλλάζοντας το `Language.Arabic` σε `Language.French`, `Language.ChineseSimplified`, κ.λπ.
- Συνδυάστε το OCR με **εξαγωγή κειμένου από εικόνα** pipelines που αποθηκεύουν τα αποτελέσματα σε βάση δεδομένων.
- Χρησιμοποιήστε την ιδιότητα `ocrResult.Confidence` για να φιλτράρετε γραμμές χαμηλής εμπιστοσύνης πριν τις αποθηκεύσετε.

Έχετε ερωτήσεις σχετικά με ειδικές περιπτώσεις ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο ή ρωτήστε στη συζήτηση. Καλό coding, και εύχομαι οι εικόνες σας πάντα να αποδίδουν καθαρό, αναζητήσιμο κείμενο!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}