# Cleaned Tobacco800 and TABME++ Datasets for Page Stream Segmentation

This repository accompanies our conference paper on Page Stream Segmentation (PSS). We release redacted versions of the Tobacco800 and TABME++ datasets, along with OCR data and preprocessing tools, to support rigorous, leakage-free benchmarking.

---

## Motivation

Document-level artifacts — such as Bates stamps and proprietary tracking IDs — are present in both the Tobacco800 and TABME++ collections. These identifiers were added for archival purposes and are not part of the original document content. In the context of PSS, they introduce significant **data leakage**: because these IDs increment sequentially (*n+1*), a model can trivially identify segment boundaries by tracking numerical continuity rather than understanding document semantics.

To ensure a rigorous benchmark, we provide versions of these datasets where such marginalia have been masked in both the image and OCR layers.

---

## Repository Structure

```
data/
└── tabme/
    └── tabme_artifact_removal.ipynb   # Artifact removal pipeline notebook
```

---

## Tobacco800 (Redacted)

We provide fully redacted images and OCR for the Tobacco800 dataset. The data is hosted on Zenodo:

> **[Zenodo link — to be added]**

### Contents

The ZIP archive contains 1,290 pages. This is one fewer than the original dataset: we identified that `wfg55f00` is a duplicate of `wfg55f00_1`, and retained only one copy.

Each page is stored in its own folder with the following structure:

```
<document_id>/
├── image/          # Redacted page image
└── ocr/            # OCR dictionary (JSON)
```

### OCR Format

Each OCR file is a JSON dictionary with the following structure:

```json
{
  "bb": {
    "<ID>": [xmin, ymin, xmax, ymax]
  },
  "tokens": {
    "<ID>": "OCR-recognized text or line"
  },
  "scores": {
    "<ID>": 0.97
  }
}
```

| Field | Type | Description |
|---|---|---|
| `bb` | dict of int[4] | Bounding box: left, top, right, bottom |
| `tokens` | dict of str | OCR-recognized text for each region |
| `scores` | dict of float | Confidence score (0.0–1.0) |

### Original Dataset References

[1] Guangyu Zhu, Yefeng Zheng, David Doermann, and Stefan Jaeger. Multi-scale Structural Saliency for Signature Detection. In *Proc. IEEE Conf. Computer Vision and Pattern Recognition (CVPR 2007)*, pp. 1–8, 2007.

[2] Guangyu Zhu and David Doermann. Automatic Document Logo Detection. In *Proc. 9th International Conf. Document Analysis and Recognition (ICDAR 2007)*, pp. 864–868, 2007.

---

## TABME / TABME++

Due to the scale of the TABME dataset, we do not provide fully preprocessed (artifact-removed) images. Manual redaction is not practical at this scale.

Instead, we provide a Jupyter notebook that demonstrates our artifact removal pipeline and includes code for automatically masking document-level artifacts using OCR bounding boxes:

```
data/tabme/tabme_artifact_removal.ipynb
```

The method achieves an **F1 score of 0.98**, evaluated on a sample of 100 pages from the test set. Users can adapt this notebook to apply the pipeline to the full dataset.

### Dataset Sources

- **TABME (original):** [https://github.com/aldolipani/TABME](https://github.com/aldolipani/TABME)
- **TABME++ (improved OCR):** [https://huggingface.co/datasets/rootsautomation/TABMEpp](https://huggingface.co/datasets/rootsautomation/TABMEpp)

### TABME Citation

```bibtex
@inproceedings{mungmeeprued-etal-2022-tab-this,
  title     = {Tab this Folder of Documents: Page Stream Segmentation of Business Documents},
  author    = {Thisanaporn Mungmeeprued and Yuxin Ma and Nisarg Mehta and Aldo Lipani},
  year      = {2022},
  booktitle = {Proceedings of the ACM Symposium on Document Engineering},
  publisher = {ACM},
  address   = {San Jose, CA, USA},
  series    = {DocEng '22}
}

@misc{heidenreich2024largelanguagemodelspage,
  title         = {Large Language Models for Page Stream Segmentation},
  author        = {Hunter Heidenreich and Ratish Dalvi and Rohith Mukku and Nikhil Verma and Neven Pičuljan},
  year          = {2024},
  eprint        = {2408.11981},
  archivePrefix = {arXiv},
  primaryClass  = {cs.CL},
  url           = {https://arxiv.org/abs/2408.11981}
}
```

---

## Citation

The citation for this work will be available following the conclusion of the peer-review process.

```bibtex
@inproceedings{placeholder2026,
  note = {Citation information to be updated upon publication.}
}
---

## License

Please refer to the licenses of the original Tobacco800 and TABME datasets for terms of use. Our redacted versions and processing code are released for research purposes.
