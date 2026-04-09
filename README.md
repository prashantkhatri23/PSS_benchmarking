# Tobacco800 & TABME — Redacted Datasets for Page Stream Segmentation

This repository accompanies our conference paper on Page Stream Segmentation (PSS). It provides redacted versions of the Tobacco800 and TABME++ document collections, with document-level archival artifacts removed from both image and OCR layers to enable rigorous, leakage-free benchmarking.

---

## Motivation

We identify and redact document-level artifacts present in the original Tobacco800 and TABME++ collections. These identifiers (e.g., Bates stamps and proprietary tracking IDs) are not part of the original document content but were added for archival purposes.

In the context of PSS, these IDs introduce significant data leakage: because they increment sequentially (*n*+1), a model can trivially identify segment boundaries by tracking numerical continuity rather than understanding document semantics. To ensure a rigorous benchmark, we provide versions of these datasets where such marginalia have been masked in both the image and OCR layers.

---

## Repository Structure

```
data/
└── tabme/
    └── tabme_artifact_removal.ipynb   # Artifact removal pipeline for TABME
```

---

## Tobacco800 (Redacted)

The redacted Tobacco800 dataset is available via Zenodo: **[TODO: add Zenodo link]**

The dataset contains **1,290 pages** — one fewer than the original dataset. We observed that one file was a duplicate: `wfg55f00` is a copy of `wfg55f00_1`, so we retained only one.

The Zenodo deposit includes the redacted images alongside `tobacco800_test_redacted.pdf`, a combined PDF of the test page stream assembled from the individual redacted images. The procedure is described in detail in the paper. The train stream is not fixed — users can construct it from the remaining images as needed.

### OCR Format

```json
{
  "bb": {
    "<ID>": ["xmin (int)", "ymin (int)", "xmax (int)", "ymax (int)"]
  },
  "tokens": {
    "<ID>": "OCR-recognized text or line (string)"
  },
  "scores": {
    "<ID>": "confidence score, 0.0–1.0 (float)"
  }
}
```

### References

```bibtex
@inproceedings{Zhu-CVPR07,
  AUTHOR    = {Guangyu Zhu and Yefeng Zheng and David Doermann and Stefan Jaeger},
  TITLE     = {Multi-scale Structural Saliency for Signature Detection},
  BOOKTITLE = {In Proc. IEEE Conf. Computer Vision and Pattern Recognition (CVPR 2007)},
  PAGES     = {1--8},
  YEAR      = {2007},
}

@inproceedings{Zhu-ICDAR07,
  AUTHOR    = {Guangyu Zhu and David Doermann},
  TITLE     = {Automatic Document Logo Detection},
  BOOKTITLE = {In Proc. 9th International Conf. Document Analysis and Recognition (ICDAR 2007)},
  PAGES     = {864--868},
  YEAR      = {2007},
}
```

---

## TABME Dataset

Due to the large scale of the TABME dataset, we do not provide preprocessed (artifact-removed) images. Manual redaction of document-level artifacts is not practical at this scale.

Instead, we provide a Jupyter notebook (`data/tabme/tabme_artifact_removal.ipynb`) that demonstrates our artifact removal pipeline and includes code for automatically masking such artifacts using OCR bounding boxes. Users can adapt this code to apply it to the full dataset.

The proposed method achieves an **F1 score of 0.98**, evaluated on a sample of 100 pages from the test set.

**Original source:** https://github.com/aldolipani/TABME

**TABME++ (improved OCR):** https://huggingface.co/datasets/rootsautomation/TABMEpp

### References

```bibtex
@inproceedings{mungmeeprued-etal-2022-tab-this,
  title     = {Tab this Folder of Documents: Page Stream Segmentation of Business Documents},
  author    = {Thisanaporn Mungmeeprued and Yuxin Ma and Nisarg Mehta and Aldo Lipani},
  year      = {2022},
  booktitle = {Proceedings of the ACM Symposium on Document Engineering},
  publisher = {ACM},
  address   = {San Jose, CA, USA},
  series    = {DocEng '22},
}

@misc{heidenreich2024largelanguagemodelspage,
  title         = {Large Language Models for Page Stream Segmentation},
  author        = {Hunter Heidenreich and Ratish Dalvi and Rohith Mukku and Nikhil Verma and Neven Pi\v{c}uljan},
  year          = {2024},
  eprint        = {2408.11981},
  archivePrefix = {arXiv},
  primaryClass  = {cs.CL},
  url           = {https://arxiv.org/abs/2408.11981},
}
```
