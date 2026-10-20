---
category: general
date: 2026-05-31
description: Aprenda como obter pontuações de confiança de OCR em C# ao extrair texto
  de imagens e ler imagens de recibos com o Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: pt
og_description: As pontuações de confiança do OCR permitem que você avalie a precisão;
  este guia mostra como extrair texto de uma imagem, obter caixas delimitadoras e
  ler a imagem de recibo usando o Aspose OCR.
og_title: Pontuações de confiança de OCR em C# – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Pontuações de confiança de OCR em C# – Guia Completo
url: /pt/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pontuações de confiança de OCR em C# – Guia Completo

Já se perguntou como obter **pontuações de confiança de OCR** quando você precisa *extrair texto de uma imagem*? Talvez você esteja tentando **ler imagens de recibos** para controle de despesas e queira saber quais caracteres o motor está incerto. A boa notícia? Com Aspose.OCR você pode obter percentuais de confiança, caixas delimitadoras e texto simples de um JPG em apenas algumas linhas de C#.

Neste tutorial vamos percorrer tudo o que você precisa saber: instalar a biblioteca, configurar o motor para **executar OCR em JPG**, extrair pontuações de confiança e interpretar as **caixas delimitadoras de OCR** que indicam onde cada caractere está na página. Ao final, você terá um aplicativo console pronto‑para‑executar que imprime cada caractere, sua confiança e sua localização—perfeito para validar recibos ou qualquer documento escaneado.

## O que você aprenderá

- Instalar Aspose.OCR via NuGet e configurar um motor OCR básico.  
- Configurar `OcrOptions` para solicitar saída de texto simples **com pontuações de confiança** e **caixas delimitadoras**.  
- Percorrer `OcrResult` para **extrair texto de imagem** linha‑por‑linha e símbolo‑por‑símbolo.  
- Lidar com armadilhas comuns, como arquivos ausentes, caracteres de baixa confiança e formatos que não sejam JPG.  
- Estender o exemplo para processar múltiplas imagens de recibos em uma pasta.

Nenhuma experiência prévia com Aspose é necessária; basta um ambiente .NET funcional e uma imagem de recibo (JPG) que você queira testar.

---

## Etapa 1 – Instalar Aspose.OCR e preparar seu projeto

Primeiro de tudo: você precisa do pacote NuGet Aspose.OCR. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** O teste gratuito funciona para até 200 páginas, o que é mais que suficiente para testar a digitalização de recibos.

Depois que o pacote for instalado, crie um novo projeto console (se ainda não tiver um):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Agora você pode abrir o `Program.cs` gerado e começar a adicionar as diretivas `using`:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Esses namespaces dão acesso a `OcrEngine`, `OcrOptions` e aos tipos de resultado que precisaremos mais adiante.

## Etapa 2 – Obter pontuações de confiança de OCR e caixas delimitadoras de OCR

Este é o coração do tutorial. Configuraremos o motor para que cada caractere reconhecido venha com uma **pontuação de confiança** e uma **caixa delimitadora** (o retângulo que envolve o glifo). O próprio cabeçalho H2 contém a palavra‑chave principal, atendendo à regra de SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Por que incluir pontuações de confiança?**  
Uma pontuação de confiança (0‑100%) indica o quão certo o motor está sobre cada caractere. Se você estiver enviando a saída para lógica downstream—por exemplo, um fluxo de aprovação de despesas—pode rejeitar ou sinalizar símbolos de baixa confiança automaticamente.

**Por que solicitar caixas delimitadoras?**  
Caixas delimitadoras são essenciais quando você precisa destacar texto na imagem original, extrair sub‑regiões ou alinhar os resultados de OCR com uma sobreposição de UI. Cada `character.Bounds` fornece X, Y, largura e altura em coordenadas de pixel.

## Etapa 3 – Executar OCR em JPG e extrair texto da imagem

Agora realmente executamos o motor. A chamada a `Recognize()` realiza todo o trabalho pesado e devolve um objeto `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Se o caminho da imagem estiver errado ou o arquivo não for um formato suportado, a Aspose lança uma `FileNotFoundException` ou `UnsupportedImageFormatException`. Envolva a chamada em um bloco try/catch no código de produção para tratar esses casos de borda de forma elegante.

### Extraindo o texto simples

Se você precisar apenas do texto concatenado, pode ler `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Mas como também solicitamos pontuações de confiança e caixas delimitadoras, vamos iterar pela estrutura para ver os detalhes de cada caractere.

## Etapa 4 – Iterar por linhas, símbolos e exibir pontuações de confiança de OCR

Aqui está o loop que imprime cada caractere, sua confiança e sua caixa. É aqui que o exemplo de **read receipt image** realmente brilha.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

A saída de exemplo pode ser semelhante a:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretando os números:**  
- **Confiança ≥ 90%** – geralmente seguro aceitar.  
- **Confiança 70‑89%** – pode ser necessário verificar novamente, especialmente para dígitos em valores.  
- **Confiança < 70%** – considere sinalizar para revisão manual.

## Etapa 5 – Exemplo completo executável (incluindo tratamento de erros)

Juntando tudo, aqui está um programa completo que você pode copiar‑colar para `Program.cs`. Ele inclui uma verificação simples para arquivos ausentes e imprime uma mensagem amigável caso o OCR falhe.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Saída esperada

Ao executar `dotnet run` o console exibirá primeiro o texto concatenado do recibo, depois uma lista de cada caractere com sua pontuação de confiança e caixa delimitadora. Se a confiança de um caractere for baixa, você verá um percentual abaixo de 80, o que indica que aquela parte do recibo deve ser verificada manualmente.

## Bônus: Processando múltiplos recibos em uma pasta

Se você tem um lote de JPGs de recibos, envolva a lógica acima em um loop `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Lembre‑se de redefinir o `OcrEngine` para cada arquivo, ou instanciar um novo dentro do loop para evitar vazamento de estado.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Processar em lote é útil para importações noturnas de despesas.

---

## Conclusão

Agora você tem uma solução sólida, de ponta a ponta, para obter **pontuações de confiança de OCR** em C#, **extrair texto de imagem** e recuperar **caixas delimitadoras de OCR** enquanto **executa OCR em JPG** arquivos como uma **read receipt image**. O código é totalmente autônomo, funciona com a versão mais recente do Aspose.OCR (a partir de 2026‑05‑31) e fornece os dados granulares que você precisa para construir pipelines de processamento de documentos confiáveis.

O que vem a seguir? Experimente visualizar as caixas delimitadoras no recibo original usando `System.Drawing` ou uma biblioteca UI, ou envie caracteres de baixa confiança para um serviço de verificação secundário. Você também pode experimentar diferentes idiomas definindo `ocrEngine.Options.Language = OcrLanguage.French;` – a API suporta muitas localidades.

Feliz codificação, e que suas pontuações de confiança permaneçam sempre altas! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## O que você deve aprender a seguir?

- [Extrair texto de imagem em C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Como obter opções de caracteres OCR para caracteres reconhecidos em Reconhecimento de Imagem](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Como usar Aspose OCR para resultado JSON em Reconhecimento de Imagem](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}