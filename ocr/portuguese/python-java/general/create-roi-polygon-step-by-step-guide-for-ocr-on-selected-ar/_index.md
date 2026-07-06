---
category: general
date: 2026-03-26
description: Crie um polígono de ROI para executar OCR na área selecionada. Aprenda
  como definir múltiplas regiões, registrá‑las e extrair texto com um motor OCR em
  Python.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: pt
og_description: Crie um polígono de ROI e execute OCR na área selecionada com um motor
  Python. Código completo, explicações e dicas incluídos.
og_title: Criar Polígono ROI – OCR Rápido na Área Selecionada
tags:
- OCR
- Python
- Image Processing
title: Criar Polígono de ROI – Guia passo a passo para OCR na área selecionada
url: /pt/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Polígono ROI – Tutorial Completo para OCR em Área Selecionada

Já precisou **criar um polígono ROI** para executar OCR apenas na parte da imagem que importa? Talvez você esteja escaneando recibos e só os totais importam, ou tenha um formulário onde apenas o campo de assinatura precisa ser lido. Nesses casos, **ocr em área selecionada** economiza tempo e aumenta a precisão.  

Neste guia vamos percorrer tudo o que você precisa: desde definir dois polígonos, registrá‑los em um motor OCR, até extrair o texto reconhecido em uma única chamada limpa. Ao final você terá um script pronto‑para‑executar e uma compreensão sólida de por que focar em regiões de interesse é importante.

## O que você aprenderá

- Como **criar objetos de polígono ROI** usando uma biblioteca OCR típica.  
- A diferença entre definir uma única região versus múltiplas.  
- Como registrar essas regiões no motor para que `ocr em área selecionada` seja executado.  
- Saída esperada e como solucionar armadilhas comuns (por exemplo, ROIs sobrepostos, resultados vazios).

### Pré-requisitos

- Python 3.8+ instalado.  
- Uma biblioteca OCR que exponha os métodos `Polygon`, `Point` e `add_region_of_interest` (o exemplo usa um módulo fictício `ocr`; substitua pelo seu SDK real, como wrappers do Tesseract‑Python ou EasyOCR).  
- Um arquivo de imagem de exemplo (`sample.png`) que contenha texto nas coordenadas mostradas abaixo.

> **Dica profissional:** Se estiver usando uma biblioteca real, certifique‑se de que a imagem seja carregada no mesmo espaço de coordenadas (origem no canto superior‑esquerdo, X aumentando para a direita, Y aumentando para baixo).  

---  

## Passo 1: Importar o Módulo OCR e Carregar sua Imagem  

Primeiro, traga o pacote OCR para o escopo e leia a imagem que você deseja processar.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Por que isso importa:* O motor precisa dos dados da imagem antes que você possa anexar qualquer **polígono ROI**. Algumas bibliotecas também permitem passar a imagem depois, mas inicializar cedo mantém o fluxo de trabalho organizado.

## Passo 2: Definir o Primeiro Polígono ROI  

Agora criamos a primeira região de interesse. Pense nisso como desenhar um retângulo ao redor do cabeçalho de uma tabela.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explicação:*  
- `ocr.Point(x, y)` usa coordenadas em pixels.  
- A lista de pontos está ordenada no sentido horário, que a maioria dos motores espera.  
- Você pode adicionar quantos pontos quiser para criar formas irregulares; um retângulo é apenas um caso especial.

## Passo 3: Definir Polígonos ROI Adicionais (Opcional)  

Você não precisa parar em um só. Aqui está um segundo polígono que captura um campo de assinatura mais abaixo na página.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Por que adicionar mais?* Executar **ocr em área selecionada** para múltiplas zonas permite extrair pedaços de dados diferentes em uma única passagem, o que é muito mais rápido que recortar e processar cada trecho separadamente.

## Passo 4: Registrar os ROIs no Motor OCR  

Com os polígonos prontos, informe ao motor quais áreas inspecionar.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Nota importante:* Alguns SDKs exigem que você chame um método `clear_regions()` antes de adicionar novos se reutilizar o motor para outra imagem.

## Passo 5: Executar OCR e Recuperar o Texto  

Finalmente, dispare o reconhecimento. O motor olhará apenas dentro dos polígonos que acabamos de adicionar.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Saída esperada** (supondo que `sample.png` contenha as palavras “Invoice Total: $123.45” no primeiro ROI e “Signature: John Doe” no segundo):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Se a saída estiver vazia, verifique novamente se as coordenadas realmente intersectam texto e se a resolução da imagem corresponde ao sistema de coordenadas.

## Casos de Borda e Armadilhas Comuns  

| Situação                               | O que observar                                   | Correção / Solução                              |
|----------------------------------------|--------------------------------------------------|-------------------------------------------------|
| **ROIs sobrepostos**                    | O texto pode ser retornado duas vezes.          | Mantenha os polígonos disjuntos ou deduplicate a saída. |
| **ROI fora dos limites da imagem**      | O motor pode gerar erro ou não retornar nada.   | Limite as coordenadas a `0 ≤ x < width`, `0 ≤ y < height`. |
| **ROI muito pequeno**                   | A precisão do OCR cai por falta de pixels.      | Expanda o polígono alguns pixels ou aumente a resolução da imagem primeiro. |
| **Forma não retangular**                | Alguns motores suportam apenas polígonos convexos. | Divida formas complexas em múltiplos ROIs convexos. |
| **Alteração do tamanho da imagem**      | Coordenadas codificadas ficam inválidas.         | Calcule as coordenadas do ROI em relação às dimensões da imagem (por exemplo, porcentagens). |

## Exemplo Completo Funcionando  

Abaixo está o script completo que você pode copiar‑colar e executar (substitua `ocr` pela sua biblioteca real).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Execute-o com `python ocr_roi_example.py` e você deverá ver as strings extraídas das duas zonas definidas.

## Próximos Passos  

- **Geração dinâmica de ROI:** Em vez de codificar coordenadas, use processamento de imagem (por exemplo, detecção de contornos com OpenCV) para localizar automaticamente tabelas ou campos.  
- **Pós‑processamento:** Remova espaços em branco, aplique expressões regulares ou converta números para tipos de dados adequados.  
- **Processamento em lote:** Percorra uma pasta de imagens, reutilizando as mesmas definições de ROI se o layout for consistente.  

Se você estiver curioso sobre **ocr em área selecionada** para documentos mais complexos—pense em PDFs de várias páginas ou formulários escaneados—investigue bibliotecas que suportam registro de ROI por página.  

---  

### Visão Geral Visual  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="exemplo de criação de polígono roi mostrando duas áreas selecionadas"}

O diagrama ilustra como os dois retângulos (azul e verde) se mapeiam sobre a imagem subjacente, destacando exatamente o que o motor OCR lerá.

---  

## Conclusão  

Acabamos de **criar objetos de polígono ROI**, registrá‑los em um motor OCR e executar `ocr em área selecionada` em um script limpo e reproduzível. Ao limitar o motor às zonas que importam, você reduz o tempo de processamento, melhora a precisão e simplifica o tratamento posterior dos dados.  

Experimente com suas próprias imagens—ajuste as coordenadas, adicione mais polígonos ou conecte a saída a um banco de dados. O céu é o limite quando você domina OCR baseado em regiões.  

Tem perguntas ou quer compartilhar um caso de uso interessante? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}