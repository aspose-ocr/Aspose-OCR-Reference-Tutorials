---
category: general
date: 2026-01-12
description: Como realizar OCR de forma rápida e precisa. Aprenda a executar OCR em
  documentos, extrair texto de TIFF, carregar imagem para OCR e definir o idioma do
  OCR em Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: pt
og_description: Como realizar OCR em Python. Este tutorial mostra como executar OCR
  em documentos, extrair texto de arquivos TIFF, carregar imagens para OCR e definir
  o idioma do OCR.
og_title: Como Realizar OCR em um Documento TIFF – Guia Completo
tags:
- OCR
- Python
- Image Processing
title: Como Realizar OCR em um Documento TIFF – Guia Passo a Passo
url: /pt/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em um Documento TIFF – Guia Completo

Já se perguntou **como realizar OCR** em um arquivo TIFF escaneado sem passar horas procurando a biblioteca certa? Você não está sozinho. Muitos desenvolvedores se deparam com dificuldades ao precisar extrair texto de imagens TIFF, especialmente quando desempenho e configurações de idioma são importantes.

Neste tutorial vamos percorrer tudo o que você precisa saber: desde a instalação do pacote OCR, carregamento da imagem para OCR, definição do idioma do OCR, até finalmente **executar OCR no documento** e obter texto limpo. Ao final, você terá um script pronto‑para‑usar que pode ser inserido em qualquer projeto.

> **Dica profissional:** Embora o exemplo use um módulo genérico `ocr`, os mesmos conceitos se aplicam ao Tesseract, EasyOCR ou qualquer motor OCR moderno que exponha uma API Python.

---

## O Que Você Precisa

- Python 3.8+ (qualquer versão recente funciona)
- Uma biblioteca OCR que forneça uma classe `OcrEngine` (o exemplo usa um pacote fictício `ocr`; substitua pelo que você realmente usa)
- Um arquivo TIFF multipágina que você queira processar (vamos chamá‑lo de `big_document.tif`)
- Uma máquina com pelo menos 4 núcleos de CPU se você pretende definir a contagem de threads

Sem serviços externos, sem chaves de nuvem — apenas código local que roda em segundos.

---

![exemplo de como realizar OCR](/images/ocr-example.png "como realizar OCR em um documento TIFF")

*Texto alternativo da imagem: como realizar OCR em um documento TIFF – pré‑visualização do texto extraído.*

---

## Etapa 1: Instalar e Importar a Biblioteca OCR

Primeiro de tudo: obtenha a biblioteca na sua máquina. A maioria dos pacotes OCR está no PyPI, então um simples `pip install` resolve.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Agora importe as classes que você precisará. Se você estiver usando o Tesseract, a linha de importação será diferente, mas o restante do código permanece o mesmo.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Por que isso importa:* Importar os símbolos corretos logo no início evita conflitos de namespace depois e torna o script mais fácil de ler.

---

## Etapa 2: Criar e Configurar o Motor OCR (Definir Idioma do OCR)

Configurar o motor é onde você **define o idioma do OCR** para um reconhecimento preciso. inglês é o padrão, mas você pode para, alemão ou até modo multilíngue com uma única linha.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Por que 4 threads?** A maioria dos laptops modernos tem pelo menos quatro núcleos, e limitar a contagem de threads impede que o processo de OCR consuma toda a máquina — especialmente útil quando o script roda em um servidor compartilhado.

Se precisar de outro idioma, basta substituir `ocr.Language.ENGLISH` por `ocr.Language.FRENCH`, `ocr.Language.SPANISH` etc.

---

## Etapa 3: Carregar Imagem para OCR (Load Image for OCR)

Agora **carregamos a imagem para OCR**. O método `Image.load` lê o arquivo TIFF para a memória, lidando automaticamente com documentos multipágina.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Caso extremo:* Se o arquivo for muito grande, você pode ficar sem RAM. Nesse cenário, considere carregar uma página por vez com `Image.load_page(page_number)` (se a biblioteca suportar).

---

## Etapa 4: Executar OCR no Documento

Com o motor pronto e a imagem carregada, é hora de **executar OCR no documento**. O método `process` faz o trabalho pesado e devolve um objeto de resultado.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Nos bastidores, o motor divide a imagem em blocos de texto, executa o modelo de reconhecimento e junta os resultados. A chamada é bloqueante, ou seja, o script aguarda até que todo o TIFF seja processado — perfeito para trabalhos em lote.

---

## Etapa 5: Extrair Texto do TIFF e Verificar a Saída

Finalmente, **extraímos o texto do TIFF** acessando o atributo `text` do resultado. Vamos imprimir os primeiros 200 caracteres como uma verificação rápida.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Saída esperada (exemplo):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Se precisar do texto completo, basta usar `ocr_result.text`. Para processamento posterior, talvez queira gravá‑lo em um arquivo `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Exemplo Completo Funcionando

Juntando tudo, aqui está um script pronto‑para‑executar. Substitua o nome do pacote placeholder pelo que você realmente instalou.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Execute o script com:

```bash
python ocr_tiff_example.py
```

Você deverá ver uma pré‑visualização impressa no console e um arquivo chamado `extracted_text.txt` contendo a transcrição completa.

---

## Perguntas Frequentes & Casos de Borda

- **E se o TIFF contiver várias páginas?**  
  A maioria dos motores OCR trata cada página como uma imagem separada internamente. O `ocr_result.text` conterá uma quebra de linha entre as páginas. Se precisar manipular página por página, itere com `Image.load_page(page_number)`.

- **Posso processar um PNG ou JPEG em vez de TIFF?**  
  Absolutamente. O método `Image.load` geralmente aceita qualquer formato suportado pelo Pillow ou pela biblioteca subjacente. Basta mudar a extensão do arquivo.

- **Meu texto está ilegível — devo mudar o idioma?**  
  Sim. A etapa **definir idioma do OCR** é crucial para documentos que não são em inglês. Certifique‑se de que o pacote de idioma esteja instalado (por exemplo, `tesseract‑lang‑fra` para francês).

- **Estou ficando sem memória?**  
  Reduza o `set_memory_limit` ou processe as páginas uma a uma. Alguns motores também permitem reduzir a escala da imagem antes do reconhecimento.

---

## Conclusão

Aí está — um guia conciso e totalmente funcional sobre **como realizar OCR** em um arquivo TIFF usando Python. Cobriram‑nos tudo, desde a instalação da biblioteca, configuração do motor (incluindo **definir idioma do OCR**), **carregar imagem para OCR**, **executar OCR no documento**, e finalmente **extrair texto do TIFF**.  

Sinta‑se à vontade para experimentar: ajuste a contagem de threads, troque de idioma ou alimente a saída OCR em um pipeline de linguagem natural. O céu é o limite depois que você domina o básico.

Tem mais perguntas? Deixe um comentário abaixo e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}