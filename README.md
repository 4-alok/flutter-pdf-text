# PDF Text Plugin

[![Pub Version](https://img.shields.io/pub/v/pdf_text)](https://pub.dev/packages/pdf_text)
[![GitHub issues](https://img.shields.io/github/issues/AlessioLuciani/flutter-pdf-text)](https://github.com/AlessioLuciani/flutter-pdf-text/issues)
[![GitHub forks](https://img.shields.io/github/forks/AlessioLuciani/flutter-pdf-text)](https://github.com/AlessioLuciani/flutter-pdf-text/network)
[![GitHub stars](https://img.shields.io/github/stars/AlessioLuciani/flutter-pdf-text)](https://github.com/AlessioLuciani/flutter-pdf-text/stargazers)
[![GitHub license](https://img.shields.io/github/license/AlessioLuciani/flutter-pdf-text)](https://github.com/AlessioLuciani/flutter-pdf-text/blob/master/LICENSE)

This plugin for [Flutter](https://flutter.dev) allows you to read the text content of PDF documents and convert it into strings. It works on iOS and Android. On iOS it uses Apple's [PDFKit](https://developer.apple.com/documentation/pdfkit). On Android it uses Apache's [PdfBox](https://github.com/TomRoush/PdfBox-Android) Android porting.

<p align="center">
  <img src="https://raw.githubusercontent.com/AlessioLuciani/flutter-pdf-text/master/example/flutter-pdf-text.gif" alt="Demo Example App" style="margin:auto"  width="250"  height="550">
</p>

## Getting Started

Add this to your package's `pubspec.yaml` file:

```yaml
dependencies:
  pdf_text: ^0.1.2
```

## Usage

Import the package with:

```dart
import 'package:pdf_text/pdf_text.dart';
```

Create a PDF document instance using a File object:

```dart
PDFDoc doc = await PDFDoc.fromFile(file);
```

or using a path string:

```dart
PDFDoc doc = await PDFDoc.fromPath(path);
```

Read the text of the entire document:

```dart
String docText = await doc.text;
```

Retrieve the number of pages of the document:

```dart
int numPages = doc.length;
```

Access a page of the document:

```dart
PDFPage page = doc.pageAt(pageNumber);
```

Read the text of a page of the document:

```dart
String pageText = await page.text;
```

## Functioning

This plugin applies lazy loading for the text contents of the pages. The text is cached page per page. When you request the text of a page for the first time, it is parsed and stored in memory, so that the second access will be faster. Anyway, the text of pages that are not requested is not loaded. This mechanism
allows you not to waste time loading text that you will probably not use. When you request the text content of the entire document, only the pages that have not been loaded yet are then loaded.

## Public Methods
  
### PDFDoc

| Return  | Description  |

| PDFPage | **pageAt(int pageNumber)** <br> Gets the page of the document at the given page number. |

| static Future\<PDFDoc> | **fromFile(File file)** <br> Creates a PDFDoc object with a File instance. |

| static Future\<PDFDoc> | **fromPath(String path)** <br> Creates a PDFDoc object with a file path. |

## Objects

```dart
class PDFDoc {
  int length; // Number of pages of the document
  List<PDFPage> pages; // Pages of the document
  Future<String> text; // Text of the document
}

class PDFPage {
  int number; // Number of the page in the document
  Future<String> text; // Text of the page
}
```

## Contribute

If you have any suggestions, improvements or issues, feel free to contribute to this project.
You can either submit a new issue or propose a pull request.