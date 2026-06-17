---
category: general
date: 2026-03-05
description: como usar OCR em C# para extrair texto de imagens de recibos. Aprenda
  como carregar a imagem para OCR e reconhecer a imagem do recibo em minutos.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: pt
og_description: como usar OCR em C# para extrair texto de recibos. Siga este guia
  passo a passo para carregar uma imagem para OCR e reconhecer a imagem do recibo
  de forma eficiente.
og_title: como usar OCR em C# – Extração rápida de texto de recibos
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Como usar OCR em C# – Extraia texto de recibos rapidamente
url: /pt/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como usar OCR em C# – Extrair Texto de Recibos Rapidamente

Já se perguntou **como usar OCR** para extrair dados diretamente de uma foto de um recibo de supermercado? Você não está sozinho. Em muitos aplicativos de pequenas empresas, o gargalo é transformar um PNG borrado em texto estruturado que você realmente pode usar.  

A boa notícia? Com algumas linhas de C# e Aspose.OCR você pode **carregar imagem para OCR**, executar o motor e **reconhecer imagem de recibo** em menos de um minuto. A seguir você verá um exemplo completo, pronto‑para‑executar, além de dicas para as partes complicadas que a maioria dos tutoriais ignora.

## O Que Este Guia Cobre

* Instalar o pacote NuGet Aspose.OCR.  
* Configurar o motor OCR – o núcleo de **como usar OCR** corretamente.  
* Carregar um arquivo de recibo (esse é o passo de **carregar imagem para OCR**).  
* Executar o processo de reconhecimento e extrair tanto os dados de layout JSON quanto XML.  
* Tratar armadilhas comuns, como licenças ausentes ou formatos de imagem não suportados.  

Ao final, você terá um programa autônomo que extrai o texto de qualquer recibo que você colocar em uma pasta. Sem serviços externos, sem mágica oculta.

## Pré‑requisitos

* .NET 6 SDK ou posterior (o código também compila com .NET Core).  
* Um arquivo de licença válido do Aspose.OCR (`Aspose.OCR.lic`). Você pode obter um teste gratuito da Aspose se ainda não tiver um.  
* Uma imagem de recibo de exemplo – `receipt.png` funciona bem, mas qualquer formato raster comum serve.  

Se você já tem tudo isso, ótimo – vamos mergulhar.

![exemplo de como usar OCR](https://example.com/ocr-receipt.png "exemplo de como usar OCR")

## Etapa 1: Instalar Aspose.OCR e Criar um Novo Projeto

Primeiro de tudo: você precisa da biblioteca que realmente faz o trabalho pesado. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Esse comando cria a estrutura de um aplicativo de console e traz o pacote mais recente do Aspose.OCR. Na minha experiência, manter o nome do projeto curto facilita a leitura dos caminhos gerados, especialmente quando você começa a lidar com vários aplicativos de demonstração.

## Etapa 2: Inicializar o Motor OCR – o Coração de **como usar OCR**

Agora vamos escrever o código que responde à pergunta “**como usar OCR** em C#”. Abra `Program.cs` e substitua seu conteúdo pelo trecho abaixo. Observe os comentários – eles explicam o *porquê* de cada linha, não apenas o *quê*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Por Que Isso Funciona

* **`OcrEngine`** é o ponto de entrada; ele contém todas as configurações que você pode ajustar posteriormente (idioma, DPI, etc.).  
* **`SetLicense`** remove a marca d'água de avaliação – um passo crucial quando você planeja distribuir o código.  
* **`ImageStream.FromFile`** realiza o trabalho de **carregar imagem para OCR**, lidando com PNG, JPEG, BMP, TIFF e mais.  
* **`Recognize()`** é o método que realmente **reconhece imagem de recibo**. Nos bastidores ele realiza binarização, segmentação e classificação de caracteres.  
* Exportar para JSON e XML fornece tanto um dump legível por humanos quanto uma estrutura amigável para máquinas que você pode alimentar em analisadores posteriores.

## Etapa 3: Executar a Demo e Verificar a Saída

Compile e execute:

```bash
dotnet run
```

Se tudo estiver configurado corretamente, você verá algo como:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

O console imprime o texto puro, enquanto `receipt.json` e `receipt.xml` contêm informações detalhadas de layout (coordenadas, pontuações de confiança, etc.). Esses arquivos são úteis se você precisar mapear cada linha para um campo de banco de dados posteriormente.

## Casos de Borda & Dicas Profissionais

### 1️⃣ Licença Ausente ou Inválida
Se `SetLicense` falhar, o motor recairá para o modo de avaliação e você receberá uma marca d'água na saída. Envolva a chamada em um try/catch e registre uma mensagem amigável:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Formatos de Imagem Não Suportados
Aspose.OCR suporta a maioria dos formatos raster, mas se você fornecer um PDF ou um TIFF de várias páginas, será necessário converter a página de interesse em uma imagem primeiro. A biblioteca `Aspose.PDF` pode lidar com essa conversão.

### 3️⃣ Recibos Grandes & Desempenho
Processar uma imagem de 10 MB pode ser lento. Reduza a resolução antes de enviá‑la ao motor:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

O método `Resize` mantém a proporção (`0` para altura) e reduz o tamanho do arquivo drasticamente sem sacrificar a precisão do OCR para recibos típicos.

### 4️⃣ Problemas de Idioma & Fonte
Recibos podem conter caracteres especiais (€, ¥, etc.). Defina o idioma explicitamente se você souber a localidade:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Para recibos de idiomas mistos, você pode habilitar o modo multilíngue:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Extraindo Dados Estruturados
O texto bruto é útil, mas a maioria dos aplicativos precisa de campos estruturados (data, total, itens). O layout JSON inclui coordenadas `BoundingBox` para cada palavra. Você pode pós‑processá‑lo assim:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Esse trecho demonstra a ideia; em produção você provavelmente usaria uma expressão regular ou um pequeno motor de regras.

## Perguntas Frequentes

**Q: Posso executar isso no Linux?**  
A: Absolutamente. Aspose.OCR é multiplataforma; basta instalar o runtime .NET na sua máquina Linux e o mesmo código funciona.

**Q: E se eu precisar processar dezenas de recibos por minuto?**  
A: Crie um loop `Parallel.ForEach` e reutilize uma única instância de `OcrEngine` – ele é thread‑safe para operações somente de leitura. Lembre‑se de lidar com os limites de concorrência da licença.

**Q: Isso funciona com fotos tiradas em dispositivos móveis em ângulo?**  
A: O motor inclui correção básica de inclinação, mas para imagens muito inclinadas você pode pré‑processar com uma biblioteca de processamento de imagens (por exemplo, OpenCV) para endireitar o recibo primeiro.

## Exemplo Completo (Copiar‑Colar)

Abaixo está o programa *inteiro* que você pode colocar em `Program.cs`. Nenhum outro arquivo é necessário além da licença e de uma imagem de recibo.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}