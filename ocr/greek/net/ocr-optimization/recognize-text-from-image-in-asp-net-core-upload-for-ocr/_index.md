---
category: general
date: 2026-06-28
description: Αναγνώριση κειμένου από εικόνα σε ASP.NET Core – μάθετε πώς να ανεβάζετε
  εικόνα για OCR και να επεξεργάζεστε την εικόνα OCR από ροή αποδοτικά.
draft: false
keywords:
- recognize text from image
- upload image for ocr
- ocr image from stream
language: el
og_description: αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR σε ASP.NET
  Core. Ανεβάστε εικόνα για OCR, επεξεργαστείτε την εικόνα OCR από ροή και επιστρέψτε
  καθαρό κείμενο.
og_title: Αναγνώριση κειμένου από εικόνα σε ASP.NET Core – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  headline: recognize text from image in ASP.NET Core – upload for OCR
  type: TechArticle
- description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  name: recognize text from image in ASP.NET Core – upload for OCR
  steps:
  - name: Why This Pattern Works
    text: '- **Single `OcrEngine` instance**: Instantiating the engine once avoids
      the overhead of loading language data on every request. - **Async everything**:
      By using `await` on `FromStreamAsync` and `RecognizeAsync`, the ASP.NET Core
      thread pool stays free to serve other callers. - **`IFormFile` binding*'
  - name: Edge Cases to Watch
    text: '- **Corrupt files**: If the uploaded file isn’t a valid image, `FromStreamAsync`
      throws an exception. Wrap the call in a try/catch if you need graceful error
      messages. - **Unsupported formats**: Aspose supports PNG, JPEG, BMP, TIFF, etc.
      If you need PDF input, you’ll have to convert it to an image f'
  - name: Why Not Use `Recognize` (Sync)?
    text: The synchronous version would block the ASP.NET Core thread pool until the
      CPU‑intensive OCR finishes. On a busy server that quickly becomes a bottleneck,
      leading to 504 timeouts. The async variant keeps the API snappy.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Aspose.OCR
title: Αναγνώριση κειμένου από εικόνα στο ASP.NET Core – μεταφόρτωση για OCR
url: /el/net/ocr-optimization/recognize-text-from-image-in-asp-net-core-upload-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε ASP.NET Core – Πλήρες Εγχειρίδιο

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** μέσα σε ένα web API και δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Σε πολλά έργα—σκεφτείτε σαρωτές τιμολογίων, παρακολούθηση αποδείξεων, ή ακόμη και μια απλή λειτουργία «διάβασε‑με»—η απόκτηση αξιόπιστων αποτελεσμάτων OCR είναι μια απαραίτητη δεξιότητα.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **ανεβάσετε εικόνα για OCR**, να μετατρέψετε αυτό το ανέβασμα σε **ocr image from stream**, και τελικά να επιστρέψετε το εξαγόμενο κείμενο ως καθαρό JSON. Χωρίς ελλείποντα κομμάτια, χωρίς ασαφείς αναφορές—απλώς μια αυτόνομη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο ASP.NET Core σήμερα.

## Τι Θα Αποκομίσετε

- Ένας πλήρως λειτουργικός `OcrController` που δέχεται ανεβάσματα multipart form.  
- Εξήγηση βήμα‑βήμα κάθε γραμμής, ώστε να κατανοήσετε *γιατί* κάνουμε ό,τι κάνουμε.  
- Συμβουλές για διαχείριση μεγάλων αρχείων, αποφυγή φραγής νήματος, και διατήρηση της ανταπόκρισης του API.  
- Μια ματιά στο πώς να επεκτείνετε τη λύση (πολλαπλές γλώσσες, προεπεξεργασία εικόνας, κ.λπ.).  

**Προαπαιτούμενα**: .NET 6 ή νεότερο, Visual Studio 2022 (ή VS Code), και άδεια Aspose.OCR (η δωρεάν δοκιμή λειτουργεί για δοκιμές). Αν τα έχετε, ας ξεκινήσουμε.

![recognize text from image workflow diagram](https://example.com/ocr-workflow.png "recognize text from image workflow")

## Πώς να Αναγνωρίσετε Κείμενο από Εικόνα σε ASP.NET Core

Η καρδιά της λύσης βρίσκεται σε έναν μόνο controller. Παρακάτω είναι ο **πλήρης, εκτελέσιμος κώδικας**· κάθε εισαγωγή, κάθε οδηγία `using`, και κάθε async κλήση περιλαμβάνονται ώστε να μπορείτε να το αντιγράψετε‑και‑επικολλήσετε απευθείας σε ένα νέο έργο ASP.NET Core Web API.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

[ApiController]
[Route("api/ocr")]
public class OcrController : ControllerBase
{
    // Step 1: Create a reusable OCR engine instance
    // Reusing the same OcrEngine across requests saves memory and speeds up init.
    private readonly OcrEngine _ocrEngine = new OcrEngine();

    // Step 2: Define the endpoint that accepts a file upload
    [HttpPost("recognize")]
    public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
    {
        // Guard clause – make sure we actually got a file
        if (uploadedFile == null || uploadedFile.Length == 0)
            return BadRequest(new { error = "No file uploaded." });

        // Step 3: Open the uploaded file as a read‑only stream
        // This is the **ocr image from stream** part.
        await using var imageStream = uploadedFile.OpenReadStream();

        // Step 4: Load the image asynchronously for OCR processing
        // Aspose.OCR provides FromStreamAsync which off‑loads the I/O work.
        var ocrImage = await OcrImage.FromStreamAsync(imageStream);

        // Step 5: Run OCR recognition without blocking the request thread
        // RecognizeAsync runs the heavy lifting on a background thread.
        var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);

        // Step 6: Return the extracted text as a JSON response
        return Ok(new { text = ocrResult.Text });
    }
}
```

### Γιατί Λειτουργεί Αυτό το Σχέδιο

- **Μονή παρουσία `OcrEngine`**: Η δημιουργία του engine μία φορά αποφεύγει το κόστος φόρτωσης δεδομένων γλώσσας σε κάθε αίτηση.  
- **Όλα Async**: Χρησιμοποιώντας `await` στο `FromStreamAsync` και `RecognizeAsync`, η ομάδα νημάτων του ASP.NET Core παραμένει ελεύθερη για εξυπηρέτηση άλλων κλήσεων.  
- `IFormFile` binding`: Το χαρακτηριστικό `[FromForm]` επιτρέπει στον πελάτη να κάνει απλώς POST ένα multipart/form‑data αίτημα—ακριβώς αυτό που γνωρίζουν ήδη οι browsers και εργαλεία όπως το Postman.  

Τώρα που ο κώδικας είναι μπροστά σας, ας αναλύσουμε κάθε λογικό τμήμα.

## Ανέβασμα Εικόνας για OCR – Διαχείριση του Multipart Αιτήματος

Όταν ένας πελάτης στέλνει ένα αρχείο, το ASP.NET Core το δεσμεύει στο `IFormFile`. Αυτό το αντικείμενο μας παρέχει έναν ασφαλή χειριστή των ακατέργαστων bytes χωρίς να φορτώνουμε ολόκληρο το αρχείο στη μνήμη ταυτόχρονα.

```csharp
[HttpPost("recognize")]
public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
{
    if (uploadedFile == null || uploadedFile.Length == 0)
        return BadRequest(new { error = "No file uploaded." });

    // …
}
```

**Συμβουλή**: Αν αναμένετε τεράστιες εικόνες (σκεφτείτε >10 MB), σκεφτείτε να προσθέσετε έναν έλεγχο μεγέθους εδώ και να επιστρέφετε 413 Payload Too Large. Προστατεύει τον διακομιστή σας από τυχαίες καταρρεύσεις OOM.

## Επεξεργασία OCR Image από Stream Ασύγχρονα

Η γραμμή `await OcrImage.FromStreamAsync(imageStream)` κάνει το βαριά έργο της αποκωδικοποίησης των bytes της εικόνας σε μορφή που το Aspose.OCR μπορεί να καταλάβει. Επειδή είναι async, το υποκείμενο I/O (δίσκος ή δίκτυο) δεν θα μπλοκάρει το νήμα του αιτήματος.

```csharp
await using var imageStream = uploadedFile.OpenReadStream();
var ocrImage = await OcrImage.FromStreamAsync(imageStream);
```

### Περιπτώσεις Ακρότητας που Πρέπει να Προσέξετε

- **Κατεστραμμένα αρχεία**: Αν το ανεβασμένο αρχείο δεν είναι έγκυρη εικόνα, το `FromStreamAsync` ρίχνει εξαίρεση. Τυλίξτε την κλήση σε try/catch αν χρειάζεστε ευγενικά μηνύματα σφάλματος.  
- **Μη υποστηριζόμενες μορφές**: Το Aspose υποστηρίζει PNG, JPEG, BMP, TIFF κ.λπ. Αν χρειάζεστε είσοδο PDF, θα πρέπει πρώτα να το μετατρέψετε σε εικόνα (το Aspose.PDF μπορεί να βοηθήσει).  

## Εκτέλεση του OCR Engine Χωρίς Φραγή

`_ocrEngine.RecognizeAsync(ocrImage)` εκτελεί τον αλγόριθμο OCR σε ένα νήμα παρασκηνίου. Αυτή είναι η στιγμή που η λειτουργία **αναγνώρισης κειμένου από εικόνα** πραγματικά συμβαίνει.

```csharp
var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);
```

Το επιστρεφόμενο `ocrResult` περιέχει μια ιδιότητα `Text` με το ακατέργαστο εξαγόμενο κείμενο. Μπορείτε να το επεξεργαστείτε περαιτέρω (αφαιρέστε κενά, διορθώστε κοινά σφάλματα OCR κ.λπ.) πριν το στείλετε πίσω.

### Γιατί να Μην Χρησιμοποιήσετε το `Recognize` (Συγχρονικό);

Η συγχρονική έκδοση θα φράξει την ομάδα νημάτων του ASP.NET Core μέχρι να ολοκληρωθεί το CPU‑έντονο OCR. Σε έναν φορτωμένο διακομιστή αυτό γίνεται γρήγορα σημείο συμφόρησης, οδηγώντας σε 504 timeouts. Η async παραλλαγή διατηρεί το API γρήγορο.

## Επιστροφή Καθαρής JSON – Το Τελευταίο Τμήμα

```csharp
return Ok(new { text = ocrResult.Text });
```

Οι πελάτες λαμβάνουν ένα τακτοποιημένο JSON payload:

```json
{
  "text": "Sample extracted text from the uploaded image."
}
```

Αν χρειάζεστε πρόσθετα μεταδεδομένα—βαθμοί εμπιστοσύνης, ανίχνευση γλώσσας, περιοριστικά πλαίσια—απλώς επεκτείνετε το ανώνυμο αντικείμενο ή ορίστε ένα κατάλληλο DTO.

## Δοκιμή του Endpoint

Μπορείτε να επαληθεύσετε ότι όλα λειτουργούν με **cURL**, **Postman**, ή ακόμη και μια απλή HTML φόρμα.

```bash
curl -X POST https://localhost:5001/api/ocr/recognize \
     -F "uploadedFile=@/path/to/your/image.png"
```

Μια επιτυχής απάντηση φαίνεται ως εξής:

```
{"text":"Hello World"}
```

Αν ξεχάσετε να στείλετε αρχείο, θα λάβετε:

```
{"error":"No file uploaded."}
```

## Προχωρώντας Περαιτέρω – Συνηθισμένες Βελτιώσεις

| Βελτίωση | Γιατί Βοηθά | Γρήγορη Υπόδειξη Κώδικα |
|------------|--------------|-----------------|
| **Επιλογή γλώσσας** | Η ακρίβεια του OCR βελτιώνεται όταν ενημερώνετε το engine ποια γλώσσα να περιμένει. | `_ocrEngine.Language = OcrLanguage.English;` |
| **Προεπεξεργασία εικόνας** | Η ρύθμιση φωτεινότητας/αντίθεσης μπορεί να σώσει σαρώσεις χαμηλής ποιότητας. | `ocrImage = OcrImage.FromBitmap(ImageProcessor` |

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες λειτουργίες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εκτελέσετε Εξαγωγή Κειμένου από Εικόνα από Stream Χρησιμοποιώντας Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}