---
category: general
date: 2026-06-28
description: Como fazer OCR em lote no Python — extrair texto de imagens e converter
  páginas escaneadas em texto usando processamento de OCR em lote.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: pt
og_description: Aprenda como fazer OCR em lote no Python, extrair texto de imagens
  e converter páginas escaneadas em texto com processamento de OCR em lote eficiente.
og_title: Como fazer OCR em lote no Python – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Como fazer OCR em lote no Python – Guia completo para extrair texto de imagens
url: /pt/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote no Python – Guia completo para extrair texto de imagens

Se você está se perguntando **como fazer OCR em lote no Python**, está no lugar certo. Este tutorial mostra uma maneira rápida de **extrair texto de imagens** e **converter páginas escaneadas em texto** usando uma única instância do motor OCR. Chega de copiar‑colar um arquivo após o outro—deixe o código fazer o trabalho pesado.

Vamos percorrer tudo o que você precisa: instalar a biblioteca, carregar uma pasta inteira de escaneamentos, executar o processamento de OCR em lote e lidar com os resultados de forma elegante. Ao final, você terá um script reutilizável que transforma uma pilha de PNGs ou JPEGs em arquivos de texto pesquisáveis em segundos.

## O que você precisará

* Python 3.9+ instalado (o código funciona também no 3.8, mas o 3.9+ oferece os recursos de tipagem mais recentes).
* Uma biblioteca OCR moderna—aqui usamos **Aspose.OCR for Python via .NET**, que expõe a classe `OcrEngine` mostrada no snippet original.  
  ```bash
  pip install aspose-ocr
  ```
* Uma pasta com páginas escaneadas (`page1.png`, `page2.png`, …). Qualquer coisa que o Pillow possa abrir funcionará, então PDFs, TIFFs ou BMPs também são aceitos.
* Um pouquinho de curiosidade—se você nunca automatizou a conversão de imagem‑para‑texto antes, está prestes a descobrir por que OCR em lote é um divisor de águas.

> **Dica profissional:** Se você prefere uma biblioteca puramente Python, troque `OcrEngine` por `pytesseract.image_to_string`. A lógica ao redor permanece idêntica.

## Como fazer OCR em lote no Python – Guia passo a passo

Abaixo está o script completo e executável. Cada linha está comentada para que você veja *por que* cada parte importa, não apenas *o que* ela faz.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Saída esperada

Executar o script em uma pasta com três escaneamentos PNG produz algo como:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

A pré‑visualização mostra os primeiros 200 caracteres de cada página, e o texto completo fica no diretório `ocr_output`.

## Extrair texto de imagens usando um único motor

Por que criamos **um** `OcrEngine` e o reutilizamos? Instanciar o motor pode ser caro porque ele carrega pacotes de idioma e DLLs nativas. Ao compartilhar a mesma instância ao longo do lote, você:

* **Economizar memória** – apenas um conjunto de recursos permanece na RAM.
* **Aumentar velocidade** – o motor permanece aquecido, evitando inicializações repetidas.
* **Manter consistência** – as mesmas configurações de reconhecimento se aplicam a cada página, o que é essencial quando você deseja **extrair texto de imagens** que compartilham o mesmo layout.

Se precisar ajustar o reconhecimento (por exemplo, habilitar correção ortográfica ou mudar o idioma), faça isso *antes* de chamar `recognize_batch`. Todas as páginas subsequentes herdarão essas configurações automaticamente.

## Converter páginas escaneadas em texto de forma eficiente

O cerne do problema—**converter páginas escaneadas em texto**—é resolvido por `engine.recognize_batch(images)`. Nos bastidores, a biblioteca processa cada imagem em um pool de threads em segundo plano, proporcionando escalabilidade quase linear em máquinas multi‑core. Algumas coisas a ter em mente:

* **A qualidade da imagem importa** – 300 dpi ou mais produz os melhores resultados. Se seus escaneamentos são de baixa resolução, considere aumentar a escala com Pillow antes de enviá‑los ao motor.
* **Cor vs. escala de cinza** – os motores OCR geralmente funcionam mais rápido em escala de cinza de 8‑bits. Você pode adicionar uma etapa de pré‑processamento:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Suporte a idiomas** – Aspose.OCR suporta mais de 40 idiomas. Defina `engine.language = "eng"` ou `"fra"` antes da chamada em lote se você não estiver trabalhando com inglês.

## Melhores práticas para processamento de OCR em lote

Mesmo que o código acima já seja conciso, OCR em lote de nível de produção costuma exigir algumas salvaguardas extras:

| Preocupação | Abordagem recomendada |
|-------------|-----------------------|
| **Grandes lotes ( > 500 arquivos )** | Divida em blocos de 100–200 imagens para manter a memória sob controle. |
| **Arquivos corrompidos ou não suportados** | O helper `load_images` já captura exceções e registra um aviso; você também pode escrever um fallback para pular ou mover arquivos problemáticos. |
| **Monitoramento de progresso** | Envolva `recognize_batch` em um loop que devolva após cada imagem se a biblioteca expuser callbacks por imagem. |
| **Pós‑processamento** | Execute uma verificação ortográfica ou limpeza com regex nas strings resultantes para melhorar a pesquisabilidade posterior. |
| **Paralelismo** | Se você tem um ambiente multi‑nó, distribua pastas entre os workers e mescle os arquivos `.txt` ao final. |

Essas dicas ajudam a escalar **processamento de OCR em lote** de algumas páginas para milhares sem travar seu script.

## Perguntas frequentes

**Q: Posso usar isso diretamente com PDFs?**  
A: Absolutamente. Converta cada página PDF em uma imagem primeiro (por exemplo, usando `pdf2image`) e alimente a lista resultante ao `recognize_batch`. O restante do pipeline permanece inalterado

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair texto de imagem com Aspose OCR – Guia passo a passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair texto de imagens usando operação OCR em pastas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Como extrair texto de arquivos ZIP usando Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}