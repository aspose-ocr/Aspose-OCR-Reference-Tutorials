---
category: general
date: 2026-02-11
description: Aprenda como executar OCR em um TIFF de várias páginas em C# usando Aspose
  OCR. Converta TIFF em texto, extraia texto de TIFF e reconheça texto de imagem rapidamente.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: pt
og_description: Como executar OCR em um TIFF multipágina usando Aspose OCR em C#.
  Guia passo a passo para converter TIFF em texto, extrair texto de TIFF e reconhecer
  texto a partir de imagem.
og_title: Como Executar OCR em Imagens TIFF de Múltiplas Páginas – Tutorial Completo
  em C#
tags:
- OCR
- C#
- Aspose
- TIFF
title: Como executar OCR em imagens TIFF de várias páginas com Aspose OCR – Guia C#
url: /pt/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR em Imagens TIFF de Múltiplas Páginas com Aspose OCR

Já se perguntou **como executar OCR** em um TIFF escaneado que contém várias páginas? Você não está sozinho—muitos desenvolvedores enfrentam esse problema quando precisam extrair texto pesquisável de documentos antigos. A boa notícia? Com Aspose OCR você pode reconhecer texto de arquivos de imagem em apenas algumas linhas de código C#, e obterá texto simples concatenado pronto para indexação ou processamento adicional.

Neste tutorial vamos percorrer todo o fluxo de trabalho: desde a instalação do pacote Aspose OCR, carregamento de um TIFF de múltiplas páginas, até a conversão de TIFF para texto e, finalmente, a exibição do conteúdo extraído. Ao final, você será capaz de **extrair texto de arquivos TIFF**, **reconhecer texto de imagem** e até automatizar o processo para dezenas de arquivos em um trabalho em lote. Sem mágica, apenas passos claros e práticos.

## O Que Você Vai Aprender

- Como configurar o motor Aspose OCR para reconhecimento de idioma inglês.  
- O código exato necessário para **converter TIFF para texto** usando a classe `OcrEngine`.  
- Dicas para lidar com imagens de múltiplas páginas e garantir que cada página seja separada corretamente.  
- Armadilhas comuns (como dependências nativas ausentes) e como evitá‑las.  

**Pré‑requisitos** – você precisará do .NET 6 ou superior, Visual Studio (ou qualquer editor C#) e uma conexão à internet para o recurso de download automático de recursos. É só isso; sem bibliotecas nativas extras para lidar.

---

## Etapa 1 – Instalar o Pacote NuGet Aspose OCR

Antes de poder **executar OCR em imagem** você deve adicionar a biblioteca ao seu projeto.

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se você estiver trabalhando dentro do Visual Studio, também pode clicar com o botão direito no projeto → *Manage NuGet Packages* → pesquisar por “Aspose.OCR” e clicar em *Install*.

O pacote inclui tudo que você precisa, e com `AutomaticResourceDownload = true` o motor buscará os pacotes de idioma automaticamente.

---

## Etapa 2 – Inicializar o Motor OCR (Como Executar OCR)

Agora que o pacote está instalado, criamos e configuramos uma instância de `OcrEngine`. Este é o coração de **como executar OCR** no nosso cenário.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Por que isso importa:** Definir `Language` informa ao motor qual conjunto de caracteres esperar, enquanto `AutomaticResourceDownload` evita que você precise colocar manualmente os arquivos de idioma no servidor. `OutputFormat` como `Text` nos fornece uma string simples—perfeito para pipelines de **converter TIFF para texto**.

---

## Etapa 3 – Carregar o TIFF de Múltiplas Páginas (Reconhecer Texto da Imagem)

Um TIFF pode conter muitos frames, cada um representando uma página. A classe `System.Drawing.Image` abstrai isso para nós.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **E se o arquivo não estiver na mesma pasta?** Basta fornecer um caminho absoluto completo ou usar `Path.Combine` com `AppContext.BaseDirectory`.  
> **E quanto ao uso de memória?** A instrução `using` descarta a imagem após o processamento, evitando vazamentos—crucial quando você processa em lote dezenas de TIFFs grandes.

A chamada `Recognize` itera automaticamente sobre cada página do TIFF, concatenando os resultados com quebras de linha. Por isso você verá cada página separada ao imprimir `ocrResult.Text`.

---

## Etapa 4 – Exemplo Completo (Todas as Etapas em Um Arquivo)

A seguir está um aplicativo console completo e pronto‑para‑executar. Copie‑e‑cole em um novo projeto console .NET e pressione **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Saída esperada** (truncada para brevidade):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Cada página aparece em sua própria linha porque `OcrOutputFormat.Text` insere uma quebra de linha entre os frames. Se precisar de um delimitador diferente, você pode pós‑processar `result.Text` com `String.Replace`.

---

## Etapa 5 – Tratando Casos de Borda Comuns

### 5.1 Large TIFF Files  
Ao lidar com TIFFs de tamanho gigabyte, carregar o arquivo inteiro na memória pode ser problemático. Uma solução alternativa é processar cada frame individualmente:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Non‑English Documents  
Se precisar **reconhecer texto de imagem** em espanhol ou francês, basta alterar a propriedade `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose baixará automaticamente os recursos de idioma apropriados.

### 5. Saving the Output  
Frequentemente você desejará **converter TIFF para texto** e armazenar o resultado em um arquivo `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Você também pode dividir a saída por página usando `String.Split(Environment.NewLine)` e gravar cada fatia em um arquivo separado.

---

## Dicas Profissionais & Armadilhas

- **AutomaticResourceDownload** funciona na primeira execução do aplicativo; execuções subsequentes são offline.  
- Se aparecerem caracteres estranhos, verifique novamente a configuração `Language`; pacotes de idioma incompatíveis causam reconhecimento incorreto.  
- Para PDFs que foram rasterizados em TIFFs, pode ser interessante aumentar `ocrEngine.Dpi` (o padrão é 300) para melhorar a precisão.  
- Sempre envolva `Image.FromFile` em um bloco `using`; caso contrário o arquivo ficará bloqueado e não poderá ser excluído ou movido depois.

---

## Perguntas Frequentes

**Q: Isso funciona com TIFFs de página única?**  
A: Absolutamente. O motor trata um TIFF de frame único da mesma forma; você receberá apenas uma linha de texto.

**Q: Posso processar arquivos PNG ou JPEG da mesma maneira?**  
A: Sim—basta mudar a extensão do arquivo. O método `Recognize` aceita qualquer formato `System.Drawing.Image`.

**Q: E se eu precisar do resultado OCR como PDF em vez de texto simples?**  
A: Defina `OutputFormat = OcrOutputFormat.Pdf` e o `ocrResult` conterá um array de bytes PDF que você pode gravar no disco.

---

## Conclusão

Agora você tem uma solução completa, de ponta a ponta, para **como executar OCR** em arquivos TIFF de múltiplas páginas usando Aspose OCR em C#. Ao configurar o motor, carregar a imagem e invocar `Recognize`, você pode **extrair texto de TIFF**, **converter TIFF para texto** e **reconhecer texto de imagem** com apenas algumas linhas de código. Sinta‑se à vontade para ajustar o idioma, o formato de saída ou o processamento frame‑a‑frame para atender às suas necessidades de processamento em lote.

Pronto para o próximo passo? Experimente combinar esta abordagem com um serviço de monitoramento de pastas para **executar OCR automaticamente em imagens** assim que chegarem a uma pasta de entrada, ou integre a saída em um índice de busca para pesquisa de texto completo instantânea. As possibilidades são infinitas, e o código que você acabou de ver é uma base sólida.

Se encontrou algum problema, deixe um comentário abaixo ou me avise no GitHub. Boa codificação e aproveite para transformar aqueles TIFFs teimosos em texto pesquisável!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}