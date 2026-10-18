---
category: general
date: 2026-06-06
description: Como fazer OCR de PDF usando o Aspose OCR Cloud. Aprenda a extrair texto
  de PDF, converter página de PDF em PNG e salvar imagens de páginas de PDF em Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: pt
og_description: Como fazer OCR de PDF com Aspose OCR Cloud. Este guia mostra como
  extrair texto simples de PDF, converter página de PDF em PNG e salvar imagens das
  páginas do PDF.
og_title: Como fazer OCR de PDF com Aspose OCR Cloud – Passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Como fazer OCR de PDF com Aspose OCR Cloud – Guia Completo
url: /pt/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em PDF com Aspose OCR Cloud – Guia Completo

Já se perguntou **como fazer OCR em PDF** sem precisar lidar com ferramentas pesadas de desktop? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo quando precisam de uma maneira rápida e programática de extrair texto de documentos escaneados. A boa notícia? Com o Aspose OCR Cloud você pode **extrair texto de PDF**, transformar cada página em PNG e até **salvar imagens de páginas PDF** para uso posterior, tudo a partir de um script Python organizado.

Neste tutorial vamos percorrer tudo o que você precisa saber: desde a instalação do SDK, licenciamento do motor, e reconhecimento de PDFs com várias páginas, até a extração de texto puro, conversão de páginas para PNG e persistência dessas imagens em disco. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto que precise de **como fazer OCR em PDF**.

## O que você vai precisar

- **Python 3.8+** (o código funciona também em 3.10 e versões mais recentes)  
- Uma conta no Aspose OCR Cloud – você receberá um arquivo de licença de teste gratuito (`Aspose.OCR.lic`)  
- O pacote `asposeocrcloud` (`pip install asposeocrcloud`)  
- Um PDF escaneado, com várias páginas, que você deseja processar  

É só isso. Sem binários extras, sem dependências nativas, apenas Python puro.

## Como fazer OCR em PDF – Configuração e Licença

Antes de chamar qualquer método de OCR, você precisa informar ao SDK quem você é. O Aspose usa um arquivo de licença leve que você coloca em um local acessível ao seu script.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Dica:* Se você pular a etapa de licença, o SDK ainda funcionará, mas inserirá uma pequena marca d'água nas imagens de saída. Não é ideal para produção.

## Etapa 2: Instalar o SDK Python Aspose OCR Cloud

Abra um terminal e execute:

```bash
pip install asposeocrcloud
```

O pacote traz todas as dependências necessárias (requests, pillow, etc.) para que você não precise procurar nada mais.

## Etapa 3: Criar um Motor OCR e Escolher um Idioma

O motor é o coração da operação. Você pode especificar qualquer idioma suportado pelo Aspose; o inglês funciona na maioria dos casos.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Por que definir o idioma? Porque o motor OCR usa dicionários específicos de idioma para melhorar a precisão. Se você estiver processando PDFs em francês, basta trocar `ENGLISH` por `FRENCH`.

## Etapa 4: Apontar para o seu PDF de Múltiplas Páginas

Forneça ao motor o caminho completo do arquivo que você deseja processar. Caminhos relativos são aceitos, desde que resolvam a partir do diretório de trabalho do script.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Certifique‑se de que o arquivo seja legível; caso contrário, você verá um `FileNotFoundError`.

## Etapa 5: Executar OCR – Você Recebe uma Lista de Resultados

Chamar `recognize_pdf` retorna uma lista onde cada elemento corresponde a uma página do PDF de origem.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Cada `OcrResult` contém duas propriedades úteis:

* `text` – a representação em texto puro da página (ótimo para **extrair texto puro de pdf**)  
* `image` – um objeto Pillow `Image` da página renderizada (perfeito para **converter página pdf png**)

## Etapa 6: Extrair Texto do PDF e Converter Páginas para PNG

Agora percorremos os resultados, imprimimos o texto extraído e salvamos uma versão PNG de cada página.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Saída Esperada no Console

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Você também encontrará `page_1.png`, `page_2.png`, … dentro de `YOUR_DIRECTORY`. Essas são as imagens rasterizadas das páginas que podem ser alimentadas em pipelines de processamento de imagem posteriores.

## Etapa 7: Salvar Imagens de Páginas PDF (Processamento Opcional)

Se você precisar apenas das imagens e não do texto, pode pular a linha `print(res.text)`. Por outro lado, se quiser armazenar o texto em arquivos `.txt` separados, basta acrescentar uma pequena gravação:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Esta pequena adição demonstra como é fácil **salvar imagens de páginas PDF** enquanto também persiste o conteúdo extraído.

## Exemplo Completo Funcional

Juntando tudo, aqui está o script completo que você pode copiar‑colar em `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Execute-o com:

```bash
python ocr_pdf.py
```

Você deverá ver a impressão no console do texto de cada página e uma série de arquivos PNG.


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}