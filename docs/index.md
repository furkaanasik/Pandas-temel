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

df
```





  <div id="df-0219a633-5edb-4149-b95f-a40da4dcc66d">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-0219a633-5edb-4149-b95f-a40da4dcc66d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-0219a633-5edb-4149-b95f-a40da4dcc66d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0219a633-5edb-4149-b95f-a40da4dcc66d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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

df
```

    Index(['column 1', 'column 2', 'column 3'], dtype='object')
    ------------------------------
    





  <div id="df-1cab80e1-8165-4528-a5af-3a0cbefc53d2">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sutün 1</th>
      <th>sütun 2</th>
      <th>sütun 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>20</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-1cab80e1-8165-4528-a5af-3a0cbefc53d2')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-1cab80e1-8165-4528-a5af-3a0cbefc53d2 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-1cab80e1-8165-4528-a5af-3a0cbefc53d2');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
    0     2     7
    1     8     3
    2     7     3
    3     1     9
    4     4     5
    ------------------------------
       pro1  pro2
    a     2     7
    b     8     3
    c     7     3
    d     1     9
    e     4     5
    

### **DataFrame indeks ile satırlara erişmek**


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

rows = df["a": "b"]

rows
```





  <div id="df-3679fcba-ce44-4bef-ae15-7c3b99f48f2b">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>column 1</th>
      <th>column 2</th>
      <th>column 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>10</td>
      <td>20</td>
      <td>30</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3679fcba-ce44-4bef-ae15-7c3b99f48f2b')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-3679fcba-ce44-4bef-ae15-7c3b99f48f2b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-3679fcba-ce44-4bef-ae15-7c3b99f48f2b');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
locate
```

        a   b   c   d   e
    0  43  71  40  18  80
    1  90  92  63  19  66
    2  14  83  36  43  45
    3  77  24  69  95  37
    4  96  98  61  28  12
    5  72  35  20  87  93
    6  29  40  85  12  99
    7  67  67  13  92  35
    8  76  97  31  54  27
    9  83  32  76  24  88
    ------------------------------
    





  <div id="df-bbdd379b-34cb-490c-a543-83535bcc85b5">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>92</td>
      <td>63</td>
      <td>19</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14</td>
      <td>83</td>
      <td>36</td>
      <td>43</td>
      <td>45</td>
    </tr>
    <tr>
      <th>3</th>
      <td>77</td>
      <td>24</td>
      <td>69</td>
      <td>95</td>
      <td>37</td>
    </tr>
    <tr>
      <th>4</th>
      <td>96</td>
      <td>98</td>
      <td>61</td>
      <td>28</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5</th>
      <td>72</td>
      <td>35</td>
      <td>20</td>
      <td>87</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-bbdd379b-34cb-490c-a543-83535bcc85b5')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-bbdd379b-34cb-490c-a543-83535bcc85b5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-bbdd379b-34cb-490c-a543-83535bcc85b5');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada oluşturmuş olduğumuz 10 satırlı bir DataFrame içerisindeki 1. elemandan ve 5. elemana (dahil) kadar bir veri seçme işlemi gerçekleştirdik.*

#### **iloc**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

print(df)
print("-" * 30)

locate = df.iloc[1:5]

locate
```

        a   b   c   d   e
    0  20  69  97   7  43
    1  80   9   1  24  27
    2  24   4  41  78  89
    3  69  89  46  61   9
    4  81  36   2  81  73
    5   3  74  14  65  67
    6  41   9  73  69  13
    7  77  40  21  64  85
    8  26  39  93  32  65
    9  93  93  70  81  39
    ------------------------------
    





  <div id="df-d25eb34e-9786-48ce-8769-0a95e3fd9480">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>9</td>
      <td>1</td>
      <td>24</td>
      <td>27</td>
    </tr>
    <tr>
      <th>2</th>
      <td>24</td>
      <td>4</td>
      <td>41</td>
      <td>78</td>
      <td>89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>69</td>
      <td>89</td>
      <td>46</td>
      <td>61</td>
      <td>9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>81</td>
      <td>36</td>
      <td>2</td>
      <td>81</td>
      <td>73</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d25eb34e-9786-48ce-8769-0a95e3fd9480')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d25eb34e-9786-48ce-8769-0a95e3fd9480 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d25eb34e-9786-48ce-8769-0a95e3fd9480');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
    0  51  99  17  55  27
    1  73  15  82  89  84
    2  37  46  43  23  72
    3  28  34  77  74  75
    4  31  12  90  88  84
    ------------------------------
    loc ile veriye erişmek
        a   b   c   d   e
    1  73  15  82  89  84
    2  37  46  43  23  72
    3  28  34  77  74  75
    ------------------------------
    iloc ile veriye erişmek
        a   b   c   d   e
    1  73  15  82  89  84
    2  37  46  43  23  72
    ------------------------------
    

*Burada gördüğünüz üzere loc ve iloc aralığını aynı verdiğimizde, loc son aralık değerini dahil etti fakat iloc dahil etmedi.*

#### **Satır ve sütun veri seçme işlemi**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

locate = df.iloc[0:3, 0:2]
locate
```





  <div id="df-19c27e34-9206-4372-bf7d-4f74fdc9c852">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>84</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>84</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>52</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-19c27e34-9206-4372-bf7d-4f74fdc9c852')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-19c27e34-9206-4372-bf7d-4f74fdc9c852 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-19c27e34-9206-4372-bf7d-4f74fdc9c852');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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

    0    11
    1    44
    2    22
    3    65
    Name: a, dtype: int64
    

**Burada direkt bir sütunun değerini veya satırın değerini verdiğimiz için loc ifadesi ile veri seçme işlemimizi gerçekleştirmiş olduk**

####**iloc ile sütun seçme işlemi**


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

locate = df.iloc[0:3]["a"]

locate
```




    0    50
    1    58
    2     5
    Name: a, dtype: int64



*Burada iloc ile sütun seçme işlemi yaptık burada satır olarak 0'dan 3'e kadar olan satırları seçtik ve bu satırladın da sahip olduğu a sütununu aldık.*

Birden fazla sütun seçmek istersek fancy kullanabiliriz. Örneğin;


```python
import numpy as np

random_arr = np.random.randint(1, 100, size = (5, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

locate = df.iloc[0:3][["a", "d", "e"]]

locate
```





  <div id="df-15c09f6f-581f-4042-a1c5-05d952c94bee">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>14</td>
      <td>88</td>
    </tr>
    <tr>
      <th>1</th>
      <td>54</td>
      <td>90</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>87</td>
      <td>79</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-15c09f6f-581f-4042-a1c5-05d952c94bee')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-15c09f6f-581f-4042-a1c5-05d952c94bee button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-15c09f6f-581f-4042-a1c5-05d952c94bee');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada fancy yardımıyla birden fazla sütun seçme işlemini yapabildik.*

#### **Koşullu eleman seçme işlemi**



```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

df[df.a > 15]
```





  <div id="df-785a701c-acf5-4619-b497-b6da05787983">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>29</td>
      <td>3</td>
      <td>24</td>
      <td>22</td>
      <td>13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>18</td>
      <td>4</td>
      <td>1</td>
      <td>22</td>
      <td>19</td>
    </tr>
    <tr>
      <th>8</th>
      <td>27</td>
      <td>18</td>
      <td>19</td>
      <td>26</td>
      <td>8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>17</td>
      <td>3</td>
      <td>28</td>
      <td>13</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-785a701c-acf5-4619-b497-b6da05787983')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-785a701c-acf5-4619-b497-b6da05787983 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-785a701c-acf5-4619-b497-b6da05787983');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada a sütunundaki değerlerin 15'den büyük olma koşulunu verdik. DataFrame içerisindeki sütuna erişmek için df.a ifadesini kullandık.*

Birden fazla koşul girmek;


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (10, 5))
df = pd.DataFrame(random_arr, columns=["a", "b", "c", "d", "e"])

df[(df.a > 15) & (df.d > 5)]
```





  <div id="df-54422a65-67cc-4b15-aff7-f62eceeee362">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>22</td>
      <td>5</td>
      <td>27</td>
      <td>27</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>21</td>
      <td>24</td>
      <td>26</td>
      <td>20</td>
      <td>15</td>
    </tr>
    <tr>
      <th>8</th>
      <td>21</td>
      <td>12</td>
      <td>2</td>
      <td>6</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-54422a65-67cc-4b15-aff7-f62eceeee362')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-54422a65-67cc-4b15-aff7-f62eceeee362 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-54422a65-67cc-4b15-aff7-f62eceeee362');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada a sütunundaki değerlerin 15'den büyük olduğu ve d sütunundaki değerlerin 5'den büyük olduğu değerleri aldık.*

### DataFrame sütunları değiştirmek

DataFrame içerisindeki sütunları değiştirmek istersek columns kullanabiliriz.


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (5, 3))
df = pd.DataFrame(random_arr, columns=["a", "b", "c"])

df.columns = ["A", "B", "C"]

df
```





  <div id="df-d92c25da-e3f4-4d0a-8590-60e63422a804">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24</td>
      <td>11</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13</td>
      <td>26</td>
      <td>29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>14</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>20</td>
      <td>17</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>20</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d92c25da-e3f4-4d0a-8590-60e63422a804')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d92c25da-e3f4-4d0a-8590-60e63422a804 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d92c25da-e3f4-4d0a-8590-60e63422a804');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
    0  18  13  21
    1  28  13   1
    2  15  26  19
    3   6  22  17
    4   6  23  28
    ------------------------------
    Oluşturulan ikinci DataFrame
        a   b   c
    0  36  26  42
    1  56  26   2
    2  30  52  38
    3  12  44  34
    4  12  46  56
    ------------------------------
    df1 ve df2 DataFrame birleştirme işlemi
        a   b   c
    0  18  13  21
    1  28  13   1
    2  15  26  19
    3   6  22  17
    4   6  23  28
    0  36  26  42
    1  56  26   2
    2  30  52  38
    3  12  44  34
    4  12  46  56
    

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
    0  20   1  13
    1  11   8  29
    2   7  28  26
    3   5  12   7
    4  24  13  28
    ------------------------------
    Oluşturulan ikinci DataFrame
        a   b   c
    0  40   2  26
    1  22  16  58
    2  14  56  52
    3  10  24  14
    4  48  26  56
    ------------------------------
    df1 ve df2 DataFrame birleştirme işlemi
        a   b   c
    0  20   1  13
    1  11   8  29
    2   7  28  26
    3   5  12   7
    4  24  13  28
    5  40   2  26
    6  22  16  58
    7  14  56  52
    8  10  24  14
    9  48  26  56
    

*Burada concat methodunun içerisine ignore_index parametresine True atadığımızda indeks problemimiz ortadan kalktı.*

#### **Farklı sütünlara sahip olan DataFrame birleştirme işlemi**


```python
import numpy as np

random_arr = np.random.randint(1, 30, size = (5, 3))
df1 = pd.DataFrame(random_arr, columns=["a", "b", "c"])
random_arr = np.random.randint(1,30, size = (5,3))
df2 = pd.DataFrame(random_arr, columns=["Column 1", "Column 2", "c"])

pd.concat([df1, df2],  ignore_index=True)
```





  <div id="df-4268ecfe-eb12-467d-9e45-d816cabc7ce0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>Column 1</th>
      <th>Column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>23.0</td>
      <td>2.0</td>
      <td>29</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>3.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>29.0</td>
      <td>9.0</td>
      <td>19</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10.0</td>
      <td>1.0</td>
      <td>21</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6.0</td>
      <td>14.0</td>
      <td>27</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>13</td>
      <td>14.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>6</td>
      <td>1.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>25</td>
      <td>9.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>23</td>
      <td>3.0</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>6</td>
      <td>28.0</td>
      <td>17.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-4268ecfe-eb12-467d-9e45-d816cabc7ce0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-4268ecfe-eb12-467d-9e45-d816cabc7ce0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4268ecfe-eb12-467d-9e45-d816cabc7ce0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada görülen NaN ifadeleri birinci DataFrame ile ikinci DataFrame eşleşmediğinden ortaya çıkmıştır. Görüldüğü gibi sütun c iki DataFramede eşleştiği için otomatik c ifadesinin bulunduğu sütuna yazılmıştır.*


```python
pd.concat([df1, df2], join="inner", ignore_index=True)
```





  <div id="df-75077d07-cfa6-4c56-8e90-debda57a614c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
    </tr>
    <tr>
      <th>5</th>
      <td>13</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>23</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-75077d07-cfa6-4c56-8e90-debda57a614c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-75077d07-cfa6-4c56-8e90-debda57a614c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-75077d07-cfa6-4c56-8e90-debda57a614c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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

student_department
```





  <div id="df-7c5fd56c-7399-4b9c-9eb6-ea2c2b49f054">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>Kimya</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>Yazılım</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>Yazılım</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7c5fd56c-7399-4b9c-9eb6-ea2c2b49f054')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7c5fd56c-7399-4b9c-9eb6-ea2c2b49f054 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7c5fd56c-7399-4b9c-9eb6-ea2c2b49f054');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
graduation = {
    "name" : ["Furkan", "Özlem", "Kardem", "Doga"],
    "year" : ["2023", "2023", "2024", "2021"]
}

graduation_year = pd.DataFrame(graduation)

graduation_year
```





  <div id="df-bb92cd4b-0f44-4b75-b160-a1665dab9013">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-bb92cd4b-0f44-4b75-b160-a1665dab9013')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-bb92cd4b-0f44-4b75-b160-a1665dab9013 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-bb92cd4b-0f44-4b75-b160-a1665dab9013');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
pd.merge(student_department, graduation_year)
```





  <div id="df-11757725-12fd-4952-a7fd-61f499bab3b5">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>Kimya</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-11757725-12fd-4952-a7fd-61f499bab3b5')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-11757725-12fd-4952-a7fd-61f499bab3b5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-11757725-12fd-4952-a7fd-61f499bab3b5');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
school
```





  <div id="df-092af27e-666d-4d3f-8522-8950423ddd68">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>Kimya</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-092af27e-666d-4d3f-8522-8950423ddd68')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-092af27e-666d-4d3f-8522-8950423ddd68 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-092af27e-666d-4d3f-8522-8950423ddd68');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
department = {
    "department" : ["Bilgisayar", "Yazılım", "Kimya"],
    "head" : ["Raif", "Volkan", "Asım"]
}

department_heads = pd.DataFrame(department)

department_heads
```





  <div id="df-fd6fc44f-2684-4186-9fe1-70255bf214a0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>department</th>
      <th>head</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bilgisayar</td>
      <td>Raif</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yazılım</td>
      <td>Volkan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kimya</td>
      <td>Asım</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fd6fc44f-2684-4186-9fe1-70255bf214a0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-fd6fc44f-2684-4186-9fe1-70255bf214a0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fd6fc44f-2684-4186-9fe1-70255bf214a0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
pd.merge(school, department_heads)
```





  <div id="df-ef526d9b-e6e0-4e8f-84b7-9b36f1213005">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
      <th>year</th>
      <th>head</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
      <td>Raif</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>Kimya</td>
      <td>2023</td>
      <td>Asım</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
      <td>Volkan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
      <td>Volkan</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ef526d9b-e6e0-4e8f-84b7-9b36f1213005')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ef526d9b-e6e0-4e8f-84b7-9b36f1213005 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ef526d9b-e6e0-4e8f-84b7-9b36f1213005');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
school
```





  <div id="df-8477287a-1ea3-4972-a24f-124e63963c5c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>Kimya</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-8477287a-1ea3-4972-a24f-124e63963c5c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-8477287a-1ea3-4972-a24f-124e63963c5c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-8477287a-1ea3-4972-a24f-124e63963c5c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
department = {
    "department" : ["Bilgisayar", "Yazılım", "Kimya"],
    "head" : ["Raif", "Volkan", "Asım"]
}

department_heads = pd.DataFrame(department)

department_heads
```





  <div id="df-222ea7aa-5517-4055-aeff-d9f72a95f145">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>department</th>
      <th>head</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bilgisayar</td>
      <td>Raif</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yazılım</td>
      <td>Volkan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kimya</td>
      <td>Asım</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-222ea7aa-5517-4055-aeff-d9f72a95f145')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-222ea7aa-5517-4055-aeff-d9f72a95f145 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-222ea7aa-5517-4055-aeff-d9f72a95f145');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
departments = pd.merge(school, department_heads)

departments
```





  <div id="df-75f125f7-cadf-4b5e-af30-0910e958d2ec">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
      <th>year</th>
      <th>head</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
      <td>Raif</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Özlem</td>
      <td>Kimya</td>
      <td>2023</td>
      <td>Asım</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
      <td>Volkan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
      <td>Volkan</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-75f125f7-cadf-4b5e-af30-0910e958d2ec')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-75f125f7-cadf-4b5e-af30-0910e958d2ec button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-75f125f7-cadf-4b5e-af30-0910e958d2ec');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
department_skills = {
    "department" : ["Bilgisayar", "Bilgisayar", "Kimya", "Yazılım", "Yazılım"],
    "skills" : ["Kodlama", "Linux", "Çözelti hazırlama", "Kodlama", "Database"]
}

skills = pd.DataFrame(department_skills)

skills

```





  <div id="df-0d84694f-13a4-4710-9118-00ce19e91d03">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>department</th>
      <th>skills</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bilgisayar</td>
      <td>Kodlama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bilgisayar</td>
      <td>Linux</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kimya</td>
      <td>Çözelti hazırlama</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Yazılım</td>
      <td>Kodlama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Yazılım</td>
      <td>Database</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-0d84694f-13a4-4710-9118-00ce19e91d03')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-0d84694f-13a4-4710-9118-00ce19e91d03 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0d84694f-13a4-4710-9118-00ce19e91d03');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
pd.merge(departments, skills)
```





  <div id="df-0026bdb1-3c0f-480f-8e71-47dc489acf33">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>department</th>
      <th>year</th>
      <th>head</th>
      <th>skills</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
      <td>Raif</td>
      <td>Kodlama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Furkan</td>
      <td>Bilgisayar</td>
      <td>2023</td>
      <td>Raif</td>
      <td>Linux</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Özlem</td>
      <td>Kimya</td>
      <td>2023</td>
      <td>Asım</td>
      <td>Çözelti hazırlama</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
      <td>Volkan</td>
      <td>Kodlama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kardem</td>
      <td>Yazılım</td>
      <td>2024</td>
      <td>Volkan</td>
      <td>Database</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
      <td>Volkan</td>
      <td>Kodlama</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Doga</td>
      <td>Yazılım</td>
      <td>2021</td>
      <td>Volkan</td>
      <td>Database</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-0026bdb1-3c0f-480f-8e71-47dc489acf33')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-0026bdb1-3c0f-480f-8e71-47dc489acf33 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0026bdb1-3c0f-480f-8e71-47dc489acf33');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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
df.head()
```





  <div id="df-3b609f3c-0e42-4e4f-99b9-05a3c0e3dfb4">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>method</th>
      <th>number</th>
      <th>orbital_period</th>
      <th>mass</th>
      <th>distance</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>269.300</td>
      <td>7.10</td>
      <td>77.40</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>874.774</td>
      <td>2.21</td>
      <td>56.95</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>763.000</td>
      <td>2.60</td>
      <td>19.84</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>326.030</td>
      <td>19.40</td>
      <td>110.62</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>516.220</td>
      <td>10.50</td>
      <td>119.47</td>
      <td>2009</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3b609f3c-0e42-4e4f-99b9-05a3c0e3dfb4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-3b609f3c-0e42-4e4f-99b9-05a3c0e3dfb4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-3b609f3c-0e42-4e4f-99b9-05a3c0e3dfb4');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*seaborn kütüphanesindeki "planets" verisetini değişkenimize atıyoruz ve ekrana bastırıyoruz.*


```python
df.shape
```




    (1035, 6)



*Yüklediğimiz datasetinde 1035 satır ve 6 sütun var olduğunu gözlemledik.*


```python
df.count()
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
df.mean()
```

    /usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.
      """Entry point for launching an IPython kernel.
    




    number               1.785507
    orbital_period    2002.917596
    mass                 2.638161
    distance           264.069282
    year              2009.070531
    dtype: float64



*Her bir sütunun ortalamasını belirten mean methodunu kullandık.*

Eğer tek bir sütunun ortalamasını almak istersek;


```python
df["number"].mean()
```




    1.7855072463768116



*Burada ise sadece number sütununun ortalamasını aldık.*


```python
df.describe()
```





  <div id="df-b626fb95-a82d-4a25-a1a6-5c29a6e9f9a0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>number</th>
      <th>orbital_period</th>
      <th>mass</th>
      <th>distance</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1035.000000</td>
      <td>992.000000</td>
      <td>513.000000</td>
      <td>808.000000</td>
      <td>1035.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.785507</td>
      <td>2002.917596</td>
      <td>2.638161</td>
      <td>264.069282</td>
      <td>2009.070531</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.240976</td>
      <td>26014.728304</td>
      <td>3.818617</td>
      <td>733.116493</td>
      <td>3.972567</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>0.090706</td>
      <td>0.003600</td>
      <td>1.350000</td>
      <td>1989.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
      <td>5.442540</td>
      <td>0.229000</td>
      <td>32.560000</td>
      <td>2007.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
      <td>39.979500</td>
      <td>1.260000</td>
      <td>55.250000</td>
      <td>2010.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.000000</td>
      <td>526.005000</td>
      <td>3.040000</td>
      <td>178.500000</td>
      <td>2012.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>7.000000</td>
      <td>730000.000000</td>
      <td>25.000000</td>
      <td>8500.000000</td>
      <td>2014.000000</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b626fb95-a82d-4a25-a1a6-5c29a6e9f9a0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b626fb95-a82d-4a25-a1a6-5c29a6e9f9a0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b626fb95-a82d-4a25-a1a6-5c29a6e9f9a0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




Burada count, mean, std, min, 25%, 50%, 75% ve max methodlarını her bir sütun için uygulanmış tabloyu görüyoruz.


```python
df.describe().T
```





  <div id="df-a9c66bc1-43fa-498c-8cde-c1fe3cc64b6a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>number</th>
      <td>1035.0</td>
      <td>1.785507</td>
      <td>1.240976</td>
      <td>1.000000</td>
      <td>1.00000</td>
      <td>1.0000</td>
      <td>2.000</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>orbital_period</th>
      <td>992.0</td>
      <td>2002.917596</td>
      <td>26014.728304</td>
      <td>0.090706</td>
      <td>5.44254</td>
      <td>39.9795</td>
      <td>526.005</td>
      <td>730000.0</td>
    </tr>
    <tr>
      <th>mass</th>
      <td>513.0</td>
      <td>2.638161</td>
      <td>3.818617</td>
      <td>0.003600</td>
      <td>0.22900</td>
      <td>1.2600</td>
      <td>3.040</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>distance</th>
      <td>808.0</td>
      <td>264.069282</td>
      <td>733.116493</td>
      <td>1.350000</td>
      <td>32.56000</td>
      <td>55.2500</td>
      <td>178.500</td>
      <td>8500.0</td>
    </tr>
    <tr>
      <th>year</th>
      <td>1035.0</td>
      <td>2009.070531</td>
      <td>3.972567</td>
      <td>1989.000000</td>
      <td>2007.00000</td>
      <td>2010.0000</td>
      <td>2012.000</td>
      <td>2014.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a9c66bc1-43fa-498c-8cde-c1fe3cc64b6a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a9c66bc1-43fa-498c-8cde-c1fe3cc64b6a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a9c66bc1-43fa-498c-8cde-c1fe3cc64b6a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Okunabilirliği arttırmak adına describe methodunun transpozunu aldık.*


```python
df.dropna()
```





  <div id="df-41686160-fcb7-4495-99be-22a3fc8088b0">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>method</th>
      <th>number</th>
      <th>orbital_period</th>
      <th>mass</th>
      <th>distance</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>269.30000</td>
      <td>7.100</td>
      <td>77.40</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>874.77400</td>
      <td>2.210</td>
      <td>56.95</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>763.00000</td>
      <td>2.600</td>
      <td>19.84</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>326.03000</td>
      <td>19.400</td>
      <td>110.62</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>516.22000</td>
      <td>10.500</td>
      <td>119.47</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>640</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>111.70000</td>
      <td>2.100</td>
      <td>14.90</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>641</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>5.05050</td>
      <td>1.068</td>
      <td>44.46</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>642</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>311.28800</td>
      <td>1.940</td>
      <td>17.24</td>
      <td>1999</td>
    </tr>
    <tr>
      <th>649</th>
      <td>Transit</td>
      <td>1</td>
      <td>2.70339</td>
      <td>1.470</td>
      <td>178.00</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>784</th>
      <td>Radial Velocity</td>
      <td>3</td>
      <td>580.00000</td>
      <td>0.947</td>
      <td>135.00</td>
      <td>2012</td>
    </tr>
  </tbody>
</table>
<p>498 rows × 6 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-41686160-fcb7-4495-99be-22a3fc8088b0')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-41686160-fcb7-4495-99be-22a3fc8088b0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-41686160-fcb7-4495-99be-22a3fc8088b0');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada verisetimizde var olan verilerden eksik olanları çıkarttık ve ortaya 784 sütun çıktı.*

Toplulaştırma başlığı altında verilen methodları kendiniz kullanabilirsiniz. 


### **Gruplama (groupby)**


```python
data = {
    "Class" : ["a", "b", "c", "a", "b", "c"],
    "student exam result" : [20, 13, 32, 40, 32, 11]
}

df = pd.DataFrame(data, columns = ["Class", "student exam result"])
df
```





  <div id="df-a952a3b1-ab2d-4d50-8678-02ccf3421b02">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Class</th>
      <th>student exam result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>32</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>32</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a952a3b1-ab2d-4d50-8678-02ccf3421b02')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a952a3b1-ab2d-4d50-8678-02ccf3421b02 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a952a3b1-ab2d-4d50-8678-02ccf3421b02');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada sınıflar ve sınıflardaki herhangi bir kişinin aldığı not belirtilmektedir. Herhangi bir sınıf için bakılmak istenirse groupby kullanılabilir.*


```python
df.groupby("Class").mean()
```





  <div id="df-8245822e-8536-443f-99c8-1edcef9e36a3">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student exam result</th>
    </tr>
    <tr>
      <th>Class</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>30.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>22.5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>21.5</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-8245822e-8536-443f-99c8-1edcef9e36a3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-8245822e-8536-443f-99c8-1edcef9e36a3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-8245822e-8536-443f-99c8-1edcef9e36a3');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada ise gruplanan sınıflara göre ortalama notu görmekteyiz.*


```python
df.groupby("Class").sum()
```





  <div id="df-413fe715-bf91-49c4-96a6-45d02ffe8ee5">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student exam result</th>
    </tr>
    <tr>
      <th>Class</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>60</td>
    </tr>
    <tr>
      <th>b</th>
      <td>45</td>
    </tr>
    <tr>
      <th>c</th>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-413fe715-bf91-49c4-96a6-45d02ffe8ee5')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-413fe715-bf91-49c4-96a6-45d02ffe8ee5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-413fe715-bf91-49c4-96a6-45d02ffe8ee5');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada ise gruplanan sınıflardaki öğrencilerin toplam notlarını görmekteyiz.*

Toplulaştırmada kullanılan veriseti üzerinde gruplama;


```python
import seaborn as sns

df = sns.load_dataset("planets")
df
```





  <div id="df-7fe1d062-6f6e-4737-ae28-24c96e196016">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>method</th>
      <th>number</th>
      <th>orbital_period</th>
      <th>mass</th>
      <th>distance</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>269.300000</td>
      <td>7.10</td>
      <td>77.40</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>874.774000</td>
      <td>2.21</td>
      <td>56.95</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>763.000000</td>
      <td>2.60</td>
      <td>19.84</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>326.030000</td>
      <td>19.40</td>
      <td>110.62</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Radial Velocity</td>
      <td>1</td>
      <td>516.220000</td>
      <td>10.50</td>
      <td>119.47</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1030</th>
      <td>Transit</td>
      <td>1</td>
      <td>3.941507</td>
      <td>NaN</td>
      <td>172.00</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>1031</th>
      <td>Transit</td>
      <td>1</td>
      <td>2.615864</td>
      <td>NaN</td>
      <td>148.00</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1032</th>
      <td>Transit</td>
      <td>1</td>
      <td>3.191524</td>
      <td>NaN</td>
      <td>174.00</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1033</th>
      <td>Transit</td>
      <td>1</td>
      <td>4.125083</td>
      <td>NaN</td>
      <td>293.00</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>1034</th>
      <td>Transit</td>
      <td>1</td>
      <td>4.187757</td>
      <td>NaN</td>
      <td>260.00</td>
      <td>2008</td>
    </tr>
  </tbody>
</table>
<p>1035 rows × 6 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7fe1d062-6f6e-4737-ae28-24c96e196016')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7fe1d062-6f6e-4737-ae28-24c96e196016 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7fe1d062-6f6e-4737-ae28-24c96e196016');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada method sütunu bir kategorik değişken olduğu için bu sütunu gruplayabiliriz.*


```python
df.groupby("method").describe()
```





  <div id="df-37ff8671-7e11-4106-bf18-dc83612274dd">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">number</th>
      <th colspan="2" halign="left">orbital_period</th>
      <th>...</th>
      <th colspan="2" halign="left">distance</th>
      <th colspan="8" halign="left">year</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>...</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>method</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Astrometry</th>
      <td>2.0</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>631.180000</td>
      <td>...</td>
      <td>19.3225</td>
      <td>20.77</td>
      <td>2.0</td>
      <td>2011.500000</td>
      <td>2.121320</td>
      <td>2010.0</td>
      <td>2010.75</td>
      <td>2011.5</td>
      <td>2012.25</td>
      <td>2013.0</td>
    </tr>
    <tr>
      <th>Eclipse Timing Variations</th>
      <td>9.0</td>
      <td>1.666667</td>
      <td>0.500000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.00</td>
      <td>2.0</td>
      <td>9.0</td>
      <td>4751.644444</td>
      <td>...</td>
      <td>500.0000</td>
      <td>500.00</td>
      <td>9.0</td>
      <td>2010.000000</td>
      <td>1.414214</td>
      <td>2008.0</td>
      <td>2009.00</td>
      <td>2010.0</td>
      <td>2011.00</td>
      <td>2012.0</td>
    </tr>
    <tr>
      <th>Imaging</th>
      <td>38.0</td>
      <td>1.315789</td>
      <td>0.933035</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>4.0</td>
      <td>12.0</td>
      <td>118247.737500</td>
      <td>...</td>
      <td>132.6975</td>
      <td>165.00</td>
      <td>38.0</td>
      <td>2009.131579</td>
      <td>2.781901</td>
      <td>2004.0</td>
      <td>2008.00</td>
      <td>2009.0</td>
      <td>2011.00</td>
      <td>2013.0</td>
    </tr>
    <tr>
      <th>Microlensing</th>
      <td>23.0</td>
      <td>1.173913</td>
      <td>0.387553</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>2.0</td>
      <td>7.0</td>
      <td>3153.571429</td>
      <td>...</td>
      <td>4747.5000</td>
      <td>7720.00</td>
      <td>23.0</td>
      <td>2009.782609</td>
      <td>2.859697</td>
      <td>2004.0</td>
      <td>2008.00</td>
      <td>2010.0</td>
      <td>2012.00</td>
      <td>2013.0</td>
    </tr>
    <tr>
      <th>Orbital Brightness Modulation</th>
      <td>3.0</td>
      <td>1.666667</td>
      <td>0.577350</td>
      <td>1.0</td>
      <td>1.5</td>
      <td>2.0</td>
      <td>2.00</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>0.709307</td>
      <td>...</td>
      <td>1180.0000</td>
      <td>1180.00</td>
      <td>3.0</td>
      <td>2011.666667</td>
      <td>1.154701</td>
      <td>2011.0</td>
      <td>2011.00</td>
      <td>2011.0</td>
      <td>2012.00</td>
      <td>2013.0</td>
    </tr>
    <tr>
      <th>Pulsar Timing</th>
      <td>5.0</td>
      <td>2.200000</td>
      <td>1.095445</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.00</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>7343.021201</td>
      <td>...</td>
      <td>1200.0000</td>
      <td>1200.00</td>
      <td>5.0</td>
      <td>1998.400000</td>
      <td>8.384510</td>
      <td>1992.0</td>
      <td>1992.00</td>
      <td>1994.0</td>
      <td>2003.00</td>
      <td>2011.0</td>
    </tr>
    <tr>
      <th>Pulsation Timing Variations</th>
      <td>1.0</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1170.000000</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>2007.000000</td>
      <td>NaN</td>
      <td>2007.0</td>
      <td>2007.00</td>
      <td>2007.0</td>
      <td>2007.00</td>
      <td>2007.0</td>
    </tr>
    <tr>
      <th>Radial Velocity</th>
      <td>553.0</td>
      <td>1.721519</td>
      <td>1.157141</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.00</td>
      <td>6.0</td>
      <td>553.0</td>
      <td>823.354680</td>
      <td>...</td>
      <td>59.2175</td>
      <td>354.00</td>
      <td>553.0</td>
      <td>2007.518987</td>
      <td>4.249052</td>
      <td>1989.0</td>
      <td>2005.00</td>
      <td>2009.0</td>
      <td>2011.00</td>
      <td>2014.0</td>
    </tr>
    <tr>
      <th>Transit</th>
      <td>397.0</td>
      <td>1.954660</td>
      <td>1.399119</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.00</td>
      <td>7.0</td>
      <td>397.0</td>
      <td>21.102073</td>
      <td>...</td>
      <td>650.0000</td>
      <td>8500.00</td>
      <td>397.0</td>
      <td>2011.236776</td>
      <td>2.077867</td>
      <td>2002.0</td>
      <td>2010.00</td>
      <td>2012.0</td>
      <td>2013.00</td>
      <td>2014.0</td>
    </tr>
    <tr>
      <th>Transit Timing Variations</th>
      <td>4.0</td>
      <td>2.250000</td>
      <td>0.500000</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.25</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>79.783500</td>
      <td>...</td>
      <td>1487.0000</td>
      <td>2119.00</td>
      <td>4.0</td>
      <td>2012.500000</td>
      <td>1.290994</td>
      <td>2011.0</td>
      <td>2011.75</td>
      <td>2012.5</td>
      <td>2013.25</td>
      <td>2014.0</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 40 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-37ff8671-7e11-4106-bf18-dc83612274dd')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-37ff8671-7e11-4106-bf18-dc83612274dd button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-37ff8671-7e11-4106-bf18-dc83612274dd');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada her bir sütun için describe methodu çağırılıyor.*

Tek bir sütun için toplulaştırma;


```python
df.groupby("method")["number"].describe()
```





  <div id="df-010442d3-a068-4856-9956-9e8026e43df1">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>method</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Astrometry</th>
      <td>2.0</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Eclipse Timing Variations</th>
      <td>9.0</td>
      <td>1.666667</td>
      <td>0.500000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.00</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Imaging</th>
      <td>38.0</td>
      <td>1.315789</td>
      <td>0.933035</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>Microlensing</th>
      <td>23.0</td>
      <td>1.173913</td>
      <td>0.387553</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Orbital Brightness Modulation</th>
      <td>3.0</td>
      <td>1.666667</td>
      <td>0.577350</td>
      <td>1.0</td>
      <td>1.5</td>
      <td>2.0</td>
      <td>2.00</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Pulsar Timing</th>
      <td>5.0</td>
      <td>2.200000</td>
      <td>1.095445</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.00</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>Pulsation Timing Variations</th>
      <td>1.0</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.00</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Radial Velocity</th>
      <td>553.0</td>
      <td>1.721519</td>
      <td>1.157141</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.00</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>Transit</th>
      <td>397.0</td>
      <td>1.954660</td>
      <td>1.399119</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.00</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>Transit Timing Variations</th>
      <td>4.0</td>
      <td>2.250000</td>
      <td>0.500000</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.25</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-010442d3-a068-4856-9956-9e8026e43df1')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-010442d3-a068-4856-9956-9e8026e43df1 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-010442d3-a068-4856-9956-9e8026e43df1');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




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

df
```





  <div id="df-f7aec2c8-ba2e-4aaa-b0c7-1789bfefd55c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>class</th>
      <th>students_id</th>
      <th>exam_result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>35</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>27</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>15</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>41</td>
      <td>50</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>80</td>
      <td>14</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c</td>
      <td>9</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-f7aec2c8-ba2e-4aaa-b0c7-1789bfefd55c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-f7aec2c8-ba2e-4aaa-b0c7-1789bfefd55c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f7aec2c8-ba2e-4aaa-b0c7-1789bfefd55c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




#### **Aggregate**


```python
df.groupby("class").aggregate(["min", np.median, "max"])
```





  <div id="df-5bc9ef7a-131e-418f-9f7f-ad6ce3e45613">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">students_id</th>
      <th colspan="3" halign="left">exam_result</th>
    </tr>
    <tr>
      <th></th>
      <th>min</th>
      <th>median</th>
      <th>max</th>
      <th>min</th>
      <th>median</th>
      <th>max</th>
    </tr>
    <tr>
      <th>class</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>35</td>
      <td>38.0</td>
      <td>41</td>
      <td>50</td>
      <td>75.0</td>
      <td>100</td>
    </tr>
    <tr>
      <th>b</th>
      <td>27</td>
      <td>53.5</td>
      <td>80</td>
      <td>14</td>
      <td>17.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>c</th>
      <td>9</td>
      <td>12.0</td>
      <td>15</td>
      <td>40</td>
      <td>65.0</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5bc9ef7a-131e-418f-9f7f-ad6ce3e45613')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-5bc9ef7a-131e-418f-9f7f-ad6ce3e45613 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5bc9ef7a-131e-418f-9f7f-ad6ce3e45613');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada verisetimizi class sütununa göre grupladık ve sonrasında aggregate methodu ile bu gruplanan tablodan min, median ve max değerletini getirdik.*


```python
query = {
    "students_id" : np.median,
    "exam_result" : ["min", "max"] 
}

df.groupby("class").aggregate(query)
```





  <div id="df-e5c08632-fc7d-4347-8680-fa333ea38009">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>students_id</th>
      <th colspan="2" halign="left">exam_result</th>
    </tr>
    <tr>
      <th></th>
      <th>median</th>
      <th>min</th>
      <th>max</th>
    </tr>
    <tr>
      <th>class</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>38.0</td>
      <td>50</td>
      <td>100</td>
    </tr>
    <tr>
      <th>b</th>
      <td>53.5</td>
      <td>14</td>
      <td>20</td>
    </tr>
    <tr>
      <th>c</th>
      <td>12.0</td>
      <td>40</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e5c08632-fc7d-4347-8680-fa333ea38009')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e5c08632-fc7d-4347-8680-fa333ea38009 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e5c08632-fc7d-4347-8680-fa333ea38009');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada farklı sütunlara farklı işlemler uyguladık. students_id sütununa median işlemini exam_result sütununa da min ve max işlemini uyguladık*

#### **Filter**

Kendi yazdığımız fonksiyonlarımızı DataFrame üzerinde filtrelemeye yarar.




```python
def filter_func(df):
  return df["exam_result"].std() > 9
```


```python
df.groupby("class").filter(filter_func)
```





  <div id="df-c9ce7c7c-6950-46ab-b9d4-da4bec995bed">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>class</th>
      <th>students_id</th>
      <th>exam_result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>35</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>15</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>41</td>
      <td>50</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c</td>
      <td>9</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c9ce7c7c-6950-46ab-b9d4-da4bec995bed')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-c9ce7c7c-6950-46ab-b9d4-da4bec995bed button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c9ce7c7c-6950-46ab-b9d4-da4bec995bed');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada class sütununa göre bir gruplama işlemi yaptık. Bu sütunlama işleminin ardından kendi yazdığımız fonksiyona göre filtreleme işlemi yaptık. Burada fonksiyonumuz exam_result tablosundaki standart sapması 9 dan büyük olanları geri döndürdü.*

#### **Transform**

Değişkenlerin hepsinde gezip istediğimiz fonksiyonu uygulayan method.


```python
change_df = df.iloc[:, 1:3]

change_df.transform(lambda value: value - value.mean())
```





  <div id="df-cfb28c00-980d-4e8a-83f8-5df753abf09f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>students_id</th>
      <th>exam_result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.5</td>
      <td>47.666667</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-7.5</td>
      <td>-32.333333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-19.5</td>
      <td>-12.333333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6.5</td>
      <td>-2.333333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45.5</td>
      <td>-38.333333</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-25.5</td>
      <td>37.666667</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-cfb28c00-980d-4e8a-83f8-5df753abf09f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-cfb28c00-980d-4e8a-83f8-5df753abf09f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-cfb28c00-980d-4e8a-83f8-5df753abf09f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada class sütunu bir kategorik değişken olduğundan dolayı, biz bu sütunu almayıp yeni bir değişkene atıyoruz. Ardından değerlerden değerlerin ortalamasını çıkaran bir fonksiyon yazdık.*

#### **Apply**

DataFramedeki değişkenlerin üzerinde gezen ve toplulaştırma amacıyla kullanılan method.


```python
change_df = df.iloc[:, 1:3]

change_df
```





  <div id="df-906f63c7-a167-496d-867a-1c55b1036e5f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>students_id</th>
      <th>exam_result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>35</td>
      <td>100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>27</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41</td>
      <td>50</td>
    </tr>
    <tr>
      <th>4</th>
      <td>80</td>
      <td>14</td>
    </tr>
    <tr>
      <th>5</th>
      <td>9</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-906f63c7-a167-496d-867a-1c55b1036e5f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-906f63c7-a167-496d-867a-1c55b1036e5f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-906f63c7-a167-496d-867a-1c55b1036e5f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




*Burada class olan sütunumuzu almayıp students_id ve exam_result sütununu farklı bir değişkene atadık.*


```python
change_df.apply(np.sum)
```




    students_id    207
    exam_result    314
    dtype: int64



*Burada değerlerin üzerinde gezip students_id ve exam_result değerlerinin toplamını buldu.*
