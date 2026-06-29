---
category: general
date: 2026-06-28
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose.OCR σε C#. Μάθετε να
  αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο από τιμολόγιο, να φορτώνετε
  εικόνα για OCR και να γράφετε JSON σε αρχείο.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα με το Aspose.OCR σε C#. Αυτός ο οδηγός δείχνει
  πώς να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο από τιμολόγιο και να
  γράψετε JSON σε αρχείο.
og_title: Εκτέλεση OCR σε εικόνα με C# – Εκπαιδευτικό σεμινάριο Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: Εκτέλεση OCR σε εικόνα με C# – Πλήρης οδηγός Aspose
url: /el/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε εικόνα με C# – Πλήρης Οδηγός Aspose

Έχετε χρειαστεί ποτέ να **εκτελέσετε OCR σε εικόνα** αρχεία αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη .NET θα σας έδινε καθαρά, δομημένα αποτελέσματα; Δεν είστε μόνοι—οι προγραμματιστές συχνά ρωτούν πώς να **αναγνωρίσουν κείμενο από εικόνα** πόρους, ειδικά όταν δουλεύουν με τιμολόγια ή αποδείξεις. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που όχι μόνο **φορτώνει εικόνα για OCR**, αλλά επίσης **εξάγει κείμενο από δεδομένα τιμολογίου** και **γράφει JSON σε αρχείο** για επεξεργασία downstream.

Στο τέλος αυτού του οδηγού θα έχετε μια έτοιμη‑για‑εκτέλεση εφαρμογή κονσόλας που:

* Δημιουργεί μια μηχανή Aspose OCR,
* Φορτώνει μια εικόνα PNG (ή JPG),
* Αναγνωρίζει το κειμενικό περιεχόμενο,
* Σειριοποιεί το αποτέλεσμα ως μορφοποιημένο JSON,
* Αποθηκεύει αυτό το JSON στο δίσκο.

Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφή μαγεία—απλώς καθαρός κώδικας C# που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε.

## Προαπαιτούμενα

* .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί με .NET Core και .NET Framework εξίσου).
* Ένα έγκυρο άδεια Aspose.OCR ή ένα προσωρινό κλειδί αξιολόγησης (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
* Visual Studio 2022, VS Code ή οποιοδήποτε IDE προτιμάτε.
* Ένα αρχείο εικόνας—π.χ. `invoice.png`—τοποθετημένο κάπου που μπορείτε να το αναφέρετε με πλήρη ή σχετική διαδρομή.

> **Συμβουλή:** Εάν εργάζεστε με σαρωμένα τιμολόγια, σκεφτείτε την προεπεξεργασία της εικόνας (απλοποίηση κλίσης, ενίσχυση αντίθεσης) πριν την περάσετε στη μηχανή OCR. Το Aspose.OCR διαχειρίζεται πολλά από αυτά τα βήματα αυτόματα, αλλά μια καθαρή εικόνα προέλευσης πάντα αποδίδει καλύτερα αποτελέσματα.

---

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose.OCR

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε το πακέτο NuGet Aspose.OCR.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Γιατί είναι σημαντικό αυτό το βήμα:** Η συναρμολόγηση `Aspose.OCR` παρέχει την κλάση `OcrEngine` που θα χρησιμοποιήσουμε για **εκτέλεση OCR σε εικόνα** δεδομένα. Χωρίς το πακέτο, ο μεταγλωττιστής δεν θα αναγνωρίσει κανέναν τύπο σχετικό με OCR.

---

## Βήμα 2: Φόρτωση Εικόνας για OCR

Τώρα θα γράψουμε τον κώδικα που **φορτώνει εικόνα για OCR**. Η μέθοδος `OcrImage.FromFile` δέχεται απόλυτη ή σχετική διαδρομή και τυλίγει το bitmap σε μορφή που καταλαβαίνει η μηχανή.

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **Εξήγηση:** Διαχωρίζοντας τη διαδρομή σε μια δική της μεταβλητή διατηρούμε τον κώδικα τακτοποιημένο και το κάνουμε εύκολο να επαναχρησιμοποιήσουμε την ίδια αναφορά εικόνας αργότερα (π.χ. κατά την καταγραφή ή την αποσφαλμάτωση). Εάν το αρχείο δεν βρεθεί, η `FromFile` ρίχνει μια `FileNotFoundException`, την οποία μπορείτε να πιάσετε για να δώσετε ένα φιλικό μήνυμα σφάλματος.

---

## Βήμα 3: Εκτέλεση OCR στην Εικόνα και Αναγνώριση Κειμένου

Με την εικόνα στα χέρια, δημιουργούμε μια παρουσία της `OcrEngine` και της ζητάμε να **αναγνωρίσει κείμενο από εικόνα**. Αυτό το βήμα είναι η καρδιά του tutorial—εδώ συμβαίνει η πραγματική μαγεία του OCR.

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Γιατί χρησιμοποιούμε `using var`:** Η `OcrEngine` διατηρεί μη διαχειριζόμενους πόρους (βιβλιοθήκες native). Η τοποθέτησή της σε ένα μπλοκ `using` εγγυάται σωστή αποδέσμευση, αποτρέποντας διαρροές μνήμης—ιδιαίτερα σημαντικό σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

> **Τι λαμβάνετε:** Το `ocrResult` περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και πληροφορίες διάταξης (γραμμές, λέξεις, περιοριστικά πλαίσια). Για τις περισσότερες διαδικασίες επεξεργασίας τιμολογίων, η ιδιότητα `Text` είναι επαρκής, αλλά τα επιπλέον μεταδεδομένα μπορούν να βοηθήσουν στην επικύρωση ή στην οπτική αποσφαλμάτωση.

---

## Βήμα 4: Μετατροπή του Αποτελέσματος σε Μορφοποιημένο JSON

Το Aspose.OCR κάνει εξαιρετικά εύκολο το **γράψιμο JSON σε αρχείο** επειδή το `OcrResult` προσφέρει τη μέθοδο `ToJson`. Με το να περάσουμε `indent: true` λαμβάνουμε έξοδο αναγνώσιμη από άνθρωπο, κάτι χρήσιμο όταν χρειάζεται να **εξάγετε κείμενο από τιμολόγιο** αργότερα.

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **Δείγμα αποσπάσματος JSON** (συνοπτικό για συντομία):

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **Σημείωση για ειδικές περιπτώσεις:** Εάν η μηχανή OCR αποτύχει να εντοπίσει κείμενο, το `ocrResult.Text` θα είναι κενή συμβολοσειρά, αλλά το JSON θα περιέχει ακόμη μεταδεδομένα όπως οι διαστάσεις της εικόνας. Μπορείτε να προστατέψετε τον κώδικα ελέγχοντας για κενά αποτελέσματα πριν γράψετε το αρχείο.

---

## Βήμα 5: Γράψιμο JSON σε Αρχείο

Τώρα τελικά **γράφουμε JSON σε αρχείο**. Η χρήση του `File.WriteAllText` εξασφαλίζει ότι η ολόκληρη συμβολοσειρά αποθηκεύεται στο δίσκο με μία ατομική ενέργεια.

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **Συμβουλές για παραγωγή:** Σκεφτείτε να προσθέσετε χρονική σήμανση στο όνομα του αρχείου (`invoice_20260628_1500.json`) για να αποφύγετε την αντικατάσταση προηγούμενων εκτελέσεων. Επίσης, τοποθετήστε τη λειτουργία εγγραφής σε μπλοκ try/catch για να διαχειριστείτε τα προβλήματα δικαιωμάτων με ευγένεια.

---

## Βήμα 6: Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `invoice.png`.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**Αναμενόμενη έξοδος** όταν εκτελέσετε το πρόγραμμα:

```
JSON saved to C:\Invoices\invoice.json
```

Ανοίξτε το `invoice.json` και θα δείτε μια ωραία μορφοποιημένη αναπαράσταση των δεδομένων OCR, έτοιμη για επεξεργασία ή αποθήκευση downstream.

---

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

### Τι γίνεται αν η εικόνα περιέχει πολλαπλές γλώσσες;

Το Aspose.OCR ανιχνεύει αυτόματα τη γλώσσα βάσει του συνόλου χαρακτήρων. Εάν χρειάζεται να επιβάλετε μια συγκεκριμένη γλώσσα (π.χ. Αγγλικά για τα περισσότερα τιμολόγια), ορίστε την ιδιότητα `Language` στη μηχανή:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### Πώς να διαχειριστώ μεγάλα PDF με πολλές σελίδες;

Μετατρέψτε πρώτα κάθε σελίδα σε εικόνα (χρησιμοποιώντας μια βιβλιοθήκη PDF‑σε‑εικόνα) και στη συνέχεια κάντε βρόχο στις εικόνες, εφαρμόζοντας την ίδια ρουτίνα **εκτέλεσης OCR σε εικόνα**. Συγκεντρώστε τα αποτελέσματα JSON σε έναν ενιαίο πίνακα εάν θέλετε ένα ενοποιημένο αποτέλεσμα.

### Μπορώ να μεταδώσω το JSON αντί να γράψω ολόκληρο το αρχείο;

Ναι. Εάν δημιουργείτε ένα web API, μπορείτε να επιστρέψετε το `json` απευθείας ως σώμα της απάντησης:

```csharp
return Results.Json(ocrResult);
```

### Τι γίνεται με την απόδοση;

Η μηχανή OCR εκτελείται συγχρονισμένα στο παραπάνω παράδειγμα. Για σενάρια υψηλής απόδοσης, τοποθετήστε την κλήση αναγνώρισης σε `Task.Run` ή χρησιμοποιήστε τις ασύγχρονες εκδόσεις (εάν υπάρχουν) για να διατηρήσετε το UI σας ανταποκρινόμενο ή για να παραλληλοποιήσετε την επεξεργασία παρτίδων.

---

## Συμπέρασμα

Διασχίσαμε μια σύντομη, ολοκληρωμένη λύση που **εκτελεί OCR σε εικόνα** αρχεία, **αναγνωρίζει κείμενο από εικόνα**, **εξάγει κείμενο από τιμολόγιο**, και τελικά **γράφει JSON σε αρχείο** χρησιμοποιώντας το Aspose.OCR σε C#. Ο κώδικας είναι σκόπιμα απλός ώστε να τον προσαρμόσετε σε πιο σύνθετες ροές εργασίας—είτε αυτό σημαίνει προσθήκη προεπεξεργασίας εικόνας, τροφοδοσία του JSON σε βάση δεδομένων, ή έκθεση του αποτελέσματος μέσω ενός REST endpoint.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το PNG με JPEG, πειραματιστείτε με διαφορετικές ρυθμίσεις OCR (όπως `ocrEngine.Dpi`), ή ενσωματώστε ένα βήμα μετατροπής PDF‑σε‑εικόνα για να διαχειριστείτε ολόκληρα πακέτα τιμολογίων. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα καθαρά και ακριβή!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Χρησιμοποιήσετε το Aspose OCR για Αποτέλεσμα JSON στην Αναγνώριση Εικόνας](/ocr/english/net/text-recognition/get-result-as-json/)
- [Εξαγωγή Κειμένου από Εικόνα C# με Επιλογή Γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα – Αναγνώριση Γραμμής με Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}