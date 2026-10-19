---
category: general
date: 2026-02-09
description: Πώς να χρησιμοποιήσετε OCR σε C# για την αναγνώριση κειμένου από εικόνα,
  την εξαγωγή κειμένου και τη μετατροπή εικόνας σε κείμενο με το Aspose OCR. Πλήρης
  οδηγός βήμα‑προς‑βήμα.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# για να αναγνωρίσετε κείμενο από εικόνα,
  να εξάγετε κείμενο και να μετατρέψετε την εικόνα σε κείμενο με το Aspose OCR. Πλήρης
  οδηγός με κώδικα.
og_title: Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνώριση κειμένου από εικόνες
tags:
- C#
- Aspose OCR
- Image Processing
title: Πώς να χρησιμοποιήσετε OCR σε C# – Αναγνώριση κειμένου από εικόνες
url: /el/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε OCR σε C# – Αναγνώριση Κειμένου από Εικόνες

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε OCR** για να μετατρέψετε ένα στιγμιότυπο οθόνης σε επεξεργάσιμο κείμενο; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζεται να *αναγνωρίσουν κείμενο από εικόνα* αρχεία αλλά δεν έχουν ένα σαφές, έτοιμο‑για‑εκτέλεση παράδειγμα.  

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία — φόρτωση άδειας, δημιουργία μηχανής, παροχή ροής εικόνας, και τελικά εξαγωγή απλού κειμένου. Στο τέλος θα μπορείτε να **εξάγετε κείμενο από εικόνα**, **μετατρέψετε εικόνα σε κείμενο**, και ακόμη να κατανοήσετε τις λεπτομέρειες της διαχείρισης **φόρτωσης ροής εικόνας**.

> **Τι θα λάβετε:** ένα πλήρες, εκτελέσιμο πρόγραμμα C# που χρησιμοποιεί Aspose.OCR, εξηγήσεις κάθε βήματος, και συμβουλές για την αποφυγή κοινών παγίδων.

---

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το API λειτουργεί επίσης με .NET Framework 4.6+)  
- Πακέτο NuGet Aspose.OCR for .NET (`Aspose.OCR`) εγκατεστημένο  
- Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`) – η δωρεάν δοκιμή λειτουργεί αλλά προσθέτει υδατογράφημα.  
- Μια εικόνα (`sample.jpg`) που περιέχει καθαρό, μηχανικά αναγνώσιμο κείμενο.

> **Συμβουλή:** Εάν χρησιμοποιείτε Visual Studio, η εντολή κονσόλας NuGet είναι  
> `Install-Package Aspose.OCR -Version 23.10` (αντικαταστήστε με την τελευταία έκδοση).

---

## Πώς να Χρησιμοποιήσετε OCR: Φόρτωση Άδειας και Αρχικοποίηση της Μηχανής

Το πρώτο πράγμα που πρέπει να κάνετε είναι να ενημερώσετε την Aspose ότι έχετε άδεια. Αν παραλείψετε αυτό το βήμα, το πρόγραμμα θα τρέξει, αλλά θα εμφανιστεί υδατογράφημα στην έξοδο και θα σπαταλήσετε πολύτιμο χρόνο επεξεργασίας σε ελέγχους λειτουργίας δοκιμής.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**Γιατί είναι σημαντικό:** Το αντικείμενο `License` απενεργοποιεί το υδατογράφημα δοκιμής και ξεκλειδώνει το πλήρες σύνολο λειτουργιών, που περιλαμβάνει μοντέλα υψηλότερης ακρίβειας και υποστήριξη πολλαπλών γλωσσών.  

> **Pro tip:** Κρατήστε το αρχείο άδειας εκτός του αποθετηρίου ελέγχου πηγής. Χρησιμοποιήστε μεταβλητές περιβάλλοντος ή ασφαλή θησαυροφυλακή για να ενσωματώσετε τη διαδρομή κατά την εκτέλεση.

---

## Βήμα 2 – Φόρτωση Ροής Εικόνας (και γιατί είναι καλύτερο από διαδρομή αρχείου)

Όταν *φορτώνετε ροή εικόνας* αντί να περάσετε μια ακατέργαστη διαδρομή αρχείου, κερδίζετε ευελιξία: η εικόνα μπορεί να προέρχεται από μια βάση δεδομένων, ένα αίτημα web, ή έναν πίνακα byte στη μνήμη.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**Εξήγηση:** Το `ImageStream` αφαιρεί την αφηρημένη πηγή, επιτρέποντας στη μηχανή OCR να αντιμετωπίζει τα πάντα ομοιόμορφα. Αν αργότερα αλλάξετε σε κουβά αποθήκευσης cloud, χρειάζεται μόνο να αλλάξετε τον τρόπο δημιουργίας του `ImageStream`; το υπόλοιπο του κώδικα παραμένει αμετάβλητο.

---

## Βήμα 3 – Αναγνώριση Κειμένου από Εικόνα

Τώρα έρχεται η ουσία: **αναγνωρίστε κείμενο από εικόνα**. Η μέθοδος `OcrEngine.Recognize` εκτελεί τα μοντέλα νευρωνικών δικτύων που παρέχονται με την Aspose και επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει πολλές χρήσιμες ιδιότητες.

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**Τι περιέχει το `OcrResult`;**  
- `PlainText` – μια ενιαία συμβολοσειρά με όλους τους ανιχνευμένους χαρακτήρες.  
- `Words` – μια συλλογή αντικειμένων λέξεων με πλαίσια οριοθέτησης (χρήσιμο για επισήμανση).  
- `Lines` – ομαδοποίηση κατά γραμμή, χρήσιμη για διατήρηση διακοπών παραγράφων.

Αν χρειάζεστε μόνο ακατέργαστο κείμενο, το `PlainText` είναι η πιο γρήγορη διαδρομή. Για πιο προχωρημένα σενάρια (π.χ., επικάλυψη αποτελεσμάτων στην αρχική εικόνα), εξερευνήστε τα `Words` και `Lines`.

---

## Βήμα 4 – Εμφάνιση ή Αποθήκευση του Εξαγόμενου Κειμένου

Τέλος, ας εμφανίσουμε το αναγνωρισμένο κείμενο στην κονσόλα. Σε μια πραγματική εφαρμογή μπορεί να γράψετε σε βάση δεδομένων, αρχείο ή να το στείλετε μέσω API.

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**Αναμενόμενη έξοδος:**  
Αν το `sample.jpg` περιέχει την πρόταση *«Hello World!»*, θα δείτε:

```
=== OCR Output ===
Hello World!
==================
```

Όταν χρησιμοποιείτε άδεια δοκιμής, η έξοδος θα περιλαμβάνει ένα μικρό υδατογράφημα “Aspose OCR Demo” στο τέλος του κειμένου. Με πλήρη άδεια, αυτό εξαφανίζεται εντελώς.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε τις διαδρομές με τις δικές σας τοποθεσίες και είστε έτοιμοι.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **Θυμηθείτε:** Ο παραπάνω κώδικας **εξάγει κείμενο από εικόνα** και **μετατρέπει εικόνα σε κείμενο** με μία κλήση. Χωρίς επιπλέον βρόχους, χωρίς χειροκίνητη διαχείριση pixel — η Aspose κάνει το σκληρό έργο.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα μου είναι θολή ή χαμηλής αντίθεσης;

Η Aspose OCR περιλαμβάνει επιλογές προεπεξεργασίας (π.χ., `ocrEngine.ImagePreprocessor`). Μπορείτε να ενεργοποιήσετε τη δυαδικοποίηση ή την ευθυγράμμιση πριν την αναγνώριση:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### Πώς να διαχειριστώ πολλαπλές γλώσσες;

Ορίστε την ιδιότητα `Language` στη μηχανή:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Η μηχανή θα προσπαθήσει τότε να ανιχνεύσει και τις δύο γλώσσες αυτόματα.

### Μπορώ να επεξεργαστώ PDF αντί για JPEG;

Ναι — η Aspose OCR μπορεί να διαβάσει PDF απευθείας, αλλά θα χρειαστείτε τη βιβλιοθήκη Aspose.PDF για να εξάγετε κάθε σελίδα ως εικόνα πρώτα, και στη συνέχεια να τροφοδοτήσετε τη ροή εικόνας στη μηχανή OCR.

### Τι γίνεται με μεγάλες παρτίδες;

Τυλίξτε τη λογική αναγνώρισης σε βρόχο και επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`. Η δημιουργία νέας μηχανής ανά εικόνα προσθέτει περιττό κόστος.

---

## Pro Συμβουλές για Παραγωγική OCR

- **Αποθηκεύστε στην cache το αντικείμενο άδειας**: Φορτώστε το μία φορά κατά την εκκίνηση της εφαρμογής, όχι ανά αίτημα.  
- **Επαναχρησιμοποιήστε το `OcrEngine`**: Η μηχανή διατηρεί εσωτερικές προσωρινές μνήμες· η επαναχρήση μειώνει την πίεση στο GC.  
- **Περιορίστε το μέγεθος της εικόνας**: Πολύ μεγάλες εικόνες (>5 MP) αυξάνουν δραματικά το χρόνο επεξεργασίας. Μειώστε την ανάλυση σε 150‑300 DPI αν δεν απαιτείται υψηλή ανάλυση.  
- **Επικυρώστε την έξοδο**: Η OCR δεν είναι τέλεια· υλοποιήστε έναν απλό έλεγχο εμπιστοσύνης (`ocrResult.Words.Average(w => w.Confidence)`) και σημειώστε αποτελέσματα χαμηλής εμπιστοσύνης για χειροκίνητη ανασκόπηση.  
- **Ασφάλεια νήματος**: Το `OcrEngine` δεν είναι ασφαλές για πολλαπλά νήματα. Δημιουργήστε ξεχωριστές στιγμιότυπες ανά νήμα ή χρησιμοποιήστε μοτίβο πισίνας.

---

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε OCR** σε C# από τη φόρτωση άδειας μέχρι την εξαγωγή καθαρού, αναζητήσιμου κειμένου. Ακολουθώντας τα παραπάνω βήματα μπορείτε να **αναγνωρίσετε κείμενο από εικόνα**, **εξάγετε κείμενο από εικόνα**, και χωρίς κόπο **μετατρέψετε εικόνα σε κείμενο** ενώ κυριαρχείτε το πρότυπο **φόρτωσης ροής εικόνας** που κάνει τον κώδικά σας ευέλικτο για μελλοντικές πηγές δεδομένων.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε περικοπή περιοχής ενδιαφέροντος, να ενσωματώσετε με Azure Blob storage, ή να τροφοδοτήσετε την έξοδο OCR σε pipeline επεξεργασίας φυσικής γλώσσας. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για να χτίσετε.

![Διάγραμμα που δείχνει τη ροή OCR: φόρτωση άδειας → δημιουργία μηχανής → φόρτωση ροής εικόνας → αναγνώριση → έξοδο κειμένου](image-placeholder.png "πώς να χρησιμοποιήσετε OCR για να αναγνωρίσετε κείμενο από εικόνα")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}