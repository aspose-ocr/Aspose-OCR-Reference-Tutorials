---
category: general
date: 2026-06-22
description: Obtenha coordenadas de caixas delimitadoras de imagens usando Python.
  Aprenda como extrair texto de imagens com Python usando Aspose OCR e análise de
  JSON em minutos.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: pt
og_description: Obtenha coordenadas de caixa delimitadora a partir de imagens usando
  Python. Este guia mostra como extrair texto de imagens com Python usando Aspose
  OCR e analisar dados de layout.
og_title: Obtenha as coordenadas da caixa delimitadora do OCR em Python – Tutorial
  completo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Obtenha as coordenadas da caixa delimitadora a partir de OCR em Python – Guia
  completo
url: /pt/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter Coordenadas da Caixa Delimitadora a partir de OCR em Python – Guia Completo

Já precisou **obter coordenadas da caixa delimitadora** para cada palavra em uma nota fiscal escaneada, mas não sabia por onde começar? Você não está sozinho. Em muitos projetos de automação, é necessário localizar texto em uma imagem para destacar, ocultar ou alimentar análises posteriores. A boa notícia? Com algumas linhas de Python e Aspose.OCR você pode extrair tanto o texto **quanto** sua posição exata em uma única passagem.

Neste tutorial, vamos percorrer um exemplo prático que mostra como **extrair texto de imagem no estilo python**, e então mergulhar nos dados de layout JSON para obter essas caixas delimitadoras. Sem enrolação, apenas um script funcional, explicações do porquê de cada passo e dicas para evitar armadilhas comuns.

---

## O que Você Vai Construir

Ao final deste guia, você terá um script Python pronto‑para‑executar que:

1. Carrega uma imagem (por exemplo, um PNG de nota fiscal) no Aspose OCR.
2. Configura o motor para emitir informações de layout em JSON.
3. Analisa o JSON em um dicionário Python.
4. Itera sobre cada palavra reconhecida, imprimindo seu texto **e** as coordenadas da caixa delimitadora.

Você também verá como adaptar o código para PDFs de várias páginas, diferentes formatos de imagem e sistemas de coordenadas personalizados.

### Pré-requisitos

- Python 3.8+ instalado na sua máquina.  
- Uma licença ativa do Aspose.OCR para Python ou um teste gratuito (a biblioteca funciona sem licença, mas adiciona uma marca d'água).  
- `pip install aspose-ocr` (o nome do pacote no PyPI).  
- Uma imagem de exemplo chamada `invoice.png` colocada em uma pasta que você possa referenciar.

É isso — sem frameworks pesados, sem serviços externos. Vamos mergulhar.

---

## Etapa 1: Instalar e Importar as Bibliotecas Necessárias

Primeiro, certifique-se de que o pacote Aspose OCR e o módulo interno `json` estejam disponíveis. O módulo `json` vem com o Python, portanto só precisamos instalar o Aspose.

```bash
pip install aspose-ocr
```

Agora importe‑os no seu script:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Por que isso importa:** Importar `aspose.ocr` fornece acesso ao motor OCR de alto desempenho, enquanto `json` permite transformar a string de layout bruta em um dicionário Python nativo para fácil navegação.

---

## Etapa 2: Criar o Motor OCR e Carregar Sua Imagem

O motor é o coração do processo. Você o instancia e, em seguida, aponta para a imagem que deseja escanear.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Dica profissional:** Substitua `"YOUR_DIRECTORY/invoice.png"` por um caminho absoluto ou relativo que aponte para o seu arquivo real. Se o arquivo não for encontrado, o Aspose lançará um `FileNotFoundError`, então verifique a ortografia.

---

## Etapa 3: Configurar o Motor para Emitir Dados de Layout em JSON

O Aspose OCR pode retornar texto simples, JSON apenas de OCR ou um JSON de layout completo que inclui coordenadas para palavras, linhas e até caracteres individuais. Para **obter coordenadas da caixa delimitadora**, precisamos do JSON de layout.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Por que JSON?** JSON é independente de linguagem, legível por humanos e mapeia perfeitamente para dicionários Python. O JSON de layout contém um array `"words"` onde cada entrada possui o texto e um array `boundingBox` com oito números (os quatro pontos dos cantos).

---

## Etapa 4: Executar o Reconhecimento e Capturar a String JSON Bruta

Agora realmente executamos o OCR. O método `recognize()` retorna um objeto `OcrResult`, do qual podemos extrair a string JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Se você imprimir `layout_json` verá algo como:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Caso extremo:** Algumas imagens podem gerar arrays `"words"` vazios se o motor OCR não conseguir detectar nenhum texto. Nesse caso, verifique a qualidade da imagem (contraste, resolução) antes de prosseguir.

---

## Etapa 5: Analisar o JSON em um Dicionário Python

Trabalhar com estruturas nativas do Python é muito mais fácil do que manipular strings. Use a função `json.loads()` para converter a string.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Agora `layout_data["words"]` é uma lista de dicionários, cada um representando uma palavra e sua caixa delimitadora.

---

## Etapa 6: Iterar Sobre as Palavras e **Obter Coordenadas da Caixa Delimitadora**

Aqui está o núcleo do nosso tutorial: percorrer cada palavra, extrair o texto e imprimir as coordenadas. Este é o ponto exato onde **obtemos coordenadas da caixa delimitadora**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Saída de exemplo** (seus números irão variar conforme a imagem):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Por que o formato de oito pontos?** Os quatro cantos (superior‑esquerdo, superior‑direito, inferior‑direito, inferior‑esquerdo) permitem desenhar um polígono ao redor da palavra, mesmo que o texto esteja inclinado. Se você precisar apenas de um retângulo simples, pode calcular `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` e `height = max(y…) - y_min`.

---

## Melhorias Opcionais

### 1. Converter Caixas Delimitadoras em Retângulos Simples

Se sua ferramenta downstream espera `(x, y, width, height)` em vez de oito pontos, adicione um auxiliar:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Manipular PDFs de Múltiplas Páginas

O Aspose OCR pode aceitar fluxos PDF. Substitua a linha de carregamento de imagem por:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Itere `set_page_number` para cada página, coletando coordenadas por página.

### 3. Visualizar Caixas Delimitadoras

Se você quiser ver as caixas desenhadas na imagem original, use o Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Agora você verá contornos vermelhos ao redor de cada palavra reconhecida — perfeito para depuração ou sobreposições de UI.

---

## Perguntas Frequentes & Armadilhas

- **E se o JSON for enorme?** Para documentos grandes, considere fazer streaming do JSON ou processar página por página para manter o uso de memória baixo.  
- **Por que algumas palavras estão ausentes?** Baixo contraste ou texto manuscrito frequentemente atrapalham os motores OCR. Pré‑procese a imagem (aumente o contraste, binarize) antes de enviá‑la ao Aspose.  
- **Posso obter coordenadas ao nível de caractere?** Sim — defina `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` para receber um array `"characters"` com seu próprio `boundingBox`.  
- **O sistema de coordenadas é baseado em zero?** Sim. (0, 0) é o canto superior‑esquerdo da imagem.

---

## Script Completo – Pronto para Copiar & Executar

Abaixo está o exemplo completo e executável que combina todas as etapas. Salve como `extract_bboxes.py` e execute `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


Os tutoriais a seguir cobrem tópicos estreitamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como Usar Aspose OCR para Resultado JSON no Reconhecimento de Imagem](/ocr/english/net/text-recognition/get-result-as-json/)
- [Como Extrair Texto de Imagem Preparando Retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}