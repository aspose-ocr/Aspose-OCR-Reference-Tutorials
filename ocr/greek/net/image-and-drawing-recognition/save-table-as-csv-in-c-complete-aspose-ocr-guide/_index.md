---
category: general
date: 2026-03-02
description: Αποθηκεύστε τον πίνακα ως CSV χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε πίνακα από εικόνα, πώς να εξάγετε δεδομένα πίνακα και πώς να μετατρέψετε
  τον πίνακα σε CSV σε λίγα λεπτά.
draft: false
keywords:
- save table as csv
- how to extract table
- ocr table extraction
- convert table to csv
- image table to csv
language: el
og_description: Αποθηκεύστε τον πίνακα ως CSV με το Aspose OCR. Αυτό το βήμα‑βήμα
  tutorial δείχνει πώς να εξάγετε έναν πίνακα από μια εικόνα και να τον μετατρέψετε
  σε CSV χωρίς κόπο.
og_title: Αποθήκευση Πίνακα ως CSV σε C# – Πλήρης Οδηγός Aspose OCR
tags:
- OCR
- C#
- CSV
- Aspose
title: Αποθήκευση πίνακα ως CSV σε C# – Πλήρης οδηγός Aspose OCR
url: /el/net/image-and-drawing-recognition/save-table-as-csv-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Πίνακα ως CSV σε C# – Πλήρης Οδηγός Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **αποθηκεύσετε πίνακα ως CSV** όταν το μόνο που έχετε είναι μια σαρωμένη απόδειξη ή ένα στιγμιότυπο οθόνης ενός υπολογιστικού φύλλου; Δεν είστε οι μόνοι. Σε πολλά πραγματικά έργα τα δεδομένα προέρχονται από εικόνες, και η εξαγωγή τους σε μορφή που μπορεί να διαβαστεί από μηχανή μοιάζει με τράβηγμα δοντιών.  

Τα καλά νέα; Με το Aspose.OCR μπορείτε να **εξάγετε τον πίνακα**, να τον μετατρέψετε σε `DataTable` και στη συνέχεια **να μετατρέψετε τον πίνακα σε CSV** με λίγες μόνο γραμμές κώδικα. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, θα απαντήσουμε σε ερωτήσεις *πώς να εξάγετε πίνακα* και θα σας δείξουμε ένα έτοιμο‑για‑εκτέλεση παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Κερδίσετε

- Μια σαφή εικόνα της **ocr table extraction** χρησιμοποιώντας Aspose.OCR.  
- Ένα πλήρες, εκτελέσιμο απόσπασμα C# που φορτώνει μια εικόνα, εξάγει τον πίνακα και γράφει ένα αρχείο CSV.  
- Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως κενά κελιά, σαρώσεις πολλαπλών σελίδων και διαφορετικούς διαχωριστές.  
- Ιδέες για τα επόμενα βήματα, όπως η εισαγωγή του CSV σε βάση δεδομένων ή η χρήση του σε μηχανή αναφορών.

### Προαπαιτούμενα (Ναι, χρειάζεστε μερικά πράγματα)

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| .NET 6.0 ή νεότερο | Σύγχρονα χαρακτηριστικά γλώσσας και καλύτερη απόδοση |
| Πακέτο NuGet Aspose.OCR (`Aspose.OCR`) | Παρέχει `OcrEngine` και ανίχνευση πινάκων |
| Ένα αρχείο εικόνας που περιέχει καθαρό πίνακα (PNG, JPG, κ.λπ.) | Η πηγή των δεδομένων που θα εξάγουμε |
| Βασικές γνώσεις C# | Για να προσαρμόσετε το παράδειγμα στη δική σας περίπτωση |

Αν κάποιο από τα παραπάνω σας είναι άγνωστο, απλώς κατεβάστε το τελευταίο .NET SDK από τη Microsoft και εγκαταστήστε το πακέτο NuGet με `dotnet add package Aspose.OCR`. Δεν απαιτούνται άλλες εξωτερικές βιβλιοθήκες.

![Διάγραμμα που δείχνει πώς να αποθηκεύσετε έναν πίνακα ως csv χρησιμοποιώντας Aspose OCR](image-placeholder.png "διάγραμμα αποθήκευσης πίνακα ως csv")

## Βήμα 1: Φόρτωση της Εικόνας που Περιέχει τον Πίνακα

Πρώτα απ' όλα—χρειαζόμαστε ένα `Bitmap` που να δείχνει στο αρχείο στο δίσκο. Η κλάση `Bitmap` βρίσκεται στο `System.Drawing`, το οποίο είναι μέρος του .NET runtime.

```csharp
using System.Drawing;

// Replace with the actual path to your image
string imagePath = @"C:\Invoices\invoice_table.png";
Bitmap bitmapImage = new Bitmap(imagePath);
```

**Γιατί αυτό το βήμα;**  
Η μηχανή OCR λειτουργεί πάνω σε ακατέργαστα δεδομένα εικονοστοιχείων, όχι σε διαδρομές αρχείων. Δημιουργώντας ένα `Bitmap` δίνουμε στο Aspose μια καθαρή, μνήμη‑διατηρούσα αναπαράσταση της εικόνας. Αν η εικόνα είναι κατεστραμμένη ή η διαδρομή είναι λανθασμένη, θα αντιμετωπίσετε εξαίρεση ακριβώς εδώ—οπότε ελέγξτε ξανά τη θέση.

## Βήμα 2: Διαμόρφωση της Μηχανής OCR για Ανίχνευση Πινάκων

Το Aspose.OCR μπορεί να αναγνωρίζει απλό κείμενο, αλλά θέλουμε να ψάξει για πίνακες. Ορίζοντας `DetectTables = true` λέμε στη μηχανή να αναζητήσει γραμμές πλέγματος και όρια κελιών.

```csharp
using Aspose.OCR;

// Create the OCR engine with table detection enabled
OcrEngine ocrEngine = new OcrEngine
{
    DetectTables = true,
    Language = OcrLanguage.English   // Change if your table is in another language
};
```

**Γιατί ενεργοποιούμε το `DetectTables`;**  
Όταν αυτή η σημαία είναι απενεργοποιημένη, η μηχανή επιστρέφει ένα μακρύ κείμενο που χάνει τη δομή γραμμής/στήλης. Όταν είναι ενεργοποιημένη, η μηχανή δημιουργεί εσωτερικά ένα `DataTable`, διατηρώντας την ακριβή διάταξη της πηγαίας εικόνας.

## Βήμα 3: Εξαγωγή του Πίνακα σε DataTable

Τώρα συμβαίνει η μαγεία. Η μέθοδος `ExtractTable` επιστρέφει ένα `System.Data.DataTable` που μπορείτε να χρησιμοποιήσετε όπως οποιονδήποτε άλλο πίνακα στο .NET.

```csharp
using System.Data;

// Extract the table from the bitmap
DataTable extractedTable = ocrEngine.ExtractTable(bitmapImage);
```

**Τι λαμβάνετε:**  
- Κεφαλίδες στηλών (αν το OCR τις αναγνωρίσει).  
- Γραμμές γεμάτες με τιμές κειμένου.  
- Κενά κελιά γίνονται `DBNull.Value`, τα οποία θα διαχειριστούμε αργότερα.

> **Pro tip:** Αν η εικόνα περιέχει πολλαπλούς πίνακες, το `ExtractTable` θα επιστρέψει μόνο τον πρώτο. Για να επεξεργαστείτε τους υπόλοιπους, θα χρειαστεί να περικόψετε το bitmap και να τρέξετε ξανά τη μηχανή.

## Βήμα 4: Εγγραφή του DataTable σε Αρχείο CSV

Το CSV είναι απλώς απλό κείμενο με κόμματα (ή άλλο διαχωριστή) που χωρίζουν τα πεδία. Θα ρέξουμε τις γραμμές σε ένα αρχείο, διαχειριζόμενοι τις τιμές `null` με προσοχή.

```csharp
using System.IO;

// Destination CSV path
string csvPath = @"C:\Invoices\invoice.csv";

using (var writer = new StreamWriter(csvPath))
{
    // Optional: write a header line if you want column names
    writer.WriteLine(string.Join(",", extractedTable.Columns
                                            .Cast<DataColumn>()
                                            .Select(col => EscapeCsv(col.ColumnName))));

    // Write each row
    foreach (DataRow row in extractedTable.Rows)
    {
        var fields = row.ItemArray.Select(item => EscapeCsv(item?.ToString() ?? string.Empty));
        writer.WriteLine(string.Join(",", fields));
    }
}

// Helper to escape commas, quotes, and newlines per CSV spec
static string EscapeCsv(string field)
{
    if (field.Contains(',') || field.Contains('\"') || field.Contains('\n'))
    {
        field = $"\"{field.Replace("\"", "\"\"")}\"";
    }
    return field;
}
```

**Γιατί ο βοηθός `EscapeCsv`;**  
Αν ένα κελί περιέχει κόμμα ή αλλαγή γραμμής, η απλή συνένωση θα σπάσει τη δομή του CSV. Τοποθετώντας τέτοια πεδία σε διπλά εισαγωγικά (και διαφράγοντας τα εσωτερικά εισαγωγικά) διασφαλίζουμε ότι το αρχείο παραμένει σωστά μορφοποιημένο.

## Βήμα 5: Επαλήθευση του Αποτελέσματος

Αφού ολοκληρωθεί το πρόγραμμα, ανοίξτε το `invoice.csv` σε οποιονδήποτε επεξεργαστή υπολογιστικών φύλλων. Θα πρέπει να δείτε γραμμές και στήλες που αντικατοπτρίζουν την αρχική εικόνα.

```text
Item,Quantity,Price
Widget A,10,9.99
Widget B,5,19.95
Total,,149.85
```

Αν το αποτέλεσμα φαίνεται «κοκκινισμένο» ή κάποια κελιά είναι κενά, σκεφτείτε τις παρακάτω προσαρμογές:

- **Αυξήστε την ανάλυση της εικόνας** πριν τη δώσετε στο OCR (π.χ., `bitmapImage.SetResolution(300, 300)`).  
- **Προεπεξεργασία εικόνας** (δυαδικοποίηση, διόρθωση κλίσης) χρησιμοποιώντας System.Drawing ή μια εξειδικευμένη βιβλιοθήκη εικόνας.  
- **Ρυθμίστε τις γλώσσες** αν ο πίνακας περιέχει μη‑Αγγλικούς χαρακτήρες.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

### Πώς να εξάγετε πίνακα όταν η εικόνα έχει πολλαπλές σελίδες;

> **Απάντηση:** Κάντε βρόχο σε κάθε σελίδα ενός πολυσελιδικού PDF ή TIFF, μετατρέψτε κάθε σελίδα σε `Bitmap` και εκτελέστε τα βήματα εξαγωγής ξεχωριστά. Προσθέστε κάθε παραγόμενο `DataTable` σε έναν κύριο πίνακα πριν το γράψετε σε CSV.

### Τι αν χρειάζομαι διαφορετικό διαχωριστικό (π.χ., ερωτηματικό);

Απλώς αντικαταστήστε το `","` στις κλήσεις `string.Join` με `";"` και προσαρμόστε τη λογική του `EscapeCsv` αναλόγως. Κάποιες τοπικές ρυθμίσεις προτιμούν `;` επειδή ο δεκαδικός διαχωριστής είναι το κόμμα.

### Μπορώ να παραλείψω τη γραμμή κεφαλίδας;

Αν η πηγαία εικόνα δεν περιλαμβάνει κεφαλίδες, σχολιάστε το τμήμα που γράφει τις κεφαλίδες:

```csharp
// writer.WriteLine(...); // Skip this line to omit column names
```

### Λειτουργεί αυτό με εικόνες PDF;

Το Aspose.OCR μπορεί να δεχτεί ένα `Bitmap` που προέρχεται από σελίδα PDF. Χρησιμοποιήστε το `Aspose.Pdf` για να αποδώσετε τη σελίδα PDF σε bitmap πρώτα, μετά δώστε το στην μηχανή OCR.

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο να μεταγλωττιστεί ως κονσολική εφαρμογή.

```csharp
using System;
using System.Data;
using System.Drawing;
using System.IO;
using System.Linq;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image that contains the table
        string imagePath = @"C:\Invoices\invoice_table.png";
        using Bitmap bitmapImage = new Bitmap(imagePath);

        // 2️⃣ Configure OCR for table detection
        OcrEngine ocrEngine = new OcrEngine
        {
            DetectTables = true,
            Language = OcrLanguage.English
        };

        // 3️⃣ Extract the table into a DataTable
        DataTable extractedTable = ocrEngine.ExtractTable(bitmapImage);

        // 4️⃣ Write the DataTable to CSV
        string csvPath = @"C:\Invoices\invoice.csv";
        using (var writer = new StreamWriter(csvPath))
        {
            // Write column headers
            writer.WriteLine(string.Join(",", extractedTable.Columns
                                                .Cast<DataColumn>()
                                                .Select(col => EscapeCsv(col.ColumnName))));

            // Write each row
            foreach (DataRow row in extractedTable.Rows)
            {
                var fields = row.ItemArray.Select(item => EscapeCsv(item?.ToString() ?? string.Empty));
                writer.WriteLine(string.Join(",", fields));
            }
        }

        // 5️⃣ Inform the user
        Console.WriteLine("Table extracted and saved as CSV.");
    }

    // Helper to escape CSV fields
    static string EscapeCsv(string field)
    {
        if (field.Contains(',') || field.Contains('\"') || field.Contains('\n'))
        {
            field = $"\"{field.Replace("\"", "\"\"")}\"";
        }
        return field;
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run`) και θα δείτε ένα μήνυμα επιβεβαίωσης. Το αρχείο CSV θα βρίσκεται δίπλα στην εικόνα σας, έτοιμο για εισαγωγή σε Excel, Power BI ή οποιοδήποτε σύστημα επεξεργασίας.

## Συμπεράσματα

Δείξαμε πώς να **εξάγετε δεδομένα πίνακα** από μια εικόνα, πραγματοποιήσαμε **ocr table extraction** και τελικά **μετατρέψαμε τον πίνακα σε CSV**—όλα ενώ διατηρούσαμε τον κώδικα καθαρό και την εξήγηση λεπτομερή. Το κύριο συμπέρασμα είναι ότι το Aspose.OCR μετατρέπει την κάποτε επίπονη διαδικασία μετατροπής *εικόνας πίνακα σε CSV* σε μια λειτουργία λίγων γραμμών κώδικα.

### Πού να Πηγαίνετε Στη Σύντομη Μελλοντική Περίοδο;

- **Επεξεργασία παρτίδας:** Τυλίξτε τη λογική σε βρόχο `foreach` για να διαχειριστείτε δεκάδες τιμολόγια ταυτόχρονα.  
- **Εισαγωγή σε βάση δεδομένων:** Χρησιμοποιήστε `SqlBulkCopy` για να σπρώξετε το CSV απευθείας σε SQL Server.  
- **Προχωρημένη ανάλυση:** Αν οι πίνακές σας περιέχουν συγχωνευμένα κελιά, σκεφτείτε επεξεργασία του `DataTable` για να ενοποιήσετε τις στήλες.

Πειραματιστείτε ελεύθερα—αλλάξτε το διαχωριστικό, προσθέστε καταγραφή, ή ενσωματώστε το σε ένα web API που λαμβάνει εικόνες σε πραγματικό χρόνο. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για οποιαδήποτε ροή εργασίας **αποθήκευσης πίνακα ως CSV**.

Καλή προγραμματιστική, και οι CSV σας να είναι πάντα τέλεια ευθυγραμμισμένες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}