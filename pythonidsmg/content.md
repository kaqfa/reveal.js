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
| List &amp; Tuple| `*args & **kwargs` | Iterator |
| Mutability      | Generator     | Mixins      |
| List Comprehension | Decorator    | Meta Class  |

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

## Function Related (Before Class)

---

### `*args` dan `**kwargs`

- Fungsi dengan parameter, sudah biasa
- Fungsi dengan opsional parameter, banyak juga
- Di Python kita bisa membuat fungsi dengan unlimited parameter `*args`
- dan juga, keyword based unlimited parameter `**kwargs`
- serta menggabungkannya dengan parameter biasa

--

### Contoh `*args`

```python
def multiadds(*args):
    result = 0
    for number in args:
        result += number
    return result

multiadds(4, 5)
multiadds(4, 5, 6)
multiadds(4, 5, 6, 7, 8, 9, 10)
```

--

### Contoh `**kwargs`

```python
def men_attributes(**kwargs):
    for key, value in kwargs:
        print("Nilai dari {} adalah {}".format(key, value))

men_attributes(nama="Fahri Firdausillah")
men_attributes(bb=55, tb=160, rambut="hitam")
```

--

### Ordering Arguments

Jika semua jenis parameter / argumen digunakan, maka urutan deklarasinya adalah sebagai berikut:

1. Formal positional arguments
2. *args
3. Keyword arguments
4. **kwargs

--

### Contoh Positional Arguments

```python
def some_function(name, *langs, married = False, **attrs):
    print("Nama saya: {}".format(name))

    print("Keahlian", end=": ")
    for lang in langs:
        print(lang, end=" ")
    print("")

    print("Status marital", end=": ")
    if married :
        print("sudah menikah")
    else:
        print("jomblo")

    for key, value in attrs:
        print("{}: {}".format(key, value))
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

### Even Nested Loops

```python
new_list = [x * y for x in [20, 40, 60] for y in [2, 4, 6]]
new_list
```

--

### So The Syntax Is

```
[ expression for item in list if conditional ]
```

---

### Iterator

- Kita semua tahu loop `for` dalam Python tidak berbasis angka, tapi berbasis elemen *collection*
- Bagaimana jika kita ingin menggunakan loop yang tidak berbasis elemen?
- Jawabnya adalah **Iterator**

--

### Apa itu Iterator

- Iterator adalah object yang (harus) memiliki 2 method `__iter__` dan `__next__`
- `__iter__` mengembalikan object iterator itu sendiri
- `__next__` mengembalikan nilai selanjutnya dari iterator atau StopIteration Exception jika tidak ada nilai lagi

--

### Contoh Iterator Sederhana

```python
class Counter(object):
    def __init__(self, start, finish):
        self.current = start
        self.finish = finish

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.finish:
            raise StopIteration
        else:
            self.current += 1
            return self.current - 1
```

--

### Setelah Iterator Dibuat

```python
import itertools

for data in Counter(1, 10):
    print(data)

itertools.chain(Counter(1, 10), Counter(11, 20))
```

---

### Generator

- Generator hakikatnya adalah simplifikasi dari iterator dalam bentuk fungsi menggunakan perintah `yield`
- `yield` hampir sama seperti `return` hanya saja current data state tersimpan untuk dilanjutkan pada pemanggilan selanjutnya
- So generator adalah iterator, sehingga operasi yang kita lakukan pada iterator juga dapat kita lakukan pada generator

--

### Contoh Generator

```python
def ycounter(start, finish):
    current = start
    while current <= finish:
        yield current
        current += 1

y = ycounter(1, 10)
print(y.__next__())
print(y.__next__())
print(y.__next__())
```

---

### Hikmah dibalik Iterator &amp; Generator

- Jadi nggak kuper kalau diskusi atau baca kodingan orang lain
- (Katanya) lebih menghemat memori dan juga meningkatkan performa
- Terutama untuk generate list yang besar

---

### Decorator

- Dalam Python fungsi merupakan first class citizen, setara dengan nilai
- Artinya kita bisa meng-*assign* fungsi ke dalam variabel
- bisa dijadikan parameter untuk fungsi lain
- bisa juga dibuat nested function untuk di-*return* oleh fungsi induknya
- dan tentu saja bisa dibuat decorator

--

### Contoh First Class Citizen

```python
def greet(name):
    return "hello "+name

some_var = greet
some_var("Fahri")

def ahlan(name):
    return "Ahlan wa sahlan ya "+name

def greet_advanced(greet, name):
    return greet(name)+" selamat belajar Python"

greet_advanced(greet, "Fahri")
greet_advanced(ahlan, "Fahri")
```

--

### Contoh Nested Function

```python
def parent(number):
    def first_child():
        return "Ini anak pertama"

    def second_child():
        return "Ini anak kedua"

    def unborn_child():
        return "Anak yang nggak terlahir"

    if number == 1:
        return first_child
    elif number == 2:
        return second_child
    else:
        return unborn_child
```

--

### Apa itu Decorator?

- Decorator adalah *syntactic sugar* untuk nested function yang menjadi wrapper untuk fungsi lain
- Decorator membuat fungsi terlihat lebih rapi dan mudah dibaca

--

### Contoh Tanpa Decorator

```python
def greeting(name):
    return "Selamat datang di aplikasi ini {0}".format(name)

def sayonara(name):
    return "Sampai berjumpa pulang {0}".format(name)

def make_bold(func):
    def func_wrapper(name):
        return '<b>{0}</b>'.format(func(name))
    return func_wrapper

bold_greeting = make_bold(greeting)
bold_greeting("Fahri Firdausillah")
bold_sayo = make_bold(sayonara)
bold_sayo("Fahri Firdausillah")
```

--

### Dengan Decorator

```python
@make_bold
def greeting2(name):
    return "Selamat datang di aplikasi ini {0}".format(name)

@make_bold
def sayo2(name):
    return "Sampai berjumpa pulang {0}".format(name)

greeting2("Fahri Firdausillah")
sayo2("Fahri Firdausillah")
```

---

### Mixins

Content Mixin

---

### Method Resolution Order

Content MRO

---

### Meta Class

Content Meta Class
