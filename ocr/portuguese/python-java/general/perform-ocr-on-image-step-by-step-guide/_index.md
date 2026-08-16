---
category: general
date: 2026-03-18
description: Execute OCR em imagem para extrair texto da imagem rapidamente. Aprenda
  como carregar a imagem para OCR, criar o motor de OCR e melhorar a precisão do OCR
  com opções de idioma.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: pt
og_description: Realize OCR em imagem com este guia detalhado. Aprenda a carregar
  a imagem para OCR, criar o motor de OCR e melhorar a precisão do OCR para uma extração
  de texto confiável.
og_title: Realize OCR em Imagem – Tutorial Completo de Programação
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Realize OCR em Imagem – Guia Passo a Passo
url: /pt/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem – Tutorial de Programação Completo

Já precisou **executar OCR em imagem** mas não sabia qual biblioteca escolher ou como obter resultados confiáveis? Você não está sozinho. Neste guia vamos percorrer tudo o que você precisa para **extrair texto de imagem**, desde o carregamento da foto até o ajuste das opções de idioma, para que você possa **melhorar a precisão do OCR** em cada etapa.

Vamos cobrir como **carregar imagem para OCR**, como **criar engine OCR**, e por que cada configuração importa. Ao final, você terá um script pronto‑para‑executar que imprime o texto reconhecido, e entenderá o “porquê” por trás de cada linha — sem atalhos vagos como “veja a documentação”. Vamos mergulhar.

## O que Você Precisa

- Python 3.8+ (o código usa f‑strings e type hints)
- O pacote hipotético `ocr_lib` – instale com `pip install ocr_lib`
- Um arquivo de imagem contendo texto impresso claro (por exemplo, `lab_report.png`)
- Um editor de texto básico ou IDE (VS Code, PyCharm, o que preferir)

Se você já tem tudo isso, ótimo — está pronto. Caso contrário, baixe o Python em python.org e execute o comando pip; leva apenas um minuto.

![exemplo de execução de OCR em imagem](/images/ocr-example.png)

*Texto alternativo: execução de OCR em imagem – exemplo de saída mostrando texto extraído.*

## Etapa 1: Criar Engine OCR – Como **criar engine OCR** em Python

Antes que qualquer reconhecimento possa acontecer, a biblioteca precisa de um objeto engine que contém as configurações e o estado de execução. Pense na engine como o cérebro por trás da operação.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Por que isso importa:** Instanciar a engine logo no início permite que você anexe opções de idioma depois, e também faz cache dos modelos internos para chamadas subsequentes mais rápidas.

## Etapa 2: Carregar Imagem para OCR – A forma correta de **carregar imagem para OCR**

Agora que temos uma engine, precisamos fornecer algo para ela ler. O método `setImageFromFile` aceita um caminho de sistema de arquivos; o caminho pode ser absoluto ou relativo ao diretório de trabalho do script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Dica profissional:** Use um caminho absoluto ou `os.path.join` para evitar surpresas de “arquivo não encontrado” quando o script for executado a partir de outra pasta.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Etapa 3: Melhorar a Precisão do OCR – Ajustando **opções de idioma** para **melhorar a precisão do OCR**

O OCR pronto‑para‑usar funciona, mas vocabulários específicos de domínio (como jargões de laboratório) costumam atrapalhá‑lo. Ao fornecer um dicionário personalizado e uma lista negra, você reduz erros de reconhecimento, como confundir “0” com “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Por que isso ajuda:** O dicionário informa ao modelo OCR que “HPLC” é um token válido, impedindo que ele divida a palavra em nonsense. A lista negra indica ao modelo que símbolos ambíguos devem ser tratados como ruído, o que **melhora a precisão do OCR** diretamente.

## Etapa 4: Executar OCR em Imagem – A chamada central **perform OCR on image**

Com a engine preparada e a imagem anexada, é hora de realmente reconhecer o texto. Esta etapa devolve um objeto `OcrResult` que você pode consultar para texto bruto, pontuações de confiança ou caixas delimitadoras.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Se a imagem estiver borrada, você verá números de confiança mais baixos no resultado. Isso indica que é preciso pré‑processar a imagem (por exemplo, aumentar o contraste) antes de enviá‑la à engine.

## Etapa 5: Extrair Texto da Imagem – Obtendo a string final

Finalmente, pedimos ao `OcrResult` sua representação textual. O método `getText()` devolve uma string em texto simples pronta para processamento posterior (salvar em um arquivo, inserir em um banco de dados, etc.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Saída esperada:** Supondo que `lab_report.png` contenha uma tabela simples, você pode ver algo como:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Isso conclui a parte de **extrair texto da imagem**.

## Exemplo Completo – Juntando Tudo

Abaixo está um script único que une as peças das seções anteriores. Você pode copiar‑colar em `run_ocr.py` e executar `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Lista de verificação rápida

| ✅ | Item |
|---|------|
| ✔️ | Engine é criada (`create OCR engine`) |
| ✔️ | Imagem é carregada (`load image for OCR`) |
| ✔️ | Opções de idioma são definidas (`improve OCR accuracy`) |
| ✔️ | OCR é executado (`perform OCR on image`) |
| ✔️ | Texto é extraído (`extract text from image`) |

Execute o script e observe o console. Se você vir o bloco “OCR Output” com o conteúdo do seu relatório, você **executou OCR em imagem** com sucesso.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Entrada borrada** | O modelo OCR não consegue distinguir os caracteres | Pré‑processar com OpenCV: `cv2.GaussianBlur` ou aumentar DPI |
| **Idioma errado** | O idioma padrão pode estar configurado para algo diferente de inglês | Chame `engine.setLanguage("eng")` antes de `recognize()` |
| **Termos do dicionário ausentes** | Palavras específicas do domínio ficam distorcidas | Adicione‑as via `setDictionary` como mostrado na Etapa 3 |
| **Caracteres na lista negra causam |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}