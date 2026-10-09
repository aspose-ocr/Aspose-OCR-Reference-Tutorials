---
category: general
date: 2026-02-24
description: Come abilitare la GPU nell'esempio Aspose OCR C# – converti rapidamente
  un'immagine in testo semplice. Include impostazione dell'ID del dispositivo GPU
  e guida C# per leggere il testo dell'immagine.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: it
og_description: Come abilitare la GPU nell'esempio Aspose OCR C#. Impara a impostare
  l'ID del dispositivo GPU e a leggere il testo dell'immagine in C# in modo efficiente.
og_title: Come abilitare la GPU per Aspose OCR in C# – Conversione rapida da immagine
  a testo semplice
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Come abilitare la GPU per Aspose OCR in C# – Conversione rapida da immagine
  a testo
url: /it/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per Aspose OCR in C# – Conversione rapida da immagine a testo semplice

Ti sei mai chiesto **come abilitare la GPU** quando usi Aspose OCR per trasformare un'immagine in testo modificabile? Non sei solo—molti sviluppatori incontrano il collo di bottiglia delle prestazioni quando elaborano grandi fatture o contratti scansionati. La buona notizia? Convertire un'immagine in testo semplice può essere fulmineo una volta sfruttata la tua scheda grafica.

In questa guida percorreremo un **esempio completo di Aspose OCR** che ti mostra esattamente come abilitare la GPU, impostare l'ID del dispositivo GPU e **leggere il testo dell'immagine in C#**. Alla fine avrai un programma eseguibile che estrae testo da qualsiasi immagine supportata in una frazione del tempo necessario a un approccio solo CPU.

## Cosa ti serve

- .NET 6.0 o versioni successive (l'API funziona con .NET Core e .NET Framework)
- Una GPU compatibile CUDA con l'ultimo driver installato
- Una licenza Aspose.OCR per .NET (o una prova gratuita, che funziona per lo sviluppo)
- Visual Studio 2022 (o qualsiasi editor C# tu preferisca)

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.OCR`—solo la libreria stessa.

---

## Passo 1 – Installa il pacchetto NuGet Aspose OCR

Prima di tutto, aggiungi la libreria ufficiale Aspose OCR al tuo progetto. Apri la Package Manager Console ed esegui:

```powershell
Install-Package Aspose.OCR
```

Questo scarica `Aspose.OCR.dll` e tutte le sue dipendenze. Se preferisci l'interfaccia grafica, fai clic destro sul progetto → **Manage NuGet Packages** → cerca *Aspose.OCR* e fai clic su **Install**.  

*Consiglio:* Dopo l'installazione, verifica che la cartella `Aspose.OCR` compaia sotto **Dependencies** in Solution Explorer.

---

## Passo 2 – Crea uno scheletro di app console semplice

Costruiremo una piccola app console che dimostra l'intero flusso. Crea un nuovo progetto:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Sostituisci il `Program.cs` generato con il codice completo mostrato più avanti. Questo scheletro ci fornisce un punto di ingresso pulito e ci permette di concentrarci sulla logica OCR.

---

## Passo 3 – Come abilitare la GPU e impostare l'ID del dispositivo GPU

Ora la star dello spettacolo: **come abilitare la GPU** in Aspose OCR. La libreria espone un oggetto `OcrSettings` dove puoi attivare `UseGpu` e opzionalmente scegliere un dispositivo CUDA specifico tramite `GpuDeviceId`. Di seguito trovi lo snippet esatto da inserire nel tuo programma:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Perché abilitare la GPU?

Abilitare la GPU scarica il lavoro pesante—pre‑elaborazione dei pixel, segmentazione dei caratteri e inferenza della rete neurale—sulla scheda grafica. Su una modesta GTX 1650, puoi osservare un **incremento di velocità 2‑3×** rispetto alla modalità solo CPU, soprattutto con documenti ad alta risoluzione.

### Scegliere un ID dispositivo

Se il tuo computer ha più GPU, `GpuDeviceId` ti permette di puntare a una specifica. `0` seleziona il primo dispositivo; `1` scegli il secondo, e così via. Puoi scoprire gli ID disponibili usando lo strumento NVIDIA `nvidia-smi` o interrogando la classe `GpuInfo` di Aspose (non mostrata qui per brevità).

---

## Passo 4 – Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo, pronto per l'esecuzione. Incollalo in `Program.cs`, sostituisci il percorso dell'immagine con un file reale sul tuo disco, e premi **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Output previsto

Se l'immagine fornita contiene la riga *“Invoice #12345 – Total $1,250.00”*, la console stamperà:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Il risultato è testo semplice, pronto per ulteriori elaborazioni (ad esempio, inserimento in un database o in un parser di linguaggio naturale).

---

## Passo 5 – Verifica l'utilizzo della GPU (opzionale)

Per assicurarti che la GPU sia effettivamente in uso, apri lo strumento di monitoraggio GPU (come **NVIDIA‑Smi** o **GPU‑Z**) mentre il programma è in esecuzione. Dovresti vedere un picco nell'utilizzo di calcolo del dispositivo selezionato. Se vedi solo attività CPU, ricontrolla che:

- Il driver della GPU è aggiornato.
- Il flag `UseGpu` è impostato su `true`.
- Il formato della tua immagine è supportato (PNG, JPEG, TIFF, ecc.).

---

## Problemi comuni e come evitarli

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **GPU non rilevata** | Driver obsoleto o runtime CUDA mancante | Installa l'ultimo driver NVIDIA e il toolkit CUDA |
| **`Aspose.OCR` lancia “GPU not supported”** | Esecuzione su una GPU non CUDA (es. AMD più vecchia) | Imposta `UseGpu = false` o passa a una GPU compatibile |
| **Percorso immagine errato** | Il percorso relativo punta alla cartella sbagliata | Usa un percorso assoluto o passa il percorso come argomento da riga di comando |
| **Licenza non applicata** | La modalità di valutazione può limitare l'uso della GPU | Registra una licenza con `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Estendere l'esempio: Elaborazione batch con GPU

Se devi elaborare decine di fatture, avvolgi la chiamata di riconoscimento in un ciclo. Poiché la GPU rimane calda, le immagini successive beneficiano del **caching di warm‑up**, riducendo ulteriori millisecondi per ogni esecuzione.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Ricorda di mantenere la stessa istanza di `OcrEngine`—creare un nuovo engine per file reinizializzerebbe il contesto GPU e penalizzerebbe le prestazioni.

---

## Conclusione

Ora hai un solido esempio **end‑to‑end di Aspose OCR** che mostra **come abilitare la GPU**, come **impostare l'ID del dispositivo GPU**, e come **leggere il testo dell'immagine in C#**. Attivando `UseGpu` e puntando al dispositivo corretto, trasformi un'operazione OCR lenta legata alla CPU in una pipeline ad alta velocità in grado di gestire grandi fatture, ricevute o qualsiasi documento scansionato.

Sentiti libero di sperimentare: prova diversi formati immagine, regola `GpuDeviceId` su sistemi multi‑GPU, o combina questo con altre librerie Aspose per la generazione di PDF. Il cielo è il limite una volta che la GPU è in gioco.

---

<img src="gpu-ocr.png" alt="come abilitare la gpu con Aspose OCR in C# – converti rapidamente immagine in testo semplice">

*Buon coding! Se incontri problemi, lascia un commento qui sotto o visita i forum ufficiali di Aspose per approfondimenti.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}