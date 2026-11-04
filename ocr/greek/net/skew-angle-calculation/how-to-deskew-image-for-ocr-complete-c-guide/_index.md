---
category: general
date: 2026-01-06
description: Μάθετε πώς να διορθώνετε την κλίση της εικόνας, να αφαιρείτε τον θόρυβο
  και να εξάγετε κείμενο με το Aspose OCR. Ο οδηγός βήμα‑προς‑βήμα δείχνει επίσης
  πώς να φορτώνετε εικόνα για OCR.
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: el
og_description: Μάθετε πώς να διορθώνετε την κλίση της εικόνας, να αφαιρείτε τον θόρυβο
  και να εξάγετε κείμενο με το Aspose OCR. Ο οδηγός βήμα‑προς‑βήμα δείχνει επίσης
  πώς να φορτώνετε την εικόνα για OCR.
og_title: Πώς να διορθώσετε την κλίση της εικόνας για OCR – Πλήρης οδηγός C#
tags:
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση εικόνας για OCR – Πλήρης οδηγός C#
url: /el/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διορθώσετε την Κλίση μιας Εικόνας για OCR – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί **πώς να διορθώσετε την κλίση μιας εικόνας** πριν τη δώσετε σε μια μηχανή OCR; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν μια σαρωμένη φωτογραφία είναι ελαφρώς κλινή, θορυβώδης ή απλώς δύσκολη στην ανάγνωση. Το καλό νέο; Με το Aspose OCR μπορείτε να ευθυγραμμίσετε, να καθαρίσετε και στη συνέχεια να εξάγετε το κείμενο με λίγες γραμμές C#.

Σε αυτό το tutorial θα δούμε **πώς να εξάγουμε κείμενο**, **πώς να αφαιρέσουμε τον θόρυβο**, και, φυσικά, **πώς να διορθώσετε την κλίση μιας εικόνας** ώστε τα αποτελέσματα OCR να είναι ακριβή. Στο τέλος θα γνωρίζετε επίσης **πώς να φορτώσετε εικόνα για OCR** και θα έχετε καθαρά, αναζητήσιμα strings έτοιμα για την εφαρμογή σας.

---

## Τι Θα Χρειαστείτε

- **Aspose.OCR for .NET** (v23.12 ή νεότερη). Το πακέτο NuGet είναι `Aspose.OCR`.
- .NET 6+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί).
- Ένα δείγμα εικόνας που είναι κλινή ή με σπασμένα σημεία, π.χ. `skewed_photo.jpg`.
- Visual Studio, Rider ή ο αγαπημένος σας επεξεργαστής.

Δεν απαιτούνται επιπλέον native βιβλιοθήκες—το Aspose διαχειρίζεται τα πάντα εντός της διαδικασίας.

---

## Βήμα 1 – Ρύθμιση του OCR Engine (Αναγνώριση Κειμένου από Εικόνα)

Πριν μπορέσουμε **να φορτώσουμε εικόνα για OCR**, χρειαζόμαστε μια παρουσία του engine και τη γλώσσα που θέλουμε να διαβάσουμε.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**Γιατί είναι σημαντικό:** Το `OcrEngine` είναι η καρδιά της διαδικασίας. Ορίζοντας το `Language` νωρίς διασφαλίζουμε ότι ο αλγόριθμος αναγνώρισης χρησιμοποιεί το σωστό σύνολο χαρακτήρων, βελτιώνοντας δραματικά την ακρίβεια.

---

## Βήμα 2 – Φόρτωση της Εικόνας σας (Φόρτωση Εικόνας για OCR)

Τώρα δείχνουμε στο engine το αρχείο στο δίσκο. Αυτή είναι η στιγμή που πολλά tutorials σταματούν, αλλά θα συζητήσουμε επίσης κοινές παγίδες.

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **Συμβουλή:** Χρησιμοποιήστε απόλυτη διαδρομή κατά τη δοκιμή, μετά μεταβείτε σε σχετική διαδρομή ή ενσωματωμένο πόρο για παραγωγή. Επίσης, βεβαιωθείτε ότι η εικόνα είναι σε υποστηριζόμενη μορφή (JPEG, PNG, BMP, TIFF). Αν λάβετε σφάλμα “Unsupported format”, ελέγξτε ξανά την επέκταση του αρχείου και τον MIME τύπο.

---

## Βήμα 3 – Προεπεξεργασία: Διόρθωση Κλίσης και Αφαίρεση Θορύβου (Πώς να Διορθώσετε την Κλίση της Εικόνας & Πώς να Αφαιρέσετε τον Θόρυβο)

Ένα κλινό έγγραφο είναι κλασικό εφιάλτης για OCR. Το Aspose προσφέρει ένα `DeskewFilter` που ανιχνεύει αυτόματα την περιστροφή έως μια ρυθμιζόμενη γωνία. Συνδυάστε το με `DespeckleFilter` για να καθαρίσετε τον θόρυβο αλατιού‑και‑πιπεριού.

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### Πώς Λειτουργεί το Deskew Filter
Το φίλτρο σαρώει την εικόνα για κυρίαρχες βάσεις κειμένου, υπολογίζει τη γωνία κλίσης και περιστρέφει το bitmap ανάλογα. Αν η εικόνα είναι ήδη επίπεδη, το φίλτρο δεν κάνει τίποτα—έτσι μπορείτε να το προσθέτετε με ασφάλεια σε οποιοδήποτε pipeline.

### Πώς Βοηθά το Despeckle Filter
Ο θόρυβος εμφανίζεται συχνά ως απομονωμένα σκοτεινά ή φωτεινά pixel. Ο αλγόριθμος despeckle εφαρμόζει ένα median filter, διατηρώντας τις άκρες (όπως τα στίγματα των χαρακτήρων) ενώ εξομαλύνει τα σπασμένα σημεία. Πολύ μεγάλη ισχύς μπορεί να θολώσει λεπτομέρειες, γι’ αυτό ξεκινήστε με `Strength = 3` και προσαρμόστε ανάλογα με το υλικό σας.

> **Σημείωση:** Αν οι εικόνες σας έχουν ακραία περιστροφή (>15°), αυξήστε το `MaxAngle`. Για έγγραφα που έχουν σαρωθεί ανάποδα, ίσως χρειαστεί ένα προσαρμοσμένο βήμα περιστροφής πριν το φίλτρο deskew.

---

## Βήμα 4 – Εκτέλεση Αναγνώρισης (Αναγνώριση Κειμένου από Εικόνα)

Με την προεπεξεργασία στη θέση της, ζητάμε τελικά από το engine να διαβάσει το κείμενο.

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### Τι Συμβαίνει Πίσω από τις Σκηνές;
1. **Binarization:** Μετατρέπει την εικόνα σε ασπρόμαυρη, ενισχύοντας την αντίθεση.
2. **Segmentation:** Διαχωρίζει το bitmap σε γραμμές, λέξεις και χαρακτήρες.
3. **Classification:** Συγκρίνει κάθε χαρακτήρα με ένα εκπαιδευμένο μοντέλο (αγγλικό αλφάβητο, ψηφία, σημεία στίξης).
4. **Post‑processing:** Εφαρμόζει κανόνες γλώσσας (π.χ. ορθογραφικό έλεγχο) για να βελτιώσει την αναγνωσιμότητα.

Επειδή έχουμε ήδη **διορθώσει την κλίση της εικόνας** και **αφαιρέσει τον θόρυβο**, κάθε στάδιο λαμβάνει πιο καθαρά δεδομένα, κάτι που μεταφράζεται σε λιγότερα λάθη αναγνώρισης.

---

## Βήμα 5 – Επαλήθευση και Καθαρισμός του Αποτελέσματος (Πώς να Εξάγετε Κείμενο Αποτελεσματικά)

Το ακατέργαστο string μπορεί να περιέχει περιττά line breaks ή κενά. Ένας γρήγορος καθαρισμός κάνει τα δεδομένα έτοιμα για επεξεργασία.

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**Γιατί να το καθαρίσετε;** Πολλές βιβλιοθήκες OCR διατηρούν την αρχική διάταξη, κάτι που είναι χρήσιμο για PDFs αλλά δημιουργεί «θόρυβο» σε pipelines απλού κειμένου. Η κανονικοποίηση των κενών εξασφαλίζει ότι μπορείτε να αποθηκεύσετε το αποτέλεσμα σε βάση δεδομένων ή να το στείλετε σε ευρετήριο αναζήτησης χωρίς επιπλέον δουλειά.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το ολοκληρωμένο πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση. Αποθηκεύστε το ως `Program.cs`, προσθέστε το πακέτο NuGet Aspose.OCR και τρέξτε.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι η δείγμα εικόνα περιέχει τη φράση “Hello World”):

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

Αν η εικόνα είναι πολύ κλινή, θα δείτε ακατάστατους χαρακτήρες πριν προσθέσετε το `DeskewFilter`. Μετά το φίλτρο, το κείμενο γίνεται αναγνώσιμο—ακριβώς αυτό που θέλαμε να πετύχουμε.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν η εικόνα μου είναι περιστραμμένη περισσότερο από 15°;* | Αυξήστε το `MaxAngle` στο `DeskewFilter`. Τιμές μέχρι 45° είναι ασφαλείς, αλλά ακραίες γωνίες μπορεί να χρειάζονται χειροκίνητη περιστροφή πρώτα (`Image.Rotate(angle)`). |
| *Το OCR εξακολουθεί να χάνει γράμματα μετά το despeckling.* | Δοκιμάστε μεγαλύτερο `Strength` (4‑5) ή προσθέστε ένα `ContrastFilter` πριν το despeckling. |
| *Μπορώ να επεξεργαστώ PDFs απευθείας;* | Ναι—χρησιμοποιήστε `PdfDocument` για να αποδώσετε κάθε σελίδα σε εικόνα, μετά τροφοδοτήστε κάθε bitmap στο ίδιο pipeline. |
| *Είναι το engine thread‑safe;* | Δημιουργήστε ξεχωριστό `OcrEngine` ανά νήμα· η κλάση δεν εγγυάται thread‑safety. |
| *Πώς διαχειρίζομαι έγγραφα πολλαπλών γλωσσών;* | Ορίστε `ocrEngine.Language = OcrLanguage.Multilingual` ή αλλάξτε τη γλώσσα ανά σελίδα. |

---

## Συμβουλές για Παραγωγική OCR

1. **Batch Processing:** Περάστε μέσα από έναν φάκελο εικόνων, επαναχρησιμοποιώντας την ίδια παρουσία `OcrEngine` για να μειώσετε το κόστος.  
2. **Logging:** Καταγράψτε το `ocrEngine.LastError` όταν το `Recognize()` επιστρέφει false· συχνά δείχνει προβλήματα με μη υποστηριζόμενες μορφές ή κατεστραμμένα αρχεία.  
3. **Performance:** Το βήμα deskew είναι το πιο απαιτητικό σε CPU. Αν γνωρίζετε ότι οι εικόνες είναι ήδη επίπεδες, μπορείτε να παραλείψετε το φίλτρο.  
4. **Memory Management:** Αποδεσμεύστε τα αντικείμενα `ImageStream` μετά τη χρήση (`ocrEngine.Image.Dispose()`) για να αποφύγετε διαρροές μνήμης σε υπηρεσίες μακράς διάρκειας.

---

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση μιας εικόνας**, **πώς να αφαιρέσετε τον θόρυβο**, **πώς να φορτώσετε εικόνα για OCR**, και **πώς να εξάγετε κείμενο** χρησιμοποιώντας το Aspose OCR σε C#. Με την προεπεξεργασία μέσω `DeskewFilter` και `DespeckleFilter`, βελτιώνετε δραστικά τις πιθανότητες το `Recognize()` να επιστρέψει καθαρά, αναζητήσιμα strings.

Από την πρώτη γραμμή κώδικα μέχρι το τελικό καθαρό αποτέλεσμα, τα βήματα είναι απλά, αλλά αρκετά ισχυρά για πραγματικές εφαρμογές—είτε χτίζετε μια υπηρεσία αρχειοθέτησης εγγράφων, μια εφαρμογή σάρωσης αποδείξεων για κινητά, ή ένα backend μαζικής επεξεργασίας.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε ένα **βήμα ανίχνευσης γλώσσας**, ή πειραματιστείτε με **προσαρμοσμένα OCR λεξικά** για να αυξήσετε την ακρίβεια σε βιομηχανικές ορολογίες. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Καλό κώδικα, και εύχομαι οι εικόνες σας πάντα να είναι τέλεια ευθυγραμμισμένες! 

![Εικονογράφηση ενός διορθωμένου εγγράφου μετά τη διόρθωση κλίσης](deskewed_example.png "πώς να διορθώσετε την κλίση μιας εικόνας")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}