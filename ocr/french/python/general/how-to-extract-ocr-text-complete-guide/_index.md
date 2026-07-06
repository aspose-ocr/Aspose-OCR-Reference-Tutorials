---
category: general
date: 2026-02-22
description: Apprenez à extraire le texte OCR et à améliorer la précision de l'OCR
  grâce au post‑traitement par IA. Nettoyez facilement le texte OCR en Python avec
  un exemple étape par étape.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: fr
og_description: Découvrez comment extraire le texte OCR, améliorer la précision de
  l’OCR et nettoyer le texte OCR à l’aide d’un flux de travail Python simple avec
  un post‑traitement IA.
og_title: Comment extraire du texte OCR – Guide étape par étape
tags:
- OCR
- AI
- Python
title: Comment extraire le texte OCR – Guide complet
url: /fr/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte OCR – Tutoriel de programmation complet

Vous vous êtes déjà demandé **comment extraire l'OCR** d'un document numérisé sans vous retrouver avec un fouillis de fautes de frappe et de lignes cassées ? Vous n'êtes pas seul. Dans de nombreux projets réels, la sortie brute d'un moteur OCR ressemble à un paragraphe confus, et le nettoyer ressemble à une corvée.  

La bonne nouvelle ? En suivant ce guide, vous verrez une méthode pratique pour extraire des données OCR structurées, exécuter un post‑processeur IA, et obtenir **du texte OCR propre** prêt pour l'analyse en aval. Nous aborderons également des techniques pour **améliorer la précision de l'OCR** afin que les résultats soient fiables du premier coup.

Dans les quelques minutes qui suivent, nous couvrirons tout ce dont vous avez besoin : les bibliothèques requises, un script complet exécutable, et des astuces pour éviter les pièges courants. Pas de raccourcis vagues du type « voir la documentation » — seulement une solution complète et autonome que vous pouvez copier‑coller et exécuter.

## Ce dont vous avez besoin

- Python 3.9+ (le code utilise des annotations de type mais fonctionne sur les versions 3.x plus anciennes)
- Un moteur OCR capable de renvoyer un résultat structuré (par ex., Tesseract via `pytesseract` avec le drapeau `--psm 1`, ou une API commerciale qui fournit des métadonnées de blocs/lignes)
- Un modèle de post‑traitement IA — pour cet exemple nous le simulerons avec une fonction simple, mais vous pouvez le remplacer par `gpt‑4o-mini` d'OpenAI, Claude, ou tout LLM qui accepte du texte et renvoie une sortie nettoyée
- Quelques images d'exemple (PNG/JPG) pour tester

Si vous avez tout cela prêt, plongeons‑y.

## Comment extraire l'OCR – Récupération initiale

La première étape consiste à appeler le moteur OCR et à lui demander une **représentation structurée** au lieu d'une simple chaîne. Les résultats structurés conservent les limites de blocs, de lignes et de mots, ce qui rend le nettoyage ultérieur beaucoup plus facile.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Pourquoi cela importe :** En préservant les blocs et les lignes, nous évitons d'avoir à deviner où commencent les paragraphes. La fonction `recognize_structured` nous fournit une hiérarchie propre que nous pouvons ensuite alimenter dans un modèle IA.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Exécuter l'extrait affiche la première ligne exactement comme le moteur OCR l'a vue, contenant souvent des erreurs de reconnaissance comme « 0cr » au lieu de « OCR ».

## Améliorer la précision de l'OCR avec le post‑traitement IA

Maintenant que nous disposons de la sortie structurée brute, passons‑la à un post‑processeur IA. Le but est d'**améliorer la précision de l'OCR** en corrigeant les erreurs courantes, en normalisant la ponctuation, et même en re‑segmentant les lignes si nécessaire.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Astuce pro :** Si vous n'avez pas d'abonnement LLM, vous pouvez remplacer l'appel par un transformeur local (par ex., `sentence‑transformers` + un modèle de correction finement ajusté) ou même une approche basée sur des règles. L'idée clé est que l'IA voit chaque ligne isolément, ce qui suffit généralement à **nettoyer le texte OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Vous devriez maintenant voir une phrase beaucoup plus propre — fautes corrigées, espaces superflus supprimés, et ponctuation ajustée.

## Nettoyer le texte OCR pour de meilleurs résultats

Même après la correction IA, vous pourriez vouloir appliquer une étape de désinfection finale : supprimer les caractères non‑ASCII, unifier les sauts de ligne, et réduire les espaces multiples. Cette passe supplémentaire garantit que la sortie est prête pour les tâches en aval comme le NLP ou l'ingestion dans une base de données.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

La fonction `final_cleanup` vous fournit une chaîne brute que vous pouvez injecter directement dans un index de recherche, un modèle de langage, ou une exportation CSV. Comme nous avons conservé les limites de blocs, la structure des paragraphes est préservée.

## Cas limites et scénarios « et si »

- **Mises en page multi‑colonnes  :** Si votre source comporte des colonnes, le moteur OCR peut intercaler les lignes. Vous pouvez détecter les coordonnées des colonnes à partir de la sortie TSV et réordonner les lignes avant de les envoyer à l'IA.
- **Scripts non‑latins  :** Pour des langues comme le chinois ou l'arabe, modifiez l'invite du LLM pour demander une correction spécifique à la langue, ou utilisez un modèle finement ajusté sur ce script.
- **Documents volumineux  :** Envoyer chaque ligne individuellement peut être lent. Regroupez les lignes (par ex., 10 par requête) et laissez le LLM renvoyer une liste de lignes nettoyées. N'oubliez pas de respecter les limites de tokens.
- **Blocs manquants  :** Certains moteurs OCR ne renvoient qu'une liste plate de mots. Dans ce cas, vous pouvez reconstruire les lignes en regroupant les mots avec des valeurs `line_num` similaires.

## Exemple complet fonctionnel

En réunissant tous les éléments, voici un fichier unique que vous pouvez exécuter de bout en bout. Remplacez les espaces réservés par votre propre clé API et le chemin de l'image.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}