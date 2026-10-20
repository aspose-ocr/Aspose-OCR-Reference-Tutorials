---
category: general
date: 2026-09-08
description: Μάθετε πώς να ελέγξετε την υποστήριξη γλώσσας OCR σε C# χρησιμοποιώντας
  το Aspose.OCR. Επαληθεύστε τα language modules, διαχειριστείτε τα missing packs,
  και διατηρήστε τη λειτουργία OCR αξιόπιστη.
draft: false
keywords:
- check OCR language
- OCR language support
- Aspose OCR C#
- verify OCR language modules
- OCR language availability
lastmod: 2026-09-08
og_description: Μάθετε πώς να ελέγξετε την υποστήριξη γλώσσας OCR σε C# χρησιμοποιώντας
  το Aspose.OCR. Επαληθεύστε τα language modules, διαχειριστείτε τα missing packs,
  και διατηρήστε τη λειτουργία OCR αξιόπιστη.
og_image_alt: Diagram of checking OCR language support in a C# console app
og_title: Έλεγχος υποστήριξης γλώσσας OCR σε C# – Οδηγός βήμα προς βήμα
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to check OCR language support in C# using Aspose.OCR. Verify
    language modules, handle missing packs, and keep your OCR feature reliable.
  headline: Check OCR language support in C# – Step‑by‑step guide
  type: TechArticle
- description: Learn how to check OCR language support in C# using Aspose.OCR. Verify
    language modules, handle missing packs, and keep your OCR feature reliable.
  name: Check OCR language support in C# – Step‑by‑step guide
  steps:
  - name: create a minimal console project
    text: A console app lets you see output instantly without UI boilerplate. Create
      a new project with `dotnet new console -n OcrLanguageCheck` and add the Aspose.OCR
      package via `dotnet add package Aspose.OCR`. This environment mirrors any other
      .NET host (ASP.NET, WinForms, Azure Functions) once you copy t
  - name: implement the language‑check helper
    text: The core of **how to check OCR language** lives in the `CheckLanguageSupport`
      method. It receives a `Language` enum and returns a boolean. The method also
      logs the result, which is useful for diagnostics.
  - name: call the helper for a specific language
    text: In `Main`, invoke `CheckLanguageSupport(Language.Japanese)`. The method
      will print “Japanese language pack is available.” or a warning if it isn’t.
      You can replace `Language.Japanese` with any enum value such as `Language.French`,
      `Language.Spanish`, or `Language.English`.
  - name: handling missing DLLs at runtime
    text: If the language pack DLL isn’t in the same folder as the executable, `IsLanguageAvailable`
      returns `false`. Ensure the DLLs are copied to the output directory. For self‑contained
      single‑file deployments, list the language DLLs as **additional files** in the
      publish profile. **Pro tip:** Add a post‑b
  - name: avoid version mismatches
    text: Aspose.OCR releases language packs in lockstep with the core library. If
      you upgrade the core NuGet package but keep an older language DLL, the version
      check will fail and the method will return `false`. Always keep the language
      DLL version identical to the core package version.
  - name: cache the result for high‑throughput services
    text: '`IsLanguageAvailable` is thread‑safe, but repeatedly creating `OcrEngine`
      instances in a high‑traffic API can add overhead. Perform the language check
      once during application startup, store the result in a static dictionary, and
      reuse it for each OCR request.'
  type: HowTo
- questions:
  - answer: No single method returns all available languages, but you can iterate
      over `Enum.GetValues(typeof(Language))` and call `IsLanguageAvailable` for each
      entry.
    question: Can I check multiple languages in one call?
  - answer: Yes. Aspose.OCR is cross‑platform; just ensure the native language DLLs
      are present for the target OS.
    question: Does the check work on Linux/macOS?
  - answer: Most language DLLs are under 10 MB. The largest, Chinese‑Traditional,
      is approximately 12 MB, which is still trivial for modern deployment pipelines.
    question: How large can a language pack be?
  - answer: The `IsLanguageAvailable` method works in evaluation mode, but a full
      license is needed for production deployments to avoid evaluation watermarks.
    question: Is a license required for the language check?
  - answer: Aspose provides a REST endpoint for language pack downloads; you can call
      it from your app, store the DLL locally, and reload the engine without restarting
      the process.
    question: Can I download missing language packs programmatically?
  type: FAQPage
tags:
- OCR
- Aspose.OCR
- C#
- .NET
title: Έλεγχος υποστήριξης γλώσσας OCR σε C# – Οδηγός βήμα προς βήμα
url: /el/net/ocr-configuration/how-to-check-ocr-language-support-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Έλεγχος υποστήριξης γλώσσας OCR σε C# – Πλήρης οδηγός

Σε πολλά πραγματικά έργα η μηχανή OCR λειτουργεί στο παρασκήνιο, μετατρέποντας σαρωμένες εικόνες σε αναζητήσιμο κείμενο. Πριν κυκλοφορήσετε μια λύση, χρειάζεστε έναν αξιόπιστο τρόπο για **να ελέγξετε τα μοντέλα γλώσσας OCR** ώστε η λειτουργία να μην αποτυγχάνει σε χρόνο εκτέλεσης. Αυτός ο οδηγός σας δείχνει, βήμα προς βήμα, πώς να ελέγξετε την υποστήριξη γλώσσας OCR σε C# με το Aspose.OCR, γιατί η επαλήθευση είναι σημαντική και πώς να αντιδράσετε όταν λείπει ένα απαιτούμενο πακέτο γλώσσας.

Θα μάθετε πώς να:

* Επαληθεύσετε ότι μια συγκεκριμένη γλώσσα (Ιαπωνικά, στο παράδειγμά μας) είναι εγκατεστημένη.
* Αντιδράσετε με χάρη όταν λείπει ένα μοντέλο γλώσσας.
* Επεκτείνετε τον έλεγχο σε οποιαδήποτε γλώσσα χρειάζεστε, καθορίζοντας αποτελεσματικά την ικανότητα **προσδιορισμού γλώσσας OCR** σε χρόνο εκτέλεσης.

Δεν απαιτείται εξωτερική τεκμηρίωση — απλώς αντιγράψτε‑και‑επικολλήστε κώδικα και μια σειρά από βέλτιστες πρακτικές.

![How to check OCR language support diagram](image.png "Diagram showing how to check OCR language support in a C# console app")
[How to check OCR language support diagram](image.png "Diagram showing how to check OCR language support in a C# console app")

## Γρήγορες απαντήσεις
Η κλάση `OcrEngine` παρέχει λειτουργικότητα OCR, και η απαρίθμηση `Language` απαριθμεί τα υποστηριζόμενα πακέτα γλώσσας.

- **Μπορώ να ελέγξω την υποστήριξη γλώσσας σε χρόνο εκτέλεσης;** Ναι, καλέστε `OcrEngine.IsLanguageAvailable` με την επιθυμητή τιμή της απαρίθμησης `Language`.  
- **Χρειάζομαι ξεχωριστό DLL για κάθε γλώσσα;** Το Aspose.OCR παρέχει τα πακέτα γλώσσας ως ξεχωριστά DLL· συμπεριλάβετε αυτά που σκοπεύετε να χρησιμοποιήσετε.  
- **Τι συμβαίνει αν λείπει ένα DLL γλώσσας;** Ο έλεγχος επιστρέφει `false`; μπορείτε να εμφανίσετε ένα φιλικό μήνυμα ή να κατεβάσετε το πακέτο.  
- **Είναι ο έλεγχος ασφαλής για νήματα;** Απόλυτα — το `IsLanguageAvailable` μπορεί να κληθεί από πολλαπλά νήματα χωρίς κλείδωμα.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET 6.0 ή νεότερη, και η βιβλιοθήκη λειτουργεί επίσης με .NET Core 3.1 και .NET Framework 4.7.2.

## Τι είναι ο έλεγχος υποστήριξης γλώσσας OCR;
**Ο έλεγχος υποστήριξης γλώσσας OCR σημαίνει την επιβεβαίωση ότι το απαιτούμενο DLL πακέτο γλώσσας είναι παρόν και συμβατό με τη βασική βιβλιοθήκη Aspose.OCR.** Όταν καλείτε το `OcrEngine.IsLanguageAvailable`, η μηχανή αναζητά το αντίστοιχο σύνολο γλώσσας στον φάκελο της εφαρμογής και επικυρώνει την αντιστοιχία έκδοσης. Εάν το DLL λείπει ή δεν ταιριάζει, η μέθοδος επιστρέφει `false`, επιτρέποντάς σας να αποφύγετε μια εξαίρεση χρόνου εκτέλεσης.

## Γιατί να επαληθεύετε τα μοντέλα γλώσσας OCR πριν την επεξεργασία εικόνων;
Η επαλήθευση των μοντέλων γλώσσας OCR αποτρέπει απρόσμενες καταρρεύσεις και βελτιώνει την εμπειρία του χρήστη. Το Aspose.OCR υποστηρίζει **πάνω από 30 πακέτα γλώσσας** — συμπεριλαμβανομένων των Ιαπωνικών, Αραβικών και Χίντι — έτσι ένα ελλιπές πακέτο μπορεί να σταματήσει την επεξεργασία για ολόκληρες περιοχές χρηστών. Με την εκτέλεση του ελέγχου εκ των προτέρων, μπορείτε:

* Εμφανίστε ένα σαφές μήνυμα σφάλματος αντί για μια μη διαχειριζόμενη εξαίρεση.  
* Προσφέρετε έναν αυτόματο σύνδεσμο λήψης για το ελλιπές πακέτο γλώσσας.  
* Επιστρέψτε σε προεπιλεγμένη γλώσσα (συχνά Αγγλικά) για να διατηρήσετε τη ροή εργασίας ενεργή.  

Περιστατικό ποσό: Το Aspose.OCR μπορεί να επεξεργαστεί **έγγραφα έως 200 σελίδων** σε μία ενιαία αίτηση διατηρώντας τη χρήση μνήμης κάτω από 150 MB, εφόσον τα κατάλληλα DLL γλώσσας είναι φορτωμένα.

## Προαπαιτούμενα
- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Core 3.1 και .NET Framework 4.7.2).  
- Το πακέτο NuGet `Aspose.OCR` εγκατεστημένο (`Aspose.OCR`).  
- Τα μοντέλα γλώσσας που σκοπεύετε να χρησιμοποιήσετε (π.χ., `Aspose.OCR.Japanese.dll`).  

Εάν λείπει κάποιο από αυτά, ο κώδικας που θα γράψουμε αργότερα θα σας ενημερώσει ακριβώς τι δεν πάει καλά.

## Πώς να ελέγξετε την υποστήριξη γλώσσας OCR σε C# βήμα προς βήμα

Φορτώστε τη μηχανή OCR μία φορά, έπειτα ζητήστε της αν μια συγκεκριμένη γλώσσα είναι διαθέσιμη. Η παρακάτω μέθοδος περιλαμβάνει τη λογική:

```csharp
// Program.cs – entry point for the demo
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // We'll call a helper method that checks the language support.
        CheckLanguageSupport(Language.Japanese);
    }

    // Helper that encapsulates the check logic.
    static void CheckLanguageSupport(Language language)
    {
        // Step 2 lives here – see the next section.
    }
}
```

**Άμεση απάντηση:** Καλέστε τη στατική μέθοδο `OcrEngine.IsLanguageAvailable` με την επιθυμητή τιμή της απαρίθμησης `Language`; επιστρέφει `true` εάν το αντίστοιχο DLL είναι παρόν και συμβατό με την έκδοση, διαφορετικά `false`. Αυτή η μία γραμμή σας δίνει μια άμεση ένδειξη διαθεσιμότητας γλώσσας χωρίς εξαιρέσεις.

### Βήμα 1: δημιουργήστε ένα ελάχιστο έργο κονσόλας
Μια εφαρμογή κονσόλας σας επιτρέπει να δείτε το αποτέλεσμα άμεσα χωρίς περιττό UI. Δημιουργήστε ένα νέο έργο με `dotnet new console -n OcrLanguageCheck` και προσθέστε το πακέτο Aspose.OCR μέσω `dotnet add package Aspose.OCR`. Αυτό το περιβάλλον αντικατοπτρίζει οποιονδήποτε άλλο κεντρικό .NET (ASP.NET, WinForms, Azure Functions) μόλις αντιγράψετε τη βοηθητική μέθοδο.

### Βήμα 2: υλοποιήστε το βοηθητικό πρόγραμμα ελέγχου γλώσσας
Ο πυρήνας του **πώς να ελέγξετε τη γλώσσα OCR** βρίσκεται στη μέθοδο `CheckLanguageSupport`. Λαμβάνει μια απαρίθμηση `Language` και επιστρέφει boolean. Η μέθοδος επίσης καταγράφει το αποτέλεσμα, κάτι που είναι χρήσιμο για διαγνωστικούς σκοπούς.

```csharp
static void CheckLanguageSupport(Language language)
{
    // Ask Aspose.OCR whether the requested language is installed.
    bool isSupported = OcrEngine.IsLanguageAvailable(language);

    // Provide clear feedback to the developer or end‑user.
    Console.WriteLine($"{language} language module installed: {isSupported}");

    // Optional: react if the module is missing.
    if (!isSupported)
    {
        Console.WriteLine("⚠️  Language pack not found. You can download it from Aspose's website:");
        Console.WriteLine("https://downloads.aspose.com/ocr/net");
        // In a real app you might throw an exception or fall back to a default language.
    }
}
```

### Βήμα 3: καλέστε το βοηθητικό πρόγραμμα για μια συγκεκριμένη γλώσσα
Στο `Main`, καλέστε `CheckLanguageSupport(Language.Japanese)`. Η μέθοδος θα εκτυπώσει “Το πακέτο γλώσσας Ιαπωνικά είναι διαθέσιμο.” ή μια προειδοποίηση αν δεν είναι. Μπορείτε να αντικαταστήσετε το `Language.Japanese` με οποιαδήποτε τιμή της απαρίθμησης όπως `Language.French`, `Language.Spanish` ή `Language.English`.

```csharp
// Example: user selects language via a UI dropdown.
Language userChoice = GetUserSelectedLanguage(); // pseudo‑method
CheckLanguageSupport(userChoice);
```

### Βήμα 4: διαχείριση ελλιπών DLL σε χρόνο εκτέλεσης
Εάν το DLL του πακέτου γλώσσας δεν βρίσκεται στον ίδιο φάκελο με το εκτελέσιμο, το `IsLanguageAvailable` επιστρέφει `false`. Βεβαιωθείτε ότι τα DLL αντιγράφονται στον φάκελο εξόδου. Για αυτόνομα deployments ενός αρχείου, καταγράψτε τα DLL γλώσσας ως **πρόσθετα αρχεία** στο προφίλ δημοσίευσης.

**Συμβουλή:** Προσθέστε ένα script PowerShell μετά τη δημιουργία που επαληθεύει την παρουσία των απαιτούμενων DLL:

```powershell
$required = @("Aspose.OCR.Japanese.dll", "Aspose.OCR.English.dll")
foreach ($dll in $required) {
    if (-Not (Test-Path "$PSScriptRoot\bin\Release\net6.0\$dll")) {
        Write-Host "Missing $dll – please add it to your project."
    }
}
```

### Βήμα 5: αποφύγετε τις ασυμφωνίες εκδόσεων
Το Aspose.OCR κυκλοφορεί τα πακέτα γλώσσας συγχρονισμένα με τη βασική βιβλιοθήκη. Εάν αναβαθμίσετε το βασικό πακέτο NuGet αλλά διατηρήσετε ένα παλιότερο DLL γλώσσας, ο έλεγχος έκδοσης θα αποτύχει και η μέθοδος θα επιστρέψει `false`. Πάντα διατηρείτε την έκδοση του DLL γλώσσας ίδια με την έκδοση του βασικού πακέτου.

### Βήμα 6: αποθηκεύστε το αποτέλεσμα στην κρυφή μνήμη για υπηρεσίες υψηλής διαμεταγωγής
Το `IsLanguageAvailable` είναι ασφαλές για νήματα, αλλά η επαναλαμβανόμενη δημιουργία αντικειμένων `OcrEngine` σε ένα API υψηλής κίνησης μπορεί να προσθέσει επιβάρυνση. Εκτελέστε τον έλεγχο γλώσσας μία φορά κατά την εκκίνηση της εφαρμογής, αποθηκεύστε το αποτέλεσμα σε ένα static dictionary και επαναχρησιμοποιήστε το για κάθε αίτημα OCR.

## Συνηθισμένα προβλήματα και λύσεις

### Ελλιπή DLL
*Σύμπτωμα*: `IsLanguageAvailable` πάντα επιστρέφει `false`.  
*Λύση*: Επαληθεύστε ότι το DLL γλώσσας (π.χ., `Aspose.OCR.Japanese.dll`) βρίσκεται στον ίδιο φάκελο με το εκτελέσιμο ή είναι καταχωρημένο ως πρόσθετο αρχείο σε μια δημοσίευση ενός αρχείου. Χρησιμοποιήστε το παραπάνω snippet PowerShell για αυτοματοποιημένο έλεγχο.

### Ασυμφωνία έκδοσης
*Σύμπτωμα*: Μετά την ενημέρωση του `Aspose.OCR` μέσω NuGet, ο έλεγχος γλώσσας αποτυγχάνει.  
*Λύση*: Εγκαταστήστε ξανά το πακέτο γλώσσας από το NuGet ή κατεβάστε την αντίστοιχη έκδοση από το portal του Aspose. Οι αριθμοί έκδοσης του βασικού πακέτου και του DLL γλώσσας πρέπει να ταιριάζουν ακριβώς.

### Εκτέλεση σε Docker
*Σύμπτωμα*: Η δημιουργία του container ολοκληρώνεται, αλλά ο έλεγχος γλώσσας αποτυγχάνει σε χρόνο εκτέλεσης.  
*Λύση*: Αντιγράψτε τα DLL γλώσσας στον κατάλογο `/app` της εικόνας Docker και ορίστε το `LD_LIBRARY_PATH` (Linux) ή βεβαιωθείτε ότι τα DLL είναι στο `PATH` (Windows). Μια multi‑stage build που δημοσιεύει ένα αυτόνομο εκτελέσιμο με τα πακέτα γλώσσας ενσωματωμένα εξαλείφει αυτό το πρόβλημα.

### Πολυνηματικά περιβάλλοντα
*Σύμπτωμα*: Σποραδικές εξαιρέσεις `LicenseException` όταν πολλαπλά αιτήματα OCR εκτελούνται παράλληλα.  
*Λύση*: Αρχικοποιήστε την άδεια μία φορά κατά την εκκίνηση, έπειτα επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine` ή δημιουργήστε μια μικρή δεξαμενή προρυθμισμένων μηχανών. Αποθηκεύστε τα αποτελέσματα διαθεσιμότητας γλώσσας στην κρυφή μνήμη για να αποφύγετε επαναλαμβανόμενους ελέγχους.

## Συχνές ερωτήσεις

**Q: Μπορώ να ελέγξω πολλές γλώσσες με μία κλήση;**  
A: Δεν υπάρχει μέθοδος που να επιστρέφει όλες τις διαθέσιμες γλώσσες, αλλά μπορείτε να επαναλάβετε πάνω από `Enum.GetValues(typeof(Language))` και να καλέσετε `IsLanguageAvailable` για κάθε στοιχείο.

**Q: Λειτουργεί ο έλεγχος σε Linux/macOS;**  
A: Ναι. Το Aspose.OCR είναι cross‑platform· απλώς βεβαιωθείτε ότι τα εγγενή DLL γλώσσας είναι παρόντα για το στόχο OS.

**Q: Πόσο μεγάλο μπορεί να είναι ένα πακέτο γλώσσας;**  
A: Τα περισσότερα DLL γλώσσας είναι κάτω από 10 MB. Το μεγαλύτερο, Chinese‑Traditional, είναι περίπου 12 MB, κάτι που παραμένει ασήμαντο για σύγχρονα pipelines ανάπτυξης.

**Q: Απαιτείται άδεια για τον έλεγχο γλώσσας;**  
A: Η μέθοδος `IsLanguageAvailable` λειτουργεί σε λειτουργία αξιολόγησης, αλλά απαιτείται πλήρης άδεια για παραγωγικές εκδόσεις ώστε να αποφεύγονται υδατογραφήματα αξιολόγησης.

**Q: Μπορώ να κατεβάσω ελλιπή πακέτα γλώσσας προγραμματιστικά;**  
A: Το Aspose παρέχει ένα REST endpoint για λήψη πακέτων γλώσσας· μπορείτε να το καλέσετε από την εφαρμογή σας, να αποθηκεύσετε το DLL τοπικά και να επαναφορτώσετε τη μηχανή χωρίς επανεκκίνηση της διαδικασίας.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **να ελέγξετε την υποστήριξη γλώσσας OCR** σε περιβάλλον C# χρησιμοποιώντας το Aspose.OCR:

* Μία στατική κλήση (`OcrEngine.IsLanguageAvailable`) σας λέει αν υπάρχει ένα πακέτο γλώσσας.  
* Τυλίξτε αυτήν την κλήση σε μια επαναχρησιμοποιήσιμη βοηθητική μέθοδο για καθαρό κώδικα.  
* Προβλέψτε ελλιπή DLL, ασυμφωνίες εκδόσεων και ζητήματα πολυνηματικότητας.  
* Επεκτείνετε το μοτίβο για **να προσδιορίσετε τη γλώσσα OCR** δυναμικά βάσει εισόδου χρήστη ή ρυθμίσεων.  

Ενσωματώνοντας αυτούς τους ελέγχους νωρίς, μπορείτε να κυκλοφορήσετε εφαρμογές με ενεργοποιημένο OCR με σιγουριά, παρέχοντας σαφή ανατροφοδότηση όταν λείπει ένα μοντέλο γλώσσας και αποφεύγοντας απρόσμενες καταρρεύσεις. Επόμενα βήματα; Δοκιμάστε να φορτώσετε μια πραγματική εικόνα, να εκτελέσετε OCR με την επαληθευμένη γλώσσα ή να δημιουργήσετε μια διεπαφή που επιτρέπει στους χρήστες να επιλέξουν την προτιμώμενη γλώσσα και να εμφανίζει μια φιλική προειδοποίηση εάν το πακέτο δεν είναι εγκατεστημένο.

Καλή προγραμματιστική, και εύχομαι το OCR σας πάντα να διαβάζει τους σωστούς χαρακτήρες!

---

**Last Updated:** 2026-09-08  
**Tested With:** Aspose.OCR 24.10 for .NET  
**Author:** Aspose  






```csharp
// FullDemo.cs – complete, runnable example
using System;
using Aspose.OCR;

class FullDemo
{
    static void Main()
    {
        // List of languages we care about.
        Language[] languagesToCheck = { Language.Japanese, Language.English, Language.French };

        foreach (var lang in languagesToCheck)
        {
            VerifyLanguage(lang);
        }

        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }

    static void VerifyLanguage(Language lang)
    {
        bool available = OcrEngine.IsLanguageAvailable(lang);
        Console.WriteLine($"{lang} language module installed: {available}");

        if (!available)
        {
            Console.WriteLine($"⚠️  {lang} pack missing. Download from:");
            Console.WriteLine("https://downloads.aspose.com/ocr/net");
        }
        else
        {
            // Optional: demonstrate a quick OCR run with the verified language.
            // (We skip actual image processing to keep the demo lightweight.)
            Console.WriteLine($"✅  Ready to run OCR with {lang}.");
        }

        Console.WriteLine(new string('-', 40));
    }
}
```

```
Japanese language module installed: True
✅  Ready to run OCR with Japanese.
----------------------------------------
English language module installed: True
✅  Ready to run OCR with English.
----------------------------------------
French language module installed: False
⚠️  French pack missing. Download from:
https://downloads.aspose.com/ocr/net
----------------------------------------

Press any key to exit...
```

## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Πώς να εφαρμόσετε άδεια στο Aspose OCR βήμα-βήμα C Guide](/ocr/net/ocr-configuration/how-to-apply-license-in-aspose-ocr-step-by-step-c-guide/)
- [Πώς να ενεργοποιήσετε GPU για Aspose OCR βήμα-βήμα Guide](/ocr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}