---
category: general
date: 2026-06-06
description: Πώς να χρησιμοποιήσετε το OcrEngine σε C# για γρήγορο OCR πολλαπλών σελίδων.
  Μάθετε πώς να ορίζετε το OcrLanguage, να φορτώνετε αρχεία TIFF/PDF και να εξάγετε
  κείμενο με ελάχιστο κώδικα.
draft: false
keywords:
- how to use ocrengine
- OCR engine C#
- multi‑page OCR
- recognize text from TIFF
- OcrLanguage English
language: el
og_description: Πώς να χρησιμοποιήσετε το OcrEngine σε C# για να εκτελέσετε OCR πολλαπλών
  σελίδων σε αρχεία TIFF ή PDF. Κώδικας βήμα‑προς‑βήμα, εξηγήσεις και συμβουλές.
og_title: Πώς να χρησιμοποιήσετε το OcrEngine σε C# – Πλήρης οδηγός OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to use OcrEngine in C# for fast multi‑page OCR. Learn to set OcrLanguage,
    load TIFF/PDF files, and extract text with minimal code.
  headline: How to Use OcrEngine in C# – Complete OCR Guide
  type: TechArticle
- description: How to use OcrEngine in C# for fast multi‑page OCR. Learn to set OcrLanguage,
    load TIFF/PDF files, and extract text with minimal code.
  name: How to Use OcrEngine in C# – Complete OCR Guide
  steps:
  - name: Expected Output
    text: 'Assuming `multipage.tif` contains three scanned pages, you’ll see something
      like:'
  - name: 1. Switching to a Different Language
    text: '```csharp engine.Language = OcrLanguage.Spanish; // just change the enum
      value ```'
  - name: 2. Processing PDFs Instead of TIFFs
    text: '```csharp engine.Image = ImageStream.FromFile("Resources/document.pdf");
      ```'
  - name: 3. Disposing Resources Properly
    text: 'If `OcrEngine` implements `IDisposable`, wrap the whole block:'
  - name: 4. Large Documents – Page‑by‑Page Streaming
    text: '```csharp int totalPages = engine.GetPageCount(); // hypothetical method
      for (int i = 0; i < totalPages; i++) { engine.Image = ImageStream.FromFile(imagePath,
      pageIndex: i); var pageResult = engine.RecognizeSinglePage(); Console.WriteLine($"---
      Page {i + 1} ---"); Console.WriteLine(pageResult.Text);'
  type: HowTo
tags:
- OCR
- C#
- ImageProcessing
title: Πώς να χρησιμοποιήσετε το OcrEngine σε C# – Πλήρης οδηγός OCR
url: /el/net/ocr-configuration/how-to-use-ocrengine-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το OcrEngine σε C# – Πλήρης Οδηγός OCR

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το OcrEngine** όταν χρειάζεται να εξάγετε κείμενο από ένα σαρωμένο PDF ή ένα πολυ‑σελίδα TIFF; Δεν είστε μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν δυσκολίες στην αυτοματοποίηση της ψηφιοποίησης εγγράφων. Τα καλά νέα είναι ότι με λίγες μόνο γραμμές C# μπορείτε να δημιουργήσετε μια μηχανή OCR, να την κατευθύνετε σε ένα αρχείο και να λάβετε το κείμενο κάθε σελίδας σε ελάχιστο χρόνο.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει **πώς να χρησιμοποιήσετε το OcrEngine** για OCR πολλαπλών σελίδων, θα ορίσουμε το **OcrLanguage** στα Αγγλικά και θα επαναλάβουμε το αποτέλεσμα για κάθε σελίδα. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που εκτυπώνει το εξαγόμενο κείμενο, μαζί με μια σειρά συμβουλών για διαχείριση μεγαλύτερων αρχείων, μη‑Αγγλικών γλωσσών και σωστής εκκαθάρισης πόρων.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Core και .NET Framework)
- Μια αναφορά σε μια βιβλιοθήκη OCR που εκθέτει `OcrEngine`, `OcrLanguage` και `ImageStream` (πολλές εμπορικές και ανοιχτού κώδικα λύσεις χρησιμοποιούν αυτά τα ονόματα· το δείγμα υποθέτει ότι το API είναι ήδη διαθέσιμο)
- Ένα πολυ‑σελίδα αρχείο εικόνας (`.tif` ή `.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα
- Βασική εξοικείωση με εφαρμογές κονσόλας C#

Δεν απαιτούνται πρόσθετα πακέτα NuGet για τη βασική λογική, αλλά θα χρειαστείτε τα DLL της βιβλιοθήκης OCR να είναι αναφερθέντα στο πρόγραμμά σας.

## Ρύθμιση Έργου (Γρήγορη Εκκίνηση)

1. Ανοίξτε το αγαπημένο σας IDE (Visual Studio, VS Code, Rider…).
2. Δημιουργήστε ένα νέο έργο κονσόλας:

   ```bash
   dotnet new console -n OcrEngineDemo
   cd OcrEngineDemo
   ```

3. Προσθέστε μια αναφορά στο assembly OCR (αντικαταστήστε `YourOcrLib.dll` με το πραγματικό αρχείο):

   ```bash
   dotnet add reference path/to/YourOcrLib.dll
   ```

4. Τοποθετήστε ένα πολυ‑σελίδα TIFF με όνομα `multipage.tif` σε φάκελο `Resources` μέσα στη ρίζα του έργου.

Αυτό ήταν—το περιβάλλον σας είναι έτοιμο για το tutorial **πώς να χρησιμοποιήσετε το OcrEngine**.

## Βήμα 1: Εισαγωγή Ονομάτων Χώρων & Αρχικοποίηση της Μηχανής

Το πρώτο πράγμα που κάνετε όταν θέλετε να **χρησιμοποιήσετε το OcrEngine** είναι να φέρετε τα απαιτούμενα namespaces στο scope και να δημιουργήσετε μια παρουσία. Αυτό το αντικείμενο είναι το σημείο εισόδου για κάθε λειτουργία OCR.

```csharp
using System;
using OcrLibrary;          // <-- hypothetical namespace containing OcrEngine
using OcrLibrary.Imaging; // <-- contains ImageStream

namespace OcrEngineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var engine = new OcrEngine();

            // -----------------------------------------------------------------
            // Why this matters:
            // The engine holds configuration (language, DPI, etc.) and manages
            // native resources. Instantiating it once and re‑using it is far
            // more efficient than creating a new engine per page.
            // -----------------------------------------------------------------
```

> **Συμβουλή:** Αν η βιβλιοθήκη OCR σας υλοποιεί `IDisposable`, τυλίξτε τη μηχανή σε ένα `using` block για να εξασφαλίσετε σωστή εκκαθάριση.

## Βήμα 2: Επιλογή Γλώσσας για Αναγνώριση

Οι περισσότερες μηχανές OCR χρειάζονται να γνωρίζουν ποιο μοντέλο γλώσσας θα χρησιμοποιηθεί. Για το κλασικό παράδειγμα **πώς να χρησιμοποιήσετε το OcrEngine** θα παραμείνουμε στα Αγγλικά, αλλά μπορείτε να αντικαταστήσετε το `OcrLanguage.English` με οποιοδήποτε υποστηριζόμενο locale.

```csharp
            // Step 2: Choose the language for recognition
            engine.Language = OcrLanguage.English;

            // -----------------------------------------------------------------
            // Why this matters:
            // Setting the language early lets the engine preload the correct
            // character set and improves accuracy dramatically.
            // -----------------------------------------------------------------
```

Αν χρειαστεί ποτέ να αναγνωρίσετε κείμενο στα Γαλλικά, απλώς αντικαταστήστε το `English` με `French`—το ίδιο μοτίβο **πώς να χρησιμοποιήσετε το OcrEngine** ισχύει.

## Βήμα 3: Φόρτωση Πολυ-σελίδας Εικόνας (TIFF ή PDF)

Τώρα κατευθύνουμε τη μηχανή στο αρχείο που θέλουμε να επεξεργαστούμε. Η μέθοδος `ImageStream.FromFile` αφαιρεί την πολυπλοκότητα του υποκείμενου φορμά, ώστε ο ίδιος κώδικας να λειτουργεί για TIFF και PDF.

```csharp
            // Step 3: Load a multi‑page image (TIFF or PDF) from disk
            string imagePath = "Resources/multipage.tif";
            engine.Image = ImageStream.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Why this matters:
            // Loading the image once allows the engine to batch‑process all pages,
            // which is faster than loading each page individually.
            // -----------------------------------------------------------------
```

**Edge case:** Αν το αρχείο είναι μεγαλύτερο από μερικές εκατοντάδες megabytes, σκεφτείτε τη ροή σελίδα‑με‑σελίδα για να αποφύγετε πίεση μνήμης. Οι περισσότερες βιβλιοθήκες εκθέτουν μια μέθοδο `LoadPage(int index)` για αυτήν την περίπτωση.

## Βήμα 4: Εκτέλεση OCR σε Όλες τις Σελίδες Μαζί

Η καρδιά του **πώς να χρησιμοποιήσετε το OcrEngine** είναι η κλήση `RecognizeMultiPage`. Επιστρέφει μια συλλογή των οποίων τα στοιχεία περιέχουν το κείμενο για κάθε μεμονωμένη σελίδα.

```csharp
            // Step 4: Perform OCR on all pages at once
            var multiPageResult = engine.RecognizeMultiPage();

            // -----------------------------------------------------------------
            // Why this matters:
            // Batch recognition leverages internal optimizations (thread pools,
            // SIMD instructions) and often yields better throughput than
            // looping over `RecognizeSinglePage`.
            // -----------------------------------------------------------------
```

Αν χρειάζεστε μόνο την πρώτη σελίδα, αντικαταστήστε την κλήση με `engine.RecognizeSinglePage()`—το ίδιο μοτίβο παραμένει.

## Βήμα 5: Επανάληψη Μέσα από το Αποτέλεσμα Κάθε Σελίδας και Εμφάνιση Κειμένου

Τέλος, επαναλαμβάνουμε τα αποτελέσματα, εκτυπώνοντας το εξαγόμενο κείμενο κάθε σελίδας στην κονσόλα. Αυτό αντικατοπτρίζει το τυπικό σενάριο εξόδου του **πώς να χρησιμοποιήσετε το OcrEngine**.

```csharp
            // Step 5: Iterate through each page's result and display the extracted text
            for (int pageIndex = 0; pageIndex < multiPageResult.Count; pageIndex++)
            {
                Console.WriteLine($"--- Page {pageIndex + 1} ---");
                Console.WriteLine(multiPageResult[pageIndex].Text);
                Console.WriteLine(); // extra line for readability
            }

            // -----------------------------------------------------------------
            // Why this matters:
            // Separating pages with a header makes the console output easy to scan,
            // especially when dealing with long documents.
            // -----------------------------------------------------------------
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι το `multipage.tif` περιέχει τρεις σαρωμένες σελίδες, θα δείτε κάτι όπως:

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.
```

Αν η μηχανή OCR αποτύχει να αναγνωρίσει μια σελίδα, η αντίστοιχη ιδιότητα `Text` θα είναι κενή συμβολοσειρά—πάντα ελέγχετε αυτόν τον όρο σε κώδικα παραγωγής.

## Διαχείριση Συνηθισμένων Παραλλαγών & Ακραίων Περιπτώσεων

### 1. Αλλαγή σε Διαφορετική Γλώσσα

```csharp
engine.Language = OcrLanguage.Spanish; // just change the enum value
```

Το υπόλοιπο του workflow παραμένει αμετάβλητο—αυτή είναι η ομορφιά του μοτίβου **πώς να χρησιμοποιήσετε το OcrEngine**.

### 2. Επεξεργασία PDF αντί για TIFF

```csharp
engine.Image = ImageStream.FromFile("Resources/document.pdf");
```

Οι περισσότερες βιβλιοθήκες ανιχνεύουν αυτόματα το φορμά του container, οπότε δεν χρειάζεστε επιπλέον κώδικα.

### 3. Κατάλληλη Αποδέσμευση Πόρων

Αν το `OcrEngine` υλοποιεί `IDisposable`, τυλίξτε ολόκληρο το τμήμα:

```csharp
using var engine = new OcrEngine();
engine.Language = OcrLanguage.English;
engine.Image = ImageStream.FromFile(imagePath);
var result = engine.RecognizeMultiPage();
// ...process result...
```

Αυτό εξασφαλίζει ότι οι εγγενείς χειριστές απελευθερώνονται, αποτρέποντας διαρροές μνήμης σε υπηρεσίες που τρέχουν για μεγάλο χρονικό διάστημα.

### 4. Μεγάλα Έγγραφα – Ροή Σελίδα‑με‑Σελίδα

```csharp
int totalPages = engine.GetPageCount(); // hypothetical method
for (int i = 0; i < totalPages; i++)
{
    engine.Image = ImageStream.FromFile(imagePath, pageIndex: i);
    var pageResult = engine.RecognizeSinglePage();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

Η ροή μειώνει τη μέγιστη χρήση μνήμης με μικρή επιβάρυνση στην απόδοση—επιλέξτε ό,τι ταιριάζει στο σενάριό σας.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using OcrLibrary;
using OcrLibrary.Imaging;

namespace OcrEngineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create and configure the OCR engine
            using var engine = new OcrEngine();
            engine.Language = OcrLanguage.English;

            // Load the multi‑page image (TIFF or PDF)
            string imagePath = "Resources/multipage.tif";
            engine.Image = ImageStream.FromFile(imagePath);

            // Perform batch OCR
            var multiPageResult = engine.RecognizeMultiPage();

            // Output each page's text
            for (int pageIndex = 0; pageIndex < multiPageResult.Count; pageIndex++)
            {
                Console.WriteLine($"--- Page {pageIndex + 1} ---");
                Console.WriteLine(multiPageResult[pageIndex].Text);
                Console.WriteLine();
            }
        }
    }
}
```

Αποθηκεύστε το ως `Program.cs`, τρέξτε `dotnet run` και παρακολουθήστε το κείμενο να εμφανίζεται. Αν αντικαταστήσετε τη διαδρομή αρχείου με PDF, ο ίδιος κώδικας λειτουργεί—άλλη μια νίκη για την προσέγγιση **πώς να χρησιμοποιήσετε το OcrEngine**.

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε το OcrEngine** από την αρχή μέχρι το τέλος: εγκατάσταση της βιβλιοθήκης, ρύθμιση του **OcrLanguage English**, φόρτωση πολυ‑σελίδας TIFF ή PDF, εκτέλεση `RecognizeMultiPage` και εκτύπωση του κειμένου κάθε σελίδας. Το μοτίβο είναι επαναχρησιμοποιήσιμο για άλλες γλώσσες, άλλους τύπους αρχείων και ακόμη για ροή μεγάλων εγγράφων.

Τα επόμενα βήματα που μπορείτε να εξερευνήσετε περιλαμβάνουν:

- Εφαρμογή **OCR engine C#** για δημιουργία αναζητήσιμων PDF (προσθήκη του κειμένου ως αόρατου στρώματος)
- Χρήση **multi‑page OCR** για τροφοδοσία δεδομένων σε βάση δεδομένων ή μοντέλο AI
- Πειραματισμός με προεπεξεργασία εικόνας (απλοποίηση, δυαδικοποίηση) για βελτίωση της ακρίβειας

Έχετε κάποιο ιδιαίτερο σενάριο που σας ενδιαφέρει—όπως η διαχείριση χειρόγραφων σημειώσεων ή η ενσωμάτωση

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να OCR PDF σε .NET με Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Πώς να Εξάγετε OCR – Ρύθμιση OCR](/ocr/english/net/ocr-configuration/)
- [Πώς να Εκτελέσετε OCR σε Εικόνες Αρχείου με Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}