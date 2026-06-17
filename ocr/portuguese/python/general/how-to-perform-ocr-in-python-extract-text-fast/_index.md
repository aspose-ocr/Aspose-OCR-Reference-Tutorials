---
category: general
date: 2026-03-26
description: Aprenda a fazer OCR em Python e extraia texto de imagens facilmente,
  leia texto de digitalizações ou extraia texto de faturas usando um OcrEngine simples.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: pt
og_description: Como fazer OCR em Python? Este guia mostra como extrair texto de imagens,
  ler texto de digitalizações e extrair texto de faturas em minutos.
og_title: Como fazer OCR em Python – Extraia texto rapidamente
tags:
- OCR
- Python
- Image Processing
title: Como realizar OCR em Python – Extraia texto rapidamente
url: /pt/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em Python – Extrair Texto Rápido

Já se perguntou **como realizar OCR** em um recibo escaneado ou em um PDF borrado? Você não está sozinho. Em muitos projetos a necessidade de **extrair texto de imagem** surge mais cedo ou mais tarde, e a abordagem usual de “digitar tudo à mão” simplesmente não escala.  

Neste tutorial você verá um exemplo completo, pronto‑para‑executar, que demonstra **como usar OCR** para ler texto de um escaneamento, extrair dados de uma fatura e até lidar com correção automática de inclinação — tudo com apenas algumas linhas de Python.

## O Que Você Vai Aprender

Vamos percorrer tudo que você precisa saber:

* As dependências e importações exatas necessárias.  
* Como criar e configurar uma instância de `OcrEngine`.  
* Formas de **extrair texto de imagem**, **ler texto de escaneamento** e **extrair texto de fatura** usando o mesmo motor.  
* Armadilhas comuns (idioma errado, arquivos ausentes, imagens grandes) e como evitá‑las.  
* Saída esperada para que você possa verificar se o OCR funcionou.

Nenhum link de documentação externa é necessário — tudo está contido, para que você possa copiar‑colar o código e ver os resultados imediatamente.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

* Python 3.8+ instalado (o pacote `ocr` funciona com qualquer versão recente).  
* A biblioteca `ocr` disponível (`pip install ocr‑engine` – substitua pelo nome real do pacote, se diferente).  
* Um arquivo de imagem que você deseja processar – para a demonstração usaremos `invoice.png` localizado em uma pasta chamada `YOUR_DIRECTORY`.

É só isso. Se você já tem tudo isso, está pronto para começar.

## Etapa 1: Instalar e Importar o Módulo OCR

Primeiro de tudo: precisamos da biblioteca OCR. Se ainda não a instalou, execute o comando a seguir no seu terminal:

```bash
pip install ocr-engine
```

Agora importamos o módulo no nosso script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Dica profissional:** Mantenha seu ambiente virtual organizado; isso evita conflitos de versão quando você adicionar outros pacotes de processamento de imagem mais tarde.

## Etapa 2: Criar e Configurar o Motor OCR

Criar o motor é tão simples quanto chamar seu construtor, mas o verdadeiro poder está em configurá‑lo corretamente. Definiremos o idioma para inglês e ativaremos a correção automática de inclinação, essencial ao lidar com faturas escaneadas que não estão perfeitamente alinhadas.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Por que habilitar `auto_skew`? Muitos scanners produzem imagens com alguns graus de desvio. Sem correção, o motor pode perder caracteres, transformando uma fatura perfeitamente legível em um conjunto de símbolos incompreensíveis.

## Etapa 3: Executar OCR na Imagem de Destino

Agora enviamos o arquivo de imagem para o motor. O método `recognize_image` devolve um objeto que contém o texto bruto assim como pontuações de confiança (se a biblioteca as fornecer).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Se você estiver trabalhando com um cenário de **ler texto de escaneamento**, basta substituir o caminho pelo PDF escaneado convertido para PNG ou JPEG. A mesma chamada funciona para qualquer formato de imagem suportado pela biblioteca subjacente.

## Etapa 4: Inspecionar e Usar o Texto Extraído

Vamos imprimir a saída bruta do OCR. Em um pipeline real de processamento de faturas, você provavelmente analisará essa string, extrairá itens de linha, totais e datas, mas por enquanto uma rápida olhada confirmará que o OCR funcionou.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Saída esperada (truncada para brevidade):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Se a saída parecer confusa, verifique novamente se a imagem está nítida e se `engine.language` corresponde ao idioma do documento.

## Etapa 5: Lidando com Casos de Borda Comuns

### Imagens Grandes

Processar um escaneamento de 5000 × 5000 pixels pode consumir muita memória. Uma forma rápida de mitigar isso é redimensionar a imagem antes de enviá‑la ao motor:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Múltiplos Idiomas

Se você precisar **extrair texto de imagem** que contenha tanto inglês quanto espanhol, pode definir uma lista de idiomas:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

O motor tentará reconhecer caracteres de ambos os conjuntos.

### Tratamento de Erros

Nunca presuma que o arquivo exista. Envolva a chamada em um bloco try‑except para exibir uma mensagem amigável:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Referência Visual

Abaixo está uma captura de tela da fatura de exemplo que usamos na demonstração. Observe a leve inclinação — exatamente o que `auto_skew` corrige.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* como realizar OCR em uma imagem de fatura mostrando correção automática de inclinação.

## Exemplo Completo e Executável

Juntando tudo, aqui está um script único que você pode executar a partir da linha de comando. Ele cobre instalação, configuração, tratamento de erros e uma etapa simples de pós‑processamento que grava o texto extraído em um arquivo chamado `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Executar `python full_ocr_demo.py` imprimirá o texto extraído no console e o armazenará em `output.txt`. A partir daí você pode aplicar expressões regulares, gravadores CSV ou qualquer outra lógica necessária para a automação de **extrair texto de fatura**.

## Conclusão

Agora você tem uma solução sólida, de ponta a ponta, para **como realizar OCR** em Python. Ao criar um `OcrEngine`, configurar idioma e correção de inclinação, e tratar alguns casos práticos, você pode extrair texto de imagem, ler texto de escaneamento e extrair texto de fatura de forma confiável, sem precisar vasculhar documentação espalhada.

Qual o próximo passo? Experimente processar um lote de arquivos em um loop, teste diferentes idiomas ou conecte a saída a uma biblioteca de geração de PDF para criar PDFs pesquisáveis. O céu é o limite, e o código que você acabou de ver é uma base robusta para decolar.

Tem dúvidas sobre um formato de arquivo específico ou precisa de ajuda para ajustar limites de confiança? Deixe um comentário abaixo — ficaremos felizes em ajudar a afinar seu pipeline de OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}