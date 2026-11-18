---
category: general
date: 2026-06-06
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας τη μηχανή OCR σε C#. Μάθετε
  πώς να μετατρέπετε την εικόνα σε JSON, να μετατρέπετε την εικόνα σε XML και να φορτώνετε
  την εικόνα για OCR σε λίγα λεπτά.
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: el
og_description: Αναγνώριση κειμένου από εικόνα με μηχανή OCR C#. Εξαγωγή αποτελεσμάτων
  σε JSON και XML, και διαχείριση φόρτωσης εικόνων για OCR.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρης οδηγός μηχανής OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρης οδηγός μηχανής OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα σε C# – Πλήρης Οδηγός Μηχανής OCR

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερες ποια βιβλιοθήκη C# να επιλέξεις; Δεν είσαι μόνος σου—οι προγραμματιστές αντιμετωπίζουν συνεχώς το πρόβλημα του να μετατρέπουν σαρωμένες αποδείξεις, στιγμιότυπα οθόνης ή χειρόγραφα σημειώματα σε αναζητήσιμο κείμενο. Τα καλά νέα; Με μια σύγχρονη **OCR engine C#** μπορείς να το κάνεις με λίγες γραμμές κώδικα, και στη συνέχεια **να μετατρέψεις την εικόνα σε JSON** ή **να μετατρέψεις την εικόνα σε XML** για επεξεργασία downstream.

Σε αυτόν τον οδηγό θα περάσουμε από κάθε βήμα: εγκατάσταση του πακέτου OCR, φόρτωση μιας εικόνας για OCR, εξαγωγή του κειμένου, και τέλος εξαγωγή των αποτελεσμάτων τόσο σε JSON όσο και σε XML. Στο τέλος θα έχεις μια αυτόνομη εφαρμογή console που μπορείς να ενσωματώσεις σε οποιοδήποτε έργο .NET. Χωρίς ασαφείς αναφορές, μόνο μια πλήρη, εκτελέσιμη λύση.

## Τι Θα Αποκομίσετε

- Μια σαφής εικόνα για το πώς να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας μια δημοφιλής μηχανή OCR C#.  
- Λειτουργικό κώδικα που **αναγνωρίζει κείμενο από εικόνα** και επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος.  
- Απλά αποσπάσματα που **μετατρέπουν την εικόνα σε JSON** και **μετατρέπουν την εικόνα σε XML** χωρίς πρόσθετες βιβλιοθήκες.  
- Συμβουλές για διαχείριση πολυ-σελίδων PDF, διαφορετικών μορφών εικόνας, και κοινών παγίδων όπως σάρωση χαμηλής αντίθεσης.

### Προαπαιτούμενα

- .NET 6 SDK ή νεότερο (μπορείς επίσης να στοχεύσεις .NET Framework 4.8 αν προτιμάς).  
- Βασικές γνώσεις C#—τίποτα περίπλοκο, μόνο μια κατανόηση κλάσεων και `async`/`await`.  
- Ένα αρχείο εικόνας (`structured.png` στα παραδείγματα) που θέλεις να υποβληθεί σε OCR.  

Αν τα έχεις όλα, ας ξεκινήσουμε.

---

## Αναγνώριση Κειμένου από Εικόνα – Ρύθμιση της Μηχανής OCR

Πρώτα απ' όλα. Χρειαζόμαστε μια αξιόπιστη βιβλιοθήκη OCR. Για αυτόν τον οδηγό θα χρησιμοποιήσουμε το **IronOcr**, μια εμπορική μηχανή που διατίθεται με δωρεάν έκδοση κοινότητας στο NuGet. Υποστηρίζει την αγγλική γλώσσα από την αρχή και μας παρέχει την κλάση `OcrEngine` που φαίνεται στο αρχικό απόσπασμα.

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **Συμβουλή επαγγελματία:** Αν έχεις περιορισμένο προϋπολογισμό, αντικατάστησε το `IronOcr` με το `Tesseract`—το API είναι ελαφρώς διαφορετικό αλλά οι έννοιες παραμένουν ίδιες.

Τώρα δημιούργησε ένα νέο έργο console και πρόσθεσε τις απαιτούμενες δηλώσεις `using`:

```csharp
using IronOcr;
using System.IO;
```

### Βήμα‑βήμα Διαμόρφωση Μηχανής

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*Γιατί είναι σημαντικό:* Η αρχικοποίηση της μηχανής μία φορά και η επαναχρησιμοποίησή της για πολλές εικόνες μειώνει το κόστος. Επίσης, ο καθορισμός της γλώσσας αποφεύγει τη διαδικασία αυτόματης ανίχνευσης της μηχανής, η οποία μπορεί να είναι πιο αργή και λιγότερο ακριβής.

---

## Φόρτωση Εικόνας για OCR – Παροχή των Δεδομένων στη Μηχανή

Η μηχανή αναμένει ένα αντικείμενο `OcrInput`. Μπορείς να το κατευθύνεις σε διαδρομή αρχείου, ροή (stream), ή ακόμη και σε `Bitmap`. Η πιο απλή προσέγγιση είναι η εξής:

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **Ακραία περίπτωση:** Αν η πηγή σου είναι ένα πολυ‑σελίδων PDF, κάλεσε `input.AddPdf("file.pdf")` αντί για PNG. Η μηχανή OCR θα αντιμετωπίσει κάθε σελίδα ως ξεχωριστή εικόνα αυτόματα.

---

## Αναγνώριση Κειμένου από Εικόνα – Εκτέλεση της Διαδικασίας OCR

Με τη μηχανή και το input έτοιμα, η πραγματική αναγνώριση είναι μια γραμμή κώδικα:

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` είναι ένα αντικείμενο `OcrResult` που περιέχει:

- `Text` – το ακατέργαστο εξαγόμενο κείμενο.  
- `Lines` – συλλογή αντικειμένων `OcrLine` με βαθμολογίες εμπιστοσύνης.  
- `Words` – συλλογή μεμονωμένων λέξεων, επίσης με βαθμολογία εμπιστοσύνης.  

Μπορείς να το εξετάσεις απευθείας στον debugger, αλλά στις περισσότερες περιπτώσεις θα θέλεις να το σειριοποιήσεις.

---

## Μετατροπή Εικόνας σε JSON – Εξαγωγή Αποτελεσμάτων OCR

Το IronOcr παρέχει ενσωματωμένη σειριοποίηση JSON μέσω `System.Text.Json`. Το παρακάτω απόσπασμα γράφει ένα καθαρό αρχείο JSON δίπλα στην πηγή εικόνας:

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**Τι θα δεις:** ένα ωραία μορφοποιημένο έγγραφο JSON που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και τα πλαίσια (bounding boxes) για κάθε γραμμή και λέξη. Αυτή η δομή είναι ιδανική για ενσωμάτωση σε υπηρεσίες downstream όπως ElasticSearch ή Azure Cognitive Search.

---

## Μετατροπή Εικόνας σε XML – Δομημένη Εξαγωγή Δεδομένων

Ορισμένα παλαιότερα συστήματα εξακολουθούν να απαιτούν XML. Η μέθοδος `ToXml()` του IronOcr παρέχει γρήγορη μετατροπή:

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

Το XML αντικατοπτρίζει την ιεραρχία του JSON, με στοιχεία `<Line>` και `<Word>` που φέρουν χαρακτηριστικά `Confidence`. Αν χρειάζεσαι προσαρμοσμένο σχήμα, μπορείς να προβάλλεις χειροκίνητα το `result` σε ένα `XDocument`—το API είναι πλήρως συμβατό με LINQ.

---

## Πλήρες Παράδειγμα End‑to‑End

Συνδυάζοντας τα παραπάνω, εδώ είναι ένα έτοιμο προς εκτέλεση `Program.cs`:

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**Αναμενόμενη έξοδος** (κομμένη για συντομία):

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

Τρέξε το πρόγραμμα με `dotnet run`. Αν όλα είναι σωστά συνδεδεμένα, θα δεις την εκτύπωση στην κονσόλα και δύο αρχεία θα εμφανιστούν στο `YOUR_DIRECTORY`.

---

## Συχνές Ερωτήσεις & Πιθανές Παγίδες

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν η εικόνα είναι JPEG με περιστροφή EXIF;* | Χρησιμοποίησε `input.AutoRotate()` πριν το `Deskew()`. Το IronOcr θα διαβάσει την ετικέτα EXIF και θα διορθώσει τον προσανατολισμό. |
| *Μπορώ να κάνω OCR σε φάκελο εικόνων μονομιάς;* | Απόλυτα. Τυλίξτε τη λογική σε έναν βρόχο `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |
| *Πώς βελτιώνω την ακρίβεια σε θορυβώδεις σαρώσεις;* | Αυξήστε το `input.Denoise()` και εξετάστε το `input.BlackWhiteThreshold(120)`. Επίσης, παρέχετε ένα πακέτο γλώσσας που ταιριάζει στη γλώσσα του εγγράφου. |
| *Είναι η μορφή JSON συμβατή με άλλες βιβλιοθήκες OCR;* | Το σχήμα είναι αρκετά γενικό—`Text`, `Lines`, `Words`—οπότε μπορείτε να το χαρτογραφήσετε στην έξοδο του Tesseract με ελάχιστη μετατροπή. |

---

## Συμβουλές Απόδοσης (Επίπεδο Pro)

- **Επαναχρησιμοποίηση της μηχανής**: Η δημιουργία `IronTesseract` μέσα σε έναν σφιχτό βρόχο μπορεί να μειώσει την απόδοση έως και 30 %. Διατήρησε ένα singleton ανά domain εφαρμογής.  
- **Παράλληλο I/O**: Αν επεξεργάζεσαι δεκάδες εικόνες, διάβασε τις ταυτόχρονα στη μνήμη (`Task.WhenAll`) και δώσε κάθε `OcrInput` στην ίδια μηχανή—το IronOcr είναι thread‑safe.  
- **Ομαδική εξαγωγή**: Αντί να γράφεις κάθε αρχείο JSON/XML ξεχωριστά, συγκέντρωσε τα αποτελέσματα σε μια συλλογή και σειριοποίησε μία φορά. Αυτό μειώνει την καταπόνηση του δίσκου.

---

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που μπορείς να **αναγνωρίζεις κείμενο από εικόνα**, σκέψου να επεκτείνεις τη ροή εργασίας:

- **Ενσωμάτωση αναζήτησης** – σπρώξε το JSON στο Elasticsearch για πλήρη αναζήτηση κειμένου.  
- **Κατηγοριοποίηση εγγράφων** – τροφοδότησε το αποτέλεσμα OCR σε ένα ελαφρύ μοντέλο ML για αυτόματη ετικετοθέτηση τιμολογίων, συμβάσεων ή αποδείξεων.  
- **Χειρόγραφο κείμενο** – άλλαξε το πακέτο γλώσσας σε `OcrLanguage.EnglishHandwritten` (διαθέσιμο στην premium έκδοση του IronOcr).  

Κάθε ένα από αυτά βασίζεται στο θεμέλιο που μόλις χτίσαμε και θα σε κρατήσει απασχολημένο για εβδομάδες.

---

## Συμπέρασμα

Καλύψαμε πώς να **αναγνωρίζεις κείμενο από εικόνα** χρησιμοποιώντας μια σύγχρονη **OCR engine C#**, στη συνέχεια **να μετατρέπεις την εικόνα σε JSON** και **να μετατρέπεις την εικόνα σε XML**, και τέλος πώς να **φορτώνεις εικόνα για OCR** με αξιόπιστο τρόπο. Το πλήρες παράδειγμα εκτελείται σε λιγότερο από ένα λεπτό, και τα εξαγόμενα αρχεία είναι έτοιμα για οποιοδήποτε σύστημα downstream.

Δοκίμασε τον κώδικα, πειραματίσου με τις ρυθμίσεις και...

## Τι Πρέπει Να Μάθεις Στη Σύντομη Μελλοντική

Οι παρακάτω εκπαιδευτικοί οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσεις επιπλέον δυνατότητες API και να εξερευνήσεις εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σου έργων.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}