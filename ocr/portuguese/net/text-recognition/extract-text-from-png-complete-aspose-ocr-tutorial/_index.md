---
category: general
date: 2026-01-09
description: Extraia texto de PNG rapidamente com Aspose OCR. Aprenda como ler texto
  de imagens, melhorar a precisão do OCR e obter resultados limpos em C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: pt
og_description: Extraia texto de PNG rapidamente com Aspose OCR. Aprenda como ler
  texto de imagens, melhorar a precisão do OCR e obter resultados limpos em C#.
og_title: Extrair texto de PNG – Tutorial completo de OCR da Aspose
tags:
- Aspose OCR
- C#
- Image Processing
title: Extrair texto de PNG – Tutorial completo de OCR da Aspose
url: /pt/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de PNG – Tutorial Completo de Aspose OCR

Já precisou **extrair texto de PNG** e os resultados estavam cheios de caracteres estranhos? Você não está sozinho. Em muitos projetos do mundo real – notas fiscais, recibos ou formulários escaneados – a qualidade da saída do OCR pode fazer ou quebrar pipelines de automação.  

Neste guia mostraremos um método **passo a passo** para ler texto de imagens usando Aspose OCR, aplicar um dicionário personalizado para **melhorar a precisão do OCR**, limpar o ruído e, finalmente, imprimir uma string organizada. Ao final, você terá um aplicativo console C# pronto‑para‑executar que extrai texto de imagens PNG de forma confiável.

> **O que você levará consigo**  
> * Um exemplo de código completo e executável.  
> * Entendimento de por que um dicionário personalizado é importante.  
> * Dicas para lidar com casos extremos, como digitalizações de baixo contraste.  

## Pré-requisitos

- .NET 6 SDK ou superior (o código tem como alvo .NET 6, mas .NET 5 também funciona).  
- Visual Studio 2022 ou qualquer editor de sua preferência.  
- Uma imagem **PNG** que você deseja processar – por exemplo `invoice.png`.  
- O pacote **Aspose.OCR** do NuGet (`dotnet add package Aspose.OCR`).  

Nenhum arquivo de configuração extra é necessário; tudo vive em um único arquivo `.cs`.

## Etapa 1 – Instalar e Referenciar Aspose OCR

Primeiro, traga a biblioteca para o seu projeto. Abra um terminal na pasta da solução e execute:

```bash
dotnet add package Aspose.OCR
```

Essa única linha obtém a versão estável mais recente (em Jan 2026, versão 23.9). O pacote inclui a classe `OcrEngine` que usaremos ao longo do tutorial.

## Etapa 2 – Inicializar o Motor OCR

Criar uma instância de `OcrEngine` é a base. Pense nisso como ligar um scanner pronto para interpretar pixels.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Dica profissional:** Se você pretende processar muitas imagens em um loop, reutilize a mesma instância de `OcrEngine`. Ela faz cache de recursos internos e acelera chamadas subsequentes.

## Etapa 3 – Aumentar a Precisão com um Dicionário Personalizado

O OCR padrão é bom, mas pode tropeçar em palavras específicas de domínio como “Aspose”, “OCR” ou “SDK”. Adicionar esses termos a um **dicionário personalizado** informa ao motor que essas cadeias são válidas, reduzindo erros de reconhecimento.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Por que um dicionário personalizado ajuda

- **Modelos estatísticos** por trás do OCR dão peso pesado a padrões de linguagem comuns. Palavras incomuns recebem baixa probabilidade e podem ser substituídas por caracteres visualmente semelhantes.  
- Ao listá‑las explicitamente, você sobrescreve a adivinhação do modelo.  
- É especialmente útil para **ler texto de imagem** que contém códigos de produto, abreviações ou nomes de marca.

## Etapa 4 – Reconhecer Texto do Arquivo PNG

Agora fornecemos ao motor o caminho da imagem. O método `RecognizeImage` retorna uma string bruta que ainda contém tokens desconhecidos (ex.: “#@!”) que o motor não conseguiu mapear.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Caso especial:** Se o arquivo não for encontrado, `RecognizeImage` lança uma `FileNotFoundException`. Envolva a chamada em um bloco try‑catch para código de produção.

## Etapa 5 – Limpar o Resultado com `CleanText`

Aspose OCR inclui um helper que remove caracteres marcados como “desconhecidos”. Esta etapa é crucial para projetos de **extração de texto de imagem** onde analisadores posteriores esperam apenas caracteres alfanuméricos e pontuação básica.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

O método `CleanText` também normaliza quebras de linha, tornando a saída segura para armazenar em bancos de dados ou passar a outros serviços.

## Etapa 6 – Exibir o Texto Limpo

Por fim, exiba ou armazene o resultado. Em um aplicativo console, `Console.WriteLine` faz o trabalho.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Ao executar o programa, você deverá ver um bloco de texto organizado que reflete o conteúdo de `invoice.png`. Se a imagem contiver a palavra “Aspose”, o dicionário personalizado garante que ela apareça corretamente em vez de algo como “A5p0se”.

## Exemplo Completo Funcional

Juntando tudo, aqui está o `Program.cs` completo que você pode copiar‑colar em um novo projeto console:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Saída esperada** (supondo que o PNG contenha uma nota fiscal simples):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Se aparecerem símbolos estranhos, verifique a qualidade da imagem ou amplie o dicionário personalizado com mais termos.

## Bônus: Lidando com Digitalizações de Baixa Qualidade

Às vezes os PNGs são escaneados a 72 dpi ou têm artefatos de compressão fortes. Aqui vão algumas dicas rápidas para **melhorar a precisão do OCR** sem sair do C#:

1. **Pré‑processar a imagem** com uma biblioteca como `SixLabors.ImageSharp` – aumente o contraste, converta para escala de cinza ou aplique um leve desfoque para reduzir ruído.  
2. **Definir a propriedade `Resolution`** no `OcrEngine` (ex.: `ocrEngine.Resolution = 300;`) para informar ao motor que a imagem deve ser tratada como de alta resolução.  
3. **Habilitar pacotes de idioma** se você estiver lidando com texto não‑inglês (`ocrEngine.Language = Language.English;`).

As três abordagens podem ser adicionadas antes da chamada `RecognizeImage`.

## Perguntas Frequentes

- **Isso funciona com outros formatos de imagem?**  
  Sim. `RecognizeImage` aceita JPEG, BMP, TIFF e até PDF (como contêiner de imagem). Os mesmos passos se aplicam.

- **Posso extrair texto de vários PNGs em uma pasta?**  
  Absolutamente. Envolva a lógica principal em um `foreach (var file in Directory.GetFiles(folder, "*.png"))` e armazene cada resultado em uma lista ou escreva em arquivos separados.

- **E se eu precisar das coordenadas do texto?**  
  Aspose OCR também fornece objetos `OcrResult` que incluem caixas delimitadoras. Use `ocrEngine.RecognizeImageToResult(imagePath)` para esse cenário avançado.

## Conclusão

Percorremos uma solução **completa, ponta a ponta** para **extrair texto de PNG** usando Aspose OCR. Ao inicializar o motor, alimentá‑lo com um **dicionário personalizado**, limpar a saída bruta e tratar alguns obstáculos comuns, você pode ler texto de imagens de forma confiável e **melhorar a precisão do OCR** em suas próprias aplicações C#.

Pronto para o próximo passo? Experimente trocar o PNG por um recibo escaneado, adicione mais palavras específicas ao dicionário ou integre a saída a um banco de dados para processamento automático de notas fiscais. O céu é o limite quando você combina Aspose OCR com o rico ecossistema .NET.

Feliz codificação, e que seu OCR esteja sempre preciso! 

![Exemplo de extração de texto de png](/images/extract-text-from-png.png "extract text from png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}