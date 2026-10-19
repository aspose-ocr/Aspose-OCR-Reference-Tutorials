---
category: general
date: 2026-05-25
description: Μάθετε πώς να εξάγετε κείμενο από εικόνα με ένα ελάχιστο API ASP.NET
  Core. Ανεβάστε την εικόνα μέσω POST, διαβάστε τα multipart form data και εκτελέστε
  OCR στην εικόνα.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: el
og_description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας ένα ελαφρύ API ASP.NET
  Core. Αυτός ο οδηγός δείχνει πώς να ανεβάσετε εικόνα μέσω POST, να διαβάσετε δεδομένα
  multipart form και να εκτελέσετε OCR στην εικόνα.
og_title: Εξαγωγή κειμένου από εικόνα σε ASP.NET Core – Βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Εξαγωγή κειμένου από εικόνα σε ASP.NET Core Minimal API – Πλήρης οδηγός
url: /el/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα σε ASP.NET Core Minimal API – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από εικόνα** χωρίς να παλεύετε με βαριές πλατφόρμες; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται έναν γρήγορο τρόπο για να επιτρέπουν στους χρήστες να ανεβάζουν μια φωτογραφία και να λαμβάνουν πίσω τους ακατέργαστους χαρακτήρες, είτε πρόκειται για σάρωση αποδείξεων, ψηφιοποίηση χειρόγραφων σημειώσεων, είτε για τροφοδοσία ενός ευρετηρίου αναζήτησης.

Σε αυτό το tutorial θα δημιουργήσουμε ένα μικρό ASP.NET Core Minimal API που **ανεβάζει εικόνα μέσω POST**, αναλύει το φορτίο *multipart/form‑data* και στη συνέχεια **εκτελεί OCR στην εικόνα** χρησιμοποιώντας ένα singleton `OcrEngine`. Στο τέλος θα έχετε μια πλήρως εκτελέσιμη εφαρμογή που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET 8 και να αρχίσετε αμέσως να εξάγετε κείμενο από εικόνα.

## Τι Θα Δημιουργήσετε

- Μια ελαφριά web εφαρμογή που ακούει στο `/ocr`.
- Ένα endpoint που δέχεται αρχείο εικόνας αποσταλμένο με αίτημα POST τύπου `multipart/form-data`.
- Λογική που διαβάζει το ανεβασμένο αρχείο, το περνά στη μηχανή OCR και επιστρέφει αποτελέσματα σε απλό κείμενο.
- Προαιρετικό απόσπασμα επιτάχυνσης GPU (σχολιασμένο) για όσους διαθέτουν συμβατή κάρτα.

**Προαπαιτούμενα**  
- .NET 8 SDK (ή νεότερο).  
- Βασική εξοικείωση με C# και τη γραμμή εντολών.  
- Μια βιβλιοθήκη OCR που εκθέτει μια κλάση `OcrEngine` (το παράδειγμα υποθέτει ένα υποθετικό πακέτο NuGet).

Αν τα έχετε, ας βουτήξουμε.

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη του Πακέτου OCR

First, create a new web project and pull in the OCR library.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Συμβουλή επαγγελματία:** Διατηρήστε τις εξαρτήσεις σας ενημερωμένες. Οι νεότερες εκδόσεις συχνά προσφέρουν βελτιώσεις απόδοσης, ειδικά για GPU‑επιταχυμένη εκτίμηση.

## Βήμα 2: Καταχώρηση ενός Singleton OCR Engine (Κύρια Υπηρεσία)

We want a single `OcrEngine` instance for the whole app—no need to spin up a new engine per request. Register it in the builder’s service container.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Γιατί singleton;**  
Η δημιουργία μιας μηχανής OCR μπορεί να είναι δαπανηρή—σκεφτείτε τη φόρτωση βαρών νευρωνικού δικτύου στη μνήμη. Με την επαναχρησιμοποίηση της ίδιας παρουσίας εξοικονομούμε τόσο κύκλους CPU όσο και RAM, κάτι που μεταφράζεται σε ταχύτερους χρόνους απόκρισης για κάθε κλήση `/ocr`.

## Βήμα 3: Κατασκευή της Εφαρμογής

Now we materialize the `WebApplication` object.

```csharp
var app = builder.Build();
```

Αυτή η γραμμή φαίνεται σχεδόν μαγική, αλλά στο παρασκήνιο ρυθμίζει το routing, το middleware και το DI container που μόλις διαμορφώσαμε.

## Βήμα 4: Ορισμός του POST Endpoint – “Ανέβασμα Εικόνας μέσω POST”

Here’s the heart of the tutorial: an endpoint that **upload image via POST**, reads the multipart payload, and hands the data to the OCR engine.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Ανάλυση της Λογικής

| Βήμα | Τι Συμβαίνει | Γιατί Είναι Σημαντικό |
|------|--------------|------------------------|
| **ReadFormAsync** | Αναλύει το εισερχόμενο αίτημα *multipart/form-data*. | Χωρίς αυτό, δεν μπορείτε να έχετε πρόσβαση στα ανεβασμένα αρχεία. |
| **form.Files["image"]** | Ανακτά το αρχείο του οποίου το όνομα πεδίου φόρμας είναι `image`. | Εγγυάται ένα προβλέψιμο συμβόλαιο για τους καλούντες. |
| **Content‑type check** | Επικυρώνει ότι το αρχείο είναι εικόνα (π.χ., `image/png`). | Αποτρέπει τη μηχανή OCR από το να «πνίγει» με δεδομένα που δεν είναι εικόνα. |
| **Image.FromStream** | Μετατρέπει το ακατέργαστο stream σε ένα `System.Drawing.Image`. | Η βιβλιοθήκη OCR αναμένει ένα αντικείμενο `Image`, όχι έναν ακατέργαστο πίνακα bytes. |
| **ocr.Recognize(img)** | Καλεί τη μηχανή OCR για **πώς να αναγνωρίσει κείμενο από εικόνα**. | Αυτό είναι το βασικό βήμα **εκτέλεσης OCR στην εικόνα**. |
| **Results.Text** | Επιστρέφει την απάντηση σε απλό κείμενο. | Μια απλή, καταναλώσιμη μορφή για τις επόμενες υπηρεσίες. |

## Βήμα 5: Εκτέλεση του API

Finally, start the web server.

```csharp
app.Run();
```

When you execute `dotnet run`, the API will listen on `http://localhost:5000` (or a port of your choosing). You can test it with `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Αναμενόμενη έξοδος:** Η κονσόλα θα εκτυπώσει τους αναγνωρισμένους χαρακτήρες, π.χ.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Αν η εικόνα είναι θολή ή η γλώσσα δεν υποστηρίζεται, η μηχανή OCR θα επιστρέψει μια κενή συμβολοσειρά ή ένα μήνυμα σφάλματος—χειριστείτε αυτές τις περιπτώσεις σε κώδικα παραγωγής.

## Περιπτώσεις Άκρων & Καλές Πρακτικές

### 1. Μεγάλα Αρχεία

The default request body limit is 30 MB. For larger scans you might need to adjust:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Ασύγχρονο OCR

Some OCR libraries expose async methods (`RecognizeAsync`). If yours does, replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the lambda as `async`.

### 3. Θεωρήσεις Ασφάλειας

- **Επικύρωση μεγέθους αρχείου** πριν το φορτώσετε στη μνήμη.
- **Καθαρισμός του ονόματος αρχείου** εάν ποτέ το γράψετε στο δίσκο.
- **Περιορισμός ρυθμού** του endpoint για αποφυγή επιθέσεων άρνησης υπηρεσίας.

### 4. Επιτάχυνση GPU

Αν αποσχολιάσετε τη γραμμή `engine.GpuDevice = new GpuDevice(0);` και το υλικό σας υποστηρίζει CUDA ή DirectML, θα δείτε μια αξιοσημείωτη αύξηση ταχύτητας, ειδικά σε εικόνες υψηλής ανάλυσης.

## Πλήρες Παράδειγμα Λειτουργίας

Below is the complete `Program.cs` you can copy‑paste into a fresh Minimal API project.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Αποθηκεύστε, τρέξτε `dotnet run`, και είστε έτοιμοι να **εξάγετε κείμενο από εικόνα** κατόπιν ζήτησης.

## Συμπέρασμα

Διασχίσαμε μια **πλήρη, από άκρη σε άκρη λύση** για την εξαγωγή κειμένου από εικόνα χρησιμοποιώντας ASP.NET Core Minimal API. Ξεκινώντας από τη δημιουργία του έργου, **καταχωρήσαμε ένα singleton OCR engine**, χτίσαμε ένα endpoint που **ανεβάζει εικόνα μέσω POST**, **διαβάζει multipart form data**, και τελικά **εκτελεί OCR στην εικόνα** για να επιστρέψει καθαρό απλό κείμενο.

Από εδώ μπορείτε:

- Να προσθέσετε JSON wrappers για πιο πλούσιες απαντήσεις.  
- Να ενσωματώσετε μια βάση δεδομένων για αποθήκευση του εξαγόμενου κειμένου.  
- Να επεκτείνετε την υποστήριξη σε πολλές γλώσσες (`OcrLanguage.Spanish`, κλπ).

Το πρότυπο κλιμακώνεται άψογα—απλώς ενσωματώστε το ίδιο endpoint σε μια μεγαλύτερη μικροϋπηρεσία ή εκθέστε το πίσω από ένα API gateway.

Έχετε ερωτήσεις σχετικά με την επεξεργασία PDF, την επεξεργασία παρτίδων ή τη βελτιστοποίηση GPU; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

## Σχετικά Μαθήματα

- [Εξαγωγή Κειμένου από Εικόνα Χρησιμοποιώντας Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}