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

| Data Structure  | Function & Class |
|:---------------:|:----------------:|
| List &amp; Tuple| `*args & **kwargs` |
| Mutability      | Iterator        |
| List Comprehension | Generator    |
| Dict Comprehension | Decorator    |
| Subclassing Types | Mixins        |

File &amp; coding dapat diakses pada: s.id/EFg

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

## List &amp; Tuple

--

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

## Mutable &amp; Immutable

--

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

## Comprehension

--

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

### Dictionary Comprehension

- Dictionary juga mempunya syntax comprehension
- Bedanya tentu saja, untuk dictionary menggunakan `{ }` bukan `[ ]`
- Selain itu, karena Dictionary terdiri dari key:value maka nilai yang diinputkan juga harus berpasangan

--

### Contoh Dictionary Comprehension

```python
reset_data = { k:0 for k in ['i', 'n', 'd', 'o', 'n', 'e', 's', 'i', 'a'] }

# atau lebih pendek
reset_data = { k:0 for k in 'indonesia' }

kelipatan = { k:k**2 for k in range(10) }
```

---

## Subclassing Built-in Data Types

--

### Subclassing Built-in Data Types

- Masih belum puas dengan tipe data yang disediakan Python?
- Perlu diingat, bahwa di Python everything is object
- Sehingga kita bisa bikin tipe data sendiri berdasarkan tipe data yang ada

--

### Override Method

Buat dictionary baru yang tidak menerima inputan value yang redundan

```python
class DistinctError(ValueError):
    """Raised when duplicate value is added to a distinctdict."""

class uniquedict(dict):
    
    def __setitem__(self, key, value):
        if value in self.values():
            if (
                (key in self and self[key] != value) or
                key not in self
            ):
                raise DistinctError("Nilai sudah digunakan oleh key lain")

        super().__setitem__(key, value)

ud = uniquedict()
ud['key'] = 'value'
ud['other_key'] = 'value'
```

--

### Membuat Method Baru

Buat list baru yang memiliki unlimited nested sublist

```python
class SubList(list):
    def __init__(self, name):
        self.name = name

    def sub(self, nesting=0):
        offset = "  " * nesting
        print('%s%s/' % (offset, self.name))

        for element in self:
            if hasattr(element, 'sub'):
                element.sub(nesting + 1)
            else:
                print("%s  %s" % (offset, element))

tree = SubList('project')
tree.append('README.md')
src = SubList('src')
src.append('script.py')
tree.append(src)
tree.sub()
```

---

# Function &amp; Class

---

## `*args` dan `**kwargs`

--

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
    for key, value in kwargs.items():
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

    for key, value in attrs.items():
        print("{}: {}".format(key, value))
```

---

## Iterator &amp; Generator

--

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

## Decorator

--

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

--

### Syntax Decorator dengan Parameter

```python
def outer_decorator(*outer_args,**outer_kwargs):
    def decorator(fn):
        def decorated(*args,**kwargs):
            do_something(*outer_args,**outer_kwargs)
            return fn(*args,**kwargs)
        return decorated
    return decorator
```

--

### Contoh Decorator dengan Parameter

```python
def writen_by(writen_by):
    def decorator(fn):
        def decorated(*args, **kwargs):
            print('this function writen by: {}'.format(writen_by))
            return fn(*args, **kwargs)
        return decorated
    return decorator

@writen_by('Fahri Firdausillah')
def good_idea(idea):
    return idea

print(good_idea('keeping secret'))
```

---

## Mixin

--

### Mixin (aka) Multiple Inheritance

- Mixin merupakan cara python untuk menyelesaikan permasalahan dari multiple inheritance, Diamond of Death
- Mixin digunakan untuk membuat class baru dengan kombinasi beberapa class komponen
- Kalau di Django banyak digunakan pada Class Based View

--

### Contoh Mixin

```python
class BaseClassA():
    def method_a(self):
        return "Method A"

class BaseClassB():
    def method_b(self):
        return "Method B"

class ChildClass(BaseClassA, BaseClassB):
    pass

child = ChildClass()
print(child.method_a())
print(child.method_b())
```

--

### Method Resolution Order

- Kunci dari Mixin adalah urutan eksekusi
- Mixin akan dieksekusi secara urut dari kiri ke kanan
- Sehingga jika ingin menambahkan fungsionalitas dari mixin sebelah kiri, jangan lupa untuk memanggilnya dalam mixin sebelah kanan

--

### Contoh MRO

```python
class BaseClassA():
    def method(self):
        print("Method A")

class BaseClassB():
    def method(self):
        super(BaseClassB, self).method()
        print("Method B")

class ChildClassA(BaseClassA, BaseClassB):
    pass

class ChildClassB(BaseClassB, BaseClassA):
    pass

child_a = ChildClassA()
child_a.method()

child_b = ChildClassB()
child_b.method()
```

---

## Konsep Lain

--

### Yang masih Belum Dibahas

- Context Manager
- Descriptor
- Meta Classes
- Convention &amp; PEP
- dan Masih Banyak Lagi

--

### Rekomendasi Referensi

- [Learning Python](https://www.packtpub.com/application-development/learning-python)
- [Expert Python Programming](http://www.packtpub.com/expert-python-programming/book)
- [Writing Idiomatic Python](https://jeffknupp.com/writing-idiomatic-python-ebook/)
- [Python Tutorial For Beginner](https://www.programiz.com/python-programming)
- [Advanced Python Tutorial](http://herculesphaeton.com/2015/03/python-learning-advanced-level/)

---

## Ada pertanyaan?