---
category: general
date: 2026-05-06
description: Μάθετε πώς να εκτελείτε OCR σε αρχεία PDF χρησιμοποιώντας το Aspose OCR
  σε C#. Αυτό το σεμινάριο δείχνει επίσης πώς να εξάγετε κείμενο από PDF και να φορτώνετε
  PDF για OCR.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: el
og_description: Ανακαλύψτε πώς να εκτελείτε OCR σε PDF χρησιμοποιώντας το Aspose OCR
  σε C#. Κώδικας βήμα‑βήμα, εξηγήσεις και συμβουλές για την αποδοτική εξαγωγή κειμένου
  από PDF.
og_title: Εκτελέστε OCR σε PDF με το Aspose OCR – Πλήρης Οδηγός
tags:
- Aspose OCR
- C#
- PDF processing
title: Εκτελέστε OCR σε PDF με το Aspose OCR – Πλήρης Οδηγός
url: /el/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε PDF με το Aspose OCR – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε PDF** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα—σκεφτείτε την αυτοματοποιημένη επεξεργασία τιμολογίων ή την ψηφιοποίηση αρχειοθετημένων αναφορών—η δυνατότητα εξαγωγής κειμένου από ένα σαρωμένο PDF είναι απαραίτητη.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική λύση που όχι μόνο **εκτελεί OCR σε PDF** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, αλλά επίσης δείχνει πώς να **εξάγετε κείμενο από PDF**, **φορτώνετε PDF για OCR**, και ακόμη να διαχειριστείτε έγγραφα πολλαπλών γλωσσών. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα C# που μετατρέπει οποιοδήποτε σαρωμένο PDF σε αναζητήσιμο, επεξεργάσιμο κείμενο.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR σε ένα .NET project.  
- Τα ακριβή βήματα για **load PDF for OCR** και την παροχή του στο engine.  
- Πώς να αντιστοιχίσετε διαφορετικές γλώσσες σε μεμονωμένες σελίδες—χρήσιμο όταν ένα PDF συνδυάζει Αγγλικά, Γαλλικά και Γερμανικά.  
- Τρόπους επαλήθευσης του αποτελέσματος και αντιμετώπισης κοινών προβλημάτων.  

> **Pro tip:** Αν εργάζεστε με μεγάλα PDF, σκεφτείτε την επεξεργασία σελίδων παράλληλα για να μειώσετε τα λεπτά εκτέλεσης. Θα το καλύψουμε αργότερα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).  
- Ένα έγκυρο licence του Aspose OCR ή ένα προσωρινό κλειδί αξιολόγησης.  
- Ένα σαρωμένο PDF με όνομα `multilang.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικά σας.  

Δεν απαιτούνται άλλα πακέτα τρίτων.

---

## Βήμα 1 – Εγκατάσταση Aspose OCR και Δημιουργία του Engine

Πρώτα, προσθέστε το πακέτο NuGet Aspose.OCR στο project σας:

```bash
dotnet add package Aspose.OCR
```

Μόλις το πακέτο εγκατασταθεί, μπορείτε να δημιουργήσετε το OCR engine. Αυτό το αντικείμενο είναι η καρδιά της λειτουργίας· γνωρίζει πώς να διαβάζει εικόνες, PDF και να τα μετατρέπει σε κείμενο.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **Why this matters:** Η αρχικοποίηση του engine μία φορά και η επαναχρησιμοποίησή του σε πολλές σελίδες μειώνει το φορτίο μνήμης και επιταχύνει την επεξεργασία.

---

## Βήμα 2 – Φόρτωση του PDF Εγγράφου για OCR

Το engine μπορεί να ανοίξει PDF απευθείας, αλλά πρέπει να του πείτε ποιο αρχείο θα επεξεργαστεί. Αυτό είναι το βήμα **load PDF for OCR** που παραβλέπουν πολλοί προγραμματιστές.

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο μηχάνημά σας. Αν το αρχείο είναι ενσωματωμένο ως πόρος, μπορείτε επίσης να το φορτώσετε από stream.

> **Edge case:** Αν το PDF είναι προστατευμένο με κωδικό, καλέστε `ocrEngine.LoadPdf(path, password)` για να δώσετε τον κωδικό αποκρυπτογράφησης.

---

## Βήμα 3 – Αντιστοίχιση Γλωσσών σε Σελίδες (Προαιρετικό αλλά Ισχυρό)

Συχνά ένα σαρωμένο PDF περιέχει σελίδες σε διαφορετικές γλώσσες. Από προεπιλογή το Aspose OCR υποθέτει Αγγλικά, κάτι που οδηγεί σε φτωχά αποτελέσματα σε Γαλλικές ή Γερμανικές σελίδες. Θα δημιουργήσουμε ένα απλό λεξικό που λέει στο engine ποια γλώσσα να χρησιμοποιήσει ανά σελίδα.

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **Why you’d do this:** Η παροχή της σωστής γλώσσας βελτιώνει δραματικά την ακρίβεια, ειδικά για χαρακτήρες με τόνους και σημεία στίξης ειδικά για κάθε γλώσσα.

---

## Βήμα 4 – Εκτέλεση OCR και Συλλογή του Αποτελέσματος

Τώρα γίνεται η βαριά δουλειά. Η κλήση `Recognize()` επεξεργάζεται *όλες* τις σελίδες σύμφωνα με το χάρτη γλωσσών που μόλις ορίσαμε.

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

Το αντικείμενο `recognitionResult` περιέχει μια ιδιότητα `Text` που συγκεντρώνει το αναγνωρισμένο κείμενο από κάθε σελίδα.

---

## Βήμα 5 – Έξοδος του Εξαγόμενου Κειμένου

Τέλος, απλώς γράφουμε το συνδυασμένο κείμενο στην κονσόλα—ή μπορείτε να το γράψετε σε αρχείο, βάση δεδομένων ή οποιοδήποτε downstream σύστημα.

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

Αν προτιμάτε αρχείο:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **Verification tip:** Ανοίξτε το παραγόμενο `extracted_text.txt` και ψάξτε για γνωστές λέξεις από κάθε γλώσσα. Αν οι γαλλικοί τόνοι εμφανίζονται παραμορφωμένοι, ελέγξτε ξανά το χάρτη γλωσσών.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο console project και πατήστε **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**Expected output** (truncated for brevity):

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## Διαχείριση Μεγάλων PDF και Βελτιώσεις Απόδοσης

Αν το PDF σας περιέχει εκατοντάδες σελίδες, σκεφτείτε τις παρακάτω προσαρμογές:

1. **Chunked processing** – Επεξεργαστείτε 50 σελίδες τη φορά, έπειτα γράψτε ενδιάμεσα αποτελέσματα στο δίσκο.  
2. **Parallelism** – Χρησιμοποιήστε `Parallel.ForEach` με ξεχωριστές παρουσίες `OcrEngine` (κάθε engine είναι thread‑safe μετά την αρχικοποίηση).  
3. **Memory management** – Καλέστε `ocrEngine.Dispose()` μετά από κάθε τμήμα για να ελευθερώσετε τους εγγενείς πόρους.

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## Συνηθισμένα Προβλήματα & Πώς να τα Διορθώσετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|----------|
| Κατεστραμμένοι χαρακτήρες στις γαλλικές σελίδες | Λάθος γλώσσα ορισμένη | Βεβαιωθείτε ότι το `PageLanguageProvider` επιστρέφει `OcrLanguage.French` για αυτές τις σελίδες. |
| Κενό αρχείο εξόδου | PDF δεν φορτώθηκε (λάθος διαδρομή) | Επαληθεύστε τη διαδρομή και ότι το αρχείο δεν είναι κλειδωμένο από άλλη διεργασία. |
| Εξαίρεση Out‑of‑memory σε τεράστια PDF | Το engine φορτώνει ολόκληρο το PDF μονομιάς | Χρησιμοποιήστε την υπερφόρτωση μονής σελίδας του `LoadPdf` ή επεξεργαστείτε σε τμήματα. |
| Αργή επεξεργασία (> 5 min για 100 σελίδες) | Εκτέλεση σε ένα νήμα | Ενεργοποιήστε την παράλληλη επεξεργασία όπως φαίνεται παραπάνω. |

---

## Επόμενα Βήματα – Πέρα από το Βασικό OCR

Τώρα που μπορείτε να **εκτελέσετε OCR σε PDF** και να **εξάγετε κείμενο από PDF**, ίσως θέλετε να:

- **Searchable PDF creation** – Χρησιμοποιήστε Aspose.PDF για να ενσωματώσετε το κείμενο OCR πίσω στο αρχικό PDF, καθιστώντας το αναζητήσιμο.  
- **Data extraction** – Εφαρμόστε κανονικές εκφράσεις για να εξάγετε αριθμούς τιμολογίων, ημερομηνίες ή σύνολα από το εξαγόμενο κείμενο.  
- **Integration with AI** – Στείλτε το αποτέλεσμα OCR σε μοντέλο γλώσσας (π.χ., Azure OpenAI) για περίληψη ή ταξινόμηση.  

Όλες αυτές οι επεκτάσεις εξακολουθούν να βασίζονται στην κύρια δυνατότητα **load PDF for OCR**, οπότε έχετε ήδη τη βάση.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **εκτελέσετε OCR σε PDF** αρχεία χρησιμοποιώντας το Aspose OCR σε C#. Από την εγκατάσταση της βιβλιοθήκης, τη φόρτωση του PDF, την ανάθεση γλωσσών ανά σελίδα, την εκτέλεση του engine αναγνώρισης, μέχρι την τελική **εξαγωγή κειμένου από PDF** και αποθήκευση, το tutorial σας παρέχει μια αυτόνομη, έτοιμη για παραγωγή λύση.  

Μη διστάσετε να πειραματιστείτε με παράλληλη επεξεργασία, διαφορετικούς συνδυασμούς γλωσσών ή ακόμη και να συνδυάσετε το κείμενο OCR με άλλες βιβλιοθήκες επεξεργασίας εγγράφων. Αν αντιμετωπίσετε κάποιο πρόβλημα, ελέγξτε τον πίνακα αντιμετώπισης προβλημάτων παραπάνω ή αφήστε ένα σχόλιο—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}