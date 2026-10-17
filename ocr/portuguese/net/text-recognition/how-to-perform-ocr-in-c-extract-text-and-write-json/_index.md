---
category: general
date: 2026-02-09
description: Aprenda a fazer OCR em C# para extrair texto de imagens, reconhecer texto
  de PNG e gerar rapidamente um arquivo JSON em C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: pt
og_description: Como realizar OCR em C#? Siga este guia passo a passo para extrair
  texto de imagens, reconhecer texto de PNG e escrever arquivos JSON em C# de forma
  eficiente.
og_title: Como fazer OCR em C# – Extrair texto e gerar JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Como realizar OCR em C# – Extrair texto e gerar JSON
url: /pt/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em C# – Guia Completo

Realizar OCR em C# é um obstáculo comum quando você precisa **extrair texto de imagem**. Neste guia, vamos percorrer o reconhecimento de texto a partir de PNG, exportar o resultado detalhado para uma string JSON e, finalmente, **escrever arquivo JSON C#**. Já ficou olhando para um formulário escaneado e se perguntou como transformar aqueles rabiscos em texto pesquisável? Você não está sozinho; muitos desenvolvedores encontram esse problema logo no início.

Usaremos a biblioteca Aspose.OCR porque ela fornece confiança por símbolo pronta para uso e funciona bem com projetos .NET 6+. Ao final deste tutorial, você terá um aplicativo de console pronto‑para‑executar que carrega um PNG, extrai cada caractere e salva um arquivo JSON organizado que pode ser inserido em um banco de dados ou em um modelo de IA. Sem atalhos misteriosos de “ver a documentação” — apenas uma solução autônoma.

## O Que Você Precisa

- **.NET 6 SDK** (ou posterior) – a versão LTS atual no momento da escrita.
- **Aspose.OCR for .NET** pacote NuGet – `Install-Package Aspose.OCR`.
- Uma imagem PNG que você deseja escanear (por exemplo, `form.png`).  
- Uma IDE ou editor – Visual Studio, VS Code, Rider – o que for mais confortável para você.

É isso. Se você tem esses componentes, está pronto para começar.

![Exemplo de como realizar OCR](ocr-example.png "Como realizar OCR em C#")

*Texto alternativo da imagem: ilustração de como realizar OCR mostrando um aplicativo de console C# processando um PNG.*

## Etapa 1: Configurar o Projeto e Adicionar Dependências

Primeiro, crie um novo projeto de console e inclua a biblioteca Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Dica:** Use a flag `--framework net6.0` se quiser bloquear explicitamente o framework de destino.

Por que esta etapa importa: o pacote NuGet contém as classes `OcrEngine`, `ImageStream` e `JsonExporter` das quais dependeremos. Sem ele, o compilador não terá ideia do que “OCR” significa.

## Etapa 2: Escrever a Lógica Central de OCR

Abra `Program.cs` (ou crie um novo arquivo) e substitua seu conteúdo pelo seguinte. Cada seção está comentada para que você veja o motivo de sua existência.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Por Que Cada Parte É Importante

- **OcrEngine**: Pense nele como o cérebro da operação. Ele carrega modelos de linguagem e configura o pipeline de inferência.
- **ImageStream.FromFile**: Lida com qualquer PNG, JPEG, BMP, etc. Ele abstrai as peculiaridades de I/O de arquivos.
- **RecognitionResult**: Contém o texto bruto mais as pontuações de confiança. É aqui que você obtém os dados granulares necessários para validações posteriores.
- **JsonExporter**: Converte o rico `RecognitionResult` em um payload JSON limpo, perfeito para APIs.
- **File.WriteAllText**: A maneira direta do .NET de **escrever arquivo JSON C#** sem dependências extras.

## Etapa 3: Executar o Aplicativo e Verificar a Saída

Compile e execute o programa:

```bash
dotnet run
```

Você deverá ver uma mensagem no console semelhante a:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Abra `form.json` – você encontrará algo como:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

A etapa de **extrair texto de imagem** foi bem‑sucedida, e agora você tem uma representação JSON legível por máquina de cada caractere.

## Etapa 4: Lidar com Casos de Borda Comuns

### Arquivos Ausentes ou Corrompidos

Se o caminho do PNG estiver errado, `ImageStream.FromFile` lança uma `FileNotFoundException`. Envolva o código de carregamento em um bloco try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Baixas Pontuações de Confiança

Às vezes o OCR retorna baixa confiança para digitalizações ruidosas. Você pode filtrar símbolos antes de exportar:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Isso garante que o JSON contenha apenas caracteres razoavelmente confiáveis — útil quando você alimenta os dados em pipelines de validação posteriores.

### Arquivos Grandes & Memória

Processar um PNG de vários megabytes pode aumentar o uso de memória. Considere transmitir a imagem em blocos ou usar `OcrEngine.RecognizeAsync` (disponível em versões mais recentes da Aspose) para manter a UI responsiva.

## Etapa 5: Estender a Solução (Opcional)

- **Processamento em lote**: Percorra um diretório de PNGs e gere um JSON correspondente para cada arquivo.
- **Armazenamento em banco de dados**: Insira o JSON em uma coluna SQL `NVARCHAR(MAX)` para análises posteriores.
- **Seleção de idioma**: Defina `ocrEngine.Language = OcrLanguage.Spanish;` se precisar de suporte a idiomas não‑ingleses.

Todas essas extensões seguem o mesmo padrão de **como realizar OCR** que estabelecemos — inicializar, reconhecer, exportar e persistir.

## Perguntas Frequentes

**Q: Isso funciona com JPG ou TIFF?**  
A: Absolutamente. `ImageStream.FromFile` detecta automaticamente o formato, então você pode substituir o PNG por qualquer imagem raster suportada.

**Q: E se eu precisar extrair texto de um PDF?**  
A: Converta cada página do PDF em uma imagem primeiro (por exemplo, usando `Aspose.PDF`) e então alimente o PNG no fluxo OCR descrito aqui.

**Q: Posso obter o resultado do OCR como XML em vez de JSON?**  
A: Sim. Aspose.OCR também inclui um `XmlExporter`. Troque `JsonExporter` por `XmlExporter` e ajuste a extensão do arquivo.

## Conclusão

Caminhamos por **como realizar OCR** em C# do início ao fim, mostrando como **extrair texto de imagem**, **reconhecer texto de PNG** e **escrever arquivo JSON C#** sem problemas. O exemplo completo e executável está nos trechos de código acima, e agora você entende o porquê de cada etapa — inicializar o motor, lidar com casos de borda e persistir os resultados.

A seguir, você pode explorar pipelines de OCR em lote, integrar a saída JSON ao Azure Cognitive Search ou experimentar modelos de linguagem personalizados. O céu é o limite depois que você dominar o básico de OCR em C#.

Se você encontrou algum problema ou tem ideias para extensões adicionais, deixe um comentário abaixo. Feliz codificação, e aproveite transformar essas digitalizações pixeladas em dados limpos e pesquisáveis!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}