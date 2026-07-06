---
category: general
date: 2026-04-06
description: Πώς να ορίσετε την άδεια στο Aspose OCR χρησιμοποιώντας C# – μάθετε πώς
  να ενσωματώσετε πόρο, να λάβετε ενσωματωμένο πόρο και να φορτώσετε την άδεια από
  αρχείο ή ροή σε λίγα μόνο βήματα.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: el
og_description: Πώς να ορίσετε την άδεια στο Aspose OCR εξηγείται βήμα‑προς‑βήμα.
  Μάθετε πώς να ενσωματώσετε την άδεια, να την ανακτήσετε και να χρησιμοποιήσετε μια
  ροή άδειας για απρόσκοπτη ενσωμάτωση.
og_title: Πώς να ορίσετε την άδεια στο Aspose OCR – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- .NET licensing
title: Πώς να ορίσετε άδεια στο Aspose OCR – Πλήρης οδηγός C#
url: /el/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ορίσετε Άδεια στο Aspose OCR – Πλήρης Οδηγός C#

Το πώς να ορίσετε άδεια στο Aspose OCR είναι ένα συχνό εμπόδιο για τους προγραμματιστές. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για να ορίσετε την άδεια, να την ενσωματώσετε ως πόρο και να τη φορτώσετε από ροή — ώστε να ξεκινήσετε το OCR χωρίς το ενοχλητικό υδατογράφημα δοκιμαστικής λειτουργίας.

Έχετε προσπαθήσει ποτέ να εκτελέσετε μια εργασία OCR μόνο για να δείτε μια μπάρα «Έκδοση αξιολόγησης»; Αυτό είναι το σύμπτωμα μιας ελλιπούς ή λανθασμένης άδειας. Στο τέλος αυτού του οδηγού θα έχετε μια πλήρως αδειοδοτημένη παρουσία Aspose OCR, είτε διατηρείτε το αρχείο `.lic` δίπλα στα εκτελέσιμα σας είτε το κρύβετε μέσα στο assembly.

## Τι Θα Χρειαστεί

- **Aspose.OCR for .NET** (τελευταίο πακέτο NuGet τη στιγμή της συγγραφής – 23.10)
- Ένα **έγκυρο αρχείο άδειας Aspose OCR** (`Aspose.OCR.lic`)
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#
- Βασική εξοικείωση με ενσωμάτωση πόρων .NET (θα το καλύψουμε)

Δεν απαιτούνται επιπλέον βιβλιοθήκες τρίτων· όλα περιλαμβάνονται στο πακέτο Aspose.

![Εικονογράφηση για το πώς να ορίσετε άδεια](image.png "Πώς να ορίσετε άδεια")

## Βήμα 1: Εγκατάσταση του Πακέτου NuGet Aspose.OCR

Πριν γράψετε οποιονδήποτε κώδικα αδειοδότησης, βεβαιωθείτε ότι η βιβλιοθήκη είναι αναφορά:

```bash
dotnet add package Aspose.OCR
```

Ή, μέσω του διαχειριστή NuGet του Visual Studio, αναζητήστε **Aspose.OCR** και πατήστε *Install*. Αυτό θα κατεβάσει το `Aspose.OCR.dll` και τις εξαρτήσεις του.

> **Συμβουλή:** Στοχεύστε .NET 6 ή νεότερο για να απολαύσετε το πιο πρόσφατο API και καλύτερη απόδοση.

## Βήμα 2: Δημιουργία Αντικειμένου License – Ο Πυρήνας του «Πώς να Ορίσετε Άδεια»

Το Aspose χρησιμοποιεί μια απλή κλάση `License` για την εφαρμογή του εμπορικού κλειδιού. Η δημιουργία της είναι η πρώτη γραμμή κάθε αδειοδοτημένης ροής εργασίας:

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

Γιατί είναι σημαντικό: η παρουσία `License` διαβάζει το περιεχόμενο του `.lic` και το καταχωρεί παγκοσμίως για το τρέχον AppDomain. Μόλις καταχωρηθεί, κάθε `OcrEngine` που δημιουργείτε θα λειτουργεί σε πλήρη λειτουργικότητα.

## Βήμα 3: Εφαρμογή της Άδειας από Αρχείο (Κλασικό «Πώς να Φορτώσετε Άδεια»)

Αν προτιμάτε να κρατάτε το αρχείο άδειας δίπλα στο εκτελέσιμο, καλέστε το `SetLicense` με τη διαδρομή του αρχείου:

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### Πράγματα που Πρέπει να Προσέξετε

- **Απόλυτες vs. σχετικές διαδρομές:** Οι σχετικές διαδρομές λύνουν σε σχέση με το *working directory* της διεργασίας, που συχνά είναι ο φάκελος bin.
- **Δικαιώματα αρχείου:** Ο λογαριασμός που εκτελεί την εφαρμογή πρέπει να έχει πρόσβαση ανάγνωσης στο αρχείο `.lic`.
- **Διαχείριση εξαιρέσεων:** Το `SetLicense` ρίχνει `FileNotFoundException` αν η διαδρομή είναι λανθασμένη, οπότε τυλίξτε το σε `try/catch` αν χρειάζεστε ευγενική αποτυχία.

## Βήμα 4: Πώς να Ενσωματώσετε Πόρο – Αποθήκευση της Άδειας Μέσα στο Assembly

Η ενσωμάτωση της άδειας εξαλείφει την ανάγκη αποστολής ξεχωριστού αρχείου. Να πώς **πώς να ενσωματώσετε πόρο** σε ένα έργο .NET:

1. Προσθέστε το αρχείο `.lic` στο έργο σας (π.χ. σε φάκελο `Resources`).
2. Δεξί‑κλικ στο αρχείο → *Properties* → ορίστε **Build Action** σε **Embedded Resource**.
3. Κατασκευάστε το έργο· η άδεια γίνεται μέρος του μεταγλωττισμένου DLL.

Τώρα μπορείτε να το ανακτήσετε με λογική **get embedded resource**.

## Βήμα 5: Λήψη Ροής Ενσωματωμένου Πόρου

Το παρακάτω απόσπασμα δείχνει **get embedded resource** χρησιμοποιώντας reflection. Προσαρμόστε το namespace και το όνομα πόρου ώστε να ταιριάζει με τη δομή του έργου σας:

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **Γιατί reflection;** Η `Assembly.GetExecutingAssembly()` δείχνει στο τρέχον assembly, εξασφαλίζοντας ότι ο κώδικας λειτουργεί είτε σε console app, web site, είτε σε Azure Function.

## Βήμα 6: Χρήση Ροής Άδειας – Το Πρότυπο «use license stream»

Τώρα που έχετε τη ροή, **use license stream** για να εφαρμόσετε την άδεια χωρίς να αγγίξετε το σύστημα αρχείων:

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

Όταν το `SetLicense` λαμβάνει ένα `Stream`, το Aspose διαβάζει τα bytes απευθείας, καταχωρεί την άδεια και κλείνει τη ροή όταν βγείτε από το μπλοκ `using`. Αυτή είναι η πιο καθαρή μέθοδος για να κρατήσετε την άδεια κρυφή.

### Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα πάντα, εδώ είναι ένα αυτόνομο πρόγραμμα που δείχνει και τις τρεις προσεγγίσεις (αρχείο, ενσωματωμένος πόρος και ροή). Σχολιάστε τις ενότητες που δεν χρειάζεστε.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

Αν η άδεια δεν εφαρμοστεί, το Aspose ρίχνει `LicenseException` ή θα δείτε το υδατογράφημα αξιολόγησης στα αποτελέσματα OCR.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Το banner «Evaluation version» εξακολουθεί να εμφανίζεται | Η άδεια δεν φορτώθηκε ή η διαδρομή είναι λανθασμένη | Ελέγξτε ξανά τη διαδρομή του αρχείου ή το όνομα του ενσωματωμένου πόρου. |
| `NullReferenceException` στο `GetManifestResourceStream` | Λάθος όνομα πόρου ή το Build Action δεν είναι ορισμένο σε Embedded Resource | Επιβεβαιώστε το πλήρες όνομα με namespace και ορίστε σωστά το Build Action. |
| Η άδεια λειτουργεί τοπικά αλλά αποτυγχάνει μετά την ανάπτυξη | Έλλειψη δικαιωμάτων ανάγνωσης στον διακομιστή | Δώστε στο app pool identity δικαίωμα ανάγνωσης στο αρχείο `.lic`, ή ενσωματώστε την άδεια για αποφυγή προβλημάτων συστήματος αρχείων. |
| Πολλαπλά αντικείμενα `License` δεν έχουν αποτέλεσμα | Κλήσατε `SetLicense` σε *διαφορετική* παρουσία μετά την πρώτη | Διατηρήστε μία μόνο παρουσία `License` ανά AppDomain· επαναχρησιμοποιήστε την ή καλέστε `SetLicense` μία φορά κατά την εκκίνηση. |

## Πότε να Επιλέξετε Κάθε Προσέγγιση

- **Βασισμένη σε αρχείο** – Γρήγορη πρωτοτυπία, εύκολη αντικατάσταση χωρίς επανακατασκευή.
- **Ενσωματωμένος πόρος** – Ιδανική για desktop ή διανομή βιβλιοθηκών όπου δεν θέλετε την άδεια να κυκλοφορεί ελεύθερα.
- **Βασισμένη σε ροή** – Τέλεια για περιβάλλοντα cloud (Azure Functions, AWS Lambda) όπου μπορείτε να αντλήσετε την άδεια από ασφαλές vault και να τη δώσετε απευθείας.

## Επόμενα Βήματα – Εμβάθυνση στη Γνώση Αδειοδότησης

Τώρα που έχετε κατακτήσει **πώς να ορίσετε άδεια**, ίσως θέλετε να εξερευνήσετε:

- **Πώς να ενσωματώσετε πόρο** σε πιο σύνθετες λύσεις πολλαπλών έργων.
- **Get embedded resource** από satellite assemblies για σενάρια τοπικοποίησης.
- **Πώς να φορτώσετε άδεια** δυναμικά από Azure Key Vault ή AWS Secrets Manager.
- **Use license stream** μαζί με dependency injection για πιο καθαρό κώδικα εκκίνησης.

Κάθε ένα από αυτά τα θέματα βασίζεται στα θεμέλια που καλύψαμε και σας βοηθά να διατηρήσετε τη στρατηγική αδειοδότησης ασφαλή και διαχειρίσιμη.

---

### TL;DR

Σας δείξαμε **πώς να ορίσετε άδεια** στο Aspose OCR χρησιμοποιώντας τρεις αξιόπιστες τεχνικές: φόρτωση από αρχείο, ενσωμάτωση του `.lic` ως πόρο και εφαρμογή μέσω ροής. Ακολουθήστε τον κώδικα, προσέξτε τα πιθανά προβλήματα, και η μηχανή OCR σας θα τρέχει σε πλήρη λειτουργία — χωρίς υδατογράφημα δοκιμής, χωρίς εκπλήξεις.

Καλή προγραμματιστική, και να είναι τα αποτελέσματα OCR σας kristall‑clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}