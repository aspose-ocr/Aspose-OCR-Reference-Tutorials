---
category: general
date: 2026-02-28
description: Crie PDF pesquisável a partir de um TIFF multipágina em C#. Este guia
  mostra como converter imagem em PDF pesquisável com um exemplo completo de OCR em
  C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: pt
og_description: Crie PDF pesquisável a partir de um TIFF usando Aspose.OCR. Siga este
  exemplo passo a passo de OCR em C# para transformar imagens em PDFs pesquisáveis.
og_title: Criar PDF pesquisável em C# – Imagem para PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: Criar PDF pesquisável em C# – Imagem para PDF OCR
url: /pt/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável em C# – Imagem para PDF OCR

Já precisou **criar PDF pesquisável** a partir de um documento escaneado, mas não sabia por onde começar? Você não está sozinho. Em muitos fluxos de trabalho de escritório, um PDF pesquisável é a diferença entre um arquivo sem saída e um arquivo pesquisável.  

Neste tutorial, percorreremos um **exemplo c# ocr** completo que transforma um TIFF de várias páginas em um PDF pesquisável, tudo com Aspose.OCR. Ao final, você saberá exatamente como **imagem para pdf pesquisável**, como **converter tiff para pdf**, e terá um trecho de código pronto para executar que pode ser inserido em qualquer projeto .NET.

## O que você aprenderá

* Como instalar e referenciar o Aspose.OCR em um projeto C#.
* Os passos exatos para carregar um TIFF, definir o idioma e chamar `RecognizeToPdf`.
* Por que cada passo importa – desde o gerenciamento de memória até a seleção de idioma.
* Dicas para lidar com documentos grandes, solucionar problemas comuns de OCR e expandir a solução para outros formatos de imagem.

**Pré-requisitos** – um SDK .NET recente (4.6+ ou .NET Core 3.1+), Visual Studio (ou sua IDE favorita) e uma licença Aspose.OCR (a versão de avaliação gratuita funciona para testes). Nenhuma outra biblioteca externa é necessária.

---

## Criar PDF pesquisável – Visão geral

Em alto nível, o processo se parece com isto:

1. **Initialize** o `OcrEngine`.  
2. **Load** a imagem de origem (um TIFF no nosso caso).  
3. **Configure** as configurações de idioma para melhor precisão.  
4. **Run** OCR e **save** o resultado diretamente como um PDF pesquisável.  

É isso. A API Aspose faz o trabalho pesado, então você não precisa combinar bibliotecas separadas de OCR e PDF.

---

## Etapa 1: Instalar Aspose.OCR e configurar seu projeto

Primeiro, adicione o pacote NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

Ou, se preferir o Console do Gerenciador de Pacotes no Visual Studio:

```powershell
Install-Package Aspose.OCR
```

Depois que o pacote for restaurado, abra o arquivo do seu projeto e verifique a referência:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Dica profissional:** Use a versão estável mais recente (verifique o site da Aspose) para obter correções de bugs e os pacotes de idioma mais recentes.

---

## Etapa 2: Converter TIFF para PDF – Carregando a Imagem

Agora vamos carregar o TIFF que você deseja tornar pesquisável. O método `Image.Load` da Aspose suporta TIFFs de várias páginas nativamente.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Por que isso importa:** Carregar a imagem dentro de um bloco `using` garante que os recursos não gerenciados sejam liberados rapidamente — crucial ao processar documentos grandes.

---

## Etapa 3: Imagem para PDF pesquisável – Configuração do motor OCR

Antes de executar o OCR, informaremos ao motor qual idioma esperar. Inglês funciona na maioria dos casos, mas você pode trocar por qualquer valor do enum `OcrLanguage`.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Nota de especialista:** Selecionar o idioma correto reduz drasticamente os erros de reconhecimento. Se você tem idiomas mistos, pode combiná‑los com o operador `|`, por exemplo, `OcrLanguage.English | OcrLanguage.French`.

---

## Etapa 4: Exemplo C# OCR – Reconhecer e Salvar

Com o motor pronto, chame `RecognizeToPdf`. O método grava o PDF pesquisável diretamente no disco, incorporando uma camada de texto invisível atrás da imagem original.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Depois que esta linha for executada, `output.pdf` conterá as páginas originais do TIFF mais uma sobreposição de texto oculto que qualquer leitor de PDF pode pesquisar.

---

## Etapa 5: Imagem C# para PDF – Verificar o Resultado

Vamos confirmar que tudo funcionou. Abra o PDF gerado no Adobe Reader (ou qualquer visualizador) e tente buscar uma palavra que você sabe que aparece no TIFF de origem.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Se a busca retornar resultados, você criou com sucesso **pdf pesquisável** a partir de uma imagem. Caso contrário, verifique novamente a configuração de idioma ou a qualidade do TIFF de origem.

---

## Exemplo completo em funcionamento

Juntando todas as peças, aqui está um aplicativo console autônomo que você pode compilar e executar:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Saída esperada** (no console):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Abra `output.pdf` e você deverá conseguir digitar qualquer palavra do TIFF original na caixa de busca do visualizador e ver as correspondências destacadas.

---

![Exemplo de PDF pesquisável](placeholder-image.png){: .align-center alt="exemplo de pdf pesquisável"}

*A captura de tela acima mostra um PDF pesquisável aberto em um visualizador com a camada de texto oculto ativa.*

---

## Perguntas comuns e casos extremos

### E se o meu TIFF for enorme (centenas de páginas)?

Aspose.OCR transmite as páginas uma de cada vez, mas você ainda pode atingir limites de memória. Considere processar o TIFF em lotes:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Depois, mescle os PDFs por página com uma biblioteca PDF (por exemplo, Aspose.PDF).

### Posso exportar para um formato diferente, como DOCX pesquisável?

Sim—use `RecognizeToDocument` em vez de `RecognizeToPdf`. A API espelha o método PDF, basta mudar a extensão do arquivo de destino.

### Como lidar com idiomas diferentes do inglês?

Substitua `OcrLanguage.English` pelo enum apropriado, por exemplo `OcrLanguage.Spanish`. Você também pode combinar idiomas:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### E quanto a PDFs protegidos por senha?

Após a etapa de OCR, você pode abrir o PDF gerado com Aspose.PDF e aplicar criptografia:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Recapitulação

Cobremos tudo que você precisa para **criar PDFs pesquisáveis** a partir de imagens TIFF usando C#. Começando pela instalação do Aspose.OCR, carregamento da imagem, configuração de idioma, execução do OCR e, finalmente, verificação da saída pesquisável, agora você tem um sólido **exemplo c# ocr** que pode adaptar para outros formatos.  

Se você está pronto para avançar, experimente:

* **Converter TIFF para PDF** para arquivos não pesquisáveis (basta pular a etapa de OCR).  
* Experimente **imagem para pdf pesquisável**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}