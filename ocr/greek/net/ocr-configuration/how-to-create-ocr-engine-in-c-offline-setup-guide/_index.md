---
category: general
date: 2026-03-04
description: Μάθετε πώς να δημιουργήσετε OCR σε C# χωρίς internet. Αυτός ο οδηγός
  βήμα‑βήμα δείχνει επίσης πώς να εκτελείτε OCR εκτός σύνδεσης χρησιμοποιώντας τοπικούς
  πόρους.
draft: false
keywords:
- how to create OCR
- how to run OCR
- offline OCR C#
- local OCR resources
- OcrEngine setup
language: el
og_description: Πώς να δημιουργήσετε OCR σε C# χωρίς κλήσεις δικτύου. Ακολουθήστε
  αυτόν τον οδηγό για να μάθετε πώς να εκτελείτε OCR τοπικά χρησιμοποιώντας έναν LocalResourceProvider.
og_title: Πώς να δημιουργήσετε μηχανή OCR σε C# – Εγκατάσταση εκτός σύνδεσης
tags:
- OCR
- C#
- Offline Processing
title: Πώς να δημιουργήσετε μηχανή OCR σε C# – Οδηγός εγκατάστασης εκτός σύνδεσης
url: /el/net/ocr-configuration/how-to-create-ocr-engine-in-c-offline-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Δημιουργήσετε Μηχανή OCR σε C# – Οδηγός Εγκατάστασης Εκτός Σύνδεσης

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε OCR** που ποτέ δεν συνδέεται στο διαδίκτυο; Ίσως δημιουργείτε μια ασφαλή εφαρμογή επιφάνειας εργασίας, ή απλώς δεν σας αρέσουν οι ασταθείς κλήσεις δικτύου. Σε κάθε περίπτωση, θα θέλετε μια μηχανή OCR που να ζει εξ ολοκλήρου στον υπολογιστή του πελάτη.  

Τα καλά νέα; Είναι αρκετά απλό. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από **πώς να δημιουργήσετε OCR**, και στη συνέχεια θα σας δείξουμε **πώς να εκτελέσετε OCR** σε λειτουργία εκτός σύνδεσης χρησιμοποιώντας ένα `LocalResourceProvider`. Στο τέλος θα έχετε ένα αυτόνομο απόσπασμα C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET — χωρίς εξωτερικές υπηρεσίες.

## Τι Θα Μάθετε

- Τα ελάχιστα προαπαιτούμενα για μια ρύθμιση OCR εκτός σύνδεσης.  
- Πώς να δημιουργήσετε ένα `OcrEngine` και να το κατευθύνετε σε έναν τοπικό φάκελο πόρων.  
- Γιατί η χρήση τοπικού παρόχου εξαλείφει την καθυστέρηση δικτύου και βελτιώνει το απόρρητο.  
- Συνηθισμένα προβλήματα (ελλιπή αρχεία, λανθασμένες διαδρομές) και πώς να τα αποφύγετε.  

Όλος ο κώδικας που χρειάζεστε περιλαμβάνεται, μαζί με ένα γρήγορο βήμα επαλήθευσης ώστε να δείτε τη μηχανή σε δράση αμέσως μετά την αντιγραφή‑επικόλληση.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. **.NET 6.0 ή νεότερο** – η βιβλιοθήκη OCR που θα χρησιμοποιήσουμε στοχεύει .NET Standard 2.0, οπότε οποιαδήποτε πρόσφατη έκδοση runtime λειτουργεί.  
2. **Έναν φάκελο με πόρους OCR** – πακέτα γλωσσών, αρχεία εκπαιδευμένων δεδομένων και τυχόν βοηθητικά εκτελέσιμα. Αν δεν τα έχετε ακόμη, κατεβάστε το κατάλληλο πακέτο από το offline bundle του προμηθευτή και αποσυμπιέστε το στο `C:\MyApp\OcrResources`.  
3. **Visual Studio 2022** (ή οποιοδήποτε IDE προτιμάτε).  

Αυτό είναι όλο — χωρίς πακέτα NuGet που κάνουν κλήσεις στο διαδίκτυο κατά την εκτέλεση.

![Διάγραμμα που δείχνει τη ροή OCR εκτός σύνδεσης – πώς να δημιουργήσετε μηχανή OCR χωρίς κλήσεις δικτύου](offline-ocr-diagram.png)

*Image alt text: διάγραμμα δημιουργίας μηχανής OCR εκτός σύνδεσης*

---

## Βήμα 1: Προσθήκη Αναφοράς στη Βιβλιοθήκη OCR

Πρώτα, προσθέστε την αναφορά στο assembly του OCR SDK στο έργο σας. Αν έχετε ένα `.dll` από τον προμηθευτή, κάντε δεξί‑κλικ **References → Add Reference** και περιηγηθείτε στο `OcrSdk.dll`. Εναλλακτικά, αν το SDK διανέμεται ως πακέτο NuGet που υποστηρίζει λειτουργία εκτός σύνδεσης, εκτελέστε:

```bash
dotnet add package OcrSdk --version 3.2.1
```

> **Pro tip:** Καρφώστε τον αριθμό έκδοσης. Η αναβάθμιση αργότερα μπορεί να εισάγει breaking changes που επηρεάζουν τη διαδρομή των τοπικών πόρων.

---

## Βήμα 2: Δημιουργία του Αντικειμένου OCR Engine  

Τώρα θα δημιουργήσουμε πραγματικά **πώς να δημιουργήσετε OCR** κατασκευάζοντας ένα αντικείμενο `OcrEngine`. Αυτό το αντικείμενο είναι το σημείο εισόδου για όλες τις εργασίες αναγνώρισης.

```csharp
using OcrSdk;               // Namespace provided by the OCR library
using OcrSdk.Resources;    // Contains LocalResourceProvider

// ...

// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί χρειάζεται μια αφιερωμένη μηχανή; Το `OcrEngine` κρατά τη διαμόρφωση, κάνει cache τα μοντέλα γλώσσας και διαχειρίζεται τις ομάδες νημάτων. Η δημιουργία του μία φορά και η επαναχρησιμοποίησή του σε πολλαπλές σάρωση είναι πολύ πιο αποδοτική από τη δημιουργία νέου αντικειμένου για κάθε εικόνα.

---

## Βήμα 3: Κατεύθυνση της Μηχανής σε Τοπικό Φάκελο Πόρων  

Εδώ είναι το κρίσιμο μέρος που σας επιτρέπει **πώς να εκτελέσετε OCR** χωρίς ποτέ να αγγίξετε το διαδίκτυο. Αντιστοιχούμε έναν `LocalResourceProvider` που διαβάζει τα δεδομένα γλώσσας από έναν φάκελο στο δίσκο.

```csharp
// Step 3: Configure the engine to use offline resources
string resourcePath = @"C:\MyApp\OcrResources";
ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);
```

**Τι συμβαίνει στο παρασκήνιο;** Ο `LocalResourceProvider` υλοποιεί το ίδιο interface με τον προεπιλεγμένο cloud‑based provider, αλλά διαβάζει αρχεία `.dat` από το `resourcePath`. Αυτό το κόλπο εγγυάται ότι όλες οι επόμενες κλήσεις OCR παραμένουν τοπικές.

> **Προσοχή:** Αν η διαδρομή είναι λανθασμένη ή ο φάκελος λείπουν τα απαιτούμενα αρχεία (`eng.traineddata`, `ocr_config.xml`, κλπ.), η μηχανή θα ρίξει ένα `ResourceNotFoundException`. Πάντα επικυρώστε τον φάκελο πριν τον αντιστοιχίσετε.

---

## Βήμα 4: Επαλήθευση ότι η Μηχανή είναι Έτοιμη  

Μια γρήγορη έλεγχος λογικής σας σώζει από debugging αργότερα. Καλέστε `IsReady` (ή την αντίστοιχη ιδιότητα) και εκτυπώστε το αποτέλεσμα.

```csharp
// Step 4: Verify the engine can locate its resources
if (ocrEngine.IsReady)
{
    Console.WriteLine("✅ OCR engine is ready – offline mode confirmed.");
}
else
{
    Console.WriteLine("❌ OCR engine failed to load resources. Check the path and files.");
    return;
}
```

Θα πρέπει να δείτε το πράσινο σημάδι ελέγχου στην κονσόλα. Αν δείτε το κόκκινο σταυρό, ελέγξτε ξανά ότι το `resourcePath` δείχνει στον φάκελο που περιέχει τα πακέτα γλώσσας.

---

## Βήμα 5: Εκτέλεση OCR σε Δείγμα Εικόνας  

Τέλος, ας κάνουμε πραγματικά **πώς να εκτελέσετε OCR** σε μια εικόνα. Τοποθετήστε μια εικόνα με όνομα `sample.png` στον ίδιο φάκελο πόρων (ή σε οποιαδήποτε προσβάσιμη θέση) και δώστε την στη μηχανή.

```csharp
// Step 5: Perform OCR on a local image
string imagePath = Path.Combine(resourcePath, "sample.png");

// Load the image (the SDK may provide its own Image class)
var ocrImage = OcrImage.FromFile(imagePath);

// Run recognition – this call is completely offline
OcrResult result = ocrEngine.Recognize(ocrImage);

// Output the recognized text
Console.WriteLine("🖋️ Recognized Text:");
Console.WriteLine(result.Text);
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `sample.png` περιέχει τη φράση “Hello OCR!”):

```
🖋️ Recognized Text:
Hello OCR!
```

Αν το αποτέλεσμα είναι κενό, επαληθεύστε ότι η εικόνα είναι καθαρή και ότι το μοντέλο γλώσσας για τα Αγγλικά (`eng`) υπάρχει στο `OcrResources`.

---

## Ακραίες Περιπτώσεις & Συνηθισμένα Πιθανά Σφάλματα  

| Κατάσταση | Τι Συμβαίνει | Πώς να το Διορθώσετε |
|-----------|--------------|----------------------|
| **Λείπει αρχείο γλώσσας** | `ResourceNotFoundException` στο βήμα 3 | Βεβαιωθείτε ότι το `eng.traineddata` (ή η γλώσσα‑στόχος σας) υπάρχει στον φάκελο. |
| **Κατεστραμμένη εικόνα** | `OcrException` με “Unsupported format” | Μετατρέψτε την εικόνα σε PNG ή BMP πριν τη δώσετε στη μηχανή. |
| **Πολλά νήματα** | Συνθήκες αγώνα αν δημιουργήσετε πολλές μηχανές | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `OcrEngine`; είναι thread‑safe για ταυτόχρονες κλήσεις `Recognize`. |
| **Διαδρομή με κενά** | Η μηχανή δεν εντοπίζει τους πόρους | Χρησιμοποιήστε αλφαριθμητικό verbatim (`@"C:\Path With Spaces\OcrResources"`) ή διαφύγετε τις ανάστροφες κάθετες. |

---

## Πλήρες Παράδειγμα Λειτουργίας  

Παρακάτω υπάρχει ένα έτοιμο πρόγραμμα κονσόλας που συνδυάζει τα πάντα. Αντιγράψτε τον κώδικα σε ένα νέο έργο `.csproj` και πατήστε **F5**.

```csharp
// File: Program.cs
using System;
using System.IO;
using OcrSdk;
using OcrSdk.Resources;

namespace OfflineOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Point to local resources (offline mode)
            string resourcePath = @"C:\MyApp\OcrResources";
            ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);

            // 3️⃣ Verify the engine can load resources
            if (!ocrEngine.IsReady)
            {
                Console.WriteLine("❌ Engine failed to initialize. Check your resource folder.");
                return;
            }
            Console.WriteLine("✅ Engine initialized successfully.");

            // 4️⃣ Load a test image
            string imagePath = Path.Combine(resourcePath, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            var ocrImage = OcrImage.FromFile(imagePath);

            // 5️⃣ Run OCR – entirely offline
            OcrResult result = ocrEngine.Recognize(ocrImage);

            // 6️⃣ Show the result
            Console.WriteLine("\n🖋️ Recognized Text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Η εκτέλεση του προγράμματος** θα πρέπει να εκτυπώσει τα μηνύματα επιβεβαίωσης και το εξαγόμενο κείμενο, αποδεικνύοντας ότι τώρα ξέρετε **πώς να δημιουργήσετε OCR** και **πώς να εκτελέσετε OCR** χωρίς ποτέ να βγείτε από τη μηχανή.

---

## Συμπέρασμα  

Καλύψαμε όλα όσα χρειάζεστε για να μάθετε **πώς να δημιουργήσετε OCR** σε ένα έργο C# και δείξαμε **πώς να εκτελέσετε OCR** εντελώς εκτός σύνδεσης. Με τη διαμόρφωση ενός `LocalResourceProvider`, εξαλείφετε την καθυστέρηση δικτύου, προστατεύετε ευαίσθητα δεδομένα και αποκτάτε πλήρη έλεγχο του κύκλου ζωής του OCR.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αντικαταστήσετε το μοντέλο Αγγλικών με άλλη γλώσσα, ή πειραματιστείτε με διαφορετικά βήματα προεπεξεργασίας εικόνας (μετατροπή σε γκρι, διόρθωση κλίσης) για να βελτιώσετε την ακρίβεια. Το ίδιο μοτίβο ισχύει — απλώς κατευθύνετε τη μηχανή σε διαφορετικό φάκελο πόρων.

Αν αντιμετωπίσετε δυσκολίες, επιστρέψτε στον πίνακα ακραίων περιπτώσεων παραπάνω ή αφήστε ένα σχόλιο· καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}