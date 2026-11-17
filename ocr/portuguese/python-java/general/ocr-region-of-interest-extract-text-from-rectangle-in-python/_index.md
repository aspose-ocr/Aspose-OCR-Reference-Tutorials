---
category: general
date: 2026-05-31
description: Aprenda a usar a região de interesse de OCR para carregar a imagem e
  extrair texto de um retângulo, perfeito para reconhecer o valor em uma fatura.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: pt
og_description: Domine a região de interesse do OCR para carregar a imagem, extrair
  texto de um retângulo e reconhecer o texto de uma fatura em um único tutorial.
og_title: OCR Região de Interesse – Guia Python Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Região de Interesse – Extrair Texto de um Retângulo em Python
url: /pt/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Região de Interesse de OCR – Extrair Texto de um Retângulo em Python

Já se perguntou como **ocr region of interest** uma parte específica de uma nota fiscal digitalizada sem alimentar a página inteira no motor? Você não é o primeiro a encarar um recibo borrado e pensar: “Como extrair o valor que está em algum lugar no canto inferior direito?” A boa notícia é que você pode dizer à biblioteca de OCR exatamente onde olhar, aumentando drasticamente a velocidade e a precisão.

Neste guia vamos percorrer um exemplo completo e executável que mostra como **load image for OCR**, definir uma **region of interest**, e então **extract text from rectangle** para, finalmente, **recognize text from invoice** e responder à clássica pergunta “como extrair o valor”. Sem referências vagas — apenas código concreto, explicações claras e algumas dicas profissionais que você desejará ter conhecido antes.

---

## O que Você Vai Construir

Ao final deste tutorial você terá um pequeno script Python que:

1. Carrega uma imagem de nota fiscal do disco.  
2. Marca um ROI retangular onde o valor total está localizado.  
3. Executa OCR apenas dentro desse ROI.  
4. Imprime a string do valor já limpa.  

Tudo isso funciona com qualquer biblioteca de OCR que suporte ROI — aqui usaremos um pacote fictício, porém representativo, `SimpleOCR` que imita ferramentas populares como Tesseract ou EasyOCR. Sinta‑se à vontade para substituí‑lo; os conceitos permanecem os mesmos.

---

## Pré‑requisitos

- Python 3.8+ instalado (`python --version` deve mostrar ≥3.8).  
- Um pacote de OCR instalável via pip (ex.: `pip install simpleocr`).  
- Uma imagem de nota fiscal (PNG ou JPEG) colocada em uma pasta que você possa referenciar.  
- Familiaridade básica com funções e classes Python (nada sofisticado).

Se você já tem tudo isso, ótimo — vamos mergulhar. Caso contrário, obtenha a imagem primeiro; o resto das etapas é independente do conteúdo real do arquivo.

---

## Etapa 1: Load Image for OCR

A primeira coisa que qualquer fluxo de OCR precisa é um bitmap para ler. A maioria das bibliotecas expõe um método simples `load_image` que aceita um caminho de arquivo. Veja como fazer isso com o nosso motor `SimpleOCR`:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Use caminhos absolutos ou `os.path.join` para evitar surpresas de “arquivo não encontrado” ao executar o script a partir de um diretório de trabalho diferente.

---

## Etapa 2: Definir OCR Region of Interest

Em vez de deixar o motor escanear a página inteira, dizemos a ele *exatamente* onde o valor está. Esta é a etapa **ocr region of interest**, e é a chave para uma extração confiável, especialmente quando o documento contém cabeçalhos ou rodapés ruidosos.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Por que esses números? `x` e `y` são deslocamentos em pixels a partir do canto superior esquerdo, enquanto `width` e `height` descrevem o tamanho da caixa. Se estiver em dúvida, abra a imagem em qualquer editor, habilite uma régua e anote as coordenadas. Muitas IDEs até permitem imprimir a posição do cursor ao passar o mouse.

---

## Etapa 3: Extract Text from Rectangle

Agora que o ROI está definido, pedimos ao motor para **recognize text from invoice** limitado ao retângulo que acabamos de adicionar. A chamada retorna um objeto de resultado que normalmente contém a string bruta, pontuações de confiança e, às vezes, caixas delimitadoras.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Nos bastidores, `recognize()` itera sobre cada ROI, recorta aquela fatia, executa o modelo de OCR e junta os resultados. É por isso que definir uma região **extract text from rectangle** bem ajustada pode economizar segundos no tempo de processamento de trabalhos em lote.

---

## Etapa 4: Como Extrair o Valor – Limpar a Saída

OCR não é perfeito; você frequentemente obterá espaços extras, quebras de linha ou até caracteres lidos incorretamente (pense em “S” vs “5”). Um rápido `strip()` e uma regex pequena geralmente resolvem valores monetários.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Por que isso importa:** Se você pretende inserir o valor em um banco de dados ou em um gateway de pagamento, precisa de um formato previsível. Remover espaços em branco e filtrar caracteres não numéricos evita erros posteriores.

---

## Etapa 5: Recognize Text from Invoice – Script Completo

Juntando tudo, aqui está o script completo, pronto para ser executado. Salve como `extract_amount.py` e execute `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Saída Esperada

```
Amount: 1,245.67
```

Se o ROI estiver desalinhado, você pode ver algo como `Amount: 1245.6S` — note o “S” solto. Ajuste as coordenadas do retângulo e execute novamente até que a saída esteja limpa.

---

## Armadilhas Comuns & Casos de Borda

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| **ROI muito pequeno** | O texto do valor fica cortado, levando a reconhecimento parcial. | Expanda `width`/`height` em ~10‑20 % e teste novamente. |
| **DPI incorreto** | Digitalizações de baixa resolução (≤150 dpi) reduzem a precisão do OCR. | Reamostre a imagem para 300 dpi antes de carregar, ou solicite ao scanner uma DPI maior. |
| **Múltiplas moedas** | A regex captura o primeiro grupo numérico, que pode ser o número da nota. | Refine a regex para procurar símbolos de moeda (`$`, `€`, `£`) antes dos dígitos. |
| **Faturas rotacionadas** | Motores de OCR assumem texto vertical; páginas rotacionadas quebram o reconhecimento. | Aplique correção de rotação (`ocr_engine.rotate(90)`) antes de adicionar o ROI. |
| **Ruído de fundo** | Sombras ou carimbos confundem o modelo. | Pré‑processar com um simples limiar (`cv2.threshold`) ou usar um filtro de redução de ruído. |

Abordar esses casos de borda cedo salva horas de depuração depois.

---

## Dicas Profissionais para Projetos Reais

- **Processamento em Lote:** Percorra uma pasta de faturas, calcule o ROI dinamicamente (ex.: com base em detecção de modelo) e armazene os resultados em CSV.  
- **Correspondência de Modelo:** Se você lida com vários layouts de fatura, mantenha um mapa JSON de `template_id → coordenadas do ROI`. Troque o ROI com base em um classificador rápido de layout.  
- **Execução Paralela:** Use `concurrent.futures.ThreadPoolExecutor` para rodar múltiplas instâncias de OCR simultaneamente — ótimo para pipelines de back‑office de alto volume.  
- **Filtragem por Confiança:** A maioria dos resultados de OCR inclui uma pontuação de confiança. Descarte resultados abaixo de um limiar (ex.: 85 %) e marque‑os para revisão manual.

---

## Conclusão

Cobrimos tudo o que você precisa para **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, e finalmente **recognize text from invoice** para responder à clássica pergunta **how to extract amount**. O script é compacto, mas flexível o suficiente para se adaptar a diferentes formatos de documento, idiomas e back‑ends de OCR.

Agora que você dominou o básico, considere estender o fluxo: adicione leitura de código de barras, integre com um parser de PDF ou envie o valor extraído para uma API contábil. O céu é o limite, e com um ROI bem definido você sempre obterá resultados mais rápidos e limpos.

Se encontrar algum problema, deixe um comentário abaixo — boa extração de OCR!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## O que Você Deve Aprender a Seguir?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}