---
category: general
date: 2026-04-29
description: Πώς να εκτελέσετε OCR σε C# χρησιμοποιώντας το Aspose OCR – εξαγωγή κειμένου
  στα Χίντι, αναγνώριση κειμένου από PNG και αλλαγή της γλώσσας OCR εν κινήσει.
draft: false
keywords:
- how to perform OCR
- extract Hindi text
- multi language OCR
- recognize text from PNG
- change OCR language
language: el
og_description: Πώς να εκτελέσετε OCR σε C# με το Aspose OCR. Μάθετε πώς να εξάγετε
  κείμενο στα Χίντι, να αναγνωρίζετε κείμενο από αρχεία PNG και να αλλάζετε τη γλώσσα
  OCR δυναμικά.
og_title: Πώς να εκτελέσετε OCR σε C# – Πλήρης πολυγλωσσικός οδηγός
tags:
- OCR
- C#
- Aspose
title: Πώς να εκτελέσετε OCR σε C# – Οδηγός πολλαπλών γλωσσών
url: /el/net/ocr-configuration/how-to-perform-ocr-in-c-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε C# – Οδηγός Πολλαπλών Γλωσσών

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε εικόνες που περιέχουν περισσότερες από μία γλώσσες; Ίσως έχετε μια ρωσική απόδειξη και ένα φυλλάδιο στα Χίντι δίπλα-δίπλα, και χρειάζεστε το κείμενο και από τα δύο χωρίς να χρησιμοποιήσετε ξεχωριστά εργαλεία. Αυτό είναι ένα κοινό πρόβλημα για όποιον ασχολείται με διεθνή έγγραφα.  

Σε αυτό το σεμινάριο θα σας δείξουμε έναν καθαρό, ολοκληρωμένο τρόπο για **να εκτελέσετε OCR** με το Aspose OCR, να εξάγετε κείμενο στα Χίντι, να αναγνωρίσετε κείμενο από αρχεία PNG και ακόμη **να αλλάξετε τη γλώσσα OCR** εν κινήσει. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα κώδικα που λειτουργεί για οποιονδήποτε συνδυασμό υποστηριζόμενων γλωσσών.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη μηχανή Aspose OCR σε ένα έργο .NET.  
- Τη διαφορά μεταξύ στατικής διαμόρφωσης γλώσσας και εναλλαγής γλωσσών κατά το χρόνο εκτέλεσης.  
- Πώς να εξάγετε κείμενο στα Χίντι από μια εικόνα και γιατί η βιβλιοθήκη μπορεί να κατεβάσει αυτόματα τα πακέτα γλώσσας.  
- Συμβουλές για τη διαχείριση αρχείων PNG, την αντιμετώπιση ελλιπών μονάδων γλώσσας και την επίλυση κοινών προβλημάτων.

> **Συμβουλή επαγγελματία:** Αν ήδη χρησιμοποιείτε το Aspose OCR για μία γλώσσα, χρειάζεται μόνο να προσαρμόσετε μερικές γραμμές για να το μετατρέψετε σε **πολλαπλή γλώσσα OCR** λύση.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| .NET 6 ή νεότερο (ή .NET Framework 4.7+) | Το Aspose OCR στοχεύει σε σύγχρονες εκτελέσεις· παλαιότερες εκδόσεις μπορεί να μην υποστηρίζουν την αυτόματη λήψη πακέτων γλώσσας. |
| Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Παρέχει την κλάση `OcrEngine` και τα enums γλώσσας. |
| Δύο δείγματα εικόνων PNG (`russian.png` και `hindi.png`) σε γνωστό φάκελο | Δείχνει **αναγνώριση κειμένου από PNG** και **εξαγωγή κειμένου στα Χίντι** σε μία εκτέλεση. |
| Σύνδεση στο Internet (για την πρώτη φορά που ζητείται νέα γλώσσα) | Η βιβλιοθήκη κατεβάζει το απαιτούμενο μοντέλο γλώσσας κατ' απαίτηση. |

Δεν απαιτούνται επιπλέον δυαδικά αρχεία OCR ή εξωτερικά εργαλεία — το Aspose κάνει όλη τη βαριά δουλειά.

---

## Βήμα 1 – Εγκατάσταση Aspose OCR και Δημιουργία της Μηχανής

Πρώτα απ' όλα: προσθέστε το πακέτο Aspose OCR στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.OCR
```

Τώρα μπορούμε να δημιουργήσουμε ένα στιγμιότυπο `OcrEngine`. Σκεφτείτε τη μηχανή ως έναν έξυπνο σαρωτή που μπορεί να επαναρυθμιστεί κατά το χρόνο εκτέλεσης.

```csharp
using Aspose.OCR;
using System;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε τη μηχανή μόνο μία φορά; Η επαναχρησιμοποίηση του ίδιου αντικειμένου αποφεύγει το κόστος φόρτωσης των εγγενών βιβλιοθηκών OCR επανειλημμένα, κάτι που μπορεί να γίνει αισθητό σε μεγάλα παρτίδες.

---

## Βήμα 2 – Αναγνώριση Ρωσικού Κειμένου (Πρώτη Γλώσσα)

Πριν περάσουμε στα Χίντι, ας αποδείξουμε ότι η μηχανή λειτουργεί με μια γνωστή γλώσσα. Ορίζουμε τη γλώσσα σε Ρωσικά, φορτώνουμε ένα PNG και εκτυπώνουμε το αποτέλεσμα.

```csharp
        // Step 2: Configure the engine for Russian and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianImagePath = @"YOUR_DIRECTORY/russian.png";
        var russianOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianImagePath));
        Console.WriteLine("Russian: " + russianOcrResult.Text);
```

**Τι συμβαίνει στο παρασκήνιο;**  
`OcrEngine.LoadImage` διαβάζει το PNG σε εσωτερική μορφή bitmap του Aspose. Η ιδιότητα `Config.Language` λέει στη μηχανή OCR ποιο λεξικό και σύνολο χαρακτήρων να εφαρμόσει. Όταν καλείτε το `Recognize`, η μηχανή τρέχει ένα νευρωνικό μοντέλο ρυθμισμένο για κυριλλικούς χαρακτήρες και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το κείμενο σε απλό κείμενο.

> **Αναμενόμενο αποτέλεσμα (παράδειγμα)**  
> `Russian: Привет, мир! Это тестовое изображение.`

Αν δείτε ακατάλληλους χαρακτήρες, ελέγξτε ξανά ότι η εικόνα δεν είναι κατεστραμμένη και ότι το ρωσικό πακέτο γλώσσας είναι διαθέσιμο (συμπεριλαμβάνεται στο βασικό πακέτο).

---

## Βήμα 3 – Μετάβαση σε Χίντι – **Αλλαγή Γλώσσας OCR** Δυναμικά

Τώρα για το πιο διασκεδαστικό: η εναλλαγή γλώσσας χωρίς επαναδημιουργία της μηχανής. Το Aspose OCR θα κατεβάσει το πακέτο Χίντι την πρώτη φορά που το ζητήσετε, οπότε χρειάζεται μόνο μία σύνδεση στο Internet.

```csharp
        // Step 3: Switch the engine to Hindi (the language module will be downloaded automatically) and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiImagePath = @"YOUR_DIRECTORY/hindi.png";
        var hindiOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiImagePath));
        Console.WriteLine("Hindi: " + hindiOcrResult.Text);
    }
}
```

**Γιατί λειτουργεί αυτό;**  
Ο setter της ιδιότητας `Config.Language` ενεργοποιεί μια διαδικασία lazy‑load. Αν το ζητούμενο πακέτο γλώσσας δεν υπάρχει στον δίσκο, το Aspose επικοινωνεί με το CDN του, κατεβάζει το συμπιεσμένο μοντέλο, το αποθηκεύει στην cache και συνεχίζει με την αναγνώριση. Αυτός ο σχεδιασμός σας επιτρέπει να δημιουργήσετε **πολλαπλές γλώσσες OCR** pipelines που προσαρμόζονται στο περιεχόμενο κατά το χρόνο εκτέλεσης.

> **Δείγμα εξόδου στα Χίντι**  
> `Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।`

Παρατηρήστε πώς το ίδιο αντικείμενο `ocrEngine` διαχειρίζεται τόσο κυριλλικά όσο και ντεβανάγκαρι σενάρια χωρίς προβλήματα. Αυτή είναι η δύναμη της **αλλαγής γλώσσας OCR** εν κινήσει.

---

## Βήμα 4 – Αποτελεσματική Διαχείριση Αρχείων PNG

Και τα δύο παραδείγματα χρησιμοποιούν εικόνες PNG, που είναι κοινή μορφή για στιγμιότυπα οθόνης και σαρωμένα έγγραφα. Το PNG είναι lossless, δηλαδή τα δεδομένα pixel παραμένουν αμετάβλητα — ιδανικό για OCR. Ωστόσο, μεγάλα PNG μπορούν να καταναλώνουν μνήμη. Εδώ είναι μερικές γρήγορες συμβουλές:

1. **Αλλαγή μεγέθους αν χρειάζεται** – Αν το πλάτος της εικόνας υπερβαίνει τα 2000 px, μειώστε το με `System.Drawing.Image` πριν το περάσετε στο Aspose.  
2. **Ορισμός DPI** – Ορισμένες μηχανές OCR ωφελούνται από DPI 300. Μπορείτε να το ενσωματώσετε μέσω του overload του `OcrEngine.LoadImage` που δέχεται ένα `Bitmap` με προσαρμοσμένη ανάλυση.

```csharp
using System.Drawing;

// Example of downscaling a huge PNG
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/large.png");
int maxWidth = 2000;
if (original.Width > maxWidth)
{
    int newHeight = (int)((double)original.Height / original.Width * maxWidth);
    Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));
    original.Dispose(); // free original memory
    original = resized;
}
var result = ocrEngine.Recognize(OcrEngine.LoadImage(original));
```

Αυτές οι προσαρμογές διατηρούν τη χρήση μνήμης χαμηλή και συχνά βελτιώνουν την ακρίβεια, επειδή η μηχανή OCR εργάζεται με ένα πιο διαχειρίσιμο πλέγμα pixel.

---

## Βήμα 5 – Συνδυασμός Όλων – Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που δείχνει **πώς να εκτελέσετε OCR**, **να εξάγετε κείμενο στα Χίντι**, **να αναγνωρίσετε κείμενο από PNG** και **να αλλάξετε τη γλώσσα OCR** χωρίς επανεκκίνηση της μηχανής.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Create a single OCR engine instance (re‑use it for all languages)
        var ocrEngine = new OcrEngine();

        // ----------- Russian ----------
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianPath = @"YOUR_DIRECTORY/russian.png";
        var russianResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianPath));
        Console.WriteLine("Russian: " + russianResult.Text);

        // ----------- Hindi ------------
        // The first time this runs, the Hindi language pack will be downloaded automatically.
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiPath = @"YOUR_DIRECTORY/hindi.png";
        var hindiResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiPath));
        Console.WriteLine("Hindi: " + hindiResult.Text);

        // ----------- Optional PNG optimization ----------
        // If you have very large PNGs, resize them before recognition (example shown earlier).
        // This block is optional and can be removed if your images are already sized appropriately.
    }
}
```

**Η εκτέλεση του κώδικα** εκτυπώνει κάτι σαν:

```
Russian: Привет, мир! Это тестовое изображение.
Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।
```

Αν δείτε αυτές τις γραμμές, συγχαρητήρια — έχετε δημιουργήσει επιτυχώς μια **πολλαπλή γλώσσα OCR** λύση που μπορεί να **εξάγει κείμενο στα Χίντι** και **να αναγνωρίσει κείμενο από PNG** αρχεία με μία μόνο μηχανή.

---

## Συχνές Ερωτήσεις (FAQ)

| Ερώτηση | Απάντηση |
|----------|----------|
| *Χρειάζομαι άδεια για το Aspose OCR;* | Ένα δωρεάν κλειδί αξιολόγησης λειτουργεί για δοκιμές, αλλά η παραγωγική χρήση απαιτεί εμπορική άδεια. |
| *Μπορώ να αναγνωρίσω περισσότερες από δύο γλώσσες σε μία εικόνα;* | Ναι. Ορίστε `Config.Language` σε `OcrLanguage.Multiple` και περάστε μια λίστα χωρισμένη με κόμματα (π.χ., `Russian, Hindi`). |
| *Τι γίνεται αν το πακέτο γλώσσας αποτύχει να κατέβει;* | Ελέγξτε τις ρυθμίσεις firewall ή proxy. Μπορείτε επίσης να προ‑κατεβάσετε τα πακέτα από το portal του Aspose και να τα τοποθετήσετε στο φάκελο `Data`. |
| *Είναι το PNG η μόνη υποστηριζόμενη μορφή;* | Όχι. Το Aspose OCR υποστηρίζει επίσης JPEG, BMP, TIFF και PDF (ως εικόνες). Το PNG είναι απλώς μια κοινή επιλογή για απώλεια‑ποιότητας. |

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Επεξεργασία παρτίδας** – Επανάληψη σε έναν φάκελο PNG και αποθήκευση αποτελεσμάτων σε αρχείο CSV.  
- **Εξαγωγή από PDF** – Χρησιμοποιήστε `OcrEngine.RecognizePdf` για λήψη κειμένου από σαρωμένα PDF.  
- **Προσαρμοσμένα λεξικά** – Επεκτείνετε τα ενσωματωμένα πακέτα γλώσσας με λίστες λέξεων που παρέχονται από τον χρήστη για εξειδικευμένο λεξιλόγιο.  
- **Βελτιστοποίηση απόδοσης** – Παράλληλη εκτέλεση με `Parallel.ForEach` όταν εργάζεστε με μεγάλα σύνολα εικόνων.

Η εξερεύνηση αυτών των περιοχών θα εμβαθύνει την εξειδίκευσή σας στο **πώς να εκτελέσετε OCR** σε διαφορετικά σενάρια.

---

## Συμπέρασμα

Μάθατε **πώς να εκτελέσετε OCR** σε C# χρησιμοποιώντας το Aspose OCR, να αλλάζετε γλώσσες εν κινήσει και να **εξάγετε κείμενο στα Χίντι** από μια εικόνα PNG. Το βασικό συμπέρασμα είναι ότι ένα μόνο αντικείμενο `OcrEngine` μπορεί να λειτουργήσει ως ευέλικτος, **πολλαπλής γλώσσας OCR** μοχλός — απλώς ορίστε `Config.Language` και αφήστε τη βιβλιοθήκη να κάνει το υπόλοιπο.

Δοκιμάστε τον κώδικα, αντικαταστήστε τις δείγμα εικόνες με τις δικές σας και πειραματιστείτε με επιπλέον γλώσσες. Η ευελιξία του Aspose OCR σημαίνει ότι μπορείτε να κλιμακώσετε από ένα γρήγορο πρωτότυπο σε μια παραγωγική γραμμή επεξεργασίας εγγράφων με ελάχιστες αλλαγές.

Καλό κώδικα, και οι περιπέτειές σας στην εξαγωγή κειμένου να είναι χωρίς σφάλματα! 

![how to perform OCR example](/images/ocr-demo.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}