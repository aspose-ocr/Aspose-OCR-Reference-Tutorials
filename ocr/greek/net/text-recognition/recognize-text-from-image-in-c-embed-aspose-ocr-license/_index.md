---
category: general
date: 2026-02-28
description: Αναγνωρίστε κείμενο από εικόνα με το Aspose OCR σε C#. Μάθετε πώς να
  ενσωματώσετε την άδεια και να εξάγετε κείμενο χρησιμοποιώντας OCR σε λίγα εύκολα
  βήματα.
draft: false
keywords:
- recognize text from image
- extract text using OCR
- how to embed license
language: el
og_description: Αναγνωρίστε κείμενο από εικόνα με Aspose OCR. Αυτό το σεμινάριο δείχνει
  πώς να ενσωματώσετε την άδεια και να εξάγετε κείμενο χρησιμοποιώντας OCR σε C#.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – πλήρης οδηγός αδειοδότησης
tags:
- Aspose OCR
- C#
- Licensing
title: Αναγνώριση κειμένου από εικόνα σε C# – ενσωμάτωση άδειας Aspose OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-embed-aspose-ocr-license/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αναγνώριση κειμένου από εικόνα σε C# – ενσωμάτωση άδειας Aspose OCR

Έχετε χρειαστεί ποτέ να **αναγνωρίσετε κείμενο από εικόνα** σε μια εφαρμογή C#; Η αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR είναι παιχνιδάκι μόλις ενσωματώσετε σωστά την άδεια. Σε αυτόν τον οδηγό θα σας δείξουμε επίσης πώς να **εξάγετε κείμενο χρησιμοποιώντας OCR** και θα απαντήσουμε στην επίμονη ερώτηση **πώς να ενσωματώσετε την άδεια** χωρίς να αγγίξετε το σύστημα αρχείων.

Αν έχετε ποτέ κοίταξει μια κενή κλάση `LicenseDemo` και αναρωτηθείτε γιατί η μηχανή OCR συνεχίζει να ρίχνει σφάλματα “Trial version”, δεν είστε μόνοι. Θα περάσουμε γραμμή-γραμμή, θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό και θα ολοκληρώσουμε με ένα εκτελέσιμο παράδειγμα που εκτυπώνει το εξαγόμενο κείμενο στην κονσόλα. Χωρίς εξωτερική τεκμηρίωση, χωρίς εικασίες—απλώς καθαρός κώδικας έτοιμος για αντιγραφή‑επικόλληση.

---

## Τι θα χρειαστείτε πριν ξεκινήσουμε

- **.NET 6** (ή οποιαδήποτε νεότερη έκδοση .NET) – η επιφάνεια του API δεν έχει αλλάξει από το 2023, οπότε είστε ασφαλείς.
- **Aspose.OCR for .NET** πακέτο NuGet – εγκαταστήστε το μέσω `dotnet add package Aspose.OCR`.
- Το **αρχείο άδειας Aspose OCR** (`*.lic`). Θα το ενσωματώσουμε ως πόρο ώστε να μην χρειάζεται ποτέ να αποστέλλετε ξεχωριστό αρχείο.
- Ένα δείγμα εικόνας (`sample.png`) τοποθετημένο στη ρίζα του έργου ή σε οποιονδήποτε φάκελο θέλετε.

Αυτό είναι όλο. Χωρίς επιπλέον ρυθμίσεις, χωρίς βαριές μηχανές OCR, μόνο μερικές γραμμές C#.

---

## Βήμα 1 – Ενσωμάτωση της άδειας Aspose OCR (**πώς να ενσωματώσετε την άδεια**)

Η ενσωμάτωση της άδειας μέσα στο assembly εγγυάται ότι η άδεια μεταφέρεται μαζί με το DLL σας, εξαλείφοντας σφάλματα σχετιζόμενα με διαδρομές σε διαφορετικούς υπολογιστές.

```csharp
using System;
using System.IO;
using System.Reflection;
using Aspose.OCR;

namespace OcrDemo
{
    public static class LicenseHelper
    {
        /// <summary>
        /// Loads the embedded Aspose OCR license.
        /// The license file must be added to the project as an Embedded Resource
        /// with the exact name "OcrDemo.Resources.AspectsOCR.lic".
        /// </summary>
        public static void ApplyLicense()
        {
            // Get the assembly that contains the embedded resource
            Assembly assembly = Assembly.GetExecutingAssembly();

            // Open the stream to the embedded .lic file
            using Stream? licenseStream = assembly.GetManifestResourceStream(
                "OcrDemo.Resources.AspectsOCR.lic");

            if (licenseStream == null)
            {
                throw new FileNotFoundException(
                    "Embedded license not found. Verify the resource name and Build Action.");
            }

            // Apply the license – after this the OCR engine works in full mode
            License license = new License();
            license.SetLicense(licenseStream);
        }
    }
}
```

**Γιατί να ενσωματώσετε;**  
Όταν διανέμετε μια επιφάνεια εργασίας ή web εφαρμογή, ο τρέχων φάκελος μπορεί να διαφέρει δραματικά (π.χ. `bin\Debug` vs. ένας φάκελος δημοσίευσης). Η σκληρή κωδικοποίηση μιας διαδρομής (`C:\Licenses\my.lic`) δημιουργεί ευαίσθητη εξάρτηση. Ένας ενσωματωμένος πόρος ζει μέσα στο DLL, έτσι το runtime το βρίσκει πάντα.

**Συμβουλή:** Στο Visual Studio, κάντε δεξί‑κλικ στο αρχείο `.lic` → *Properties* → ορίστε **Build Action** σε **Embedded Resource**. Το όνομα του πόρου συνήθως ακολουθεί το μοτίβο `Namespace.Folder.FileName`. Αν μετονομάσετε το φάκελο, προσαρμόστε το string αναλόγως.

---

## Βήμα 2 – Αρχικοποίηση της μηχανής OCR για **αναγνώριση κειμένου από εικόνα**

Τώρα που η άδεια είναι ενεργή, η δημιουργία μιας στιγμής `OcrEngine` σας παρέχει πλήρεις δυνατότητες OCR.

```csharp
using Aspose.OCR;

namespace OcrDemo
{
    public class OcrProcessor
    {
        private readonly OcrEngine _engine;

        public OcrProcessor()
        {
            // The license must be applied before any OCR operation
            LicenseHelper.ApplyLicense();

            // Create a fully‑licensed engine
            _engine = new OcrEngine();
        }

        // Expose the engine for later calls
        public OcrEngine Engine => _engine;
    }
}
```

Παρατηρήστε ότι καλούμε το `LicenseHelper.ApplyLicense()` **μέσα στον constructor**. Αυτό εγγυάται ότι οποιοσδήποτε καταναλωτής του `OcrProcessor` δεν μπορεί να ξεχάσει να ενεργοποιήσει την άδεια της μηχανής—ένας εύκολος τρόπος να αποφύγετε την ανεπιθύμητη εξαίρεση “Trial mode”.

---

## Βήμα 3 – Φόρτωση εικόνας και **εξαγωγή κειμένου χρησιμοποιώντας OCR**

Με μια μηχανή με άδεια έτοιμη, η τροφοδότηση της με μια εικόνα είναι απλή. Παρακάτω φορτώνουμε ένα PNG, εκτελούμε την αναγνώριση και εκτυπώνουμε το αποτέλεσμα.

```csharp
using System;
using System.Drawing;          // Requires System.Drawing.Common on non‑Windows
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare the processor (license applied automatically)
            OcrProcessor processor = new OcrProcessor();

            // 2️⃣ Load the image – adjust the path as needed
            string imagePath = Path.Combine(AppContext.BaseDirectory, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }

            using Image image = Image.FromFile(imagePath);
            processor.Engine.SetImage(image);

            // 3️⃣ Perform recognition
            string extractedText = processor.Engine.Recognize();

            // 4️⃣ Output the result
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(extractedText);
        }
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `sample.png` περιέχει τη λέξη “Hello World”):

```
=== OCR Result ===
Hello World
```

Αν η εικόνα είναι θορυβώδης, μπορεί να εμφανιστούν επιπλέον αλλαγές γραμμής ή λανθασμένα αναγνωρισμένοι χαρακτήρες. Εκεί έρχεται το επόμενο βήμα—η ρύθμιση της μηχανής.

---

## Βήμα 4 – Λεπτομερής ρύθμιση της μηχανής (προαιρετικό) – καλύτερα αποτελέσματα κατά την **εξαγωγή κειμένου χρησιμοποιώντας OCR**

Το Aspose OCR προσφέρει μια σειρά από ιδιότητες που μπορείτε να ρυθμίσετε:

| Ιδιότητα | Τι κάνει | Τυπική χρήση |
|----------|----------|--------------|
| `Engine.Language` | Ορίζει το μοντέλο γλώσσας (π.χ., `Language.English`). | Βελτιώνει την ακρίβεια για μη λατινικά αλφάβητα. |
| `Engine.ImagePreprocess` | Ενεργοποιεί τη δυαδικοποίηση, την ευθυγράμμιση κ.λπ. | Καθαρίζει σαρώσεις χαμηλής αντίθεσης. |
| `Engine.IsAutoRotate` | Ανιχνεύει αυτόματα την προσανατολισμό της εικόνας. | Διαχειρίζεται περιστρεφμένες φωτογραφίες. |

Παράδειγμα ενεργοποίησης μερικών βοηθητικών λειτουργιών:

```csharp
processor.Engine.Language = Language.English;
processor.Engine.ImagePreprocess = ImagePreprocess.Binarization | ImagePreprocess.Deskew;
processor.Engine.IsAutoRotate = true;
```

**Γιατί να ασχοληθείτε;** Η προεπιλεγμένη μηχανή λειτουργεί καλά για καθαρές στιγμιότυπες, αλλά τα πραγματικά έγγραφα συχνά υποφέρουν από σκιές, περιστροφή ή μικτές γλώσσες. Η ρύθμιση αυτών των σημαιών μπορεί να αυξήσει το ποσοστό εμπιστοσύνης από ~70 % σε >95 % σε πολλές περιπτώσεις.

---

## Βήμα 5 – Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

1. **Λείπει το όνομα του πόρου** – Αν λάβετε `FileNotFoundException`, ελέγξτε ξανά το πλήρως προσδιορισμένο string του πόρου. Χρησιμοποιήστε `assembly.GetManifestResourceNames()` για να εμφανίσετε όλα τα ενσωματωμένα ονόματα κατά το χρόνο εκτέλεσης.
2. **Λάθος μορφή εικόνας** – `Image.FromFile` υποστηρίζει BMP, PNG, JPEG, GIF, TIFF. Για PDF ή πολυ-σελίδες TIFF θα χρειαστείτε υπερφορτώσεις `ImageStream`.
3. **Εκτέλεση σε Linux/macOS** – `System.Drawing.Common` εξαρτάται από εγγενείς βιβλιοθήκες (`libgdiplus`). Εγκαταστήστε τις μέσω `apt-get install libgdiplus` ή μεταβείτε στο `Aspose.OCR.ImageStream` που είναι ανεξάρτητο από την πλατφόρμα.
4. **Η άδεια δεν εφαρμόστηκε έγκαιρα** – Η άδεια πρέπει να οριστεί **πριν** από οποιαδήποτε κατασκευή `OcrEngine`. Η τοποθέτηση του `LicenseHelper.ApplyLicense()` σε static constructor ή στο `Main` πριν από οποιοδήποτε `new OcrEngine()` είναι η πιο ασφαλής επιλογή.

---

## Βήμα 6 – Επαλήθευση ότι η πλήρης λύση λειτουργεί

Συγκεντρώστε και εκτελέστε το πρόγραμμα:

```bash
dotnet build
dotnet run --project OcrDemo
```

Θα πρέπει να δείτε την έξοδο της κονσόλας με το εξαγόμενο κείμενο. Αν η έξοδος εξακολουθεί να λέει “Trial version”, επανεξετάστε το **Βήμα 1**—η πιο συνηθισμένη αιτία είναι ένας εσφαλμένα ενσωματωμένος πόρος.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αναγνωρίζετε κείμενο από εικόνα** σε C# χρησιμοποιώντας Aspose OCR, πώς να **ενσωματώνετε την άδεια** ώστε η μηχανή να λειτουργεί σε πλήρη λειτουργία, και τις βέλτιστες πρακτικές για **εξαγωγή κειμένου χρησιμοποιώντας OCR** αξιόπιστα. Ο πλήρης, έτοιμος για αντιγραφή‑επικόλληση κώδικας παραπάνω καλύπτει τα πάντα, από την άδεια μέχρι την προεπεξεργασία εικόνας, ώστε να τον ενσωματώσετε σε οποιοδήποτε έργο .NET και να αρχίσετε αμέσως να εξάγετε κείμενο από εικόνες.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε τη μηχανή με μια δέσμη αρχείων, πειραματιστείτε με πακέτα γλωσσών, ή διοχετεύστε την έξοδο OCR σε ευρετήριο αναζήτησης. Το ίδιο μοτίβο—ενσωμάτωση‑άδειας → αρχικοποίηση μηχανής → φόρτωση εικόνας → αναγνώριση—λειτουργεί για PDF, πολυ‑σελίδες TIFF και ακόμη και ζωντανές ροές κάμερας.

Έχετε ερωτήσεις για ειδικές περιπτώσεις ή χρειάζεστε βοήθεια στην αποσφαλμάτωση μιας δύσκολης εικόνας; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}