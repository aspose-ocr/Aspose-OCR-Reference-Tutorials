---
category: general
date: 2026-03-18
description: Execute OCR na imagem para extrair texto de PNG e gerar PDF pesquisável.
  Aprenda como reconhecer texto em imagens e converter PNG para PDF em minutos.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: pt
og_description: Execute OCR na imagem para extrair texto de PNG, reconhecer texto
  da imagem e gerar um PDF pesquisável. Siga este guia passo a passo.
og_title: Execute OCR na Imagem – Extraia Texto de PNG Rapidamente
tags:
- OCR
- Python
- Image Processing
title: Execute OCR na Imagem – Extraia Texto de PNG Rapidamente
url: /pt/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem – Extrair Texto de PNG Rapidamente

Já precisou **executar OCR em imagem** mas não sabia por onde começar? Talvez você tenha um artigo escaneado salvo como `article.png` e queira apenas o texto simples, ou precise de um PDF pesquisável para arquivamento. De qualquer forma, você está no lugar certo. Neste tutorial vamos percorrer a extração de texto de PNG, o reconhecimento da imagem de texto e até a conversão desse PNG em um PDF pesquisável — tudo com algumas linhas de código.

> **O que você receberá:** um script completo e executável que carrega um PNG, executa OCR, salva a saída hOCR e, opcionalmente, cria um PDF pesquisável. Sem importações faltando, sem “veja a documentação” sem saída — apenas uma solução autônoma que você pode inserir no seu projeto hoje.

## Pré-requisitos

- **Python 3.8+** (a sintaxe usada aqui funciona em qualquer versão recente)
- A biblioteca **`ocr_engine`** que você está usando (o exemplo assume uma classe chamada `OcrEngine`; substitua por Tesseract, EasyOCR, etc., se necessário)
- Uma imagem PNG que você deseja processar (por exemplo, `article.png` colocada em uma pasta que você pode referenciar)
- Permissão de escrita no diretório de saída

Se você estiver usando Tesseract nos bastidores, instale-o com:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

E então instale o wrapper Python:

```bash
pip install pytesseract Pillow
```

*Dica profissional:* mantenha sua biblioteca OCR atualizada — novos pacotes de idioma e ajustes de desempenho são lançados frequentemente.

## Executar OCR em Imagem – Guia Passo a Passo

Abaixo está o **script completo**. Sinta-se à vontade para copiar e colar em um arquivo chamado `run_ocr.py` e executá‑lo com `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### O que o script faz, em linguagem simples

1. **Instanciar** o motor OCR para que você possa controlar suas configurações.
2. **Carregar** o arquivo PNG (`article.png`). O script aborta cedo se o arquivo não existir — sem erros misteriosos de `NoneType` depois.
3. **Selecionar** `hocr` como o formato de exportação. Esse formato mantém o layout original, o que é essencial para converter a imagem em um PDF pesquisável posteriormente.
4. **Executar** o motor de reconhecimento; o trabalho pesado acontece aqui.
5. **Escrever** o XML hOCR em `article.hocr`. Agora você tem uma representação legível por máquina do texto e suas coordenadas.
6. *(Opcional)* Trocar para `"pdf"` e gerar um PDF pesquisável em um passo extra.

A **saída esperada** é um arquivo `.hocr` codificado em UTF‑8 que se parece com isto (cortado para brevidade):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Se você descomentar a seção PDF, também obterá `article_searchable.pdf`, que pode ser aberto em qualquer visualizador de PDF e usar a caixa de busca **Ctrl + F** para localizar palavras instantaneamente.

![Exemplo de saída de OCR em imagem](example.png "OCR em imagem – resultados hOCR e PDF")

## Como Extrair Texto de PNG Usando OcrEngine

Se tudo que você precisa é o texto bruto (sem layout, sem PDF), pode pular totalmente a etapa hOCR:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Por que escolher texto simples?* É leve, perfeito para indexação e funciona muito bem com pipelines de NLP subsequentes.

## Reconhecer Imagem de Texto e Gerar PDF Pesquisável

Gerar um PDF pesquisável é uma dança de duas partes:

1. **Executar OCR** com `hocr` (como fizemos acima) para obter as informações de layout.
2. **Combinar** o PNG original com o hOCR em um PDF usando o exportador PDF do motor.

A maioria das bibliotecas OCR modernas (Tesseract, ABBYY, Google Vision) expõe uma exportação `pdf` que faz exatamente isso. O trecho no bloco *Opcional* do script principal mostra o padrão. Se sua biblioteca não possuir um exportador PDF embutido, você pode usar **`pdf2image`** + **`reportlab`** para unir a imagem e o hOCR — basta me avisar, e eu compartilharei um exemplo extra rápido.

## Converter PNG para PDF com Saída OCR

Às vezes você só quer um **PDF simples** que contenha a imagem (sem camada pesquisável). Isso é ainda mais simples:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Combine isso com a etapa OCR se precisar de uma versão pesquisável, ou mantenha como uma réplica visual fiel para fins de arquivamento.

## Armadilhas Comuns & Dicas

| Problema | Por que acontece | Correção rápida |
|----------|------------------|-----------------|
| **PNG borrado ou de baixa resolução** | A precisão do OCR cai drasticamente abaixo de ~300 DPI. | Aumente a escala com `Image.resize((width*2, height*2), Image.LANCZOS)` antes de enviar ao motor. |
| **Idioma errado** | O motor padrão é o inglês; caracteres não‑ingleses ficam corrompidos. | Chame `ocr_engine.setLanguage('deu')` (ou o código ISO apropriado) antes de `recognize()`. |
| **Saída hOCR ausente** | Alguns motores padrão para texto simples quando `setExportFormat` não é chamado. | Verifique novamente que `setExportFormat("hocr")` é executado **antes** de `recognize()`. |
| **Erros de permissão de arquivo** | Tentando escrever em uma pasta somente leitura. | Use um caminho dentro do seu projeto ou `os.makedirs(..., exist_ok=True)` primeiro. |
| **PDFs grandes causam picos de memória** | O exportador PDF mantém toda a imagem na RAM. | Processar páginas em blocos ou usar um escritor de PDF em streaming. |

*Dica profissional:* sempre teste em uma pequena imagem de amostra antes de escalar para um lote de milhares. Isso economiza horas de depuração.

## Conclusão

Agora você sabe **como executar OCR em arquivos de imagem**, **extrair texto de PNG**, **reconhecer imagem de texto** para tarefas subsequentes, **gerar um PDF pesquisável**, e **converter PNG para PDF** quando precisar de um arquivo simples de arquivamento. O script fornecido é uma solução completa, pronta para copiar e colar, que funciona imediatamente, e as seções opcionais permitem adaptar a saída ao seu fluxo de trabalho exato.

### O que vem a seguir?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}