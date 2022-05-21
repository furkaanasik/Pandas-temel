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





  <div id="df-e7afef22-809a-495d-aaf6-e9fe37d3ce18">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-e7afef22-809a-495d-aaf6-e9fe37d3ce18')"
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
          document.querySelector('#df-e7afef22-809a-495d-aaf6-e9fe37d3ce18 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e7afef22-809a-495d-aaf6-e9fe37d3ce18');
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
    





  <div id="df-980f4b13-f4da-4498-9e34-74ad83c6bf72">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-980f4b13-f4da-4498-9e34-74ad83c6bf72')"
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
          document.querySelector('#df-980f4b13-f4da-4498-9e34-74ad83c6bf72 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-980f4b13-f4da-4498-9e34-74ad83c6bf72');
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
    0     0     2
    1     5     1
    2     9     7
    3     0     3
    4     9     2
    ------------------------------
       pro1  pro2
    a     0     2
    b     5     1
    c     9     7
    d     0     3
    e     9     2
    

### **DataFrame indeks ile satırlara erişmek**


```python
import numpy as np

arr = np.array([[10, 20, 30], [1, 2, 3], [40, 50, 60]])

df = pd.DataFrame(arr, columns=["column 1", "column 2", "column 3"], index = ["a", "b", "c"])

rows = df["a": "b"]

rows
```





  <div id="df-c3ab8193-945e-403c-b5b4-bd7c54af88da">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-c3ab8193-945e-403c-b5b4-bd7c54af88da')"
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
          document.querySelector('#df-c3ab8193-945e-403c-b5b4-bd7c54af88da button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c3ab8193-945e-403c-b5b4-bd7c54af88da');
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
    0  98   2  38  97  51
    1  28   6  27   8  20
    2  95  66   9  97  55
    3  19  20  44  99   2
    4  96  32  23  12  76
    5  53  70  46  54  14
    6   3  63  59  64   3
    7  48  19  58  75  68
    8  72  30  62  44  57
    9  11  45  29  97  83
    ------------------------------
    





  <div id="df-e0a40144-169c-4e2d-ab04-46ff06b97041">
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
      <td>28</td>
      <td>6</td>
      <td>27</td>
      <td>8</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>95</td>
      <td>66</td>
      <td>9</td>
      <td>97</td>
      <td>55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19</td>
      <td>20</td>
      <td>44</td>
      <td>99</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>96</td>
      <td>32</td>
      <td>23</td>
      <td>12</td>
      <td>76</td>
    </tr>
    <tr>
      <th>5</th>
      <td>53</td>
      <td>70</td>
      <td>46</td>
      <td>54</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e0a40144-169c-4e2d-ab04-46ff06b97041')"
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
          document.querySelector('#df-e0a40144-169c-4e2d-ab04-46ff06b97041 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e0a40144-169c-4e2d-ab04-46ff06b97041');
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
    0  52  45  97  12  77
    1  15  53   8  65  83
    2  54  74  57  72  21
    3  73  93  34  42  71
    4  77  21  15  58  92
    5  88  60   2  60  45
    6  47  94  10  97   5
    7  66  50   2   3   5
    8  40  31  85  76  76
    9   6  39  94  30  82
    ------------------------------
    





  <div id="df-b1167e19-02ec-4dbd-811d-d06805f817b5">
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
      <td>15</td>
      <td>53</td>
      <td>8</td>
      <td>65</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>54</td>
      <td>74</td>
      <td>57</td>
      <td>72</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>73</td>
      <td>93</td>
      <td>34</td>
      <td>42</td>
      <td>71</td>
    </tr>
    <tr>
      <th>4</th>
      <td>77</td>
      <td>21</td>
      <td>15</td>
      <td>58</td>
      <td>92</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b1167e19-02ec-4dbd-811d-d06805f817b5')"
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
          document.querySelector('#df-b1167e19-02ec-4dbd-811d-d06805f817b5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b1167e19-02ec-4dbd-811d-d06805f817b5');
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
    0  50  33  79  52  95
    1  58  24  34  43  23
    2  12   4  74  40  24
    3  90   3   8  15  75
    4  65  31  66  77  72
    ------------------------------
    loc ile veriye erişmek
        a   b   c   d   e
    1  58  24  34  43  23
    2  12   4  74  40  24
    3  90   3   8  15  75
    ------------------------------
    iloc ile veriye erişmek
        a   b   c   d   e
    1  58  24  34  43  23
    2  12   4  74  40  24
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





  <div id="df-b0153d37-5157-49b3-b3e1-9d9a0ab92279">
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
      <td>83</td>
      <td>69</td>
    </tr>
    <tr>
      <th>1</th>
      <td>69</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b0153d37-5157-49b3-b3e1-9d9a0ab92279')"
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
          document.querySelector('#df-b0153d37-5157-49b3-b3e1-9d9a0ab92279 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b0153d37-5157-49b3-b3e1-9d9a0ab92279');
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

    0    30
    1    87
    2     4
    3    94
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




    0    91
    1    55
    2    98
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





  <div id="df-b47a7ded-8e91-4c76-bbbe-634535920374">
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
      <td>27</td>
      <td>99</td>
      <td>82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>26</td>
      <td>5</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>85</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b47a7ded-8e91-4c76-bbbe-634535920374')"
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
          document.querySelector('#df-b47a7ded-8e91-4c76-bbbe-634535920374 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b47a7ded-8e91-4c76-bbbe-634535920374');
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





  <div id="df-e07a4f31-ddd8-4431-9119-969f3f572328">
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
      <th>0</th>
      <td>26</td>
      <td>3</td>
      <td>1</td>
      <td>13</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>24</td>
      <td>17</td>
      <td>13</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21</td>
      <td>14</td>
      <td>8</td>
      <td>27</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>17</td>
      <td>28</td>
      <td>26</td>
      <td>29</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>8</td>
      <td>25</td>
      <td>23</td>
      <td>29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>26</td>
      <td>21</td>
      <td>28</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e07a4f31-ddd8-4431-9119-969f3f572328')"
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
          document.querySelector('#df-e07a4f31-ddd8-4431-9119-969f3f572328 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e07a4f31-ddd8-4431-9119-969f3f572328');
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





  <div id="df-b320ff84-67bb-4b24-932f-e121b385d35a">
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
      <td>24</td>
      <td>13</td>
      <td>1</td>
      <td>12</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>23</td>
      <td>12</td>
      <td>23</td>
      <td>17</td>
      <td>26</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>1</td>
      <td>16</td>
      <td>19</td>
      <td>24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25</td>
      <td>12</td>
      <td>6</td>
      <td>20</td>
      <td>16</td>
    </tr>
    <tr>
      <th>7</th>
      <td>28</td>
      <td>15</td>
      <td>2</td>
      <td>8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>21</td>
      <td>2</td>
      <td>29</td>
      <td>15</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b320ff84-67bb-4b24-932f-e121b385d35a')"
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
          document.querySelector('#df-b320ff84-67bb-4b24-932f-e121b385d35a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b320ff84-67bb-4b24-932f-e121b385d35a');
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





  <div id="df-be7b3fa0-8f86-460d-84a1-64834ddcc4f8">
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
      <td>28</td>
      <td>25</td>
      <td>18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>26</td>
      <td>5</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>16</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>13</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>5</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-be7b3fa0-8f86-460d-84a1-64834ddcc4f8')"
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
          document.querySelector('#df-be7b3fa0-8f86-460d-84a1-64834ddcc4f8 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-be7b3fa0-8f86-460d-84a1-64834ddcc4f8');
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
    0  27  19  10
    1  19   9  26
    2   1  18  14
    3   4   7  16
    4  13   3  23
    ------------------------------
    Oluşturulan ikinci DataFrame
        a   b   c
    0  54  38  20
    1  38  18  52
    2   2  36  28
    3   8  14  32
    4  26   6  46
    ------------------------------
    df1 ve df2 DataFrame birleştirme işlemi
        a   b   c
    0  27  19  10
    1  19   9  26
    2   1  18  14
    3   4   7  16
    4  13   3  23
    0  54  38  20
    1  38  18  52
    2   2  36  28
    3   8  14  32
    4  26   6  46
    

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
    0   9   3  29
    1   7  12  19
    2  28  14  14
    3   5  15  27
    4  11   3   5
    ------------------------------
    Oluşturulan ikinci DataFrame
        a   b   c
    0  18   6  58
    1  14  24  38
    2  56  28  28
    3  10  30  54
    4  22   6  10
    ------------------------------
    df1 ve df2 DataFrame birleştirme işlemi
        a   b   c
    0   9   3  29
    1   7  12  19
    2  28  14  14
    3   5  15  27
    4  11   3   5
    5  18   6  58
    6  14  24  38
    7  56  28  28
    8  10  30  54
    9  22   6  10
    

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





  <div id="df-552ff0b1-0849-4771-b9eb-a0cfd8d24497">
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
      <td>6.0</td>
      <td>16.0</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>16.0</td>
      <td>17.0</td>
      <td>14</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13.0</td>
      <td>5.0</td>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17.0</td>
      <td>14.0</td>
      <td>21</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>18.0</td>
      <td>29.0</td>
      <td>22</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>19</td>
      <td>1.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>13</td>
      <td>1.0</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>8</td>
      <td>10.0</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>9</td>
      <td>15.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>20</td>
      <td>2.0</td>
      <td>13.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-552ff0b1-0849-4771-b9eb-a0cfd8d24497')"
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
          document.querySelector('#df-552ff0b1-0849-4771-b9eb-a0cfd8d24497 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-552ff0b1-0849-4771-b9eb-a0cfd8d24497');
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





  <div id="df-c3a8388e-4f07-43f5-807c-4e6ad6adde5a">
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
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>19</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c3a8388e-4f07-43f5-807c-4e6ad6adde5a')"
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
          document.querySelector('#df-c3a8388e-4f07-43f5-807c-4e6ad6adde5a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c3a8388e-4f07-43f5-807c-4e6ad6adde5a');
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





  <div id="df-e73d55b7-1a97-4097-8076-8aca5a95cf00">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-e73d55b7-1a97-4097-8076-8aca5a95cf00')"
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
          document.querySelector('#df-e73d55b7-1a97-4097-8076-8aca5a95cf00 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e73d55b7-1a97-4097-8076-8aca5a95cf00');
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





  <div id="df-94ea6881-f12a-4c40-ad06-f9f53b2c53e8">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-94ea6881-f12a-4c40-ad06-f9f53b2c53e8')"
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
          document.querySelector('#df-94ea6881-f12a-4c40-ad06-f9f53b2c53e8 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-94ea6881-f12a-4c40-ad06-f9f53b2c53e8');
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





  <div id="df-f65395d0-868f-4e59-a026-98dd86909dab">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-f65395d0-868f-4e59-a026-98dd86909dab')"
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
          document.querySelector('#df-f65395d0-868f-4e59-a026-98dd86909dab button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f65395d0-868f-4e59-a026-98dd86909dab');
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





  <div id="df-84f597cf-4956-4b45-b869-c745d80709d1">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-84f597cf-4956-4b45-b869-c745d80709d1')"
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
          document.querySelector('#df-84f597cf-4956-4b45-b869-c745d80709d1 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-84f597cf-4956-4b45-b869-c745d80709d1');
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





  <div id="df-c473a2e6-3f97-4c2d-9c05-7e3e42cae429">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-c473a2e6-3f97-4c2d-9c05-7e3e42cae429')"
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
          document.querySelector('#df-c473a2e6-3f97-4c2d-9c05-7e3e42cae429 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c473a2e6-3f97-4c2d-9c05-7e3e42cae429');
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





  <div id="df-c78aeebc-8b2a-4d3e-b8f2-bf1a8b92bc81">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-c78aeebc-8b2a-4d3e-b8f2-bf1a8b92bc81')"
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
          document.querySelector('#df-c78aeebc-8b2a-4d3e-b8f2-bf1a8b92bc81 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c78aeebc-8b2a-4d3e-b8f2-bf1a8b92bc81');
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





  <div id="df-fc9ae549-5e17-42ff-8757-4fc408c7a012">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-fc9ae549-5e17-42ff-8757-4fc408c7a012')"
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
          document.querySelector('#df-fc9ae549-5e17-42ff-8757-4fc408c7a012 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fc9ae549-5e17-42ff-8757-4fc408c7a012');
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





  <div id="df-b96da7c6-0eb2-4055-9f9b-1cd47fda05b4">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-b96da7c6-0eb2-4055-9f9b-1cd47fda05b4')"
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
          document.querySelector('#df-b96da7c6-0eb2-4055-9f9b-1cd47fda05b4 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b96da7c6-0eb2-4055-9f9b-1cd47fda05b4');
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





  <div id="df-2296c687-72f5-41f2-b408-b46d035ff956">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-2296c687-72f5-41f2-b408-b46d035ff956')"
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
          document.querySelector('#df-2296c687-72f5-41f2-b408-b46d035ff956 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-2296c687-72f5-41f2-b408-b46d035ff956');
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





  <div id="df-0db14fb8-ad7d-415e-87e6-476eafa68714">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-0db14fb8-ad7d-415e-87e6-476eafa68714')"
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
          document.querySelector('#df-0db14fb8-ad7d-415e-87e6-476eafa68714 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-0db14fb8-ad7d-415e-87e6-476eafa68714');
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





  <div id="df-77512f05-d3fa-4289-9e7b-fd8ba0514d4d">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-77512f05-d3fa-4289-9e7b-fd8ba0514d4d')"
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
          document.querySelector('#df-77512f05-d3fa-4289-9e7b-fd8ba0514d4d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-77512f05-d3fa-4289-9e7b-fd8ba0514d4d');
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





  <div id="df-39cf88b9-bb3f-4843-b3fb-bebaeac5e557">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-39cf88b9-bb3f-4843-b3fb-bebaeac5e557')"
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
          document.querySelector('#df-39cf88b9-bb3f-4843-b3fb-bebaeac5e557 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-39cf88b9-bb3f-4843-b3fb-bebaeac5e557');
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





  <div id="df-b2bef411-778b-4f2e-8c56-e9f723fec29e">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-b2bef411-778b-4f2e-8c56-e9f723fec29e')"
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
          document.querySelector('#df-b2bef411-778b-4f2e-8c56-e9f723fec29e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b2bef411-778b-4f2e-8c56-e9f723fec29e');
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





  <div id="df-5b56d097-6957-490b-8e5e-55ce99bfc483">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-5b56d097-6957-490b-8e5e-55ce99bfc483')"
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
          document.querySelector('#df-5b56d097-6957-490b-8e5e-55ce99bfc483 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5b56d097-6957-490b-8e5e-55ce99bfc483');
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





  <div id="df-29d13425-85a2-4b53-a15d-91d4e3958752">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-29d13425-85a2-4b53-a15d-91d4e3958752')"
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
          document.querySelector('#df-29d13425-85a2-4b53-a15d-91d4e3958752 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-29d13425-85a2-4b53-a15d-91d4e3958752');
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





  <div id="df-1076f46a-1168-4f75-b85b-26ad6c8a4072">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-1076f46a-1168-4f75-b85b-26ad6c8a4072')"
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
          document.querySelector('#df-1076f46a-1168-4f75-b85b-26ad6c8a4072 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-1076f46a-1168-4f75-b85b-26ad6c8a4072');
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





  <div id="df-4975c100-5962-455a-9c74-adb31782b78d">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-4975c100-5962-455a-9c74-adb31782b78d')"
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
          document.querySelector('#df-4975c100-5962-455a-9c74-adb31782b78d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4975c100-5962-455a-9c74-adb31782b78d');
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





  <div id="df-59002d0f-028d-4207-8af7-29b31cb2a3b0">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-59002d0f-028d-4207-8af7-29b31cb2a3b0')"
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
          document.querySelector('#df-59002d0f-028d-4207-8af7-29b31cb2a3b0 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-59002d0f-028d-4207-8af7-29b31cb2a3b0');
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





  <div id="df-29cfdda8-fa18-4dc5-b7b7-3fee365c9e4c">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-29cfdda8-fa18-4dc5-b7b7-3fee365c9e4c')"
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
          document.querySelector('#df-29cfdda8-fa18-4dc5-b7b7-3fee365c9e4c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-29cfdda8-fa18-4dc5-b7b7-3fee365c9e4c');
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





  <div id="df-4e944ab7-b9e5-4fc2-bb1f-6a3820fa3293">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-4e944ab7-b9e5-4fc2-bb1f-6a3820fa3293')"
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
          document.querySelector('#df-4e944ab7-b9e5-4fc2-bb1f-6a3820fa3293 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4e944ab7-b9e5-4fc2-bb1f-6a3820fa3293');
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





  <div id="df-29ca2477-6bad-4368-961c-f771223bb961">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-29ca2477-6bad-4368-961c-f771223bb961')"
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
          document.querySelector('#df-29ca2477-6bad-4368-961c-f771223bb961 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-29ca2477-6bad-4368-961c-f771223bb961');
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





  <div id="df-68c324b7-3f82-40dc-9a14-cf7cd3e61ab1">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-68c324b7-3f82-40dc-9a14-cf7cd3e61ab1')"
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
          document.querySelector('#df-68c324b7-3f82-40dc-9a14-cf7cd3e61ab1 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-68c324b7-3f82-40dc-9a14-cf7cd3e61ab1');
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





  <div id="df-ec5a1136-cb83-4e7b-a1ee-ccdab69c7c96">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-ec5a1136-cb83-4e7b-a1ee-ccdab69c7c96')"
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
          document.querySelector('#df-ec5a1136-cb83-4e7b-a1ee-ccdab69c7c96 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ec5a1136-cb83-4e7b-a1ee-ccdab69c7c96');
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





  <div id="df-4c8e8bdb-f304-41a6-9b7c-5fa322f33b4f">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-4c8e8bdb-f304-41a6-9b7c-5fa322f33b4f')"
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
          document.querySelector('#df-4c8e8bdb-f304-41a6-9b7c-5fa322f33b4f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4c8e8bdb-f304-41a6-9b7c-5fa322f33b4f');
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





  <div id="df-fbac9bf5-a7f9-4089-976f-caeee9475a85">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-fbac9bf5-a7f9-4089-976f-caeee9475a85')"
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
          document.querySelector('#df-fbac9bf5-a7f9-4089-976f-caeee9475a85 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fbac9bf5-a7f9-4089-976f-caeee9475a85');
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





  <div id="df-96d82242-d027-49b8-9621-d132cb2fdc37">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-96d82242-d027-49b8-9621-d132cb2fdc37')"
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
          document.querySelector('#df-96d82242-d027-49b8-9621-d132cb2fdc37 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-96d82242-d027-49b8-9621-d132cb2fdc37');
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





  <div id="df-80e7bbcc-1ba5-4e85-8a5a-38a1805c9f5e">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-80e7bbcc-1ba5-4e85-8a5a-38a1805c9f5e')"
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
          document.querySelector('#df-80e7bbcc-1ba5-4e85-8a5a-38a1805c9f5e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-80e7bbcc-1ba5-4e85-8a5a-38a1805c9f5e');
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
