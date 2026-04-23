---
category: general
date: 2026-02-13
description: Πώς να διαβάσετε γρήγορα μια απόδειξη χρησιμοποιώντας το Aspose OCR και
  να εξάγετε το ποσό με χρήση regex. Μάθετε βήμα‑βήμα την επεξεργασία της απόδειξης
  με OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: el
og_description: Πώς να διαβάσετε απόδειξη σε C# χρησιμοποιώντας Aspose OCR και regex.
  Αυτός ο οδηγός σας δείχνει πώς να επεξεργαστείτε την απόδειξη με OCR και να εξάγετε
  το συνολικό ποσό.
og_title: Πώς να Διαβάσετε Απόδειξη σε C# – Πλήρης Οδηγός OCR & Regex
tags:
- OCR
- C#
- Regex
- Aspose
title: Πώς να διαβάσετε απόδειξη σε C# – Οδηγός OCR + Regex
url: /el/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διαβάσετε Απόδειξη σε C# – Οδηγός OCR + Regex

Έχετε αναρωτηθεί ποτέ **πώς να διαβάσετε απόδειξη** εικόνες χωρίς να πληκτρολογείτε χειροκίνητα κάθε γραμμή; Σε πολλές εφαρμογές μικρών επιχειρήσεων χρειάζεται να εξάγετε το συνολικό ποσό από μια φωτογραφία απόδειξης, και η χειροκίνητη διαδικασία αναιρεί το σκοπό του αυτοματισμού. Τα καλά νέα; Με το Aspose OCR μπορείτε να αφήσετε τη μηχανή να κάνει το σκληρό έργο, και στη συνέχεια μια απλή κανονική έκφραση θα εντοπίσει το σύνολο. Σε αυτό το tutorial θα περάσουμε από την **επεξεργασία απόδειξης με OCR**, θα εξάγουμε το ποσό χρησιμοποιώντας regex, και θα καταλήξουμε με μια έτοιμη προς χρήση τιμή συνολικού ποσού.

Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα, θα ανακαλύψετε γιατί το μοντέλο γλώσσας απόδειξης είναι σημαντικό, και θα λάβετε συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως διαφορετικά σύμβολα νομισμάτων ή ελλιπείς ετικέτες “Total”. Δεν απαιτούνται εξωτερικά έγγραφα — όλα όσα χρειάζεστε είναι εδώ.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε το Aspose OCR για αναγνώριση ειδικά για αποδείξεις (το μοντέλο γλώσσας `Receipt` διορθώνει αυτόματα την κλίση και το θόρυβο της εικόνας).  
- Πώς να εφαρμόσετε μια κανονική έκφραση που **εξαγωγή ποσού με regex** λειτουργεί για τις περισσότερες αποδείξεις τύπου US.  
- Πώς να διαχειριστείτε κοινές παραλλαγές όπως “TOTAL”, “Total:”, ή “Grand Total – $12.34”.  
- Πώς να εμφανίσετε το αποτέλεσμα με ασφάλεια και τι να κάνετε όταν το μοτίβο δεν βρεθεί.  

**Prerequisites**: .NET 6+ (ή .NET Framework 4.7+), έγκυρη άδεια Aspose OCR ή δοκιμαστική έκδοση, και μια εικόνα απόδειξης αποθηκευμένη τοπικά. Αυτό είναι όλο — χωρίς επιπλέον πακέτα NuGet εκτός του Aspose.OCR.

---

## Βήμα 1 – Εγκατάσταση Aspose OCR και Προετοιμασία του Έργου

### Γιατί είναι σημαντικό

Το Aspose OCR παρέχει ένα ειδικά σχεδιασμένο μοντέλο **επεξεργασία απόδειξης με OCR** που ξέρει πώς να ισιώσει ένα τσαλακωμένο χαρτί και να αγνοήσει τον θόρυβο του φόντου. Η χρήση του γενικού μοντέλου κειμένου θα σας έδινε περισσότερα σφάλματα, ειδικά σε σαρώσεις χαμηλής ανάλυσης.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro tip:** Κρατήστε το αρχείο άδειας εκτός του φακέλου ελέγχου εκδόσεων για να αποφύγετε τυχαίες δεσμεύσεις.

---

## Βήμα 2 – Διαμόρφωση της Μηχανής OCR για Αναγνώριση Απόδειξης

### Γιατί είναι σημαντικό

Το μοντέλο γλώσσας `Receipt` περιλαμβάνει ενσωματωμένη διόρθωση κλίσης και θορύβου, κάτι που βελτιώνει δραματικά την ακρίβεια σε πραγματικές αποδείξεις που συχνά είναι διπλωμένες ή τσαλακωμένες.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Βήμα 3 – Αναγνώριση Κειμένου από την Εικόνα της Απόδειξης

### Γιατί είναι σημαντικό

Χρειάζεστε το ακατέργαστο κείμενο πριν μπορέσετε να εφαρμόσετε οποιοδήποτε regex. Η μέθοδος `RecognizeImage` επιστρέφει ένα `OcrResult` που περιέχει ολόκληρη τη συμβολοσειρά, βαθμολογίες εμπιστοσύνης, και περισσότερα αν τα χρειαστείτε αργότερα.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Expected OCR output (example)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Βήμα 4 – Δημιουργία Regex για **Εξαγωγή Ποσού με Regex**

### Γιατί είναι σημαντικό

Οι αποδείξεις εμφανίζονται σε πολλές μορφές, αλλά η λέξη “Total” (ή μια κοντινή παραλλαγή) ακολουθούμενη από ποσό σε δολάρια είναι αξιόπιστο άγκυρο. Το παρακάτω μοτίβο αντέχει προαιρετικά κενά, άνω-κάτω (colon), παύλες, και ένα προαιρετικό σύμβολο `$`.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Explanation of the pattern**

| Μέρος | Σημασία |
|------|---------|
| `Total` | Αναζητά τη λέξη “Total” (χωρίς διάκριση πεζών‑κεφαλαίων). |
| `\s*[:\-]?` | Επιτρέπει οποιοδήποτε whitespace, έπειτα προαιρετικό άνω-κάτω ή παύλα. |
| `\s*\$?` | Προαιρετικό whitespace και προαιρετικό σύμβολο δολαρίου. |
| `(\d+(\.\d{2})?)` | Καταγράφει ένα ή περισσότερα ψηφία, προαιρετικά ακολουθούμενα από δεκαδικό σημείο και δύο δεκαδικά ψηφία. |

---

## Βήμα 5 – Εμφάνιση του Εξαγόμενου Συνολικού ή Διαχείριση Ελλιπών Δεδομένων

### Γιατί είναι σημαντικό

Ακόμη και το καλύτερο OCR μπορεί να χάσει μια λέξη, ειδικά σε θολές αποδείξεις. Η παροχή μιας κομψής εναλλακτικής αποτρέπει καταρρεύσεις και σας δίνει ένα σημείο εισόδου για προσαρμοσμένη λογική (π.χ., ζητήστε επιβεβαίωση από τον χρήστη).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Sample console output**  
```
Total: $12.25
```

---

## Πλήρες Παράδειγμα Λειτουργίας – Όλα τα Βήματα σε Ένα Αρχείο

Παρακάτω υπάρχει ένα ενιαίο, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα έργο κονσόλας. Περιλαμβάνει σχόλια, διαχείριση σφαλμάτων, και την προαιρετική φόρτωση άδειας.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Running the program**

1. Δημιουργήστε ένα νέο έργο κονσόλας (`dotnet new console -n ReceiptReader`).  
2. Προσθέστε το πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Αντικαταστήστε το `YOUR_DIRECTORY/receipt.jpg` με την πραγματική διαδρομή σε μια εικόνα απόδειξης.  
4. Κατασκευάστε και τρέξτε (`dotnet run`).  

Θα πρέπει να δείτε το dump του OCR ακολουθούμενο από `Total: $xx.xx` αν όλα ευθυγραμμιστούν.

---

## Διαχείριση Ειδικών Περιπτώσεων & Κοινών Παραλλαγών

### 1. Διαφορετικά Σύμβολα Νομισμάτων

Αν εργάζεστε με ευρώ (€) ή λίρες (£), επεκτείνετε το μοτίβο:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Ελλιπής Ετικέτα “Total”

Κάποιες αποδείξεις εμφανίζουν μόνο “Grand Total”. Προσθέστε μια εναλλακτική:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Πολλαπλά Συνολικά (π.χ., “Subtotal” και “Total”)

Αν το regex ταιριάζει με την πρώτη εμφάνιση, ίσως θέλετε την **τελευταία** αντιστοίχιση:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Εικόνες Χαμηλής Ανάλυσης

- Αυξήστε το DPI κατά τη σάρωση (`300 DPI` είναι το ιδανικό σημείο).  
- Προεπεξεργάστε την εικόνα με ένα απλό φίλτρο μείωσης θολώματος πριν τη δώσετε στο Aspose (εκτός του πεδίου αυτού του οδηγού, αλλά αξίζει να το εξερευνήσετε).

---

## Pro Tips για Πραγματικά Έργα

- **Cache the OCR result** αν χρειάζεται να εξάγετε πολλά πεδία (φόρος, είδη κ.λπ.) — πληρώνετε το κόστος OCR μόνο μία φορά.  
- **Log the raw OCR text** σε μια βάση δεδομένων· γίνεται πολύτιμο αποδεικτικό ίχνος για αμφισβητούμενες δαπάνες.  
- Όταν δημιουργείτε ένα web API, **run OCR in a background worker**· μπορεί να διαρκέσει μερικές εκατοντάδες χιλιοστά του δευτερολέπτου, κάτι που είναι αποδεκτό ασύγχρονα αλλά όχι ιδανικό για συγχρονική κλήση.  
- **Validate the extracted amount** έναντι επιχειρηματικών κανόνων (π.χ., το ποσό πρέπει να είναι > 0) πριν το αποθηκεύσετε.

---

## Συμπέρασμα

Καλύψαμε **πώς να διαβάσετε απόδειξη** εικόνες σε C# χρησιμοποιώντας το Aspose OCR, και στη συνέχεια **εξαγωγή ποσού με regex** για να βρούμε αξιόπιστα τη γραμμή του συνολικού. Εκμεταλλευόμενοι το μοντέλο γλώσσας `Receipt` λαμβάνετε κείμενο διορθωμένο για κλίση και θόρυβο, και μια σύντομη κανονική έκφραση διαχειρίζεται την πλειονότητα των ιδιωματισμών μορφοποίησης. Το πλήρες απόσπασμα κώδικα παραπάνω είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε έργο .NET κονσόλας ή υπηρεσίας, και οι προτάσεις για ειδικές περιπτώσεις σας δίνουν μια σταθερή βάση για παραγωγική χρήση.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να επεκτείνετε τη λύση ώστε να εξάγετε μεμονωμένα στοιχεία γραμμής, να υπολογίζετε αυτόματα τον φόρο, ή να ενσωματώσετε με ένα API παρακολούθησης εξόδων. Και αν συναντήσετε μια απόδειξη που σπάει το μοτίβο, θυμηθείτε ότι η προσέγγιση **regex find total** είναι μόνο ένα ξεκίνημα — μπορείτε πάντα να προσαρμόσετε το μοτίβο ώστε να ταιριάζει στη δική σας περιοχή.

Καλή προγραμματιστική, και εύχομαι η επεξεργασία αποδείξεών σας να είναι γρήγορη, ακριβής και πλήρως αυτοματοποιημένη!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}