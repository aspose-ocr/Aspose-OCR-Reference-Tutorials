---
category: general
date: 2026-02-20
description: Μάθετε πώς να διαβάζετε απόδειξη σε C# εξάγοντας κείμενο από εικόνα και
  μετατρέποντάς το σε JSON. Κώδικας βήμα‑προς‑βήμα χρησιμοποιώντας Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: el
og_description: Ανακαλύψτε πώς να διαβάσετε απόδειξη σε C# φορτώνοντας ένα αρχείο
  εικόνας, εξάγοντας κείμενο με το Aspose OCR και μετατρέποντας το αποτέλεσμα σε JSON.
  Πλήρες παράδειγμα κώδικα.
og_title: Πώς να διαβάσετε απόδειξη σε C# – Εξαγωγή κειμένου, μετατροπή σε JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Πώς να διαβάσετε απόδειξη σε C# – Πλήρης οδηγός εξαγωγής κειμένου από εικόνα
url: /el/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διαβάσετε Απόδειξη σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να διαβάσετε απόδειξη** εικόνες προγραμματιστικά; Ίσως να δημιουργείτε μια εφαρμογή παρακολούθησης εξόδων και χρειάζεται να εξάγετε τα στοιχεία γραμμής από μια φωτογραφία απόδειξης παντοπωλείου. Από την εμπειρία μου, το μεγαλύτερο πρόβλημα είναι η μετατροπή εκείνου του θολού JPEG σε δομημένα δεδομένα που μπορείτε πραγματικά να χρησιμοποιήσετε. Τα καλά νέα; Με μερικές γραμμές C# και Aspose OCR μπορείτε να **extract text from image**, στη συνέχεια **convert image to JSON** με τρόπο που φαίνεται σχεδόν μαγικός.

Σε αυτό το tutorial θα αποκτήσετε μια έτοιμη προς εκτέλεση λύση που **φορτώνει ένα αρχείο εικόνας C#**, εκτελεί OCR και παράγει ένα λεπτομερές JSON payload. Χωρίς εξωτερικές υπηρεσίες, χωρίς περίπλοκες κλήσεις REST—απλώς καθαρός κώδικας .NET που μπορείτε να ενσωματώσετε σε οποιοδήποτε console ή ASP.NET project. Στο τέλος θα καταλάβετε γιατί κάθε βήμα είναι σημαντικό, πώς να αντιμετωπίζετε κοινές περιπτώσεις άκρων (όπως μη‑τυπικά μεγέθη αποδείξεων), και πώς φαίνεται πραγματικά η έξοδος JSON.

## Τι Θα Χρειαστεί

- **.NET 6.0 ή νεότερο** – ο κώδικας χρησιμοποιεί `System.Drawing.Common` που υποστηρίζεται σε Windows, Linux και macOS.
- **Aspose.OCR για .NET** – μπορείτε να κατεβάσετε ένα δωρεάν trial πακέτο NuGet (`Aspose.OCR`) ή να χρησιμοποιήσετε μια αδειοδοτημένη έκδοση αν την έχετε.
- Μια **δείγμα εικόνας απόδειξης** (`receipt.jpg`) τοποθετημένη κάπου που η εφαρμογή σας μπορεί να διαβάσει.
- Οποιοδήποτε IDE προτιμάτε (Visual Studio, Rider, VS Code).  

Αυτό είναι όλο. Χωρίς επιπλέον ρυθμίσεις, χωρίς κλειδιά API.

---

## Βήμα 1 – Φόρτωση Αρχείου Εικόνας C# (Κύρια Λέξη-Κλειδί σε Δράση)

Πριν η μηχανή OCR μπορέσει να κάνει τη μαγεία της, πρέπει να φορτώσετε την εικόνα στη μνήμη. Αυτό είναι το κλασικό βήμα “load image file C#” που παραβλέπουν πολλοί προγραμματιστές.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Γιατί είναι σημαντικό:**  
`Image.FromFile` διαβάζει το αρχείο *μία φορά* και κρατά ανοιχτό ένα handle, κάτι που είναι τέλειο για μια γρήγορη εκτέλεση OCR. Αν επεξεργάζεστε πολλές αποδείξεις σε βρόχο, σκεφτείτε να χρησιμοποιήσετε `Image.FromStream` για να αποφύγετε το κλείδωμα του αρχείου.

> **Συμβουλή:** Αν αντιμετωπίσετε *FileNotFoundException*, ελέγξτε ξανά τη διαδρομή και βεβαιωθείτε ότι η εικόνα υπάρχει. Οι σχετικές διαδρομές λειτουργούν επίσης (`"./receipt.jpg"`), αλλά οι απόλυτες διαδρομές είναι πιο ασφαλείς για παραγωγικές εργασίες.

---

## Βήμα 2 – Δημιουργία και Ρύθμιση της Μηχανής OCR

Το Aspose OCR έρχεται με ένα έτοιμο `OcrEngine`. Δεν χρειάζεται να εκπαιδεύσετε μοντέλο· η βιβλιοθήκη ήδη ξέρει πώς να διαβάσει εκτυπωμένο κείμενο, που είναι ακριβώς αυτό που χρησιμοποιούν οι περισσότερες αποδείξεις.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Γιατί ορίζουμε αυτές τις επιλογές:**  
`DetectOrientation` λέει στη μηχανή να περιστρέφει αυτόματα την εικόνα αν η απόδειξη έχει σαρωθεί ανάποδα. Ορίζοντας τη γλώσσα περιορίζει το σύνολο χαρακτήρων, κάτι που μπορεί να βελτιώσει την ακρίβεια—ιδιαίτερα όταν χρειάζεστε μόνο αγγλικά αλφαριθμητικά δεδομένα.

---

## Βήμα 3 – Αναγνώριση της Εικόνας και Μετατροπή σε JSON

Τώρα έρχεται το διασκεδαστικό μέρος: **extract text from image** και **convert image to JSON** με μία κλήση.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Η μέθοδος `RecognizeToJson` επιστρέφει μια πλούσια δομή JSON που περιλαμβάνει:

- `Text`: το απλό ενωμένο κείμενο.
- `Lines`: ένας πίνακας αντικειμένων γραμμής με συντεταγμένες.
- `Words`: κάθε λέξη με βαθμούς εμπιστοσύνης.
- `Regions`: περιοριστικά κουτιά για τα ανιχνευμένα μπλοκ κειμένου.

Μπορείτε να αποσαφηνίσετε αυτό το JSON σε αντικείμενο C# αν χρειάζεστε τυποποιημένη πρόσβαση, αλλά για πολλές περιπτώσεις η εκτύπωση του ακατέργαστου JSON είναι αρκετή.

---

## Βήμα 4 – Έξοδος του JSON (ή Αποθήκευση)

Ας δούμε την έξοδο και να συζητήσουμε τι να κάνουμε με αυτήν.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Παράδειγμα Εξόδου

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Τι να κάνετε στη συνέχεια;**  
Αναλύστε τον πίνακα `Lines` για να εξάγετε το ποσό `Total`, ή στείλτε το JSON σε μια υπηρεσία downstream που αποθηκεύει εγγραφές εξόδων. Επειδή το αποτέλεσμα είναι ήδη JSON, μπορείτε να το ενσωματώσετε απευθείας σε οποιαδήποτε NoSQL βάση δεδομένων, Azure Function ή ροή Power Automate.

---

## Βήμα 5 – Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

Ακόμη και οι καλύτερες μηχανές OCR αντιμετωπίζουν προβλήματα σε ορισμένα πράγματα. Παρακάτω είναι σενάρια που μπορεί να συναντήσετε ενώ μαθαίνετε **how to read receipt** εικόνες.

| Κατάσταση | Διόρθωση / Σύσταση |
|-----------|----------------------|
| **Low‑resolution receipt (≤ 150 dpi)** | Upscale the image first using `Bitmap` and `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Rotated or skewed receipt** | Keep `DetectOrientation = true`. For severe skew, pre‑process with `Image.RotateFlip` or a third‑party library like OpenCV. |
| **Colored background (e.g., receipt on a table)** | Convert to grayscale and increase contrast before OCR (`ImageAttributes`). |
| **Multiple receipts in one photo** | Crop each receipt region manually or use `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Large files causing OutOfMemory** | Use `using` statements to dispose `Image` objects promptly, or process in chunks. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Βήμα 6 – Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το *πλήρες* πρόγραμμα που μπορείτε να μεταγλωττίσετε αμέσως. Περιλαμβάνει όλα τα βήματα, τις σωστές οδηγίες `using`, και ευγενικό χειρισμό σφαλμάτων.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Τρέξτε το:**  
`dotnet run` από το φάκελο του project. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το JSON να εκτυπώνεται στην κονσόλα και να αποθηκεύεται δίπλα στην εικόνα της απόδειξης.

---

## Συμπέρασμα

Μόλις καλύψαμε **how to read receipt** εικόνες σε C# από την αρχή μέχρι το τέλος. Φορτώνοντας την εικόνα, ρυθμίζοντας το Aspose OCR και καλώντας το `RecognizeToJson`, μπορείτε να **extract text from image** και **convert image to JSON** με σχεδόν καθόλου boilerplate. Η προσέγγιση κλιμακώνεται—από μια επίδειξη μίας απόδειξης μέχρι έναν επεξεργαστή παρτίδας που διαχειρίζεται εκατοντάδες αποδείξεις κάθε νύχτα.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- **Parse the JSON** για να εξάγετε ημερομηνίες, σύνολα και στοιχεία γραμμής (χρησιμοποιήστε `System.Text.Json` ή `Newtonsoft.Json`).
- **Integrate with a database** (SQL, Cosmos DB) για αυτόματη αποθήκευση εγγραφών εξόδων.
- **Add a UI** (WinForms, WPF, ή Blazor) ώστε οι χρήστες να μπορούν να σύρουν‑και‑αποθέτουν αποδείξεις.
- **Swap Aspose OCR** με άλλη μηχανή (Tesseract, Microsoft Azure OCR) αν η αδειοδότηση είναι πρόβλημα—απλώς διατηρήστε το ίδιο μοτίβο “load image file C#”.

Νιώστε ελεύθεροι να πειραματιστείτε, να σπάσετε πράγματα, και μετά να επιστρέψετε εδώ για μια ανανέωση. Αν αντιμετωπίσετε πρόβλημα, η κοινότητα (και τα φόρουμ Aspose) είναι εξαιρετικά μέρη για ερωτήσεις. Καλή προγραμματιστική, και απολαύστε τη μετατροπή των χαρτινών αποδείξεων σε καθαρά, αναζητήσιμα δεδομένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}