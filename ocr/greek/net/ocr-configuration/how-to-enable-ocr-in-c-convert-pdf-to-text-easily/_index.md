---
category: general
date: 2026-02-27
description: Πώς να ενεργοποιήσετε το OCR σε C# για να μετατρέψετε PDF σε κείμενο.
  Μάθετε πώς να εξάγετε κείμενο από PDF πολλαπλών γλωσσών χρησιμοποιώντας το Aspose
  OCR.
draft: false
keywords:
- how to enable ocr
- convert pdf to text
- how to extract text
- how to recognize pdf
- recognize pdf text c#
language: el
og_description: Πώς να ενεργοποιήσετε το OCR σε C# και να μετατρέψετε PDF σε κείμενο.
  Οδηγός βήμα‑προς‑βήμα για την εξαγωγή και αναγνώριση κειμένου PDF χρησιμοποιώντας
  το Aspose OCR.
og_title: Πώς να ενεργοποιήσετε το OCR σε C# – Μετατροπή PDF σε κείμενο
tags:
- OCR
- C#
- PDF
- Aspose
title: Πώς να ενεργοποιήσετε το OCR σε C# – Μετατρέψτε εύκολα PDF σε κείμενο
url: /el/net/ocr-configuration/how-to-enable-ocr-in-c-convert-pdf-to-text-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε το OCR σε C# – Μετατρέψτε εύκολα PDF σε κείμενο

Το πώς να ενεργοποιήσετε το OCR σε C# είναι μια ερώτηση που κάνουν πολλοί προγραμματιστές όταν χρειάζεται να εξάγουν κείμενο από PDF. Αν έχετε ποτέ κολλήσει σε ένα σαρωμένο τιμολόγιο και αναρωτηθήκατε *«Πώς μπορώ να εξάγω αυτό το κείμενο χωρίς να το πληκτρολογήσω ξανά;»* βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που όχι μόνο δείχνει **πώς να ενεργοποιήσετε το OCR**, αλλά επίσης παρουσιάζει **πώς να μετατρέψετε PDF σε κείμενο**, **πώς να εξάγετε κείμενο** από πολυγλωσσικά έγγραφα, και **πώς να αναγνωρίσετε περιεχόμενο PDF** χρησιμοποιώντας C#.

Θα χρησιμοποιήσουμε τη βιβλιοθήκη Aspose.OCR, η οποία υποστηρίζει δεκάδες γλώσσες έτοιμες για χρήση, ώστε να μην χρειάζεται να διαχειρίζεστε ξεχωριστές μηχανές για Αγγλικά, Αραβικά, Ιαπωνικά ή οποιοδήποτε άλλο σύστημα γραφής. Στο τέλος αυτού του οδηγού θα έχετε μια μοναδική μέθοδο που **αναγνωρίζει κείμενο PDF C#**, το εκτυπώνει στην κονσόλα και μπορεί να ενσωματωθεί σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα – Τι χρειάζεστε πριν ξεκινήσετε

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)
- Άδεια ή δωρεάν δοκιμή του **Aspose.OCR for .NET** – μπορείτε να πάρετε ένα προσωρινό κλειδί από την ιστοσελίδα της Aspose.
- Ένα δείγμα PDF που περιέχει πολλές γλώσσες (θα το ονομάσουμε `multilang.pdf`).

Αν λείπει κάποιο από αυτά, κατεβάστε το SDK από την ιστοσελίδα της Microsoft και εγκαταστήστε το πακέτο NuGet:

```bash
dotnet add package Aspose.OCR
```

Αυτό είναι όλο το setup. Έτοιμοι; Ας βουτήξουμε.

## Πώς να ενεργοποιήσετε το OCR σε C# – Ρύθμιση και Διαμόρφωση

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία του OCR engine και να του πείτε ποιες γλώσσες περιμένετε. Αυτό είναι το βήμα **πώς να ενεργοποιήσετε το OCR** που τροφοδοτεί το υπόλοιπο workflow.

```csharp
using Aspose.OCR;
using System;

public class OcrDemo
{
    public static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Enable the languages you need (English, Arabic, Japanese)
        ocrEngine.Language = OcrLanguage.English |
                             OcrLanguage.Arabic |
                             OcrLanguage.Japanese;

        // Step 3: Recognize text from the PDF file
        string recognizedText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

        // Step 4: Output the extracted text
        Console.WriteLine(recognizedText);
    }
}
```

**Γιατί είναι σημαντικό:** Ορίζοντας ρητά την ιδιότητα `Language` καθοδηγείτε τη μηχανή να διαθέσει τα σωστά μοντέλα χαρακτήρων, κάτι που βελτιώνει δραματικά την ακρίβεια — ιδιαίτερα για PDF με μεικτά σύμβολα. Η παράλειψη αυτού του βήματος (ή η χρήση της προεπιλογής) θα έκανε τη μηχανή να μαντεύει, συχνά οδηγώντας σε ακατάληπτο αποτέλεσμα.

> **Pro tip:** Αν γνωρίζετε ότι τα έγγραφά σας περιέχουν μόνο μία γλώσσα, περιορίστε τη σημαία σε αυτή τη γλώσσα. Αυτό επιταχύνει την επεξεργασία έως και 30 %.

### Image – Visual Overview of Enabling OCR  
![Screenshot of OCR engine configuration showing how to enable OCR in C#](/images/enable-ocr-csharp.png)

*Alt text: Διάγραμμα που απεικονίζει πώς να ενεργοποιήσετε το OCR σε C# χρησιμοποιώντας Aspose.OCR.*

## Μετατροπή PDF σε κείμενο με Aspose OCR

Τώρα που το **πώς να ενεργοποιήσετε το OCR** έχει διευθετηθεί, ας μιλήσουμε για την πραγματική μετατροπή. Η μέθοδος `RecognizeFromFile` κάνει το σκληρό έργο: ανοίγει το PDF, εκτελεί το OCR engine σε κάθε σελίδα και επιστρέφει ένα ενιαίο string που περιέχει όλους τους εξαγόμενους χαρακτήρες.

### Τι συμβαίνει στο παρασκήνιο;

1. **Rasterization σελίδας** – Κάθε σελίδα PDF μετατρέπεται σε bitmap, επειδή το OCR λειτουργεί σε εικόνες.
2. **Επιλογή μοντέλου γλώσσας** – Βάσει των σημαιών που ορίσατε νωρίτερα, η μηχανή επιλέγει το κατάλληλο νευρωνικό δίκτυο.
3. **Ανίχνευση γραμμών κειμένου** – Η μηχανή εντοπίζει γραμμές κειμένου, ακόμη και όταν είναι λοξά.
4. **Αποκωδικοποίηση χαρακτήρων** – Τελικά, αντιστοιχίζει τα πρότυπα pixel σε χαρακτήρες Unicode.

Επειδή η μέθοδος επιστρέφει ένα απλό string, μπορείτε να **μετατρέψετε PDF σε κείμενο** με μία γραμμή κώδικα. Αν χρειάζεστε πιο λεπτομερή προσέγγιση (π.χ. επεξεργασία σελίδα‑με‑σελίδα), μπορείτε να καλέσετε `RecognizeFromStream` μέσα σε βρόχο.

## Πώς να εξάγετε κείμενο από PDF πολλαπλών γλωσσών

Ας υποθέσουμε ότι το PDF σας περιέχει τίτλους στα Αγγλικά, σώμα κειμένου στα Αραβικά και υποσημειώσεις στα Ιαπωνικά. Ο κώδικας που δείξαμε νωρίτερα ήδη διαχειρίζεται αυτό το σενάριο, αλλά μπορεί να αναρωτηθείτε **πώς να εξάγετε κείμενο** μόνο από ένα συγκεκριμένο γλωσσικό τμήμα.

Μπορείτε να φιλτράρετε το αποτέλεσμα χρησιμοποιώντας απλές λειτουργίες string ή κανονικές εκφράσεις. Ακολουθεί ένα γρήγορο παράδειγμα που εξάγει μόνο τα αγγλικά τμήματα:

```csharp
using System.Text.RegularExpressions;

// After recognizing the whole document...
string allText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

// Regex to keep only ASCII characters (roughly English)
string englishOnly = Regex.Replace(allText, @"[^\u0000-\u007F]+", string.Empty);

Console.WriteLine("English extracted:");
Console.WriteLine(englishOnly);
```

**Γιατί το φιλτράρισμα;** Σε πολλές επιχειρηματικές ροές χρειάζεστε μόνο το τμήμα με λατινικό αλφάβητο για ευρετηρίαση, ενώ το υπόλοιπο αποθηκεύεται αλλού. Αυτό το μοτίβο δείχνει **πώς να εξάγετε κείμενο** αποδοτικά χωρίς δεύτερο πέρασμα OCR.

## Πώς να αναγνωρίσετε PDF – Αντιμετώπιση Ακραίων Περιπτώσεων

Ακόμη και οι καλύτερες μηχανές OCR δυσκολεύονται με ορισμένα PDF. Παρακάτω είναι κοινά προβλήματα και πώς να τα αντιμετωπίσετε:

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Σαρώσεις χαμηλής ανάλυσης (<150 dpi) | Χαμένα χαρακτήρες, ακατάληπτες λέξεις | Προεπεξεργασία PDF με `ocrEngine.ImageProcessingOptions.Dpi = 300;` |
| Σελίδες με περιστροφή | Το κείμενο εμφανίζεται πλαγίως | Ορίστε `ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;` |
| PDF με κωδικό πρόσβασης | `RecognizeFromFile` πετάει εξαίρεση | Περνάτε τον κωδικό: `ocrEngine.RecognizeFromFile(path, "myPassword");` |
| Μεγάλα αρχεία (>100 σελίδες) | Κατάρρευση μνήμης | Επεξεργαστείτε σε τμήματα: φορτώστε 10 σελίδες τη φορά και συνδυάστε τα αποτελέσματα. |

Η υλοποίηση αυτών των προσαρμογών εξασφαλίζει ότι η λύση σας **αναγνωρίζει PDF** αξιόπιστα, ανεξάρτητα από ιδιαιτερότητες.

```csharp
// Example of handling low‑resolution and rotation
ocrEngine.ImageProcessingOptions.Dpi = 300;
ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;
```

## Recognize PDF Text C# – Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Δείχνει **πώς να ενεργοποιήσετε το OCR**, **πώς να μετατρέψετε PDF σε κείμενο**, **πώς να εξάγετε συγκεκριμένα γλωσσικά τμήματα**, και **πώς να διαχειριστείτε κοινές ακραίες περιπτώσεις**.

```csharp
using Aspose.OCR;
using System;
using System.Text.RegularExpressions;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable languages (English, Arabic, Japanese)
            ocrEngine.Language = OcrLanguage.English |
                                 OcrLanguage.Arabic |
                                 OcrLanguage.Japanese;

            // Optional: improve accuracy for low‑res PDFs
            ocrEngine.ImageProcessingOptions.Dpi = 300;
            ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;

            // 3️⃣ Path to your multi‑language PDF
            string pdfPath = @"C:\Docs\multilang.pdf";

            // 4️⃣ Recognize all text
            string fullText = ocrEngine.RecognizeFromFile(pdfPath);
            Console.WriteLine("=== Full extracted text ===");
            Console.WriteLine(fullText);
            Console.WriteLine();

            // 5️⃣ Extract only English (as an example of how to extract text)
            string englishOnly = Regex.Replace(fullText, @"[^\u0000-\u007F]+", string.Empty);
            Console.WriteLine("=== English‑only excerpt ===");
            Console.WriteLine(englishOnly);
        }
    }
}
```

**Αναμενόμενη έξοδος** (κομμένη για συντομία):

```
=== Full extracted text ===
Welcome to our report…
مرحبا بكم في تقريرنا…
ようこそ、私たちのレポートへ…

=== English‑only excerpt ===
Welcome to our report...
```

Τρέξτε το πρόγραμμα, δείξτε το στο PDF σας και θα δείτε την κονσόλα να εκτυπώνει τόσο το πλήρες πολυγλωσσικό κείμενο όσο και το φιλτραρισμένο αγγλικό απόσπασμα.

## Συχνές Ερωτήσεις (και Γρήγορες Απαντήσεις)

- **Λειτουργεί αυτό με .NET Framework 4.7;**  
  Ναι. Το πακέτο NuGet Aspose.OCR στοχεύει στο .NET Standard 2.0, το οποίο είναι συμβατό τόσο με .NET Core όσο και με .NET Framework.

- **Τι γίνεται αν χρειαστεί να κάνω OCR σε εικόνες αντί για PDF;**  
  Χρησιμοποιήστε `ocrEngine.RecognizeFromImage("image.png")`. Οι ίδιες σημαίες γλώσσας ισχύουν, οπότε εξακολουθείτε να εφαρμόζετε **πώς να ενεργοποιήσετε το OCR** μία φορά.

- **Μπορώ να γράψω το αποτέλεσμα σε αρχείο .txt;**  
  Απόλυτα. Αντικαταστήστε `Console.WriteLine(fullText);` με `File.WriteAllText("output.txt", fullText);`.

- **Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;**  
  Το Aspose.OCR εκθέτει αντικείμενα `OcrResult` όπου μπορείτε να διαβάσετε το `Confidence` ανά λέξη. Δείτε την τεκμηρίωση API για `RecognizeFromFile(..., out OcrResult result)`.

## Συμπέρασμα

Καλύψαμε **πώς να ενεργοποιήσετε το OCR** σε C#, σας δείξαμε **πώς να μετατρέψετε PDF σε κείμενο**, εξηγήσαμε **πώς να εξάγετε κείμενο** από συγκεκριμένα γλωσσικά τμήματα, και επιδείξαμε **πώς να αναγνωρίσετε PDF** αρχεία αξιόπιστα χρησιμοποιώντας Aspose OCR. Ο πλήρης, εκτελέσιμος κώδικας παραπάνω σας παρέχει μια σταθερή βάση για ενσωμάτωση OCR σε οποιαδήποτε εφαρμογή .NET — είτε δημιουργείτε σύστημα διαχείρισης εγγράφων, αυτοματοποιημένο επεξεργαστή τιμολογίων, ή πολυγλωσσικό ευρετήριο αναζήτησης.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε τις σημαίες γλώσσας ώστε να συμπεριλάβετε Κινέζικα ή Κορεάτικα, πειραματιστείτε με τις `ImageProcessingOptions` για θορυβώδεις σαρώσεις, ή διοχετεύστε το εξαγόμενο κείμενο σε pipeline επεξεργασίας φυσικής γλώσσας. Όλες αυτές οι επεκτάσεις βασίζονται στην ίδια βασική αρχή: **πώς να ενεργοποιήσετε το OCR** σωστά από την αρχή.

Καλή προγραμματιστική, και εύχομαι τα PDF σας να είναι πάντα αναζητήσιμα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}