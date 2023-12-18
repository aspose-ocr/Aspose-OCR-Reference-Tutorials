---
title: Specifying Allowed Characters in Aspose.OCR
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
description: 
type: docs
weight: 15
url: /java/advanced-ocr-techniques/specify-allowed-characters/
---

## Complete Source Code
```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;

public class SpecifyAllowedCharacters {

	public static void main(String[] args) {
		// ExStart:1
		// The path to the documents directory.
		String dataDir = "Your Document Directory";

		// The image path
		String imagePath = dataDir + "0001460985.Jpeg";

		//Create api instance
		AsposeOCR api = new AsposeOCR("123456789");

		try {
			String result = api.RecognizeLine(imagePath);
			System.out.println("File: " + imagePath);
			System.out.println("Result line: " + result);
		} catch (IOException e) {
			e.printStackTrace();
		}
		// ExEnd:1
	}
}

```
