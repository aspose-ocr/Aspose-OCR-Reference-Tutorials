---
category: general
date: 2026-06-25
description: Extrair texto de imagem usando OCR em Python. Aprenda como carregar a
  imagem para OCR, realizar OCR em Python e converter o recibo para JSON em alguns
  passos simples.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: pt
og_description: Extraia texto de imagem usando OCR em Python. Este tutorial orienta
  você a carregar uma imagem para OCR, executar OCR em Python e converter um recibo
  em JSON.
og_title: Extrair Texto de Imagem em Python – Guia Completo de OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Extrair texto de imagem em Python – Guia completo de OCR
url: /pt/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em Python – Guia Completo de OCR

Já precisou **extrair texto de imagem** mas não sabia por onde começar? Neste tutorial vamos guiá‑lo passo a passo para **carregar a imagem para OCR**, **executar OCR em Python** e **converter recibo para JSON** — tudo com apenas algumas linhas de código.

Se você já desenvolveu um app de escaneamento de recibos, um rastreador de despesas, ou simplesmente quer automatizar a entrada de dados, verá por que dominar esse fluxo é transformador. Ao final, você terá um script funcional que lê a foto de um recibo e gera um payload JSON limpo pronto para serviços downstream.

## O que você vai aprender

Cobriremos cada etapa, desde a instalação da biblioteca `aocr` até o tratamento do resultado bruto. Especificamente, você aprenderá a:

1. **Criar uma instância do motor OCR** – ponto de entrada para todo o trabalho de reconhecimento.  
2. **Carregar uma imagem para OCR** – informar ao motor qual arquivo ler.  
3. **Escolher o formato de exportação** – JSON ou XML; vamos usar JSON porque é mais fácil de consumir.  
4. **Executar o reconhecimento** – realmente fazer OCR em Python.  
5. **Imprimir ou armazenar o resultado** – converter recibo para JSON e visualizar a saída.

Nenhuma experiência prévia com OCR é necessária; apenas uma configuração básica de Python e um arquivo de imagem (um recibo, um flyer, o que precisar).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="diagrama mostrando o fluxo de extração de texto de imagem usando OCR em Python"}

## Extrair Texto de Imagem – OCR em Python passo a passo

Abaixo está o script completo, pronto para ser executado. Sinta‑se à vontade para copiá‑lo e colá‑-lo em um arquivo chamado `receipt_ocr.py` e executar `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Por que isso funciona

- **Instância do motor** – `aocr.OcrEngine()` encapsula todo o trabalho pesado (carregamento de modelo, pré‑processamento etc.).  
- **Carregamento da imagem** – `engine.load_image()` indica à biblioteca exatamente qual bitmap analisar; você pode fornecer JPEG, PNG ou até PDFs de várias páginas.  
- **Formato de exportação** – Definir `engine.export_format` para `aocr.ExportFormat.JSON` transforma o resultado em uma string estruturada, perfeita para APIs que esperam JSON.  
- **Chamada de reconhecimento** – `engine.recognize()` executa a inferência da rede neural nos bastidores; retorna uma string JSON que contém blocos de texto detectados, escores de confiança e informações de layout.  

---

## Carregar Imagem para OCR com aocr

Se você está se perguntando se a imagem precisa de algum pré‑processamento especial, a resposta curta é **não** — `aocr` lida com a maioria dos casos comuns (ajuste de contraste, correção de inclinação) automaticamente. Contudo, você pode melhorar a precisão ao:

- Garantir que a imagem tenha pelo menos 300 dpi.  
- Recortar bordas irrelevantes.  
- Converter para escala de cinza antes de enviá‑la (opcional, `engine.load_image()` faz isso para você).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Dica de especialista:* Se o recibo contiver muito ruído, a etapa extra acima pode aumentar a **perform OCR in Python** precisão de forma perceptível.

---

## Escolher Formato de Exportação e Converter Recibo para JSON

Você pode se perguntar: “Por que não obter apenas texto puro?” Porque JSON preserva a estrutura hierárquica (linhas, palavras, caixas delimitadoras). Isso facilita muito mapear campos como *valor total* ou *data* posteriormente.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Ao executar o script, `json_result` terá algo parecido com isto (abreviado para brevidade):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Agora você tem um payload de **convert receipt to JSON** que pode ser enviado diretamente para um banco de dados, um endpoint REST ou um modelo de machine‑learning.

---

## Executar Reconhecimento e Recuperar Resultados

A etapa final — realmente executar o OCR — é tão simples quanto chamar `recognize()`. Nos bastidores, a biblioteca:

1. Envia a imagem por uma rede convolucional pré‑treinada.  
2. Decodifica a saída da rede em caracteres legíveis.  
3. Empacota tudo no formato selecionado (JSON no nosso caso).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Se precisar armazenar a saída em vez de imprimi‑la, basta gravá‑la em um arquivo:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Caso extremo:* Alguns recibos contêm caracteres não‑ASCII (por exemplo, “€”). Certifique‑se de abrir o arquivo com codificação UTF‑8, como mostrado acima, para evitar texto corrompido.

---

## Exemplo Completo (Todas as Etapas em Um Script)

Juntando tudo, aqui está o script final que você pode executar de ponta a ponta:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Execute com:

```bash
python receipt_ocr.py
```

Você deverá ver uma linha de confirmação e, na mesma pasta, um arquivo `receipt_output.json` contendo os dados estruturados.

---

## Conclusão

Agora você sabe **como extrair texto de imagem** usando Python, como **carregar imagem para OCR**, como **executar OCR em Python** e como **converter recibo para JSON** para consumo downstream. Esse fluxo end‑to‑end é leve, requer apenas o pacote `aocr` e pode ser inserido em qualquer pipeline de automação.

Qual o próximo passo? Experimente trocar o formato de exportação para XML, teste diferentes técnicas de pré‑processamento de imagem ou crie uma pequena API Flask que aceite um recibo enviado e retorne instantaneamente o payload JSON. O céu é o limite quando você domina o básico.

Tem dúvidas ou encontrou algum problema? Deixe um comentário abaixo e feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair Texto de Imagem – Otimização de OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Como extrair tabela de imagem usando Aspose.OCR para .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}