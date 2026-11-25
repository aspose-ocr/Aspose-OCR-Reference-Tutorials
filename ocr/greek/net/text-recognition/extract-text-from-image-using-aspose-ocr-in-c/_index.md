---
category: general
date: 2026-08-09
description: Εξάγετε κείμενο από εικόνα με το Aspose OCR σε C#. Μάθετε πώς να φορτώνετε
  εικόνα για OCR, να ορίζετε τη γλώσσα OCR, να επεξεργάζεστε την εικόνα με OCR και
  να μετατρέπετε την εικόνα σε κείμενο αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: el
lastmod: 2026-08-09
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Αυτό
  το σεμινάριο δείχνει πώς να φορτώσετε εικόνα για OCR, να ορίσετε τη γλώσσα OCR,
  να επεξεργαστείτε την εικόνα με OCR και να μετατρέψετε την εικόνα σε κείμενο με
  λίγες γραμμές κώδικα.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#
url: /el/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#

Αν χρειάζεστε **εξαγωγή κειμένου από εικόνα** σε μια εφαρμογή .NET, αυτός ο οδηγός σας καθοδηγεί βήμα‑βήμα μέσα από μια πλήρη, έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να **φορτώνετε εικόνα για OCR**, να επιλέξετε το κατάλληλο πακέτο γλώσσας, να εκτελέσετε τη μηχανή OCR και τελικά να **μετατρέψετε την εικόνα σε κείμενο** με λίγες μόνο γραμμές C#.

Το tutorial καλύπτει όλα όσα απαιτούνται για αξιόπιστα αποτελέσματα με το Aspose.OCR, συμπεριλαμβανομένων κοινών παγίδων όπως μη υποστηριζόμενες μορφές εικόνας και λεπτομέρειες ειδικές για κάθε γλώσσα. Στο τέλος, θα έχετε ένα αυτόνομο πρόγραμμα που εκτυπώνει το αναγνωρισμένο κείμενο στην κονσόλα.

## Τι θα πετύχετε

* Φορτώστε ένα αρχείο εικόνας στη μηχανή Aspose OCR.  
* **Ορίστε τη γλώσσα OCR** (Cyrillic στο παράδειγμα, αλλά λειτουργεί οποιαδήποτε υποστηριζόμενη γλώσσα).  
* **Επεξεργαστείτε την εικόνα με OCR** και λάβετε την κειμενική αναπαράσταση.  
* **Μετατρέψτε την εικόνα σε κείμενο** και εμφανίστε το, έτοιμο για περαιτέρω επεξεργασία ή αποθήκευση.  

**Προαπαιτούμενα**

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#).  
* Πακέτο NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Εξαγωγή κειμένου από εικόνα – πλήρης περιήγηση κώδικα

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο πρόγραμμα. Αντιγράψτε το σε ένα νέο έργο κονσόλας και αντικαταστήστε το `YOUR_DIRECTORY/sample_cyrillic.jpg` με τη διαδρομή της δικής σας εικόνας.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Γιατί κάθε βήμα είναι σημαντικό

1. **Δημιουργία μιας παρουσίας του OCR engine** – Το `OcrEngine` ενσωματώνει όλη τη λειτουργικότητα OCR. Η άμεση απελευθέρωση του απελευθερώνει τους εγγενείς πόρους, κάτι που είναι κρίσιμο για υπηρεσίες μακράς διάρκειας.  
2. **Ορισμός γλώσσας OCR** – Η επιλογή του σωστού πακέτου γλώσσας βελτιώνει δραματικά την ακρίβεια. Το Aspose παρέχει πάνω από 30 πακέτα γλωσσών· η προεπιλογή είναι η Αγγλική. Το παράδειγμα χρησιμοποιεί Cyrillic για να δείξει ένα μη‑λατινικό σύστημα γραφής.  
3. **Φόρτωση εικόνας για OCR** – Η μηχανή λειτουργεί με ένα `ImageStream`. Η παροχή εικόνας υψηλής ανάλυσης (≥300 dpi) μειώνει τις λανθασμένες αναγνώσεις, ειδικά για σύνθετα συστήματα γραφής.  
4. **Επεξεργασία εικόνας OCR** – Εδώ γίνεται η βαριά δουλειά. Η μέθοδος επιστρέφει ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο, τους δείκτες εμπιστοσύνης και προαιρετικά δεδομένα διάταξης.  
5. **Μετατροπή εικόνας σε κείμενο** – Το `result.Text` είναι ένα απλό `string`. Μπορείτε να το γράψετε σε αρχείο, να το τροφοδοτήσετε σε ευρετήριο αναζήτησης ή να το περάσετε σε επόμενα στάδια NLP.  

---

## Φόρτωση εικόνας για OCR

Η μέθοδος `ImageStream.FromFile` υποστηρίζει κοινές μορφές raster. Εάν λαμβάνετε εικόνες ως byte arrays (π.χ., από web API), χρησιμοποιήστε `ImageStream.FromBytes(byte[])` αντί αυτού:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Συμβουλή:** Πάντα επαληθεύετε ότι η εικόνα δεν είναι κατεστραμμένη πριν τη περάσετε στη μηχανή. Ένας γρήγορος έλεγχος `try { Image.FromFile(...); } catch { ... }` αποτρέπει εξαιρέσεις χρόνου εκτέλεσης.

---

## Ορισμός γλώσσας OCR

Το Aspose.OCR περιλαμβάνει πακέτα γλωσσών που μπορείτε να ενεργοποιήσετε κατά το χρόνο εκτέλεσης. Για να εμφανίσετε όλες τις διαθέσιμες γλώσσες:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Εάν χρειάζεται να αναγνωρίσετε πολλαπλές γλώσσες στο ίδιο έγγραφο, συνδυάστε τις με τον τελεστή bitwise OR:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Περίπτωση άκρης:** Ο συνδυασμός γλωσσών από δεξιά προς αριστερά (RTL) (π.χ., Αραβικά) με γραφές από αριστερά προς δεξιά μπορεί να απαιτεί πρόσθετη διαχείριση διάταξης. Το Aspose ανιχνεύει αυτόματα την κατεύθυνση, αλλά μπορείτε να το ρυθμίσετε λεπτομερέστερα μέσω του `engine.PageSegmentationMode`.

---

## Επεξεργασία εικόνας OCR

Η κλήση `Process` είναι συγχρονισμένη και μπλοκάρει μέχρι να ολοκληρωθεί η μηχανή. Για μεγάλες παρτίδες ή εφαρμογές UI, εξετάστε την ασύγχρονη υπερφόρτωση:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Κοινή παγίδα:** Η παράλειψη του ορισμού `engine.Image` πριν την κλήση του `Process` προκαλεί `InvalidOperationException`. Πάντα ορίστε πρώτα την εικόνα.

---

## Μετατροπή εικόνας σε κείμενο

Το εξαγόμενο string μπορεί να χειριστεί όπως οποιοδήποτε άλλο .NET `string`. Για παράδειγμα, για να γράψετε το αποτέλεσμα σε αρχείο:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Εάν χρειάζεται να διατηρήσετε τις αλλαγές γραμμής ακριβώς όπως εμφανίζονται στην εικόνα, χρησιμοποιήστε απευθείας το `result.Text`. Για μετα-επεξεργασία (π.χ., αφαίρεση περιττών κενών), εφαρμόστε τις τυπικές μεθόδους string:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Ανασκόπηση πλήρους παραδείγματος

Συνδυάζοντας όλα, το πρόγραμμα:

1. Δημιουργεί μια παρουσία του `OcrEngine`.  
2. **Ορίζει τη γλώσσα OCR** σε Cyrillic (ή σε οποιαδήποτε γλώσσα επιλέξετε).  
3. **Φορτώνει εικόνα για OCR** από το δίσκο.  
4. **Επεξεργάζεται την εικόνα OCR** για να λάβει το κειμενικό αποτέλεσμα.  
5. **Μετατρέπει την εικόνα σε κείμενο** και το εκτυπώνει.  

Η εκτέλεση του δείγματος με μια καθαρή εικόνα Cyrillic παράγει έξοδο παρόμοια με:

```
=== Recognized Text ===
Пример текста на кириллице
```

Εάν η εικόνα περιέχει αγγλικό κείμενο, απλώς αλλάξτε το `engine.Language = OcrLanguage.English;` και ο ίδιος κώδικας θα **εξάγει κείμενο από την εικόνα** σωστά.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **εξάγετε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR σε C#. Το tutorial κάλυψε τη φόρτωση της εικόνας, την επιλογή της κατάλληλης γλώσσας, την εκτέλεση της διαδικασίας OCR και την **μετατροπή εικόνας σε κείμενο** για περαιτέρω χρήση.

Από εδώ μπορείτε να:

* Δοκιμάσετε άλλες γλώσσες (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Ενσωματώσετε το βήμα OCR σε μεγαλύτερο pipeline (π.χ., εισαγωγή εγγράφων, PDF με δυνατότητα αναζήτησης).  
* Βελτιστοποιήσετε την απόδοση ομαδοποιώντας εικόνες ή χρησιμοποιώντας το ασύγχρονο API.  

Μη διστάσετε να εξερευνήσετε την τεκμηρίωση του Aspose.OCR για προχωρημένα χαρακτηριστικά όπως προσαρμοσμένα λεξικά, λειτουργίες διαχωρισμού σελίδων και βελτιστοποίηση ακρίβειας OCR. Καλό προγραμματισμό!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να Εκτελέσετε Εξαγωγή Κειμένου Εικόνας από Ροή Χρησιμοποιώντας Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}