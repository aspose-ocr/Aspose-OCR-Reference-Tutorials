---
category: general
date: 2026-03-29
description: Como realizar OCR em C# e ler texto de arquivos PNG. Aprenda a extrair
  texto em russo, ler texto de PNG e como extrair texto usando Aspose OCR.
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: pt
og_description: Como realizar OCR em C# com Aspose OCR. Este guia mostra como ler
  texto de PNG, extrair texto em russo e implementar uma solução completa de OCR em
  C#.
og_title: Como Realizar OCR em C# – Extração Completa de Texto de PNG
tags:
- OCR
- C#
- Aspose
title: Como Realizar OCR em Imagens PNG em C# – Guia Passo a Passo
url: /pt/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em Imagens PNG no C# – Tutorial Completo

Já precisou **realizar OCR** em uma captura de tela ou documento escaneado e não sabia por onde começar no C#? Você não está sozinho. Desenvolvedores perguntam constantemente: “Como leio texto de arquivos PNG sem enviá‑los para um serviço externo?” A boa notícia é que, com o Aspose.OCR, você pode **extrair texto em russo**, **ler texto de png**, e obter uma string limpa de volta em apenas algumas linhas de código.

Neste tutorial vamos percorrer tudo que você precisa: configurar a biblioteca, escolher o modelo de idioma correto, executar o reconhecimento e lidar com armadilhas comuns. Ao final, você será capaz de **como extrair texto** de qualquer imagem PNG, seja em inglês, russo ou em qualquer um dos mais de 70 idiomas suportados pelo Aspose. Sem enrolação, apenas um exemplo prático e executável que você pode inserir em um aplicativo console agora mesmo.

---

## O Que Você Vai Aprender

- Instalar e referenciar o pacote NuGet Aspose.OCR.  
- Inicializar o motor OCR em seu modo padrão de auto‑download.  
- Configurar o motor para **extrair texto russo** usando o modelo de idioma cirílico.  
- Executar OCR em um arquivo PNG local e exibir o resultado.  
- Dicas para solucionar problemas de arquivos de idioma ausentes e melhorar a precisão.

**Pré‑requisitos**: .NET 6+ (ou .NET Framework 4.7.2+), Visual Studio 2022 ou VS Code, e conexão à internet para a primeira execução (o modelo de idioma é baixado automaticamente).

---

## Etapa 1 – Instalar o Pacote Aspose.OCR

Para começar, adicione a biblioteca Aspose.OCR ao seu projeto. Abra um terminal na pasta do projeto e execute:

```bash
dotnet add package Aspose.OCR
```

Ou, se preferir a interface do Visual Studio, clique com o botão direito em **Dependencies → Manage NuGet Packages**, procure por **Aspose.OCR** e clique em **Install**.

> **Dica profissional**: O pacote tem apenas alguns megabytes, e os modelos de idioma são obtidos sob demanda, então você não inflará seu aplicativo com arquivos desnecessários.

---

## Etapa 2 – Inicializar o Motor OCR (Palavra‑Chave Principal em Ação)

Criar o motor é simples. O construtor habilita automaticamente o *modo de auto‑download*, o que significa que, na primeira vez que você solicitar um idioma que não esteja presente localmente, o Aspose o baixará para você.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Por que isso importa**: Ao usar o modo padrão de auto‑download você evita manipulação manual de arquivos. Se mais tarde precisar **ler texto de png** em outro idioma, basta mudar `Language.RussianCyrillic` para o valor enum apropriado.

---

## Etapa 3 – Preparar Sua Imagem PNG

Certifique‑se de que a imagem que você deseja processar esteja acessível em tempo de execução. Coloque `sample_russian.png` na mesma pasta do `.exe` compilado, ou use um caminho absoluto se preferir. A imagem deve ser uma varredura ou captura de tela clara; a precisão do OCR cai drasticamente em PNGs desfocados ou fortemente comprimidos.

**Caso comum**: Se o PNG contiver múltiplos idiomas, você pode definir `ocrEngine.Language = Language.Multilingual;` para que o motor detecte cada bloco automaticamente.

---

## Etapa 4 – Executar o Aplicativo e Verificar a Saída

Compile e execute o programa:

```bash
dotnet run
```

Você deverá ver o texto russo extraído impresso no console, algo como:

```
Привет, мир! Это пример текста на русском языке.
```

Se receber uma string vazia, verifique:

1. Se o caminho do arquivo está correto.  
2. Se a imagem não está totalmente branca ou totalmente preta.  
3. Se o modelo de idioma foi baixado com sucesso (procure uma pasta `Aspose.OCR` no seu perfil de usuário).

---

## Etapa 5 – Ajustes Avançados para Melhor Precisão

Embora as configurações padrão funcionem na maioria dos casos, você pode querer afinar o motor:

| Configuração | O que faz | Quando usar |
|--------------|-----------|-------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | Corrige rotação leve | Documentos escaneados que não estão perfeitamente alinhados |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | Filtra ruídos de fundo | PNGs de baixa qualidade tirados com câmeras de celular |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | Limita os caracteres a dígitos | Extraindo números de faturas |

Adicione qualquer uma dessas linhas antes de chamar `RecognizeImage`:

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## Etapa 6 – Exportar Resultados para um Arquivo (Opcional)

Se precisar **como extrair texto** para um arquivo para processamento posterior, basta gravar o resultado no disco:

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

Agora você tem uma cópia persistente que pode ser inserida em um banco de dados, índice de busca ou motor de tradução.

---

## Perguntas Frequentes

**P: Isso funciona com outros formatos de imagem, como JPEG ou BMP?**  
R: Absolutamente. `RecognizeImage` aceita qualquer formato suportado pela biblioteca `System.Drawing` do .NET, incluindo JPEG, BMP e TIFF.

**P: E se eu precisar extrair texto em inglês na mesma execução?**  
R: Crie uma segunda instância de `OcrEngine` com `Language.English` ou altere a propriedade de idioma entre as chamadas.

**P: Posso executar OCR em uma Web API sem bloquear a thread principal?**  
R: Sim. Envolva a chamada de reconhecimento em `Task.Run` ou use a sobrecarga assíncrona `RecognizeImageAsync` (disponível nas versões mais recentes do Aspose).

**P: Existe um limite para o tamanho do PNG?**  
R: A biblioteca pode lidar com imagens grandes, mas o uso de memória cresce com a resolução. Se encontrar `OutOfMemoryException`, considere reduzir a escala da imagem primeiro.

---

## Exemplo Completo (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode colar em um novo projeto console (`dotnet new console`) e executar imediatamente após instalar o pacote NuGet.

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**Saída esperada no console** (supondo que o exemplo contenha a frase “Привет, мир!”):

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## Conclusão

Cobrimos **como realizar OCR** em imagens PNG usando C#, desde a instalação do Aspose.OCR até a personalização das opções de pré‑processamento e exportação dos resultados. Agora você sabe como **ler texto de png**, **como extrair texto** em diferentes idiomas e, especificamente, **extrair texto russo** com código mínimo.

Pronto para o próximo desafio? Experimente alimentar a saída do OCR em uma biblioteca de detecção de idioma, ou combine‑a com o Azure Cognitive Services para tradução. O céu é o limite quando você combina um motor OCR confiável com o poderoso ecossistema do C#.

Se este **c# ocr tutorial** foi útil, dê uma estrela, compartilhe com a equipe ou deixe um comentário com suas próprias dicas. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}