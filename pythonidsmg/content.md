### Python is Not Your Previous Programming Language
**Write Better Code Using Python**

### Fahri Firdausillah

---

### Fahri Firdausillah

- **profesi**: Pengajar di UDINUS
- **keahlian**: Django, Android, Laravel, CI
- **blog**: kaqfa.github.io
- **blog dinus**: fahri.blog.dinus.ac.id
- **github**: @kaqfa
- **google scholar**: s.id/DWi

---

### Table of Contents

| Data Structure  | Before Class  | After Class |
|---------------- |-------------- |-------------|
| List &amp; Tuple| `*args & **kwargs` | Mixins |
| Mutability      | Iterator      | Method Resolution Order |
| List Comprehension | Generator  | Meta Class |
|                 | Decorator     |            |

---

### Preambule

- Kebanyakan (hampir semua) dari kita mempelajari Python setelah belajar bahasa pemrograman lain
- Sudut serang yang digunakan pun akhirnya masih terbayang sudut yang lama
- Banyak fitur Python jadi nganggur

--

#### Ibarat ngomong Indonesian English

### Join **with** us

--

#### Ibarat Nyetir Mobil Tapi

### mental pengendara **motor**

---

# Data Structure

---

### List &amp; Tuple

- Python tidak memiliki **Array**
- Tapi punya List, Tuple, Set, &amp; Dictionary

--

### List vs Tuple

- List menggunakan `[ ]` Tuple menggunakan `( )`
- Tuple (sedikit) lebih cepat dari List
- List **Mutable** dan Tuple **Immutable**

--

### Contoh Koding

```python
a_list = [1, 2, 3, 4, 5]
a_tuple = (1, 2, 3, 4, 5)

print(a_list[2])
print(a_tuple[2])

a_list = [6, 7, 8, 9, 10]
a_tuple = (6, 7, 8, 9, 10)

a_list[3] = 12
a_tuple[3] = 12 # error
```

---

### Immutable types in python

int, float, decimal, complex, bool, string, tuple, range, frozenset, bytes

--

### Mutable types in python

list, dict, set, bytearray, **user-defined classes**

--

### Mutable vs Immutable

- *Immutable* tidak sama dengan konstanta
- *Immutable* berarti nilai yang tersimpan tidak bisa dirubah
- Sedangkan isi dari variabel bisa tetap berubah

--

### How Immutable Change

Ketika kita melakukan perubahan nilai pada variabel yang menyimpan immutable types, Python akan meminta slot memori baru untuk nilai baru tersebut, kemudian mereferensikan alamat yang baru pada variabel penampung.

--

### How Mutable Change

Python akan langsung merubah nilai yang tersimpan di alamat memori variabel mutable

--

### Passing By Refference?

- Kita bisa memanfaatkan mutable types untuk (semacam) parameter passing by refference

```python
def bad_changer(nilai, best_mark):
    nilai = best_mark

def good_changer(nilai, best_mark):
    nilai[0] = best_mark

nilai_mhs1 = 80
bad_changer(nilai_mhs1, 90)
print(nilai_mhs1)

nilai_mhs2 = [80]
good_changer(nilai_mhs2, 90)
print(nilai_mhs2[0])
```

--

### Performance Improvement?

Studi kasus pada konkatenasi String

```python
first = "Fahri"
last = "Firdausillah"
fullname = first+' '+last
# atau
fullname = ' '.join((first, last))

def concateplus(times):
    teks = ''
    for time in range(times):
        teks += "Teks "
    return teks

def concatejoin(times):
    temp = []
    for time in range(times):
        temp.append("Teks ")
    return ''.join(temp)
```

---

### List Comprehension

Buat perintah untuk melakukan generate list dari 1 hingga 10

--

### So Lame

```python
new_list = []
for data in range(1, 11):
    new_list.append(data)

new_list
```

--

### Like a Boss

```python
new_list = [data for data in range(1, 11)]
new_list
```

--

### Additional Process

```python
new_list = [data*2 for data in range(1, 11)]
new_list
```

--

### With Condition

```python
new_list = [data for data in range(1, 11) if data % 2 == 0]
new_list
```

--

### So The Syntax Is

```
[ expression for item in list if conditional ]
```

---

### Iterator

Content 2.1

---

### Generator

Content 3.1

---

### Decorator

Content 3.2

---

### Mixins

Content Mixin

---

### Method Resolution Order

Content MRO

---

### Meta Class

Content Meta Class
