# 📄 GROBID PDF Section Extractor

This project automates the extraction of structured metadata and section outlines from PDF documents using [GROBID](https://github.com/kermitt2/grobid), and maps section headings to their corresponding page numbers using Python.

---

## 🚀 Features

- Full-text PDF processing using GROBID
- Extraction of document title and section headings (H1, H2)
- Mapping of each section heading to its first appearance in the PDF (by page)
- Generation of a clean and structured JSON output

---

## 🛠️ Setup Instructions

### 1. Clone and Build GROBID

```bash
git clone https://github.com/kermitt2/grobid.git
cd grobid
./gradlew clean install
