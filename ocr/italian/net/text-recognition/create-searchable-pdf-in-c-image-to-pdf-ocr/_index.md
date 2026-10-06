---
category: general
date: 2026-02-28
description: Crea PDF ricercabile da un TIFF multipagina in C#. Questa guida mostra
  come convertire un'immagine in PDF ricercabile con un esempio completo di OCR in
  C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: it
og_description: Crea PDF ricercabile da un TIFF usando Aspose.OCR. Segui questo esempio
  passo‑passo di OCR in C# per trasformare le immagini in PDF ricercabili.
og_title: Crea PDF ricercabile in C# – Da immagine a PDF con OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: Crea PDF Ricercabile in C# – Da immagine a PDF con OCR
url: /it/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile in C# – Immagine a PDF OCR

Hai mai avuto bisogno di **creare PDF ricercabili** da un documento scansionato ma non sapevi da dove cominciare? Non sei l'unico. In molti flussi di lavoro d'ufficio un PDF ricercabile è la differenza tra un file senza via d'uscita e un archivio ricercabile.  

In questo tutorial vedremo un **esempio c# ocr** completo che trasforma un TIFF multi‑pagina in un PDF ricercabile, il tutto con Aspose.OCR. Alla fine saprai esattamente come **convertire un'immagine in PDF ricercabile**, come **convertire tiff in pdf**, e avrai uno snippet di codice pronto all'uso da inserire in qualsiasi progetto .NET.

## Cosa Imparerai

* Come installare e fare riferimento ad Aspose.OCR in un progetto C#.  
* I passaggi esatti per caricare un TIFF, impostare la lingua e chiamare `RecognizeToPdf`.  
* Perché ogni passaggio è importante – dalla gestione della memoria alla selezione della lingua.  
* Suggerimenti per gestire documenti di grandi dimensioni, risolvere problemi comuni di OCR e estendere la soluzione ad altri formati immagine.

**Prerequisiti** – un SDK .NET recente (4.6+ o .NET Core 3.1+), Visual Studio (o il tuo IDE preferito) e una licenza Aspose.OCR (la versione di prova gratuita è sufficiente per i test). Non sono richieste altre librerie esterne.

---

## Creare PDF Ricercabile – Panoramica

A livello alto il processo è così:

1. **Inizializzare** il `OcrEngine`.  
2. **Caricare** l'immagine sorgente (un TIFF nel nostro caso).  
3. **Configurare** le impostazioni della lingua per una maggiore precisione.  
4. **Eseguire** l'OCR e **salvare** il risultato direttamente come PDF ricercabile.  

È tutto. L'API di Aspose si occupa del lavoro pesante, così non devi combinare librerie OCR e PDF separate.

---

## Passo 1: Installa Aspose.OCR e Configura il Tuo Progetto

Per prima cosa, aggiungi il pacchetto NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

Oppure, se preferisci la Console di Gestione Pacchetti in Visual Studio:

```powershell
Install-Package Aspose.OCR
```

Dopo che il pacchetto è stato ripristinato, apri il file del progetto e verifica il riferimento:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Consiglio professionale:** Usa l'ultima versione stabile (controlla il sito Aspose) per ottenere correzioni di bug e i pacchetti lingua più recenti.

---

## Passo 2: Converti TIFF in PDF – Caricamento dell'Immagine

Ora caricheremo il TIFF che vuoi rendere ricercabile. Il metodo `Image.Load` di Aspose supporta i TIFF multi‑pagina senza configurazioni aggiuntive.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Perché è importante:** Caricare l'immagine all'interno di un blocco `using` garantisce che le risorse non gestite vengano rilasciate prontamente—fondamentale quando si elaborano documenti di grandi dimensioni.

---

## Passo 3: Immagine a PDF Ricercabile – Configurazione del Motore OCR

Prima di eseguire l'OCR indicheremo al motore quale lingua aspettarsi. L'inglese funziona nella maggior parte dei casi, ma puoi sostituire con qualsiasi valore dell'enumerazione `OcrLanguage`.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Nota dell'esperto:** Selezionare la lingua corretta riduce drasticamente le errate riconoscenze. Se hai lingue miste, puoi combinarle con l'operatore `|`, ad esempio `OcrLanguage.English | OcrLanguage.French`.

---

## Passo 4: Esempio OCR in C# – Riconosci e Salva

Con il motore pronto, chiama `RecognizeToPdf`. Il metodo scrive il PDF ricercabile direttamente su disco, incorporando uno strato di testo invisibile dietro l'immagine originale.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Dopo l'esecuzione di questa riga, `output.pdf` conterrà le pagine TIFF originali più un overlay di testo nascosto che qualsiasi lettore PDF può ricercare.

---

## Passo 5: Immagine C# a PDF – Verifica il Risultato

Confermiamo che tutto ha funzionato. Apri il PDF generato in Adobe Reader (o qualsiasi visualizzatore) e prova a cercare una parola che sai è presente nel TIFF di origine.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Se la ricerca restituisce risultati, hai creato con successo **pdf ricercabile** da un'immagine. In caso contrario, ricontrolla l'impostazione della lingua o la qualità del TIFF di origine.

---

## Esempio Completo Funzionante

Mettendo insieme tutti i pezzi, ecco un'app console autonoma che puoi compilare ed eseguire:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Output previsto** (nella console):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Apri `output.pdf` e dovresti poter digitare qualsiasi parola del TIFF originale nella casella di ricerca del visualizzatore e vedere le corrispondenze evidenziate.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="esempio di pdf ricercabile"}

*Lo screenshot sopra mostra un PDF ricercabile aperto in un visualizzatore con lo strato di testo nascosto attivo.*

---

## Domande Frequenti & Casi Limite

### Cosa succede se il mio TIFF è enorme (centinaia di pagine)?

Aspose.OCR elabora le pagine una alla volta, ma potresti comunque raggiungere i limiti di memoria. Considera di elaborare il TIFF in batch:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Successivamente, unisci i PDF per pagina con una libreria PDF (ad esempio, Aspose.PDF).

### Posso esportare in un formato diverso, come DOCX ricercabile?

Sì—usa `RecognizeToDocument` invece di `RecognizeToPdf`. L'API rispecchia il metodo PDF, basta cambiare l'estensione del file di destinazione.

### Come gestisco lingue diverse dall'inglese?

Sostituisci `OcrLanguage.English` con l'enumerazione appropriata, ad esempio `OcrLanguage.Spanish`. Puoi anche combinare le lingue:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### E i PDF protetti da password?

Dopo il passaggio OCR, puoi aprire il PDF generato con Aspose.PDF e applicare la crittografia:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Riepilogo

Abbiamo coperto tutto ciò di cui hai bisogno per **creare file PDF ricercabili** da immagini TIFF usando C#. Dall'installazione di Aspose.OCR, al caricamento dell'immagine, alla configurazione della lingua, all'esecuzione dell'OCR e infine alla verifica dell'output ricercabile, ora disponi di un solido **esempio c# ocr** che puoi adattare ad altri formati.  

Se sei pronto a fare di più, prova:

* **Converti TIFF in PDF** per archivi non ricercabili (basta saltare il passaggio OCR).  
* Sperimenta con **immagine a PDF ricercabile**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}