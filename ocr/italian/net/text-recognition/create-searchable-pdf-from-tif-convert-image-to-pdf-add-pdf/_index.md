---
category: general
date: 2026-04-04
description: Crea PDF ricercabile da un'immagine TIF in C# – scopri come convertire
  l'immagine in PDF, aggiungere i metadati PDF e generare un documento ricercabile
  usando Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: it
og_description: Crea PDF ricercabile da un file TIF con C#. Converti l'immagine in
  PDF, aggiungi i metadati PDF e genera un documento ricercabile usando Aspose.OCR.
og_title: Crea PDF ricercabile da TIF – Guida passo‑passo
tags:
- Aspose.OCR
- C#
- PDF generation
title: Crea PDF ricercabile da TIF – Converti immagine in PDF, aggiungi metadati PDF
url: /it/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile da TIF – Guida Completa C#

Ti è mai capitato di **creare un PDF ricercabile** da una fattura scannerizzata senza sapere come mantenere il testo indicizzabile e i metadati del file ordinati? Non sei l'unico. In molti progetti di automazione il PDF deve essere sia leggibile dalla macchina sia correttamente etichettato con informazioni come titolo, autore e soglie di confidenza.  

In questa guida percorreremo una soluzione completa che **converte un’immagine in PDF**, inserisce **metadati PDF**, e filtra i risultati OCR a bassa confidenza—tutto con la libreria Aspose.OCR. Alla fine avrai a disposizione uno snippet pronto all'uso da inserire in qualsiasi progetto .NET, più alcuni consigli per gestire casi particolari.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.6+)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un’immagine TIF che desideri trasformare in PDF ricercabile (ad es., `input.tif`)  
- Familiarità di base con C# e Visual Studio (o il tuo IDE preferito)

Nessun altro servizio esterno è necessario: l’intero processo avviene in locale.

## Passo 1 – Configura il Motore OCR (Create Searchable PDF Core)

La prima cosa di cui abbiamo bisogno è un’istanza di `OcrEngine` che sappia quale lingua riconoscere. Nella maggior parte degli scenari aziendali l’inglese è sufficiente, ma puoi sostituire `Language.English` con qualsiasi lingua supportata.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Perché è importante:** Il motore OCR si occupa della parte più pesante, trasformando i pixel raster in testo Unicode. Impostare correttamente la lingua migliora l’accuratezza e riduce il numero di parole a bassa confidenza che verranno poi filtrate.

> **Consiglio professionale:** Se elabori documenti multilingue, istanzia più motori oppure usa `Language.Multilingual` per far sì che Aspose gestisca automaticamente il rilevamento della lingua.

## Passo 2 – Carica l’Immagine TIF (Create PDF from TIF)

Ora puntiamo il motore al file di origine. L’aiutante `ImageStream.FromFile` legge l’immagine in uno stream che il motore OCR può consumare.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Ti starai chiedendo, *“Posso fornire un JPEG o PNG invece?”* Assolutamente—Aspose.OCR supporta la maggior parte dei formati raster. Basta cambiare l’estensione del file e sei pronto.

## Passo 3 – Configura le Opzioni PDF (Add Metadata to PDF)

Prima della conversione, definiamo un oggetto `PdfOptions`. Qui è dove **aggiungiamo i metadati PDF** come titolo e autore, e allo stesso tempo indichiamo al motore di scartare le parole la cui confidenza è inferiore a una soglia.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Cosa succede qui?**  
- `Title` e `Author` diventano parte del dizionario delle informazioni del documento PDF, rendendo il file più facile da indicizzare nei sistemi di gestione documentale.  
- `MinConfidence` è una barriera di sicurezza: l’OCR spesso interpreta male caratteri sbiaditi; filtrandoli si mantiene pulito lo strato ricercabile e si migliora l’estrazione di testo successiva.

Se ti servono metadati personalizzati (ad es., `Subject`, `Keywords`), puoi impostarli tramite `PdfOptions.CustomProperties`.

## Passo 4 – Converti l’Immagine in un PDF Ricercabile (Convert Image to PDF)

Con il motore pronto e le opzioni impostate, la chiamata finale esegue la conversione. Scrive un PDF ricercabile su disco, incorporando lo strato di testo OCR sotto l’immagine originale.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Dopo l’esecuzione di questa riga, `output.pdf` contiene:
- L’immagine TIF originale come sfondo visivo  
- Uno strato di testo invisibile che i motori di ricerca e le operazioni di copia‑incolla possono leggere  
- I metadati definiti in precedenza (titolo, autore, ecc.)

### Risultato Atteso

Apri il PDF generato con Adobe Reader o qualsiasi visualizzatore PDF e prova a selezionare del testo. Dovresti riuscire a copiare frasi che corrispondono alla scansione originale. La finestra di dialogo **Proprietà** del documento mostrerà il titolo “Invoice #12345” e l’autore “MyCompany”.

## Passo 5 – Verifica il Filtraggio di Confidenza (Why MinConfidence Helps)

È utile confermare che le parole a bassa confidenza siano state effettivamente rimosse. Puoi ispezionare il testo nascosto del PDF usando uno strumento come `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Se la parola non compare, il filtro `MinConfidence` ha funzionato come previsto. Regola la soglia (ad es., `0.7f`) se ti serve un filtro più aggressivo o più permissivo.

## Passo 6 – Gestione di Pagine Multiple (Create Searchable PDF from Multi‑Page TIF)

Molte fatture arrivano come TIFF a più pagine. Aspose.OCR tratta ogni frame come una pagina separata automaticamente. Basta puntare il motore al file multi‑page; la stessa chiamata `ConvertToSearchablePdf` genererà un PDF ricercabile a più pagine.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Caso limite:** Se una pagina è vuota, l’OCR potrebbe comunque generare uno strato di testo vuoto, il che è innocuo. Tuttavia, puoi saltare le pagine vuote controllando `ocrEngine.HasText` prima della conversione.

## Passo 7 – Pacchettizzare l’Esempio Completo (All Steps Together)

Di seguito trovi un programma unico, pronto all’esecuzione, che unisce tutti i passaggi. Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella sul tuo computer.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Esegui il programma (`dotnet run` o premi **F5** in Visual Studio) e vedrai il messaggio di conferma. Il PDF generato verrà salvato accanto all’immagine di origine, pronto per l’indicizzazione o l’archiviazione.

## Domande Frequenti & Trappole

| Domanda | Risposta |
|----------|----------|
| **Posso aggiungere un font personalizzato allo strato ricercabile?** | Lo strato OCR utilizza Unicode; l’aspetto visivo è determinato dall’immagine di base, quindi non è necessario incorporare font aggiuntivi. |
| **E se il mio TIF è a colori?** | Aspose.OCR converte automaticamente le immagini a colori in scala di grigi per l’OCR, ma puoi mantenere i colori originali nel PDF impostando `PdfOptions.PreserveColor = true`. |
| **La libreria è thread‑safe?** | Ogni istanza di `OcrEngine` deve essere usata da un singolo thread. Per l’elaborazione parallela, crea un motore separato per ogni thread. |
| **Come crittografo il PDF?** | Usa `PdfOptions.Security` per impostare una password e i permessi dopo la conversione OCR. |

## Prossimi Passi (Espandi il Tuo Toolkit PDF)

- **Elaborazione batch:** Scorri una cartella di TIFF e genera un PDF ricercabile per ciascuno.  
- **Post‑processing:** Usa Aspose.PDF per unire i PDF generati in un unico documento master.  
- **Metadati avanzati:** Popola campi XMP personalizzati per una migliore integrazione con SharePoint o sistemi ECM.  

Tutte queste estensioni si basano sul modello di base appena mostrato: **crea PDF ricercabile**, **converti immagine in PDF**, e **aggiungi metadati PDF**.

---

*Buon coding! Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione di Aspose.OCR per gli ultimi aggiornamenti dell’API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}