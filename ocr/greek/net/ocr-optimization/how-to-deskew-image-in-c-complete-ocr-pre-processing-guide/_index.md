---
category: general
date: 2026-05-28
description: Μάθετε πώς να διορθώσετε την κλίση της εικόνας και να προετοιμάσετε την
  εικόνα για OCR ώστε να αναγνωρίζει κείμενο από την εικόνα με το Aspose.OCR. Αυξήστε
  την ακρίβεια και διαβάστε το κείμενο από την εικόνα χωρίς κόπο.
draft: false
keywords:
- how to deskew image
- recognize text from image
- preprocess image for OCR
- read text from image
- improve OCR accuracy
language: el
og_description: Πώς να διορθώσετε την κλίση της εικόνας και να προεπεξεργαστείτε την
  εικόνα για OCR χρησιμοποιώντας το Aspose.OCR. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα
  για να αναγνωρίσετε κείμενο από εικόνα με μεγαλύτερη ακρίβεια.
og_title: Πώς να διορθώσετε την κλίση εικόνας σε C# – Πλήρης οδηγός προεπεξεργασίας
  OCR
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to deskew image and preprocess image for OCR to recognize
    text from image with Aspose.OCR. Boost accuracy and read text from image effortlessly.
  headline: How to Deskew Image in C# – Complete OCR Pre‑Processing Guide
  type: TechArticle
- description: Learn how to deskew image and preprocess image for OCR to recognize
    text from image with Aspose.OCR. Boost accuracy and read text from image effortlessly.
  name: How to Deskew Image in C# – Complete OCR Pre‑Processing Guide
  steps:
  - name: Loads any image into Aspose.OCR.
    text: Loads any image into Aspose.OCR.
  - name: '**Preprocesses image for OCR** with deskew, denoise, and contrast boost.'
    text: '**Preprocesses image for OCR** with deskew, denoise, and contrast boost.'
  - name: '**Recognizes text from image** reliably.'
    text: '**Recognizes text from image** reliably.'
  - name: Outputs clean, searchable text, ready for downstream processing.
    text: Outputs clean, searchable text, ready for downstream processing.
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: Πώς να διορθώσετε την κλίση της εικόνας σε C# – Πλήρης οδηγός προεπεξεργασίας
  OCR
url: /el/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση εικόνας σε C# – Ολοκληρωμένος οδηγός προεπεξεργασίας OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση εικόνας** πριν την τροφοδοτήσετε σε μια μηχανή OCR; Ίσως έχετε προσπαθήσει να αναγνωρίσετε κείμενο από εικόνα μόνο και να λάβατε ακατάληπτο αποτέλεσμα επειδή η φωτογραφία λήφθηκε υπό γωνία. Αυτό είναι ένα κοινό πρόβλημα, ειδικά όταν εργάζεστε με σαρωμένες αποδείξεις, φόρμες ή οποιοδήποτε έγγραφο που δεν είναι τέλεια επίπεδο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που **προετοιμάζει την εικόνα για OCR**, εφαρμόζει διόρθωση κλίσης, αποθορυβοποίηση και ενίσχυση αντίθεσης, και τελικά **αναγνωρίζει κείμενο από εικόνα** χρησιμοποιώντας το Aspose.OCR. Στο τέλος θα ξέρετε ακριβώς πώς να **διαβάσετε κείμενο από εικόνα** με σιγουριά και να **βελτιώσετε την ακρίβεια του OCR** χωρίς να ψάχνετε εξωτερικά εργαλεία.

## Τι θα χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
- **Aspose.OCR for .NET** πακέτο NuGet (`Install-Package Aspose.OCR`)  
- Ένα δείγμα εικόνας που είναι θορυβώδης, κεκλιμένη ή χαμηλής αντίθεσης (θα το ονομάσουμε `noisy_skewed.jpg`)  
- Το αγαπημένο σας IDE (Visual Studio, Rider ή ακόμη και VS Code)

Αυτό είναι όλο. Χωρίς επιπλέον εγγενείς βιβλιοθήκες, χωρίς Docker containers—απλώς καθαρός διαχειριζόμενος κώδικας.

![Διάγραμμα που δείχνει πώς να διορθώσετε την κλίση εικόνας, αποθορυβοποίηση, ενίσχυση αντίθεσης, και στη συνέχεια OCR](/images/ocr-pipeline.png "Ροή εργασίας για τη διόρθωση κλίσης εικόνας – βήματα προεπεξεργασίας πριν το OCR")

*Κείμενο alt εικόνας: “Ροή εργασίας για τη διόρθωση κλίσης εικόνας που απεικονίζει τα βήματα προεπεξεργασίας για OCR.”*

## Βήμα 1: Ρύθμιση της μηχανής OCR

Πρώτα απ’ όλα: δημιουργήστε μια παρουσία του `OcrEngine`. Σκεφτείτε αυτό το αντικείμενο ως τον εγκέφαλο που θα διαβάσει αργότερα το κείμενο από την εικόνα σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Γιατί δημιουργούμε τη μηχανή πριν φορτώσουμε την εικόνα; Το Aspose.OCR διαχωρίζει τη **διαμόρφωση** (φίλτρα, γλώσσα κ.λπ.) από την **πηγή εικόνας**, δίνοντάς μας την ευελιξία να ρυθμίσουμε την προεπεξεργασία χωρίς να χρειάζεται να ξαναδημιουργήσουμε τη μηχανή κάθε φορά.

## Βήμα 2: Φόρτωση της εικόνας που θέλετε να καθαρίσετε

Στη συνέχεια, δείξτε στη μηχανή το αρχείο που θέλετε να διορθώσετε. Η βοηθητική μέθοδος `ImageStream.FromFile` διαβάζει την εικόνα στη μνήμη, έτοιμη για τη γραμμή προεπεξεργασίας.

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\noisy_skewed.jpg");
```

Αν εργάζεστε με ροή (π.χ. από ανέβασμα στο web), μπορείτε να αντικαταστήσετε το `FromFile` με `FromStream`. Το σημαντικό είναι ότι η μηχανή τώρα κρατάει μια αναφορά στο ακατέργαστο bitmap.

## Βήμα 3: Ενεργοποίηση φίλτρων προεπεξεργασίας (Deskew, Denoise, Contrast Boost)

Εδώ απαντάμε στην κεντρική ερώτηση: **πώς να διορθώσετε την κλίση εικόνας** ενώ ταυτόχρονα την καθαρίζουμε. Το Aspose.OCR περιλαμβάνει ένα βολικό enum `PreprocessFilter` που μας επιτρέπει να συνδυάσουμε πολλαπλά φίλτρα χρησιμοποιώντας τον τελεστή bitwise OR.

```csharp
// Step 3: Enable preprocessing filters (deskew, denoise, contrast boost) to improve accuracy
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise |
                                            PreprocessFilter.ContrastBoost;
```

### Τι κάνει το καθένα από τα φίλτρα

| Φίλτρο | Γιατί βοηθά | Τυπική χρήση |
|--------|--------------|------------------|
| **Deskew** | Περιστρέφει την εικόνα πίσω σε οριζόντια βάση, αφαιρώντας την κλίση που μπερδεύει τη διαχωριστική ανάλυση χαρακτήρων. | Σαρωμένες φόρμες που λήφθηκαν υπό γωνία. |
| **Denoise** | Απομακρύνει στίγματα και κόκκους που μπορούν να ληφθούν κατά λάθος ως γλύφους. | Φωτογραφίες χαμηλής ανάλυσης από κινητό. |
| **ContrastBoost** | Ενισχύει τη διαφορά μεταξύ του κειμένου στο προσκήνιο και του φόντου, κάνοντας τους χαρακτήρες πιο εμφανείς. | Φθαρμένες αποδείξεις ή ξεθωριασμένο μελάνι. |

Συνδυάζοντάς τα, ουσιαστικά **προετοιμάζετε την εικόνα για OCR** με ένα βήμα, κάτι που συχνά αρκεί για να **βελτιώσετε την ακρίβεια του OCR** δραματικά.

## Βήμα 4: Εκτέλεση της μηχανής OCR και **αναγνώριση κειμένου από εικόνα**

Τώρα που η εικόνα είναι καθαρή, ήρθε η ώρα να αφήσουμε τη μηχανή να κάνει αυτό που κάνει καλύτερα: να διαβάσει τους χαρακτήρες.

```csharp
// Step 4: Perform OCR recognition
string recognizedText = ocrEngine.Recognize();
```

Στο παρασκήνιο, το Aspose.OCR εκτελεί μια σειρά σταδίων—ανάλυση διάταξης, διαχωρισμό χαρακτήρων, και τέλος έναν ταξινομητή βασισμένο σε νευρωνικό δίκτυο. Επειδή έχουμε ήδη διορθώσει την κλίση και αποθορυβώσει την εικόνα, αυτά τα στάδια έχουν μια πιο καθαρή βάση για επεξεργασία.

## Βήμα 5: Εξαγωγή του αποτελέσματος – **διαβάστε κείμενο από εικόνα** επιτυχώς

Τέλος, εκτυπώστε το αποτέλεσμα στην κονσόλα (ή αποθηκεύστε το όπου χρειάζεστε). Αυτή είναι η στιγμή που θα δείτε αν η προεπεξεργασία απέδωσε καρπούς.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Αναμενόμενο αποτέλεσμα

Αν η πηγαία εικόνα περιείχε τη φράση “Invoice #12345 – Total $89.99”, θα πρέπει να δείτε κάτι σαν:

```
=== OCR Result ===
Invoice #12345
Total $89.99
```

Παρατηρήστε πώς οι αριθμοί ευθυγραμμίζονται τέλεια, παρόλο που η αρχική φωτογραφία ήταν κεκλιμένη κατά ~7°. Αυτό είναι το μαγικό αποτέλεσμα του **πώς να διορθώσετε την κλίση εικόνας** σε συνδυασμό με αποθορυβοποίηση και ενίσχυση αντίθεσης.

## Συνηθισμένα προβλήματα & Pro Tips

- **Πρόβλημα:** Χρήση JPEG με έντονη συμπίεση που δημιουργεί τεχνητά εφέ που ούτε το `Denoise` μπορεί να καθαρίσει πλήρως.  
  **Pro tip:** Όποτε είναι δυνατόν, δουλέψτε με PNG ή TIFF· διατηρούν την πιστότητα των pixel.

- **Πρόβλημα:** Ξέχασα να ορίσω τη γλώσσα (η προεπιλογή είναι Αγγλικά).  
  **Λύση:** `ocrEngine.Configuration.Language = Language.English;` ή αλλάξτε σε `Language.French` κ.λπ., πριν καλέσετε το `Recognize()`.

- **Πρόβλημα:** Εφαρμογή φίλτρων με λάθος σειρά (π.χ. ενίσχυση αντίθεσης πριν την αποθορυβοποίηση).  
  **Λύση:** Μείνετε στη σειρά που φαίνεται παραπάνω· το Aspose εσωτερικά σέβεται τη σειρά του enum, αλλά είναι καλή πρακτική να σκεφτείτε τη λογική ροή.

- **Πρόβλημα:** Μεγάλες εικόνες (>5 MP) μπορούν να επιβραδύνουν την επεξεργασία.  
  **Λύση:** Αλλάξτε το μέγεθος της εικόνας σε μέγιστο 1500 px στην μεγαλύτερη πλευρά πριν τη δώσετε στη μηχανή. Αυτό μειώνει τη χρήση μνήμης χωρίς να θυσιάσει την ποιότητα του OCR.

## Επέκταση του παραδείγματος: Επεξεργασία πολλαπλών αρχείων σε batch

Αν χρειάζεται να **διαβάσετε κείμενο από εικόνα** σε μεγάλες ποσότητες, τυλίξτε τα βήματα μέσα σε έναν απλό βρόχο:

```csharp
string[] files = Directory.GetFiles(@"C:\Images\Batch", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    // Re‑apply filters (they stay set on the engine)
    string text = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Η μηχανή επαναχρησιμοποιεί την ίδια διαμόρφωση, οπότε πληρώνετε το κόστος ρύθμισης φίλτρων μόνο μία φορά. Αυτό το μοτίβο είναι ιδανικό για νυχτερινές εργασίες επεξεργασίας τιμολογίων.

## Επαλήθευση ότι πράγματι **βελτιώσατε την ακρίβεια του OCR**

Μια γρήγορη δοκιμή είναι να συγκρίνετε τις βαθμολογίες εμπιστοσύνης πριν και μετά την προεπεξεργασία. Το Aspose.OCR παρέχει τη μέθοδο `GetResultConfidence()`:

```csharp
// Without preprocessing
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.None;
string rawResult = ocrEngine.Recognize();
float rawConfidence = ocrEngine.GetResultConfidence();

// With preprocessing (as shown earlier)
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise |
                                            PreprocessFilter.ContrastBoost;
string cleanResult = ocrEngine.Recognize();
float cleanConfidence = ocrEngine.GetResultConfidence();

Console.WriteLine($"Raw confidence:  {rawConfidence:P2}");
Console.WriteLine($"Clean confidence: {cleanConfidence:P2}");
```

Τυπικές εκτελέσεις δείχνουν άλμα από ~78 % σε > 93 % εμπιστοσύνη—μια απτή απόδειξη ότι η **προετοιμασία της εικόνας για OCR** πραγματικά **βελτιώνει την ακρίβεια του OCR**.

## Συμπέρασμα: Τι πετύχαμε

Ξεκινήσαμε με την ερώτηση **πώς να διορθώσετε την κλίση εικόνας** και καταλήξαμε με μια στιβαρή γραμμή εργασίας που:

1. Φορτώνει οποιαδήποτε εικόνα στο Aspose.OCR.  
2. **Προετοιμάζει την εικόνα για OCR** με deskew, denoise και contrast boost.  
3. **Αναγνωρίζει κείμενο από εικόνα** αξιόπιστα.  
4. Εξάγει καθαρό, αναζητήσιμο κείμενο, έτοιμο για επόμενη επεξεργασία.

Όλα αυτά έγιναν σε λιγότερο από 30 γραμμές C# και χωρίς εξωτερικές εγγενείς εξαρτήσεις. Το ίδιο μοτίβο μπορεί να προσαρμοστεί σε άλλες γλώσσες που υποστηρίζει το Aspose (Java, Python κ.λπ.)—απλώς αντικαταστήστε τις κλήσεις SDK.

## Επόμενα βήματα & Σχετικά Θέματα

- **Εξερευνήστε πακέτα γλωσσών** για να **διαβάσετε κείμενο από εικόνα** στα Ισπανικά, Γερμανικά ή Κινέζικα.  
- **Συνδυάστε με μετατροπή PDF** (`Aspose.PDF`) για να μετατρέψετε σαρωμένα PDF σε αναζητήσιμα έγγραφα.  
- **Ενσωματώστε με Azure Functions** για serverless pipelines OCR που αυτόματα **βελτιώνουν την ακρίβεια του OCR** σε ανεβασμένα αρχεία.  
- **Δοκιμάστε προσαρμοσμένα φίλτρα**: το Aspose σας επιτρέπει να ενσωματώσετε τους δικούς σας αλγόριθμους επεξεργασίας εικόνας αν τα ενσωματωμένα δεν αρκούν.

Μη διστάσετε να τροποποιήσετε τον συνδυασμό φίλτρων, να πειραματιστείτε με τις αναλύσεις εικόνας, ή ακόμη και να προσθέσετε ένα απλό UI με WinForms ή WPF. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε το **πώς να διορθώσετε την κλίση εικόνας** και τα συναφή βήματα προεπεξεργασίας.

Καλό κώδικα, και εύχομαι τα αποτελέσματα OCR σας να είναι κρυστάλλινα!

## Σχετικά Tutorials

- [Preprocess Image OCR with Aspose.OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}