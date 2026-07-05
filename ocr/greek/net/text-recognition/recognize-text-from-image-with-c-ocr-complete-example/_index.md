---
category: general
date: 2026-07-05
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας C# OCR – ένας οδηγός βήμα‑προς‑βήμα
  με πλήρες παράδειγμα C# OCR, φόρτωση εικόνας για OCR και εξαγωγή κειμένου από την
  εικόνα σε λίγα λεπτά.
draft: false
keywords:
- recognize text from image
- c# ocr example
- c# image to text
- load image for OCR
- extract text from image
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα σε C# με έναν πρακτικό οδηγό. Μάθετε
  ένα παράδειγμα OCR σε C#, πώς να φορτώσετε εικόνα για OCR και να εξάγετε κείμενο
  από την εικόνα γρήγορα.
og_title: Αναγνώριση κειμένου από εικόνα με C# OCR – Πλήρες Παράδειγμα
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: recognize text from image using C# OCR – a step‑by‑step guide with
    a full c# ocr example, load image for OCR and extract text from image in minutes.
  headline: recognize text from image with C# OCR – Complete Example
  type: TechArticle
- description: recognize text from image using C# OCR – a step‑by‑step guide with
    a full c# ocr example, load image for OCR and extract text from image in minutes.
  name: recognize text from image with C# OCR – Complete Example
  steps:
  - name: 1️⃣ Image Size & Quality
    text: 'OCR accuracy drops sharply on blurry or tiny pictures. A good rule of thumb:
      **minimum 300 dpi** for printed documents, and at least **800 px** on the longest
      side for photos. If you can’t control the source, consider up‑scaling with a
      bicubic algorithm before feeding it to the engine.'
  - name: 2️⃣ Multiple Languages
    text: If your image mixes scripts (e.g., English and Thai), set the language to
      `OcrLanguage.Multi` or pass an array of languages if the library supports it.
  - name: 3️⃣ Memory Management
    text: When processing many images in a loop, remember to dispose of streams and
      engine instances to avoid memory leaks.
  - name: 4️⃣ Error Reporting
    text: Wrap the OCR call in a try/catch block. Some engines throw `OcrException`
      when the language pack fails to download.
  - name: Got questions?
    text: Feel free to drop a comment—whether you’re stuck on a language pack, need
      help with image pre‑processing, or just want to share your success story. Happy
      coding, and enjoy turning pictures into searchable text!
  type: HowTo
tags:
- C#
- OCR
- Image Processing
title: Αναγνώριση κειμένου από εικόνα με C# OCR – Πλήρες Παράδειγμα
url: /el/net/text-recognition/recognize-text-from-image-with-c-ocr-complete-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με C# OCR – Πλήρες Παράδειγμα

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερτε ποια βιβλιοθήκη C# να επιλέξετε; Δεν είστε μόνοι—οι προγραμματιστές συνεχίζουν να ρωτούν, “Πώς μπορώ να μετατρέψω μια φωτογραφία μιας πινακίδας σε επεξεργάσιμο κείμενο;” Τα καλά νέα είναι ότι με λίγες μόνο γραμμές κώδικα μπορείτε να έχετε ένα πλήρως λειτουργικό **c# ocr example** έτοιμο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από όλα όσα χρειάζεστε για να **αναγνωρίσετε κείμενο από εικόνα**: εγκατάσταση του πακέτου OCR, φόρτωση της εικόνας, εκτέλεση της μηχανής και, τέλος, εκτύπωση του αποτελέσματος. Στο τέλος θα μπορείτε να επεξεργαστείτε οποιοδήποτε bitmap (μια σκαναρισμένη απόδειξη, μια φωτογραφία πινακίδας, ό,τι θέλετε) και να εξάγετε καθαρά, αναζητήσιμα strings.

---

## Τι Θα Χρειαστείτε

- **.NET 6** ή νεότερο (ο κώδικας λειτουργεί σε .NET Core, .NET Framework και .NET 5+)
- Μια πρόσφατη έκδοση του πακέτου NuGet **Microsoft Cognitive Services Vision** *ή* του πακέτου **IronOCR**—και τα δύο εκθέτουν ένα API τύπου `OcrEngine`. Τα αποσπάσματα παρακάτω στοχεύουν στη γενική διεπαφή `OcrEngine` που υλοποιούν οι περισσότερες βιβλιοθήκες.
- Ένα αρχείο εικόνας που θέλετε να επεξεργαστείτε (θα χρησιμοποιήσουμε το `thai_sign.png` στο παράδειγμα).
- Ένας επεξεργαστής κώδικα—Visual Studio, VS Code ή Rider αρκούν.

Αυτό είναι όλο. Χωρίς βαριές SDK OCR, χωρίς εξωτερικές υπηρεσίες, μόνο μερικές αναφορές NuGet και λίγες δηλώσεις C#.

---

## Βήμα 1: Ρύθμιση του Έργου για **αναγνώριση κειμένου από εικόνα**

Πρώτα, δημιουργήστε μια εφαρμογή κονσόλας (ή ένα μικρό εργαλείο WPF/WinForms) και προσθέστε το πακέτο OCR. Για το σκοπό αυτού του οδηγού θα υποθέσουμε ότι χρησιμοποιείτε **IronOCR** επειδή παρέχει μια απλή κλάση `OcrEngine`.

```bash
dotnet new console -n ImageToTextDemo
cd ImageToTextDemo
dotnet add package IronOcr
```

> **Pro tip:** Αν προτιμάτε το Azure Computer Vision, αντικαταστήστε το `IronOcr` με το `Microsoft.Azure.CognitiveServices.Vision.ComputerVision` και προσαρμόστε τον κώδικα ανάλογα—και τα δύο εκθέτουν την ίδια υψηλού επιπέδου ροή εργασίας.

---

## Βήμα 2: Φόρτωση της Εικόνας για OCR

Πριν η μηχανή μπορέσει να **αναγνωρίσει κείμενο από εικόνα**, χρειάζεται μια πηγή. Η βοηθητική μέθοδος `ImageStream.FromFile` (ή `File.ReadAllBytes` για καθαρό .NET) κάνει το σκληρό κομμάτι.

```csharp
using IronOcr;

// ...

// Step 2: Load the image you want to process
var imagePath = Path.Combine(Environment.CurrentDirectory, "thai_sign.png");

// Verify the file exists – a tiny sanity check that saves hours of debugging
if (!File.Exists(imagePath))
{
    Console.Error.WriteLine($"❌ Image not found: {imagePath}");
    return;
}

// IronOCR can read directly from a file path, but we’ll demonstrate the stream approach
using var imageStream = new FileStream(imagePath, FileMode.Open, FileAccess.Read);
var ocrImage = OcrInput.FromStream(imageStream);
```

Παρατηρήστε το σχόλιο “**load image for OCR**” – αντικατοπτρίζει τη δευτερεύουσα λέξη-κλειδί και σας θυμίζει γιατί τυλίγουμε το αρχείο σε stream. Αν παίρνετε εικόνες από ένα web API, απλώς αντικαταστήστε το `FileStream` με ένα `MemoryStream` που δημιουργείται από την HTTP απόκριση.

---

## Βήμα 3: Δημιουργία και Ρύθμιση της Μηχανής OCR

Τώρα ξεκινάμε τη μηχανή που θα **αναγνωρίσει κείμενο από εικόνα**. Η ρύθμιση της γλώσσας είναι προαιρετική, αλλά βελτιώνει δραματικά την ακρίβεια όταν γνωρίζετε το αλφάβητο.

```csharp
// Step 3: Create an OCR engine instance
var engine = new OcrEngine();

// Optional: tell the engine which language to expect.
// Here we use Thai as in the original snippet; change it to English, Chinese, etc.
engine.Language = OcrLanguage.Thai; // triggers language data download on first use
```

Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη, η ιδιότητα μπορεί να ονομάζεται `DefaultLanguage` ή `Language`. Η ιδέα παραμένει η ίδια: επιλέξτε το σωστό πακέτο γλώσσας **πριν εξάγετε κείμενο από εικόνα**.

---

## Βήμα 4: Εκτέλεση της Αναγνώρισης – Ο Πυρήνας της **αναγνώρισης κειμένου από εικόνα**

Με την εικόνα φορτωμένη και τη μηχανή ρυθμισμένη, η πραγματική κλήση OCR είναι μια μιά‑γραμμή.

```csharp
// Step 4: Run the OCR process
var result = engine.Read(ocrImage);
```

Η μέθοδος `Read` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το εξαγόμενο string, τους δείκτες εμπιστοσύνης και ακόμη και τα bounding boxes αν χρειαστεί να επισημάνετε το κείμενο αργότερα. Εδώ συμβαίνει η μαγεία—το πρόγραμμά σας τελικά **αναγνωρίζει κείμενο από εικόνα**.

---

## Βήμα 5: Εξαγωγή του Αναγνωρισμένου Κειμένου

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα ή δρομολογήστε το σε άλλο σύστημα (βάση δεδομένων, ευρετήριο αναζήτησης κ.λπ.). Η ιδιότητα `Text` περιέχει το καθαρισμένο string.

```csharp
// Step 5: Show the extracted text
Console.WriteLine("📝 Recognized text:");
Console.WriteLine(result.Text);
```

Τυπικό αποτέλεσμα για το δείγμα της ταϊλανδικής πινακίδας μπορεί να είναι:

```
📝 Recognized text:
สวัสดีประเทศไทย
```

Αν η εμπιστοσύνη είναι χαμηλή, μπορείτε να εξετάσετε το `result.Confidence` και να αποφασίσετε αν θα ξαναπροσπαθήσετε με εικόνα υψηλότερης ανάλυσης.

---

## Διαχείριση Συνηθισμένων Edge Cases

### 1️⃣ Μέγεθος & Ποιότητα Εικόνας

Η ακρίβεια του OCR πέφτει απότομα σε θολές ή πολύ μικρές εικόνες. Ένας καλός κανόνας: **τουλάχιστον 300 dpi** για έντυπα έγγραφα, και τουλάχιστον **800 px** στην μεγαλύτερη πλευρά για φωτογραφίες. Αν δεν μπορείτε να ελέγξετε την πηγή, σκεφτείτε να κάνετε up‑scaling με αλγόριθμο bicubic πριν τη δώσετε στη μηχανή.

### 2️⃣ Πολλαπλές Γλώσσες

Αν η εικόνα σας περιέχει μικτά αλφάβητα (π.χ. Αγγλικά και Ταϊλανδικά), ορίστε τη γλώσσα σε `OcrLanguage.Multi` ή περάστε έναν πίνακα γλωσσών αν η βιβλιοθήκη το υποστηρίζει.

```csharp
engine.Language = OcrLanguage.Multi; // or new[] { OcrLanguage.Thai, OcrLanguage.English }
```

### 3️⃣ Διαχείριση Μνήμης

Όταν επεξεργάζεστε πολλές εικόνες σε βρόχο, θυμηθείτε να απελευθερώνετε streams και instances της μηχανής για να αποφύγετε διαρροές μνήμης.

```csharp
using var engine = new OcrEngine(); // ensures Dispose is called
```

### 4️⃣ Αναφορά Σφαλμάτων

Τυλίξτε την κλήση OCR σε try/catch block. Κάποιες μηχανές ρίχνουν `OcrException` όταν αποτυγχάνει η λήψη του πακέτου γλώσσας.

```csharp
try
{
    var result = engine.Read(ocrImage);
    Console.WriteLine(result.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❗ OCR failed: {ex.Message}");
}
```

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑αντιγραφή πρόγραμμα που **αναγνωρίζει κείμενο από εικόνα** χρησιμοποιώντας τα παραπάνω βήματα. Αποθηκεύστε το ως `Program.cs` μέσα στο έργο που δημιουργήσατε νωρίτερα.

```csharp
using System;
using System.IO;
using IronOcr;

class Program
{
    static void Main()
    {
        // 1️⃣ Define the image path
        var imagePath = Path.Combine(Environment.CurrentDirectory, "thai_sign.png");
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"❌ Image not found: {imagePath}");
            return;
        }

        // 2️⃣ Load the image (load image for OCR)
        using var imageStream = new FileStream(imagePath, FileMode.Open, FileAccess.Read);
        var ocrInput = OcrInput.FromStream(imageStream);

        // 3️⃣ Create and configure the OCR engine
        using var engine = new OcrEngine();
        engine.Language = OcrLanguage.Thai; // download on first use

        // 4️⃣ Perform recognition (recognize text from image)
        var result = engine.Read(ocrInput);

        // 5️⃣ Output the extracted text (extract text from image)
        Console.WriteLine("📝 Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

**Αναμενόμενο αποτέλεσμα στην κονσόλα**

```
📝 Recognized text:
สวัสดีประเทศไทย
```

Τρέξτε το με `dotnet run`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε τη φράση στα Ταϊλανδικά να εκτυπώνεται, επιβεβαιώνοντας ότι η εφαρμογή μπορεί να **αναγνωρίσει κείμενο από εικόνα** σε λίγα δευτερόλεπτα.

---

## Οπτική Επισκόπηση

![Diagram illustrating the recognize text from image pipeline: load image → configure OCR engine → run recognition → get extracted text](/images/ocr-pipeline.png)

*Alt text:* *εικόνα διαγράμματος ροής αναγνώρισης κειμένου από εικόνα*

---

## Ανακεφαλαίωση & Επόμενα Βήματα

Μόλις δημιουργήσαμε ένα **c# ocr example** που φορτώνει μια εικόνα, ρυθμίζει τη γλώσσα, τρέχει τη μηχανή και εκτυπώνει το εξαγόμενο string—ουσιαστικά μια πλήρης ροή **c# image to text**. Τώρα ξέρετε πώς να **φορτώνετε εικόνα για OCR**, πώς να **εξάγετε κείμενο από εικόνα**, και πώς να αντιμετωπίζετε τα πιο συχνά προβλήματα.

Θέλετε να προχωρήσετε παραπέρα; Δοκιμάστε τις παρακάτω ιδέες:

- **Επεξεργασία παρτίδας:** Επανάληψη σε φάκελο PDF ή φωτογραφιών και αποθήκευση κάθε αποτελέσματος σε βάση δεδομένων.
- **Οπτικοποίηση bounding‑box:** Χρησιμοποιήστε τη συλλογή `result.Words` για να σχεδιάσετε ορθογώνια γύρω από το ανιχνευμένο κείμενο.
- **Υβριδικές προσεγγίσεις:** Συνδυάστε OCR με κανονικές εκφράσεις για εξαγωγή αριθμών τηλεφώνου, ημερομηνιών ή συνολικών τιμών τιμολογίων.
- **Υπηρεσίες cloud:** Αντικαταστήστε τη τοπική μηχανή με Azure Computer Vision αν χρειάζεστε τεράστια κλιμάκωση.

---

### Έχετε ερωτήσεις;

Μη διστάσετε να αφήσετε ένα σχόλιο—είτε είστε κολλημένοι με κάποιο πακέτο γλώσσας, χρειάζεστε βοήθεια με την προεπεξεργασία εικόνας, ή απλώς θέλετε να μοιραστείτε την επιτυχία σας. Καλό κώδικα, και απολαύστε τη μετατροπή εικόνων σε αναζητήσιμο κείμενο!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}