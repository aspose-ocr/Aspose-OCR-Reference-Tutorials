---
title: How to Set License for Aspose.OCR in Java
linktitle: How to Set License for Aspose.OCR in Java
second_title: Aspose.OCR Java API
description: 
type: docs
weight: 10
url: /java/ocr-basics/set-license/
---

## Complete Source Code
```java
package com.aspose.ocr.examples.License;

import com.aspose.ocr.License;

public class SetLicense {

	public static void main(String[] args) {
		// ExStart:1
		//Set license
		String file = "Aspose.Total.lic"; //change the path to point to a valid license
		License.setLicense(file);

		//Check license
		boolean resLicense = License.isValid();
		System.out.println("License is set: " + resLicense);
		// ExEnd:1
	}
}

```
