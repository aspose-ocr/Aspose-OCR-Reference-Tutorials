---
category: general
date: 2026-09-19
description: O tutorial de OCR em Python mostra como converter PNG em texto usando
  o Aspose OCR. Aprenda extração de texto OCR em Python e extraia texto de imagens
  digitalizadas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: pt
lastmod: 2026-09-19
og_description: Tutorial de OCR em Python guia você na conversão de PNG para texto
  usando o Aspose OCR. Domine a extração de texto OCR em Python e extraia texto de
  imagens digitalizadas.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Tutorial de OCR em Python – converta PNG em texto com Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Tutorial de OCR em Python: converta PNG em texto com Aspose'
url: /pt/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de OCR em Python: converter PNG em texto com Aspose

Se você precisa de um **tutorial de OCR em python** que transforma uma imagem PNG em texto editável, este guia oferece uma solução completa e pronta‑para‑executar. Você verá como instalar a biblioteca Aspose OCR, carregar uma imagem, executar o motor de reconhecimento e imprimir os resultados — tudo em poucos passos concisos.

Digitalizar um documento e extrair o texto pode ser trabalhoso, especialmente quando você lida com formatos de imagem e configurações de idioma. Este tutorial elimina as dúvidas ao mostrar exatamente quais métodos chamar e por que eles são importantes, para que você possa focar na integração do OCR em suas próprias aplicações.

Você também aprenderá a **converter PNG em texto**, lidar com armadilhas comuns e adaptar o código para outros tipos de imagem, como JPEG ou TIFF. Ao final, será capaz de extrair texto de qualquer imagem escaneada com confiança.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8 ou mais recente instalado.
* Uma conexão com a internet para baixar o pacote Aspose OCR.
* Uma imagem PNG (ou qualquer formato suportado) que contenha texto legível.

Você **não** precisa de um motor OCR separado ou binários externos — o Aspose OCR inclui tudo que você precisa.

## Etapa 1: Instalar o pacote Aspose OCR

O primeiro passo é adicionar a biblioteca ao seu ambiente. A Aspose fornece um pacote puro‑Python que pode ser instalado via pip.

```bash
pip install aspose-ocr
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv venv`) para manter as dependências isoladas de outros projetos.

Instalar o pacote disponibiliza o módulo `aspose.ocr`, que contém a classe `OcrEngine` usada ao longo deste tutorial.

## Etapa 2: Importar a classe do motor OCR

Agora que o pacote está presente, importe a classe que conduz o processo de reconhecimento.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` encapsula toda a lógica para carregar imagens, configurar idioma e extrair texto. Importá‑la no início segue a prática padrão do Python e mantém o script organizado.

## Etapa 3: Criar uma instância do motor OCR

Criar uma instância fornece um motor novo com configurações padrão. Você pode personalizar propriedades como idioma ou pré‑processamento de imagem posteriormente.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Um novo objeto `engine` representa uma única sessão de OCR. Reutilizar a mesma instância para várias imagens pode melhorar o desempenho, pois recursos internos são armazenados em cache.

## Etapa 4: Carregar a imagem que você deseja processar

Especifique o caminho para o arquivo PNG que deseja converter. O método `load_image` aceita qualquer formato suportado pelo Aspose OCR, então você também pode passar arquivos JPEG, BMP ou TIFF.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Se o arquivo não for encontrado, `load_image` gera um `FileNotFoundError`. Envolva a chamada em um bloco try/except no código de produção para fornecer uma mensagem de erro amigável.

## Etapa 5: Executar OCR para extrair texto da imagem

Chamar `recognize` executa o pipeline de reconhecimento e devolve a string extraída. O método lida automaticamente com análise de layout, segmentação de caracteres e detecção de idioma (o padrão é Inglês).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Você pode mudar o idioma antes de chamar `recognize`:

```python
engine.language = "fr"   # for French text
```

Essa flexibilidade é útil quando você precisa de **extração de texto OCR python** para documentos multilíngues.

## Etapa 6: Exibir o texto reconhecido

Por fim, imprima ou armazene o resultado. Para uma verificação rápida, `print` exibe a string bruta no console.

```python
# Step 6: Output the recognized text
print(text)
```

### Saída esperada

Se `sample.png` contiver a frase “Hello, world!”, o console mostrará:

```
Hello, world!
```

A saída pode incluir quebras de linha ou espaços extras dependendo do layout original. Você pode pós‑processar a string com `str.strip()` ou expressões regulares para limpá‑la.

## Tratamento de casos comuns

### 1. Formatos que não são PNG

Embora este tutorial foque em **converter PNG em texto**, você pode receber arquivos JPEG ou TIFF. O mesmo código funciona; basta alterar a extensão do arquivo em `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Imagens de baixa resolução

A precisão do OCR cai abaixo de 150 dpi. Se você encontrar resultados ruins, aumente a resolução da imagem primeiro usando Pillow:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Extrair texto de uma imagem escaneada com múltiplos idiomas

Defina uma lista separada por vírgulas de códigos de idioma:

```python
engine.language = "en,es,de"
```

O Aspose OCR tentará reconhecer caracteres de todos os idiomas listados.

### 4. Documentos extensos

Processar muitas páginas em uma única execução pode esgotar a memória. Procure processar cada página individualmente:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Script completo e executável

Juntando todas as etapas, obtém‑se um programa autocontido que você pode copiar, colar e executar.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Execute o script com:

```bash
python python_ocr_tutorial.py
```

Você deverá ver o texto extraído impresso no console.

## Conclusão

Este **tutorial de OCR em python** demonstrou como **converter PNG em texto** usando Aspose OCR, abordando instalação, carregamento de imagem, reconhecimento e tratamento da saída. Agora você tem um padrão confiável para **extração de texto OCR python**, e pode adaptar o código para **extrair texto de imagem python** de qualquer documento escaneado.

A partir daqui, considere:

* Integrar o script a um serviço web (por exemplo, Flask) para oferecer OCR como API.
* Armazenar o texto extraído em um banco de dados para arquivos pesquisáveis.
* Experimentar diferentes configurações de idioma para lidar com digitalizações multilíngues.

Boa codificação e aproveite para transformar imagens em texto pesquisável e editável!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais, com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Converter Imagem em Texto: Extrair Texto de Imagem Usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Tutorial de OCR em Python: Extrair Texto de Tabelas de Imagens](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}