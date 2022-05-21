
# **Pandas**

## **Pandas nedir?**

Pandas veri okuma, veri analizi ve veri temizlemede kullanılan açık kaynak kodlu python kütüphanesidir. Numpy alternatifi değildir, Numpy özelliklerini kullanıp genişletir.

## **Nasıl kurulur?**

```
pip install pandas
```

## **Projeye entegre edilmesi**


```python
# Artık pandas kütüphanesi pd ile adlandırılacaktır.
import pandas as pd 
```

## **Pandas sürümünü kontrol etmek**



```python
pd.__version__
```




    '1.3.5'



# **Pandas veri yapıları**

*   Series
*   DataFrames

## **Series**

Seriler, etiketlerden (indeks) oluşan tek boyutlu bir veri yapısıdır.

### Seri oluşturma

Pandas kütüphanesi içerisindeki Series methodunu kullanabilirz. Series methodu içerisine **data** vermemiz gerekmekte bu data değer, liste, Numpy dizisi veya sözlükler (dictionary) olabilir.


```python
series = pd.Series([10, 20, 30, 40, 50])

print(series)
```

    0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64
    

**Bir etiket vermediğimizden için etiketlerimiz otomatik olarak 0'dan başlayarak atandı. **

### **Etiket (indeks) bilgileri**

Serilerin etiket (indeks) bilgilerine erişmek için axes kullanılabilir.


```python
series.axes
```




    [RangeIndex(start=0, stop=5, step=1)]



*Burada 0'dan başlayıp 5'e kadar gitmiş ve birer birer artmıştır*

### **Değerler ile ilgili bilgi almak**

Değerler ile ilgili bilgi almak istediğimizde dtype kullanabiliriz.


```python
series.dtype
```




    dtype('int64')



### **Öğe sayısını almak**


```python
series.size
```




    5



### **Dizi şeklinde değerlere erişmek**

Serileri dizi şeklinde değerlerine erişmek istersek values özelliğini kullanabiliriz. values özelliği serileri türüne bağlı olarak ndarray (Numpy array) şeklinde geri döndürür.


```python
series.values
```




    array([10, 20, 30, 40, 50])



### **İlk belirli bir elemana erişmek**

Bir serinin ilk belirli elemanına erişmek istersek head methodunu kullanabiliriz. head methodu içerisine yazdığımız değer kadar elemanı bize geri döndürür.


```python
series.head()
```




    0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64



*Default değer 5 atandığı için head içerisine bir şey yazmadığımızda ilk 5 elemanı bizlere getirecektir.*


```python
series.head(3)
```




    0    10
    1    20
    2    30
    dtype: int64



### **Seri içerisindeki değerleri toplamak (sum)**

Serimizin içerisindeki değerleri toplamak istersen sum methodunu kullanabiliriz.


```python
summation = series.sum()

print(summation)
```

    150
    

### **Seri içerisindeki en büyük değere ulaşmak (max)**

Seri içerisinde en büyük değere ulaşmak için max methodunu kullanabiliriz.


```python
maximum = series.max()

print(maximum)
```

    50
    

### **Seri içerisindeki en küçük değere ulaşmak (min)**

Seri içerisinde en küçük değere ulaşmak için min methodunu kullanabiliriz.


```python
minimum = series.min()

print(minimum)
```

    10
    

### **Serinin ortalamasını bulmak (mean)**

Serinin ortalamasını bulmak için mean methodunu kullanabiliriz.


```python
average = series.mean()

print(average)
```

    30.0
    

### **Etiket isimlendirme**

Etiket isimlendirme işleminde seri oluştururken Series methoduna bir index paramatresi göndererek etiketleme işlemini yapabiliriz.


```python
series = pd.Series([11, 32, 45, 62, 71], index = [1, 3, 5, 7, 9])

print(series)
```

    1    11
    3    32
    5    45
    7    62
    9    71
    dtype: int64
    

*Etiketleri elimizle index ifadesine verdiğimiz için artık serimizin etiketleri bizim verdiğimiz değerler olacaktır.*


```python
series = pd.Series([11, 32, 45, 62, 71], index = ["a", "b", "c", "d", "e"])

print(series)
```

    a    11
    b    32
    c    45
    d    62
    e    71
    dtype: int64
    

*Etiket verme işleminde illa tam sayı olacak diye bir koşul yok string değer de verebiliriz.*

### **Etikete göre elemana erişme**

Serinin etiketine göre elemana erişmek istersek sözlük (dictionary) mantığını gibi kullanabiliriz.


```python
series = pd.Series([11, 32, 45, 62, 71], index = ["a", "b", "c", "d", "e"])

first_element = series["a"] # ilk etiket "a" olduğu için bu şekilde kullandık
last_element = series["e"]

print(first_element)
print(last_element)
```

    11
    71
    

### **Serinin belirli bir aralığına erişme**

Serinin belirli bir aralığına erişmek için kullanılan etikete göre elemana erişme işleminden sonra gidilecek yeri söyleyerek bir aralığa erişebiliriz.


```python
series = pd.Series([11, 32, 45, 62, 71], index = ["a", "b", "c", "d", "e"])

intermittent_values = series["a": "c"] # dizinin "a" etiketinden "c" etiketi dahil olmak üzere belirlenen aralığı getirir

print(intermittent_values)
```

    a    11
    b    32
    c    45
    dtype: int64
    

### **İki seriyi birleştirme**

İki seriyi birleştirmek için pandas kütüphanesinden concat methodu kullanılabilir. concat methodu kullanılırken içine verilecek değerleri bir listenin içerisinde yazmamız gerekmektedir.


```python
series1 = pd.Series([11, 32, 45, 62, 71], index = ["a", "b", "c", "d", "e"])
series2 = pd.Series([1, 2, 3, 4, 5, 6])

compound_series = pd.concat([series1, series2])

print(compound_series)
```

    a    11
    b    32
    c    45
    d    62
    e    71
    0     1
    1     2
    2     3
    3     4
    4     5
    5     6
    dtype: int64
    

### **Serinin etiketlerine erişmek**

Bir serinin etiketlerine erişmek istersek index özelliğini kullanabiliriz.


```python
series = pd.Series([1, 2, 3, 4, 5], index = ["a", "b", "c", "d", "e"])

print(series.index)
```

    Index(['a', 'b', 'c', 'd', 'e'], dtype='object')
    

### Serinin değerlerine erişmek

Bir serinin değerlerine erişmek istersek keys özelliğini kullanabiliriz.


```python
series = pd.Series([1, 2, 3, 4, 5], index = ["a", "b", "c", "d", "e"])

print(series.keys)
```

    <bound method Series.keys of a    1
    b    2
    c    3
    d    4
    e    5
    dtype: int64>
    

### **Seriyi listeye dönüştürme**

Bir seriyi listeye dönüştürmek istersek items methodu ile bir liste şekline sonra da list methodu ile listeye çevirebiliriz.


```python
series = pd.Series([1, 2, 3, 4, 5], index = ["a", "b", "c", "d", "e"])

sample_list = list(series.items())

print(sample_list)
```

    [('a', 1), ('b', 2), ('c', 3), ('d', 4), ('e', 5)]
    

### **Fancy ile elemana erişmek**


```python
series = pd.Series([1, 2, 3, 4, 5], index = ["a", "b", "c", "d", "e"])

sample_fancy = series[["a", "d"]]

print(sample_fancy)
```

    a    1
    d    4
    dtype: int64
    

*Serimizin içerisine istediğimiz değerleri liste şeklinde gönderip fancy yardımıyla bu değerlere erişmiş olduk.*

### Etiketin değerini değiştirmek


```python
series = pd.Series([1, 2, 3, 4, 5], index = ["a", "b", "c", "d", "e"])

series["a"] = 10

print(series)
```

    a    10
    b     2
    c     3
    d     4
    e     5
    dtype: int64
    

*Serimizin içerisindeki "a" değerine erişip bu değişkene 10 değeri ile değiştirme işlemi yaptık.*

## **DataFrame**

DataFrame veri çerçevesi anlamına gelir. Sql tablosuna benzer bir yapıdadır. DataFrameler veriyi daha kolay işleme imkanı sunar.

### **DataFrame oluşturma**

Pandas kütüphanesinin içerisinde yer alan DataFrame ile oluşturulabilir. DataFrame içerisine bir data ve index gibi bir çok özellik alır. Eğer index değişkenine atama yapmazsak otomatik 0'dan başlayarak artar. Eğer columns değerini girersek oluşacak olan DataFrame yapısının column ismini ayarlar.


```python
df = pd.DataFrame([10, 20, 30, 40, 50], columns=["column 1"])

print(df)
```

       column 1
    0        10
    1        20
    2        30
    3        40
    4        50
    

*DataFrame içerisindeki data parametresi yerine sözlük (Dictionary), Numpy dizisi veya başka bir DataFrame koyabiliriz.*

### **DataFrame sütunları isimlendirmek**

DataFrame kullanırken sütunlara erişmek veya bu sütunlarin isimlerini değiştirmek istediğimizde columns özelliğini kullanabiliriz.


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"])

print(df.columns) # DataFrame içerisinde yer alan sütunların isimlerini geri döndürür

print("-" * 30)
df.columns = ("sutün 1", "sütun 2", "sütun 3") # Sütünlar otomatik atadığımız değişkenlerle değiştir tekrar yeni bir değişkene atama işlemimize gerek yoktur.

print(df)
```

    Index(['column 1', 'column 2', 'column 3'], dtype='object')
    ------------------------------
       sutün 1  sütun 2  sütun 3
    0       10       20       30
    1        1        2        3
    

*Numpy dizilerini kullanarak iki boyutlu ve üç elemanlı bir dizi oluşturduk. Oluşan bu diziyi ise DataFrame data özelliği olarak verdik ve sütun isimlendirilmesi yaptık.*

### **DataFrame içserisindeki değerleri çekme**

DataFrame içerisinde değerleri çekmek için values özelliği kullanılabilir. Fakat values özelliği bir numpy dizisi geri döndürür.


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"])

print(df.values) # Diz içerisindeki verilere ulaşma işlemi
print("-" * 30)
print(type(df.values)) # ndarray şeklinde bir numpy dizisi geri döndürür
```

    [[10 20 30]
     [ 1  2  3]]
    ------------------------------
    <class 'numpy.ndarray'>
    

### **DataFrame index değiştirmek**

DataFrame index değiştirme işlemi için index özelliğine yeni indeks değerleri atanabilir.


```python
import numpy as np

arr1 = np.random.randint(10, size=5)
arr2 = np.random.randint(10, size=5)

dictionary = {
    "pro1" : arr1,
    "pro2" : arr2
}

# Sözlük kullanarak bir DataFrame oluşturduk.
df = pd.DataFrame(dictionary)

# DataFrame ilk hali
print(df)
print("-" * 30)

df.index = ["a", "b", "c", "d", "e"]

# DataFrame son hali
print(df)
```

       pro1  pro2
    0     8     3
    1     8     7
    2     0     0
    3     9     8
    4     2     0
    ------------------------------
       pro1  pro2
    a     8     3
    b     8     7
    c     0     0
    d     9     8
    e     2     0
    

### **DataFrame indeks ile satırlara erişmek**


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

rows = df["a": "b"]

print(rows)
```

       column 1  column 2  column 3
    a        10        20        30
    b         1         2         3
    

*DataFrame içerisinden indekse göre satırlara erişmek istediğimizden bu şekilde kullanabiliriz.*

### **DataFrame içerisinden satır silme**

DataFrame içerisinden bir satırı silmek istediğimizde drop methodunu kullanabiliriz.


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

print(df)
print("-" * 30)

# DataFrame içerisindeki etiketi "b" olan satırı silme işlemi.
df.drop("b", axis=0, inplace = True)

print(df)
```

       column 1  column 2  column 3
    a        10        20        30
    b         1         2         3
    c        40        50        60
    ------------------------------
       column 1  column 2  column 3
    a        10        20        30
    c        40        50        60
    

*drop methodunun ilk parametresi neyi silmek istediğimizi belirtir ikinci parametresi olan axis parametresini eğer 0 olarak atama yaparsak DataFrame içerisinde satırları belirtir, eğer axis parametresini 1 olarak atama yaparsak sütunları belirtir. drop fonksiyonun üçüncü parametresi olan inplace özelliği bizim değişiklik yaptığımız DataFrame üzerinde değişiklik yapılmasını kontrol eder. Varsayılan olarak inplace özelliği False olarak ayarlanmıştır yani bir satır silmek istediğimizde ve inplace özelliğine False değerini atamış olursak varsayılan DataFrame herhangi bir değişikliğe uğramayacaktır.*


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

print(df)
print("-" * 30)

# DataFrame içerisindeki etiketi "column 1" olan sütünu silme işlemi.
df.drop("column 1", axis=1, inplace = True)

print(df)
```

       column 1  column 2  column 3
    a        10        20        30
    b         1         2         3
    c        40        50        60
    ------------------------------
       column 2  column 3
    a        20        30
    b         2         3
    c        50        60
    

*drop fonksiyonunun ilk parametresini neyi silmek istediğimizi verdik, ikinci parametrede satır mı sütun mu bunu belirttik (0 = Satır, 1 = sütun), üçüncü parametresinde ise DataFrame üzerinde bir değişiklik yapılacağını inplace özelliğini True atayarak yapmış olduk.*

birden fazla satır veya sütun silme işlemi;


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

print(df)
print("-" * 30)

# DataFrame içerisindeki etiketi "column 1" olan sütünu silme işlemi.
df.drop(["a", "b"], axis=0, inplace = True)

print(df)
```

       column 1  column 2  column 3
    a        10        20        30
    b         1         2         3
    c        40        50        60
    ------------------------------
       column 1  column 2  column 3
    c        40        50        60
    

*Burada birden fazla satır silme işlemi yapmak için fancy kullandık yani drop methodumuza bu sefer tek bir elemanı sil demedik birden fazla elemani liste şeklinde gönderdik.*

### DataFrame içerisine yeni bir sütun oluşturmak

Listeye eleman ekleme yapısı gibi atama işlemi yapabiliriz.


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

print(df)
print("-" * 30)

df["column 4"] = df["column 1"] + df["column 2"]

print(df)
```

       column 1  column 2  column 3
    a        10        20        30
    b         1         2         3
    c        40        50        60
    ------------------------------
       column 1  column 2  column 3  column 4
    a        10        20        30        30
    b         1         2         3         3
    c        40        50        60        90
    

*Burada "column 4" sütununu oluşturmak istiyoruz ve listeye eleman ekleme işlemi gibi uyguluyoruz.*

### **DataFrame üzerinde veri seçme işlemleri**

*   loc
*   iloc

#### **loc**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

print(df)
print("-" * 30)

locate = df.loc[1:5]
print(locate)
```

        a   b   c   d   e
    0  15  70  89  76  20
    1  69  22  55   6  71
    2  49  67  97  72  61
    3  49  91  98  22  61
    4  72  96   5  72  56
    5  45  81  39  47  39
    6  50  93  19  85  11
    7  34  50  78  98  19
    8  73  44  79  88   8
    9  10   7  60  36  25
    ------------------------------
        a   b   c   d   e
    1  69  22  55   6  71
    2  49  67  97  72  61
    3  49  91  98  22  61
    4  72  96   5  72  56
    5  45  81  39  47  39
    

*Burada oluşturmuş olduğumuz 10 satırlı bir DataFrame içerisindeki 1. elemandan ve 5. elemana (dahil) kadar bir veri seçme işlemi gerçekleştirdik.*

#### **iloc**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

print(df)
print("-" * 30)

locate = df.iloc[1:5]

print(locate)
```

        a   b   c   d   e
    0  41  40  18   4  96
    1  41  58  51  95  76
    2  19   9  98  82  58
    3  81  56  16  78  64
    4  11  55  72  11  97
    5  30  53  30  39  79
    6  15  63  62  17   2
    7  23  36  68  50  74
    8  32  94  71  74  90
    9  53  41  89  33  45
    ------------------------------
        a   b   c   d   e
    1  41  58  51  95  76
    2  19   9  98  82  58
    3  81  56  16  78  64
    4  11  55  72  11  97
    

#### **iloc ile loc arasında aralıklı veri seçim farkı**

iloc ile loc temel farkını satır ve sütun veri seçme işleminde göreceğiz.

loc kullandığımızda verdiğimiz aralığın ikisini de kapsar fakat iloc kullandığımızda verilen aralığın ilki dahil ikindisi dahil olmayaktır. Örneğim 5 satırlık bir DataFrame oluşturduk ve biz bu DataFrame içerisinden ilk 1. satırdan 3. satıra (dahil değil) kadar olan verilere erişmek istiyoruz. Burada iki farklı yolumuz vardır;

*   loc ifadesi ile = df.loc[1:2] 
*   iloc ifadesi ile = df.iloc[1:3]

Eğer loc ile iloc aralığını aynı verirsek farkı daha iyi anlayabiliriz. Örnek olarak;


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

# Oluşturduğumuz DataFrame
print("Oluşturduğumuz DataFrame")
print(df)
print("-" * 30)

# loc ile veriye erişmek
print("loc ile veriye erişmek")
locate = df.loc[1:3]
print(locate)
print("-" * 30)

# iloc ile veriye erişmek
print("iloc ile veriye erişmek")
locate = df.iloc[1:3]
print(locate)
print("-" * 30)
```

    Oluşturduğumuz DataFrame
        a   b   c   d   e
    0  89  50  27  47  53
    1  91  28  11  19  69
    2  92  88  72  83  99
    3  99  78  65  35  86
    4  90  35  74  60  61
    ------------------------------
    loc ile veriye erişmek
        a   b   c   d   e
    1  91  28  11  19  69
    2  92  88  72  83  99
    3  99  78  65  35  86
    ------------------------------
    iloc ile veriye erişmek
        a   b   c   d   e
    1  91  28  11  19  69
    2  92  88  72  83  99
    ------------------------------
    

*Burada gördüğünüz üzere loc ve iloc aralığını aynı verdiğimizde, loc son aralık değerini dahil etti fakat iloc dahil etmedi.*

#### **Satır ve sütun veri seçme işlemi**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

locate = df.iloc[0:3, 0:2]
print(locate)
```

        a   b
    0  11  74
    1  57  27
    2  88  18
    

*Burada veri seçme işlemi için dilersek iloc dilersek de loc kullanabiliriz. iloc veya loc içerisine verilen ilk aralık(0:3) satırları, ikinci aralık(0:2) ise sütunları temsil eder.*

**ÖNEMLİ**

**iloc ile direkt sütun işlemi yapılmaz indeks işlemi yapılır**

Örneğin;


```python
import numpy as np
import logging
import traceback

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

try:
  locate = df.iloc[0:3, "a"]
  print(locate)
except Exception as e:
  logging.error(traceback.format_exc())
```

    ERROR:root:Traceback (most recent call last):
      File "/usr/local/lib/python3.7/dist-packages/pandas/core/indexing.py", line 754, in _has_valid_tuple
        self._validate_key(k, i)
      File "/usr/local/lib/python3.7/dist-packages/pandas/core/indexing.py", line 1426, in _validate_key
        raise ValueError(f"Can only index by location with a [{self._valid_types}]")
    ValueError: Can only index by location with a [integer, integer slice (START point is INCLUDED, END point is EXCLUDED), listlike of integers, boolean array]
    
    The above exception was the direct cause of the following exception:
    
    Traceback (most recent call last):
      File "<ipython-input-37-4cd83f647b7b>", line 9, in <module>
        locate = df.iloc[0:3, "a"]
      File "/usr/local/lib/python3.7/dist-packages/pandas/core/indexing.py", line 925, in __getitem__
        return self._getitem_tuple(key)
      File "/usr/local/lib/python3.7/dist-packages/pandas/core/indexing.py", line 1506, in _getitem_tuple
        self._has_valid_tuple(tup)
      File "/usr/local/lib/python3.7/dist-packages/pandas/core/indexing.py", line 759, in _has_valid_tuple
        ) from err
    ValueError: Location based indexing can only have [integer, integer slice (START point is INCLUDED, END point is EXCLUDED), listlike of integers, boolean array] types
    
    

*Burada eğer bir aralık vermeyip istediğimiz satırı veya sütunun değerini verirsek indeks bazlı veri seçmek olacak fakat iloc index bazlı seçim yapamaz burada iloc yerine loc kullanabiliriz.*


```python
import numpy as np
import logging
import traceback

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

try:
  locate = df.loc[0:3, "a"]
  print(locate)
except Exception as e:
  logging.error(traceback.format_exc())
```

    0    44
    1    93
    2    64
    3    47
    Name: a, dtype: int64
    

**Burada direkt bir sütunun değerini veya satırın değerini verdiğimiz için loc ifadesi ile veri seçme işlemimizi gerçekleştirmiş olduk**

####**iloc ile sütun seçme işlemi**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

locate = df.iloc[0:3]["a"]

print(locate)
```

    0    30
    1    48
    2    65
    Name: a, dtype: int64
    

*Burada iloc ile sütun seçme işlemi yaptık burada satır olarak 0'dan 3'e kadar olan satırları seçtik ve bu satırladın da sahip olduğu a sütununu aldık.*

Birden fazla sütun seçmek istersek fancy kullanabiliriz. Örneğin;


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

locate = df.iloc[0:3][["a", "d", "e"]]

print(locate)
```

        a   d   e
    0  42  22  23
    1  74  92  19
    2   5  19  95
    

*Burada fancy yardımıyla birden fazla sütun seçme işlemini yapabildik.*

#### **Koşullu eleman seçme işlemi**



```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

print(df[df.a > 15])
```

        a   b   c   d   e
    0  22  29   3  18  21
    2  17  23  23   9  11
    4  26  12  13  20  23
    7  18  19   7  13  24
    

*Burada a sütunundaki değerlerin 15'den büyük olma koşulunu verdik. DataFrame içerisindeki sütuna erişmek için df.a ifadesini kullandık.*

Birden fazla koşul girmek;


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

print(df[(df.a > 15) & (df.d > 5)])
```

        a   b   c   d   e
    0  28  19   5  18  13
    1  27  10   6   8   5
    4  19  22  12   9  18
    6  28  29  12  17  11
    7  29  26   5  15  15
    

*Burada a sütunundaki değerlerin 15'den büyük olduğu ve d sütunundaki değerlerin 5'den büyük olduğu değerleri aldık.*

### DataFrame sütunları değiştirmek

DataFrame içerisindeki sütunları değiştirmek istersek columns kullanabiliriz.


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (5, 3))
df = pd.DataFrame(random_arr, columns=["a", "b", "c"])

df.columns = ["A", "B", "C"]

print(df)
```

        A   B   C
    0  16  20   7
    1  21  27   3
    2   1  23   2
    3  19  21  24
    4  26  23   4
    

### DataFrame birleştirme işlemleri (concat)

DataFrame birleştirme işlemleri için concat methodunu kullanabiliriz


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (5, 3))
df1 = pd.DataFrame(random_arr, columns=["a", "b", "c"])
df2 = df1 * 2 # Oluşturulan df1 değerini 2 ile çarpıp df2 değişkenine atanma işlemi

print("Oluşturulan ilk DataFrame")
print(df1)
print("-" * 30)
print("Oluşturulan ikinci DataFrame")
print(df2)
print("-" * 30)

concat_df = pd.concat([df1, df2])
print("df1 ve df2 DataFrame birleştirme işlemi")
print(concat_df)
```

    Oluşturulan ilk DataFrame
        a   b   c
    0  24  28  13
    1  16   4  29
    2  26  22  26
    3  24  23  18
    4  18  24  22
    ------------------------------
    Oluşturulan ikinci DataFrame
        a   b   c
    0  48  56  26
    1  32   8  58
    2  52  44  52
    3  48  46  36
    4  36  48  44
    ------------------------------
    df1 ve df2 DataFrame birleştirme işlemi
        a   b   c
    0  24  28  13
    1  16   4  29
    2  26  22  26
    3  24  23  18
    4  18  24  22
    0  48  56  26
    1  32   8  58
    2  52  44  52
    3  48  46  36
    4  36  48  44
    

*Burada indeksleri birleştirme işlemi sonrasında indeksleri incelediğimizde bir hata görüyoruz. İndeksler 0'dan başlayıp 5'e kadar ilerlemiş fakat tekrar 0'dan başlayıp 5'e kadar ilerlemiş.*

Bu sorunu çözmek için;


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (5, 3))
df1 = pd.DataFrame(random_arr, columns=["a", "b", "c"])
df2 = df1 * 2 # Oluşturulan df1 değerini 2 ile çarpıp df2 değişkenine atanma işlemi

print("Oluşturulan ilk DataFrame")
print(df1)
print("-" * 30)
print("Oluşturulan ikinci DataFrame")
print(df2)
print("-" * 30)

concat_df = pd.concat([df1, df2], ignore_index=True)
print("df1 ve df2 DataFrame birleştirme işlemi")
print(concat_df)
```

    Oluşturulan ilk DataFrame
        a   b   c
    0   8  10  23
    1  27  20   3
    2  26   7   6
    3  20  14  14
    4  23  16  23
    ------------------------------
    Oluşturulan ikinci DataFrame
        a   b   c
    0  16  20  46
    1  54  40   6
    2  52  14  12
    3  40  28  28
    4  46  32  46
    ------------------------------
    df1 ve df2 DataFrame birleştirme işlemi
        a   b   c
    0   8  10  23
    1  27  20   3
    2  26   7   6
    3  20  14  14
    4  23  16  23
    5  16  20  46
    6  54  40   6
    7  52  14  12
    8  40  28  28
    9  46  32  46
    

*Burada concat methodunun içerisine ignore_index parametresine True atadığımızda indeks problemimiz ortadan kalktı.*

#### **Farklı sütünlara sahip olan DataFrame birleştirme işlemi**


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (5, 3))
df1 = pd.DataFrame(random_arr, columns=["a", "b", "c"])
random_arr = np.random.randint(1,30, size = (5,3))
df2 = pd.DataFrame(random_arr, columns=["Column 1", "Column 2", "c"])

print(pd.concat([df1, df2],  ignore_index=True))
```

          a     b   c  Column 1  Column 2
    0   1.0  29.0  11       NaN       NaN
    1  18.0  28.0   4       NaN       NaN
    2  23.0  12.0   4       NaN       NaN
    3  23.0  15.0  13       NaN       NaN
    4  20.0  20.0  14       NaN       NaN
    5   NaN   NaN   1      19.0      17.0
    6   NaN   NaN  16      10.0      21.0
    7   NaN   NaN   8      13.0       2.0
    8   NaN   NaN   1      17.0       6.0
    9   NaN   NaN  11       6.0       4.0
    

*Burada görülen NaN ifadeleri birinci DataFrame ile ikinci DataFrame eşleşmediğinden ortaya çıkmıştır. Görüldüğü gibi sütun c iki DataFramede eşleştiği için otomatik c ifadesinin bulunduğu sütuna yazılmıştır.*


```python
print(pd.concat([df1, df2], join="inner", ignore_index=True))
```

        c
    0  11
    1   4
    2   4
    3  13
    4  14
    5   1
    6  16
    7   8
    8   1
    9  11
    

*Burada iki DataFramede ortak sütun olanları birleştirdik.*

### **İleri Birleştirme işlemleri (merge)**

*   Birebir (one to one) birleştirme
*   Çoktan bire (many to one) birleştirme



#### **Birebir (one to one) birleştirme**


```python
students = {
    "name": ["Furkan", "Özlem", "Kardem", "Doga"],
    "department": ["Bilgisayar", "Kimya", "Yazılım", "Yazılım"]
}

student_department = pd.DataFrame(students)

print(student_department)
```

         name  department
    0  Furkan  Bilgisayar
    1   Özlem       Kimya
    2  Kardem     Yazılım
    3    Doga     Yazılım
    


```python
graduation = {
    "name" : ["Furkan", "Özlem", "Kardem", "Doga"],
    "year" : ["2023", "2023", "2024", "2021"]
}

graduation_year = pd.DataFrame(graduation)

print(graduation_year)
```

         name  year
    0  Furkan  2023
    1   Özlem  2023
    2  Kardem  2024
    3    Doga  2021
    


```python
print(pd.merge(student_department, graduation_year))
```

         name  department  year
    0  Furkan  Bilgisayar  2023
    1   Özlem       Kimya  2023
    2  Kardem     Yazılım  2024
    3    Doga     Yazılım  2021
    

*student_department ile graduation_year DataFramelerimizi birleştirmek istedik ve merge ifadesi kullanılarak bu işlemi gerçekleştirdik. merge methodou otomatik olarak ortak olan sütuna göre birleştirme işlemi yapar.*

#### **Çoktan teke (many to one) birleştirme işlemi**


```python
students = {
    "name": ["Furkan", "Özlem", "Kardem", "Doga"],
    "department": ["Bilgisayar", "Kimya", "Yazılım", "Yazılım"]
}

graduation = {
    "name" : ["Furkan", "Özlem", "Kardem", "Doga"],
    "year" : ["2023", "2023", "2024", "2021"]
}

student_department = pd.DataFrame(students)
graduation_year = pd.DataFrame(graduation)

school = pd.merge(student_department, graduation_year)
print(school)
```

         name  department  year
    0  Furkan  Bilgisayar  2023
    1   Özlem       Kimya  2023
    2  Kardem     Yazılım  2024
    3    Doga     Yazılım  2021
    


```python
department = {
    "department" : ["Bilgisayar", "Yazılım", "Kimya"],
    "head" : ["Raif", "Volkan", "Asım"]
}

department_heads = pd.DataFrame(department)

print(department_heads)
```

       department    head
    0  Bilgisayar    Raif
    1     Yazılım  Volkan
    2       Kimya    Asım
    


```python
print(pd.merge(school, department_heads))
```

         name  department  year    head
    0  Furkan  Bilgisayar  2023    Raif
    1   Özlem       Kimya  2023    Asım
    2  Kardem     Yazılım  2024  Volkan
    3    Doga     Yazılım  2021  Volkan
    

*Burada bölümün başkanlarını belirten bir DataFrame oluşuturduk. Bu DataFrame ile daha önceden Öğrenci-Bölüm DataFrame ve Öğrenci-Mezuniyet yılını birleştirdiğimiz DataFrame ile birleştirme işlemi yaptık. Burada department her ikisi için olduğundan otomatik olarak birleştirme işlemi gerçekleşti. Görüleceği gibi yazılım bölümünün birden fazla bulunmaktadır.*

#### **Çoktan çoka (many to many) birleştirme**


```python
students = {
    "name": ["Furkan", "Özlem", "Kardem", "Doga"],
    "department": ["Bilgisayar", "Kimya", "Yazılım", "Yazılım"]
}

graduation = {
    "name" : ["Furkan", "Özlem", "Kardem", "Doga"],
    "year" : ["2023", "2023", "2024", "2021"]
}

student_department = pd.DataFrame(students)
graduation_year = pd.DataFrame(graduation)

school = pd.merge(student_department, graduation_year)
print(school)
```

         name  department  year
    0  Furkan  Bilgisayar  2023
    1   Özlem       Kimya  2023
    2  Kardem     Yazılım  2024
    3    Doga     Yazılım  2021
    


```python
department = {
    "department" : ["Bilgisayar", "Yazılım", "Kimya"],
    "head" : ["Raif", "Volkan", "Asım"]
}

department_heads = pd.DataFrame(department)

print(department_heads)
```

       department    head
    0  Bilgisayar    Raif
    1     Yazılım  Volkan
    2       Kimya    Asım
    


```python
departments = pd.merge(school, department_heads)

print(departments)
```

         name  department  year    head
    0  Furkan  Bilgisayar  2023    Raif
    1   Özlem       Kimya  2023    Asım
    2  Kardem     Yazılım  2024  Volkan
    3    Doga     Yazılım  2021  Volkan
    


```python
department_skills = {
    "department" : ["Bilgisayar", "Bilgisayar", "Kimya", "Yazılım", "Yazılım"],
    "skills" : ["Kodlama", "Linux", "Çözelti hazırlama", "Kodlama", "Database"]
}

skills = pd.DataFrame(department_skills)

print(skills)
```

       department             skills
    0  Bilgisayar            Kodlama
    1  Bilgisayar              Linux
    2       Kimya  Çözelti hazırlama
    3     Yazılım            Kodlama
    4     Yazılım           Database
    


```python
print(pd.merge(departments, skills))
```

         name  department  year    head             skills
    0  Furkan  Bilgisayar  2023    Raif            Kodlama
    1  Furkan  Bilgisayar  2023    Raif              Linux
    2   Özlem       Kimya  2023    Asım  Çözelti hazırlama
    3  Kardem     Yazılım  2024  Volkan            Kodlama
    4  Kardem     Yazılım  2024  Volkan           Database
    5    Doga     Yazılım  2021  Volkan            Kodlama
    6    Doga     Yazılım  2021  Volkan           Database
    

*Burada department_skills tablosunda olan bölümün yetenekleri belirtilmiştir. Bu tablo ile departments tablosundaki verileri birleştirme işlemi uyguladık. Son çıkan tablomuzda bir departman birden fazla yeteneğe sahip olabileceğinden bir kişiden iki tane görüyoruz.*

### **Toplulaştırma (Aggregation)**

*   count()
*   first()
*   last()
*   mean()
*   meadian()
*   min()
*   max()
*   std()
*   var()
*   sum()


```python
import seaborn as sns
```

*seaborn kütüphanesi içindeki hazır verisetlerini kullanacağız.*


```python
df = sns.load_dataset("planets")
print(df.head())
```

                method  number  orbital_period   mass  distance  year
    0  Radial Velocity       1         269.300   7.10     77.40  2006
    1  Radial Velocity       1         874.774   2.21     56.95  2008
    2  Radial Velocity       1         763.000   2.60     19.84  2011
    3  Radial Velocity       1         326.030  19.40    110.62  2007
    4  Radial Velocity       1         516.220  10.50    119.47  2009
    

*seaborn kütüphanesindeki "planets" verisetini değişkenimize atıyoruz ve ekrana bastırıyoruz.*


```python
print(df.shape)
```

    (1035, 6)
    

*Yüklediğimiz datasetinde 1035 satır ve 6 sütun var olduğunu gözlemledik.*


```python
print(df.count())
```

    method            1035
    number            1035
    orbital_period     992
    mass               513
    distance           808
    year              1035
    dtype: int64
    

*Her bir sütündan kaç tane olduğunu belirten count methodunu kullandık.*


```python
print(df.mean())
```

    number               1.785507
    orbital_period    2002.917596
    mass                 2.638161
    distance           264.069282
    year              2009.070531
    dtype: float64
    

    /usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      """Entry point for launching an IPython kernel.
    

*Her bir sütunun ortalamasını belirten mean methodunu kullandık.*

Eğer tek bir sütunun ortalamasını almak istersek;


```python
print(df["number"].mean())
```

    1.7855072463768116
    

*Burada ise sadece number sütununun ortalamasını aldık.*


```python
print(df.describe())
```

                number  orbital_period        mass     distance         year
    count  1035.000000      992.000000  513.000000   808.000000  1035.000000
    mean      1.785507     2002.917596    2.638161   264.069282  2009.070531
    std       1.240976    26014.728304    3.818617   733.116493     3.972567
    min       1.000000        0.090706    0.003600     1.350000  1989.000000
    25%       1.000000        5.442540    0.229000    32.560000  2007.000000
    50%       1.000000       39.979500    1.260000    55.250000  2010.000000
    75%       2.000000      526.005000    3.040000   178.500000  2012.000000
    max       7.000000   730000.000000   25.000000  8500.000000  2014.000000
    

Burada count, mean, std, min, 25%, 50%, 75% ve max methodlarını her bir sütun için uygulanmış tabloyu görüyoruz.


```python
print(df.describe().T)
```

                     count         mean           std          min         25%  \
    number          1035.0     1.785507      1.240976     1.000000     1.00000   
    orbital_period   992.0  2002.917596  26014.728304     0.090706     5.44254   
    mass             513.0     2.638161      3.818617     0.003600     0.22900   
    distance         808.0   264.069282    733.116493     1.350000    32.56000   
    year            1035.0  2009.070531      3.972567  1989.000000  2007.00000   
    
                          50%       75%       max  
    number             1.0000     2.000       7.0  
    orbital_period    39.9795   526.005  730000.0  
    mass               1.2600     3.040      25.0  
    distance          55.2500   178.500    8500.0  
    year            2010.0000  2012.000    2014.0  
    

*Okunabilirliği arttırmak adına describe methodunun transpozunu aldık.*


```python
print(df.dropna())
```

                  method  number  orbital_period    mass  distance  year
    0    Radial Velocity       1       269.30000   7.100     77.40  2006
    1    Radial Velocity       1       874.77400   2.210     56.95  2008
    2    Radial Velocity       1       763.00000   2.600     19.84  2011
    3    Radial Velocity       1       326.03000  19.400    110.62  2007
    4    Radial Velocity       1       516.22000  10.500    119.47  2009
    ..               ...     ...             ...     ...       ...   ...
    640  Radial Velocity       1       111.70000   2.100     14.90  2009
    641  Radial Velocity       1         5.05050   1.068     44.46  2013
    642  Radial Velocity       1       311.28800   1.940     17.24  1999
    649          Transit       1         2.70339   1.470    178.00  2013
    784  Radial Velocity       3       580.00000   0.947    135.00  2012
    
    [498 rows x 6 columns]
    

*Burada verisetimizde var olan verilerden eksik olanları çıkarttık ve ortaya 784 sütun çıktı.*

Toplulaştırma başlığı altında verilen methodları kendiniz kullanabilirsiniz. 


### **Gruplama (groupby)**


```python
data = {
    "Class" : ["a", "b", "c", "a", "b", "c"],
    "student exam result" : [20, 13, 32, 40, 32, 11]
}

df = pd.DataFrame(data, columns = ["Class", "student exam result"])
print(df)
```

      Class  student exam result
    0     a                   20
    1     b                   13
    2     c                   32
    3     a                   40
    4     b                   32
    5     c                   11
    

*Burada sınıflar ve sınıflardaki herhangi bir kişinin aldığı not belirtilmektedir. Herhangi bir sınıf için bakılmak istenirse groupby kullanılabilir.*


```python
print(df.groupby("Class").mean())
```

           student exam result
    Class                     
    a                     30.0
    b                     22.5
    c                     21.5
    

*Burada ise gruplanan sınıflara göre ortalama notu görmekteyiz.*


```python
print(df.groupby("Class").sum())
```

           student exam result
    Class                     
    a                       60
    b                       45
    c                       43
    

*Burada ise gruplanan sınıflardaki öğrencilerin toplam notlarını görmekteyiz.*

Toplulaştırmada kullanılan veriseti üzerinde gruplama;


```python
import seaborn as sns

df = sns.load_dataset("planets")
print(df)
```

                   method  number  orbital_period   mass  distance  year
    0     Radial Velocity       1      269.300000   7.10     77.40  2006
    1     Radial Velocity       1      874.774000   2.21     56.95  2008
    2     Radial Velocity       1      763.000000   2.60     19.84  2011
    3     Radial Velocity       1      326.030000  19.40    110.62  2007
    4     Radial Velocity       1      516.220000  10.50    119.47  2009
    ...               ...     ...             ...    ...       ...   ...
    1030          Transit       1        3.941507    NaN    172.00  2006
    1031          Transit       1        2.615864    NaN    148.00  2007
    1032          Transit       1        3.191524    NaN    174.00  2007
    1033          Transit       1        4.125083    NaN    293.00  2008
    1034          Transit       1        4.187757    NaN    260.00  2008
    
    [1035 rows x 6 columns]
    

*Burada method sütunu bir kategorik değişken olduğu için bu sütunu gruplayabiliriz.*


```python
print(df.groupby("method").describe())
```

                                  number                                           \
                                   count      mean       std  min  25%  50%   75%   
    method                                                                          
    Astrometry                       2.0  1.000000  0.000000  1.0  1.0  1.0  1.00   
    Eclipse Timing Variations        9.0  1.666667  0.500000  1.0  1.0  2.0  2.00   
    Imaging                         38.0  1.315789  0.933035  1.0  1.0  1.0  1.00   
    Microlensing                    23.0  1.173913  0.387553  1.0  1.0  1.0  1.00   
    Orbital Brightness Modulation    3.0  1.666667  0.577350  1.0  1.5  2.0  2.00   
    Pulsar Timing                    5.0  2.200000  1.095445  1.0  1.0  3.0  3.00   
    Pulsation Timing Variations      1.0  1.000000       NaN  1.0  1.0  1.0  1.00   
    Radial Velocity                553.0  1.721519  1.157141  1.0  1.0  1.0  2.00   
    Transit                        397.0  1.954660  1.399119  1.0  1.0  1.0  2.00   
    Transit Timing Variations        4.0  2.250000  0.500000  2.0  2.0  2.0  2.25   
    
                                       orbital_period                 ...  \
                                   max          count           mean  ...   
    method                                                            ...   
    Astrometry                     1.0            2.0     631.180000  ...   
    Eclipse Timing Variations      2.0            9.0    4751.644444  ...   
    Imaging                        4.0           12.0  118247.737500  ...   
    Microlensing                   2.0            7.0    3153.571429  ...   
    Orbital Brightness Modulation  2.0            3.0       0.709307  ...   
    Pulsar Timing                  3.0            5.0    7343.021201  ...   
    Pulsation Timing Variations    1.0            1.0    1170.000000  ...   
    Radial Velocity                6.0          553.0     823.354680  ...   
    Transit                        7.0          397.0      21.102073  ...   
    Transit Timing Variations      3.0            3.0      79.783500  ...   
    
                                    distance            year               \
                                         75%      max  count         mean   
    method                                                                  
    Astrometry                       19.3225    20.77    2.0  2011.500000   
    Eclipse Timing Variations       500.0000   500.00    9.0  2010.000000   
    Imaging                         132.6975   165.00   38.0  2009.131579   
    Microlensing                   4747.5000  7720.00   23.0  2009.782609   
    Orbital Brightness Modulation  1180.0000  1180.00    3.0  2011.666667   
    Pulsar Timing                  1200.0000  1200.00    5.0  1998.400000   
    Pulsation Timing Variations          NaN      NaN    1.0  2007.000000   
    Radial Velocity                  59.2175   354.00  553.0  2007.518987   
    Transit                         650.0000  8500.00  397.0  2011.236776   
    Transit Timing Variations      1487.0000  2119.00    4.0  2012.500000   
    
                                                                               \
                                        std     min      25%     50%      75%   
    method                                                                      
    Astrometry                     2.121320  2010.0  2010.75  2011.5  2012.25   
    Eclipse Timing Variations      1.414214  2008.0  2009.00  2010.0  2011.00   
    Imaging                        2.781901  2004.0  2008.00  2009.0  2011.00   
    Microlensing                   2.859697  2004.0  2008.00  2010.0  2012.00   
    Orbital Brightness Modulation  1.154701  2011.0  2011.00  2011.0  2012.00   
    Pulsar Timing                  8.384510  1992.0  1992.00  1994.0  2003.00   
    Pulsation Timing Variations         NaN  2007.0  2007.00  2007.0  2007.00   
    Radial Velocity                4.249052  1989.0  2005.00  2009.0  2011.00   
    Transit                        2.077867  2002.0  2010.00  2012.0  2013.00   
    Transit Timing Variations      1.290994  2011.0  2011.75  2012.5  2013.25   
    
                                           
                                      max  
    method                                 
    Astrometry                     2013.0  
    Eclipse Timing Variations      2012.0  
    Imaging                        2013.0  
    Microlensing                   2013.0  
    Orbital Brightness Modulation  2013.0  
    Pulsar Timing                  2011.0  
    Pulsation Timing Variations    2007.0  
    Radial Velocity                2014.0  
    Transit                        2014.0  
    Transit Timing Variations      2014.0  
    
    [10 rows x 40 columns]
    

*Burada her bir sütun için describe methodu çağırılıyor.*

Tek bir sütun için toplulaştırma;


```python
print(df.groupby("method")["number"].describe())
```

                                   count      mean       std  min  25%  50%   75%  \
    method                                                                          
    Astrometry                       2.0  1.000000  0.000000  1.0  1.0  1.0  1.00   
    Eclipse Timing Variations        9.0  1.666667  0.500000  1.0  1.0  2.0  2.00   
    Imaging                         38.0  1.315789  0.933035  1.0  1.0  1.0  1.00   
    Microlensing                    23.0  1.173913  0.387553  1.0  1.0  1.0  1.00   
    Orbital Brightness Modulation    3.0  1.666667  0.577350  1.0  1.5  2.0  2.00   
    Pulsar Timing                    5.0  2.200000  1.095445  1.0  1.0  3.0  3.00   
    Pulsation Timing Variations      1.0  1.000000       NaN  1.0  1.0  1.0  1.00   
    Radial Velocity                553.0  1.721519  1.157141  1.0  1.0  1.0  2.00   
    Transit                        397.0  1.954660  1.399119  1.0  1.0  1.0  2.00   
    Transit Timing Variations        4.0  2.250000  0.500000  2.0  2.0  2.0  2.25   
    
                                   max  
    method                              
    Astrometry                     1.0  
    Eclipse Timing Variations      2.0  
    Imaging                        4.0  
    Microlensing                   2.0  
    Orbital Brightness Modulation  2.0  
    Pulsar Timing                  3.0  
    Pulsation Timing Variations    1.0  
    Radial Velocity                6.0  
    Transit                        7.0  
    Transit Timing Variations      3.0  
    

*Burada method sütununu gruplaştırdık ve bu gruplaştırmadan sonra number sütününün describe methodunu çağırdık.*

### **İleri toplulaştırma işlemleri (aggregate, filter, transform, apply)**

*    Aggregate
*    filter
*    transform
*    apply

Kullanacağımız veriseti;


```python
import pandas as pd
import numpy as np

dictionary = {
    "class" : ["a", "b", "c", "a", "b", "c"],
    "students_id" : [35, 27, 15, 41, 80, 9],
    "exam_result" : [100, 20, 40, 50, 14, 90]
}

df = pd.DataFrame(dictionary)

print(df)
```

      class  students_id  exam_result
    0     a           35          100
    1     b           27           20
    2     c           15           40
    3     a           41           50
    4     b           80           14
    5     c            9           90
    

#### **Aggregate**


```python
print(df.groupby("class").aggregate(["min", np.median, "max"]))
```

          students_id            exam_result            
                  min median max         min median  max
    class                                               
    a              35   38.0  41          50   75.0  100
    b              27   53.5  80          14   17.0   20
    c               9   12.0  15          40   65.0   90
    

*Burada verisetimizi class sütununa göre grupladık ve sonrasında aggregate methodu ile bu gruplanan tablodan min, median ve max değerletini getirdik.*


```python
query = {
    "students_id" : np.median,
    "exam_result" : ["min", "max"] 
}

print(df.groupby("class").aggregate(query))
```

          students_id exam_result     
               median         min  max
    class                             
    a            38.0          50  100
    b            53.5          14   20
    c            12.0          40   90
    

*Burada farklı sütunlara farklı işlemler uyguladık. students_id sütununa median işlemini exam_result sütununa da min ve max işlemini uyguladık*

#### **Filter**

Kendi yazdığımız fonksiyonlarımızı DataFrame üzerinde filtrelemeye yarar.




```python
def filter_func(df):
  return df["exam_result"].std() > 9
```


```python
print(df.groupby("class").filter(filter_func))
```

      class  students_id  exam_result
    0     a           35          100
    2     c           15           40
    3     a           41           50
    5     c            9           90
    

*Burada class sütununa göre bir gruplama işlemi yaptık. Bu sütunlama işleminin ardından kendi yazdığımız fonksiyona göre filtreleme işlemi yaptık. Burada fonksiyonumuz exam_result tablosundaki standart sapması 9 dan büyük olanları geri döndürdü.*

#### **Transform**

Değişkenlerin hepsinde gezip istediğimiz fonksiyonu uygulayan method.


```python
change_df = df.iloc[:, 1:3]

print(change_df.transform(lambda value: value - value.mean()))
```

       students_id  exam_result
    0          0.5    47.666667
    1         -7.5   -32.333333
    2        -19.5   -12.333333
    3          6.5    -2.333333
    4         45.5   -38.333333
    5        -25.5    37.666667
    

*Burada class sütunu bir kategorik değişken olduğundan dolayı, biz bu sütunu almayıp yeni bir değişkene atıyoruz. Ardından değerlerden değerlerin ortalamasını çıkaran bir fonksiyon yazdık.*

#### **Apply**

DataFramedeki değişkenlerin üzerinde gezen ve toplulaştırma amacıyla kullanılan method.


```python
change_df = df.iloc[:, 1:3]

print(change_df)
```

       students_id  exam_result
    0           35          100
    1           27           20
    2           15           40
    3           41           50
    4           80           14
    5            9           90
    

*Burada class olan sütunumuzu almayıp students_id ve exam_result sütununu farklı bir değişkene atadık.*


```python
change_df.apply(np.sum)
```




    students_id    207
    exam_result    314
    dtype: int64



*Burada değerlerin üzerinde gezip students_id ve exam_result değerlerinin toplamını buldu.*
