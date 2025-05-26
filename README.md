## Task

### Name & Description
**Decoder-Only Transformer for Dialogue Generation**  
Mengimplementasikan dan melatih model Transformer _decoder-only_ dari awal (from-scratch) untuk tugas multi-turn dialogue generation, tanpa menggunakan pustaka tinggi seperti Huggingface Transformers atau PyTorch-Lightning, sehingga komponen dasar (self-attention, multi-head attention, positional encoding, feed-forward, layer norm) dipahami secara mendalam.

---

## Dataset

### Nama & Link Asli
- **Nama**: DailyDialog  
- **Link**: https://huggingface.co/datasets/li2017dailydialog/daily_dialog

### Ringkasan Dataset
DailyDialog adalah dataset dialog multi-turn berkualitas tinggi, ditulis oleh manusia dan relatif bebas noise. Dialog mencerminkan komunikasi sehari-hari dan dilengkapi anotasi _dialogue act_ (intent) dan _emotion_ per utterance.

### Statistik
| Split       | #Dialogues | Avg Turns/Dialog | Avg Tokens/Turn |
|-------------|------------|------------------|-----------------|
| Train       | 11 118     | 7.84             | ~15             |
| Validation  | 1 000      | 8.07             | ~15             |
| Test        | 1 000      | 7.74             | ~15             |
| **Total**   | **13 118** | **7.85**         | **~15**         |

### Data Fields
- **dialog**: `list[string]` — urutan utterance lengkap, dipisah token `<sep>` dan ditandai `<bos>`/`<eos>`.  
- **act**: `list[int]` — label dialogue act:  
  - 0 = __dummy__, 1 = inform, 2 = question, 3 = directive, 4 = commissive  
- **emotion**: `list[int]` — label emotion:  
  - 0 = no emotion, 1 = anger, 2 = disgust, 3 = fear, 4 = happiness, 5 = sadness, 6 = surprise  

### Contoh Isi (cropped)
```json
{
  "act":     [2, 1, 1, 1, 1, 2, 3, 2, 3, 4],
  "dialog":  [
    "<bos> Good afternoon . This is Michelle Li speaking ... <sep>",
    "This is Mr Meng speaking . <sep>",
    "...",
    "Certainly . I will send you an update via email . <eos>"
  ],
  "emotion": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
}
