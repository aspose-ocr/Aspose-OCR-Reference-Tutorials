---
category: general
date: 2026-05-03
description: Extrayez du texte d’une image instantanément avec Aspose OCR. Apprenez
  à définir la région d’intérêt, charger l’image pour l’OCR et extraire le texte d’une
  facture en quelques minutes.
draft: false
keywords:
- extract text from image
- define region of interest
- load image for ocr
- extract text from invoice
- process image with ocr
language: fr
og_description: Extraire du texte d’une image à l’aide d’Aspose OCR. Ce guide montre
  comment définir la région d’intérêt, charger l’image pour l’OCR et extraire le texte
  d’une facture efficacement.
og_title: Extraire du texte d’une image avec Aspose OCR – Tutoriel complet
tags:
- ocr
- python
- image-processing
title: Extraire du texte d’une image avec Aspose OCR – Guide étape par étape
url: /fr/python-java/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec Aspose OCR – Guide étape par étape

Besoin d'**extraire du texte d'une image** rapidement ? Vous n'êtes pas seul—les développeurs luttent constamment contre les scans bruyants, les reçus et les factures. Dans ce tutoriel, nous parcourrons une solution complète qui montre non seulement comment *extraire du texte d'une image*, mais aussi comment **définir une région d'intérêt**, **charger une image pour l'OCR**, et extraire la ligne exacte dont vous avez besoin dans une facture.  

Nous couvrirons tout, de l'installation de la bibliothèque Aspose OCR à la gestion des cas limites comme les pages tournées. À la fin, vous disposerez d'un script exécutable qui extrait le texte souhaité en un seul appel—sans recadrage manuel.  

## Ce que vous apprendrez

- Comment **charger une image pour l'OCR** en utilisant l'API Python d'Aspose.  
- La meilleure façon de **définir une région d'intérêt** (ROI) afin de ne traiter que la partie de l'image qui importe.  
- Comment **extraire du texte d'une facture** sans récupérer toute la page.  
- Astuces pour **traiter une image avec l'OCR** efficacement et éviter les pièges courants.  

**Prérequis** – un environnement Python 3.9+ récent, un fichier de licence Aspose OCR valide, et une image (par ex., un PNG de facture). Aucun autre outil externe n'est requis.

---

## Étape 1 – Initialiser le moteur OCR (Configuration principale)

Avant de pouvoir **traiter une image avec l'OCR**, vous avez besoin d'une instance du moteur qui possède votre licence. Cette étape est cruciale car un moteur non licencié ne renverra qu'un jeu de résultats limité.

```python
import aspose.ocr as ocr  # Make sure you installed aspose-ocr via pip

# Create the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with your actual .lic file location
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

*Pourquoi c'est important* : l'objet `OcrEngine` est le cœur de la bibliothèque ; il gère les modèles linguistiques, le prétraitement d'image et la licence. Configurer la licence dès le départ garantit une précision totale et aucune filigrane.

---

## Étape 2 – Charger l'image pour l'OCR

Maintenant que le moteur est prêt, nous devons **charger l'image pour l'OCR**. Aspose prend en charge de nombreux formats (PNG, JPEG, TIFF), mais l'utilisation de `Image.from_file` garantit que l'image est décodée correctement.

```python
# Load the target image – change the path to point at your invoice file
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.from_file(image_path)
```

> **Astuce pro** : Gardez vos fichiers image en dessous de 5 Mo pour un traitement le plus rapide possible. Les fichiers plus volumineux peuvent être réduits avec `image.resize(width, height)` avant l'OCR.

---

## Étape 3 – Définir la région d'intérêt (ROI)

La plupart des factures contiennent beaucoup de texte superflu—blocs d'adresse, pieds de page, etc. En **définissant une région d'intérêt**, nous indiquons au moteur de ne regarder que là où se trouvent le montant ou la date, ce qui améliore la vitesse et la précision.

```python
# Define ROI: (x, y, width, height) in pixels
# Adjust these numbers based on the layout of your specific invoice
roi = ocr.Rectangle(150, 300, 400, 120)
```

*Comment ça fonctionne* : la classe `Rectangle` recadre l'image virtuellement ; le moteur OCR ne voit jamais les pixels en dehors du rectangle, ainsi le bruit hors de la ROI est ignoré.

---

## Étape 4 – Reconnaître le texte à l'intérieur de la ROI

Avec le moteur, l'image et la ROI prêts, nous **extraitons enfin le texte de l'image**. La méthode `recognize` renvoie un objet `OcrResult` contenant la chaîne détectée et les scores de confiance.

```python
# Perform OCR only within the defined ROI
ocr_result = ocr_engine.recognize(image, roi=roi)

# Print the raw extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

**Sortie attendue** (exemple pour une ligne de total de facture typique) :

```
Text inside ROI:
Total Amount: $1,245.67
```

Si la ROI est correctement positionnée, vous ne verrez que la ligne dont vous avez besoin—rien d'autre.

---

## Étape 5 – Exemple complet fonctionnel (prêt à copier‑coller)

Ci-dessous le script complet qui regroupe toutes les étapes précédentes. Enregistrez-le sous le nom `extract_invoice_roi.py` et exécutez `python extract_invoice_roi.py`.

```python
# extract_invoice_roi.py
import aspose.ocr as ocr

def main():
    # 1️⃣ Initialize OCR engine and apply license
    ocr_engine = ocr.OcrEngine()
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image you want to process
    image = ocr.Image.from_file("YOUR_DIRECTORY/invoice.png")

    # 3️⃣ Define the region of interest (ROI) – rectangle where the text lives
    roi = ocr.Rectangle(150, 300, 400, 120)   # (x, y, width, height)

    # 4️⃣ Recognize text only inside the ROI
    ocr_result = ocr_engine.recognize(image, roi=roi)

    # 5️⃣ Display the extracted text
    print("Text inside ROI:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Exécutez le script et vous devriez voir la ligne ciblée affichée dans la console. Si vous obtenez une chaîne vide, revérifiez les coordonnées de la ROI — quelques pixels de décalage peuvent exclure complètement le texte.

---

## Étape 6 – Variations courantes et cas limites

### a) Dispositions de factures différentes

Les factures de différents fournisseurs déplacent souvent la zone du total. Pour **traiter une image avec l'OCR** sur plusieurs dispositions, envisagez :

- **ROIs multiples** : exécutez le moteur séquentiellement avec plusieurs rectangles et choisissez le résultat avec la plus haute confiance.  
- **Détection dynamique de ROI** : utilisez une bibliothèque de traitement d'image légère (par ex., OpenCV) pour localiser d'abord le libellé « Total », puis calculez la ROI relative à celui‑ci.

### b) Images tournées ou inclinées

Si le scan est incliné, appelez `image.rotate(angle)` avant la reconnaissance :

```python
image = image.rotate(2.5)  # Rotate 2.5 degrees clockwise
```

Aspose OCR propose également une auto‑correction d'inclinaison, mais la rotation manuelle vous donne un contrôle plus précis.

### c) Caractères non latins

Le modèle linguistique par défaut est l'anglais. Pour **extraire du texte d'une facture** rédigée dans une autre langue, définissez la langue avant la reconnaissance :

```python
ocr_engine.language = ocr.Language.French  # Example for French invoices
```

### d) Gros PDFs

Lors du traitement de PDFs multi‑pages, extrayez chaque page en tant qu'image d'abord (Aspose PDF → Image), puis appliquez la même logique de ROI page par page.

---

## Étape 7 – Conseils de performance et astuces pro

- **Mettre en cache le moteur** : créer `OcrEngine` à plusieurs reprises dans une boucle ralentit le processus. Instanciez‑le une fois et réutilisez‑le.  
- **Traitement par lots** : si vous avez des dizaines de factures, encapsulez l'appel OCR dans un `ThreadPoolExecutor` pour paralléliser le travail I/O‑bound.  
- **Vérification de la confiance** : `ocr_result.confidence` renvoie un flottant entre 0 et 1. Rejetez les résultats inférieurs à 0,85 et recourez à une ROI plus grande ou à une révision manuelle.  

> **Attention** : définir la ROI trop petite peut couper des caractères, entraînant une sortie illisible. Testez toujours avec quelques factures d'exemple avant de passer à l'échelle.

## Conclusion

Vous disposez maintenant d'une méthode solide, prête pour la production, pour **extraire du texte d'une image** avec Aspose OCR, incluant une façon de **définir une région d'intérêt**, **charger une image pour l'OCR**, et d'**extraire de façon fiable le texte des champs de facture**. En limitant l'OCR à une ROI précise, vous augmentez à la fois la vitesse et la précision—idéal pour le traitement par lots de milliers de reçus.  

Prêt pour l'étape suivante ? Essayez d'intégrer ce script dans une API Flask afin que votre application web puisse télécharger une facture et renvoyer instantanément le montant total. Ou expérimentez avec plusieurs ROIs pour extraire la date, le numéro de facture et le nom du fournisseur en une seule fois. Les possibilités sont infinies, et avec les bases couvertes ici, vous êtes bien équipé pour relever tout défi OCR.

Bon codage, et que votre texte extrait soit toujours propre !  

![Diagramme du flux montrant comment extraire du texte d'une image avec Aspose OCR](workflow.png){: .center-image alt="Diagramme du flux montrant comment extraire du texte d'une image avec Aspose OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}