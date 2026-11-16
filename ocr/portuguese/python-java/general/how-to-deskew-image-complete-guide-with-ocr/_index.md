---
category: general
date: 2026-03-26
description: Aprenda a corrigir a inclinação de imagens, reconhecer texto a partir
  de imagens e criar um pipeline de pré‑processamento de imagens para remover ruído
  de digitalizações e converter imagens escaneadas em texto.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: pt
og_description: Como corrigir a inclinação de uma imagem e transformar uma digitalização
  inclinada em texto pesquisável. Siga este guia para reconhecer texto a partir da
  imagem, remover ruído da digitalização e converter a imagem escaneada em texto.
og_title: Como Corrigir a Inclinação de Imagem – Guia de OCR Passo a Passo
tags:
- OCR
- image-processing
- Python
title: Como Desinclinar Imagem – Guia Completo com OCR
url: /pt/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Deskew Image – Guia Completo com OCR

Já se perguntou **how to deskew image** que saiu de um scanner barato? Você não está sozinho. Uma página torta parece pouco profissional e, mais importante, a inclinação pode atrapalhar qualquer motor OCR que tenta **recognize text from image**.  

Neste tutorial, percorreremos um **image preprocessing pipeline** completo que deskews, binarizes e denoises uma digitalização, e então o entrega a um motor OCR para que você possa **convert scanned image to text** com o mínimo de esforço. Sem mágica, apenas Python puro e uma pequena biblioteca que faz o trabalho pesado.

## O que você vai precisar

- Python 3.9+ (o código funciona em 3.10 e superior)
- O pacote `ocr` (instale via `pip install ocr‑toolkit` – substitua pelo nome real da sua biblioteca)
- Um JPEG ou PNG escaneado que esteja visivelmente inclinado (por exemplo, `skewed_scan.jpg`)
- Um pouco de curiosidade sobre por que cada etapa de pré‑processamento importa

É isso. Sem dependências pesadas como OpenCV, a menos que você queira aprofundar mais tarde.

## Etapa 1: Carregar a Imagem Escaneada

A primeira coisa é carregar o arquivo na memória. Esta etapa é simples, mas crucial—se o caminho estiver errado, tudo o mais falha.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Por quê?**  
> Carregar a imagem nos fornece um objeto manipulável com o qual o `ocr.ImagePreprocessor` pode trabalhar. Pular esta etapa deixaria o pipeline cego aos dados reais dos pixels.

## Como Deskew Image e Prepará‑la para OCR

Agora que temos a imagem, vamos endireitá‑la. O método `deskew()` estima o ângulo de inclinação e gira a foto de volta à horizontal.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Dica de especialista:** Se suas digitalizações estiverem apenas ligeiramente fora de alinhamento (≤ 3°), o algoritmo padrão geralmente acerta. Para ângulos extremos, pode ser necessário ajustar os parâmetros internos—verifique a documentação da biblioteca para `max_angle`.

## Binarizar a Imagem – Torná‑la Preto‑e‑Branco

Motores OCR adoram entrada de alto contraste. Converter a foto para uma representação binária (preto‑e‑branco) remove tons sutis que podem confundir o reconhecimento de caracteres.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **O que está acontecendo?**  
> Pixels mais claros que 128 tornam‑se brancos; todo o resto fica preto. Ajuste o limiar se sua digitalização estiver incomumente escura ou clara.

## Remover Ruído da Digitalização antes do OCR

Mesmo uma imagem perfeitamente deskewed pode conter manchas, poeira ou artefatos de compressão. Esses pequenos pontos são a ruína de qualquer motor OCR.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Por que remover ruído?**  
> O ruído cria bordas falsas que o motor OCR pode interpretar como caracteres. Um raio pequeno funciona para a maioria das digitalizações; aumente‑o para documentos muito granulados.

## Aplicar o Pipeline de Pré‑processamento de Imagem

Todas as configurações estão definidas—agora executamos o pipeline na imagem original.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Resultado:** `processed_image` é um bitmap limpo, reto e de alto contraste pronto para extração de texto.

## Reconhecer Texto da Imagem com o Motor OCR

Hora de realmente ler o texto. Inicializamos o motor OCR, alimentamos a nossa imagem aprimorada e solicitamos a string bruta.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Saída esperada** (exemplo):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Se você vir caracteres estranhos, verifique novamente a etapa de deskewing ou experimente um valor diferente de `threshold`.

## Construindo um Pipeline de Pré‑processamento de Imagem – Script Completo

Juntando tudo, aqui está um script único e executável que você pode colocar em um arquivo `.py` e executar:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Dica:** Envolva tudo em uma função (`def ocr_from_file(path): …`) se você pretende processar muitos arquivos em lote.

## Perguntas Frequentes & Casos Limítrofes

- **E se a imagem já estiver na posição correta?**  
  O método `deskew()` detecta um ângulo quase zero e deixa a foto intacta, então você pode executá‑la com segurança em cada arquivo.

- **Minha digitalização está em cores—devo mantê‑la?**  
  Cor não agrega valor para a maioria das tarefas OCR. A binarização a remove, acelerando o processamento e reduzindo o uso de memória.

- **Posso encadear múltiplas etapas de pré‑processamento?**  
  Absolutamente. A classe `ImagePreprocessor` foi projetada para pipelines; você pode adicionar `sharpen()`, `contrast_enhance()` ou filtros personalizados antes de chamar `apply()`.

- **A saída OCR tem quebras de linha indesejadas—como corrigir?**  
  Pós‑procese a string com `text.replace("\n", " ").strip()` ou use uma biblioteca de análise de layout mais avançada como os modos `--psm` do Tesseract.

## Próximos Passos

Agora que você sabe **how to deskew image** e tem um **image preprocessing pipeline** sólido, pode explorar:

- Integrar **recognize text from image** em uma API Flask para uploads de documentos em tempo real.
- Usar o pipeline para **remove noise from scan** de documentos históricos onde a preservação é essencial.
- Escalar para processar em lote milhares de páginas e gerar um PDF pesquisável usando `pdfminer` ou `PyMuPDF`.

Sinta‑se à vontade para experimentar diferentes limiares, raios de denoise, ou até trocar o backend OCR por Tesseract se precisar de suporte multilíngue. Os fundamentos permanecem os mesmos: endireitar, limpar e então ler.

---

*Feliz codificação! Se encontrar problemas, deixe um comentário abaixo—ficarei feliz em ajudar a ajustar o pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}