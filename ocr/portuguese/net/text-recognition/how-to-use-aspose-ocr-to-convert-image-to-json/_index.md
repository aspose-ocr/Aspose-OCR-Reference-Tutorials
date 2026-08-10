---
category: general
date: 2026-03-15
description: Como usar o Aspose OCR para extrair texto de imagens e converter imagem
  em JSON em C#. Aprenda a reconhecer texto de PNG e obter saída estruturada rapidamente.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: pt
og_description: Como usar o Aspose OCR para extrair texto de imagens e converter a
  imagem em JSON em C#. Este guia orienta você a reconhecer texto de PNG e obter saída
  estruturada.
og_title: Como usar o Aspose OCR para converter imagem em JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Como usar o Aspose OCR para converter imagem em JSON
url: /pt/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

to ensure we close the code block correctly: It ends with triple backticks. The original snippet ends with incomplete line; we keep same.

Now produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Aspose OCR para Converter Imagem em JSON

Como usar Aspose OCR é uma pergunta comum quando os desenvolvedores precisam extrair texto de imagens. Se você está procurando **converter imagem em JSON** ou **reconhecer texto de PNG**, este guia tem o que você precisa — sem enrolação, apenas uma solução prática e completa.

Nos próximos minutos vamos percorrer tudo que você precisa: instalar a biblioteca, configurar o motor para saída JSON, carregar um PNG de recibo, executar OCR e, finalmente, gravar o resultado em um arquivo `.json`. Ao final, você será capaz de **extrair texto de imagem** com uma única chamada de método e entenderá por que cada passo é importante.

> **Pro tip:** Aspose OCR funciona com uma ampla variedade de formatos de imagem (PNG, JPEG, BMP, TIFF). O mesmo código abaixo lidará com todos eles, então você não precisa escrever lógica específica para cada formato.

## O Que Você Precisa

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+)  
- Um pacote NuGet válido do Aspose.OCR (teste gratuito ou licenciado)  
- Um arquivo de imagem que você deseja processar (por exemplo, `receipt.png`)  
- Visual Studio, VS Code ou qualquer editor C# de sua preferência  

É só isso — sem dependências extras, sem serviços externos. Pronto? Vamos começar.

![how to use aspose OCR engine](image-placeholder.png "how to use aspose OCR engine")

## Como Usar Aspose OCR – Configurar Saída JSON

A primeira coisa que você tem que fazer ao **how to use aspose** para OCR é criar uma instância de `OcrEngine` e dizer a ela para gerar JSON. Essa pequena troca de configuração salva você de ter que serializar o resultado manualmente depois.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Por que isso importa:** Definir `OutputFormat` como `Json` significa que o motor OCR já estrutura o texto em uma hierarquia de páginas, linhas e palavras. Você não precisa analisar strings brutas depois, o que torna o processamento posterior — como inserir dados em um banco de dados — muito mais limpo.

## Converter Imagem em JSON com Aspose OCR

Agora que o motor está configurado, vamos falar sobre a parte de **converter imagem em JSON** com mais detalhes.

1. **Carregar a imagem** – `Image.FromFile` funciona para qualquer formato suportado. Se você estiver lidando com um stream (por exemplo, um arquivo enviado), pode usar `Image.FromStream` em vez disso.  
2. **Executar `Recognize`** – esse método retorna um objeto `OcrResult`. Como definimos a saída como JSON, `ocrResult.Text` já contém uma string JSON.  
3. **Gravar o arquivo** – `File.WriteAllText` é a maneira mais simples de persistir o JSON. Se precisar armazená‑lo em um bucket na nuvem, basta substituir esta linha pela chamada de SDK apropriada.

### Saída JSON Esperada

Um payload JSON típico se parece com isto (reduzido para brevidade):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Agora você pode alimentar essa estrutura em qualquer sistema posterior — seja uma ferramenta de relatório, um modelo de machine‑learning ou um simples arquivo de log.

## Extrair Texto de Imagem Usando Aspose OCR

Se você só precisa da string bruta (ou seja, não se importa com JSON), basta mudar o formato de saída de volta para texto simples:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Quando escolher texto simples?**  
- Depuração rápida ou saída no console.  
- Cenários onde você aplicará pós‑processamento customizado (por exemplo, extração via regex).  

Mas lembre‑se, **extrair texto de imagem** usando JSON fornece dados posicionais — úteis para destacar texto em uma UI ou alinhar com campos de formulário.

## Reconhecer Texto de Arquivos PNG

PNG é um formato sem perdas, que frequentemente produz melhor precisão de OCR comparado a JPEGs fortemente comprimidos. Aqui está uma checklist rápida para garantir os melhores resultados ao **reconhecer texto de PNG**:

| Item da Checklist | Por Que Ajuda |
|-------------------|---------------|
| Use um DPI de 300+ | Resolução maior fornece ao motor mais pixels para trabalhar. |
| Mantenha a imagem em escala de cinza | Reduz ruído; Aspose OCR converte automaticamente, mas o pré‑processamento pode acelerar o processo. |
| Remova ruído de fundo | Fundos limpos melhoram as pontuações de confiança. |

Se você encontrar pontuações de confiança baixas, tente aumentar o DPI ou aplicar um filtro de limiar simples antes de enviar a imagem ao Aspose.

## Como Extrair Resultados de OCR Programaticamente

Além de apenas salvar o JSON, você pode querer ler programaticamente campos específicos — por exemplo, o valor total de um recibo. Como o JSON contém uma hierarquia, você pode desserializá‑lo em um objeto C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Agora você pode consultar `ocrData` com LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Por que isso funciona:** O JSON já indica onde cada palavra está na página, permitindo localizar campos de forma confiável mesmo que o layout mude levemente.

## Casos de Borda & Armadilhas Comuns

- **Resultado Nulo:** Se `ocrEngine.Recognize` retornar `null`, a imagem pode ser incompatível ou estar corrompida. Sempre proteja contra isso:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Arquivos Grandes:** Para imagens de vários megabytes, considere fazer streaming da imagem ou redimensioná‑la antes do OCR para evitar uso excessivo de memória.

- **Problemas de Licença:** A versão de avaliação adiciona uma marca d'água à saída. Certifique‑se de carregar sua licença logo no início do programa:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Scripts Não‑Latinos:** Aspose OCR suporta muitos idiomas, mas você deve definir a propriedade `Language` adequadamente (por exemplo, `ocrEngine.Configuration.Language = Language.English;`).

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}