---
category: general
date: 2026-04-04
description: Scopri come utilizzare Aspose per estrarre i dati della ricevuta, caricare
  l'immagine della ricevuta ed eseguire l'OCR dell'immagine della ricevuta con un
  esempio completo in C#. Guida passo‑passo per gli sviluppatori.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: it
og_description: Come utilizzare Aspose per estrarre i dati della ricevuta da un'immagine
  di ricevuta scannerizzata. Codice C# completo, spiegazioni e consigli per l'elaborazione
  OCR di immagini di ricevute.
og_title: Come utilizzare Aspose – Estrarre i dati della ricevuta dalle immagini
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Come utilizzare Aspose – Estrarre i dati della ricevuta dalle immagini in C#
url: /it/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare Aspose – Estrarre dati di ricevuta da immagini in C#

Ti sei mai chiesto **come usare Aspose** per estrarre informazioni strutturate da una foto di una ricevuta? Non sei l'unico. Che tu stia costruendo un'app di tracciamento spese o automatizzando l'inserimento delle fatture, il problema è lo stesso: hai un PNG o JPEG e ti servono il nome del commerciante, la data e l'importo totale senza digitare manualmente.

Il punto è che Aspose.OCR rende tutta la pipeline un gioco da ragazzi. In questo tutorial vedremo come caricare un'immagine di ricevuta, eseguire l'OCR e infine estrarre i dati della ricevuta con poche righe di C#. Alla fine avrai un programma console eseguibile che stampa il commerciante, la data e l'importo totale direttamente nella console.

> **Quick win:** Se ti serve solo il codice, vai subito alla sezione “Esempio completo funzionante” in fondo e copia‑incolla.

## Cosa ti servirà

- **.NET 6.0 o successivo** (l'API funziona con .NET Core e .NET Framework)
- **Aspose.OCR for .NET** pacchetto NuGet (`Install-Package Aspose.OCR`)
- Un'immagine di esempio di una ricevuta (PNG, JPG o BMP) salvata localmente
- Visual Studio 2022 o qualsiasi editor che supporti progetti C#

Non sono richieste altre librerie di terze parti. L'unico prerequisito è una conoscenza di base delle applicazioni console C#—se hai scritto “Hello World”, sei pronto.

## Passo 1 – Installa e riferisci Aspose.OCR

Per **come usare Aspose**, devi prima aggiungere la libreria al tuo progetto. Apri la Package Manager Console ed esegui:

```powershell
Install-Package Aspose.OCR
```

In alternativa, usa l'interfaccia NuGet UI e cerca “Aspose.OCR”. Una volta installato, aggiungi gli spazi dei nomi richiesti all'inizio del file:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip:** Mantieni i pacchetti NuGet aggiornati. A partire da oggi (aprile 2026) l'ultima versione stabile è la 23.11.0, che include miglioramenti di prestazioni per l'OCR su ricevute ad alta risoluzione.

## Passo 2 – Carica l'immagine della ricevuta

Quando **carichi immagini di ricevuta**, hai due fonti comuni: un percorso locale o uno stream da una richiesta web. Per questo tutorial lo semplifichiamo leggendo dal disco:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Sostituisci `YOUR_DIRECTORY/receipt.png` con il percorso reale del tuo file di ricevuta. Se gestisci upload da parte degli utenti, puoi fornire un `MemoryStream` a `ImageStream.FromStream`.

> **Perché è importante:** Specificare la lingua (English) indica al motore OCR quale set di caratteri aspettarsi, riducendo i falsi riconoscimenti—particolarmente importante quando **ocr receipt image** contiene numeri e simboli.

## Passo 3 – Esegui l'OCR e cattura le informazioni di layout

Il passo OCR fa più che restituire testo grezzo; cattura anche il layout, fondamentale per l'estrazione strutturata successiva.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Dopo che `Recognize()` termina, `ocrEngine` contiene sia il testo semplice sia i dati posizionali di ogni parola. Questa è la base per il passo successivo, dove chiederemo ad Aspose di “**come estrarre ricevuta**” i campi automaticamente.

## Passo 4 – Inizializza il Layout Recognizer

Aspose fornisce una classe `LayoutRecognizer` che conosce come le ricevute sono tipicamente organizzate (commerciante in alto, riga data, totale in basso). Basta passare il motore OCR configurato:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Sotto il cofano, il recognizer applica un insieme di euristiche—come la ricerca di simboli di valuta o pattern di data—per mappare il testo grezzo a campi semantici.

## Passo 5 – Estrai i dati strutturati della ricevuta

Ora arriva la parte migliore: **estrarre dati della ricevuta**. Una singola chiamata al metodo fa il lavoro pesante:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` è un oggetto di tipo `ReceiptData` (definito in `Aspose.OCR.Structured`). Contiene tre proprietà principali:

- `Merchant` – il nome del negozio
- `Date` – la data di acquisto come `DateTime` (se rilevata)
- `TotalAmount` – l'importo totale come `decimal`

Se il motore non riesce a trovare un campo specifico, la proprietà sarà `null` o `0`. Puoi aggiungere logica di fallback se necessario (ad es., chiedere all'utente di confermare).

## Passo 6 – Visualizza le informazioni estratte

Infine, stampa i risultati nella console. Qui vedrai i frutti del tuo lavoro:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Le stringhe di formato (`:d` e `:C`) producono rispettivamente una data breve e una stringa di valuta, rendendo l'output leggibile.

### Output previsto

Supponendo che la ricevuta appartenga a “Coffee Corner”, datata 2025‑12‑01, con un totale di $4.75, la console mostrerà:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Se qualche campo manca, vedrai una riga vuota o un valore predefinito—perfetto per il debug.

## Casi limite e problemi comuni

### 1. Immagini a bassa risoluzione
Se l'immagine della ricevuta è sfocata o inferiore a 150 dpi, l'accuratezza dell'OCR cala drasticamente. Upscaling dell'immagine con un semplice filtro bilineare prima di passarla ad Aspose può migliorare i risultati.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Ricevute non in inglese
L'esempio principale usa `Language.English`. Per ricevute multilingue, imposta `Language` sull'enum appropriato (ad es., `Language.French`) o usa `Language.AutoDetect` se non sei sicuro.

### 3. Più ricevute in una singola immagine
Il layout recognizer di Aspose si aspetta una sola ricevuta per immagine. Se hai una foto con più ricevute affiancate, dovrai pre‑processare l'immagine—ritagliare ogni ricevuta in un file separato prima di eseguire l'OCR.

### 4. Simbolo di valuta mancante
A volte l'importo totale appare senza il simbolo `$`. Il recognizer individua comunque i numeri, ma potresti dover post‑processare la stringa per garantire la corretta posizione decimale.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Consigli professionali per la produzione

- **Cache il motore OCR** se elabori molte ricevute in batch; riutilizzare la stessa istanza riduce l'overhead di allocazione.
- **Logga il testo OCR grezzo** (`ocrEngine.Text`) per audit trail. È utile quando un campo non viene estratto.
- **Avvolgi l'intero flusso in try/catch** e mostra un messaggio di errore amichevole (es., “Impossibile leggere la ricevuta, per favore carica un'immagine più chiara”).

## Esempio completo funzionante

Di seguito trovi un'applicazione console autonoma che puoi compilare ed eseguire così com'è. Sostituisci solo il percorso dell'immagine e sei pronto.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Eseguire il codice**

1. Crea un nuovo progetto console .NET (`dotnet new console -n ReceiptExtractor`).
2. Aggiungi il pacchetto Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Sostituisci il `Program.cs` generato con lo snippet sopra.
4. Posiziona un'immagine di ricevuta nel percorso specificato.
5. Compila ed esegui (`dotnet run`).

Dovresti vedere il commerciante, la data e il totale stampati esattamente come mostrato in precedenza.

## Conclusioni

In questa guida abbiamo coperto **come usare Aspose** per **caricare immagini di ricevuta**, eseguire **ocr receipt image**, e infine **estrarre dati di ricevuta** con poche righe di codice. Il punto chiave è che Aspose.OCR si occupa del lavoro pesante—una volta configurato il motore OCR, il `LayoutRecognizer` trasforma il testo grezzo in un oggetto strutturato di cui ti puoi fidare.

Prossimi passi? Prova a inserire i valori estratti in un database, genera un riepilogo PDF della ricevuta, o alimentali a un modello di machine‑learning per la classificazione delle spese. Puoi anche sperimentare con altri tipi di documenti strutturati come fatture o etichette di spedizione—`ExtractInvoiceData` di Aspose funziona in modo molto simile.

Hai domande su casi limite o vuoi vedere come gestire PDF multi‑pagina? Lascia un commento o consulta la documentazione ufficiale di Aspose.OCR per scenari avanzati. Buona programmazione, e goditi la semplicità di **come usare Aspose** per l'automazione delle ricevute!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}