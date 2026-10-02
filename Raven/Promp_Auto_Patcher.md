 Saya butuh JSON patch untuk repository lokal saya. **PENTING — ikuti aturan ketat JSON agar script Python bisa memprosesnya tanpa error.**
---

## KESALAHAN UMUM & CONTOH BENAR (WAJIB BACA)

 ### 1. **NEWLINE LITERAL DI DALAM STRING (Paling Sering)**

| ❌ SALAH (JSON invalid) | ✅ BENAR (Valid) |
|-------------------------|------------------|
| `"content": "int main() {` <br> `    printf("Hello");` <br> `    return 0;"` | `"content": "int main() {\n    printf(\"Hello\");\n    return 0;\n}"` |
| `"old_str": "/*` <br> ` * Old impl` <br> ` */"` | `"old_str": "/* Old impl */"` (satu baris) <br> atau <br> `"old_str": "/*\n * Old impl\n */"` |

**Setiap baris baru HARUS menggunakan `\n`, jangan pernah menekan Enter di dalam tanda kutip.**
 ---

 ### 2. **ESCAPE BACKSLASH (`\`) — KASUS SPESIAL**

 Di dalam string JSON, backslash `\` harus ditulis sebagai `\\`. Untuk literal backslash di kode (C path, regex), butuh **dua kali lipat**.

| ❌ SALAH           | ✅ BENAR                 | Penjelasan                                       |
| ----------------- | ----------------------- | ------------------------------------------------ |
| `"C:\Users\name"` | `"C:\\\\Users\\\\name"` | 4 backslash di JSON → 1 backslash di file C.     |
| `"/\d+/g"`        | `"/\\\\d+/g"`           | 2 backslash di JSON → 1 backslash di regex JS.   |
| `"Hello\nWorld"`  | `"Hello\\nWorld"`       | 2 backslash di JSON → 1 backslash + n di string. |
| `"C:\temp\"`      | `"C:\\\\temp\\\\"`      | Di C, path sering pakai double backslash.        |

 **Aturan praktis:** Jika di kode asli ada `\`, di JSON tulis menjadi `\\` (jika di string biasa) atau `\\\\` (jika di path/regex).

 ---

 ### 3. **QUOTE GANDA DI DALAM STRING**

| ❌ SALAH                             | ✅ BENAR                               |
| ----------------------------------- | ------------------------------------- |
| `"new_str": "printf("Hello");"`     | `"new_str": "printf(\"Hello\");"`     |
| `"old_str": "const str = "value";"` | `"old_str": "const str = \"value\";"` |

 **Quote tunggal (`'`) tidak perlu di-escape** (kecuali string delimiternya pakai `'`).

 ---

 ### 4. **TAB (`\t`) DAN KARAKTER KHUSUS LAINNYA**

| ❌ SALAH                                     | ✅ BENAR                        |
| ------------------------------------------- | ------------------------------ |
| `"content": "    print("x")"` (tab literal) | `"content": "\\tprint(\"x\")"` |
| `"content": "return 0;"` (newline di akhir) | `"content": "return 0;\\n"`    |

 **Karakter kontrol harus di-escape:** `\n` (newline), `\t` (tab), `\r` (carriage return).>
 ---

 ### 5. **SMART QUOTES (UNICODE)**

| ❌ SALAH | ✅ BENAR |
|----------|----------|
| `“content”` (U+201C/U+201D) | `"content"` (ASCII 0x22) |
| `‘old_str’` (U+2018/U+2019) | `"old_str"` (ASCII 0x27) |

 **Hanya gunakan tanda kutip lurus ASCII:** `"` untuk string, `'` tidak masalah di dalam string.

 ---

 ### 6. **TRAILING COMMA**

| ❌ SALAH | ✅ BENAR |
|----------|----------|
| `[ { ... }, { ... }, ]` | `[ { ... }, { ... } ]` |
| `{ "a": 1, "b": 2, }` | `{ "a": 1, "b": 2 }` |

 **Elemen terakhir di array/objek TIDAK boleh diikuti koma.**

 ---

 ### 7. **BACKTICK (`` ` ``) DI JAVASCRIPT — TIDAK PERLU DI-ESCAPE**

| ❌ SALAH (over-escape) | ✅ BENAR |
|-------------------------|------------------|
| `` `"new_str": "Hello \`world\`"` `` | `"new_str": "Hello \`world\`"` (tidak perlu escape) |
| `` `"content": "\`template\`"` `` | `"content": "\`template\`"` |

 **Backtick di template literal JS aman di JSON string. Jangan di-escape.**

 ---

 ### 8. **STRING LITERAL PYTHON MULTI-BARIS (`"""`)**

| ❌ SALAH | ✅ BENAR |
|----------|----------|
| `"content": """def main():` <br> `    pass"""` | `"content": "def main():\n    pass"` |

 **JSON tidak support triple quote. Gunakan `\n`.**

 ---

 ### 9. **UNICODE DAN EMOJI**

| ❌ SALAH | ✅ BENAR |
|----------|----------|
| `"content": "\u2713"` (jika tidak yakin) | `"content": "✓"` (langsung pakai karakter) |
| `"content": "\u00E9"` | `"content": "é"` |

 **Karakter Unicode (termasuk emoji) aman di JSON UTF-8. Tidak perlu escape.**

 ---

 ### 10. **KOMENTAR MULTI-LINE C-STYLE (`/* */`)**

| ❌ SALAH | ✅ BENAR |
|----------|----------|
| `"old_str": "/*` <br> ` * Old code` <br> ` */"` | `"old_str": "/* Old code */"` (flatten ke satu baris) |
| `"old_str": "/*` <br> ` * Step 1` <br> ` * Step 2` <br> ` */"` | `"old_str": "/*\n * Step 1\n * Step 2\n */"` (pakai `\n`) |

 ---

 ## FORMAT JSON YANG BENAR

 ```json
 {
   "description": "Deskripsi singkat perubahan",
   "operations": [
     {
       "type": "str_replace",
       "path": "src/main.c",
       "old_str": "int main() {\n    printf(\"Hello\\n\");\n    return 0;\n}",
       "new_str": "int main() {\n    printf(\"World\\n\");\n    return 0;\n}",
       "scope": "function:main",
       "context_before": "",
       "context_after": ""
     },
     {
       "type": "create",
       "path": "src/utils/logger.c",
       "content": "#include <stdio.h>\n\nvoid log_msg(const char *msg) {\n    printf(\"[LOG] %s\\n\", msg);\n}\n"
     },
     {
       "type": "delete",
       "path": "src/old.c"
     }
   ]
 }
 ```
 ---

 ## ATURAN WAJIB

 1. **Escape newline:** setiap baris baru pakai `\n`, jangan Enter.
 2. **Escape backslash:** `\` di kode → `\\` di JSON (untuk string), `\\\\` di JSON (untuk path/regex).
 3. **Escape quote ganda:** `"` di kode → `\"` di JSON.
 4. **Jangan escape backtick** (` `` ` ) — aman.
 5. **Tidak ada trailing comma.**
 6. **Gunakan ASCII quote:** `"` bukan `“`.
 7. **Urutkan multiple edits dari bawah ke atas** (baris paling akhir dulu).
 8. **Untuk `old_str`, ambil 3-5 baris konteks** agar unik.

---

## Contoh Kasus Spesifik

### **C — Path dan Pointer**
```json
{
  "old_str": "char *path = \"C:\\\\Users\\\\name\\\\file.txt\";",
  "new_str": "char *path = \"D:\\\\Data\\\\file.txt\";"
}
```

### **JS — Regex dan Template Literal**
```json
{
  "old_str": "const regex = /\\d+/g;\nconst str = `Hello\\nWorld`;",
  "new_str": "const regex = /\\w+/g;\nconst str = `Hello World`;"
}
```

### **CSS — Pseudo-class dan Unicode**
```json
{
  "old_str": ".btn:hover {\n    color: red;\n}",
  "new_str": ".btn:focus {\n    color: blue;\n}"
}
```

### **Python — Multi-line String dan F-string**
```json
{
  "old_str": "def greet(name):\n    return f\"Hello {name}\"",
  "new_str": "def greet(name, title):\n    return f\"Hello {title} {name}\""
}
```

