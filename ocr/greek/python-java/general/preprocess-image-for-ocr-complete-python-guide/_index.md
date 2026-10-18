---
category: general
date: 2026-06-28
description: Προεπεξεργασία εικόνας για OCR με Python ώστε να αυξήσετε την ακρίβεια.
  Μάθετε μια πλήρη αλυσίδα προεπεξεργασίας εικόνας, βελτιώστε τα αποτελέσματα του
  OCR και εξάγετε κείμενο από κυριλλικές εικόνες.
draft: false
keywords:
- preprocess image for OCR
- how to improve OCR accuracy
- python OCR with preprocessing
- image preprocessing pipeline python
- extract text from Cyrillic image
language: el
og_description: Προεπεξεργασία εικόνας για OCR σε Python και μάθετε πώς να βελτιώσετε
  την ακρίβεια του OCR. Αυτός ο οδηγός σας καθοδηγεί μέσα από μια πλήρη διαδικασία
  προεπεξεργασίας και την εξαγωγή κειμένου από κυριλλικές εικόνες.
og_title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Python
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the code works on 3.10+ as well). - Basic familiarity
      with Python packages and virtual environments. - An OCR library that provides
      `OcrEngine`, `Language`, and `ImagePreprocessor` classes (e.g., a wrapper around
      Tesseract or a commercial SDK). - A sample Cyrillic image (`cyri'
  - name: Why These Three Steps?
    text: 1. **Deskew** – OCR engines assume left‑to‑right (or top‑to‑bottom) alignment.
      A few degrees of rotation can drop accuracy by 30 % or more. 2. **Binarize**
      – Converting to a binary image reduces the data the OCR engine must analyze,
      sharpening character edges. 3. **Denoise** – Small specks or compre
  - name: How This Improves OCR Accuracy
    text: '- By feeding a **clean, deskewed, binarized** image, the engine can focus
      on character shapes rather than fighting noise. - Specifying `Language.Cyrillic`
      activates the correct character set and language model, which is a key factor
      in **how to improve OCR accuracy** for non‑Latin scripts.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Python
url: /el/python-java/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Πλήρης Οδηγός Python

Έχετε αναρωτηθεί ποτέ πώς να **προεπεξεργαστείτε εικόνα για OCR** ώστε το κείμενο να βγαίνει κρυστάλλινα καθαρό; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν προβλήματα όταν η μηχανή OCR εκτυπώνει ακατάληπτους χαρακτήρες, ειδικά με κεκλιμένες ή θορυβώδεις σκανιές κυριλλικού κειμένου. Το καλό νέο; Ένα καλά σχεδιασμένο pipeline προεπεξεργασίας εικόνας μπορεί να αυξήσει δραματικά τα ποσοστά αναγνώρισης.

Σε αυτό το tutorial θα βουτήξουμε κατευθείαν σε μια **Python OCR με προεπεξεργασία** λύση που αντιμετωπίζει το deskewing, το binarization και το denoising, και στη συνέχεια θα σας δείξει πώς να **εξάγετε κείμενο από κυριλλική εικόνα**. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script, θα κατανοήσετε **πώς να βελτιώσετε την ακρίβεια του OCR**, και θα είστε έτοιμοι να προσαρμόσετε το pipeline για οποιαδήποτε γλώσσα ή πηγή εικόνας.

## Τι Θα Μάθετε

- Τον λόγο πίσω από κάθε βήμα προεπεξεργασίας και γιατί είναι σημαντικό για το OCR.  
- Πώς να συναρμολογήσετε ένα **image preprocessing pipeline python** που μπορεί να επαναχρησιμοποιηθεί σε πολλά projects.  
- Ένα πλήρες, εκτελέσιμο παράδειγμα που δημιουργεί μια μηχανή OCR, προεπεξεργάζεται μια κυριλλική εικόνα και εκτυπώνει το αναγνωρισμένο κείμενο.  
- Συμβουλές για την αντιμετώπιση ακραίων περιπτώσεων όπως έντονη κλίση, χαμηλή αντίθεση ή πολυγλωσσικά έγγραφα.  
- Ιδέες για επόμενα βήματα όπως batch processing, προσαρμοσμένα language packs, και ενσωμάτωση με cloud OCR services.

### Προαπαιτούμενα

- Python 3.8 ή νεότερη (ο κώδικας λειτουργεί και σε 3.10+).  
- Βασική εξοικείωση με πακέτα Python και εικονικά περιβάλλοντα.  
- Μια βιβλιοθήκη OCR που παρέχει τις κλάσεις `OcrEngine`, `Language` και `ImagePreprocessor` (π.χ. ένα wrapper γύρω από το Tesseract ή ένα εμπορικό SDK).  
- Ένα δείγμα κυριλλικής εικόνας (`cyrillic_skewed.jpg`) τοποθετημένο σε φάκελο που ελέγχετε.

> **Pro tip:** Αν δεν έχετε έτοιμο OCR wrapper, ρίξτε μια ματιά στο ανοιχτό‑πηγή πακέτο `pytesseract` και συνδυάστε το με `opencv-python`. Οι έννοιες σε αυτόν τον οδηγό μεταφράζονται άμεσα.

---

## Βήμα 1: Εγκατάσταση και Εισαγωγή Απαιτούμενων Πακέτων

Πρώτα, ας τακτοποιήσουμε τις εξαρτήσεις. Θα χρησιμοποιήσουμε μια υποθετική `ocr_lib` που ενσωματώνει τη μηχανή και τα εργαλεία προεπεξεργασίας. Αν χρησιμοποιείτε `pytesseract` + OpenCV, αντικαταστήστε τις εισαγωγές ανάλογα.

```python
# Install the (fictional) OCR library – replace with your actual package manager command
# pip install ocr-lib

from ocr_lib import OcrEngine, Language, ImagePreprocessor
import os
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή των σωστών κλάσεων εξασφαλίζει ότι έχουμε καθαρό διαχωρισμό μεταξύ της μηχανής OCR (αναγνώριση) και του image pre‑processor (βελτίωση). Η ανάμειξή τους μπορεί να οδηγήσει σε ακατάστατο κώδικα δύσκολο στην αποσφαλμάτωση.

---

## Βήμα 2: Δημιουργία Pipeline **Preprocess Image for OCR**

Τώρα θα δημιουργήσουμε την καρδιά του tutorial: ένα pipeline που κάνει deskew, binarize και denoise την είσοδο. Κάθε μετασχηματισμός στοχεύει σε συγκεκριμένη αδυναμία των μηχανών OCR.

```python
# Step 2: Initialise the pre‑processing chain
preprocessor = ImagePreprocessor()

# Deskew – correct rotation so text lines are horizontal
preprocessor = preprocessor.deskew()

# Binarize – convert to pure black‑and‑white using a threshold (180 works well for most scans)
preprocessor = preprocessor.binarize(threshold=180)

# Remove noise – apply a mild median filter (strength=2) to smooth speckles
preprocessor = preprocessor.removeNoise(strength=2)
```

### Γιατί Αυτά τα Τρία Βήματα;

1. **Deskew** – Οι μηχανές OCR υποθέτουν ευθυγράμμιση αριστερά‑προς‑δεξιά (ή πάνω‑προς‑κάτω). Μερικές μοίρες περιστροφής μπορούν να μειώσουν την ακρίβεια κατά 30 % ή περισσότερο.  
2. **Binarize** – Η μετατροπή σε δυαδική εικόνα μειώνει τα δεδομένα που πρέπει να αναλύσει η μηχανή OCR, ενισχύοντας τις άκρες των χαρακτήρων.  
3. **Denoise** – Μικρές κηλίδες ή τεχνητά σήματα συμπίεσης μπορούν να ληφθούν ως σημεία στίξης ή διακριτικά, ειδικά στα κυριλλικά όπου πολλά γράμματα έχουν παρόμοια σχήματα.

> **Σημείωση για ακραίες περιπτώσεις:** Αν οι πηγές σας είναι ήδη καθαρές, μπορείτε να παραλείψετε το `removeNoise` ή να μειώσετε την παράμετρο `strength`. Πολύ επιθετικό denoising μπορεί να σβήσει λεπτομέρειες όπως τα διακριτικά σημεία.

---

## Βήμα 3: Φόρτωση Εικόνας και Εφαρμογή του Pipeline

Με το pipeline έτοιμο, του δίνουμε μια διαδρομή αρχείου. Η μέθοδος `apply` επιστρέφει ένα επεξεργασμένο αντικείμενο εικόνας που η μηχανή OCR μπορεί να καταναλώσει άμεσα.

```python
# Path to the original Cyrillic image (adjust as needed)
image_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")

# Run the preprocessing pipeline
processed_image = preprocessor.apply(image_path)
```

Αν θέλετε να προβάλετε το αποτέλεσμα, μπορείτε να το αποθηκεύσετε στο δίσκο:

```python
# Optional: save the preprocessed image for visual verification
processed_image.save("preprocessed_cyrillic.jpg")
print("Preprocessed image saved – check the file to confirm deskewing and binarization.")
```

> **Γιατί η προεπισκόπηση;** Η θέαση της μετασχηματισμένης εικόνας σας βοηθά να ρυθμίσετε τα όρια. Μερικές φορές ένα όριο 180 είναι πολύ σκληρό· μειώνοντάς το στα 150 μπορεί να διατηρήσει αχνές γραμμές.

---

## Βήμα 4: Ρύθμιση Μηχανής OCR και Αναγνώριση Κειμένου

Τώρα περνάμε στο πραγματικό μέρος του OCR. Θα ρυθμίσουμε τη μηχανή ώστε να χρησιμοποιεί το πακέτο γλώσσας κυριλλικών, κάτι ουσιώδους σημασίας για **εξαγωγή κειμένου από κυριλλική εικόνα**.

```python
# Initialise the OCR engine
engine = OcrEngine()

# Tell the engine we’re working with Cyrillic text
engine.setLanguage(Language.Cyrillic)

# Perform recognition on the preprocessed image
ocr_result = engine.recognizeImage(processed_image)

# Extract plain text from the OCR result object
recognized_text = ocr_result.getText()
print("=== Recognized Text ===")
print(recognized_text)
```

### Πώς Αυτό Βελτιώνει την Ακρίβεια του OCR

- Τροφοδοτώντας μια **καθαρή, deskewed, binarized** εικόνα, η μηχανή μπορεί να εστιάσει στα σχήματα των χαρακτήρων αντί να παλεύει με θόρυβο.  
- Η επιλογή `Language.Cyrillic` ενεργοποιεί το σωστό σύνολο χαρακτήρων και το μοντέλο γλώσσας, που αποτελεί βασικό παράγοντα **πώς να βελτιώσετε την ακρίβεια του OCR** για μη‑λατινικά αλφάβητα.

---

## Βήμα 5: Συσκευασία Όλων σε Επαναχρησιμοποιήσιμη Συνάρτηση (Προαιρετικό)

Αν σκοπεύετε να επεξεργαστείτε πολλά αρχεία, η περιτύλιξη της λογικής σε συνάρτηση καθιστά τον κώδικά σας πιο καθαρό και εύκολο στη συντήρηση.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Preprocess an image and extract Cyrillic text using the OCR engine.

    Parameters
    ----------
    image_path : str
        Full path to the source image.

    Returns
    -------
    str
        Recognized Cyrillic text.
    """
    # Build the preprocessing pipeline (could be cached for performance)
    preprocessor = (ImagePreprocessor()
                    .deskew()
                    .binarize(threshold=180)
                    .removeNoise(strength=2))

    processed = preprocessor.apply(image_path)

    engine = OcrEngine()
    engine.setLanguage(Language.Cyrillic)

    result = engine.recognizeImage(processed)
    return result.getText()


# Example usage
if __name__ == "__main__":
    sample_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")
    text = extract_cyrillic_text(sample_path)
    print("Extracted Cyrillic text:")
    print(text)
```

> **Γιατί συνάρτηση;** Απομονώνει τη λογική προεπεξεργασίας, καθιστώντας απλό το να αλλάξετε γλώσσα ή παραμέτρους χωρίς να ξαναγράψετε ολόκληρο το script.

---

## Συνηθισμένα Παράπλοκα και Πώς να Τα Αντιμετωπίσετε

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| **Έντονη κλίση (>15°)** | Το κείμενο εμφανίζεται ακατάληπτο ή λείπει | Αυξήστε την ανθεκτικότητα του `deskew()` ή προ‑περιστρέψτε χειροκίνητα χρησιμοποιώντας το `getRotationMatrix2D` του OpenCV. |
| **Χαμηλή αντίθεση** | Η binarization κάνει τα πάντα λευκά | Μειώστε την τιμή `threshold` ή εφαρμόστε βήμα stretching αντίθεσης πριν το `binarize()`. |
| **Μικρό μέγεθος γραμματοσειράς** | Οι χαρακτήρες συγχωνεύονται μετά το binarize | Χρησιμοποιήστε εικόνα υψηλότερης ανάλυσης ή εφαρμόστε ήπιο Gaussian blur πριν το thresholding. |
| **Πολλαπλές γλώσσες** | Τα κυριλλικά γράμματα γίνονται ακατανόητα | Ορίστε `engine.setLanguage([Language.Cyrillic, Language.English])` αν η βιβλιοθήκη υποστηρίζει multi‑language mode. |
| **Μη υποστηριζόμενη μορφή εικόνας** | Η `apply()` πετάει σφάλμα | Μετατρέψτε την εικόνα σε PNG ή JPEG εκ των προτέρων χρησιμοποιώντας Pillow (`Image.open().convert('RGB')`). |

---

## Επέκταση της Προσέγγισης **Image Preprocessing Pipeline Python**

1. **Batch Processing** – Επανάληψη πάνω σε φάκελο εικόνων, αποθήκευση κάθε αποτελέσματος σε αρχείο CSV.  
2. **Parallel Execution** – Χρήση `concurrent.futures.ThreadPoolExecutor` για επιτάχυνση μεγάλων φορτίων.  
3. **Custom Filters** – Προσθήκη μορφολογικών λειτουργιών (`erode`, `dilate`) για έντυπες φόρμες.  
4. **Cloud OCR Integration** – Αντικατάσταση του `OcrEngine` με client API (Google Vision, Azure Computer Vision) διατηρώντας τα ίδια βήματα προεπεξεργασίας.

```python
# Example of batch processing with ThreadPoolExecutor
from concurrent.futures import ThreadPoolExecutor, as_completed

def batch_extract(folder: str):
    files = [os.path.join(folder, f) for f in os.listdir(folder) if f.lower().endswith('.jpg')]
    results = {}

    with ThreadPoolExecutor(max_workers=4) as executor:
        future_to_file = {executor.submit(extract_cyrillic_text, f): f for f in files}
        for future in as_completed(future_to_file):
            file_path = future_to_file[future]
            try:
                results[file_path] = future.result()
            except Exception as exc:
                results[file_path] = f"Error: {exc}"
    return results
```

---

## Οπτική Σύνοψη

![παράδειγμα προεπεξεργασίας εικόνας για OCR](/images/ocr_preprocess_example.png "Διάγραμμα που δείχνει τη διαδικασία προεπεξεργασίας εικόνας για OCR: deskew → binarize → denoise → OCR engine")

*Το διάγραμμα απεικονίζει κάθε στάδιο της ροής **preprocess image for OCR**, από την ακατέργαστη σάρωση μέχρι την τελική εξαγωγή κειμένου.*

---

## Συμπέρασμα

Διασχίσαμε μια πλήρη λύση **preprocess image for OCR** σε Python, καλύπτοντας τα πάντα από την εγκατάσταση των σωστών πακέτων μέχρι την κατασκευή ενός ανθεκτικού **image preprocessing pipeline python** και τελικά την **εξαγωγή κειμένου από κυριλλική εικόνα**. Εφαρμόζοντας deskewing, binarization και denoising πριν τροφοδοτήσετε την εικόνα στη μηχανή OCR, θα παρατηρήσετε σημαντική βελτίωση στην **πώς να βελτιώσετε την ακρίβεια του OCR**, ειδικά για απαιτητικά κυριλλικά σενάρια.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αλλάξετε το μοντέλο γλώσσας σε Αραβικά, πειραματιστείτε με adaptive thresholding, ή συνδέστε το pipeline με ένα Flask API για επεξεργασία εγγράφων σε πραγματικό χρόνο. Ο ουρανός είναι το όριο, και με αυτή τη βάση είστε καλά εξοπλισμένοι για να μετατρέψετε ακατάστατες σαρές σε καθαρό, αναζητήσιμο κείμενο.

Καλή κωδικοποίηση, και εύχομαι τα OCR αποτελέσματά σας να είναι πάντα κρυστάλλινα καθαρά!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}