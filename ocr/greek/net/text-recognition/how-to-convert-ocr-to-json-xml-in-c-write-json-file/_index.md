---
category: general
date: 2026-04-01
description: Πώς να μετατρέψετε την έξοδο OCR σε JSON και XML σε C# – μάθετε πώς να
  εξάγετε κείμενο από εικόνα και να γράψετε αρχείο JSON σε C# χρησιμοποιώντας το Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: el
og_description: Πώς να μετατρέψετε τα αποτελέσματα OCR σε δομημένα αρχεία JSON και
  XML με C#. Οδηγός βήμα‑προς‑βήμα για την εξαγωγή κειμένου από εικόνα και τη δημιουργία
  αρχείου JSON με C#.
og_title: Πώς να μετατρέψετε OCR σε JSON & XML σε C# – Γράψτε αρχείο JSON
tags:
- OCR
- C#
- Aspose
title: Πώς να μετατρέψετε OCR σε JSON & XML σε C# – Γράψτε αρχείο JSON
url: /el/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Μετατρέψετε OCR σε JSON & XML σε C# – Γράψτε Αρχείο JSON

**Πώς να μετατρέψετε τα αποτελέσματα OCR** σε κάτι που μπορείτε πραγματικά να χρησιμοποιήσετε είναι ερώτηση που κάνουν πολλοί προγραμματιστές. Σε αυτόν τον οδηγό θα δείξουμε πώς να εξάγετε κείμενο από μια εικόνα, να μετατρέψετε το αποτέλεσμα OCR σε καλοδιατυπωμένα JSON και XML, και στη συνέχεια να γράψετε αυτά τα αρχεία στο δίσκο με C#.

Αν έχετε ποτέ κολλήσει σε μια ακατέργαστη συμβολοσειρά OCR και σκεφτείτε «Πρέπει να υπάρχει καλύτερος τρόπος να το αποθηκεύσω», βρίσκεστε στο σωστό μέρος. Στο τέλος θα έχετε ένα πλήρες, εκτελέσιμο πρόγραμμα που όχι μόνο **εξάγει κείμενο από αρχεία εικόνας** αλλά ξέρει επίσης πώς να **γράψει αρχείο JSON C#** και **γράψει αρχείο XML C#** χωρίς καμία δυσκολία.

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).  
- Πακέτο NuGet **Aspose.OCR** – εγκαταστήστε το με `dotnet add package Aspose.OCR`.  
- Μια εικόνα που περιέχει κείμενο (π.χ., `invoice.png`).  
- Οποιοδήποτε IDE προτιμάτε – Visual Studio, Rider ή VS Code είναι αποδεκτά.

> **Pro tip:** Κρατήστε τα αρχεία εικόνας σε έναν αφιερωμένο φάκελο (π.χ., `Resources/`) ώστε οι διαδρομές να παραμένουν τακτικές.

## Βήμα 1: Ρύθμιση του OCR Engine – Πώς να Μετατρέψετε OCR

Πρώτα, δημιουργούμε ένα αντικείμενο `OcrEngine` και του λέμε ποια γλώσσα πρέπει να αναγνωρίσει. Στις περισσότερες περιπτώσεις η Αγγλική είναι αρκετή, αλλά μπορείτε να αντικαταστήσετε το `Language.English` με οποιαδήποτε υποστηριζόμενη γλώσσα.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Γιατί είναι σημαντικό:** Η αρχικοποίηση του κινητήρα με τη σωστή γλώσσα βελτιώνει δραστικά την ακρίβεια, ειδικά για μη‑λατινικά αλφάβητα.

## Βήμα 2: Αναγνώριση Κειμένου – Εξαγωγή Κειμένου από Εικόνα

Τώρα τροφοδοτούμε την εικόνα στον κινητήρα. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο καθώς και δεδομένα θέσης.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Αν η εικόνα δεν βρεθεί, το `Recognize` ρίχνει μια `FileNotFoundException`. Για να κρατήσουμε το demo απλό, υποθέτουμε ότι η διαδρομή είναι σωστή, αλλά σε παραγωγικό περιβάλλον θα θέλατε να το τυλίξετε σε μπλοκ try‑catch.

## Βήμα 3: Μετατροπή του Αποτελέσματος σε JSON – Γράψτε Αρχείο JSON C#

Το Aspose.OCR κάνει τη σειριοποίηση παιχνιδάκι. Η μέθοδος `ToJson` δέχεται μια σημαία `indent` για να παραγάγει όμορφα μορφοποιημένο αποτέλεσμα, ιδανικό όταν θέλετε να ανοίξετε το αρχείο σε επεξεργαστή κειμένου.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Παράδειγμα Αναμενόμενου JSON

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Πώς να εξάγετε κείμενο:** Η ιδιότητα `Text` σας δίνει τη σύγχρονη συμβολοσειρά που μπορείτε να περάσετε σε άλλες υπηρεσίες (ευρετήρια αναζήτησης, βάσεις δεδομένων κ.λπ.).

## Βήμα 4: Αποθήκευση του JSON – Γράψτε Αρχείο JSON C# (Συνέχεια)

Με το JSON έτοιμο, απλώς το γράφουμε σε αρχείο χρησιμοποιώντας `File.WriteAllText`. Αυτό εξασφαλίζει κωδικοποίηση UTF‑8 από προεπιλογή.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Τώρα έχετε ένα `invoice.json` δίπλα στην εικόνα σας, έτοιμο για επεξεργασία downstream.

## Βήμα 5: Μετατροπή του Αποτελέσματος σε XML – Γράψτε Αρχείο XML C#

Αν προτιμάτε XML για παλαιότερα συστήματα, η μέθοδος `ToXml` κάνει το δύσκολο μέρος. Όπως το `ToJson`, υποστηρίζει και μορφοποίηση με όμορφο τύπωμα.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Παράδειγμα Αναμενόμενου XML

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Βήμα 6: Αποθήκευση του XML – Γράψτε Αρχείο XML C# (Συνέχεια)

Η αποθήκευση του XML είναι πανομοιότυπη με το βήμα του JSON· απλώς χρησιμοποιήστε την επέκταση `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Πλήρες Παράδειγμα Λειτουργικού Κώδικα

Συνδυάζοντας όλα τα παραπάνω, ορίστε το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή κονσόλας:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Τρέξτε το πρόγραμμα και θα βρείτε δύο νέα αρχεία—`invoice.json` και `invoice.xml`—ακριβώς εκεί που τα καθορίσατε. Ανοίξτε τα για να επαληθεύσετε ότι η δομή ταιριάζει με τα παραδείγματα παραπάνω.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η εικόνα περιέχει πολλαπλές γλώσσες;** | Δημιουργήστε ξεχωριστά αντικείμενα `OcrEngine` για κάθε γλώσσα ή χρησιμοποιήστε `Language.Multi` αν υποστηρίζεται. |
| **Μπορώ να ελέγξω τη μορφή εξόδου (π.χ., να εξαιρέσω δεδομένα περιοχής);** | Ναι. Τanto `ToJson` όσο και `ToXml` δέχονται προαιρετικές παραμέτρους για φιλτράρισμα πεδίων· δείτε την τεκμηρίωση Aspose.OCR για `ExportOptions`. |
| **Πώς να διαχειριστώ μεγάλα PDF με πολλές σελίδες;** | Επεξεργαστείτε κάθε σελίδα ξεχωριστά, συγκεντρώστε τα αποτελέσματα και μετά σειριοποιήστε μία φορά. |
| **Είναι η έξοδος ασφαλής για UTF‑8;** | Απόλυτα—το Aspose.OCR χρησιμοποιεί Unicode εσωτερικά, και το `File.WriteAllText` γράφει UTF‑8 από προεπιλογή. |
| **Τι γίνεται με την απόδοση;** | Το OCR είναι απαιτητικό σε CPU. Για εργασίες σε παρτίδες, σκεφτείτε παράλληλη εκτέλεση σε πολλούς πυρήνες ή χρήση του cloud API του Aspose. |

## Συμπέρασμα

Τώρα ξέρετε **πώς να μετατρέψετε τα αποτελέσματα OCR** σε τόσο JSON όσο και XML χρησιμοποιώντας C#. Ακολουθώντας τα παραπάνω βήματα μπορείτε να **εξάγετε κείμενο από εικόνα**, μετά να **γράψετε αρχείο JSON C#** και **γράψετε αρχείο XML C#** με λίγες μόνο γραμμές κώδικα. Η προσέγγιση αυτή είναι γρήγορη, αξιόπιστη και λειτουργεί με οποιονδήποτε τύπο εικόνας που υποστηρίζει το Aspose.OCR.

Είστε έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να τροφοδοτήσετε το

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}