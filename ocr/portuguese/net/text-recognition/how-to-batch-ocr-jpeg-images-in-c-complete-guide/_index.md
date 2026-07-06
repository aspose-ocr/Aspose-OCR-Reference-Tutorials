---
category: general
date: 2026-02-22
description: Como fazer OCR em lote de imagens JPEG em C# com Aspose.OCR. Aprenda
  a extrair texto de JPG, converter JPG para TXT e processar imagens em lote de forma
  eficiente.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: pt
og_description: Como fazer OCR em lote de imagens JPEG em C# usando Aspose.OCR. Este
  tutorial mostra como extrair texto de JPG, converter JPG para TXT e processar imagens
  em lote em minutos.
og_title: Como fazer OCR em lote de imagens JPEG em C# – Guia completo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Como fazer OCR em lote de imagens JPEG em C# – Guia completo
url: /pt/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote de imagens JPEG em C# – Guia Completo

Já se perguntou **como fazer OCR em lote** de uma pasta cheia de imagens sem precisar escrever um programa separado para cada arquivo? Neste guia vamos mostrar exatamente **como fazer OCR em lote** de arquivos JPEG usando Aspose.OCR, para que você possa **extrair texto de jpg** e **converter jpg para txt** com apenas algumas linhas de código.  

Se você já ficou olhando para um diretório de notas fiscais escaneadas e pensou: “Tem que existir um jeito mais rápido”, está no lugar certo. Vamos percorrer cada passo, explicar por que cada parte importa e ainda dar algumas dicas de especialista para lidar com lotes grandes.

## O que você vai construir

Ao final deste tutorial você terá um pequeno aplicativo console que:

* Varre um diretório especificado em busca de arquivos `*.jpg`.  
* Envia cada imagem para o motor Aspose OCR (acelerado por GPU se você tiver uma placa compatível).  
* Grava o texto reconhecido em um arquivo `.txt` que fica ao lado da imagem original.  

Sem serviços externos, sem copiar‑e‑colar manual — apenas C# puro e uma biblioteca OCR confiável.

### Pré‑requisitos

* .NET 6.0 ou superior (o código também funciona no .NET Framework 4.8).  
* Visual Studio 2022 ou qualquer editor que suporte C#.  
* Um pacote NuGet Aspose.OCR (a versão de avaliação gratuita serve para testes).  

Se estiver faltando algum desses, pause agora e instale; o restante do guia assume que tudo já está pronto.

![Exemplo de OCR em lote](/images/how-to-batch-ocr.png "diagrama de OCR em lote")

## Etapa 1: Instalar o pacote NuGet Aspose.OCR

Primeiro passo — seu projeto precisa da biblioteca OCR. Abra um terminal na pasta da solução e execute:

```bash
dotnet add package Aspose.OCR
```

Ou use a UI do NuGet Package Manager no Visual Studio. Isso traz tudo que você precisa, incluindo os binários habilitados para GPU caso sua máquina os suporte.

> **Dica de especialista:** Se você pretende rodar isso em um servidor sem GPU, defina `UseGpu = false` mais adiante; o motor voltará automaticamente para a CPU.

## Etapa 2: Configurar o motor OCR

Criar e configurar o `OcrEngine` é onde a mágica começa. Você informará ao motor qual idioma esperar, se deve usar a GPU e qual formato a saída deve ter.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Por que isso importa:** Definir `Language` melhora a precisão porque o motor pode restringir o conjunto de caracteres. Habilitar `UseGpu` pode reduzir o tempo de processamento pela metade em uma placa gráfica moderna, o que é uma grande vantagem ao fazer **processamento em lote de imagens**.

## Etapa 3: Reconhecer todos os arquivos JPEG em uma pasta

Agora deixamos a Aspose fazer o trabalho pesado. O método estático `BatchProcessor.RecognizeFolder` percorre o diretório, executa OCR em cada arquivo correspondente e devolve uma coleção de resultados.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Tratamento de casos extremos:** Se a pasta contiver subpastas, você pode acrescentar a sobrecarga `SearchOption.AllDirectories` (ou fazer a recursão manualmente) para garantir que nenhum arquivo seja perdido.

## Etapa 4: Gravar cada resultado em um arquivo `.txt` correspondente

Os objetos `OcrResult` contêm o caminho original do arquivo e o texto reconhecido. Percorra‑os, altere a extensão e escreva a saída.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

É isso — cada JPEG agora tem um arquivo de texto irmão que você pode alimentar em processos posteriores, índices de busca ou simplesmente arquivar.

## Etapa 5: Executar a aplicação e verificar a saída

Compile e execute o programa:

```bash
dotnet run
```

Assumindo que a pasta contenha `invoice1.jpg` e `receipt2.jpg`, você deverá ver `invoice1.txt` e `receipt2.txt` aparecer ao lado deles. Abra qualquer um dos arquivos `.txt`; você encontrará a saída bruta do OCR, por exemplo:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Se o texto aparecer confuso, verifique se as imagens de origem têm alto contraste e se a propriedade `Language` corresponde ao idioma do documento.

## Etapa 6: Ajustes avançados (opcional)

### a) Lidando com digitalizações de baixa qualidade

Às vezes os JPEGs são ruidosos. Você pode pré‑processar as imagens com Aspose.Imaging ou qualquer outra biblioteca:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Paralelizando o lote

Se você tem muitos arquivos e uma CPU multi‑core, envolva o loop em `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Só tenha em mente que o motor Aspose OCR não é thread‑safe; será necessário uma instância separada de `OcrEngine` por thread ou usar uma fila concorrente.

### c) Registro de logs e tratamento de erros

Uma solução robusta registra falhas para que você possa tentar novamente depois:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Exemplo completo em funcionamento

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em um novo Console App:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Execute, observe a saída no console e depois abra alguns arquivos `.txt` para confirmar que a etapa **extrair texto de jpg** foi bem‑sucedida.  

---

## Conclusão

Acabamos de cobrir **como fazer OCR em lote** de uma coleção de imagens JPEG em C# usando Aspose.OCR, transformando cada foto em um arquivo `.txt` pesquisável. A solução é compacta, consciente de GPU e fácil de estender para tratamento de erros, pré‑processamento de imagens ou execução paralela.  

Se você está pronto para avançar, considere os próximos passos:

* **Processar em lote** imagens de outros formatos (`*.png`, `*.tif`) ajustando o `searchPattern`.  
* Combinar a saída com um motor de busca full‑text como Lucene.NET para consulta instantânea de documentos.  
* Explorar os recursos de conversão para PDF da Aspose e gerar PDFs pesquisáveis diretamente a partir dos resultados de OCR.  

Sinta‑se à vontade para experimentar — troque o idioma, desative a GPU ou direcione o texto para um banco de dados. O padrão central permanece o mesmo, e agora você tem uma base sólida para construir.

Bom código, e que seus pipelines de OCR sejam sempre rápidos e precisos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}