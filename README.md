---
language:
  - id
tags:
  - instruction-tuning
  - indonesia
  - qa
  - factual
size_categories:
  - 1K<n<10K
license: mit
---

# Fakta Menarik Tentang Indonesia - Instruction Tuning Dataset

Dataset pasangan tanya-jawab (instruction / output) dalam Bahasa Indonesia natural,
dikumpulkan dari hasil scraping puluhan situs web (Wikipedia ID & EN, portal pemerintah,
situs fakta internasional) menggunakan browser headless Obscura, lalu diekstrak dan
digerakan menjadi format instruction-tuning.

## Format

```json
{
  "instruction": "pertanyaan dalam Bahasa Indonesia",
  "output": "jawaban dalam Bahasa Indonesia"
}
```

Setiap baris pada `pairs` juga menyertakan metadata `category`, `source`, dan `source_url`
untuk pelacakan asal fakta.

## Statistik

- Total pasangan: 5.870
- Bahasa: Indonesia (id)
- Kategori (jumlah pasangan):
  - sejarah: 1.666
  - demografi: 964
  - lingkungan: 754
  - satwa: 608
  - ekonomi: 548
  - umum: 534
  - budaya: 480
  - geografi: 316

## File

- `indonesia_qa_all.json` — seluruh 5.870 pasangan dalam satu file.

## Catatan

Fakta diekstrak verbatim dari sumber dan diolah menjadi pertanyaan Bahasa Indonesia
yang natural (bukan terjemahan mesin kaku). Periksa keakuratan sebelum digunakan untuk
training.
# pbl-analisis-sentimen-rs-batam
