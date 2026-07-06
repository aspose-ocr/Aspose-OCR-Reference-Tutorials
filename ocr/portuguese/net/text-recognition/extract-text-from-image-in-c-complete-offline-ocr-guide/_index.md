---
category: general
date: 2026-03-18
description: Extrair texto de imagem usando Aspose OCR em C#. Aprenda como extrair
  texto, executar reconhecimento OCR e reconhecer texto cirílico sem internet.
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: pt
og_description: Extraia texto de imagem com Aspose OCR. Guia passo a passo para executar
  o reconhecimento OCR, como extrair texto e reconhecer texto cirílico offline.
og_title: Extrair Texto de Imagem em C# – Tutorial de OCR Offline
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrair Texto de Imagem em C# – Guia Completo de OCR Offline
url: /pt/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem – Guia Completo de OCR Offline

Já precisou **extrair texto de imagem** mas se preocupou com a latência da rede ou restrições de licenciamento? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando seu aplicativo precisa funcionar em um ambiente isolado, mas ainda assim requer OCR confiável. A boa notícia? Com o Aspose OCR você pode executar todo o pipeline localmente, **extrair texto de imagem** sem nunca tocar na internet.

Neste tutorial, percorreremos um exemplo prático que mostra **como extrair texto**, configurar um mecanismo offline, **executar reconhecimento OCR**, e até **reconhecer texto cirílico**. Ao final, você terá um aplicativo de console C# pronto‑para‑executar que imprime a string detectada diretamente no console.

## O que você precisará

- .NET 6.0 SDK (ou qualquer versão recente do .NET)  
- Visual Studio 2022 ou VS Code – o que preferir  
- Pacote NuGet Aspose.OCR para .NET  
- Uma pasta contendo os arquivos de modelo Aspose OCR (baixe uma vez do portal Aspose)  
- Um arquivo de imagem que inclui caracteres em inglês e cirílico (por exemplo, `cyrillic_doc.jpg`)

Sem serviços externos, sem downloads ocultos em tempo de execução – tudo reside no seu disco.

## Etapa 1: Instalar Aspose.OCR e Preparar Recursos

Primeiro, adicione o pacote NuGet Aspose.OCR ao seu projeto:

```bash
dotnet add package Aspose.OCR
```

Em seguida, crie uma pasta chamada `AsposeOCRResources` em algum lugar da sua máquina e copie os arquivos de modelo que você baixou da Aspose para ela. O mecanismo OCR procurará pacotes de idioma neste diretório, portanto, certifique‑se de que o caminho esteja correto.

> **Dica profissional:** Mantenha a pasta de recursos ao lado do seu arquivo `.csproj`; isso simplifica o gerenciamento de caminhos durante o desenvolvimento.

## Etapa 2: Construir o Motor OCR Offline

Agora vamos instanciar o motor e apontá‑lo para a pasta de recursos. Esta é a etapa crucial que nos permite **executar reconhecimento OCR** totalmente offline.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

Por que carregar idiomas explicitamente? Porque instruímos o motor a permanecer offline; ele não acessará os servidores da Aspose para buscar pacotes ausentes. Se você esquecer de carregar um idioma, quaisquer caracteres desse script serão ignorados.

## Etapa 3: Alimentar a Imagem no Motor

Com o motor pronto, agora fornecemos a imagem que queremos processar. O auxiliar `ImageStream.FromFile` lê o arquivo em um formato que o motor OCR entende.

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

Se sua imagem for grande, considere redimensioná‑la previamente para melhorar a velocidade e a precisão. O motor OCR funciona melhor com um DPI em torno de 300.

## Etapa 4: Executar o Processo de Reconhecimento

Chamar `Recognize` realiza o trabalho pesado. O método retorna um objeto `OcrResult` que contém a string extraída, pontuações de confiança e mais.

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Nos bastidores, a Aspose analisa o bitmap, executa redes neurais específicas de idioma e une os caracteres. Como carregamos tanto o inglês quanto o cirílico, documentos de script misto são tratados sem problemas.

## Etapa 5: Exibir o Texto Extraído

Finalmente, exibimos o resultado. Em um aplicativo real você pode armazená‑lo em um banco de dados ou enviá‑lo para outro serviço, mas para esta demonstração apenas o imprimiremos.

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Executar o programa deve gerar algo como:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

Se você vir caracteres distorcidos, verifique novamente se o pacote de idioma cirílico está corretamente colocado na pasta de recursos e se a imagem não está muito borrada.

![exemplo de extração de texto de imagem](extract_text_image.png "extrair texto de imagem")

*Texto alternativo da imagem: extrair texto de imagem – resultado OCR mostrando linhas em inglês e cirílico.*

## Lidando com Problemas Comuns

### Pacotes de Idioma Ausentes

Se você receber uma exceção dizendo “Language data not found”, o motor não conseguiu localizar os arquivos de modelo. Verifique `ResourcesPath` e certifique‑se de que a pasta contém `english.dat` e `cyrillic.dat` (ou arquivos com nomes semelhantes).

### Baixas Pontuações de Confiança

Ocasionalmente o motor OCR retornará baixa confiança para certos caracteres, especialmente se a imagem tiver ruído. Você pode melhorar a precisão ao:

- Converter a imagem para escala de cinza antes de alimentá‑la ao motor  
- Aplicar um filtro mediano para reduzir manchas  
- Garantir que o texto esteja alinhado horizontalmente (gire se necessário)

### Imagens Grandes

Processar uma foto de 10 MP pode ser lento. Reduza para uma largura máxima de 2000 px preservando a proporção; o motor ainda capturará a maioria dos caracteres com precisão.

## Estendendo o Exemplo

- **Processamento em lote:** Envolva a lógica de reconhecimento em um loop que itere sobre todos os arquivos em um diretório.  
- **Formatos de saída:** `OcrResult` também fornece uma coleção `TextLines` que inclui caixas delimitadoras — útil para destacar texto em aplicações de UI.  
- **Idiomas adicionais:** Basta chamar `LoadLanguage` com qualquer outro valor de enumeração suportado (por exemplo, `Language.French`).  

Todas essas extensões ainda obedecem ao princípio de **como extrair texto** — basta carregar os pacotes de idioma apropriados e deixar o motor fazer o resto.

## Recapitulação do Código Fonte Completo

Abaixo está o programa completo, pronto para copiar e colar. Substitua `YOUR_DIRECTORY` pelo caminho real na sua máquina.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Salve isso como `Program.cs`, execute `dotnet run` e observe o console imprimir o texto que o motor extraiu da sua imagem. É isso — você **extraiu texto de imagem** com sucesso offline.

## Conclusão

Cobrimos tudo o que você precisa para **extrair texto de imagem** usando o Aspose OCR em um cenário completamente offline. O guia mostrou **como extrair texto**, demonstrou **executar reconhecimento OCR**, e provou que você pode **reconhecer texto cirílico** ao lado do inglês sem nenhuma chamada de rede.

Desde a configuração do pacote NuGet até o tratamento de casos extremos como pacotes de idioma ausentes, você agora tem uma base sólida para construir recursos alimentados por OCR em qualquer aplicação .NET.

Qual o próximo passo? Experimente alimentar PDFs, escanear várias páginas ou integrar a saída com um índice de busca. O céu é o limite assim que você dominar o OCR offline.

Feliz codificação, e que suas imagens estejam sempre cristalinas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}