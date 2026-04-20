---
category: general
date: 2026-03-18
description: Como usar OCR para extrair texto de imagens – um guia rápido para reconhecer
  texto de arquivos PNG e carregar imagens para OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: pt
og_description: Como usar OCR para extrair texto de imagens – aprenda a reconhecer
  texto de PNG, carregar a imagem para OCR e extrair texto com um script Python simples.
og_title: 'Como usar OCR: extrair texto de imagens em Python'
tags:
- OCR
- Python
- Image Processing
title: 'Como usar OCR: extrair texto de imagens em Python'
url: /pt/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR: Extrair texto de imagens em Python

Já se perguntou **como usar OCR** quando tem uma captura de tela bagunçada ou um recibo escaneado? Você não está sozinho—desenvolvedores precisam constantemente extrair texto legível de imagens, especialmente PNGs que vêm de aplicativos móveis ou uploads na web. Neste tutorial, vamos percorrer um exemplo completo e executável que mostra como **extrair texto de imagem**, **reconhecer texto de PNG** e até **carregar imagem para OCR** com apenas algumas linhas de Python.

Cobriremos tudo, desde a instalação da biblioteca correta até o tratamento de documentos multilíngues, então, ao final, você saberá exatamente *como extrair texto* de qualquer imagem que submeter ao motor. Sem referências vagas, apenas uma solução clara, passo a passo, que você pode copiar‑colar e executar.

## O que você aprenderá

1. Configurar um motor OCR leve (sem dependências pesadas necessárias).  
2. Carregar um arquivo de imagem—especificamente um PNG—no motor.  
3. Habilitar a detecção automática de idioma para que o motor possa lidar com conteúdo multilíngue.  
4. Executar o processo de reconhecimento e obter o resultado em texto simples.  
5. Ajustar o fluxo de trabalho para casos extremos, como arquivos ausentes ou formatos não suportados.

Se você está confortável com Python básico, está pronto. Não é necessária experiência prévia com OCR, embora uma rápida olhada na documentação da biblioteca nunca faça mal.

---

![Como usar OCR em uma imagem PNG](placeholder.png "Como usar OCR em uma imagem PNG – guia passo a passo")

## Como usar OCR – Carregar imagem e reconhecer texto {#how-to-use-ocr}

### Etapa 1: Instalar a biblioteca OCR

Primeiro de tudo, você precisa de um pacote Python que forneça a classe `OcrEngine`. Para este tutorial, usaremos o fictício porém ilustrativo pacote **SimpleOCR**, que pode ser instalado via pip:

```bash
pip install simple-ocr
```

> **Dica profissional:** Se você estiver trabalhando em um ambiente virtual (altamente recomendado), ative‑o antes de executar o comando de instalação. Isso mantém as dependências do seu projeto organizadas.

### Etapa 2: Importar o motor e criar uma instância

Criar o motor é tão fácil quanto chamar seu construtor. Pense no motor como o “cérebro” que posteriormente processará a imagem que você fornecer.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Por que criamos uma nova instância a cada vez? Isolamento. Um motor novo garante que nenhum estado residual de uma execução anterior contamine o reconhecimento atual, o que é crucial ao processar muitos arquivos em lote.

### Etapa 3: Carregar a imagem que você deseja processar

Agora realmente **carregamos a imagem para OCR**. O método `setImageFromFile` aceita um caminho para qualquer imagem raster; apontaremos para um PNG chamado `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Se o arquivo não for encontrado, `SimpleOCR` lança um claro `FileNotFoundError`. Você pode capturá‑lo para fornecer uma mensagem de erro amigável:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Etapa 4: Habilitar detecção automática de idioma

A maioria dos motores OCR modernos vem com pacotes de idioma. Ao passar `"multilingual"` informamos ao motor para farejar o texto e escolher o modelo de idioma correto automaticamente. Isso é especialmente útil quando seu PNG contém uma mistura de inglês e espanhol, por exemplo.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Se você souber o idioma com antecedência, pode substituir `"multilingual"` por um locale específico como `"eng"` ou `"spa"` para acelerar o processamento.

### Etapa 5: Executar o processo de reconhecimento

O trabalho pesado acontece aqui. `recognize()` escaneia a imagem, aplica segmentação, executa a rede neural e constrói um buffer de texto internamente.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Nos bastidores o motor realiza:

- **Pré‑processamento** (correção de inclinação, binarização)  
- **Análise de layout** (detecção de colunas, tabelas)  
- **Classificação de caracteres** (usando um modelo de deep‑learning)  

Tudo isso é abstraído, por isso você precisa de apenas uma linha.

### Etapa 6: Recuperar e imprimir o texto reconhecido

Finalmente, buscamos o objeto de resultado e extraímos a string simples. Esta é a parte onde você realmente **extrai texto de imagem**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Saída esperada** (truncada para brevidade):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Se a imagem não contiver caracteres reconhecíveis, `text` será uma string vazia. Você pode proteger contra isso:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Extrair texto de imagem – Lidando com casos extremos comuns

### Múltiplos idiomas em um único arquivo

Quando um documento mistura idiomas, a configuração `"multilingual"` geralmente funciona corretamente. No entanto, se você notar erros de reconhecimento, pode especificar manualmente uma lista de fallback:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Formatos não‑PNG

Embora nosso foco seja **reconhecer texto de PNG**, `SimpleOCR` também aceita JPEG, BMP e TIFF. Basta mudar a extensão do arquivo em `setImageFromFile`. Para pilhas TIFF, pode ser necessário selecionar uma página específica:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Arquivos grandes e uso de memória

Se você estiver processando varreduras gigapixel, considere redimensionar antes do OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Redimensionar reduz a pressão de memória enquanto preserva detalhes suficientes para um reconhecimento preciso.

### Depurando carregamentos falhos

Às vezes, uma imagem parece boa a olho nu, mas está corrompida internamente. Habilite o registro detalhado para ver o que o motor vê:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Script completo, pronto‑para‑executar

Abaixo está o programa completo que reúne todas as peças. Copie‑o para um arquivo chamado `ocr_demo.py`, ajuste o placeholder `YOUR_DIRECTORY` e execute `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Executar este script deve gerar a versão em texto simples de qualquer coisa que esteja dentro de `mixed_doc.png`. Sinta‑se à vontade para trocar o arquivo por qualquer outra imagem—**como extrair texto** funciona da mesma forma.

---

## Conclusão

Acabamos de percorrer **como usar OCR** em Python para **extrair texto de arquivos de imagem**, focando especificamente em **reconhecer texto de PNG** e nos passos práticos para **carregar imagem para OCR**. O trecho acima é uma solução autônoma: instale o pacote, forneça um arquivo, habilite a detecção multilíngue, execute o motor e obtenha o resultado.

A partir daqui você pode:

- Integrar o script em um serviço web que aceita uploads de usuários.  
- Processar em lote uma pasta de PDFs convertidos para PNGs.  
- Adicionar pós‑processamento (por exemplo, limpeza com regex, correção ortográfica) para melhorar a precisão.

Lembre‑se, a qualidade do OCR depende da clareza da imagem, dos pacotes de idioma corretos e, às vezes, de um pouco de pré‑processamento—então experimente

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}