---
category: general
date: 2026-06-25
description: Obtenez rapidement les caractères pris en charge par l'OCR en utilisant
  la bibliothèque aocr. Apprenez à lister les caractères OCR, à définir les langues
  et à déboguer votre moteur OCR en Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: fr
og_description: Obtenez les caractères pris en charge par l’OCR avec aocr. Ce guide
  vous montre comment lister les caractères OCR, choisir les langues et gérer les
  cas limites en Python.
og_title: Obtenez les caractères pris en charge par l'OCR en Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Obtenez les caractères pris en charge par l’OCR en Python – Guide complet
url: /fr/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir les caractères pris en charge par l’OCR en Python – Guide complet

Vous êtes-vous déjà demandé comment **obtenir les caractères pris en charge par l’OCR** pour une langue spécifique lorsque vous bricolez avec un moteur OCR ? Vous n’êtes pas seul. Que vous construisiez un scanner de reçus ou un analyseur de documents multilingues, connaître exactement quels glyphes votre moteur peut reconnaître est un vrai sauveur. Dans ce tutoriel, nous parcourrons l’ensemble du processus — installation de la bibliothèque, configuration de la langue, puis affichage de ces caractères — pour que vous puissiez déboguer et affiner votre pipeline OCR en quelques minutes.

Nous utiliserons la bibliothèque **aocr**, un moteur OCR Python léger qui rend la requête des capacités linguistiques très simple. À la fin de ce guide, vous serez capable de **lister les caractères OCR**, de basculer entre les **langues OCR prises en charge**, et même d’identifier les lacunes de couverture avant qu’elles ne vous posent problème en production.

---

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Python 3.8 ou plus récent (le paquet aocr ne supporte plus la version 3.7)
* Un terminal ou invite de commande avec accès à Internet
* Une connaissance de base du scripting Python (si vous avez déjà écrit un `print()`, vous êtes bon)

Aucune dépendance externe lourde — seul le paquet pip `aocr` est requis.

---

## Installer la bibliothèque aocr (Moteur OCR Python)

La première chose dont vous avez besoin est une installation fonctionnelle du **moteur OCR Python**. Le paquet aocr est disponible sur PyPI, donc une simple commande pip suffit :

```bash
pip install aocr
```

Si vous utilisez un environnement virtuel (fortement recommandé), activez‑le d’abord :

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Astuce :** épinglez la version (`pip install aocr==1.2.4`) pour éviter les changements inattendus d’API plus tard.

---

## Choisir une langue (Langues OCR prises en charge)

aocr fournit un petit nombre de packs de langues intégrés. Chaque pack définit l’ensemble des points de code Unicode que le moteur peut reconnaître. Pour interroger ces packs, vous devez définir l’attribut `language` sur l’instance du moteur.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Vous pouvez remplacer `aocr.Language.ENGLISH` par n’importe quelle autre valeur d’énumération (`FRENCH`, `GERMAN`, etc.). Si vous essayez d’assigner une langue qui n’est pas fournie, aocr lève une `ValueError`. C’est pourquoi il est judicieux de vérifier d’abord la liste des **langues OCR prises en charge** :

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Récupérer l’ensemble des caractères (Obtenir les caractères OCR pris en charge)

Voici le cœur du tutoriel : réellement **obtenir les caractères OCR pris en charge**. Le moteur expose une méthode pratique appelée `get_supported_characters()` qui renvoie une liste de chaînes d’un seul caractère.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

En coulisses, aocr lit un fichier JSON fourni avec le pack de langue et convertit chaque point de code Unicode en une chaîne Python. Le résultat est déterministe, ce qui signifie que vous obtiendrez la même liste à chaque exécution du script sur la même version de langue.

---

## Afficher le nombre de caractères pris en charge

Connaître le nombre vous aide à évaluer rapidement l’étendue de la couverture. Pour l’anglais, vous verrez généralement quelques milliers de caractères (y compris la ponctuation et les chiffres).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

L’appel `len()` est O(1) parce que Python stocke la longueur de la liste en interne, il n’y a donc aucune pénalité de performance même pour de grands alphabets.

---

## Prévisualiser les 100 premiers caractères pris en charge

Un rapide contrôle visuel peut révéler si le moteur inclut les symboles dont vous avez besoin (par exemple le signe Euro ou les guillemets typographiques). Imprimons les cent premiers caractères :

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

L’opération `join` concatène la tranche en une chaîne unique, ce qui est plus lisible que d’imprimer une liste Python.

---

## Script complet – Toutes les étapes en un seul endroit

Voici l’exemple complet, exécutable, qui rassemble tout. Enregistrez‑le sous le nom `list_supported_chars.py` et lancez `python list_supported_chars.py` depuis votre terminal.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Sortie attendue (troncature pour la brièveté) :**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Le nombre exact peut varier légèrement selon la version de aocr, mais vous verrez toujours un long alphabet accompagné de la ponctuation courante.

---

## Gestion des cas particuliers

### Que faire si le pack de langue est absent ?

Si vous demandez une langue qui n’est pas fournie, `aocr.Language` ne contiendra pas l’énumération, et vous obtiendrez une `AttributeError`. Protégez‑vous avec une vérification simple :

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Liste de caractères vide

Certaines langues rares peuvent renvoyer une liste vide si les données d’entraînement sous‑jacentes sont incomplètes. Dans ce cas, vous pouvez revenir à une langue par défaut (par ex. l’anglais) ou émettre un avertissement :

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalisation Unicode

La liste peut contenir des caractères combinés (par ex., “é” sous forme `e` + accent aigu). Si votre traitement en aval attend des glyphes précomposés, effectuez une étape de normalisation :

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Astuces pro pour les projets réels

* **Mettre en cache la liste de caractères** – Si vous traitez des milliers d’images, appeler `get_supported_characters()` à chaque itération ajoute une surcharge inutile. Stockez la liste dans une variable de niveau module ou sérialisez‑la en JSON pour une réutilisation ultérieure.
* **Validation inter‑langues** – Lorsque vous supportez plusieurs langues dans une même application, intersectez les ensembles de caractères pour trouver un sous‑ensemble commun. Cela vous aide à concevoir des éléments d’interface cohérents entre les paramètres régionaux.
* **Débogage des échecs OCR** – Si le moteur classe mal un glyphe, comparez le caractère incriminé avec le résultat de `list_supported_chars`. S’il manque, vous avez identifié une lacune de couverture qui pourra nécessiter un entraînement personnalisé.
* **Combiner avec des polices personnalisées** – aocr respecte la plage Unicode, mais la qualité de rendu peut varier selon la police. Testez vos caractères pris en charge avec la police exacte que vous utiliserez en production afin d’éviter les mauvaises surprises.

---

## FAQ

**Q : Cela fonctionne‑t‑il avec la version 2.x de aocr ?**  
R : Oui, la méthode `get_supported_characters()` est stable entre les versions 1.x et 2.x. Le seul changement est que les énumérations de langues ont été déplacées vers `aocr.languages`.

**Q : Puis‑je obtenir le point de code Unicode pour chaque caractère ?**  
R : Absolument. Utilisez `ord(ch)` dans une compréhension de liste :

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q : Qu’en est‑il des scripts de droite à gauche comme l’arabe ?**  
R : aocr inclut une énumération `ARABIC`. La liste de caractères contiendra les glyphes arabes, mais vous devrez peut‑être activer le rendu RTL dans votre interface en aval.

---

## Conclusion

Vous savez maintenant **comment obtenir les caractères pris en charge par l’OCR** avec la bibliothèque aocr en Python, comment basculer entre les **langues OCR prises en charge**, et pourquoi **lister les caractères OCR** est essentiel pour des pipelines de reconnaissance de texte robustes. Armé du script complet et des conseils ci‑dessus, vous pouvez rapidement vérifier la couverture linguistique, déboguer les glyphes manquants et créer des applications OCR plus intelligentes.

Prêt pour l’étape suivante ? Essayez d’associer cette liste de caractères à un filtre de listes de mots personnalisé, ou expérimentez avec un autre moteur OCR (Tesseract, EasyOCR) et comparez les résultats. Plus vous explorez, meilleures seront vos solutions OCR.

Bon codage, et que vos jeux de caractères soient toujours complets !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Spécifier les caractères autorisés OCR – Utilisation d’Aspose.OCR pour .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Comment OCR du texte d’image avec langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Post‑traitement OCR – Obtenir les choix de caractères](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}