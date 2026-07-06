---
category: general
date: 2026-04-03
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε πώς
  να εξάγετε κείμενο από εικόνα, να αναγνωρίζετε κείμενο στα Χίντι, να φορτώνετε εικόνα
  για OCR και να ορίζετε τη γλώσσα OCR εύκολα.
draft: false
keywords:
- run OCR on image
- extract text from image
- recognize Hindi text
- load image for OCR
- set OCR language
language: el
og_description: Εκτελέστε OCR σε εικόνα σε C# με το Aspose OCR. Αυτός ο οδηγός δείχνει
  πώς να εξάγετε κείμενο από εικόνα, να αναγνωρίσετε κείμενο στα Χίντι, να φορτώσετε
  εικόνα για OCR και να ορίσετε τη γλώσσα του OCR.
og_title: Εκτέλεση OCR σε εικόνα με το Aspose – Πλήρης οδηγός C#
tags:
- Aspose
- C#
- OCR
title: Εκτέλεση OCR σε εικόνα με το Aspose σε C# – Πλήρης οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/run-ocr-on-image-with-aspose-in-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με Aspose σε C# – Πλήρης οδηγός

Έχετε ποτέ χρειαστεί να **run OCR on image** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας έδινε άμεσα αποτελέσματα; Δεν είστε οι μόνοι—οι προγραμματιστές διαχειρίζονται συνεχώς την προεπεξεργασία εικόνας, τα πακέτα γλωσσών και την περιστασιακή έλλειψη πόρων.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα έτοιμο‑για‑εκτέλεση παράδειγμα που **extracts text from image** αρχεία, σας δείχνει πώς να **recognize Hindi text**, και εξηγεί το μικρό‑αλλά‑καίριο βήμα του **loading image for OCR** ενώ **set OCR language** σωστά.

Στο τέλος θα έχετε μια μοναδική εφαρμογή κονσόλας C# που εξάγει κάθε εκτυπώσιμο χαρακτήρα από μια εικόνα, χωρίς να απαιτούνται χειροκίνητες λήψεις γλωσσών. Τα μόνα προαπαιτούμενα είναι ένα IDE συμβατό με .NET (Visual Studio, Rider ή VS Code) και μια άδεια Aspose OCR (ή μια δωρεάν δοκιμή).  

---

## Τι θα χρειαστείτε πριν ξεκινήσετε

- **Aspose.OCR for .NET** (πακέτο NuGet `Aspose.OCR`).  
- **.NET 6.0** ή νεότερο – το API λειτουργεί τόσο με .NET Core όσο και με .NET Framework.  
- Ένα δείγμα εικόνας που περιέχει γραφή Hindi (π.χ., `hindi_sign.jpg`).  
- Προαιρετικά: ένα έγκυρο αρχείο άδειας Aspose (`Aspose.Total.lic`) για να αποφύγετε υδατογραφήματα αξιολόγησης.  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—κάθε σημείο θα διευκρινιστεί καθώς προχωράμε.

---

## Βήμα 1: Εγκατάσταση του πακέτου Aspose OCR NuGet

Αρχικά, ανοίξτε το φάκελο του έργου σας σε ένα τερματικό και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, μπορείτε επίσης να κάνετε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε “Aspose.OCR” και κάντε κλικ στο **Install**.  

Αυτό φέρνει το `Aspose.OCR.dll` και όλες τις εξαρτήσεις του, παρέχοντάς σας πρόσβαση στην κλάση `OcrEngine` που θα χρειαστούμε για να **run OCR on image** δεδομένα.

---

## Βήμα 2: Δημιουργία νέου σκελετού εφαρμογής κονσόλας

Παρακάτω είναι ο πλήρης σκελετός του προγράμματος. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`. Τα σχόλια επισημαίνουν γιατί κάθε γραμμή είναι σημαντική.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – this object does all the heavy lifting.
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Enable auto‑download of language resources.
            //    If the Hindi pack isn’t present locally, Aspose will fetch it silently.
            ocrEngine.AutoDownloadResources = true;

            // 3️⃣ Set the OCR language to Hindi – this tells the engine what character set to expect.
            ocrEngine.Language = OcrLanguage.Hindi;

            // 4️⃣ Load the image you want to process.
            //    Replace the path with the actual location of your Hindi sign picture.
            Image sourceImage = Image.FromFile("YOUR_DIRECTORY/hindi_sign.jpg");

            // 5️⃣ Run the OCR process and capture the recognized text.
            string recognizedText = ocrEngine.Recognize(sourceImage);

            // 6️⃣ Output the result to the console.
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Γιατί το flag `AutoDownloadResources` είναι σημαντικό

Η Aspose παρέχει τα πακέτα γλωσσών ως ξεχωριστά αρχεία για να διατηρήσει τη βασική βιβλιοθήκη ελαφριά. Με το να θέσετε το `AutoDownloadResources` σε `true`, αποφεύγετε ένα *FileNotFoundException* την πρώτη φορά που προσπαθείτε να **recognize Hindi text**. Η μηχανή επικοινωνεί με το CDN της Aspose, κατεβάζει το μοντέλο Hindi, το αποθηκεύει τοπικά και προχωρά αυτόματα.

---

## Βήμα 3: Κατανόηση του πώς να **Load Image for OCR**

Η κλήση `Image.FromFile` είναι ο πιο απλός τρόπος για να φορτώσετε ένα bitmap στη μνήμη, αλλά υποθέτει ότι το αρχείο υπάρχει και είναι μορφή που υποστηρίζεται από το `System.Drawing`. Αν χρειαστεί να διαχειριστείτε PDFs, πολυ‑σελίδες TIFF ή απομακρυσμένα URLs, σκεφτείτε αυτές τις εναλλακτικές:

| Σενάριο | Συνιστώμενη προσέγγιση |
|----------|----------------------|
| **Large images** ( > 5 MB ) | Χρησιμοποιήστε `Image.FromStream` με ένα `FileStream` και ορίστε `Image.FromStream(stream, useEmbeddedColorManagement: false, validateImageData: false)` για να μειώσετε την πίεση μνήμης. |
| **Non‑BMP formats** (π.χ., WebP) | Μετατρέψτε πρώτα σε υποστηριζόμενη μορφή χρησιμοποιώντας `ImageMagick` ή `SkiaSharp`. |
| **Remote image** | Κατεβάστε με `HttpClient` → stream → `Image.FromStream`. |

Αυτές οι παραλλαγές εξασφαλίζουν ότι ο κώδικάς σας παραμένει ανθεκτικός, ειδικά όταν αργότερα **extract text from image** πηγές πέρα από το τοπικό σύστημα αρχείων.

---

## Βήμα 4: Εκτέλεση της εφαρμογής και επαλήθευση του αποτελέσματος

Συγκεντρώστε και εκτελέστε:

```bash
dotnet run
```

Αν όλα είναι συνδεδεμένα σωστά, θα πρέπει να δείτε κάτι όπως:

```
=== Recognized Text ===
स्वागत है
```

Το ακριβές αποτέλεσμα εξαρτάται από την ποιότητα του `hindi_sign.jpg`; πιο καθαρή σήμανση δίνει πιο καθαρά αποτελέσματα.  

### Κοινά προβλήματα και πώς να τα διορθώσετε

- **Missing language pack** – Ακόμη και με `AutoDownloadResources`, ένα εταιρικό firewall μπορεί να μπλοκάρει τη λήψη. Κατεβάστε χειροκίνητα το πακέτο Hindi από το portal της Aspose και τοποθετήστε το στο φάκελο `Resources` δίπλα στο εκτελέσιμο.  
- **Incorrect image path** – Ελέγξτε ξανά την ευαισθησία πεζών‑κεφαλαίων σε Linux/macOS· τα Windows είναι επιεική, αλλά τα άλλα λειτουργικά συστήματα όχι.  
- **Low‑resolution image** – Η ακρίβεια του OCR μειώνεται δραματικά κάτω από 300 dpi. Αυξήστε την ανάλυση της εικόνας χρησιμοποιώντας μια βιβλιοθήκη όπως `ImageSharp` πριν τη δώσετε στη μηχανή.

---

## Βήμα 5: Προαιρετικά – Αποθήκευση του αναγνωρισμένου κειμένου

Συχνά θα θέλετε να αποθηκεύσετε το αποτέλεσμα αντί να το εκτυπώσετε μόνο. Εδώ είναι ένα γρήγορο απόσπασμα που γράφει το κείμενο σε αρχείο UTF‑8:

```csharp
string outputPath = "output.txt";
File.WriteAllText(outputPath, recognizedText, System.Text.Encoding.UTF8);
Console.WriteLine($"Text saved to {Path.GetFullPath(outputPath)}");
```

Τώρα δεν έχετε μόνο **run OCR on image**, αλλά έχετε επίσης δημιουργήσει μια επαναχρησιμοποιήσιμη ροή εργασίας που μπορεί να ενσωματωθεί σε μεγαλύτερα συστήματα επεξεργασίας εγγράφων.

---

## Οπτική αναφορά

Παρακάτω είναι ένα εικονικό στιγμιότυπο της εξόδου της κονσόλας. Το κείμενο alt περιέχει σκόπιμα τη βασική λέξη-κλειδί για σκοπούς SEO.

![Παράδειγμα εξόδου OCR σε εικόνα](example.png "Εκτέλεση OCR σε εικόνα – αποτέλεσμα κονσόλας που εμφανίζει το αναγνωρισμένο κείμενο Hindi")

---

## Ανασκόπηση & Επόμενα βήματα

Καλύψαμε ολόκληρο τον κύκλο ζωής του **running OCR on an image** με την Aspose:

1. Εγκατάσταση του πακέτου NuGet.  
2. Αρχικοποίηση του `OcrEngine` και ενεργοποίηση του auto‑download.  
3. **Set OCR language** σε Hindi (ή οποιαδήποτε άλλη υποστηριζόμενη γλώσσα).  
4. **Load image for OCR** χρησιμοποιώντας `System.Drawing`.  
5. Κλήση του `Recognize` για **extract text from image**.  
6. Εξαγωγή ή αποθήκευση του αποτελέσματος.

Αν είστε άνετοι με τα Hindi, δοκιμάστε να αντικαταστήσετε το `OcrLanguage.Hindi` με `OcrLanguage.English`, `OcrLanguage.Arabic` ή οποιαδήποτε από τις 60+ γλώσσες που υποστηρίζει η Aspose.

### Πού να πάτε από εδώ;

- **Batch processing:** Επανάληψη σε έναν φάκελο εικόνων και εγγραφή κάθε αποτελέσματος σε ξεχωριστό αρχείο.  
- **Pre‑processing:** Εφαρμογή μετατροπής σε κλίμακα του γκρι, μείωσης θορύβου ή διόρθωσης κλίσης με `ImageSharp` πριν το OCR για βελτίωση της ακρίβειας.  
- **Integration:** Ενσωμάτωση του βήματος OCR σε ένα API ASP.NET Core ώστε οι πελάτες να μπορούν να ανεβάζουν εικόνες και να λαμβάνουν κείμενο κωδικοποιημένο σε JSON.  

Μη διστάσετε να πειραματιστείτε—το OCR είναι εκπληκτικά ανεκτικό μόλις κατακτήσετε τα βασικά.

---

### Συχνές ερωτήσεις

**Q: Λειτουργεί αυτό σε .NET Framework 4.8;**  
A: Ναι. Το ίδιο σύνολο `Aspose.OCR` στοχεύει τόσο το .NET Core όσο και το .NET Framework. Απλώς αλλάξτε το αρχείο έργου στο κατάλληλο target framework.

**Q: Τι γίνεται αν χρειαστεί να αναγνωρίσω πολλαπλές γλώσσες στην ίδια εικόνα;**  
A: Ορίστε `ocrEngine.Language = OcrLanguage.MultiLanguage;` και προαιρετικά περάστε μια συμβολοσειρά χωρισμένη με κόμμα κωδικών γλωσσών μέσω `ocrEngine.Language = OcrLanguage.FromString("Hindi,English");`.

**Q: Μπορώ να το τρέξω σε Linux;**  
A: Απόλυτα—απλώς βεβαιωθείτε ότι το πακέτο `libgdiplus` είναι εγκατεστημένο, επειδή το `System.Drawing.Common` εξαρτάται από αυτό για πλατφόρμες εκτός των Windows.

**Έτοιμοι να χρησιμοποιήσετε τις νέες σας δεξιότητες OCR;** Πάρτε μερικές πολυγλωσσικές πινακίδες, προσαρμόστε την ιδιότητα `Language` και δείτε την Aspose να μετατρέπει εικόνες σε κείμενο αναζητήσιμο σε δευτερόλεπτα. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}