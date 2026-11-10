---
category: general
date: 2026-06-03
description: Tutorial de OCR de legendas de vídeo mostrando como extrair quadros de
  vídeo e ler texto de arquivos de vídeo como MP4 usando Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: pt
og_description: Aprenda OCR de legendas de vídeo com Aspose.OCR. Extraia quadros de
  vídeo, leia texto do vídeo e extraia texto de MP4 em poucos minutos.
og_title: OCR de Legendas de Vídeo em C# – Guia Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR de Legendas de Vídeo em C# – Guia Completo
url: /pt/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR de Legendas de Vídeo em C# – Guia Completo

Já precisou de **video subtitle ocr** mas não sabia por onde começar? Você não está sozinho. Seja digitalizando gravações de aulas, extraindo legendas de vídeos de treinamento, ou simplesmente curioso sobre como ler texto de vídeo, este tutorial mostra exatamente como fazer isso com C# e Aspose.OCR.  

Nos próximos minutos, extrairemos quadros do vídeo, executaremos OCR nesses quadros e, finalmente, exibiremos o texto da legenda quadro a quadro. Ao final, você será capaz de **ler texto de vídeo** arquivos — incluindo MP4 — sem precisar procurar ferramentas de terceiros.

## O que você vai construir

Vamos criar um pequeno aplicativo de console que:

1. Decodifica um MP4 (ou qualquer formato suportado) em quadros individuais `Bitmap`.  
2. Limita a região de OCR à faixa de legenda para que o motor não seja distraído pela imagem inteira.  
3. Processa cada quadro com o `VideoOcrProcessor` da Aspose.  
4. Imprime o texto da legenda reconhecido no console.

Sem enrolação, apenas um exemplo funcional de ponta a ponta que você pode inserir em um projeto real.

## Pré-requisitos

- **.NET 6.0** ou posterior (o código também funciona no .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – instale via NuGet: `Install-Package Aspose.OCR`.  
- Um arquivo de vídeo (MP4 funciona muito bem).  
- Uma forma de decodificar quadros de vídeo – a demonstração usa um método placeholder, mas você pode integrar FFmpeg, OpenCV ou qualquer biblioteca que retorne objetos `Bitmap`.  

> Dica profissional: Se você estiver no Windows, o pacote `System.Drawing.Common` funciona bem para `Bitmap`. No Linux/macOS você precisará da dependência nativa `libgdiplus`.

## Etapa 1 – Extrair Quadros do Vídeo

O primeiro obstáculo é transformar uma imagem em movimento em imagens estáticas. O método `GetVideoFrames` abaixo foi deixado intencionalmente em branco; substitua-o pelo seu decodificador favorito. Aqui está um esboço rápido usando FFmpeg‑Core (apenas para ilustrar a forma dos dados):

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Por que isso importa:** Extrair quadros fornece ao motor de OCR uma imagem estática para trabalhar, o que melhora drasticamente a precisão em comparação com tentar ler diretamente de um fluxo de vídeo.

## Etapa 2 – Configurar o VideoOcrProcessor

Agora que temos uma sequência de objetos `Bitmap`, podemos entregá-los ao Aspose.OCR. O `VideoOcrProcessor` nos permite definir uma **Região de Interesse (ROI)** – perfeito para legendas que geralmente ficam na parte superior ou inferior do quadro.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Por que limitar a ROI?** Ao ignorar o resto da imagem, reduzimos o ruído, diminuímos o tempo de processamento e evitamos falsos positivos de gráficos de fundo.

## Etapa 3 – Executar OCR na Sequência de Quadros

Com o processador pronto, alimentar os quadros é uma única linha de código. O método `Process` retorna um enumerável de objetos `OcrResult`, cada um contendo o texto reconhecido para seu respectivo quadro.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **O que está acontecendo nos bastidores?** O Aspose.OCR normaliza internamente cada bitmap, executa um reconhecedor baseado em rede neural e, em seguida, pós-processa a saída para melhorar pontuação e quebras de linha.

## Etapa 4 – Exibir o Texto Extraído

Finalmente, iteramos sobre os resultados e imprimimos cada linha de legenda. Você também pode gravá-las em um arquivo SRT, em um banco de dados ou enviá-las para um serviço de tradução.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Exemplo Completo Funcional

Juntando tudo, obtemos um programa de console autônomo:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Saída esperada (exemplo)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Se o OCR tiver dificuldades com um quadro específico, você verá uma string vazia – isso indica que você deve ajustar a ROI ou aumentar a taxa de extração de quadros.

## Armadilhas Comuns & Como Corrigi‑las

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Caracteres estranhos** | Quadros de baixa resolução ou compressão pesada | Extraia quadros em uma taxa de bits mais alta, ou aumente a escala do bitmap antes do OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **Nenhum texto retornado** | A ROI não cobre realmente a faixa de legenda | Verifique as coordenadas do retângulo (use uma ferramenta de captura de tela para medir). |
| **Gargalo de desempenho** | Processar todos os quadros a 30 fps é excessivo | Reduza a taxa para 1‑2 fps na maioria dos fluxos de legenda; ainda é possível capturar cada mudança de legenda. |
| **FFmpeg não encontrado** | `ffmpeg.exe` não está no `PATH` | Forneça o caminho completo em `ProcessStartInfo.FileName` ou instale o FFmpeg globalmente. |

## Expandindo a Solução

- **Exportar para SRT** – concatene os timestamps com o texto OCR e escreva um arquivo SubRip.  
- **Suporte multilíngue** – defina `ocrProcessor.Language = OcrLanguage.Spanish` (ou qualquer idioma suportado).  
- **Processamento em tempo real** – canalize quadros diretamente de um stream ao vivo ao invés de ler do disco.  

Todas essas variações ainda giram em torno das ideias principais de **extrair quadros de vídeo**, **ler texto de vídeo**, e **extrair texto de mp4**.

## Conclusão

Acabamos de percorrer um fluxo de trabalho completo de **video subtitle ocr** em C#. Ao extrair quadros do vídeo, focar o OCR na faixa de legenda e iterar sobre os resultados, você pode ler **texto de vídeo** de forma confiável em arquivos como MP4. O código está pronto para copiar‑colar, e o design modular permite trocar por qualquer decodificador de quadros que preferir.

Próximos passos? Tente exportar os resultados para um arquivo SRT, experimente diferentes tamanhos de ROI, ou envie as legendas para uma API de tradução para legendas multilíngues. O céu é o limite depois que você dominar o básico de extração de texto de vídeo.

Feliz codificação, e que suas legendas estejam sempre cristalinas!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}