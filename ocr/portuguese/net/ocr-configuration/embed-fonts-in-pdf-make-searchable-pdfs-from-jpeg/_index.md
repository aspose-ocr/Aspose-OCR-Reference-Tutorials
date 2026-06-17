---
category: general
date: 2026-03-05
description: Incorpore fontes no PDF ao converter um JPEG em PDF pesquisável usando
  o Aspose OCR. Aprenda como reconhecer texto a partir de JPEG e incorporar fontes
  para conformidade com PDF/A‑2b.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: pt
og_description: Incorpore fontes em PDF ao transformar um JPEG em PDF pesquisável.
  Este guia passo a passo mostra como reconhecer texto a partir de JPEG e criar arquivos
  compatíveis com PDF/A‑2b.
og_title: Incorporar fontes em PDF – Crie PDFs pesquisáveis a partir de JPEG
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: Incorporar fontes em PDF – Criar PDFs pesquisáveis a partir de JPEG
url: /pt/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporar fontes em PDF – Crie PDFs pesquisáveis a partir de JPEG

Já precisou **incorporar fontes em PDF** que foram gerados a partir de imagens digitalizadas? Você não está sozinho. A maioria dos desenvolvedores encontra o problema onde o PDF resultante parece bom na sua máquina, mas mostra texto ausente quando aberto em outro lugar porque as fontes não foram incorporadas.  

A boa notícia? Com o Aspose OCR você pode **reconhecer texto de JPEG**, incorporar as fontes necessárias e gerar um documento PDF/A‑2b totalmente pesquisável em apenas algumas linhas de C#. Neste tutorial, percorreremos cada passo — por que cada configuração importa, como evitar armadilhas comuns e como o PDF final deve ficar.

Ao final deste guia, você será capaz de **converter imagem em PDF pesquisável**, incorporar fontes corretamente e entender como **executar OCR em arquivos de imagem** programaticamente.

---

## O que você precisará

- **Aspose.OCR for .NET** (última versão, por exemplo, 23.10) – a biblioteca que faz o trabalho pesado.
- Um arquivo de licença **Aspose OCR válido** (`Aspose.OCR.lic`). O teste gratuito funciona, mas uma versão licenciada remove as marcas d'água de avaliação.
- Uma imagem JPEG (`input.jpg`) que contém texto impresso ou digitado.
- Um ambiente de desenvolvimento .NET (Visual Studio, Rider ou VS Code com a extensão C#).

Nenhum pacote NuGet adicional é necessário; o mecanismo OCR já inclui as utilidades de geração de PDF.

## Etapa 1: Configurar o mecanismo OCR e aplicar a licença *(Incorporar fontes em PDF)*

Antes de executar qualquer reconhecimento, você deve criar uma instância de `OcrEngine` e informar qual licença usar. Pular a etapa de licença fará com que o mecanismo rode em modo de avaliação, o que adiciona uma sobreposição “Powered by Aspose” em cada página.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Por que isso importa:** A licença não apenas remove as marcas d'água, mas também desbloqueia opções de conformidade PDF/A que precisaremos mais tarde para incorporar fontes.

## Etapa 2: Carregar a imagem JPEG que você deseja processar *(Reconhecer texto de JPEG)*

O mecanismo OCR trabalha com a propriedade `Image` que aceita um `ImageStream`. Aponte para o JPEG que você deseja converter.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**Dica:** Se sua imagem está em um stream (por exemplo, enviada via API), você pode usar `ImageStream.FromStream(yourStream)` em vez de `FromFile`.

## Etapa 3: Configurar as opções de salvamento PDF para um PDF pesquisável

Este é o cerne do requisito “incorporar fontes em PDF”. Usaremos `PdfSaveOptions` para:

1. Alvo **PDF/A‑2b** (um padrão de arquivamento amplamente aceito).
2. **Incorporar todas as fontes usadas** para que o PDF seja renderizado da mesma forma em qualquer lugar.
3. Aplicar **compressão Flate sem perdas** para manter o tamanho do arquivo razoável.
4. Manter o JPEG original como camada de fundo, o que preserva a fidelidade visual.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**Por que essas configurações?**  
- **PdfAStandard.PdfA2b** garante preservação a longo prazo e força a incorporação de fontes.  
- **EmbedFonts = true** é a flag explícita que satisfaz o objetivo principal da palavra‑chave.  
- **Compression.Flate** reduz o tamanho sem sacrificar a qualidade.  
- **RenderOriginalImage** mantém a aparência visual da página escaneada enquanto a camada OCR oculta fornece texto pesquisável.

## Etapa 4: Executar o reconhecimento OCR na imagem *(Executar OCR em imagem)*

Com tudo preparado, inicie o reconhecimento. O mecanismo analisará o JPEG, extrairá os caracteres e criará internamente uma camada de texto.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**Pergunta comum:** *Preciso especificar idioma ou dicionário?*  
Se seu documento não for em inglês, defina `ocrEngine.Language = OcrLanguage.French;` (ou qualquer idioma suportado) antes de chamar `Recognize()`. O padrão é inglês.

## Etapa 5: Salvar a saída como PDF pesquisável com fontes incorporadas

Finalmente, escreva o resultado no disco. O método `Save` recebe o caminho de destino e o `PdfSaveOptions` que definimos anteriormente.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

Ao abrir `output.pdf` no Adobe Acrobat ou em qualquer visualizador de PDF, você deverá poder:

- **Pesquisar** por qualquer palavra que apareceu no JPEG original.
- Ver **nenhum aviso de fonte ausente** (graças a `EmbedFonts = true`).
- Verificar que o arquivo está em conformidade com **PDF/A‑2b** (Arquivo → Propriedades → PDF/A).

## Exemplo completo em funcionamento

Abaixo está o programa completo, pronto‑para‑executar. Copie‑e‑cole em um novo projeto de Console App, ajuste os caminhos dos arquivos e pressione **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**Saída esperada:**  
O console imprime uma mensagem de sucesso, e `output.pdf` aparece na pasta de destino. Ao abrir o PDF e usar a caixa de pesquisa do visualizador, deve localizar qualquer palavra que estava presente em `input.jpg`.

## Perguntas Frequentes & Casos Limite

### 1. “E se meu JPEG for um TIFF de múltiplas páginas?”

O Aspose OCR trata cada página separadamente. Converta o TIFF em uma série de JPEGs (ou use `ImageStream.FromFile` em cada página) e faça um loop no processo OCR, anexando cada resultado ao mesmo PDF reutilizando a mesma instância de `OcrEngine`.

### 2. “Posso controlar o DPI ou o pré‑processamento da imagem?”

Sim. Antes de chamar `Recognize()`, você pode ajustar a resolução da imagem:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

Um DPI mais alto costuma gerar melhor precisão de reconhecimento, especialmente para fontes pequenas.

### 3. “Meu PDF ainda mostra fontes ausentes no Adobe Reader — o que há de errado?”

Certifique‑se de que está direcionando **PDF/A‑2b** e que `EmbedFonts` está definido como `true`. Se você alterou manualmente `PdfAStandard` para `None`, a etapa de validação PDF/A é ignorada e algumas fontes podem permanecer não incorporadas.

### 4. “A camada OCR é pesquisável em dispositivos móveis?”

Absolutamente. A camada de texto oculta faz parte da especificação PDF, portanto, qualquer visualizador de PDF que suporte extração de texto (incluindo iOS Files, Android PDF Viewer, etc.) permitirá que os usuários pesquisem.

### 5. “Como lidar com idiomas da direita para a esquerda, como o árabe?”

Defina o idioma antes do reconhecimento:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

O Aspose OCR troca automaticamente a direção do texto e incorpora as fontes apropriadas quando `EmbedFonts` é true.

## Dicas Profissionais & Armadilhas Comuns

- **Dica profissional:** Se suas imagens de origem são fotografias coloridas, considere convertê‑las para escala de cinza primeiro (`ocrEngine.Image.ConvertToGrayscale();`). Isso reduz o tamanho do arquivo sem prejudicar a precisão do OCR.
- **Cuidado:** Usar a licença de teste gratuito com uma imagem **grande** pode fazer o mecanismo truncar o texto OCR. Atualize para uma licença completa para cargas de trabalho de produção.
- **Dica de desempenho:** Reutilizar a mesma instância de `OcrEngine` em várias imagens evita a sobrecarga de carregar repetidamente as DLLs do OCR.
- **Nota de segurança:** Arquivos PDF/A‑2b são **somente‑leitura** por design, o que ajuda a prevenir injeção acidental de scripts — um bônus agradável para ambientes com alta exigência de conformidade.

## Conclusão

Cobrimos todo o pipeline para **incorporar fontes em PDF** enquanto **reconhecemos texto de JPEG** e produzimos um **PDF pesquisável** que atende aos padrões PDF/A‑2b. O processo resume‑se a:

1. Inicializar `OcrEngine` e aplicar sua licença.  
2. Carregar a imagem JPEG.  
3. Configurar `PdfSaveOptions` (incorporar fontes, PDF/A‑2b, compressão).  
4. Executar `Recognize()`.  
5. Salvar com as opções configuradas.

Agora você pode integrar esse fluxo em serviços web, utilitários de desktop ou jobs em lote que precisem **converter imagem em PDF pesquisável** em tempo real. Em seguida, você pode explorar **como criar PDF pesquisável** a partir de PDFs de múltiplas páginas ou PDFs gerados

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}