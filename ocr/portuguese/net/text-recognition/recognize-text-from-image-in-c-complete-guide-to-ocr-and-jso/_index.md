---
category: general
date: 2026-01-10
description: Aprenda a reconhecer texto a partir de imagens, extrair as coordenadas
  do texto e converter recibos para JSON usando o Aspose OCR em C#. Tutorial passo
  a passo.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: pt
og_description: reconhecer texto de imagem em C# usando Aspose OCR. Este guia mostra
  como extrair texto, obter coordenadas e converter o recibo para JSON.
og_title: Reconhecer texto a partir de imagem – Tutorial completo de OCR em C#
tags:
- OCR
- C#
- Aspose
title: Reconhecer texto de imagem em C# – Guia completo de OCR e JSON
url: /pt/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto a partir de imagem – Tutorial Completo de OCR em C#

Já precisou reconhecer texto a partir de uma imagem, mas não sabia qual biblioteca escolher? Você não está sozinho. Em muitos aplicativos reais—controladores de despesas, scanners de recibos ou arquivadores de documentos—extrair texto de forma confiável é o primeiro obstáculo.  

Neste tutorial vamos percorrer **como extrair texto**, obter suas caixas delimitadoras e, finalmente, **converter recibo para JSON** usando Aspose.OCR para .NET. Ao final, você terá um projeto C# autônomo que recebe uma foto de um recibo e gera um arquivo JSON organizado com pontuações de confiança e coordenadas.

## O que você vai precisar

Antes de mergulharmos, certifique‑se de que tem o seguinte na sua máquina:

- **.NET 6.0 SDK** (ou qualquer versão posterior). Frameworks mais antigos também funcionam, mas o .NET 6 é o ponto ideal para bibliotecas modernas.
- **Visual Studio 2022** ou VS Code com a extensão C#.
- **Aspose.OCR for .NET** pacote NuGet (`Aspose.OCR` e `Aspose.OCR.Output`). Você pode instalá‑lo via Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Uma imagem de exemplo de recibo (por exemplo, `receipt.jpg`) colocada em uma pasta que será referenciada mais adiante.

É só isso—sem SDKs extras, sem binários nativos, apenas código gerenciado puro.

## Etapa 1: Criar um Novo Projeto de Console

Primeiro de tudo, crie um aplicativo de console. É a maneira mais rápida de testar OCR sem sobrecarga de UI.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Dica:** Mantenha a pasta do projeto organizada; crie uma sub‑pasta chamada `Resources` e coloque `receipt.jpg` lá. Isso facilita o manuseio de caminhos.

## Etapa 2: Carregar a Imagem do Recibo

Agora vamos realmente **reconhecer texto a partir de imagem**. O primeiro passo é apontar o motor OCR para o arquivo.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Por que envolvemos o carregamento em uma simples verificação de existência? Porque em produção você costuma lidar com uploads de usuários que podem estar ausentes ou corrompidos. Detectar o problema cedo evita exceções enigmáticas mais tarde.

## Etapa 3: Executar OCR – **reconhecer texto a partir de imagem**

Com a imagem na memória, pedimos ao Aspose para **reconhecer texto a partir de imagem**. Esta operação é síncrona e devolve um conjunto rico de resultados.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Nos bastidores, o Aspose executa uma rede neural treinada com milhões de caracteres. O motor preenche `ocrEngine.Text`, `ocrEngine.RecognitionResult` e uma coleção de objetos `OcrRegion` que contêm coordenadas. Isso é exatamente o que precisamos para a próxima etapa.

## Etapa 4: **Como extrair texto** – Obtendo a string bruta

Se você se importa apenas com o texto puro (talvez para uma busca rápida), pode obtê‑lo diretamente do motor:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Você notará quebras de linha onde o OCR detectou limites de parágrafo. Em muitos cenários de escaneamento de recibos, a string bruta basta para extrair totais, datas ou nomes de fornecedores usando expressões regulares simples.

## Etapa 5: **extrair coordenadas de texto** – Caixas delimitadoras para cada palavra

Frequentemente você precisa saber *onde* na imagem determinado trecho de texto está—por exemplo, para destacar o valor total em uma UI. O Aspose fornece isso via objetos `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Observe que estamos iterando sobre **extrair coordenadas de texto** para cada segmento reconhecido. As coordenadas são relativas à imagem original, de modo que você pode sobrepô‑las em um canvas gráfico ou no elemento HTML `<canvas>`.

## Etapa 6: **converter recibo para JSON** – Salvando resultados detalhados

Agora vem a parte que une tudo: queremos uma estrutura legível por máquina que inclua o texto, as pontuações de confiança e as caixas delimitadoras. O Aspose vem com `JsonSaveOptions` que tornam isso muito simples.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

O arquivo resultante tem a seguinte aparência (abreviado para brevidade):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Você agora tem um artefato **converter recibo para JSON** que pode ser alimentado a serviços downstream—pense em APIs de relatórios de despesas, pipelines de análise ou até mesmo uma UI simples que desenha retângulos ao redor de cada palavra.

## Exemplo Completo Funcional

Juntando todas as peças, aqui está o `Program.cs` completo que você pode copiar‑colar no seu projeto:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Execute o programa (`dotnet run`) e observe a saída no console. Abra `Resources/receipt.json` para verificar a estrutura.

## Perguntas Frequentes & Casos de Borda

- **E se a imagem estiver borrada?**  
  O Aspose OCR funciona melhor com 300 dpi ou mais. Se você obtiver pontuações de confiança baixas, considere aplicar um filtro de nitidez antes de enviar a imagem ao motor.

- **Posso reconhecer múltiplos idiomas?**  
  Sim. Defina `ocrEngine.Language = Language.English | Language.Spanish;` antes de chamar `Recognize()`.

- **Como limitar a saída apenas a números (por exemplo, totais)?**  
  Depois de obter o texto puro, execute uma regex como `\d+\.\d{2}` em `ocrEngine.Text`. Como já temos as coordenadas, você pode mapear a string correspondida de volta à sua região para realce visual.

- **O formato JSON é personalizável?**  
  A classe `JsonSaveOptions` expõe algumas flags. Se precisar de um esquema completamente customizado, pode iterar sobre `ocrEngine.RecognitionResult.Regions` e serializar os objetos manualmente com `System.Text.Json`.

## Conclusão

Acabamos de demonstrar como **reconhecer texto a partir de imagem** em C# usando Aspose.OCR, **como extrair texto**, obter **extrair coordenadas de texto**, e finalmente **converter recibo para JSON**. Todo o fluxo vive em um único aplicativo de console fácil de executar, tornando‑o perfeito para protótipos ou como bloco de construção em sistemas maiores.

Próximos passos? Experimente alimentar o JSON em um front‑end que desenha as caixas delimitadoras, ou conecte a saída a um serviço de relatório de despesas. Você também pode testar diferentes formatos de imagem (PNG, TIFF) ou processar em lote uma pasta de recibos.

Tem mais perguntas sobre OCR, Aspose ou manipulação de JSON? Deixe um comentário abaixo, e feliz codificação! 

![Exemplo de imagem de recibo para reconhecer texto a partir de imagem](receipt.jpg "Exemplo de imagem de recibo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}