---
category: general
date: 2026-02-25
description: 'Οδηγός μετατροπής PDF πολλαπλών σελίδων με OCR: μάθετε πώς να μετατρέπετε
  PDF σε HTML, να εξάγετε κείμενο από PDF και να επεξεργάζεστε PDF με OCR χρησιμοποιώντας
  το Aspose OCR σε C#.'
draft: false
keywords:
- ocr multi page pdf
- convert pdf to html
- extract text from pdf
- process pdf with ocr
- recognize pdf pages c#
language: el
og_description: 'Οδηγός μετατροπής PDF πολλαπλών σελίδων με OCR: μάθετε πώς να μετατρέπετε
  PDF σε HTML, να εξάγετε κείμενο από PDF και να επεξεργάζεστε PDF με OCR χρησιμοποιώντας
  το Aspose OCR σε C#.'
og_title: OCR πολυσελίδων PDF – Μετατροπή σε HTML με C# Aspose OCR
tags:
- OCR
- C#
- Aspose
- PDF
title: ocr πολυσελίδα pdf – Μετατροπή σε HTML με C# Aspose OCR
url: /el/net/text-recognition/ocr-multi-page-pdf-convert-to-html-with-c-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr multi page pdf – Μετατροπή σε HTML με C# Aspose OCR

Έχετε ποτέ χρειαστεί να **ocr multi page pdf** αρχεία αλλά δεν ήξερες πώς να διατηρήσεις την αρχική διάταξη; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να εξάγουν κείμενο από PDF διατηρώντας στήλες, πίνακες και εικόνες.  

Το καλό νέο είναι ότι με το Aspose OCR μπορείτε να **process pdf with ocr**, μετατρέψετε κάθε σελίδα σε καθαρό HTML, και να έχετε περιεχόμενο αναζητήσιμο και έτοιμο για το web με λίγες μόνο γραμμές C#.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη ροή εργασίας: από τη φόρτωση ενός multi‑page PDF, τη ρύθμιση της μηχανής για **convert pdf to html**, την εξαγωγή του κειμένου, και τελικά την αποθήκευση κάθε σελίδας ως ανεξάρτητο αρχείο HTML. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστεί

- **.NET 6** ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework).  
- **Aspose.OCR for .NET** πακέτο NuGet (έκδοση 22.12 ή νεότερη).  
- Ένα multi‑page PDF που θέλετε να μετατρέψετε—οποιοδήποτε μέγεθος είναι αποδεκτό, αλλά προσέξτε τη μνήμη για πολύ μεγάλα αρχεία.  
- Ένα περιβάλλον ανάπτυξης όπως το Visual Studio 2022 ή το VS Code.

Δεν απαιτούνται πρόσθετες βιβλιοθήκες· το Aspose OCR διαχειρίζεται εσωτερικά την απόδοση εικόνας, την αναγνώριση και τη δημιουργία HTML.

## Βήμα 1 – Εγκατάσταση Aspose OCR και Δημιουργία του Έργου

Πρώτα, προσθέστε το πακέτο Aspose.OCR στο έργο σας:

```bash
dotnet add package Aspose.OCR
```

Στη συνέχεια, δημιουργήστε μια απλή εφαρμογή console (ή ενσωματώστε τον κώδικα σε υπάρχουσα υπηρεσία):

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            PdfMultiPage.Run();
        }
    }
}
```

**Γιατί είναι σημαντικό:** Η εγκατάσταση του πακέτου φέρνει όλα τα απαραίτητα native binaries για OCR, έτσι δεν χρειάζεται να ανησυχείτε για εξωτερικά εργαλεία όπως το Tesseract. Επίσης σας παρέχει την κλάση `OcrEngine` που κάνει το **recognize pdf pages c#** παιχνιδάκι.

## Βήμα 2 – Φόρτωση του PDF και Ορισμός της Εξόδου σε HTML

Εδώ λέμε στη μηχανή τι θέλουμε: ένα multi‑page PDF να μετατραπεί σε HTML διατηρώντας τη διάταξη.

```csharp
public class PdfMultiPage
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose we need HTML output (keeps columns, tables, etc.)
        ocrEngine.Config.OutputFormat = OutputFormat.Html;

        // 3️⃣ Load the PDF – replace the path with your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");

        // 4️⃣ Run OCR on every page in one go
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Write each page's HTML to a separate file
        for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
        {
            string htmlFile = $"YOUR_DIRECTORY/page_{pageIndex + 1}.html";
            System.IO.File.WriteAllText(htmlFile, ocrResult.GetPageHtml(pageIndex));
            Console.WriteLine($"Saved {htmlFile}");
        }
    }
}
```

**Εξήγηση των βασικών γραμμών**

* `ocrEngine.Config.OutputFormat = OutputFormat.Html;` – Από προεπιλογή το Aspose επιστρέφει απλό κείμενο. Η αλλαγή σε HTML σας επιτρέπει να **convert pdf to html** διατηρώντας τη οπτική δομή.
* `ImageStream.FromFile` – Το Aspose αντιμετωπίζει κάθε σελίδα PDF ως εικόνα εσωτερικά, γι' αυτό το ίδιο API λειτουργεί για σκαναρισμένα PDFs και ψηφιακά PDFs.
* `ocrEngine.Recognize()` – Αυτή η ενιαία κλήση επεξεργάζεται **ocr multi page pdf** σε μία δέσμη, αποφεύγοντας την ανάγκη για χειροκίνητο βρόχο σελίδων.

## Βήμα 3 – Εκτέλεση του Κώδικα και Επαλήθευση του Αποτελέσματος

Συγκεντρώστε (compile) και εκτελέστε:

```bash
dotnet run
```

Θα πρέπει να δείτε έξοδο κονσόλας παρόμοια με:

```
Saved YOUR_DIRECTORY/page_1.html
Saved YOUR_DIRECTORY/page_2.html
...
```

Ανοίξτε οποιοδήποτε από τα παραγόμενα αρχεία `.html` σε έναν περιηγητή. Θα παρατηρήσετε ότι οι επικεφαλίδες, οι πίνακες και ακόμη και οι εικόνες εμφανίζονται ακριβώς όπως στο αρχικό PDF—αυτή είναι η δύναμη του **process pdf with ocr** χρησιμοποιώντας τη μηχανή με επίγνωση διάταξης του Aspose.

**Γρήγορος έλεγχος λογικής:** Αναζητήστε μια γνωστή φράση από το PDF μέσα στο HTML. Αν εμφανιστεί, η εξαγωγή κειμένου πέτυχε.

## Βήμα 4 – Διαχείριση Συνηθισμένων Ακραίων Περιπτώσεων

### PDF με Κωδικό Πρόσβασης

Αν το PDF προέλευσης είναι κρυπτογραφημένο, ορίστε τον κωδικό πριν καλέσετε το `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile("protected.pdf", "myPassword");
```

### Πολύ Μεγάλα PDF

Για PDF με δεκάδες ή εκατοντάδες σελίδες, ίσως θέλετε να τα επεξεργαστείτε σε τμήματα ώστε να αποφύγετε υψηλή χρήση μνήμης:

```csharp
for (int i = 0; i < totalPages; i += 10) // process 10 pages at a time
{
    ocrEngine.Image = ImageStream.FromFile("big.pdf", startPage: i, pageCount: 10);
    var result = ocrEngine.Recognize();
    // save result as before
}
```

### Προσαρμοσμένες Γλώσσες OCR

Το Aspose περιλαμβάνει την Αγγλική γλώσσα από την αρχή, αλλά μπορείτε να φορτώσετε επιπλέον πακέτα γλώσσας:

```csharp
ocrEngine.Config.Language = Language.English | Language.Spanish;
```

### Όταν Χρειάζεστε Μόνο Απλό Κείμενο

Αν αποφασίσετε αργότερα ότι το **extract text from pdf** χωρίς HTML είναι αρκετό, απλώς αλλάξτε τη μορφή εξόδου:

```csharp
ocrEngine.Config.OutputFormat = OutputFormat.Text;
```

## Βήμα 5 – Ενσωμάτωση σε Web API (Προαιρετικό)

Πολλές ομάδες προτιμούν να εκθέτουν τη μετατροπή ως REST endpoint. Εδώ είναι ένας ελάχιστος ελεγκτής ASP.NET Core που επαναχρησιμοποιεί την ίδια λογική:

```csharp
[ApiController]
[Route("api/[controller]")]
public class OcrController : ControllerBase
{
    [HttpPost("convert")]
    public IActionResult Convert(IFormFile pdf)
    {
        using var stream = pdf.OpenReadStream();
        var ocrEngine = new OcrEngine
        {
            Image = ImageStream.FromStream(stream)
        };
        ocrEngine.Config.OutputFormat = OutputFormat.Html;
        var result = ocrEngine.Recognize();

        var htmlPages = new List<string>();
        for (int i = 0; i < result.PageCount; i++)
            htmlPages.Add(result.GetPageHtml(i));

        return Ok(htmlPages); // returns a JSON array of HTML strings
    }
}
```

Τώρα οποιοσδήποτε πελάτης μπορεί να στείλει POST ένα PDF και να λάβει έναν πίνακα από HTML strings—ιδανικό για **convert pdf to html** άμεσα.

## Οπτική Επισκόπηση

Below is a schematic of the flow (primary keyword appears in the alt text for SEO):

![Διάγραμμα ροής μετατροπής ocr multi page pdf](/images/ocr-multi-page-pdf-flow.png "ροή μετατροπής ocr multi page pdf")

*Το διάγραμμα δείχνει: Φόρτωση PDF → Ορισμός εξόδου HTML → Recognize → Αποθήκευση HTML ανά σελίδα.*

## Συμβουλές & Προβλήματα

- **Pro tip:** Αποθηκεύστε το αποτέλεσμα OCR σε έναν προσωρινό φάκελο πρώτα, μετά μετακινήστε το στην τελική του θέση. Αυτό αποτρέπει αρχεία που γράφτηκαν μερικώς αν η διαδικασία καταρρεύσει.
- **Watch out for:** PDF που αποτελούνται από επιλέξιμο κείμενο (όχι σκαναρισμένες εικόνες). Το Aspose OCR θα εξακολουθήσει να rasterize κάθε σελίδα, κάτι που μπορεί να είναι πιο αργό. Σε αυτές τις περιπτώσεις, σκεφτείτε τη χρήση του `PdfExtractor` για άμεση εξαγωγή κειμένου.
- **Performance tip:** Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine` για πολλαπλά PDF όταν είναι δυνατόν· η μηχανή αποθηκεύει στην cache τα δεδομένα γλώσσας, μειώνοντας τον χρόνο εκκίνησης έως και 30 %.
- **Debugging:** Αν μια σελίδα φαίνεται κενή, ελέγξτε τη ρύθμιση DPI (`ocrEngine.Config.Dpi`). Η αύξηση από το προεπιλεγμένο 300 σε 400 μπορεί να βελτιώσει την αναγνώριση σε σάρωση χαμηλής αντίθεσης.

## Αναμενόμενα Αποτελέσματα

Running the sample on a 3‑page invoice PDF yields three files:

- `page_1.html` – περιέχει την κεφαλίδα και το λογότυπο της εταιρείας.
- `page_2.html` – εμφανίζει τα στοιχεία γραμμής σε πίνακα που ταιριάζει με την αρχική διάταξη.
- `page_3.html` – δείχνει τα σύνολα και τους όρους πληρωμής.

Ανοίγοντας οποιοδήποτε αρχείο στο Chrome εμφανίζει μια πιστή αναπαραγωγή της αρχικής σελίδας, και μπορείτε να αντιγράψετε‑επικολλήσετε το κείμενο χωρίς να χάσετε την ευθυγράμμιση των στηλών.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή λύση για αρχεία **ocr multi page pdf**, **convert pdf to html**, και **extract text from pdf** χρησιμοποιώντας το Aspose OCR σε C#. Η προσέγγιση διαχειρίζεται έγγραφα με κωδικό πρόσβασης, μεγάλες παρτίδες, και ακόμη ενσωματώνεται ομαλά σε web API, παρέχοντάς σας ένα ευέλικτο θεμέλιο για οποιοδήποτε pipeline επεξεργασίας εγγράφων.

Τι θα ακολουθήσει; Δοκιμάστε να προσθέσετε ένα βήμα post‑processing που αφαιρεί περιττό CSS, ή τροφοδοτήστε το HTML σε έναν ευρετηριαστή μηχανής αναζήτησης. Μπορείτε επίσης να πειραματιστείτε με

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}