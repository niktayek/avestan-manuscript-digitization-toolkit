# Avestan Manuscript Digitization Toolkit

**Jupyter notebooks and resources for OCR model training and manuscript processing**

**Status**: Supporting materials for Master's thesis research  
**Related work**: [Avestan Text Processing Suite](https://github.com/niktayek/Avestan-Text-Processing-Suite) (thesis repository)  
**OCR Model**: Published on [Hugging Face](https://huggingface.co/Nikyek/avestan-ocr-kraken-v1)

---

## Overview

This toolkit provides Jupyter notebooks and Google Colab resources designed to make Avestan OCR model training accessible to researchers without extensive command-line expertise. These materials were developed during master's thesis research at Freie Universität Berlin in collaboration with the Corpus Avesticum Berolinense (CAB) project.

The notebooks guide users through:
- Setting up eScriptorium for manuscript image segmentation
- Training Kraken OCR models on annotated ground truth
- Applying trained models to new manuscripts
- Converting OCR output to standard TEI and CAB XML formats

All workflows use the same models and methods as documented in the main thesis repository.

---

## Who Should Use This

- **Manuscript digitization projects** needing OCR for historical scripts
- **Researchers** without local GPU/computational infrastructure (Colab-based workflows)
- **Digital humanities practitioners** working on low-resource language OCR
- **CAB collaborators** processing Avestan manuscript collections
- **Colleagues** at partner institutions seeking to replicate or adapt the workflow

---

## Contents

### Colab Notebooks

All notebooks run in Google Colab with free GPU access. No local installation required.

#### Setup & Configuration
- `Colab_INSTRUCTIONS.md` — Quick start guide for first-time Colab users
- `Kraken_OCR_SetupWizard.ipynb` — Interactive environment and dependency check

#### OCR Model Training
- `Kraken_ALTO_OCR_Colab_PROJECTS_TRAINER.ipynb` — Full training workflow (recommended)
- `Kraken_ALTO_OCR_Colab.ipynb` — Standard training pipeline
- `Kraken_ALTO_OCR_Colab_AUTO.ipynb` — Automated project discovery from eScriptorium
- `Kraken_ALTO_OCR_Colab_CHAINED.ipynb` — Sequential training for multiple manuscripts

#### Model Application & Conversion
- `Kraken_ALTO_Colab_v5.ipynb` — Apply trained models to new images
- `xml_translator_colab.ipynb` — Convert ALTO XML to CAB XML format
- `xml_translator_colab_canonical.ipynb` — Canonical text processing variant
- `mirror_images_colab.ipynb` — Image preprocessing (mirroring for RTL scripts)

#### Analysis & Visualization
- `Yasna_filled_changes_to_network.ipynb` — Manuscript relationship visualization (multiple variants)
- `Yasna_Scribal_Features_Jaccard.ipynb` — Orthographic feature analysis
- `eScriptorium_API_colab.ipynb` — Direct API integration examples

### Data & Configuration

- `colab_ocr_package/` — Self-contained package with:
  - Pre-trained Avestan OCR model
  - Sample manuscript images
  - Training configuration templates
  - Test datasets

---

## Installation & Usage

### Option 1: Google Colab (Recommended - No Installation)

1. Click any `.ipynb` notebook link above
2. Open in Google Colab (top of notebook or `File → Open in Colab`)
3. Authenticate with Google Drive (required for data access)
4. Run cells in order

**First-time setup:**
- See `Colab_INSTRUCTIONS.md` for credential configuration
- Colab provides free GPU (K80/T4) with 12 GB memory

### Option 2: Local Installation

Clone this repository and run notebooks locally:

```bash
# Clone
git clone https://github.com/niktayek/avestan-manuscript-digitization-toolkit.git
cd avestan-manuscript-digitization-toolkit

# Install dependencies
pip install jupyter notebook tensorflow torch kraken pillow lxml pyyaml

# Run Jupyter
jupyter notebook
```

Requires:
- Python 3.8+
- GPU recommended (CUDA 11.0+ for faster training)
- 8+ GB RAM

---

## Workflow Overview

```
1. Prepare manuscript images
   └─ mirror_images_colab.ipynb (if needed for RTL scripts)

2. Import & segment in eScriptorium
   └─ eScriptorium_API_colab.ipynb

3. Annotate ground truth manually (in eScriptorium GUI)
   └─ ~40-50 pages minimum for good model

4. Export training data from eScriptorium
   └─ (via eScriptorium web interface)

5. Train OCR model
   └─ Kraken_ALTO_OCR_Colab_PROJECTS_TRAINER.ipynb

6. Apply model to new manuscripts
   └─ Kraken_ALTO_Colab_v5.ipynb

7. Convert output to standard formats
   └─ xml_translator_colab.ipynb (ALTO → CAB XML)

8. Analysis & validation (optional)
   └─ Yasna_Scribal_Features_Jaccard.ipynb
```

---

## Key Features

- **No GPU setup required** — Use free Colab GPUs
- **eScriptorium integration** — Connect directly to your manuscript project
- **Batch processing** — Train/apply to multiple manuscripts efficiently
- **Standard output formats** — ALTO XML, CAB XML, TEI
- **Reproducible workflows** — Same notebooks work across different manuscripts
- **Well-documented** — Inline comments and methodology explanations

---

## Model Training Parameters

All notebooks use configuration suitable for historical script OCR with limited ground truth:

| Parameter | Value | Rationale |
|-----------|-------|-----------|
| Batch size | 16 | Colab memory constraints |
| Learning rate | 0.001 | Transfer learning from Hebrew model |
| Epochs | 30-50 | Early stopping on validation loss |
| Ground truth lines | 40-100 | Low-resource language setting |
| Transfer learning | Yes | Hebrew Avestan model as base |

See `colab_ocr_package/training_config/` for detailed hyperparameter templates.

---

## Expected Accuracy

On historical Avestan manuscripts with proper ground truth annotation:

| Metric | Typical Range |
|--------|---------------|
| Character accuracy | 95-99% |
| Word accuracy | 90-97% |
| Training time (Colab) | 2-4 hours |

Validation performed on Yasna 9 (14 witnesses) achieved 99.2% character accuracy. See main thesis repository for methodology.

---

## Troubleshooting

### Colab Authentication Issues
- Notebooks may request Google Drive access on first run
- Grant permission to allow file uploads/downloads
- See `Colab_INSTRUCTIONS.md` for details

### eScriptorium Connection Errors
- Verify eScriptorium instance URL is correct
- Check API credentials in notebook configuration
- Ensure network connectivity to eScriptorium server

### Out of Memory Errors
- Reduce batch size (change `BATCH_SIZE = 16` to `8`)
- Process fewer images per training run
- Use local GPU with more VRAM if available

### Low OCR Accuracy
- Ensure ground truth has at least 40-50 annotated lines
- Check image quality (contrast, resolution)
- Verify annotation accuracy in eScriptorium
- Try longer training (increase epochs)

See individual notebooks for detailed troubleshooting sections.

---

## Citation

If using these materials in research, cite the main thesis repository and this toolkit:

Yekrang Safakar, N. (2025). *Integrating OCR and Automated Apparatus Construction for Avestan Texts*. Master's thesis, Freie Universität Berlin. https://github.com/niktayek/Avestan-Text-Processing-Suite

For this toolkit specifically:

Yekrang Safakar, N. (2025). Avestan Manuscript Digitization Toolkit. Supporting materials for Master's thesis. https://github.com/niktayek/avestan-manuscript-digitization-toolkit

---

## Related Repositories

- **[Avestan Text Processing Suite](https://github.com/niktayek/Avestan-Text-Processing-Suite)** — Master's thesis with OCR and critical apparatus pipelines
- **[avestan-computational-philology](https://github.com/niktayek/avestan-computational-philology)** — Experimental textual analysis tools (leitfehler, scribal schools)
- **[avestan-ocr-kraken-v1](https://huggingface.co/Nikyek/avestan-ocr-kraken-v1)** — Published model on Hugging Face

---

## Resources & Documentation

- **[Kraken OCR documentation](https://kraken.re/)** — Training and inference guide
- **[eScriptorium documentation](https://escriptorium.readthedocs.io/)** — Manuscript segmentation and annotation
- **[TEI Guidelines](https://tei-c.org/)** — Text encoding standards
- **[CAB project](https://www.avesta.uni-frankfurt.de/)** — Corpus Avesticum Berolinense

---

## Contributing

Issues, questions, and suggestions are welcome. Please open a GitHub issue with:
- Notebook name and cell number where issue occurred
- Error message or description
- Your manuscript/language context
- Steps to reproduce

---

## License

These Jupyter notebooks and supporting materials are provided under the MIT License. See LICENSE file for details.

The underlying methodologies are described in the Master's thesis (2025) and are available for academic and research use.

---

## Questions & Contact

- **Issues**: GitHub Issues
- **Questions about notebooks**: Check notebook comments and troubleshooting sections
- **Methodology questions**: See main thesis repository for research details
- **Contact**: niktaayekrang@gmail.com

---

**Last updated**: February 2026  
**Maintained by**: Nikta Yekrang Safakar  
**Status**: Supporting materials for published thesis research
