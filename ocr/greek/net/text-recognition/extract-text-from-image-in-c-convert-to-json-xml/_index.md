---
category: general
date: 2026-04-26
description: Εξαγάγετε κείμενο από εικόνα σε C# χρησιμοποιώντας το Aspose.OCR και
  μάθετε πώς να μετατρέψετε την εικόνα σε μορφές JSON και XML σε λίγα λεπτά.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: el
og_description: Εξαγωγή κειμένου από εικόνα σε C# με το Aspose.OCR. Μάθετε βήμα‑βήμα
  πώς να μετατρέψετε το αποτέλεσμα σε JSON και XML άμεσα.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Μετατροπή σε JSON & XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Ανάκτηση κειμένου από εικόνα σε C# – Μετατροπή σε JSON & XML
url: /el/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα σε C# – Μετατροπή σε JSON & XML

Έχετε ποτέ χρειαστεί να **εξάγετε κείμενο από εικόνα** σε ένα έργο .NET αλλά να νιώσατε κολλημένοι στο “πώς θα πάρω πραγματικά τα δεδομένα έξω;” Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές—σκεφτείτε επεξεργασία τιμολογίων, σάρωση αποδείξεων ή επαλήθευση ταυτοτήτων—η λήψη των ακατέργαστων χαρακτήρων από μια εικόνα είναι το πρώτο, κρίσιμο βήμα.  

Τα καλά νέα; Με το Aspose.OCR μπορείτε να το κάνετε σε λίγες γραμμές, και στη συνέχεια άμεσα **μετατρέψτε την εικόνα σε JSON** ή **μετατρέψτε την εικόνα σε XML** για τα downstream συστήματα. Σε αυτόν τον οδηγό θα περάσουμε από τον πλήρη, έτοιμο‑για‑εκτέλεση κώδικα, θα εξηγήσουμε γιατί κάθε μέρος είναι σημαντικό, και θα σας δείξουμε μερικά κόλπα για να αποφύγετε κοινά προβλήματα.

---

## Τι Θα Χρειαστεί

- **.NET 6+** (οποιοδήποτε πρόσφατο SDK λειτουργεί· το δείγμα στοχεύει στο .NET 6)
- **Aspose.OCR for .NET** πακέτο NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Ένα αρχείο εικόνας (PNG, JPG, κ.λπ.) που περιέχει εκτυπώσιμο κείμενο· θα χρησιμοποιήσουμε το `invoice.png` ως παράδειγμα.
- Ένας επεξεργαστής κώδικα—Visual Studio, VS Code ή Rider—ό,τι προτιμάτε.

Αυτό είναι όλο. Καμία επιπλέον μηχανή OCR, καμία εξωτερική υπηρεσία, μόνο ένα πακέτο NuGet.

---

## Βήμα 1: Ρύθμιση του OCR Engine – Πώς να εξάγετε κείμενο από εικόνα

Αρχικά δημιουργούμε μια παρουσία `OcrEngine` και την κατευθύνουμε στο αρχείο εικόνας. Αυτό το βήμα είναι η βάση· χωρίς σωστά φορτωμένη εικόνα, η μηχανή δεν μπορεί να αναγνωρίσει τίποτα.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Γιατί είναι σημαντικό:**  
- `OcrEngine` περιλαμβάνει όλη την χαμηλού επιπέδου προεπεξεργασία εικόνας (δυαδικοποίηση, διόρθωση κλίσης).  
- Η φόρτωση της εικόνας μέσω `ImageStream.FromFile` εξασφαλίζει ότι η μηχανή διαβάζει τα ακριβή bytes, διατηρώντας το DPI και το βάθος χρώματος—και τα δύο μπορούν να επηρεάσουν την ακρίβεια της αναγνώρισης.  

> **Συμβουλή:** Εάν οι πηγαίες εικόνες σας βρίσκονται σε ροή (π.χ., ανεβάζονται μέσω web API), χρησιμοποιήστε `ImageStream.FromStream(yourStream)` αντί για `FromFile`.

---

## Βήμα 2: Ενημέρωση της Μηχανής για τη Γλώσσα που Αναμένεται – εξάγετε κείμενο από εικόνα με ακρίβεια

Το Aspose.OCR υποστηρίζει πολλά αλφάβητα. Η καθορισμένη σωστή γλώσσα περιορίζει το σύνολο χαρακτήρων και αυξάνει την ακρίβεια.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Γιατί:**  
Όταν ορίζετε `Language.Latin`, η μηχανή OCR αγνοεί κυριλλικούς ή ασιατικούς γλύφους, μειώνοντας τα ψευδώς θετικά. Εάν αργότερα χρειαστείτε να διαχειριστείτε έγγραφα πολλαπλών γλωσσών, μπορείτε να μεταβείτε σε `Language.Multilingual` ή να συνδυάσετε γλώσσες.

---

## Βήμα 3: Εκτέλεση της Διαδικασίας Αναγνώρισης – εξάγετε κείμενο από εικόνα με μία κλήση

Τώρα πραγματικά αναγνωρίζουμε το κείμενο. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `RecognitionResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης και ακόμη δεδομένα διάταξης.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Γιατί:**  
Η κλήση του `Recognize` μία φορά είναι αρκετή επειδή η μηχανή εσωτερικά εκτελεί προεπεξεργασία, τμηματοποίηση και ταξινόμηση χαρακτήρων. Η ιδιότητα `Text` σας δίνει μια απλή συμβολοσειρά, ιδανική για καταγραφή ή γρήγορη επικύρωση.

---

## Βήμα 4: Μετατροπή του Αποτελέσματος σε JSON – μετατρέψτε την εικόνα σε json εύκολα

Πολλές σύγχρονες υπηρεσίες προτιμούν φορτία JSON. Το Aspose.OCR παρέχει μια βολική μέθοδο `ToJson` που σειριοποιεί ολόκληρο το `RecognitionResult`, συμπεριλαμβανομένων των τιμών εμπιστοσύνης και των περιγραμμάτων.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Γιατί μπορεί να θέλετε JSON:**  
- **Διαλειτουργικότητα:** Εφαρμογές front‑end (React, Angular) μπορούν να καταναλώσουν το JSON άμεσα.  
- **Ανίχνευση σφαλμάτων:** Το JSON περιλαμβάνει εμπιστοσύνη ανά χαρακτήρα, επιτρέποντας να επισημάνετε λέξεις χαμηλής εμπιστοσύνης για χειροκίνητη ανασκόπηση.  

> **Ακραία περίπτωση:** Εάν το downstream σύστημα σας χρειάζεται μόνο το απλό κείμενο, μπορείτε να εξάγετε `recognitionResult.Text` και να το τυλίξετε σε ένα προσαρμοσμένο αντικείμενο JSON αντί για το πλήρες payload του Aspose.

---

## Βήμα 5: Μετατροπή του Αποτελέσματος σε XML – μετατρέψτε την εικόνα σε xml για παλαιά συστήματα

Κάποιες επιχειρήσεις εξακολουθούν να βασίζονται σε σχήματα XML για ανταλλαγή δεδομένων. Η μέθοδος `ToXml` αντικατοπτρίζει το `ToJson` αλλά εξάγει XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Γιατί XML:**  
- **Επικύρωση σχήματος:** Μπορείτε να ορίσετε ένα XSD που ταιριάζει στη δομή που εκδίδει το Aspose, εξασφαλίζοντας τη συμμόρφωση του συμβολαίου.  
- **Ενσωμάτωση:** Παλαιότερα ERP ή συστήματα διαχείρισης εγγράφων συχνά αναλύουν XML έτοιμα.

---

## Πλήρες Παράδειγμα Εργασίας – Κώδικας-Μία-Στάση

Παρακάτω είναι το πλήρες πρόγραμμα που συνδέει όλα τα παραπάνω. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο κονσόλας (`dotnet new console`) και τρέξτε το.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Αναμενόμενη έξοδος (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Τα αρχεία JSON και XML θα περιέχουν μια πιο πλούσια δομή, για παράδειγμα:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα είναι θολή ή περιστραμμένη;

Το Aspose.OCR αυτόματα διορθώνει την κλίση των περισσότερων εικόνων, αλλά για ακραίες περιπτώσεις μπορεί να θέλετε να προεπεξεργαστείτε με `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Η προσθήκη μιας μικρής ενίσχυσης αντίθεσης (`ImageProcessor.AdjustContrast`) μπορεί επίσης να βελτιώσει το σκορ εμπιστοσύνης.

### Μπορώ να εξάγω κείμενο από PDF;

Ναι—μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας Aspose.PDF ή μια δωρεάν βιβλιοθήκη όπως PDFium) και στη συνέχεια δώστε αυτές τις εικόνες στην ίδια ροή OCR.

### Πώς να διαχειριστώ πολλαπλές γλώσσες σε ένα έγγραφο;

Ορίστε `ocrEngine.Language = Language.Multilingual;` ή συνδυάστε συγκεκριμένες γλώσσες:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Να γνωρίζετε ότι τα ευρύτερα σύνολα γλωσσών μπορεί να

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}