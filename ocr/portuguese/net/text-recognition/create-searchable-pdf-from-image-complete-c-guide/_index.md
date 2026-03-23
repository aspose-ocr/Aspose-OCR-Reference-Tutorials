---
category: general
date: 2026-03-23
description: Crie PDF pesquisável a partir de imagem usando o Aspose OCR. Aprenda
  como converter TIFF para PDF com alta compressão e reconhecer o texto da imagem
  em minutos.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: pt
og_description: Criar PDF pesquisável a partir de imagem com Aspose OCR. Este tutorial
  mostra como converter TIFF para PDF, adicionar uma camada de texto pesquisável e
  aplicar alta compressão.
og_title: Criar PDF pesquisável a partir de imagem – Guia completo de C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Criar PDF pesquisável a partir de imagem – Guia completo de C#
url: /pt/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem – Guia completo em C#

Já precisou **criar PDF pesquisável** a partir de um documento escaneado, mas não sabia por onde começar? Você não está sozinho — muitos desenvolvedores enfrentam o mesmo obstáculo ao transformar escaneamentos TIFF em PDFs pesquisáveis. A boa notícia? Com Aspose OCR você pode **converter tiff para pdf**, adicionar uma camada de texto oculta por cima e ainda reduzir o tamanho do arquivo com opções de **high compression pdf**, tudo em algumas linhas de C#.

Neste tutorial, percorreremos todo o processo: desde a instalação dos pacotes NuGet corretos, carregamento de uma imagem TIFF, reconhecimento do seu texto e, finalmente, exportação de um PDF pesquisável. Ao final, você terá um aplicativo de console executável que **recognize image text** e produz um PDF compacto e pesquisável pronto para indexação. Sem ferramentas extras, sem etapas manuais de OCR — apenas código limpo e um pouco de explicação.

## Pré-requisitos e o que você precisará

- **.NET 6+** (ou .NET Framework 4.6+). A API funciona em ambos, mas o .NET 6 oferece as melhorias mais recentes de runtime.  
- **Visual Studio 2022** ou qualquer IDE de sua preferência.  
- Pacotes NuGet **Aspose.OCR** e **Aspose.OCR.Gpu** (o pacote GPU é opcional, mas acelera o reconhecimento em hardware suportado).  
- Um arquivo TIFF de exemplo (por exemplo, `invoice.tif`) colocado em uma pasta que você controla.  

Se você já tem esses itens, ótimo — siga em frente. Caso contrário, a etapa de instalação abaixo cobrirá tudo.

## Etapa 1: Instalar pacotes Aspose OCR

Para começar, abra a pasta do seu projeto em um terminal e execute:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Esses comandos trazem tanto o motor OCR central quanto a biblioteca de aceleração GPU. Esta última não é obrigatória; o motor retornará ao modo CPU se não encontrar uma GPU compatível.  

> **Dica profissional:** Ao direcionar um ambiente de produção, fixe as versões dos pacotes no seu `csproj` para evitar alterações inesperadas que quebrem o código.

## Etapa 2: Configurar a estrutura do projeto

Crie um novo aplicativo de console (se ainda não tiver um):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Substitua o `Program.cs` gerado automaticamente pelo código completo mostrado mais adiante. O programa irá:

1. Inicializar um `OcrEngine` com suporte a GPU.  
2. Carregar a imagem TIFF.  
3. Executar OCR e abortar graciosamente em caso de falha.  
4. Configurar **PdfExportOptions** para uma camada pesquisável e **high compression**.  
5. Gravar o arquivo de saída.

## Etapa 3: Escrever o código completo (exemplo completo)

Abaixo está o arquivo fonte *inteiro*. Copie‑e cole em `Program.cs`. Os comentários explicam o “porquê” de cada linha, não apenas o “o quê”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Por que isso funciona

- **GPU acceleration** pode reduzir o tempo de reconhecimento de segundos para milissegundos em placas modernas — útil para processamento em lote.  
- **IncludeTextLayer** incorpora o texto derivado do OCR de forma invisível, permitindo que visualizadores de PDF pesquisem o documento sem alterar sua aparência visual.  
- **High compression** usa compressão Flate (ZIP) no fluxo de imagem, que é sem perdas mas reduz drasticamente o tamanho do arquivo — ideal para arquivar milhares de faturas.

## Etapa 4: Executar a aplicação e verificar a saída

Abra um terminal dentro da pasta do projeto e execute:

```bash
dotnet run
```

Se tudo estiver configurado corretamente, você verá:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Abra `invoice.pdf` em qualquer leitor de PDF (Adobe Acrobat, Edge ou até mesmo um navegador). Tente pesquisar por uma palavra que você sabe que aparece no TIFF original — por exemplo, “Total”. O visualizador deve destacar a palavra mesmo que ela faça parte da imagem. Esse é o sinal distintivo de um **searchable pdf**.

### Tamanho de arquivo esperado

Uma fatura escaneada típica (≈300 KB TIFF) costuma reduzir para **~80 KB** após aplicar `PdfCompression.High`. O tamanho exato depende da complexidade da imagem, mas você notará uma redução clara.

## Etapa 5: Variações comuns e casos de borda

| Situação | O que ajustar | Por quê |
|-----------|----------------|-----|
| **GPU não disponível** | Altere `new OcrEngine(GpuMode.Enabled)` para `new OcrEngine(GpuMode.Disabled)` | Impede que o motor tente inicializar a GPU, o que pode causar um pequeno atraso. |
| **Múltiplas páginas (TIFF multipágina)** | Defina `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Carrega todos os quadros; Aspose processará cada página e gerará um PDF multipágina. |
| **Necessita de idioma OCR diferente do inglês** | `ocrEngine.Language = Language.French;` (ou qualquer idioma suportado) | Melhora a precisão para documentos que não são em inglês. |
| **Deseja sobreposição de texto visível em vez de camada oculta** | `pdfExportOptions.IncludeTextLayer = false;` e adicione manualmente objetos `TextFragment`. | Útil quando você deseja que o texto OCR apareça como texto selecionável sobre a imagem. |
| **PDFs ultra‑pequenos** | Combine `PdfCompression.High` com `ImageResolution = 150` DPI antes do reconhecimento. | DPI mais baixo reduz os dados da imagem, diminuindo ainda mais o PDF ao custo da fidelidade visual. |

> **Nota:** Sempre teste casos de borda em uma amostra pequena antes de escalar para produção. A precisão do OCR pode variar com a qualidade da imagem, ruído e idioma.

## Etapa 6: Dicas para implementações prontas para produção

1. **Error Logging** – Substitua `Console.WriteLine` por um framework de logging adequado (Serilog, NLog) para diagnósticos mais fáceis.  
2. **Batch Processing** – Envolva a lógica central em um método que aceita caminhos de entrada/saída e, em seguida, itere sobre um diretório de arquivos TIFF.  
3. **Async I/O** – Embora o Aspose OCR seja síncrono, o carregamento e salvamento de arquivos podem ser assíncronos para manter as threads da UI responsivas.  
4. **Security** – Se você expor essa funcionalidade via uma API web, valide os caminhos dos arquivos e limite os tamanhos dos arquivos para evitar abusos.  
5. **Version Pinning** – Use números de versão exatos (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) para garantir comportamento consistente em todas as compilações.

## Conclusão

Acabamos de criar uma **solução completa, de ponta a ponta** que **create searchable pdf** arquivos a partir de imagens escaneadas, **convert tiff to pdf**, e faz isso com configurações de **high compression pdf** enquanto **recognize image text** com precisão. O **searchable pdf from image** resultante é leve, pesquisável e pronto para fluxos de trabalho subsequentes, como indexação, arquivamento ou e‑discovery.

Tem um lote de faturas? Conecte o método em um loop, aponte para uma pasta e deixe o Aspose OCR fazer o trabalho pesado. Quer experimentar diferentes níveis de compressão ou pacotes de idioma? O código é modular o suficiente para trocar essas opções em segundos.

---

*Pronto para evoluir?* Tente adicionar uma marca d'água, incorporar metadados ou até mesmo juntar vários PDFs processados por OCR. A suíte Aspose oferece muitas extensões — explore a documentação e mantenha o ritmo. Feliz codificação!

![Captura de tela do exemplo de criação de PDF pesquisável a partir de imagem](https://example.com/images/create-searchable-pdf.png "exemplo de pdf pesquisável")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}