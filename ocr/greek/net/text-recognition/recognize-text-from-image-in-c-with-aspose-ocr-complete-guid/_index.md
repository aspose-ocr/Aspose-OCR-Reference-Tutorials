---
category: general
date: 2026-06-25
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να διαβάζετε κείμενο από PNG, να φορτώνετε εικόνα για OCR και να ενεργοποιείτε
  την αυτόματη ανίχνευση γλώσσας σε ένα απλό παράδειγμα.
draft: false
keywords:
- recognize text from image
- read text from png
- load image for ocr
- aspose ocr c# example
- enable automatic language detection
language: el
og_description: Αναγνώριση κειμένου από εικόνα με Aspose OCR σε C#. Αυτός ο οδηγός
  δείχνει πώς να διαβάσετε κείμενο από PNG, να φορτώσετε εικόνα για OCR και να ενεργοποιήσετε
  την αυτόματη ανίχνευση γλώσσας.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Aspose OCR βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Recognize text from image using Aspose OCR in C#. Learn how to read
    text from PNG, load image for OCR, and enable automatic language detection in
    a simple example.
  headline: Recognize Text from Image in C# with Aspose OCR – Complete Guide
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
- OCR
title: Αναγνώριση κειμένου από εικόνα σε C# με Aspose OCR – Πλήρης οδηγός
url: /el/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα σε C# με Aspose OCR – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερες ποιο API θα διαχειριστεί εικόνες με μικτές γλώσσες χωρίς προβλήματα; Δεν είσαι μόνος. Σε πολλές πραγματικές εφαρμογές — σκεφτείτε σαρωτές αποδείξεων ή αναγνώστες πολυγλωσσικών πινακίδων — πρέπει να **διαβάσετε κείμενο από αρχεία PNG**, και θέλετε επίσης η μηχανή να εντοπίζει τη γλώσσα αυτόματα.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα σύντομο **παράδειγμα Aspose OCR C#** που φορτώνει μια εικόνα για OCR, ενεργοποιεί την αυτόματη ανίχνευση γλώσσας και, τέλος, εκτυπώνει το εξαγόμενο κείμενο. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που μπορεί να **αναγνωρίσει κείμενο από εικόνα** αρχείων με οποιονδήποτε συνδυασμό γλωσσών.

## Τι Θα Μάθετε

- Πώς να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας τη μέθοδο `OcrImage.FromFile` της Aspose.  
- Τα ακριβή βήματα για **ενεργοποίηση αυτόματης ανίχνευσης γλώσσας** ώστε να μην χρειάζεται να κωδικοποιήσετε σκληρά τις γλωσσικές enum.  
- Πώς να **διαβάσετε κείμενο από PNG** (ή οποιοδήποτε υποστηριζόμενο bitmap) και να εμφανίσετε τόσο τις ανιχνευθείσες γλώσσες όσο και το ακατέργαστο αποτέλεσμα OCR.  
- Συνηθισμένα προβλήματα όπως ελλιπείς διαδρομές αρχείων, μη υποστηριζόμενες μορφές εικόνας, και πώς να τα αντιμετωπίσετε.  

**Προαπαιτούμενα** – .NET 6 (ή νεότερο) SDK, ένα νέο έργο κονσόλας, και το πακέτο NuGet Aspose.OCR. Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

---

![Διάγραμμα που απεικονίζει τη ροή αναγνώρισης κειμένου από εικόνα με Aspose OCR σε C#](recognize-text-from-image-aspnet-ocr-diagram.png){.align-center alt="αναγνώριση κειμένου από εικόνα χρησιμοποιώντας παράδειγμα Aspose OCR C#"}

## Βήμα 1 – Αναγνώριση Κειμένου από Εικόνα με Aspose OCR

Το πρώτο που χρειάζεστε είναι μια παρουσία του `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο της λειτουργίας· κρατά όλες τις ρυθμίσεις, συμπεριλαμβανομένης της λειτουργίας γλώσσας.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class AutoDetectExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this object will do all the heavy lifting.
        var ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Η δημιουργία του κινητήρα μία φορά και η επαναχρησιμοποίησή του σε πολλαπλές εικόνες μειώνει το κόστος. Σε μεγαλύτερες υπηρεσίες συνήθως διατηρείται μια singleton παρουσία.

## Βήμα 2 – Φόρτωση Εικόνας για OCR και Ανάγνωση Κειμένου από PNG

Τώρα που υπάρχει ο κινητήρας, πρέπει να του δώσουμε κάτι για ανάγνωση. Η Aspose δέχεται διάφορες μορφές, αλλά το PNG είναι κοινή επιλογή επειδή διατηρεί την απώλεια ποιότητας.

```csharp
        // 2️⃣ Tell the engine which file to process.
        //    OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
        var image = OcrImage.FromFile("YOUR_DIRECTORY/mixed_languages.png");
```

> **Συμβουλή:** Αν δεν είστε σίγουροι για την ακριβή διαδρομή, χρησιμοποιήστε `Path.Combine(Environment.CurrentDirectory, "mixed_languages.png")`. Αποτρέπει τυχαία σφάλματα “file not found” όταν τρέχετε την εφαρμογή από διαφορετικό φάκελο εργασίας.

## Βήμα 3 – Ενεργοποίηση Αυτόματης Ανίχνευσης Γλώσσας

Οι περισσότερες βιβλιοθήκες OCR απαιτούν να καθορίσετε έναν κωδικό γλώσσας (π.χ., `Language.English`). Αυτό λειτουργεί καλά για μονόγλωσσα έγγραφα, αλλά γίνεται ενοχλητικό όταν η εικόνα περιέχει Αγγλικά **και** Γαλλικά, ή οποιονδήποτε άλλο συνδυασμό. Η Aspose λύνει αυτό με την enum `Language.AutoDetect`.

```csharp
        // 3️⃣ Switch on auto‑detect so the engine guesses the language(s) on the fly.
        ocrEngine.Settings.Language = Language.AutoDetect;
```

> **Τι συμβαίνει στο παρασκήνιο;** Ο κινητήρας εκτελεί μια γρήγορη στατιστική ανάλυση στα γλύφους, τα συγκρίνει με τα ενσωματωμένα μοντέλα γλώσσας και επιλέγει το πιο πιθανό σύνολο. Αυτό προσθέτει αμελητέο κόστος απόδοσης αλλά βελτιώνει σημαντικά την ακρίβεια για πολυγλωσσικό περιεχόμενο.

## Βήμα 4 – Εκτέλεση της Αναγνώρισης OCR

Με την εικόνα φορτωμένη και την ανίχνευση γλώσσας ενεργοποιημένη, καλούμε τελικά το `Recognize`. Η μέθοδος επιστρέφει ένα `RecognitionResult` που περιέχει τόσο το εξαγόμενο κείμενο όσο και μια λίστα με τις ανιχνευθείσες γλώσσες.

```csharp
        // 4️⃣ Run the OCR process.
        var recognitionResult = ocrEngine.Recognize(image);
```

> **Ακραία περίπτωση:** Αν η εικόνα είναι πολύ θορυβώδης, το αποτέλεσμα μπορεί να περιέχει ακατάλληλους χαρακτήρες. Σκεφτείτε προεπεξεργασία με `image.AdjustContrast` ή `image.RemoveNoise` πριν από την αναγνώριση.

## Βήμα 5 – Εμφάνιση Ανιχνευμένων Γλωσσών και Εξαγόμενου Κειμένου

Το τελευταίο βήμα είναι απλώς η εκτύπωση των αποτελεσμάτων. Σε μια πραγματική υπηρεσία πιθανότατα θα επιστρέφατε ένα JSON payload, αλλά για αυτήν την επίδειξη κονσόλας το `Console.WriteLine` κάνει τη δουλειά.

```csharp
        // 5️⃣ Show what the engine found.
        Console.WriteLine("Detected languages: " + string.Join(", ", recognitionResult.DetectedLanguages));
        Console.WriteLine("Extracted text:");
        Console.WriteLine(recognitionResult.Text);
    }
}
```

### Αναμενόμενο Αποτέλεσμα

```
Detected languages: English, French
Extracted text:
Welcome to our store!
Bienvenue dans notre magasin!
```

Αν δείτε μια κενή λίστα γλωσσών, ελέγξτε ξανά ότι η εικόνα περιέχει αναγνωρίσιμους χαρακτήρες και ότι η άδεια Aspose OCR (αν χρησιμοποιείτε πληρωμένη έκδοση) έχει εφαρμοστεί σωστά.

---

## Συχνές Ερωτήσεις & Pro Συμβουλές

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να επεξεργαστώ JPEG ή BMP αντί για PNG;** | Απολύτως. Το `OcrImage.FromFile` λειτουργεί με οποιαδήποτε μορφή υποστηρίζεται από το Aspose OCR. Απλώς αλλάξτε την επέκταση του αρχείου. |
| **Τι αν θέλω να περιορίσω την ανίχνευση σε συγκεκριμένο σύνολο γλωσσών;** | Ορίστε `ocrEngine.Settings.Language = Language.English | Language.Spanish;` χρησιμοποιώντας τον τελεστή bitwise OR. |
| **Υπάρχει τρόπος να λάβω βαθμολογίες εμπιστοσύνης;** | Ναι. Το `recognitionResult.Confidence` παρέχει ένα float μεταξύ 0 και 1 για κάθε αναγνωρισμένη γραμμή. |
| **Πώς διαχειρίζομαι μεγάλες παρτίδες;** | Επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` και τυλίξτε τον βρόχο σε `Parallel.ForEach` για παράλληλη επεξεργασία. |

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση αφού προσθέσετε το πακέτο NuGet Aspose.OCR (`dotnet add package Aspose.OCR`) και τοποθετήσετε ένα αρχείο `mixed_languages.png` στον καθορισμένο φάκελο.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

class AutoDetectExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.Settings.Language = Language.AutoDetect;

        // Step 3: Load the image that contains mixed languages
        // Replace YOUR_DIRECTORY with the actual folder path.
        var image = OcrImage.FromFile("YOUR_DIRECTORY/mixed_languages.png");

        // Step 4: Perform OCR recognition on the image
        var recognitionResult = ocrEngine.Recognize(image);

        // Step 5: Display the detected languages and extracted text
        Console.WriteLine("Detected languages: " + string.Join(", ", recognitionResult.DetectedLanguages));
        Console.WriteLine("Extracted text:");
        Console.WriteLine(recognitionResult.Text);
    }
}
```

Τρέξτε το πρόγραμμα με `dotnet run` και θα δείτε τις ανιχνευμένες γλώσσες ακολουθούμενες από το εξαγόμενο κείμενο στην κονσόλα.

---

## Συμπεράσματα – Γιατί Έχει Σημασία

Μόλις **αναγνωρίσαμε κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR, δείξαμε πώς να **διαβάσουμε κείμενο από PNG**, και παρουσιάσαμε τον πιο απλό τρόπο για **ενεργοποίηση αυτόματης ανίχνευσης γλώσσας**. Αυτές οι πέντε γραμμές κώδικα αποτελούν τη ραχοκοκαλιά κάθε πολυγλωσσικής λύσης σάρωσης — είτε χτίζετε έναν αναγνώστη αποδείξεων, έναν σαρωτή διαβατηρίων, ή ένα εργαλείο διαχείρισης εικόνων κοινωνικών δικτύων.

### Επόμενα Βήματα

- **Πειραματιστείτε με άλλες μορφές** – δοκιμάστε ένα υψηλής ανάλυσης JPEG και συγκρίνετε την ακρίβεια.  
- **Ενσωματώστε βαθμολογίες εμπιστοσύνης** – φιλτράρετε τις γραμμές χαμηλής εμπιστοσύνης πριν τις αποθηκεύσετε.  
- **Συνδυάστε με Azure Blob Storage** – φορτώστε εικόνες απευθείας από το cloud αντί για τοπικό σύστημα αρχείων.  
- **Εξερευνήστε τις προχωρημένες επιλογές του Aspose OCR** – όπως `ocrEngine.Settings.ImagePreprocessing` για μείωση θορύβου.

Αν σας ενδιαφέρει η επέκταση σε Web API, δείτε τον οδηγό μας για το “**ASP.NET Core OCR endpoint**” όπου επαναχρησιμοποιούμε τον ίδιο κινητήρα για εξυπηρέτηση HTTP αιτημάτων.  

Καλό κώδικα, και εύχομαι το επόμενο έργο σας να διαβάζει κείμενα από PNG τόσο εύκολα όσο διαβάζετε αυτόν τον οδηγό!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}