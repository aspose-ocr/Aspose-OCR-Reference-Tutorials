---
category: general
date: 2026-05-31
description: Crie PDF pesquisável a partir de imagens escaneadas usando OCR em Python.
  Aprenda como converter PDF de imagem escaneada, converter TIFF para PDF e adicionar
  camada de texto OCR em minutos.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: pt
og_description: Crie PDF pesquisável instantaneamente. Este guia mostra como executar
  OCR, converter PDF de imagem escaneada e adicionar camada de texto OCR usando um
  único script Python.
og_title: Criar PDF pesquisável com Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Criar PDF pesquisável com Python – Guia passo a passo
url: /pt/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável com Python – Guia passo a passo

Já se perguntou como **criar PDF pesquisável** a partir de uma página escaneada sem lidar com dezenas de ferramentas? Você não está sozinho. Em muitos fluxos de trabalho de escritório, um TIFF ou JPEG escaneado chega a uma unidade compartilhada, e a pessoa seguinte precisa copiar‑colar o texto manualmente — doloroso, propenso a erros e desperdiça tempo.  

Neste tutorial vamos percorrer uma solução limpa e programática que permite **converter PDF de imagem escaneada**, **converter TIFF para PDF** e **adicionar camada de texto OCR** de uma só vez. Ao final, você terá um script pronto‑para‑usar que executa OCR, incorpora o texto oculto e gera um PDF pesquisável que pode ser indexado, buscado ou compartilhado com confiança.

## O que você precisará

- Python 3.9+ (qualquer versão recente funciona)
- Pacotes `aspose-ocr` e `aspose-pdf` (instalados via `pip install aspose-ocr aspose-pdf`)
- Um arquivo de imagem escaneada (`.tif`, `.png`, `.jpg` ou até mesmo uma página PDF que seja apenas uma imagem)
- Uma quantidade modesta de RAM (o motor OCR é leve; até um laptop lida com ele)

> **Dica profissional:** Se você estiver no Windows, a maneira mais fácil de obter os pacotes é executar o comando em uma janela do PowerShell elevada.

```bash
pip install aspose-ocr aspose-pdf
```

Agora que os pré‑requisitos foram resolvidos, vamos mergulhar no código.

## Etapa 1: Criar uma Instância do Motor OCR – *create searchable pdf*

A primeira coisa que fazemos é iniciar o motor OCR. Pense nele como o cérebro que lerá cada pixel e o transformará em caracteres.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Por que isso importa:** Inicializar o motor apenas uma vez mantém o uso de memória baixo. Se você chamar `OcrEngine()` dentro de um loop para cada página, rapidamente ficará sem recursos.

## Etapa 2: Carregar a Imagem Escaneada – *convert tiff to pdf* & *convert scanned image pdf*

Em seguida, aponte o motor para o arquivo que deseja processar. A API aceita qualquer imagem raster, então um TIFF funciona tão bem quanto um JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Se você tiver um PDF que contém apenas uma imagem escaneada, ainda pode usar `load_image` porque o Aspose extrairá a primeira página automaticamente.

## Etapa 3: Configurar Opções de Salvamento de PDF – *add OCR text layer*

Aqui configuramos como o PDF final deve ficar. O parâmetro crucial é `create_searchable_pdf`; defini‑lo como `True` indica à biblioteca que incorpore uma camada de texto invisível que espelha o conteúdo visual.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **O que a camada de texto faz:** Quando você abre o arquivo resultante no Adobe Reader e tenta selecionar texto, verá os caracteres ocultos. Os mecanismos de busca também podem indexá‑los — perfeito para conformidade ou arquivamento.

## Etapa 4: Executar OCR e Salvar – *how to run OCR* in a single call

Agora a mágica acontece. Uma única chamada de método executa o motor de reconhecimento e grava o PDF pesquisável no disco.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

O método `recognize` devolve um objeto de status que você pode inspecionar para erros, mas na maioria dos cenários simples a chamada acima é suficiente.

### Saída esperada

Executar o script imprime:

```
PDF saved as searchable PDF.
```

Se você abrir `scanned_page_searchable.pdf` perceberá que pode selecionar texto, copiar‑colar e até executar uma busca `Ctrl+F`. Esse é o marco de um fluxo **create searchable pdf**.

## Script completo em funcionamento

Abaixo está o script completo, pronto‑para‑executar. Basta substituir os caminhos de placeholder pelos caminhos reais dos seus arquivos.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Salve isso como `create_searchable_pdf.py` e execute:

```bash
python create_searchable_pdf.py
```

## Perguntas comuns & casos de borda

### 1️⃣ Posso processar PDFs de múltiplas páginas?

Sim. Use `ocr_engine.load_image("file.pdf")` e então faça um loop sobre cada página com `ocr_engine.recognize(pdf_save_options, page_number)`. A biblioteca gerará automaticamente um PDF pesquisável de várias páginas.

### 2️⃣ E se meu arquivo de origem for um TIFF de alta resolução (300 dpi+)?

DPI mais alto gera melhor precisão de OCR, mas também maior uso de memória. Se você encontrar um `MemoryError`, reduza a escala da imagem primeiro:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Como altero o idioma do OCR?

Defina a propriedade `language` no motor antes de carregar a imagem:

```python
ocr_engine.language = "fra"   # French
```

Uma lista completa de códigos de idioma suportados está na documentação da Aspose.

### 4️⃣ E se eu precisar manter a qualidade original da imagem?

A classe `PdfSaveOptions` possui a propriedade `compression`. Defina‑a como `PdfCompression.None` para preservar os dados raster exatamente como estavam.

```python
pdf_save_options.compression = "None"
```

## Dicas para implantações prontas para produção

- **Processamento em lote:** Envolva a lógica principal em uma função que aceita uma lista de caminhos de arquivos. Registre cada sucesso/falha em um CSV para trilhas de auditoria.
- **Paralelismo:** Use `concurrent.futures.ThreadPoolExecutor` para executar OCR em múltiplos núcleos. Apenas lembre‑se de que cada thread precisa de sua própria instância `OcrEngine`.
- **Segurança:** Se você estiver lidando com documentos sensíveis, execute o script em um ambiente sandbox e exclua os arquivos temporários imediatamente após o processamento.

## Conclusão

Agora você sabe como **criar PDF pesquisável** a partir de imagens escaneadas usando um script Python conciso. Ao inicializar um motor OCR, carregar um TIFF (ou qualquer raster), configurar `PdfSaveOptions` para **add OCR text layer** e, finalmente, chamar `recognize`, todo o pipeline **convert scanned image pdf** e **convert TIFF to PDF** se torna um único comando repetível.

Próximos passos? Experimente encadear este script com um observador de arquivos para que qualquer nova digitalização deixada em uma pasta se torne automaticamente pesquisável. Ou experimente diferentes idiomas de OCR para suportar arquivos multilíngues. O céu é o limite quando você combina OCR com geração de PDF.

Tem mais perguntas sobre **how to run OCR** em outras linguagens ou frameworks? Deixe um comentário abaixo e feliz codificação! 

![Diagrama mostrando o fluxo de imagem escaneada → motor OCR → PDF pesquisável (create searchable pdf)](searchable-pdf-flow.png "Diagrama de fluxo criar PDF pesquisável")


## O que você deve aprender a seguir?

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}