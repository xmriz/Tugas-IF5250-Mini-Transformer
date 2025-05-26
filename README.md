# Decoder-Only Transformer for Dialogue Generation

## Deskripsi Proyek

Implementasi dari model Transformer *decoder-only* sederhana untuk tugas *multi-turn dialogue generation*. Proyek ini bertujuan untuk memahami dan membangun komponen dasar Transformer dari awal (*from scratch*) tanpa menggunakan library tinggi seperti Huggingface Transformers atau PyTorch Lightning.

Komponen inti yang diimplementasikan:

* Token & Positional Embedding
* Multi-Head Self-Attention (dengan varian *relative positional bias*)
* Feed-Forward Network
* Layer Normalization
* Residual Connection

## Variants

Empat varian model digunakan dalam eksperimen ini:

* `vanilla_small`: Positional encoding absolut, dimensi kecil
* `vanilla_big`: Positional encoding absolut, dimensi besar
* `relpos_small`: Menggunakan *MultiHeadSelfAttentionRelPos*, dimensi kecil
* `relpos_big`: Menggunakan *MultiHeadSelfAttentionRelPos*, dimensi besar

Varian `relpos_*` menggunakan attention dengan *relative positional bias* untuk menangani perbedaan posisi token secara lebih fleksibel. Bias ini diimplementasikan dalam kelas `MultiHeadSelfAttentionRelPos` dengan indeks posisi relatif dan parameter bias learnable per head.

## Dataset

**DailyDialog** dari Huggingface Datasets

* Link: [https://huggingface.co/datasets/li2017dailydialog/daily\_dialog](https://huggingface.co/datasets/li2017dailydialog/daily_dialog)
* Dialog sehari-hari yang ditulis manusia dan disertai label intent (dialogue act) dan emosi.

### Statistik Dataset

| Split      | #Dialogues | Avg Turns/Dialog | Avg Tokens/Turn |
| ---------- | ---------- | ---------------- | --------------- |
| Train      | 11,118     | 7.84             | \~15            |
| Validation | 1,000      | 8.07             | \~15            |
| Test       | 1,000      | 7.74             | \~15            |

## Struktur Direktori

```
.
├── requirements.txt
├── notebook.ipynb            # Main implementation in notebook
```

## Instalasi & Eksekusi

1. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

2. Jalankan seluruh cell pada `notebook.ipynb` untuk memulai pelatihan dan evaluasi model.

## Evaluasi

Model dievaluasi dengan metrik:

* ROUGE (rouge1, rouge2, rougeL, rougeLsum)
* BLEU
* METEOR

Metrik ini menghitung kedekatan antara respons model dan respons referensi dalam dialog test set.

## Catatan Tambahan

* Notebook menggunakan subset data dengan maksimal 8 turn per dialog.
* Ukuran token maksimal (`MAX_SEQ_LEN`) diatur ke 64.
* Implementasi tidak menggunakan model pretrained, seluruh parameter diinisialisasi dari nol.

---

