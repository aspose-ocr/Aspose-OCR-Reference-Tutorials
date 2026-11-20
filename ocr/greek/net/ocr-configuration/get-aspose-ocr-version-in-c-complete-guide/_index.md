---
category: general
date: 2026-06-03
description: Αποκτήστε την έκδοση του Aspose OCR σε C# με ένα απλό απόσπασμα. Μάθετε
  πώς να ανακτήσετε την έκδοση της βιβλιοθήκης Aspose OCR χρησιμοποιώντας το OcrEngine GetVersion.
draft: false
keywords:
- get aspose ocr version
- aspose ocr library
- ocrengine getversion
- c# ocr example
- retrieve aspose version
language: el
og_description: Αποκτήστε γρήγορα την έκδοση του Aspose OCR σε C#. Αυτό το σεμινάριο
  δείχνει ακριβώς πώς να ανακτήσετε την έκδοση της βιβλιοθήκης Aspose OCR χρησιμοποιώντας
  το OcrEngine GetVersion.
og_title: Αποκτήστε την έκδοση Aspose OCR σε C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  headline: Get Aspose OCR Version in C# – Complete Guide
  type: TechArticle
- description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  name: Get Aspose OCR Version in C# – Complete Guide
  steps:
  - name: Why this matters
    text: When you install the package, the assembly version on disk may differ from
      the version reported by the library at runtime. Querying the version via code
      ensures you’re reading the exact build that the CLR loaded, which is crucial
      for debugging and for compliance audits.
  - name: Expected output
    text: 'When you run `dotnet run` inside the project folder, you should see something
      similar to:'
  - name: What if `GetVersion()` returns an empty string?
    text: That usually signals a corrupted installation or a missing native dependency.
      Re‑install the NuGet package and verify that the `Aspose.OCR.Native.dll` (or
      the appropriate platform‑specific binary) sits alongside your executable.
  - name: Does the method work on .NET Core 2.0?
    text: Yes, **Aspose OCR** supports .NET Standard 2.0 and higher, so any .NET Core
      version that implements that standard can call `OcrEngine.GetVersion()`. Just
      make sure you reference the correct runtime identifiers (`win-x64`, `linux-x64`,
      etc.) if you’re publishing a self‑contained app.
  - name: Can I retrieve the version without a license file?
    text: Absolutely. `GetVersion()` does **not** require a license; it simply reports
      the library build number. However, if you attempt to perform OCR without a valid
      license, you’ll get a runtime exception. That’s why the `try/catch` in our snippet
      is valuable—it isolates the version check from the OCR exec
  type: HowTo
tags:
- Aspose
- OCR
- C#
- .NET
title: Αποκτήστε την έκδοση Aspose OCR σε C# – Πλήρης οδηγός
url: /el/net/ocr-configuration/get-aspose-ocr-version-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόκτηση Έκδοσης Aspose OCR σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **αποκτήσετε την έκδοση Aspose OCR** από το .NET project σας; Ίσως αντιμετωπίζετε ένα πρόβλημα ασυμφωνίας, ή απλώς θέλετε να καταγράψετε την ακριβή έκδοση της βιβλιοθήκης που τρέχει στην παραγωγή. Όποιος και αν είναι ο λόγος, βρίσκεστε στο σωστό μέρος.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα μικρό, αυτόνομο πρόγραμμα C# που καλεί το `OcrEngine.GetVersion()` και εκτυπώνει το αποτέλεσμα. Στο τέλος θα γνωρίζετε όχι μόνο *πώς* να ανακτήσετε την έκδοση, αλλά και *γιατί* ο έλεγχος της έκδοσης μπορεί να σας εξοικονομήσει προβλήματα κατά την αναβάθμιση της **βιβλιοθήκης Aspose OCR**.

## Τι Θα Μάθετε

- Προσθέστε το πακέτο NuGet Aspose.OCR σε ένα έργο C#  
- Χρησιμοποιήστε τη μέθοδο `OcrEngine.GetVersion()` (το σημείο εισόδου **ocrengine getversion**)  
- Διαχειριστείτε πιθανές εξαιρέσεις και επαληθεύστε το αποτέλεσμα  
- Επεκτείνετε το απόσπασμα για πραγματικές περιπτώσεις όπως καταγραφή ή συνθήκες ενεργοποίησης λειτουργιών  

Δεν απαιτείται προηγούμενη εμπειρία με OCR — απλώς μια βασική κατανόηση του C# και του Visual Studio (ή του αγαπημένου σας IDE). Ας ξεκινήσουμε.

---

## Βήμα 1: Ρύθμιση του Έργου και Ενσωμάτωση της Βιβλιοθήκης Aspose OCR

Πριν μπορέσετε να καλέσετε οποιαδήποτε API σχετικό με OCR, χρειάζεται η **βιβλιοθήκη Aspose OCR** να αναφέρεται στο έργο σας.

1. Ανοίξτε ένα τερματικό ή το Package Manager Console στο Visual Studio.  
2. Εκτελέστε την παρακάτω εντολή για να εγκαταστήσετε την πιο πρόσφατη σταθερή έκδοση:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Εάν στοχεύετε στο .NET Framework αντί για .NET Core, χρησιμοποιήστε το UI του NuGet Package Manager και επιλέξτε την έκδοση που ταιριάζει στο runtime σας. Το πακέτο περιλαμβάνει την κλάση `OcrEngine` που θα χρησιμοποιήσουμε αργότερα.

### Γιατί είναι σημαντικό

Όταν εγκαθιστάτε το πακέτο, η έκδοση του assembly στο δίσκο μπορεί να διαφέρει από την έκδοση που αναφέρει η βιβλιοθήκη κατά την εκτέλεση. Η ανάκτηση της έκδοσης μέσω κώδικα εξασφαλίζει ότι διαβάζετε την ακριβή κατασκευή που φόρτωσε το CLR, κάτι που είναι κρίσιμο για τον εντοπισμό σφαλμάτων και για ελέγχους συμμόρφωσης.

---

## Βήμα 2: Γράψτε τον Ελάχιστο Κώδικα για **Απόκτηση Έκδοσης Aspose OCR**

Δημιουργήστε μια νέα εφαρμογή κονσόλας (`dotnet new console -n OcrVersionDemo`) και αντικαταστήστε το προεπιλεγμένο `Program.cs` με το παρακάτω:

```csharp
using System;
using Aspose.OCR;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 2a: Retrieve the Aspose OCR library version.
                // This is the core of the get aspose ocr version operation.
                string version = OcrEngine.GetVersion();   // e.g., "24.5.7"

                // Step 2b: Display the version information to the console.
                Console.WriteLine($"Aspose OCR version: {version}");
            }
            catch (Exception ex)
            {
                // If something goes wrong (missing DLL, license issue, etc.)
                Console.Error.WriteLine($"Failed to get Aspose OCR version: {ex.Message}");
            }
        }
    }
}
```

**Επεξήγηση κάθε μέρους**

- `using Aspose.OCR;` φέρνει το namespace OCR στο πεδίο ορατότητας, επιτρέποντάς μας να καλέσουμε το `OcrEngine`.  
- `OcrEngine.GetVersion()` είναι η στατική μέθοδος **ocrengine getversion** που επιστρέφει μια συμβολοσειρά όπως `"24.5.7"`.  
- Η περιτύλιξη της κλήσης σε μπλοκ `try/catch` σας προστατεύει από απρόσμενα σφάλματα εκτέλεσης — ίσως τα εγγενή δυαδικά αρχεία να μην βρεθούν στο στόχο.  
- Η διασυνδεδεμένη συμβολοσειρά `$"Aspose OCR version: {version}"` εκτυπώνει μια σαφή, ανθρώπινα αναγνώσιμη γραμμή.

### Αναμενόμενη έξοδος

Όταν εκτελέσετε `dotnet run` μέσα στο φάκελο του έργου, θα πρέπει να δείτε κάτι παρόμοιο με:

```
Aspose OCR version: 24.5.7
```

Εάν η βιβλιοθήκη δεν μπορεί να φορτωθεί, το κλαδί σφάλματος θα εμφανίσει ένα συνοπτικό μήνυμα, βοηθώντας σας να εντοπίσετε το πρόβλημα γρήγορα.

---

## Βήμα 3: Επαλήθευση ότι η Έκδοση Συμφωνεί με το Πακέτο NuGet σας

Είναι εύκολο να υποθέσετε ότι η έκδοση NuGet που εγκαταστήσατε είναι αυτή που χρησιμοποιείται κατά την εκτέλεση, αλλά ιδιαιτερότητες του περιβάλλοντος μπορούν να επηρεάσουν. Για διπλό έλεγχο:

```csharp
// After retrieving the version, compare it to the package metadata.
var assembly = typeof(OcrEngine).Assembly;
var fileVersion = System.Diagnostics.FileVersionInfo.GetVersionInfo(assembly.Location).FileVersion;

Console.WriteLine($"Assembly file version: {fileVersion}");
```

Η εκτέλεση αυτού του επιπλέον αποσπάσματος θα εκτυπώσει κάτι όπως:

```
Assembly file version: 24.5.7.0
```

Εάν οι δύο τιμές διαφέρουν, μπορεί να φορτώνετε ένα παλιότερο DLL από το Global Assembly Cache (GAC) ή από έναν προηγούμενο φάκελο κατασκευής. Σε αυτήν την περίπτωση, καθαρίστε τη λύση σας (`dotnet clean`) και ξαναχτίστε.

---

## Βήμα 4: Ενσωμάτωση του Ελέγχου Έκδοσης στην Καταγραφή Παραγωγής

Οι περισσότερες πραγματικές εφαρμογές δεν εκτυπώνουν μόνο στην κονσόλα· γράφουν σε αρχείο καταγραφής ή σύστημα τηλεμετρίας. Εδώ είναι ένα γρήγορο παράδειγμα χρησιμοποιώντας το `Microsoft.Extensions.Logging`:

```csharp
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

// Set up a minimal logger.
var serviceProvider = new ServiceCollection()
    .AddLogging(builder => builder.AddConsole())
    .BuildServiceProvider();

var logger = serviceProvider.GetService<ILogger<Program>>();

try
{
    string version = OcrEngine.GetVersion();
    logger.LogInformation("Aspose OCR version: {Version}", version);
}
catch (Exception ex)
{
    logger.LogError(ex, "Unable to retrieve Aspose OCR version");
}
```

Τώρα η έκδοση εμφανίζεται στα δομημένα logs σας, καθιστώντας εύκολο το φιλτράρισμα με `{Version}` αργότερα. Αυτό το μοτίβο είναι ιδιαίτερα χρήσιμο όταν έχετε πολλαπλές μικρο‑υπηρεσίες που ενδέχεται να φορτώνουν διαφορετικό OCR DLL.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το `GetVersion()` επιστρέψει κενή συμβολοσειρά;

Αυτό συνήθως υποδηλώνει κατεστραμμένη εγκατάσταση ή έλλειψη εγγενούς εξάρτησης. Επανεγκαταστήστε το πακέτο NuGet και βεβαιωθείτε ότι το `Aspose.OCR.Native.dll` (ή το αντίστοιχο δυαδικό για την πλατφόρμα) βρίσκεται δίπλα στο εκτελέσιμο σας.

### Λειτουργεί η μέθοδος σε .NET Core 2.0;

Ναι, το **Aspose OCR** υποστηρίζει .NET Standard 2.0 και νεότερο, έτσι οποιαδήποτε έκδοση .NET Core που υλοποιεί αυτό το πρότυπο μπορεί να καλέσει το `OcrEngine.GetVersion()`. Απλώς βεβαιωθείτε ότι αναφέρετε τα σωστά αναγνωριστικά runtime (`win-x64`, `linux-x64`, κλπ.) εάν δημοσιεύετε μια αυτόνομη εφαρμογή.

### Μπορώ να ανακτήσω την έκδοση χωρίς αρχείο άδειας;

Απολύτως. Το `GetVersion()` **δεν** απαιτεί άδεια· απλώς αναφέρει τον αριθμό κατασκευής της βιβλιοθήκης. Ωστόσο, εάν προσπαθήσετε να εκτελέσετε OCR χωρίς έγκυρη άδεια, θα λάβετε μια εξαίρεση χρόνου εκτέλεσης. Γι' αυτό το `try/catch` στο απόσπασμά μας είναι χρήσιμο—απομονώνει τον έλεγχο έκδοσης από τη ροή εκτέλεσης OCR.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο να τοποθετηθεί σε ένα νέο έργο κονσόλας. Περιλαμβάνει το προαιρετικό μπλοκ καταγραφής, ώστε να δείτε τόσο την έξοδο κονσόλας όσο και τα δομημένα logs σε δράση.

```csharp
using System;
using Aspose.OCR;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            // Set up a simple console logger.
            var services = new ServiceCollection()
                .AddLogging(builder => builder.AddConsole())
                .BuildServiceProvider();

            var logger = services.GetService<ILogger<Program>>();

            try
            {
                // Retrieve the Aspose OCR library version.
                string version = OcrEngine.GetVersion();   // get aspose ocr version

                // Log and display the version.
                logger.LogInformation("Aspose OCR version: {Version}", version);
                Console.WriteLine($"Aspose OCR version: {version}");

                // Extra verification – compare with assembly file version.
                var assembly = typeof(OcrEngine).Assembly;
                var fileVersion = System.Diagnostics.FileVersionInfo
                    .GetVersionInfo(assembly.Location).FileVersion;
                logger.LogDebug("Assembly file version: {FileVersion}", fileVersion);
                Console.WriteLine($"Assembly file version: {fileVersion}");
            }
            catch (Exception ex)
            {
                logger.LogError(ex, "Failed to get Aspose OCR version");
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

Τρέξτε το με `dotnet run` και θα δείτε δύο γραμμές που επιβεβαιώνουν την έκδοση, καθώς και μια γραμμή εντοπισμού σφαλμάτων εάν ενεργοποιήσετε το `LogLevel.Debug`.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **αποκτήσετε την έκδοση Aspose OCR** σε περιβάλλον C# — από την εγκατάσταση της **βιβλιοθήκης Aspose OCR**, την κλήση της μεθόδου **ocrengine getversion**, τη διαχείριση σφαλμάτων, έως την ενσωμάτωση του αποτελέσματος σε καταγραφή επιπέδου παραγωγής. Εξοπλισμένοι με αυτή τη γνώση, μπορείτε πλέον να επαληθεύετε αξιόπιστα την ακριβή έκδοση OCR που χρησιμοποιεί η εφαρμογή σας, να αποφεύγετε σφάλματα σχετιζόμενα με εκδόσεις και να ικανοποιείτε απαιτήσεις συμμόρφωσης χωρίς κόπο.

Επόμενα βήματα; Δοκιμάστε να συνδυάσετε αυτόν τον έλεγχο έκδοσης με μια πραγματική κλήση OCR (`OcrEngine` → `RecognizeImage`) και καταγράψτε τόσο την έκδοση όσο και το αποτέλεσμα αναγνώρισης. Μπορείτε επίσης να εξερευνήσετε το μοτίβο **retrieve aspose version** για άλλα προϊόντα Aspose (PDF, Slides, Cells) ώστε να διατηρείτε ολόκληρη τη σουίτα σας συγχρονισμένη.

Καλό κώδικα, και εύχομαι οι OCR αγωγοί σας να παραμείνουν οξυοδόντες!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Get OCR Results with Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}