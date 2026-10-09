---
category: general
date: 2026-03-05
description: Πώς να αποκτήσετε γρήγορα OCR χρησιμοποιώντας το Aspose.OCR και να αναγνωρίσετε
  κείμενο από ροή σε λίγα απλά βήματα. Μάθετε τον πλήρη κώδικα C# και συμβουλές για
  τη ροή δεδομένων εικόνας.
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: el
og_description: Πώς να χρησιμοποιήσετε OCR σε C# και να αναγνωρίσετε κείμενο από ροή
  χρησιμοποιώντας το Aspose.OCR. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για μια έτοιμη
  προς εκτέλεση λύση.
og_title: Πώς να αποκτήσετε OCR σε C# – Πλήρης οδηγός αναγνώρισης ροής
tags:
- OCR
- C#
- Aspose
title: Πώς να αποκτήσετε OCR σε C# – Αναγνώριση κειμένου από ροή
url: /el/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Λάβετε OCR σε C# – Αναγνώριση Κειμένου από Ροή

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε OCR** να λειτουργεί σε μια εφαρμογή .NET χωρίς πρώτα να αποθηκεύσετε ολόκληρη την εικόνα στο δίσκο; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να **αναγνωρίσουν κείμενο από ροή** — για παράδειγμα όταν επεξεργάζονται εικόνες που φθάνουν μέσω δικτύου, ροής κάμερας ή API αποθήκευσης στο cloud.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει ακριβώς αυτό. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα C# που δημιουργεί μια μηχανή Aspose OCR, στέλνει κομμάτια εικόνας σε αυτήν μέσω ροής και εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα. Χωρίς μυστηριώδη εξωτερικά εργαλεία, μόνο καθαρός κώδικας και μερικές πρακτικές συμβουλές.

## Τι Θα Μάθετε

- Πώς να εγκαταστήσετε και να αδειοδοτήσετε τη βιβλιοθήκη Aspose.OCR.
- Πώς να τροφοδοτήσετε δεδομένα εικόνας κομμάτι‑με‑κομμάτι χρησιμοποιώντας τη μέθοδο `AppendChunk`.
- Πώς να ξεκινήσετε και να ολοκληρώσετε τον κύκλο αναγνώρισης (`BeginRecognize` / `EndRecognize`).
- Πώς να αντιμετωπίσετε κοινές περιπτώσεις άκρων όπως ελλιπή κομμάτια ή σφάλματα άδειας.
- Πώς φαίνεται η έξοδος και πώς να την επαληθεύσετε.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).
- Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`). Μπορείτε να αποκτήσετε δωρεάν δοκιμή από την ιστοσελίδα της Aspose.
- Βασική εξοικείωση με C# και `async`/`await` εάν θέλετε να διαβάσετε από μια ασύγχρονη ροή (το παράδειγμα χρησιμοποιεί μια συγχρονική ψεύτικη υλοποίηση για σαφήνεια).

> **Γιατί είναι σημαντικό:** Το OCR μέσω ροής σας επιτρέπει να διατηρείτε τη χρήση μνήμης χαμηλή και μειώνει την καθυστέρηση όταν εργάζεστε με μεγάλες εικόνες ή συνεχείς ροές βίντεο. Είναι ένα μοτίβο που θα δείτε σε σαρωτές εγγράφων σε πραγματικό χρόνο, κινητές εφαρμογές και αγωγούς επεξεργασίας στην πλευρά του διακομιστή.

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη του Aspose.OCR

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε το πακέτο NuGet Aspose.OCR.

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

**Συμβουλή:** Εάν χρησιμοποιείτε Visual Studio, κάντε δεξί κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε “Aspose.OCR” και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση.

Τώρα προσθέστε το αρχείο άδειας στη ρίζα του έργου και ορίστε την ιδιότητα **Copy to Output Directory** σε **Copy always**. Αυτό εξασφαλίζει ότι το αρχείο είναι διαθέσιμο κατά την εκτέλεση.

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## Βήμα 2: Αρχικοποίηση της Μηχανής OCR και Εφαρμογή της Άδειας

Η δημιουργία της μηχανής είναι απλή, αλλά η εφαρμογή της άδειας **πρέπει** να γίνει πριν από οποιαδήποτε κλήση αναγνώρισης· διαφορετικά θα αντιμετωπίσετε περιορισμό λειτουργίας δοκιμής.

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

**Γιατί το κάνουμε:** Η έγκαιρη ρύθμιση της άδειας εγγυάται ότι όλες οι επόμενες κλήσεις API εκτελούνται σε πλήρη λειτουργία, αποφεύγοντας το υδατογράφημα “evaluation version”.

## Βήμα 3: Προσομοίωση Πηγής Ροής

Σε μια πραγματική εφαρμογή θα διαβάζατε από `NetworkStream`, `FileStream` ή SDK κάμερας. Για επίδειξη, θα προσομοιώσουμε μια ροή με μια βοηθητική μέθοδο που επιστρέφει έναν πίνακα byte που αντιπροσωπεύει ένα κομμάτι εικόνας JPEG.

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

**Σημείωση περί περιπτώσεων άκρων:** Εάν λαμβάνετε πολλά μικρά κομμάτια, μπορείτε να καλέσετε επανειλημμένα το `engine.Image.AppendChunk(chunk)` πριν τερματίσετε την αναγνώριση. Η μηχανή αποθηκεύει εσωτερικά μέχρι να έχει επαρκή δεδομένα για να ξεκινήσει την επεξεργασία.

## Βήμα 4: Τροφοδοσία Δεδομένων Εικόνας Κομμάτι‑με‑Κομμάτι και Εκτέλεση OCR

Τώρα φέρνουμε όλα μαζί. Η ακολουθία είναι:

1. `BeginRecognize()` – ενημερώνει τη μηχανή ότι πρόκειται να τροφοδοτήσουμε δεδομένα.
2. `AppendChunk()` – προσθέτει κάθε πίνακα byte (μπορείτε να κάνετε βρόχο πάνω σε πολλά κομμάτια).
3. `EndRecognize()` – σηματοδοτεί ότι το τελευταίο κομμάτι έχει σταλεί και ενεργοποιεί την πραγματική αναγνώριση.

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## Βήμα 5: Συνδυάστε Όλα στο `Main`

Ακολουθεί η πλήρης μέθοδος `Main` που ενώνει όλα, εκτυπώνει το αναγνωρισμένο κείμενο και απελευθερώνει τη μηχανή σωστά.

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### Αναμενόμενη Έξοδος

Εάν το `sample.jpg` περιέχει τη φράση “Hello, World!” θα πρέπει να δείτε:

```
=== Recognized Text ===
Hello, World!
```

Εάν η εικόνα είναι θολή ή το κομμάτι είναι ελλιπές, η έξοδος μπορεί να είναι κενή ή να περιέχει ακατάλληλους χαρακτήρες — γι' αυτό είναι κρίσιμος ο σωστός χειρισμός των κομματιών (διασφαλίζοντας ότι το τελευταίο κομμάτι έχει σταλεί).

## Διαχείριση Πολλαπλών Κομματιών (Προχωρημένο)

Όταν εργάζεστε με πραγματικά ροές δεδομένων, πιθανότατα θα λαμβάνετε πολλά μικρά κομμάτια. Το παρακάτω μοτίβο δείχνει πώς να κάνετε βρόχο μέχρι το τέλος της πηγής.

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

**Γιατί βοηθά:** Με τη ροή απευθείας από `NetworkStream` ή `FileStream`, δεν φορτώνετε ποτέ ολόκληρη την εικόνα στη μνήμη, κάτι που είναι ιδιαίτερα ωφέλιμο για μεγάλα PDF ή φωτογραφίες υψηλής ανάλυσης.

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Η άδεια δεν βρέθηκε | `SetLicense` πετάει `FileNotFoundException` | Επαληθεύστε τη διαδρομή και ορίστε *Copy to Output Directory* σε *Copy always*. |
| Κενό αποτέλεσμα | Δεν εκτυπώθηκε κείμενο | Βεβαιωθείτε ότι καλέσατε `BeginRecognize` **πριν** το `AppendChunk` και `EndRecognize` **μετά** το τελευταίο κομμάτι. |
| Διαρροή μνήμης | Η εφαρμογή επιβραδύνεται μετά από πολλές κλήσεις OCR | Απελευθερώστε το `OcrEngine` μετά από κάθε χρήση ή επαναχρησιμοποιήστε μια μόνο παρουσία με σωστές κλήσεις `Dispose`. |
| Κατεστραμμένο κομμάτι | Ακατάλληλοι χαρακτήρες | Επικυρώστε το μέγεθος του κομματιού· για JPEG/PNG τα πρώτα μερικά byte πρέπει να ξεκινούν με `0xFF 0xD8` ή `0x89 0x50`. |

## Μπόνους: Χρήση Ασύγχρονων Ροών

Εάν η πηγή σας είναι μια ροή απόκρισης `HttpClient`, μπορείτε να προσαρμόσετε το βρόχο ώστε να κάνει `await` στις αναγνώσεις:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

## Συμπέρασμα

Τώρα έχετε μια **πλήρη, αυτόνομη λύση για το πώς να κάνετε OCR** σε C# και **να αναγνωρίζετε κείμενο από ροή** χρησιμοποιώντας το Aspose.OCR. Το tutorial κάλυψε τα πάντα, από την αδειοδότηση και την αρχικοποίηση μέχρι την τροφοδοσία κομματιών εικόνας, τη διαχείριση περιπτώσεων άκρων και ακόμη και μια ασύγχρονη παραλλαγή.

Δοκιμάστε το—αντικαταστήστε το `sample.jpg` με μια ζωντανή ροή κάμερας, μια εικόνα αποθηκευμένη στο cloud ή ένα multipart HTTP upload. Μόλις νιώσετε άνετα, εξερευνήστε προχωρημένες δυνατότητες όπως πακέτα γλωσσών, προσαρμοσμένη προεπεξεργασία ή επεξεργασία παρτίδας πολλαπλών ροών.

**Επόμενα βήματα:**  
- Δοκιμάστε OCR σε PDF μετατρέποντας πρώτα κάθε σελίδα σε εικόνα.  
- Πειραματιστείτε με το `engine.Config` για να βελτιώσετε την ακρίβεια για συγκεκριμένες γραμματοσειρές.  
- Συνδυάστε το με Azure Functions ή AWS Lambda για αδιάκοπες αλυσίδες εξαγωγής κειμένου.

Καλή προγραμματιστική, και εύχομαι οι ροές σας πάντα να είναι καθαρές και τα αποτελέσματα OCR άψογα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}