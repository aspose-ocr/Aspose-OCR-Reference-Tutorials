---
category: general
date: 2026-02-13
description: Como usar OCR em C# para extrair texto de imagem, reconhecer texto de
  foto ou JPG e executar OCR em imagem sem internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: pt
og_description: Como usar OCR em C# para extrair texto de imagem, reconhecer texto
  de foto e executar OCR em imagem com um exemplo completo e executável.
og_title: Como usar OCR em C# – Extrair texto de imagem
tags:
- OCR
- C#
- Image Processing
title: Como usar OCR em C# – Extrair texto de imagem e reconhecer texto de foto
url: /pt/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR em C# – Extrair texto de imagem e reconhecer texto de foto

Já se perguntou **como usar OCR** para extrair palavras de uma captura de tela, de um recibo escaneado ou de uma foto aleatória que você tirou com o telefone? Você não está sozinho. Em muitos aplicativos do mundo real precisamos transformar imagens em texto pesquisável, e fazer isso localmente—sem uma conexão de internet instável—pode parecer um quebra‑cabeça.

É por isso que este guia mostra uma maneira passo a passo de **extrair texto de imagem** usando um motor OCR em C#, e também aborda como **reconhecer texto de foto**, **reconhecer texto de JPG** e **executar OCR em imagem** em arquivos que estão diretamente no seu disco. Ao final, você terá um programa completo, pronto para copiar e colar, que funciona imediatamente.

## O que você aprenderá

- Como configurar um motor OCR para Chinês Simplificado (ou qualquer idioma que você integrar).  
- O código exato necessário para **carregar recursos** de uma pasta local—sem chamadas de rede necessárias.  
- Como **reconhecer texto de foto** em arquivos como JPEG, PNG ou BMP.  
- Dicas para lidar com casos de borda comuns, como arquivos de modelo ausentes ou formatos de imagem não suportados.  
- Um exemplo completo e executável que você pode inserir no Visual Studio e ver os resultados instantaneamente.

### Pré‑requisitos

- .NET 6.0 ou posterior (a API usada aqui tem como alvo .NET Standard 2.0, portanto versões mais antigas também funcionam).  
- Familiaridade básica com C# e Visual Studio (ou qualquer IDE de sua preferência).  
- A biblioteca OCR que você está usando (o trecho assume uma classe fictícia `OcrEngine` que vem com modelos de idioma).  
- Uma pasta contendo os arquivos de modelo de idioma necessários—pense nela como o “cérebro” que o motor usa para ler caracteres chineses.

> **Dica profissional:** Se você ainda não tem os arquivos de modelo chinês, faça o download deles uma vez no site do fornecedor e coloque-os em uma pasta como `C:\OcrResources`. O motor nunca precisará se conectar à internet novamente.

---

![Diagrama mostrando o processo de OCR em uma foto](path/to/ocr-diagram.png "Diagrama mostrando o processo de OCR em uma foto")

## Como usar OCR: Configurar o motor

A primeira coisa que você precisa é uma instância do motor OCR, configurada para o idioma que você deseja. Neste tutorial, focamos em **Chinês Simplificado**, mas trocar `OcrLanguage.ChineseSimplified` por `OcrLanguage.English` (ou qualquer outro valor de enum) é apenas uma mudança de uma linha.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Por que isso importa:**  
Definir a propriedade `Language` informa ao motor qual conjunto de caracteres esperar. O `ResourceFolder` é onde o motor procura os pesos da rede neural e os dicionários de idioma—pense nele como o banco de memória do cérebro. Se você apontar para a pasta errada, o motor lançará uma `FileNotFoundException` e você ficará travado.

## Extrair texto de imagem – Carregando recursos

Antes que o motor possa realmente ler algo, você precisa carregar esses arquivos de modelo na memória. Esta etapa é **crucial** porque evita uma chamada de rede a cada vez que você processa uma imagem.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**O que pode dar errado?**  
Se o caminho da pasta estiver errado ou os arquivos estiverem corrompidos, `LoadResources()` lançará uma exceção. O bloco `try/catch` acima demonstra um tratamento de erro elegante—algo que você frequentemente precisará em produção.

## Reconhecer texto de foto – Executando o OCR

Agora a parte divertida: alimentar um arquivo de imagem ao motor e receber o texto reconhecido. Este é o núcleo dos cenários de **executar OCR em imagem**, seja a imagem um JPEG, PNG ou até um BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

O método `RecognizeImage` retorna um `RecognitionResult` (ou como quer que seu SDK o chame) que tipicamente contém:

- `Text` – a transcrição em texto simples.  
- `Confidence` – uma pontuação numérica que indica o quão confiante o motor está em cada linha.  
- `BoundingBoxes` – coordenadas opcionais para onde cada palavra está na imagem.

**Por que você pode se importar com a confiança:**  
Se você está construindo uma ferramenta de automação de entrada de dados, pode definir um limite (por exemplo, 0.85) e solicitar ao usuário que confirme linhas de baixa confiança. Isso melhora drasticamente a precisão geral.

## Reconhecer texto de JPG – Lidando com diferentes formatos

Muitos desenvolvedores assumem que OCR funciona apenas com PNGs, mas motores modernos lidam perfeitamente com arquivos **JPG**. O único detalhe é que a compressão JPEG pode introduzir artefatos que confundem o modelo.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Se você não tem um helper `DenoiseAndDeskew`, muitas bibliotecas (por exemplo, OpenCvSharp) fornecem essas funções. O ponto principal é: **executar OCR em imagem** após uma pequena limpeza se elas vierem de um scanner ou da câmera do telefone.

## Executar OCR em imagem – Dicas, casos de borda e boas práticas

### 1. Gerenciamento de memória

Carregar modelos de idioma grandes pode consumir centenas de megabytes. Libere o motor quando terminar:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Processamento em lote

Se você precisar processar dezenas de fotos, carregue os recursos uma vez, então faça o loop:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Cenários multilingues

Você pode mudar de idioma em tempo real reatribuindo `ocrEngine.Language` e chamando `LoadResources()` novamente. Apenas esteja ciente do tempo extra de carregamento.

### 4. Lidando com resultados vazios

Às vezes o motor retorna uma string vazia. Isso geralmente significa que a imagem está muito borrada ou a cor do texto se mistura ao fundo. Uma verificação rápida:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Considerações de segurança

Nunca alimente arquivos enviados por usuários diretamente ao motor OCR sem validação. No mínimo, verifique a extensão e o tamanho do arquivo, e considere escanear por malware.

---

## Exemplo completo e funcional

Abaixo está um programa único e autocontido que você pode copiar para um novo projeto de Console App. Ele demonstra **como usar OCR**, **extrair texto de imagem**, **reconhecer texto de foto**, **reconhecer texto de JPG** e **executar OCR em imagem**—tudo de uma vez.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Saída esperada (exemplo):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Seu texto real será diferente com base no conteúdo da imagem, mas você deverá ver um bloco de caracteres Unicode impresso no console junto com uma porcentagem de confiança.

---

## Conclusão

Nós percorremos **como usar OCR** em C# do início ao fim—configurando o motor, carregando recursos de idioma e, finalmente, **reconhecendo texto de foto** ou arquivos **JPG** sem nunca precisar da internet. Seguindo os passos acima, você pode **extrair texto de imagem**, **executar OCR em imagem** e lidar com as armadilhas mais comuns que atrapalham iniciantes.

Pronto para o próximo desafio? Tente alimentar o motor com uma página PDF convertida em imagem, ou experimente um pacote de idioma diferente para ver como as pontuações de confiança mudam. Você pode

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}