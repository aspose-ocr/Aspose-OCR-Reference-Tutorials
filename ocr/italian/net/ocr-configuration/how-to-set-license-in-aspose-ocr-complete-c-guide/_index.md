---
category: general
date: 2026-04-06
description: Come impostare la licenza in Aspose OCR usando C# – impara come incorporare
  una risorsa, ottenere la risorsa incorporata e caricare la licenza da un file o
  da uno stream in pochi semplici passaggi.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: it
og_description: Come impostare la licenza in Aspose OCR è spiegato passo passo. Scopri
  come incorporare la licenza, recuperarla e utilizzare un flusso di licenza per un'integrazione
  senza interruzioni.
og_title: Come impostare la licenza in Aspose OCR – Guida completa C#
tags:
- Aspose OCR
- C#
- .NET licensing
title: Come impostare la licenza in Aspose OCR – Guida completa C#
url: /it/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare la licenza in Aspose OCR – Guida completa in C#

Impostare la licenza in Aspose OCR è un ostacolo comune per gli sviluppatori. In questo tutorial vedremo passo passo come impostare la licenza, incorporarla come risorsa e caricarla da uno stream—così potrai iniziare a fare OCR senza la fastidiosa filigrana della modalità di prova.

Hai mai provato a eseguire un lavoro di OCR solo per vedere un banner “Versione di valutazione”? È il sintomo di una licenza mancante o applicata in modo errato. Alla fine di questa guida avrai un'istanza di Aspose OCR completamente licenziata, sia che tu mantenga il file `.lic` accanto ai binari sia che lo nasconda all'interno del tuo assembly.

## Cosa ti serve

- **Aspose.OCR per .NET** (ultimo pacchetto NuGet al momento della stesura – 23.10)
- Un **file di licenza Aspose OCR valido** (`Aspose.OCR.lic`)
- Visual Studio 2022 o qualsiasi IDE compatibile con C#
- Familiarità di base con l'incorporamento di risorse .NET (lo copriremo)

Non sono necessarie librerie di terze parti aggiuntive; tutto è contenuto nel pacchetto Aspose.

![Illustrazione su come impostare la licenza](image.png "Come impostare la licenza")

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

Prima di poter toccare qualsiasi codice di licenza, assicurati che la libreria sia referenziata:

```bash
dotnet add package Aspose.OCR
```

Oppure, tramite il gestore NuGet di Visual Studio, cerca **Aspose.OCR** e premi *Installa*. Questo scaricherà `Aspose.OCR.dll` e le sue dipendenze.

> **Consiglio professionale:** Target .NET 6 o versioni successive per usufruire delle API più recenti e di migliori prestazioni.

## Passo 2: Crea un oggetto License – Il nucleo del “Come impostare la licenza”

Aspose utilizza una semplice classe `License` per applicare la chiave commerciale. Istanziare questa classe è la prima riga di qualsiasi flusso di lavoro licenziato:

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

Perché è importante: l'istanza `License` legge il contenuto del file `.lic` e lo registra globalmente per l'AppDomain corrente. Una volta registrata, ogni `OcrEngine` che crei opererà in modalità completa.

## Passo 3: Applica la licenza da un file (Classico “Come caricare la licenza”)

Se preferisci tenere il file di licenza accanto all'eseguibile, chiama `SetLicense` passando il percorso del file:

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### Cose da tenere d'occhio

- **Percorsi assoluti vs relativi:** I percorsi relativi sono risolti rispetto alla *directory di lavoro* del processo, che spesso è la cartella `bin`.
- **Permessi del file:** L'account che esegue l'app deve avere accesso in lettura al file `.lic`.
- **Gestione delle eccezioni:** `SetLicense` lancia `FileNotFoundException` se il percorso è errato, quindi avvolgilo in un `try/catch` se vuoi una degradazione elegante.

## Passo 4: Come incorporare una risorsa – Inserire la licenza all'interno del tuo assembly

Incorporare la licenza elimina la necessità di distribuire un file separato. Ecco come **incorporare una risorsa** in un progetto .NET:

1. Aggiungi il file `.lic` al tuo progetto (ad esempio, in una cartella chiamata `Resources`).
2. Fai clic destro sul file → *Proprietà* → imposta **Build Action** su **Embedded Resource**.
3. Compila il progetto; la licenza diventa parte della DLL compilata.

Ora puoi recuperarla con la logica **get embedded resource**.

## Passo 5: Ottieni lo stream della risorsa incorporata

Il frammento seguente dimostra **get embedded resource** usando la reflection. Regola lo spazio dei nomi e il nome della risorsa per farli corrispondere alla struttura del tuo progetto:

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **Perché la reflection?** `Assembly.GetExecutingAssembly()` punta all'assembly in esecuzione, garantendo che il codice funzioni sia in un'app console, sia in un sito web, sia in una Azure Function.

## Passo 6: Usa lo stream della licenza – Il pattern “use license stream”

Ora che hai lo stream, **use license stream** per applicare la licenza senza toccare il file system:

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

Quando `SetLicense` riceve uno `Stream`, Aspose legge i byte direttamente, registra la licenza e dispone lo stream quando esci dal blocco `using`. Questo è il modo più pulito per tenere la licenza nascosta.

### Esempio completo funzionante

Mettendo tutto insieme, ecco un programma autonomo che dimostra tutti e tre gli approcci (file, risorsa incorporata e stream). Commenta le sezioni che non ti servono.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**Output previsto**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

Se la licenza non viene applicata, Aspose lancia una `LicenseException` o vedrai la filigrana di valutazione nei risultati OCR.

## Problemi comuni e come evitarli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| Il banner “Versione di valutazione” appare ancora | Licenza non caricata o percorso errato | Ricontrolla il percorso del file o il nome della risorsa incorporata. |
| `NullReferenceException` su `GetManifestResourceStream` | Nome della risorsa errato o Build Action non impostata su Embedded Resource | Verifica il nome qualificato dallo spazio dei nomi e imposta correttamente la Build Action. |
| La licenza funziona in locale ma fallisce dopo il deployment | Permessi di lettura mancanti sul server | Concedi all'identità del pool dell'app permessi di lettura sul file `.lic`, oppure incorpora la licenza per evitare problemi di file system. |
| Più oggetti `License` non hanno effetto | Hai chiamato `SetLicense` su un *diverso* oggetto dopo il primo | Mantieni una singola istanza di `License` per AppDomain; riutilizzala o chiama `SetLicense` una sola volta all'avvio. |

## Quando scegliere ciascun approccio

- **Basato su file** – Prototipazione rapida, facile da sostituire senza ricompilare.
- **Risorsa incorporata** – Ideale per distribuzioni desktop o librerie dove non vuoi che la licenza sia visibile.
- **Basato su stream** – Perfetto per ambienti cloud (Azure Functions, AWS Lambda) dove potresti recuperare la licenza da un vault sicuro e passarla direttamente.

## Prossimi passi – Approfondire la tua conoscenza delle licenze

Ora che hai padroneggiato **come impostare la licenza**, potresti voler esplorare:

- **How to embed resource** in soluzioni multi‑progetto più complesse.
- **Get embedded resource** da assembly satellite per scenari di localizzazione.
- **How to load license** dinamicamente da Azure Key Vault o AWS Secrets Manager.
- **Use license stream** insieme all’iniezione delle dipendenze per un codice di avvio più pulito.

Ognuno di questi argomenti si basa sui fondamenti trattati qui e ti aiuta a mantenere la tua strategia di licenza sicura e manutenibile.

---

### TL;DR

Ti abbiamo mostrato **come impostare la licenza** in Aspose OCR usando tre tecniche affidabili: caricamento da file, incorporamento del `.lic` come risorsa e applicazione tramite stream. Segui il codice, rispetta le insidie evidenziate, e il tuo motore OCR funzionerà a pieno regime—senza filigrane di prova, senza sorprese.

Buon coding, e che i tuoi risultati OCR siano cristallini!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}