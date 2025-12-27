---
category: general
date: 2025-12-27
description: Δημιουργήστε καταγραφέα κονσόλας σε C# και ενεργοποιήστε την αυτόματη
  λήψη σε διορθωμένους πίνακες χρησιμοποιώντας το AsposeAI. Μάθετε πώς να εμφανίζετε
  τη διορθωμένη έξοδο του πίνακα σε λίγα μόνο βήματα.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: el
og_description: Δημιουργήστε καταγραφέα κονσόλας σε C# και ενεργοποιήστε την αυτόματη
  λήψη σε σωστούς πίνακες χρησιμοποιώντας το AsposeAI. Ακολουθήστε αυτόν τον οδηγό
  για να εμφανίσετε γρήγορα το διορθωμένο αποτέλεσμα του πίνακα.
og_title: Δημιουργήστε καταγραφέα κονσόλας και διορθώστε πίνακες με το AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Δημιουργία καταγραφέα κονσόλας και διόρθωση πινάκων με το AsposeAI
url: /el/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία καταγραφέα κονσόλας και διόρθωση πινάκων με AsposeAI

Ποτέ δεν χρειάστηκε να **δημιουργήσετε καταγραφέα κονσόλας** για μια αλυσίδα C# AI αλλά δεν ήξερα πού να ξεκινήσετε; Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία — πώς να δημιουργήσετε έναν καταγραφέα κονσόλας, να ενεργοποιήσετε την αυτόματη λήψη αρχείων μοντέλων και, τέλος, **πώς να διορθώσετε πίνακες** που προέκυψαν από OCR. Στο τέλος θα μπορείτε να **εμφανίσετε τα διορθωμένα αποτελέσματα πινάκων** στην κονσόλα σας με λίγες μόνο γραμμές κώδικα.

Θα καλύψουμε τα πάντα, από την αρχική ρύθμιση του καταγραφέα μέχρι την τελική εκκαθάριση, ώστε να μην χρειάζεται να ψάχνετε σε διάσπαρτη τεκμηρίωση. Δεν απαιτείται προγενέστερη εμπειρία με το AsposeAI· μια βασική κατανόηση του C# και του .NET αρκεί. Καθ' όλη τη διάρκεια θα ρίξουμε κάποιες συμβουλές για **ρυθμίσεις καταγραφέα κονσόλας**, θα συζητήσουμε σενάρια άκρων περιπτώσεων και θα δείξουμε πώς πρέπει να φαίνεται η έξοδος.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- .NET 6.0 ή νεότερο (ο κώδικας χρησιμοποιεί σύγχρονα χαρακτηριστικά της γλώσσας)
- Visual Studio 2022 ή οποιοδήποτε IDE που υποστηρίζει έργα C#
- Πακέτο NuGet **Aspose.AI** εγκατεστημένο (`Install-Package Aspose.AI`)
- Πακέτο NuGet **Aspose.OCR** εγκατεστημένο (`Install-Package Aspose.OCR`)
- Ένα δείγμα αντικειμένου αποτελέσματος OCR (`ocrResult`) από προηγούμενη κλήση Aspose.OCR

Αν λείπει κάτι από τα παραπάνω, κάντε παύση τώρα και φροντίστε να το αποκτήσετε — θα σας ευχαριστήσει αργότερα.

---

## Βήμα 1: Δημιουργία καταγραφέα κονσόλας και αρχικοποίηση AsposeAI

Το πρώτο που χρειαζόμαστε είναι ένας καταγραφέας που γράφει απευθείας στην κονσόλα. Αυτό κάνει την αποσφαλμάτωση εύκολη και μας παρέχει άμεση ανάδραση ενώ τρέχει η μηχανή AI.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Γιατί είναι σημαντικό:**  
`ConsoleLogger` υλοποιεί τη διεπαφή `ILogger`, έτσι οποιαδήποτε εσωτερικά μηνύματα από το AsposeAI (φόρτωση μοντέλου, κατάσταση post‑processor, σφάλματα) εμφανίζονται αμέσως στο τερματικό σας. Είναι ο πιο απλός τρόπος για **ρύθμιση καταγραφέα κονσόλας** χωρίς εξωτερικά πλαίσια καταγραφής.

> **Συμβουλή επαγγελματία:** Αν αργότερα χρειαστείτε καταγραφή σε αρχείο, απλώς αντικαταστήστε το `ConsoleLogger` με έναν προσαρμοσμένο καταγραφέα που υλοποιεί το `ILogger` — ο υπόλοιπος κώδικας παραμένει αμετάβλητος.

---

## Βήμα 2: Ενεργοποίηση αυτόματης λήψης για μοντέλα AI

Το AsposeAI μπορεί να κατεβάσει τα απαιτούμενα αρχεία μοντέλων «on‑the‑fly». Η ενεργοποίηση αυτής της δυνατότητας σας εξοικονομεί το χειροκίνητο κατέβασμα μεγάλων δυαδικών αρχείων.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Τι μπορεί να πάει στραβά;**  
Αν το `DirectoryModelPath` δείχνει σε τοποθεσία μόνο για ανάγνωση, η αυτόματη λήψη θα αποτύχει και θα δείτε εξαίρεση στην κονσόλα. Βεβαιωθείτε ότι ο φάκελος υπάρχει και ότι η εφαρμογή σας έχει δικαιώματα εγγραφής.

---

## Βήμα 3: Δημιουργία post‑processor πινάκων (πώς να διορθώσετε πίνακες)

Οι πίνακες που εξάγονται από OCR είναι συχνά ακατάστατοι — συγχωνευμένα κελιά, ελλιπείς γραμμές ή κείμενο που δεν ευθυγραμμίζεται. Ο `TableAIProcessor` του AsposeAI μπορεί να τους καθαρίσει αυτόματα.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Γιατί λειτουργία AUTO;**  
`AITableDetectionMode.AUTO` επιτρέπει στη μηχανή να εξετάσει το αποτέλεσμα OCR και να αποφασίσει αν χρειάζεται διόρθωση. Αν προτιμάτε χειροκίνητο έλεγχο, μπορείτε να χρησιμοποιήσετε το `MANUAL` και να καλέσετε το `RunCorrection()` μόνοι σας.

---

## Βήμα 4: Σύνδεση του post‑processor και της διαμόρφωσής του

Τώρα ενώνουμε όλα μαζί — καταγραφέα, ρυθμίσεις μοντέλου και τον επεξεργαστή πινάκων.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

Σε αυτό το σημείο η μηχανή AI γνωρίζει *πού* να αποθηκεύσει τα μοντέλα, *πώς* να καταγράφει και *τι* post‑processing να εφαρμόσει. Είναι μια καθαρή διαχωρισμένη αρχιτεκτονική που κάνει τις μελλοντικές αλλαγές αβίαστης δυσκολίας.

---

## Βήμα 5: Εκτέλεση του post‑processor στο αποτέλεσμα OCR

Υποθέτοντας ότι έχετε ήδη ένα `ocrResult` από Aspose.OCR, απλώς παραδώστε το στη μηχανή.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Προειδοποίηση για άκρες περιπτώσεις:**  
Αν το `ocrResult` δεν περιέχει πίνακες, ο επεξεργαστής θα παραλείψει τη διόρθωση σιωπηλά. Μπορείτε να ελέγξετε το `tableProcessor.GetResult().Count` μετά για να βεβαιωθείτε ότι κάτι επεξεργάστηκε.

---

## Βήμα 6: Ανάκτηση και **εμφάνιση διορθωμένου πίνακα** στην έξοδο

Τέλος, ας πάρουμε το καθαρισμένο κείμενο του πίνακα και να το εκτυπώσουμε στην κονσόλα.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

Η έξοδος θα μοιάζει κάπως έτσι (ανάλογα με την πηγή εικόνας):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Αν δείτε κενή συμβολοσειρά, ελέγξτε ξανά αν το OCR ανίχνευσε πραγματικά πίνακα και αν το `AllowAutoDownload` ολοκληρώθηκε επιτυχώς.

---

## Βήμα 7: Εκκαθάριση πόρων

Καλή πρακτική σημαίνει να απελευθερώνετε βαριά αντικείμενα όταν τελειώσετε.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Η παράλειψη αυτού του βήματος μπορεί να αφήσει ανοιχτές χειρολαβές αρχείων, ειδικά στα Windows όπου τα αρχεία μοντέλων παραμένουν κλειδωμένα.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο κονσόλας. Αντικαταστήστε το `"YOUR_DIRECTORY"` με πραγματική διαδρομή και βεβαιωθείτε ότι το `ocrResult` είναι γεμάτο πριν καλέσετε το `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Αναμενόμενη έξοδος κονσόλας** (υποθέτοντας μια απλή εικόνα πίνακα):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## Συχνές Ερωτήσεις & Απαντήσεις

- **Χρειάζεται σύνδεση στο διαδίκτυο για την αυτόματη λήψη;**  
  Ναι. Την πρώτη φορά που ζητείται το μοντέλο, το AsposeAI επικοινωνεί με το CDN του. Αφού το αρχείο αποθηκευτεί στο `DirectoryModelPath`, οι επόμενες εκτελέσεις λειτουργούν offline.

- **Τι γίνεται αν ο πίνακάς μου έχει συγχωνευμένα κελιά;**  
  Το μοντέλο AI προσπαθεί να χωρίσει τα συγχωνευμένα κελιά βάσει οπτικών ενδείξεων. Αν το αποτέλεσμα φαίνεται λανθασμένο, σκεφτείτε προεπεξεργασία της εικόνας (αύξηση αντίθεσης, ευθυγράμμιση περιστροφής) πριν το OCR.

- **Μπορώ να επεξεργαστώ πολλούς πίνακες ταυτόχρονα;**  
  Φυσικά. Το `tableProcessor.GetResult()` επιστρέφει λίστα· κάντε επανάληψη πάνω της για να εκτυπώσετε κάθε πίνακα.

- **Είναι το `ConsoleLogger` ασφαλές για νήματα (thread‑safe);**  
  Γράφει απευθείας στο `System.Console`, το οποίο είναι thread‑safe για απλές εγγραφές. Σε βαριές πολυνηματικές καταστάσεις, ίσως προτιμήσετε έναν προσαρμοσμένο καταγραφέα με συγχρονισμό.

---

## Επόμενα Βήματα & Σχετικά Θέματα

Τώρα που ξέρετε **πώς να διορθώσετε πίνακες**, μπορείτε να:

- **Ενεργοποιήσετε την αυτόματη λήψη** για άλλα μοντέλα AsposeAI (π.χ., μετάφραση γλώσσας).
- **Ρυθμίσετε καταγραφέα κονσόλας** με διαφορετικά επίπεδα καταγραφής (Info, Warning, Error) για πιο λεπτομερή έλεγχο.
- Εξερευνήσετε **εμφάνιση διορθωμένου πίνακα** σε GUI (WinForms ή WPF) αντί για την κονσόλα.
- Συνδυάσετε τη διόρθωση πινάκων με **εξαγωγή δεδομένων** για άμεση εισαγωγή σε βάση δεδομένων.

Κάθε ένα από αυτά βασίζεται στο θεμέλιο που μόλις θέσαμε, οπότε μη διστάσετε να πειραματιστείτε.

---

## Συμπέρασμα

Διασχίσαμε όλο τον κύκλο ζωής του **δημιουργίας καταγραφέα κονσόλας**, της ενεργοποίησης αυτόματης λήψης και της **διόρθωσης πινάκων** με το AsposeAI, ολοκληρώνοντας με έναν καθαρό τρόπο να **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}