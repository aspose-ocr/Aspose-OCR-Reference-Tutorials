---
category: general
date: 2026-02-13
description: Come leggere rapidamente una ricevuta usando Aspose OCR ed estrarre l'importo
  con regex. Impara a elaborare passo‑passo la ricevuta con OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: it
og_description: Come leggere una ricevuta in C# usando Aspose OCR e regex. Questa
  guida ti mostra come elaborare la ricevuta con OCR ed estrarre l'importo totale.
og_title: Come leggere una ricevuta in C# – Tutorial completo su OCR e Regex
tags:
- OCR
- C#
- Regex
- Aspose
title: Come leggere una ricevuta in C# – Guida OCR + Regex
url: /it/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

lists, blockquote, code placeholders, tables.

Check for any missed bold: we kept bold phrases unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come leggere una ricevuta in C# – Guida OCR + Regex

Ti sei mai chiesto **come leggere una ricevuta** dalle immagini senza digitare manualmente ogni riga? In molte app per piccole imprese è necessario estrarre l'importo totale da una foto di una ricevuta, e farlo a mano vanifica lo scopo dell'automazione. La buona notizia? Con Aspose OCR puoi lasciare che il motore faccia il lavoro pesante, poi una semplice espressione regolare individuerà il totale. In questo tutorial vedremo **process receipt with OCR**, estrarremo l'importo usando regex e otterremo un valore totale pronto all'uso.

Vedrai un esempio completo e eseguibile, scoprirai perché il modello linguistico per le ricevute è importante e otterrai consigli per gestire casi limite come simboli di valuta diversi o etichette “Total” mancanti. Non sono necessari documenti esterni—tutto ciò di cui hai bisogno è qui.

## Cosa imparerai

- Come configurare Aspose OCR per il riconoscimento specifico delle ricevute (il modello linguistico `Receipt` de‑skew e de‑noise automaticamente l'immagine).  
- Come applicare un'espressione regolare che **extract amount using regex** pattern che funzionano per la maggior parte delle ricevute in stile US.  
- Come gestire variazioni comuni come “TOTAL”, “Total:”, o “Grand Total – $12.34”.  
- Come outputtare il risultato in modo sicuro e cosa fare quando il pattern non viene trovato.  

**Prerequisites**: .NET 6+ (or .NET Framework 4.7+), una licenza valida di Aspose OCR o una versione di prova, e un'immagine di una ricevuta salvata localmente. È tutto—nessun pacchetto NuGet extra oltre Aspose.OCR.

---

## Passo 1 – Installa Aspose OCR e prepara il progetto

### Perché è importante

Aspose OCR fornisce un modello **process receipt with OCR** appositamente progettato che sa come raddrizzare un foglio accartocciato e ignorare il rumore di fondo. Usare il modello di testo generico produrrebbe più errori, soprattutto su scansioni a bassa risoluzione.

### Codice

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro tip:** Mantieni il file di licenza al di fuori della cartella di controllo del codice sorgente per evitare commit accidentali.

---

## Passo 2 – Configura il motore OCR per il riconoscimento delle ricevute

### Perché è importante

Il modello linguistico `Receipt` include de‑skew e de‑noise integrati, il che migliora notevolmente l'accuratezza su ricevute reali spesso piegate o accartocciate.

### Codice

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Passo 3 – Riconosci il testo dall'immagine della ricevuta

### Perché è importante

Hai bisogno del testo grezzo prima di poter applicare qualsiasi regex. Il metodo `RecognizeImage` restituisce un `OcrResult` contenente la stringa completa, i punteggi di confidenza e altro se ti servono in seguito.

### Codice

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Output OCR previsto (esempio)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Passo 4 – Costruisci una Regex per **Extract Amount Using Regex**

### Perché è importante

Le ricevute sono disponibili in molti formati, ma la parola “Total” (o una variante simile) seguita da un importo in dollari è un'ancora affidabile. Il pattern qui sotto tollera spazi opzionali, due punti, trattini e un segno `$` opzionale.

### Codice

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Spiegazione del pattern**

| Part | Meaning |
|------|---------|
| `Total` | Cerca la parola “Total” (case‑insensitive). |
| `\s*[:\-]?` | Consente qualsiasi spazio bianco, poi un due punti o un trattino opzionale. |
| `\s*\$?` | Spazio bianco opzionale e segno dollaro opzionale. |
| `(\d+(\.\d{2})?)` | Cattura una o più cifre, opzionalmente seguite da un decimale e due centesimi. |

---

## Passo 5 – Output del totale estratto o gestione dei dati mancanti

### Perché è importante

Anche il miglior OCR può perdere una parola, soprattutto su ricevute sfocate. Fornire un fallback elegante previene crash e ti offre un punto di aggancio per logica personalizzata (ad esempio, chiedere all'utente di confermare).

### Codice

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Esempio di output console**

```
Total: $12.25
```

---

## Esempio completo funzionante – Tutti i passaggi in un unico file

Di seguito trovi un unico programma autonomo che puoi copiare‑incollare in un progetto console. Include commenti, gestione degli errori e il caricamento opzionale della licenza.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Esecuzione del programma**

1. Crea un nuovo progetto console (`dotnet new console -n ReceiptReader`).  
2. Aggiungi il pacchetto NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Sostituisci `YOUR_DIRECTORY/receipt.jpg` con il percorso reale di un'immagine di ricevuta.  
4. Compila ed esegui (`dotnet run`).  

Dovresti vedere il dump OCR seguito da `Total: $xx.xx` se tutto è allineato.

---

## Gestione dei casi limite e variazioni comuni

### 1. Simboli di valuta diversi

Se lavori con euro (€) o sterline (£), estendi il pattern:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Etichetta “Total” mancante

Alcune ricevute mostrano solo “Grand Total”. Aggiungi un'alternativa:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Totali multipli (ad esempio, “Subtotal” e “Total”)

Se la regex corrisponde alla prima occorrenza, potresti volere l'**ultima** corrispondenza:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Immagini a bassa risoluzione

- Aumenta i DPI durante la scansione (`300 DPI` è un buon compromesso).  
- Pre‑processa l'immagine con un semplice filtro di riduzione sfocatura prima di passarla ad Aspose (fuori dallo scopo di questa guida, ma vale la pena esplorarlo).

---

## Pro Tips per progetti reali

- **Cache the OCR result** se hai bisogno di estrarre diversi campi (tassa, articoli, ecc.) – paghi il costo OCR una sola volta.  
- **Log the raw OCR text** su un database; diventa una preziosa traccia di audit per spese contestate.  
- Quando costruisci un'API web, **run OCR in a background worker**; può richiedere qualche centinaio di millisecondi, il che è accettabile in modo asincrono ma non ideale per una richiesta sincrona.  
- **Validate the extracted amount** rispetto alle regole di business (ad esempio, l'importo deve essere > 0) prima di salvare.  

---

## Conclusione

Abbiamo coperto **how to read receipt** immagini in C# usando Aspose OCR, poi **extract amount using regex** per trovare in modo affidabile la riga del totale. Sfruttando il modello linguistico `Receipt` ottieni testo de‑skewed, de‑noised, e una regex concisa gestisce la maggior parte delle stranezze di formattazione. Lo snippet di codice completo sopra è pronto per essere inserito in qualsiasi progetto .NET console o di servizio, e i suggerimenti aggiuntivi per i casi limite ti forniscono una solida base per l'uso in produzione.

Pronto per il passo successivo? Prova ad estendere la soluzione per estrarre le singole voci di riga, calcolare automaticamente le tasse, o integrare con un'API di tracciamento delle spese. E se ti imbatti in una ricevuta che rompe il pattern, ricorda che l'approccio **regex find total** è solo un punto di partenza—puoi sempre modificare il pattern per adattarlo al tuo locale specifico.

Buon coding, e che il tuo processamento delle ricevute sia veloce, accurato e completamente automatizzato!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}