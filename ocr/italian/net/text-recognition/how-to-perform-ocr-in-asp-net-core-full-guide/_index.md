---
category: general
date: 2026-05-28
description: Come eseguire OCR in ASP.NET Core—impara a caricare un'immagine, estrarre
  il testo dall'immagine e gestire il caricamento dei file in modo efficiente.
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: it
og_description: Come eseguire l'OCR in ASP.NET Core. Impara passo passo come caricare
  un'immagine, estrarre il testo dall'immagine e gestire il caricamento dei file con
  Aspose OCR.
og_title: Come eseguire l'OCR in ASP.NET Core – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: Come eseguire l'OCR in ASP.NET Core – Guida completa
url: /it/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in ASP.NET Core – Guida completa

Ti sei mai chiesto **come eseguire OCR** all'interno di una moderna API web senza impazzire? Non sei l'unico. Gli sviluppatori hanno costantemente bisogno di consentire agli utenti di caricare un'immagine—magari una ricevuta, una scansione di passaporto o una nota scritta a mano—e ottenere il testo grezzo in JSON.  

In questo tutorial percorreremo una soluzione completa, pronta per la produzione, che mostra **come caricare un file**, lo valida, esegue Aspose OCR e infine **estrae il testo dall'immagine**. Alla fine avrai un controller pronto da incollare che potrai inserire in qualsiasi progetto ASP.NET Core.

## Cosa Costruirai

- Un `OcrController` che accetta upload multipart/form‑data
- Validazione che il file esista realmente e non sia vuoto
- Elaborazione OCR asincrona usando il motore Aspose OCR
- Una risposta JSON pulita contenente il testo riconosciuto

## Prerequisiti (Cosa Ti Serve Prima di Iniziare)

| Requisito | Perché è Importante |
|-------------|----------------|
| .NET 6 SDK o successivo | ASP.NET Core 6+ ci fornisce funzionalità API minime e supporto async. |
| Visual Studio 2022 (o VS Code) | L'IDE semplifica il debug, ma funziona qualsiasi editor. |
| Pacchetto NuGet Aspose.OCR (`dotnet add package Aspose.OCR`) | Il motore che effettua realmente il lavoro di OCR. |
| Conoscenza di base di ASP.NET Core MVC | Useremo `ControllerBase` e gli attributi di routing. |

Se li hai, ottimo—tuffiamoci.

## Passo 1: Configura il Progetto e Installa Aspose OCR

Apri un terminale e crea un nuovo progetto web API:

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Quel singolo comando scarica la libreria OCR e tutte le sue dipendenze. Non c'è nient'altro da configurare; Aspose funziona subito per i formati di immagine più comuni.

## Passo 2: Aggiungi il Controller OCR (Il Cuore di **come eseguire OCR**)

Crea un nuovo file `Controllers/OcrController.cs` e incolla il codice seguente. È l'esempio completo e eseguibile—senza parti mancanti.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### Perché Funziona

- **`[FromForm] IFormFile`** indica ad ASP.NET Core di associare la parte multipart del file a `uploadedFile`. È il modo classico per **gestire il caricamento di file** in una web API.
- Il controllo `if` garantisce che gestiamo gli errori di **caricamento file** in modo elegante, restituendo un 400 Bad Request se il client ha dimenticato di inviare un file.
- `using var fileStream = uploadedFile.OpenReadStream();` apre uno stream *sola lettura*, essenziale per file di grandi dimensioni—non è necessario caricare l'intera immagine in memoria.
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` invia lo stream direttamente a Aspose OCR, mantenendo la pipeline snella.
- `await ocrEngine.RecognizeAsync();` esegue il lavoro pesante su un thread in background, così la nostra API rimane reattiva. Questo è il cuore di **come eseguire OCR** in modo asincrono.
- Infine, avvolgiamo il risultato in un oggetto JSON (`{ extractedText }`)—perfetto per il consumo da parte del front‑end.

## Passo 3: Configura il Limite di Dimensione della Richiesta (Opzionale ma Utile)

Se ti aspetti scansioni ad alta risoluzione, aumenta la dimensione predefinita della richiesta. Aggiungi questo a `Program.cs`:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

Ora l'API non si bloccherà con un'immagine di ricevuta da 10 MB. Regola il limite in base al tuo caso d'uso.

## Passo 4: Testa l'Endpoint con cURL o Postman

Ecco un rapido comando cURL che puoi eseguire dal terminale:

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

Dovresti vedere un payload JSON simile a:

```json
{
  "extractedText": "Sample text that was on the image."
}
```

Se l'immagine non contiene caratteri riconoscibili, la stringa sarà vuota—nulla si blocca, solo un risultato vuoto. È un caso limite da tenere presente.

## Passo 5: Conferma Visiva (Immagine Opzionale)

Di seguito è un'immagine segnaposto che mostra la risposta JSON che riceverai dopo una richiesta OCR riuscita.

![Risultato di come eseguire OCR – screenshot della risposta JSON che mostra il testo estratto](/images/ocr-result.png)

*Testo alternativo:* **screenshot del risultato di come eseguire OCR che mostra il testo estratto dall'immagine**

## Problemi Comuni & Consigli Pro

| Problema | Soluzione |
|---------|----------|
| **Formato immagine non supportato** (es. TIFF con più pagine) | Converti prima in PNG/JPEG o usa `ImageConverter` di Aspose prima di passarlo a `OcrEngine`. |
| **File di grandi dimensioni causano pressione sulla memoria** | Streamma il file come mostrato; evita `IFormFile.CopyToAsync` in un `MemoryStream`. |
| **OCR restituisce testo incomprensibile** | Assicurati che l'immagine abbia alto contrasto e sia orientata correttamente. Pre‑processa con `ocrEngine.Preprocess()` se necessario. |
| **Richieste concorrenti multiple** | Aspose OCR è thread‑safe, ma potresti voler limitare la concorrenza con un semaforo se il tuo server ha risorse di memoria limitate. |

## Estendere l'Esempio: Upload di Massa & Elaborazione Parallela

Se hai bisogno di **gestire il caricamento di file** per diverse immagini contemporaneamente, modifica la firma dell'azione per accettare una lista:

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

Ora puoi **caricare OCR di immagini** in massa—ideale per scansionare una cartella di ricevute in un unico passaggio.

## Considerazioni di Sicurezza

- **Convalida le estensioni dei file** (`.png`, `.jpg`, `.jpeg`) prima di processarli per evitare upload dannosi.
- **Scansiona alla ricerca di virus** se la tua API è esposta a internet; integra un servizio come ClamAV.
- **Limita la frequenza** dell'endpoint per prevenire attacchi di denial‑of‑service.

## Output Atteso & Come Verificarlo

Quando chiami l'endpoint `/ocr/upload` con un'immagine chiara contenente la parola “Hello”, la risposta dovrebbe essere:

```json
{
  "extractedText": "Hello"
}
```

Puoi verificare rapidamente aprendo gli strumenti per sviluppatori del browser → scheda Network, o ispezionando l'output di cURL.

## Riepilogo – Cosa Abbiamo Coperto

- Configurato un progetto ASP.NET Core e aggiunto il pacchetto NuGet Aspose OCR.
- Implementato un controller pulito che mostra **come eseguire OCR**, **gestire il caricamento di file**, e **estrarre testo dall'immagine**.
- Discutito la gestione degli errori, ottimizzazioni delle prestazioni e le migliori pratiche di sicurezza.
- Fornito un esempio di codice pronto all'uso più una variante per upload di massa.

## Prossimi Passi

- **Aggiungi supporto linguistico**: Aspose OCR può essere configurato per diverse lingue (`ocrEngine.Language = Language.English;`).
- **Integra con un database**: Salva il testo estratto insieme ai metadati per ricerche future.
- **Interfaccia front‑end**: Costruisci una semplice pagina React o Blazor che consenta agli utenti di trascinare le immagini e vedere immediatamente il risultato OCR.

Sentiti libero di sperimentare—sostituisci il motore OCR, prova diversi passaggi di pre‑processamento dell'immagine, o collega il risultato a un modello AI a valle. Il cielo è il limite quando sai **come eseguire OCR** in uno stack .NET moderno.

Buon coding, e che il tuo testo sia sempre leggibile!

## Tutorial Correlati

- [Come fare OCR su Immagine – Eseguire OCR su Immagine in Riconoscimento Immagine OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Come Usare Aspose per Riconoscere Immagine da Stream in Riconoscimento Immagine OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Come Impostare il Valore di Soglia in Riconoscimento Immagine OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}