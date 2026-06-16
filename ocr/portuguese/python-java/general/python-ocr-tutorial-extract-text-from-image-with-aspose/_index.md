---
category: general
date: 2026-03-26
description: 'Tutorial de OCR em Python: aprenda como extrair texto de uma imagem,
  carregar a imagem para OCR e reconhecer texto de um recibo usando o Aspose OCR em
  apenas alguns passos.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: pt
og_description: 'Tutorial de OCR em Python: aprenda rapidamente a extrair texto de
  imagens, carregar imagens para OCR e reconhecer texto de recibos com o Aspise OCR.'
og_title: Tutorial de OCR em Python – Extrair texto de uma imagem
tags:
- OCR
- Aspose
- Python
title: Tutorial de OCR em Python – Extrair Texto de Imagem com Aspose
url: /pt/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de OCR em Python – Extrair Texto de Imagem com Aspose

Já se perguntou como extrair o texto de um recibo borrado ou de um formulário escaneado sem passar horas escrevendo expressões regulares personalizadas? Você não está sozinho. Neste **python ocr tutorial** vamos percorrer o carregamento de uma imagem para OCR, a execução de OCR em Python e, finalmente, o reconhecimento de texto de arquivos de recibo usando a biblioteca Aspose OCR.  

Ao final deste guia você terá um script pronto‑para‑executar que lê qualquer formato de imagem suportado, extrai o conteúdo textual e o imprime no console. Sem serviços externos, sem chaves de API — apenas Python puro e um poderoso motor de OCR.  

## O que você precisará

- Python 3.8 ou mais recente (o código usa type hints, então um interpretador recente é o ideal)
- Pacote `asposeocrjava` instalado via `pip install aspose-ocr`
- Uma imagem de exemplo – por exemplo `receipt_noisy.jpg` que contém um recibo de loja típico
- (Opcional) Um ambiente virtual para manter as dependências organizadas

Se você já marcou essas caixas, podemos ir direto ao código.  

## Etapa 1: Instalar e Importar as Classes do Aspose OCR

Primeiro, certifique-se de que o pacote Aspose OCR está disponível. Em seguida, importe as classes que precisaremos.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Por que isso importa:** Importar apenas os símbolos necessários mantém o namespace limpo e sinaliza ao interpretador quais partes da biblioteca realmente usamos. Também encurta as linhas de código posteriores, tornando o tutorial mais fácil de seguir.

> **Dica profissional:** Se você estiver usando um notebook Jupyter, anteponha a linha de instalação com `!` para executá‑la na célula.

## Etapa 2: Criar o Motor OCR e Habilitar o Modo Deep‑Learning

A Aspose oferece vários modos de motor. Para a maioria dos recibos do mundo real, o modelo deep‑learning fornece a maior precisão, especialmente em digitalizações ruidosas.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Por que deep‑learning?** OCR tradicional baseado em regras pode falhar com caracteres de baixo contraste ou distorcidos. O modelo deep‑learning, treinado com milhões de glifos, adapta‑se melhor às variações — exatamente o que você precisa ao *perform OCR in Python* em recibos tirados com a câmera do telefone.

## Etapa 3: Carregar Imagem para OCR

Agora realmente **load image for OCR**. Aspose.Imaging suporta PNG, JPEG, BMP, TIFF e mais, então você pode apontá‑la para praticamente qualquer foto de um documento.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Armadilha comum:** Esquecer de definir a imagem no motor resulta em um `NullReferenceException` em tempo de execução. Sempre chame `set_image` após carregar o arquivo.

## Etapa 4: Executar OCR e Extrair Texto

Com o motor preparado e a imagem anexada, podemos finalmente **perform OCR in Python** e recuperar o resultado textual.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

O método `recognize()` retorna um objeto `OcrResult` que contém não apenas o texto bruto, mas também pontuações de confiança, caixas delimitadoras e informações de idioma. Para um caso de uso rápido de **extract text from image** precisamos apenas de `get_text()`.

## Etapa 5: Exibir o Texto Reconhecido

Vamos ver o que o motor realmente leu do recibo.

```python
print("Recognized text:\n", recognized_text)
```

A saída típica se parece com:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Se a saída contiver caracteres estranhos, considere pré‑processar a imagem (por exemplo, aumentar o contraste ou aplicar um filtro de deskew) antes de carregá‑la no motor OCR. Aspose.Imaging oferece um conjunto completo de ferramentas de aprimoramento de imagem que você pode encadear.

## Lidando com Casos Limítrofes & Dicas para Melhor Precisão

### 1. Lidando com Recibos Extremamente Ruidosos

Se o recibo estiver muito borrado, você pode querer mudar para o modo `OcrEngineMode.HIGH_SPEED` para uma passagem mais rápida, embora menos precisa, e então executar uma segunda passagem em `DEEP_LEARNING` na imagem limpa.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Especificando o Idioma

Por padrão, a Aspose tenta detectar automaticamente o idioma. Para recibos em inglês você pode fixá‑lo:

```python
ocr_engine.set_language("eng")
```

### 3. Gerenciamento de Memória

Ao processar muitas imagens em um loop, libere explicitamente os recursos:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Salvando Resultados de OCR em um Arquivo

Às vezes você precisa que o texto extraído seja persistido para análise posterior.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Exemplo Completo Funcional

Abaixo está o script completo que une tudo. Copie‑e‑cole em um arquivo chamado `receipt_ocr.py`, ajuste o caminho da imagem e execute `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Executar o script deve exibir o conteúdo do recibo no seu console e também criar `receipt_output.txt` com os mesmos dados.

![Tutorial de OCR em Python – exemplo de saída de recibo](https://example.com/receipt_output.png "exemplo de tutorial de OCR em python")

*Texto alternativo da imagem:* **python ocr tutorial – sample receipt output**

## Recapitulação & Próximos Passos

Acabamos de percorrer um **python ocr tutorial** que mostra como **load image for OCR**, **perform OCR in Python**, e finalmente **recognize text from receipt** arquivos usando Aspose. Os principais pontos são:

- Escolha o modo de motor correto (deep‑learning para precisão)
- Sempre anexe a imagem antes de chamar `recognize()`
- Use o objeto `OcrResult` para extrair texto limpo, então armazene ou processe conforme necessário

Qual o próximo passo? Considere encadear filtros do Aspose Imaging para melhorar digitalizações de baixo contraste, ou integrar o script em uma API Flask para que você possa enviar recibos via um formulário web. Você também pode explorar a exportação dos dados de OCR para CSV para automação contábil.

Tem perguntas sobre como lidar com PDFs de várias páginas ou scripts não latinos? Deixe um comentário — feliz em ajudar!  

**Pronto para elevar sua automação de documentos?** Pegue o código, experimente diferentes imagens e deixe o motor OCR fazer o trabalho pesado. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}