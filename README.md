# 📄 GROBID PDF Section Extractor

**Hackathon Project: Automated PDF Outline Generation with Page Mapping**

This project leverages [GROBID](https://github.com/kermitt2/grobid) to extract structured metadata and section outlines from PDF documents, automatically mapping section headings to their corresponding page numbers for enhanced document navigation.

---

## 🚀 Features

- **Full-text PDF Processing**: Uses GROBID's machine learning models for accurate document structure extraction
- **Hierarchical Section Detection**: Identifies H1 and H2 level headings with proper nesting
- **Page Number Mapping**: Automatically finds the first page where each section heading appears
- **Structured JSON Output**: Clean, machine-readable format for further processing
- **TEI XML Parsing**: Processes GROBID's Text Encoding Initiative XML output
- **Error Handling**: Robust processing with fallback mechanisms

---

## 🏗️ Project Structure

```
grobid-pdf-extractor/
├── README.md
├── requirements.txt
├── main.py
├── input/
│   └── sample.pdf
├── output/
│   └── challenge1b_output.json
└── grobid/
    └── (GROBID installation)
```

---

## 🛠️ Setup Instructions

### Prerequisites
- Python 3.7+
- Java 8+ (for GROBID)
- Git

### 1. Clone and Setup the Project
```bash
git clone <your-repo-url>
cd grobid-pdf-extractor
```

### 2. Install Python Dependencies
```bash
pip install -r requirements.txt
```

### 3. Clone and Build GROBID
```bash
git clone https://github.com/kermitt2/grobid.git
cd grobid
./gradlew clean install
cd ..
```

### 4. Prepare Input Directory
```bash
mkdir -p input output
# Place your PDF file as input/sample.pdf
```

---

## 🚀 Usage

### 1. Start GROBID Server
```bash
cd grobid
./gradlew run
```
Wait for the server to become accessible at `http://localhost:8070/api/isalive`

### 2. Run the Extraction Script
```bash
python main.py
```

### 3. Check Output
The structured outline will be saved as `output/challenge1b_output.json`

---

## 📋 How It Works

### Step 1: PDF Processing with GROBID
- Sends PDF to GROBID's `/api/processFulltextDocument` endpoint
- Receives structured TEI XML containing document metadata and sections

### Step 2: TEI XML Parsing
- Extracts document title from `<titleStmt><title>` elements
- Identifies section headings from `<div><head>` elements
- Maintains hierarchical structure (H1, H2 levels)

### Step 3: Page Number Mapping
- Uses PyMuPDF (fitz) to open the original PDF
- Searches for each extracted heading text within PDF pages
- Records the first page number where each heading appears

### Step 4: JSON Generation
- Combines title and outline with page numbers
- Outputs structured JSON for easy consumption

---

## 📊 Output Format

```json
{
  "title": "Document Title",
  "outline": [
    {
      "level": "H1",
      "text": "Chapter 1: Introduction",
      "page": 3
    },
    {
      "level": "H2",
      "text": "1.1 Background",
      "page": 4
    },
    {
      "level": "H1",
      "text": "Chapter 2: Methodology",
      "page": 8
    }
  ]
}
```

---

## 🔧 Configuration

### GROBID Server Settings
- **Host**: `localhost`
- **Port**: `8070`
- **Endpoint**: `/api/processFulltextDocument`

### File Paths
- **Input PDF**: `input/sample.pdf`
- **Output JSON**: `output/challenge1b_output.json`

---

## 📦 Dependencies

```
requests>=2.25.1
PyMuPDF>=1.18.0
```

---

## 🐛 Troubleshooting

### GROBID Server Issues
```bash
# Check if server is running
curl http://localhost:8070/api/isalive

# If port is busy, kill existing processes
lsof -ti:8070 | xargs kill -9
```

### Common Problems

**1. Server Not Starting**
- Ensure Java 8+ is installed
- Check if port 8070 is available
- Verify GROBID built successfully

**2. PDF Processing Fails**
- Confirm PDF file exists at `input/sample.pdf`
- Check PDF is not corrupted or password-protected
- Verify file permissions

**3. Page Mapping Issues**
- Some headings might not be found due to text encoding differences
- OCR quality affects text matching accuracy
- Consider fuzzy string matching for better results

---

## 🙏 Acknowledgments

- [GROBID Team](https://github.com/kermitt2/grobid) for the excellent PDF processing framework
- [PyMuPDF](https://github.com/pymupdf/PyMuPDF) for reliable PDF text extraction
- Hackathon organizers for the inspiring challenge

---

## 📞 Contact

**Project Team**: [The Destroyer]  
**Email**: [2023kuec2058@iiitkota.ac.in]  


---
