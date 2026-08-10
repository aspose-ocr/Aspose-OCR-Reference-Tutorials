---
category: general
date: 2026-04-01
description: Como converter a saída de OCR para JSON e XML em C# – aprenda a extrair
  texto de imagem e escrever arquivo JSON em C# usando Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: pt
og_description: Como converter resultados de OCR em arquivos JSON e XML estruturados
  com C#. Guia passo a passo para extrair texto de imagem e gerar arquivo JSON em
  C#.
og_title: Como converter OCR para JSON e XML em C# – Escrever arquivo JSON
tags:
- OCR
- C#
- Aspose
title: Como converter OCR para JSON e XML em C# – Escrever arquivo JSON
url: /pt/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Converter OCR para JSON & XML em C# – Gravar Arquivo JSON

**Como converter OCR** resultados em algo que você realmente possa usar é uma pergunta que muitos desenvolvedores fazem. Neste guia vamos mostrar como extrair texto de uma imagem, transformar a saída de OCR em JSON e XML bem formatados e, em seguida, gravar esses arquivos no disco com C#.

Se você já ficou encarando uma string de OCR bruta e pensou: “Tem que haver uma maneira melhor de armazenar isso”, você está no lugar certo. Ao final, você terá um programa completo e executável que não só **extrai texto de arquivos de imagem**, mas também sabe **gravar arquivo JSON C#** e **gravar arquivo XML C#** sem esforço.

## O que Você Precisa

- **.NET 6.0** ou superior (o código também funciona com .NET Framework 4.6+).  
- Pacote NuGet **Aspose.OCR** – instale com `dotnet add package Aspose.OCR`.  
- Uma imagem contendo texto (por exemplo, `invoice.png`).  
- Qualquer IDE de sua preferência – Visual Studio, Rider ou VS Code servem.

> **Dica de especialista:** Mantenha seus arquivos de imagem em uma pasta dedicada (por exemplo, `Resources/`) para que os caminhos fiquem organizados.

## Etapa 1: Configurar o Motor OCR – Como Converter OCR

Primeiro, criamos uma instância de `OcrEngine` e informamos a qual idioma ele deve procurar. Na maioria dos casos o inglês basta, mas você pode substituir `Language.English` por qualquer idioma suportado.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Por que isso importa:** Inicializar o motor com o idioma correto melhora drasticamente a precisão, especialmente para scripts não latinos.

## Etapa 2: Reconhecer Texto – Extrair Texto da Imagem

Agora enviamos a imagem para o motor. O método `Recognize` devolve um objeto `OcrResult` que contém o texto bruto assim como os dados de localização.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Se a imagem não for encontrada, `Recognize` lança uma `FileNotFoundException`. Para manter a demonstração simples, assumimos que o caminho está correto, mas em produção você deve envolver isso em um bloco try‑catch.

## Etapa 3: Converter o Resultado para JSON – Gravar Arquivo JSON C#

Aspose.OCR torna a serialização muito fácil. O método `ToJson` aceita um parâmetro `indent` para produzir saída formatada, o que é perfeito quando você pretende abrir o arquivo em um editor de texto.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Exemplo de JSON Esperado

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Como extrair texto:** A propriedade `Text` fornece a string simples que você pode encaminhar para outros serviços (índices de busca, bancos de dados, etc.).

## Etapa 4: Persistir o JSON – Gravar Arquivo JSON C# (Continuação)

Com a string JSON pronta, basta gravá‑la em um arquivo usando `File.WriteAllText`. Isso garante codificação UTF‑8 por padrão.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Agora você tem um `invoice.json` ao lado da sua imagem, pronto para o processamento posterior.

## Etapa 5: Converter o Resultado para XML – Gravar Arquivo XML C#

Se você prefere XML para sistemas legados, o método `ToXml` faz o trabalho pesado. Assim como `ToJson`, ele também suporta formatação “pretty‑print”.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Exemplo de XML Esperado

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Etapa 6: Persistir o XML – Gravar Arquivo XML C# (Continuação)

Salvar o XML é idêntico ao passo do JSON; basta apontar para a extensão `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Exemplo Completo Funcionando

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em um aplicativo de console:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Execute o programa e você encontrará dois novos arquivos — `invoice.json` e `invoice.xml` — exatamente onde você especificou. Abra‑os para verificar se a estrutura corresponde aos exemplos acima.

## Perguntas Frequentes & Casos de Borda

| Pergunta | Resposta |
|----------|----------|
| **E se a imagem contiver vários idiomas?** | Crie instâncias separadas de `OcrEngine` para cada idioma ou use `Language.Multi` se suportado. |
| **Posso controlar o formato de saída (por exemplo, excluir dados de região)?** | Sim. Tanto `ToJson` quanto `ToXml` aceitam parâmetros opcionais para filtrar campos; consulte a documentação do Aspose.OCR para `ExportOptions`. |
| **Como lidar com PDFs grandes com muitas páginas?** | Processar cada página individualmente, agregar os resultados e então serializar uma única vez. |
| **A saída é segura em UTF‑8?** | Absolutamente — o Aspose.OCR usa Unicode internamente, e `File.WriteAllText` grava em UTF‑8 por padrão. |
| **E quanto ao desempenho?** | OCR é intensivo em CPU. Para trabalhos em lote, considere paralelizar entre núcleos ou usar a API cloud da Aspose. |

## Conclusão

Agora você sabe **como converter OCR** resultados em JSON e XML usando C#. Seguindo os passos acima, você pode **extrair texto de imagem**, depois **gravar arquivo JSON C#** e **gravar arquivo XML C#** com apenas algumas linhas de código. Essa abordagem é rápida, confiável e funciona com qualquer tipo de imagem que o Aspose.OCR suporte.

Pronto para o próximo desafio? Experimente alimentar o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}