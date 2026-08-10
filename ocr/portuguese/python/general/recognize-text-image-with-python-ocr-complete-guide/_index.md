---
category: general
date: 2026-06-28
description: Aprenda a reconhecer imagens de texto usando OCR em Python, extrair arquivos
  PNG de texto e imprimir o texto reconhecido com tratamento de erros robusto.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: pt
og_description: Tutorial passo a passo para reconhecer imagem de texto em Python,
  extrair texto PNG e imprimir o texto reconhecido com segurança.
og_title: Reconheça texto em imagens com OCR em Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Reconheça texto em imagem com OCR em Python – Guia Completo
url: /pt/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto em imagem com Python OCR – Guia Completo

Já se perguntou como **reconhecer texto em imagem** em um script Python sem usar um framework pesado? Você não está sozinho. Muitos desenvolvedores precisam de uma maneira rápida de *carregar imagem OCR* uma captura de tela, um recibo escaneado ou um PNG simples e obter o texto de volta.  

Neste tutorial, vamos configurar um mecanismo OCR mínimo, anexar um logger personalizado, **carregar imagem OCR**, executar o **processar imagem OCR**, e finalmente **imprimir texto reconhecido**. Ao final, você terá um script autônomo que também pode **extrair texto png** sob demanda.

## O que você levará consigo

- Um trecho de código Python totalmente funcional que cria um mecanismo OCR, registra cada passo e lida com falhas de forma elegante.  
- Explicações claras de *por que* cada linha importa — para que você possa adaptar o código ao Tesseract, EasyOCR ou qualquer outro backend.  
- Dicas para armadilhas comuns (fonts ausentes, PNGs corrompidos) e como depurá‑las.  

### Pré-requisitos

- Python 3.8+ instalado  
- Uma biblioteca OCR que exponha uma classe `OcrEngine` (o exemplo usa uma API fictícia mas típica; substitua por `pytesseract`, `easyocr`, etc.).  
- Uma imagem PNG que você deseja analisar, salva como `input.png` em uma pasta que você controla.  

> **Dica profissional:** Se você estiver usando `pytesseract`, instale primeiro o binário do Tesseract do sistema (`sudo apt install tesseract-ocr` no Linux) e depois `pip install pytesseract pillow`.

---

## ## Reconhecer Texto em Imagem: Configurando o Logger

Um bom logger é o herói desconhecido de qualquer pipeline OCR. Ele informa *quando* o mecanismo começou, *qual* arquivo foi aberto e *por que* ele pode ter falhado.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Por que isso importa:*  
O logger desacopla a saída de diagnóstico do núcleo OCR, facilitando redirecionar logs para um arquivo, um serviço de monitoramento ou até mesmo uma interface de usuário posteriormente.  

---

## ## Carregar Imagem OCR: Alimentando o Motor com um PNG

Antes que o motor possa **processar imagem OCR**, ele precisa de um objeto de imagem adequado. A maioria das bibliotecas aceita uma instância `Image` do Pillow.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Pontos-chave:*  

- **carregar imagem ocr** – `Image.from_file` abstrai os detalhes da decodificação PNG.  
- Mantenha o caminho configurável; codificar valores fixos torna o script frágil.  
- A chamada ao logger confirma que a imagem foi lida com sucesso, o que é útil quando o arquivo está ausente ou corrompido.

## ## Processar Imagem OCR: Reconhecendo o Texto

Agora começa o trabalho pesado. O motor escaneia o bitmap, aplica suas redes neurais ou heurísticas e gera uma string Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Por que o envolvemos em `try/except`:*  
OCR pode falhar em PNGs de baixa resolução, espaços de cor não suportados ou dados de idioma ausentes. Capturar `OcrException` permite que você **imprima texto reconhecido** somente quando ele realmente existe, evitando rastros de pilha crípticos para os usuários finais.

## ## Imprimir Texto Reconhecido & Extrair Texto PNG

Se o reconhecimento for bem‑sucedido, exibimos o resultado e, opcionalmente, gravamos em um arquivo `.txt` que espelha o nome original do PNG.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*O que você obtém:*  

- **imprimir texto reconhecido** – feedback visual imediato no terminal.  
- Um arquivo `.txt` lado a lado que efetivamente **extrai texto png** para processamento posterior (indexação de busca, entrada de dados, etc.).

## ## Casos de Borda Comuns & Como Lidar com Eles

| Situação | Sintoma | Correção |
|-----------|---------|-----|
| PNG é apenas em escala de cinza | OCR retorna string vazia | Converter para RGB (`Image.convert("RGB")`) antes de alimentar o motor. |
| Idioma não suportado | `OcrException` com código `LANG_NOT_FOUND` | Instale o pacote de idioma (ex., `tesseract‑lang‑fra` para francês) e defina `ocr_engine.language = "fra"`. |
| Imagem muito grande ( > 5 MB ) | Reconhecimento lento ou erro de memória | Reduza com `image.thumbnail((2000, 2000))` antes de `set_image`. |
| Caracteres inesperados | Saída corrompida | Garanta que a imagem seja realmente PNG; alguns arquivos se disfarçam de PNG mas são JPEGs. Use `Image.verify()` para validar. |

## ## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Saída esperada no console (caminho feliz):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Se algo der errado, você verá uma linha clara `[ERROR]` com o motivo, graças ao logger personalizado.

## ## Próximos Passos & Tópicos Relacionados

- **extrair texto png** de lotes: envolva o script em um loop `for` que percorre uma árvore de diretórios.  
- **processar imagem ocr** com pré‑processamento (deskew, aumento de contraste) usando OpenCV antes de alimentar o motor.  
- Mude para um serviço OCR em nuvem (Google Vision, Azure Read) trocando a implementação `OcrEngine` — seu código circundante permanece o mesmo.  
- Aprenda como **imprimir texto reconhecido** em PDFs usando `reportlab` para geração automática de relatórios.  

## Conclusão

Acabamos de percorrer uma forma compacta e pronta para produção de **reconhecer texto em imagem** em Python, desde o carregamento do PNG até **imprimir texto reconhecido** e salvar o resultado. Ao injetar um pequeno logger, tratar exceções e, opcionalmente, persistir a saída, o script está pronto tanto para experimentos rápidos quanto para integração em pipelines maiores.

Experimente com suas próprias capturas de tela, brinque com o pré‑processamento de imagens, e em breve você estará extraindo texto de qualquer PNG que lhe lançar. Tem dúvidas? Deixe um comentário — feliz OCR!

![recognize text image example](placeholder.png)


## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como Realizar Extração de Texto de Imagem a partir de Stream Usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Converter Imagem em Texto – Executar OCR em Imagem a partir de URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}