---
category: general
date: 2026-03-21
description: Como fazer OCR em lote em C# de forma simples—aprenda a extrair texto
  de imagens, converter imagens em texto e salvar OCR como texto com configurações
  de idioma.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: pt
og_description: Como fazer OCR em lote em C# permite extrair texto de imagens, converter
  imagens em texto e salvar OCR como texto, definindo facilmente o idioma do OCR.
og_title: Como fazer OCR em lote em C# – Guia rápido
tags:
- OCR
- C#
- Aspose
title: Como fazer OCR em lote no C# – Extraia texto de imagens rapidamente
url: /pt/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote em C# – Extrair texto de imagens rapidamente

Já se perguntou **como fazer OCR em lote** quando você tem centenas de fotos em uma pasta? Você não está sozinho—desenvolvedores perguntam constantemente como extrair texto de imagens sem escrever um loop para cada arquivo. A boa notícia é que o Aspose.OCR oferece uma maneira limpa e pronta para paralelismo de **converter imagens em texto** em apenas algumas linhas de C#.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra como **salvar OCR como texto**, escolher o idioma correto e acelerar o processamento paralelo para ganhar velocidade. Ao final, você terá uma solução autônoma que pode ser inserida em qualquer projeto .NET.

## O que você precisará

- .NET 6 ou posterior (a API funciona com .NET Core e .NET Framework)
- Aspose.OCR for .NET (pacote NuGet `Aspose.OCR`)
- Uma pasta de imagens que você deseja processar (PNG, JPEG, TIFF, etc.)
- Um pouco de curiosidade sobre programação paralela (opcional, mas útil)

Nenhum serviço extra, nenhuma chave de nuvem—apenas código C# puro que roda localmente.

---

![how to batch OCR workflow](placeholder.png){alt="diagrama do fluxo de OCR em lote"}

## Etapa 1: Configurar o Projeto e Instalar o Aspose.OCR

Primeiro de tudo, crie um aplicativo de console (ou reutilize um existente) e adicione o pacote Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se você estiver usando o Visual Studio, clique com o botão direito no projeto → *Gerenciar Pacotes NuGet* → procure por *Aspose.OCR* e instale a versão estável mais recente.

Isso lhe dá acesso a `OcrBatchProcessor`, `OcrEngineSettings` e ao enum `Language`.

## Etapa 2: Definir Pastas de Entrada e Saída

O processador em lote precisa saber onde as imagens de origem estão e onde os arquivos de texto extraídos devem ser gravados. Mantenha os caminhos absolutos ou relativos à raiz do projeto—apenas certifique‑se de que as pastas existam antes de executar o código.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Por que isso importa:** Se a pasta de saída estiver ausente, o processador lançará uma exceção, interrompendo todo o lote. Criá‑la antecipadamente garante uma execução tranquila.

## Etapa 3: Configurar as Configurações de OCR (incluindo idioma)

É aqui que você **define o idioma do OCR** para todo o lote. O Aspose.OCR suporta dezenas de idiomas; o inglês é o padrão, mas você pode mudar para francês, espanhol, etc., alterando o valor do enum `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Se algum dia precisar processar idiomas diferentes por imagem, você pode sobrescrever essa configuração por arquivo—mais detalhes adiante.

## Etapa 4: Construir o Objeto `OcrBatchProcessor`

Agora juntamos tudo. O `OcrBatchProcessor` permite especificar a pasta de entrada, pasta de saída, formato de saída, opções paralelas e as configurações compartilhadas que acabamos de criar.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Por que paralelismo?** Quando você tem dezenas ou centenas de imagens, processá‑las uma a uma pode ser dolorosamente lento. Definir `MaxDegreeOfParallelism` para 4 permite que o runtime use quatro núcleos de CPU simultaneamente, reduzindo drasticamente o tempo total em uma estação de trabalho típica.

## Etapa 5: Executar a Operação em Lote

Com o processador configurado, a execução é uma única chamada de método. A biblioteca cuida da enumeração de arquivos, OCR e gravação dos resultados automaticamente.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Quando o console imprimir *“Batch OCR completed.”* você encontrará um arquivo `.txt` ao lado de cada imagem original dentro de `BatchResults`. Cada arquivo de texto contém os caracteres brutos extraídos da imagem de origem—exatamente o que você precisa para **extrair texto de imagens** para processamento posterior.

### Saída Esperada

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Abra qualquer um desses arquivos e você verá a representação em texto puro do conteúdo da imagem.

## Etapa 6: Verificar os Resultados (Opcional)

É uma boa prática conferir alguns arquivos para garantir que o OCR funcionou como esperado. Uma maneira rápida é ler a primeira linha de cada arquivo gerado e imprimi‑la no console:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Se notar caracteres estranhos, considere mudar a configuração `Language` ou ajustar a qualidade da imagem (por exemplo, aumentar DPI, converter para escala de cinza).

## Variações Avançadas e Casos Limite

### 1. Substituições de Idioma por Arquivo
Às vezes um lote contém documentos multilíngues. Você pode inspecionar o nome de cada imagem e atribuir um idioma dinamicamente:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Diferentes Formatos de Saída
Se precisar de PDFs pesquisáveis em vez de texto simples, altere `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Isso **converterá imagens em texto** dentro de um contêiner PDF, preservando o layout original.

### 3. Manipulação de Imagens Grandes
Imagens de altíssima resolução podem consumir muita memória. Para manter o processo leve, habilite o down‑sampling da imagem:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Registro de Erros
O processador lança exceções para arquivos ilegíveis. Envolva `Execute` em um try/catch e registre os nomes de arquivos problemáticos:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto para copiar e colar:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Salve isso como `Program.cs`, compile o projeto e execute `dotnet run`. Você verá a saída no console confirmando a conclusão, seguida de uma breve pré‑visualização do texto extraído.

---

## Conclusão

Acabamos de cobrir **como fazer OCR em lote** em C# usando Aspose.OCR, mostrando como **extrair texto de imagens**, **converter imagens em texto** e **salvar OCR como texto** enquanto **define o idioma do OCR** para corresponder ao seu conteúdo. O exemplo está totalmente funcional, inclui processamento paralelo para velocidade e oferece pontos de extensão para cenários avançados como substituições de idioma por arquivo ou saída em PDF.

Pronto para o próximo passo? Experimente trocar `OcrOutputFormat.PlainText` por `SearchablePdf` e veja como é fácil gerar PDFs pesquisáveis. Ou experimente valores diferentes de `MaxDegreeOfParallelism` para extrair cada milissegundo em uma máquina multicore.

Se encontrar algum problema, verifique novamente os caminhos das pastas, assegure‑se de que as imagens são legíveis e confirme se o enum de idioma corresponde ao texto nas suas fotos. Boa codificação, e que seus lotes de OCR sejam rápidos e precisos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}