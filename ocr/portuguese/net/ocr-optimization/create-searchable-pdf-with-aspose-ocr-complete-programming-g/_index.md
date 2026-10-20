---
category: general
date: 2026-05-21
description: Crie PDF pesquisável usando Aspose OCR enquanto melhora a precisão do
  OCR e aprende como carregar imagem para OCR em C#. Tutorial passo a passo.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: pt
og_description: Crie PDF pesquisável com Aspose OCR. Aprenda como melhorar a precisão
  do OCR e carregar a imagem para OCR em um único exemplo executável.
og_title: Crie PDF pesquisável com Aspose OCR – Guia completo
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Criar PDF pesquisável com Aspose OCR – Guia completo de programação
url: /pt/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável com Aspose OCR – Guia de Programação Completo

Já precisou **criar PDF pesquisável** a partir de uma imagem escaneada, mas não sabia por onde começar? Você não está sozinho — muitos desenvolvedores encontram essa barreira ao iniciar projetos de OCR. A boa notícia é que o Aspose OCR torna todo o pipeline — carregar a imagem, aprimorar a foto para obter melhores resultados e, finalmente, salvar um PDF pesquisável — bastante simples.

Neste guia percorreremos um exemplo completo, de ponta a ponta, que não só mostra **como criar PDF pesquisável**, mas também demonstra como **melhorar a precisão do OCR** e a maneira correta de **carregar imagem para OCR**. Ao final, você terá um aplicativo console C# pronto para executar que gera um PDF pesquisável com a imagem original incorporada.

## O que você vai aprender

- Configurar o Aspose OCR (incluindo aceleração opcional por GPU)  
- Configurar o motor para francês (ou qualquer idioma) para **melhorar a precisão do OCR**  
- **Carregar imagem para OCR** corretamente usando `ImageStream`  
- Construir um pipeline de filtros para limpar a imagem antes do reconhecimento  
- Salvar o resultado como PDF pesquisável com a imagem fonte incorporada  

Nenhuma dependência externa além do Aspose OCR é necessária, e o código funciona em .NET 6+ (ou .NET Framework 4.6+). Vamos lá.

---

![Exemplo de PDF pesquisável gerado pelo Aspose OCR – criar PDF pesquisável](images/searchable-pdf-sample.png "exemplo de criar PDF pesquisável")

## Etapa 1: Criar PDF pesquisável – Ativar GPU e definir caminho de recursos  

Se você possui uma GPU compatível, ativá‑la pode acelerar o reconhecimento drasticamente. Mesmo que você ignore esta etapa, o restante do código funciona normalmente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Por que isso importa:** A aceleração por GPU reduz a latência em lotes grandes, e definir o caminho de recursos garante que o motor possa funcionar sem conexão com a internet — perfeito para pipelines de CI ou ambientes isolados.

> **Dica de especialista:** Se você estiver em um servidor sem interface gráfica, verifique se os drivers CUDA correspondem à versão incluída no Aspose OCR; versões incompatíveis podem causar falhas silenciosas.

## Etapa 2: Melhorar a precisão do OCR – Escolher o idioma correto  

Selecionar o modelo de idioma correto é um ganho rápido de precisão. Aqui escolhemos francês, mas você pode substituir `OcrLanguage.French` por qualquer idioma suportado.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Por que isso importa:** Dicionários específicos de idioma ajudam o motor a resolver caracteres ambíguos (ex.: “œ” vs “oe”). Se você pular esta etapa, o motor usará inglês por padrão, o que pode reduzir drasticamente a **precisão do OCR** para textos não‑inglês.

## Etapa 3: Carregar imagem para OCR – Usando ImageStream  

Agora vamos **carregar imagem para OCR**. O helper `ImageStream.FromFile` abstrai o manuseio bruto de bitmap e funciona com a maioria dos formatos comuns (JPG, PNG, TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Por que isso importa:** Carregar a imagem dessa forma garante que o Aspose receba o arquivo em um formato que ele pode processar eficientemente. Se você tentar fornecer um `Bitmap` bruto diretamente, pode encontrar problemas de gerenciamento de memória em arquivos grandes.

## Etapa 4: Construir um pipeline de filtros de imagem para aumentar a precisão  

Uma imagem limpa é metade da batalha. O pipeline abaixo corrige a inclinação da foto e remove ruído de fundo — dois culpados clássicos que sabotam a **precisão do OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Por que isso importa:** A correção de inclinação garante que as linhas de texto fiquem horizontais, enquanto a remoção de ruído reduz manchas falsas de caracteres. Você pode adicionar mais filtros (ex.: `ContrastFilter`) se suas digitalizações forem especialmente ruins.

## Etapa 5: Executar o reconhecimento OCR  

Com a imagem pré‑processada, finalmente deixamos o motor fazer a sua mágica.

```csharp
ocrEngine.Recognize();
```

Essa única linha dispara o modelo de deep‑learning por trás do Aspose OCR. Ela preenche `ocrEngine.Text` com texto simples e também prepara a saída em PDF.

> **E se o texto aparecer confuso?** Verifique novamente a configuração de idioma da Etapa 2 e considere adicionar um `BinarizeFilter` ao pipeline.

## Etapa 6: Salvar o resultado como PDF pesquisável  

A última etapa é salvar um **PDF pesquisável** onde o texto extraído fica atrás da imagem original — exatamente o que você precisa para documentos legais ou arquivamento.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Por que isso importa:** `EmbedOriginalImage = true` mantém a fidelidade visual da digitalização enquanto ainda permite a busca por texto. Se você definir como `false`, o PDF conterá apenas o texto extraído, o que pode ser útil para arquivos leves.

### Opcional: Imprimir texto reconhecido e JSON  

Se quiser inspecionar a saída bruta, estas linhas exibem o texto simples e um payload JSON estruturado.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Saída esperada:** Após executar o programa, você verá a(s) frase(s) em francês impressa(s) no console, seguida(s) de um objeto JSON contendo caixas delimitadoras, pontuações de confiança e metadados de idioma.

---

## Exemplo completo (pronto para copiar e colar)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Execute o programa, aponte `YOUR_DIRECTORY` para uma pasta que contenha `input.jpg` e os recursos do Aspose OCR, e você obterá `output.pdf` ao lado.

---

## Conclusão

Agora você tem uma receita sólida e pronta para produção para **criar PDF pesquisável** com Aspose OCR, enquanto aprende a **melhorar a precisão do OCR** e a **carregar imagem para OCR** corretamente. O pipeline — GPU (opcional) → seleção de idioma → carregamento da imagem → cadeia de filtros → reconhecimento → salvamento em PDF — cobre todas as etapas críticas, permitindo que você o adapte para outros idiomas, lotes maiores ou formatos de saída diferentes.

Qual o próximo passo? Experimente trocar `PdfSaveOptions` por `DocxSaveOptions` para gerar documentos Word pesquisáveis, teste filtros adicionais como `ContrastFilter`, ou integre este código em uma API ASP.NET Core para geração de PDF sob demanda. As possibilidades são infinitas, e com a base estabelecida aqui, você está bem equipado para enfrentar qualquer desafio relacionado a OCR.

Tem dúvidas ou encontrou algum obstáculo? Deixe um comentário, e feliz codificação!

## Tutoriais relacionados

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}