---
category: general
date: 2026-05-28
description: Πώς να εκτελέσετε OCR σε ASP.NET Core—μάθετε πώς να ανεβάζετε εικόνα,
  να εξάγετε κείμενο από την εικόνα και να διαχειρίζεστε αποδοτικά τη μεταφόρτωση
  αρχείων.
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: el
og_description: Πώς να εκτελέσετε OCR σε ASP.NET Core. Μάθετε βήμα‑βήμα πώς να ανεβάζετε
  μια εικόνα, να εξάγετε κείμενο από την εικόνα και να διαχειρίζεστε το ανέβασμα αρχείων
  με το Aspose OCR.
og_title: Πώς να εκτελέσετε OCR σε ASP.NET Core – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: Πώς να εκτελέσετε OCR σε ASP.NET Core – Πλήρης Οδηγός
url: /el/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε ASP.NET Core – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** μέσα σε ένα σύγχρονο web API χωρίς να τρελαίνεστε; Δεν είστε οι μόνοι. Οι προγραμματιστές χρειάζεται συνεχώς να επιτρέπουν στους χρήστες να ανεβάζουν μια εικόνα—ίσως μια απόδειξη, ένα σκανάρισμα διαβατηρίου ή ένα χειρόγραφο σημείωμα—και να λαμβάνουν το ακατέργαστο κείμενο σε JSON.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από μια πλήρη, έτοιμη για παραγωγή λύση που δείχνει **πώς να ανεβάσετε αρχείο**, το επικυρώνει, εκτελεί το Aspose OCR, και τελικά **εξάγει κείμενο από εικόνα**. Στο τέλος θα έχετε έναν έτοιμο controller που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο ASP.NET Core.

## Τι Θα Δημιουργήσετε

- Ένα `OcrController` που δέχεται ανεβάσματα multipart/form‑data
- Επικύρωση ότι το αρχείο υπάρχει πραγματικά και δεν είναι κενό
- Ασύγχρονη επεξεργασία OCR χρησιμοποιώντας τη μηχανή Aspose OCR
- Μια καθαρή JSON απάντηση που περιέχει το αναγνωρισμένο κείμενο

Καμία εξωτερική υπηρεσία, κανένα κρυφό μαγικό—απλώς καθαρός κώδικας C# που μπορείτε να εκτελέσετε τοπικά.

## Προαπαιτούμενα (Τι Χρειάζεστε Πριν Ξεκινήσετε)

| Απαίτηση | Γιατί Είναι Σημαντικό |
|----------|------------------------|
| .NET 6 SDK ή νεότερο | Το ASP.NET Core 6+ μας παρέχει δυνατότητες minimal API και υποστήριξη async. |
| Visual Studio 2022 (ή VS Code) | Το IDE καθιστά την αποσφαλμάτωση πιο εύκολη, αλλά οποιοσδήποτε επεξεργαστής λειτουργεί. |
| Πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`) | Η μηχανή που πραγματικά εκτελεί την εργασία OCR. |
| Βασικές γνώσεις του ASP.NET Core MVC | Θα χρησιμοποιήσουμε `ControllerBase` και attributes δρομολόγησης. |

Αν τα έχετε, υπέροχα—ας βουτήξουμε.

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose OCR

Ανοίξτε ένα τερματικό και δημιουργήστε ένα νέο έργο web API:

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Αυτή η εντολή φέρνει τη βιβλιοθήκη OCR και όλες τις εξαρτήσεις της. Δεν χρειάζεται άλλη ρύθμιση· το Aspose λειτουργεί έτοιμο για τις κοινές μορφές εικόνας.

## Βήμα 2: Προσθήκη του OCR Controller (Ο Πυρήνας του **πώς να εκτελέσετε OCR**)

Δημιουργήστε ένα νέο αρχείο `Controllers/OcrController.cs` και επικολλήστε τον παρακάτω κώδικα. Είναι το πλήρες, εκτελέσιμο παράδειγμα—χωρίς ελλείψεις.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### Γιατί Αυτό Λειτουργεί

- **`[FromForm] IFormFile`** λέει στο ASP.NET Core να δεσμεύσει το μέρος του multipart αρχείου στο `uploadedFile`. Αυτός είναι ο κλασικός τρόπος για **διαχείριση ανεβάσματος αρχείου** σε ένα web API.
- Η προστασία `if` εξασφαλίζει ότι **διαχειριζόμαστε σφάλματα ανεβάσματος αρχείου** με χάρη, επιστρέφοντας 400 Bad Request αν ο πελάτης ξέχασε να στείλει αρχείο.
- `using var fileStream = uploadedFile.OpenReadStream();` ανοίγει ένα *μόνο‑ανάγνωση* stream, που είναι απαραίτητο για μεγάλα αρχεία—δεν χρειάζεται να φορτώσετε ολόκληρη την εικόνα στη μνήμη ταυτόχρονα.
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` τροφοδοτεί το stream απευθείας στο Aspose OCR, διατηρώντας την αλυσίδα ελαφριά.
- `await ocrEngine.RecognizeAsync();` εκτελεί το βαρέως φορτίου σε νήμα παρασκηνίου, ώστε το API μας να παραμένει ανταποκρινόμενο. Αυτό είναι η καρδιά του **πώς να εκτελέσετε OCR** ασύγχρονα.
- Τέλος, τυλίγουμε το αποτέλεσμα σε ένα JSON αντικείμενο (`{ extractedText }`)—τέλειο για κατανάλωση από το front‑end.

## Βήμα 3: Διαμόρφωση του Ορίου Μεγέθους Αιτήματος (Προαιρετικό αλλά Χρήσιμο)

Αν αναμένετε σαρώσεις υψηλής ανάλυσης, αυξήστε το προεπιλεγμένο όριο αιτήματος. Προσθέστε αυτό στο `Program.cs`:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

Τώρα το API δεν θα κολλήσει με μια εικόνα απόδειξης 10 MB. Προσαρμόστε το όριο ανάλογα με την περίπτωση χρήσης σας.

## Βήμα 4: Δοκιμή του Endpoint με cURL ή Postman

Ακολουθεί μια γρήγορη εντολή cURL που μπορείτε να εκτελέσετε από το τερματικό:

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

Θα πρέπει να δείτε ένα JSON payload παρόμοιο με:

```json
{
  "extractedText": "Sample text that was on the image."
}
```

Αν η εικόνα δεν περιέχει αναγνωρίσιμους χαρακτήρες, η συμβολοσειρά θα είναι κενή—δεν σκάει τίποτα, απλώς ένα κενό αποτέλεσμα. Αυτό είναι μια καλή περίπτωση άκρης που πρέπει να θυμάστε.

## Βήμα 5: Οπτική Επιβεβαίωση (Προαιρετική Εικόνα)

Παρακάτω είναι ένα εικονικό screenshot που δείχνει την JSON απάντηση που θα λάβετε μετά από μια επιτυχημένη αίτηση OCR.

![Αποτέλεσμα εκτέλεσης OCR – screenshot της JSON απάντησης που δείχνει το εξαγόμενο κείμενο](/images/ocr-result.png)

*Κείμενο εναλλακτικής περιγραφής:* **αποτέλεσμα εκτέλεσης OCR screenshot που δείχνει το εξαγόμενο κείμενο από την εικόνα**

## Συνηθισμένα Πιθανά Προβλήματα & Επαγγελματικές Συμβουλές

| Πρόβλημα | Λύση |
|----------|------|
| **Μη υποστηριζόμενη μορφή εικόνας** (π.χ., TIFF με πολλαπλές σελίδες) | Μετατρέψτε πρώτα σε PNG/JPEG ή χρησιμοποιήστε το `ImageConverter` του Aspose πριν το δώσετε στο `OcrEngine`. |
| **Μεγάλα αρχεία προκαλούν πίεση μνήμης** | Μεταφέρετε το αρχείο όπως φαίνεται· αποφύγετε το `IFormFile.CopyToAsync` σε `MemoryStream`. |
| **Το OCR επιστρέφει ακατάληπτο κείμενο** | Βεβαιωθείτε ότι η εικόνα έχει υψηλή αντίθεση και είναι σωστά προσανατολισμένη. Προεπεξεργαστείτε με `ocrEngine.Preprocess()` αν χρειάζεται. |
| **Πολλαπλά ταυτόχρονα αιτήματα** | Το Aspose OCR είναι thread‑safe, αλλά ίσως θέλετε να περιορίσετε τη σύγχρονη εκτέλεση με semaphore αν ο διακομιστής σας έχει περιορισμένη μνήμη. |

## Επέκταση του Παραδείγματος: Μαζική Ανέβασμα & Παράλληλη Επεξεργασία

Αν χρειάζεται να **διαχειριστείτε ανεβάσματα αρχείων** για πολλές εικόνες ταυτόχρονα, αλλάξτε την υπογραφή της ενέργειας ώστε να δέχεται λίστα:

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

Τώρα μπορείτε να **ανεβάσετε OCR εικόνας** μαζικά—ιδανικό για σάρωση φακέλου αποδείξεων σε μία φορά.

## Θεωρήσεις Ασφάλειας

- **Επικυρώστε τις επεκτάσεις αρχείων** (`.png`, `.jpg`, `.jpeg`) πριν την επεξεργασία για να αποφύγετε κακόβουλες ανεβάσματα.
- **Σαρώστε για ιούς** αν το API σας είναι εκτεθειμένο στο διαδίκτυο· ενσωματώστε μια υπηρεσία όπως το ClamAV.
- **Περιορίστε το ρυθμό** (rate‑limit) του endpoint για να αποτρέψετε επιθέσεις άρνησης υπηρεσίας.

## Αναμενόμενο Αποτέλεσμα & Πώς να Επαληθεύσετε

Όταν καλέσετε το endpoint `/ocr/upload` με μια καθαρή εικόνα που περιέχει τη λέξη “Hello”, η απάντηση πρέπει να είναι:

```json
{
  "extractedText": "Hello"
}
```

Μπορείτε γρήγορα να επαληθεύσετε ανοίγοντας τα εργαλεία προγραμματιστή του προγράμματος περιήγησης → καρτέλα Δίκτυο, ή εξετάζοντας την έξοδο του cURL.

## Ανακεφαλαίωση – Τι Καλύψαμε

- Ρύθμιση ενός έργου ASP.NET Core και προσθήκη του πακέτου NuGet Aspose OCR.
- Υλοποίηση ενός καθαρού controller που δείχνει **πώς να εκτελέσετε OCR**, **διαχείριση ανεβάσματος αρχείου**, και **εξαγωγή κειμένου από εικόνα**.
- Συζήτηση για διαχείριση σφαλμάτων, βελτιώσεις απόδοσης, και βέλτιστες πρακτικές ασφαλείας.
- Παροχή ενός έτοιμου προς εκτέλεση δείγματος κώδικα μαζί με μια παραλλαγή μαζικού ανεβάσματος.

## Τι Έρχεται Στη Σειρά;

- **Προσθήκη υποστήριξης γλώσσας**: Το Aspose OCR μπορεί να ρυθμιστεί για διαφορετικές γλώσσες (`ocrEngine.Language = Language.English;`).
- **Ενσωμάτωση με βάση δεδομένων**: Αποθηκεύστε το εξαγόμενο κείμενο μαζί με μεταδεδομένα για μελλοντική αναζήτηση.
- **UI Front‑end**: Δημιουργήστε μια απλή σελίδα React ή Blazor που επιτρέπει στους χρήστες να σύρουν‑και‑αποθέτουν εικόνες και να βλέπουν το αποτέλεσμα OCR άμεσα.

Νιώστε ελεύθεροι να πειραματιστείτε—αντικαταστήστε τη μηχανή OCR, δοκιμάστε διαφορετικά βήματα προεπεξεργασίας εικόνας, ή συνδέστε το αποτέλεσμα με ένα downstream μοντέλο AI. Ο ουρανός είναι το όριο όταν γνωρίζετε **πώς να εκτελέσετε OCR** σε μια σύγχρονη στοίβα .NET.

Καλό κώδικα, και εύχομαι το κείμενό σας πάντα να είναι ευανάγνωστο!

## Σχετικά Μαθήματα

- [Πώς να Κάνετε OCR Εικόνας – Εκτέλεση OCR σε Εικόνα στην Αναγνώριση Εικόνας OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Πώς να Χρησιμοποιήσετε το Aspose για Αναγνώριση Εικόνας από Stream στην Αναγνώριση Εικόνας OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Πώς να Ορίσετε Τιμή Κατωφλίου στην Αναγνώριση Εικόνας OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}