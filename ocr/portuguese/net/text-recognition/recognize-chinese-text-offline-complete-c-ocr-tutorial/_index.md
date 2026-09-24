---
category: general
date: 2026-01-02
description: Aprenda a reconhecer texto chinês e extrair texto de arquivos PNG com
  reconhecimento de texto offline usando Aspose.OCR. Não é necessário internet – realize
  OCR na imagem em apenas alguns passos.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: pt
og_description: reconheça texto chinês sem internet. Este tutorial mostra como extrair
  texto de PNG usando reconhecimento de texto offline e realizar OCR em imagem em
  C#.
og_title: reconhecer texto chinês offline – Guia passo a passo em C#
tags:
- OCR
- C#
- Aspose
title: reconhecer texto chinês offline – Tutorial completo de OCR em C#
url: /pt/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto chinês offline – Tutorial Completo de OCR em C#

Já precisou **reconhecer texto chinês** de um PNG escaneado, mas seu aplicativo roda em uma máquina sem internet? Você não está sozinho. Em muitos cenários corporativos—pense em servidores isolados ou dispositivos de campo—contar com serviços em nuvem simplesmente não é uma opção.  

Neste guia vamos percorrer uma solução autônoma que permite **extrair texto de arquivos png**, executar **reconhecimento de texto offline** e **realizar OCR em imagens** usando Aspose.OCR. Ao final, você terá um programa console em C# pronto‑para‑executar que imprime os caracteres chineses diretamente no console.

## Pré‑requisitos

- .NET 6 SDK (ou qualquer versão recente do .NET) instalado localmente.  
- Visual Studio 2022 ou VS Code – o que preferir.  
- Uma cópia do pacote NuGet Aspose.OCR for .NET (`Aspose.OCR`).  
- Os arquivos de recursos de idioma para Inglês e Chinês Simplificado (o tutorial mostra como baixá‑los automaticamente).  
- Uma imagem chamada `chinese_doc.png` colocada em uma pasta que você possa referenciar (marcador `YOUR_DIRECTORY`).

Sem serviços adicionais, sem chaves de API—apenas uma DLL local e alguns arquivos de recurso.

---

## Etapa 1 – Baixar os recursos de idioma necessários (uma única vez)

Aspose.OCR armazena pacotes de idioma em disco. Na primeira execução do app você precisa baixá‑los. A chamada `ResourceManager.DownloadResources` faz exatamente isso, e como passamos tanto Inglês quanto Chinês Simplificado, o motor pode alternar entre eles depois sem nenhum tráfego de rede extra.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Dica profissional:** Mantenha a pasta baixada (`Aspose.OCR.Resources`) sob controle de versão se precisar de builds reproduzíveis em várias máquinas.

## Etapa 2 – Inicializar o motor OCR em modo offline

Definir `OfflineMode = true` indica à biblioteca que evite chamadas HTTP. Essa é a chave para um verdadeiro **reconhecimento de texto offline**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Por que isso importa:** Algumas bibliotecas de OCR recorrem a serviços em nuvem quando um pacote de idioma está ausente. Forçando o modo offline garantimos desempenho determinístico e conformidade com políticas de privacidade de dados.

## Etapa 3 – Carregar o PNG que você deseja processar

Usaremos `System.Drawing.Bitmap` para ler a imagem. Se seu projeto tem como alvo .NET 6+ em plataformas não‑Windows, considere `SkiaSharp` como alternativa, mas para a maioria das implantações centradas em Windows `Bitmap` funciona bem.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Caso extremo:** Se o PNG for muito grande (mais de 5 MP) pode ser interessante redimensioná‑lo primeiro para acelerar o reconhecimento e reduzir o uso de memória:

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Etapa 4 – Executar o reconhecimento com o idioma Chinês Simplificado

Aqui informamos ao motor exatamente qual idioma usar. O objeto `RecognitionOptions` também permite ajustar coisas como `DetectOrientation` ou `PreserveFormatting`, mas os valores padrão funcionam bem para a maioria dos documentos impressos.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Etapa 5 – Exibir (ou processar) o texto extraído

A propriedade `OcrResult.Text` contém a representação em texto puro. Você pode escrevê‑la no console, em um arquivo ou alimentá‑la em um pipeline de NLP subsequente.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Saída esperada

Se `chinese_doc.png` contiver a frase “你好，世界！”, o console mostrará:

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Observação:** A precisão do OCR depende da qualidade da imagem, clareza da fonte e contraste. Para melhores resultados, use digitalizações de alta resolução (300 dpi ou mais) e garanta que o texto não esteja inclinado.

---

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para copiar e colar. Salve como `Program.cs` dentro de um novo projeto console e execute `dotnet run`. Todas as etapas estão agrupadas, permitindo visualizar o fluxo desde o download dos recursos até a saída final.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Dica:** Envolva a chamada `ResourceManager.DownloadResources` em um bloco `try/catch` se quiser lidar graciosamente com a falta de internet. O método lançará uma `NetworkException` caso contrário.

---

## Perguntas Frequentes (FAQ)

| Pergunta | Resposta |
|----------|----------|
| **Posso reconhecer Chinês Tradicional?** | Sim—substitua `Language.ChineseSimplified` por `Language.ChineseTraditional` e baixe o pacote correspondente. |
| **E se eu precisar extrair texto de um JPEG em vez de PNG?** | O mesmo código funciona; basta mudar a extensão do arquivo. `Bitmap` suporta a maioria dos formatos raster comuns. |
| **Existe uma forma de obter caixas delimitadoras para cada caractere?** | Defina `RecognitionOptions.DetectRegions = true`. O `OcrResult` então conterá objetos `Region` com coordenadas. |
| **Como executar isso no Linux?** | Use o pacote `System.Drawing.Common` (versão 1.0+). Em Linux sem interface gráfica pode ser necessário a dependência nativa `libgdiplus`. |
| **Posso processar em lote uma pasta de imagens?** | Absolutamente—envolva a lógica de reconhecimento em um loop `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

---

## Próximos Passos & Tópicos Relacionados

- **Melhorar a precisão**: experimente `RecognitionOptions.PreprocessImage = true` para que o motor ajuste automaticamente o contraste.  
- **Combinar idiomas**: você pode passar um array de idiomas para `ResourceManager.DownloadResources` e deixar o motor detectar automaticamente.  
- **Integrar com uma UI**: migre o código console para um app WinForms ou WPF e exiba o resultado do OCR em uma caixa de texto.  
- **Explorar outras bibliotecas Aspose**: `Aspose.PDF` para geração de PDFs, `Aspose.Slides` para automação de apresentações, etc.  

Se você tem interesse em extrair texto de outros formatos de imagem, o mesmo padrão se aplica—basta trocar o caminho do arquivo e, opcionalmente, ajustar as opções de pré‑processamento. Boa codificação!

---

![exemplo de reconhecimento de texto chinês](/images/recognize-chinese-text.png "Captura de tela mostrando a saída do reconhecimento de texto chinês no console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}