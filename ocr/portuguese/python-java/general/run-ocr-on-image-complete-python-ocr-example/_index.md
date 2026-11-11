---
category: general
date: 2026-03-18
description: Execute OCR em imagens rapidamente com Python. Aprenda como reconhecer
  texto de PNG, carregar a imagem para OCR e extrair palavras da imagem em um guia
  passo a passo.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: pt
og_description: Execute OCR em uma imagem usando Python. Este tutorial mostra como
  reconhecer texto de um PNG, carregar a imagem para OCR e extrair palavras da imagem
  com um exemplo de código completo.
og_title: Executar OCR em Imagem – Guia Python
tags:
- OCR
- Python
- Image Processing
title: Executar OCR em Imagem – Exemplo Completo de OCR em Python
url: /pt/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem – Exemplo Completo de OCR em Python

Já precisou **executar OCR em arquivos de imagem** mas não sabia por onde começar? Você não está sozinho; muitos desenvolvedores encontram essa barreira ao primeiro contato com a extração de texto de documentos escaneados. Neste tutorial vamos percorrer um **exemplo de OCR em Python** que permite **reconhecer texto de arquivos PNG**, **carregar imagem para OCR** e **extrair palavras da imagem** com pontuações de confiança — tudo em apenas algumas linhas de código.

Cobriremos tudo o que você precisa: a biblioteca necessária, como configurar o motor, por que cada passo é importante e como é a saída. Ao final, você poderá inserir este trecho no seu próprio projeto e começar a extrair texto de qualquer imagem instantaneamente. Sem enrolação, apenas uma solução prática e executável.

## O que Você Vai Precisar

Antes de mergulharmos, certifique‑se de que tem:

- Python 3.8 ou superior instalado  
- O pacote `ocrengine` (ou qualquer biblioteca que forneça uma classe `OcrEngine`). Você pode instalá‑lo via `pip install ocrengine` – ajuste o nome se estiver usando outra biblioteca de OCR como `pytesseract`.  
- Um arquivo de imagem (PNG, JPG, etc.) que deseja processar – para este guia usaremos `invoice.png`.  

É só isso. Sem dependências pesadas, sem serviços externos, apenas Python puro.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Texto alternativo: exemplo de execução de OCR em imagem mostrando uma fatura escaneada sendo processada*

## Etapa 1 – Instalar e Importar a Biblioteca de OCR

Primeiro de tudo, vamos colocar o motor de OCR no nosso ambiente e importá‑lo. Se você estiver usando o hipotético pacote `ocrengine`, a importação fica assim:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Por que isso importa:** Importar a classe correta lhe dá acesso aos métodos que chamaremos depois, como `setImageFromFile` e `recognize`. Se você pular este passo, o Python lançará um `ModuleNotFoundError`, e você ficará travado antes mesmo de carregar uma imagem.

## Etapa 2 – Criar uma Instância do Motor de OCR

Agora que a biblioteca está pronta, precisamos de um objeto de motor que armazenará a configuração e o estado do processo de reconhecimento.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Dica profissional:* Alguns motores de OCR permitem ajustar modelos de idioma ou configurações de DPI neste ponto. Para um **exemplo de OCR em python** básico, os padrões funcionam bem, mas se você estiver lidando com digitalizações de baixa resolução, considere ajustá‑los aqui.

## Etapa 3 – Carregar a Imagem que Você Deseja Processar

O próximo passo lógico é **carregar imagem para OCR**. Você aponta o motor para o caminho do arquivo PNG (ou qualquer formato suportado) que deseja analisar.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**O que está acontecendo nos bastidores?** O motor lê os dados de pixel, converte‑os para um formato que o algoritmo de reconhecimento entende e os armazena internamente. Se o caminho do arquivo estiver errado, você receberá um `FileNotFoundError`, então verifique se a imagem realmente existe.

## Etapa 4 – Executar o Algoritmo de Reconhecimento

Com a imagem carregada, finalmente **executamos OCR em imagem** para extrair o conteúdo textual.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

Neste ponto o motor varre o bitmap, aplica correspondência de padrões e devolve um objeto que contém cada palavra detectada, linha e métrica de confiança.

## Etapa 5 – Iterar Sobre as Palavras Reconhecidas e Exibir a Confiança

A parte mais útil de qualquer fluxo de OCR é ver **a confiança** de cada token extraído. Ela indica o quão certo o motor está sobre cada palavra, permitindo filtrar resultados de baixa confiança, se necessário.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Saída esperada** (exemplo):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Agora você pode ver exatamente **quais palavras foram extraídas da imagem** e quão confiável é cada detecção. Este é o núcleo de qualquer pipeline de **extrair palavras de imagem**.

## Lidando com Casos de Borda Comuns

### E se a Imagem for em Tons de Cinza?

Alguns motores de OCR funcionam melhor com imagens coloridas. Se você notar baixa confiança geral, tente converter o PNG para uma versão preto‑e‑branco de alto contraste antes de enviá‑lo ao motor. O Pillow pode ajudar:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Trabalhando com Múltiplos Idiomas

Se seu documento contém tanto inglês quanto espanhol, você vai querer **reconhecer texto de PNG** usando um modelo multilíngue. A maioria dos motores permite definir a lista de idiomas durante a inicialização:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrando Palavras de Baixa Confiança

Às vezes você só precisa de palavras com confiança acima, por exemplo, de 90 %. Um filtro rápido fica assim:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Script Completo, Pronto‑para‑Executar

Juntando tudo, aqui está um script único que você pode copiar‑colar e executar imediatamente (basta substituir o caminho para o seu PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Execute com:

```bash
python run_ocr_on_image.py
```

Você deverá ver a lista de palavras e porcentagens de confiança impressas no console, exatamente como mostrado anteriormente.

## Perguntas Frequentes

**Isso funciona com arquivos JPG ou TIFF?**  
Com certeza. O método `setImageFromFile` aceita qualquer formato que a biblioteca subjacente consiga decodificar, então você pode **executar OCR em arquivos de imagem** dos tipos JPG, TIFF, BMP, etc.

**Posso processar múltiplas imagens em um loop?**  
Claro. Envolva as etapas de carregamento e reconhecimento dentro de um `for` loop sobre uma lista de caminhos de arquivos. Apenas lembre‑se de reinicializar o motor se a biblioteca exigir uma nova instância por imagem.

**E se eu precisar do texto em uma única string ao invés de palavra por palavra?**  
A maioria dos objetos de resultado de OCR expõe um método `getText()` que devolve todo o documento. Exemplo:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Próximos Passos e Tópicos Relacionados

Agora que você sabe como **executar OCR em imagem**, considere explorar:

- **Pós‑processamento**: Use expressões regulares para limpar datas, valores ou IDs extraídos de faturas.  
- **Processamento em lote**: Combine o script com `os.listdir()` para lidar com pastas inteiras de documentos escaneados.  
- **Bibliotecas alternativas**: `pytesseract` é uma opção open‑source popular; o fluxo de trabalho é semelhante — basta substituir as chamadas ao motor.  
- **Exportação de resultados**: Grave as palavras extraídas e as pontuações de confiança em CSV para análises posteriores.

Cada uma dessas extensões se baseia diretamente na fundação que construímos aqui, permitindo transformar dados brutos de OCR em informação acionável.

---

### TL;DR

Mostramos um **exemplo conciso de OCR em python** que demonstra como **carregar imagem para OCR**, **executar OCR em imagem** e **extrair palavras de imagem** enquanto reporta a confiança. O script completo está pronto para ser executado, e agora você tem o conhecimento para adaptá‑lo a qualquer projeto que precise **reconhecer texto de PNG** (ou outros formatos). Experimente, ajuste os limiares de confiança e veja suas aplicações se tornarem conscientes de texto em minutos. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}