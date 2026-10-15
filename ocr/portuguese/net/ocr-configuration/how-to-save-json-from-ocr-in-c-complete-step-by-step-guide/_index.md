---
category: general
date: 2026-03-02
description: Aprenda como salvar JSON ao extrair texto de imagem usando Aspose OCR.
  Inclui código para gravar arquivo JSON, dicas para carregar imagem bitmap e exemplo
  completo em C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: pt
og_description: Descubra como salvar JSON ao extrair texto de imagens com o Aspose
  OCR. Código C# completo, etapas para gravar o arquivo JSON e dicas práticas.
og_title: Como salvar JSON a partir de OCR em C# – Tutorial completo de programação
tags:
- C#
- OCR
- Aspose
- JSON
title: Como salvar JSON de OCR em C# – Guia completo passo a passo
url: /pt/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Salvar JSON a partir de OCR em C# – Guia Completo Passo a Passo

Já se perguntou **como salvar JSON** que contém o texto que você acabou de extrair de uma imagem? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando precisam *extrair texto de imagem* e depois persistir essa informação como um arquivo JSON bem formatado. A boa notícia? A solução é bastante direta assim que você tem as peças certas em mãos.

Neste tutorial vamos percorrer um cenário real: usar Aspose.OCR para **extrair texto de uma imagem**, depois **escrever o arquivo JSON** e, por fim, **salvar o JSON** no disco. No caminho, também mostraremos como **carregar objetos de imagem bitmap** corretamente e abordaremos alguns casos de borda que você pode encontrar. Ao final, você terá um aplicativo console em C# autônomo que faz tudo, desde carregar a foto até gerar um documento JSON pronto para uso.

## O que você vai precisar

- .NET 6.0 ou superior (o código funciona também com .NET Core e .NET Framework)  
- Aspose.OCR para .NET (você pode obter o pacote NuGet de avaliação gratuito)  
- Uma imagem PNG ou JPG de exemplo que contenha texto em inglês  
- Visual Studio, VS Code ou qualquer IDE compatível com C#

Nenhuma biblioteca adicional é necessária — apenas o namespace padrão `System.Drawing` para manipulação de bitmap e `System.Text.Json` para serialização.

---

## Etapa 1 – Carregar a Imagem Bitmap (a parte “load bitmap image”)

Antes que qualquer OCR possa acontecer, você deve colocar a imagem na memória como um `Bitmap`. Pense nisso como abrir um livro antes de começar a ler suas páginas.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Dica profissional:** Se a imagem for grande, considere redimensioná‑la primeiro para melhorar o desempenho. O motor OCR funciona mais rápido em imagens com menos de 2 MB.

---

## Etapa 2 – Configurar o Motor Aspose OCR

Agora que o bitmap está pronto, precisamos de um `OcrEngine`. Esse objeto sabe como **extrair texto de imagem** e, opcionalmente, nos fornece dados de geometria como caixas delimitadoras.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Por que habilitar `ExportBoundingBoxes`? Se você precisar destacar palavras em uma UI, essas coordenadas são valiosas. Se não precisar delas, pode definir a flag como `false` e o JSON ficará um pouco mais enxuto.

---

## Etapa 3 – Executar OCR e Obter um Resultado Estruturado

Com o motor configurado, o próximo passo é a operação real de **como extrair texto**. O método `RecognizeToOcrResult` devolve um objeto rico que contém o texto reconhecido, pontuações de confiança e, opcionalmente, dados de layout.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

A variável `ocrResult` agora contém tudo que você precisa. Se você inspecioná‑la no depurador, verá uma hierarquia de objetos `Page`, `Paragraph`, `Line` e `Word`, cada um com sua própria propriedade `Text`.

---

## Etapa 4 – Serializar o Resultado para uma String JSON Formatada

É aqui que a mágica de **como salvar json** realmente começa. Usaremos `System.Text.Json` porque ele já vem incluído, é rápido e suporta impressão formatada (pretty printing) nativamente.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Se precisar de uma convenção de nomenclatura diferente (por exemplo, camelCase), basta adicionar `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` às opções.

---

## Etapa 5 – Gravar o JSON no Disco (a etapa “write json file”)

Finalmente, nós realmente **escrevemos o arquivo JSON** no sistema de arquivos. Esta é a resposta concreta para **como salvar json** em um ambiente C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Depois que esta linha for executada, você encontrará um `sample-page.json` bem identado ao lado da sua imagem original. Abra‑o com qualquer editor de texto ou envie‑o para outro serviço — seus dados de OCR agora são portáteis.

---

## Etapa 6 – Verificar a Saída (O que você deve ver?)

Executar o programa deve imprimir uma breve confirmação no console:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Abra o JSON gerado e você verá algo como:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Se a flag `ExportBoundingBoxes` estiver true, cada palavra também conterá coordenadas `Rectangle`. Isso é útil para trabalhos de UI posteriores.

---

## Perguntas Frequentes & Casos de Borda

### E se o caminho da imagem for inválido?

Envolva o carregamento do bitmap em um bloco `try/catch` e apresente um erro claro:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Como lidar com idiomas que não sejam inglês?

Basta mudar a propriedade `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose suporta mais de 50 idiomas, então escolha aquele que corresponde ao seu material de origem.

### Preciso descartar objetos `Bitmap`?

Sim. `Bitmap` implementa `IDisposable`, portanto envolva‑lo em uma instrução `using` para liberar recursos nativos rapidamente.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### E se eu quiser um JSON compacto sem identação?

Troque as `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Isso reduz o tamanho do arquivo — útil em cenários com largura de banda limitada.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que incorpora todas as etapas, tratamento de erros e boas práticas discutidas acima. Salve‑o como `Program.cs` e execute-o a partir da linha de comando ou da sua IDE.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**O que isso faz:**  
1. Verifica se a imagem existe.  
2. Carrega‑a com segurança usando um bloco `using`.  
3. Executa OCR para **extrair texto de imagem**.  
4. Serializa o resultado em uma string JSON bem identada.  
5. Salva essa string no disco, respondendo à pergunta central **como salvar json**.

Execute `dotnet run` (ou pressione F5 no Visual Studio) e você verá a mensagem de confirmação assim que o arquivo for escrito.

---

## Conclusão

Agora você tem uma receita completa e pronta para produção de **como salvar JSON** que se origina da extração de texto baseada em OCR. Desde carregar um bitmap até escrever um JSON limpo, cada passo foi explicado com o “porquê” por trás do código, permitindo que você adapte a solução aos seus próprios projetos.

Se estiver curioso sobre a próxima fronteira, considere:

- **Como extrair texto** de PDFs convertendo cada página em uma imagem primeiro.  
- Usar os dados de caixa delimitadora para destacar palavras em uma UI WPF ou WinForms.  
- Transmitir o JSON diretamente para uma API web em vez de gravar um arquivo (use `HttpClient`).

Experimente, ajuste as opções e deixe os dados de OCR alimentarem a aplicação que você está construindo. Tem dúvidas? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}