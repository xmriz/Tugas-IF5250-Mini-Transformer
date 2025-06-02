# Mini Transformer for Dialogue Generation

Notebook ini mengimplementasikan model **Transformer Seq2Seq** (encoder–decoder) untuk tugas *dialogue generation* menggunakan dataset percakapan sederhana (*simple dialogs*).

## 1. Deskripsi Proyek

Proyek ini membangun dan melatih model Transformer Seq2Seq dari awal (**tanpa pretrained weights**) untuk menghasilkan respons dialog yang alami berdasarkan input pertanyaan. Model diujikan pada dataset *pasangan tanya–jawab* berformat tab-delimited (`dialogs.txt`).

Fitur utama:

* Training **from scratch** (seluruh parameter diinisialisasi acak)
* Eksperimen dengan 4 varian arsitektur (dengan/ tanpa relative positional bias, ukuran kecil/besar)
* Evaluasi otomatis menggunakan metrik standar generasi teks

## 2. Variants

Empat varian model yang diuji:

* **vanilla\_small**: model kecil, tanpa relative positional bias
* **vanilla\_big**: model besar, tanpa relative positional bias
* **relpos\_small**: model kecil, *dengan* relative positional bias
* **relpos\_big**: model besar, *dengan* relative positional bias

Perbedaan utama: jumlah parameter, ukuran dimensi, serta penggunaan *relative position bias* pada attention.

## 3. Dataset

Dataset yang digunakan adalah *Simple Dialogs for Chatbot* (Kaggle):

* Link: [https://www.kaggle.com/datasets/grafstor/simple-dialogs-for-chatbot](https://www.kaggle.com/datasets/grafstor/simple-dialogs-for-chatbot)

Format file `dialogs.txt`:
Setiap baris berisi satu pasangan `<pertanyaan> \t <jawaban>`, contoh:

```
hi, how are you doing?    i'm fine. how about yourself?
i'm fine. how about yourself?    i'm pretty good. thanks for asking.
...
```

**Statistik Dataset:**

| Split | # Dialogues | Max Turns/Dialog | Avg Tokens/Turn |
| ----- | ----------- | ---------------- | --------------- |
| Train | \~3,500     | 1                | \~8–12          |
| Test  | \~200       | 1                | \~8–12          |

* Total dialogs: **3725**
* Subset train/test dipilih sesuai kebutuhan eksperimen

## 4. Struktur Direktori

```
.
├── dialogs.txt         # Dataset: simple dialogs (tab-delimited)
├── notebook.ipynb      # Notebook eksperimen (end-to-end)
├── requirements.txt    # Daftar dependensi Python
├── checkpoints/        # Folder hasil checkpoint model (*.pt)
└── ... (file terkait lainnya)
```

## 5. Instalasi & Eksekusi

1. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

2. **Jalankan seluruh cell di `notebook.ipynb`** untuk:

   * Exploratory Data Analysis (EDA)
   * Preprocessing data & pembuatan vocab
   * Training model, validasi, dan penyimpanan checkpoint
   * Inference dan evaluasi otomatis

## 6. Evaluasi

Model dievaluasi pada test set menggunakan metrik:

* **ROUGE** (rouge-1, rouge-2, rouge-L, rouge-Lsum)
* **BLEU**
* **METEOR**

Metrik ini mengukur kemiripan respons model dengan jawaban referensi (semakin tinggi = semakin mirip).

## 7. Catatan Penting

* Model di-*train* dari nol, **tanpa pretrained weights**.
* Sequence input/output dibatasi hingga `MAX_SEQ_LEN=64` token.
* Notebook otomatis menampilkan *loss curves*, perbandingan model, skor metrik, serta contoh hasil prediksi.
* Checkpoint model terbaik otomatis disimpan ke folder `checkpoints/`.

---

**Referensi utama:**

* Vaswani et al., "Attention Is All You Need" (2017)
* [Kaggle: Simple Dialogs for Chatbot](https://www.kaggle.com/datasets/grafstor/simple-dialogs-for-chatbot)

---

**Contoh isi file `dialogs.txt`:**

```
hi, how are you doing?    i'm fine. how about yourself?
i'm fine. how about yourself?    i'm pretty good. thanks for asking.
...
```

---

**Total dialogs: 3725**
