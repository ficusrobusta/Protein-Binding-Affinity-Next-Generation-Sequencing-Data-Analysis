```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import re
%matplotlib inline
```

Import csv file into Pandas and view contents -->


```python
seq_df = pd.read_csv('tech_test/sequence_table.csv')
```


```python
seq_df.head()
```




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
      <th>Unnamed: 0</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGACAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>13.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>17.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
seq_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 13046 entries, 0 to 13045
    Data columns (total 3 columns):
     #   Column                        Non-Null Count  Dtype  
    ---  ------                        --------------  -----  
     0   Unnamed: 0                    13046 non-null  object 
     1   read_count_in_input_library   13046 non-null  float64
     2   read_count_in_output_library  13046 non-null  float64
    dtypes: float64(2), object(1)
    memory usage: 305.9+ KB



```python
seq_df.describe()
```




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
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>13046.000000</td>
      <td>13046.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>11.534033</td>
      <td>15.80975</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.423982</td>
      <td>29.43316</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.00000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>9.000000</td>
      <td>0.00000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>12.000000</td>
      <td>0.00000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>15.000000</td>
      <td>27.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>36.000000</td>
      <td>546.00000</td>
    </tr>
  </tbody>
</table>
</div>



Rename column with sequences


```python
seq_df.rename(columns={"Unnamed: 0": "sequence"}, inplace=True)
```


```python
seq_df.sort_values(by=["read_count_in_input_library"])

```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1136</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>534</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>11134</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>11118</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>11106</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>970</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>30.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6362</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>30.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4284</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>31.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>11840</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>31.0</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>8669</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>36.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>13046 rows × 3 columns</p>
</div>



Plot distributions of read counts 


```python
ax1 = seq_df.read_count_in_input_library.plot.hist(title="Input Read Count Distribution")
ax1.set_xlabel("Read count")
```




    Text(0.5, 0, 'Read count')




![png](output_10_1.png)



```python
ax2 = seq_df.read_count_in_output_library.plot.hist(title="Output Read Count Distribution")
ax2.set_xlabel("Read count")
```




    Text(0.5, 0, 'Read count')




![png](output_11_1.png)


Check uniqueness of sequences


```python
unique_seq= seq_df["sequence"].unique()
unique_seq_df = pd.DataFrame(data=unique_seq, columns=["sequence"])
print(unique_seq_df)
```

                                                    sequence
    0      AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGACAAGCCTGGAG...
    1      AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    2      AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    3      AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    4      AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    ...                                                  ...
    13041  GAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    13042  TAGGTGCAGCTGGTGGACTCTGGGGGAGGCCTGGTCAAGCCTGGAG...
    13043  TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    13044  TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    13045  TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    
    [13046 rows x 1 columns]


Check length of designed library


```python
variant_library = "CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTCNNSNNSNNSNNSTACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGTNNSNNSNNSNNSACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA"
```


```python
variant_library_series = pd.Series(variant_library)
variant_library_series.str.len()
```




    0    296
    dtype: int64


Create a new column to input result of whether sequence matches design

```python
seq_df["Match"]= np.nan
```


```python
variant_library_2_series = re.sub("N", ".", "CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTCNNSNNSNNSNNSTACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGTNNSNNSNNSNNSACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA")
variant_library_2_series = re.sub("S", "[GC]", "CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTC..S..S..S..STACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGT..S..S..S..SACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA")
```


```python
variant_library_2_series 
```




    'CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTC..[GC]..[GC]..[GC]..[GC]TACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGT..[GC]..[GC]..[GC]..[GC]ACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA'




```python
seq_df["Design"]= variant_library_2_series
seq_df
```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGACAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>13.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>17.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>13041</th>
      <td>GAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>20.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13042</th>
      <td>TAGGTGCAGCTGGTGGACTCTGGGGGAGGCCTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13043</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13044</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13045</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
  </tbody>
</table>
<p>13046 rows × 5 columns</p>
</div>




```python
seq_df["Match"]= seq_df['sequence'].str.match("CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTC..[GC]..[GC]..[GC]..[GC]TACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGT..[GC]..[GC]..[GC]..[GC]ACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA")
```

Check whether sequences contain only G, A, C or T


```python
variant_library_3 = re.sub(".", "[GCAT]", "CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTCNNSNNSNNSNNSTACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGTNNSNNSNNSNNSACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA")
variant_library_3

```




    '[GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT]'




```python
nucleotide_match= seq_df['sequence'].str.match('[GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT][GCAT]')
nucleotide_match
```




    0        True
    1        True
    2        True
    3        True
    4        True
             ... 
    13041    True
    13042    True
    13043    True
    13044    True
    13045    True
    Name: sequence, Length: 13046, dtype: bool



How many sequences match design?


```python
seq_df["Match"].value_counts()
```




    True     11562
    False     1484
    Name: Match, dtype: int64




```python
seq_df["Match"].value_counts(normalize=True)
```




    True     0.886249
    False    0.113751
    Name: Match, dtype: float64




```python
seq_df
```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGACAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>13.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>17.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>13041</th>
      <td>GAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>20.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13042</th>
      <td>TAGGTGCAGCTGGTGGACTCTGGGGGAGGCCTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13043</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13044</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
    <tr>
      <th>13045</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
    </tr>
  </tbody>
</table>
<p>13046 rows × 5 columns</p>
</div>




```python
seq_df["Match"].value_counts().plot(kind='bar', title= "Number of library sequences that match design")
    
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7ff4c8639af0>




![png](output_30_1.png)


Split non-matching sequences to evaluate at each position


```python
 non_match_df = seq_df.loc[seq_df["Match"] == False, "sequence"]
```


```python
non_match_df
```




    0        AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGACAAGCCTGGAG...
    1        AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    2        AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    3        AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    4        AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
                                   ...                        
    13041    GAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    13042    TAGGTGCAGCTGGTGGACTCTGGGGGAGGCCTGGTCAAGCCTGGAG...
    13043    TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    13044    TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    13045    TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...
    Name: sequence, Length: 1484, dtype: object




```python
non_match_df = non_match_df.apply(lambda x: pd.Series(list(x))) 
```


```python
non_match_df
```




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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>289</th>
      <th>290</th>
      <th>291</th>
      <th>292</th>
      <th>293</th>
      <th>294</th>
      <th>295</th>
      <th>296</th>
      <th>297</th>
      <th>298</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>13041</th>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13042</th>
      <td>T</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13043</th>
      <td>T</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13044</th>
      <td>T</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13045</th>
      <td>T</td>
      <td>A</td>
      <td>G</td>
      <td>G</td>
      <td>T</td>
      <td>G</td>
      <td>C</td>
      <td>A</td>
      <td>G</td>
      <td>C</td>
      <td>...</td>
      <td>C</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>G</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1484 rows × 299 columns</p>
</div>



Check lengths of non-matching sequences


```python
nt = non_match_df.count(axis=0) 
nt
```




    0      1484
    1      1484
    2      1484
    3      1484
    4      1484
           ... 
    294    1484
    295    1484
    296     112
    297      63
    298      31
    Length: 299, dtype: int64




```python
# Unfinished: aim to assess numbers of each nucleotide at each position and plot stacked bar chart
# nt_counts = pd.Series([])
# i = 0
# for i in non_match_df[i]:
#     nt_counts= nt_counts + non_match_df[i].value_counts()
#     if i > 295:
#         break
#     else:
#         i=i+1
# nt_counts
# non_match_df.append(nt_count)
# non_match_df_len = len(non_match_df)
# non_match_df.loc[non_match_df_len]= nt_count
```


```python
total_input_reads = seq_df["read_count_in_input_library"].sum()
total_input_reads

total_output_reads = seq_df["read_count_in_output_library"].sum()
total_output_reads

seq_df["Percentage of input pool"]= seq_df["read_count_in_input_library"]/total_input_reads * 100
seq_df

seq_df["Percentage of output pool"]= seq_df["read_count_in_output_library"]/total_output_reads * 100
seq_df

```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
      <th>Percentage of input pool</th>
      <th>Percentage of output pool</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGACAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>13.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.008639</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000000</td>
      <td>0.000485</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>17.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000000</td>
      <td>0.008242</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>13041</th>
      <td>GAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>20.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.013291</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>13042</th>
      <td>TAGGTGCAGCTGGTGGACTCTGGGGGAGGCCTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000000</td>
      <td>0.000485</td>
    </tr>
    <tr>
      <th>13043</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000000</td>
      <td>0.000485</td>
    </tr>
    <tr>
      <th>13044</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000000</td>
      <td>0.000485</td>
    </tr>
    <tr>
      <th>13045</th>
      <td>TAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>13046 rows × 7 columns</p>
</div>



Clean data, remove sequences with 0 reads


```python
seq_df_clean = seq_df[seq_df.read_count_in_output_library != 0]
seq_df_clean = seq_df_clean[seq_df_clean.read_count_in_input_library != 0]
# seq_df_clean = seq_df_clean[seq_df_clean.Match == True]
seq_df_clean
```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
      <th>Percentage of input pool</th>
      <th>Percentage of output pool</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>42</th>
      <td>CAGGTGAAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>394.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.191027</td>
    </tr>
    <tr>
      <th>59</th>
      <td>CAGGTGCAGCGACTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTG...</td>
      <td>12.0</td>
      <td>51.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.024727</td>
    </tr>
    <tr>
      <th>110</th>
      <td>CAGGTGCAGCTGGTGGAGNCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>9.0</td>
      <td>16.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.005981</td>
      <td>0.007757</td>
    </tr>
    <tr>
      <th>173</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCATTGGTCAAGCCTGGA...</td>
      <td>8.0</td>
      <td>32.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.005317</td>
      <td>0.015515</td>
    </tr>
    <tr>
      <th>192</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTNGGTCAAGCCTGGAG...</td>
      <td>12.0</td>
      <td>40.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.019394</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12895</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTNGTCAAGCCTGGAG...</td>
      <td>22.0</td>
      <td>468.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.014621</td>
      <td>0.226905</td>
    </tr>
    <tr>
      <th>12919</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGNAGGCTTGGTCAAGCCTGGAG...</td>
      <td>11.0</td>
      <td>25.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007310</td>
      <td>0.012121</td>
    </tr>
    <tr>
      <th>12936</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGTGGGGAGGCTTGGTCAAGCCTGGA...</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.014060</td>
    </tr>
    <tr>
      <th>12962</th>
      <td>CAGGTGCAGCTGGTGGNGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>18.0</td>
      <td>54.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011962</td>
      <td>0.026181</td>
    </tr>
    <tr>
      <th>13025</th>
      <td>CAGNTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.006646</td>
      <td>0.013091</td>
    </tr>
  </tbody>
</table>
<p>5421 rows × 7 columns</p>
</div>



Create affinity metric and sort by


```python
seq_df_clean["Affinity"] = seq_df_clean["read_count_in_output_library"] / seq_df_clean["read_count_in_input_library"]
```


```python
seq_df_clean
```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
      <th>Percentage of input pool</th>
      <th>Percentage of output pool</th>
      <th>Affinity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>42</th>
      <td>CAGGTGAAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>394.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.191027</td>
      <td>394.000000</td>
    </tr>
    <tr>
      <th>59</th>
      <td>CAGGTGCAGCGACTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTG...</td>
      <td>12.0</td>
      <td>51.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.024727</td>
      <td>4.250000</td>
    </tr>
    <tr>
      <th>110</th>
      <td>CAGGTGCAGCTGGTGGAGNCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>9.0</td>
      <td>16.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.005981</td>
      <td>0.007757</td>
      <td>1.777778</td>
    </tr>
    <tr>
      <th>173</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCATTGGTCAAGCCTGGA...</td>
      <td>8.0</td>
      <td>32.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.005317</td>
      <td>0.015515</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>192</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTNGGTCAAGCCTGGAG...</td>
      <td>12.0</td>
      <td>40.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.019394</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12895</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTNGTCAAGCCTGGAG...</td>
      <td>22.0</td>
      <td>468.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.014621</td>
      <td>0.226905</td>
      <td>21.272727</td>
    </tr>
    <tr>
      <th>12919</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGNAGGCTTGGTCAAGCCTGGAG...</td>
      <td>11.0</td>
      <td>25.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007310</td>
      <td>0.012121</td>
      <td>2.272727</td>
    </tr>
    <tr>
      <th>12936</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGTGGGGAGGCTTGGTCAAGCCTGGA...</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.014060</td>
      <td>2.416667</td>
    </tr>
    <tr>
      <th>12962</th>
      <td>CAGGTGCAGCTGGTGGNGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>18.0</td>
      <td>54.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011962</td>
      <td>0.026181</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>13025</th>
      <td>CAGNTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.006646</td>
      <td>0.013091</td>
      <td>2.700000</td>
    </tr>
  </tbody>
</table>
<p>5421 rows × 8 columns</p>
</div>




```python
seq_df_clean= seq_df_clean.sort_values(by=["Affinity"])
seq_df_clean
```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
      <th>Percentage of input pool</th>
      <th>Percentage of output pool</th>
      <th>Affinity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3650</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>18.0</td>
      <td>1.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011962</td>
      <td>0.000485</td>
      <td>0.055556</td>
    </tr>
    <tr>
      <th>1790</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>18.0</td>
      <td>2.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011962</td>
      <td>0.000970</td>
      <td>0.111111</td>
    </tr>
    <tr>
      <th>1715</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>9.0</td>
      <td>1.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.005981</td>
      <td>0.000485</td>
      <td>0.111111</td>
    </tr>
    <tr>
      <th>3043</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>17.0</td>
      <td>2.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011298</td>
      <td>0.000970</td>
      <td>0.117647</td>
    </tr>
    <tr>
      <th>1373</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>15.0</td>
      <td>2.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009969</td>
      <td>0.000970</td>
      <td>0.133333</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4645</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>11.0</td>
      <td>471.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007310</td>
      <td>0.228359</td>
      <td>42.818182</td>
    </tr>
    <tr>
      <th>1135</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>10.0</td>
      <td>482.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.006646</td>
      <td>0.233692</td>
      <td>48.200000</td>
    </tr>
    <tr>
      <th>6713</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>52.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.025212</td>
      <td>52.000000</td>
    </tr>
    <tr>
      <th>1803</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>6.0</td>
      <td>469.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.003987</td>
      <td>0.227390</td>
      <td>78.166667</td>
    </tr>
    <tr>
      <th>42</th>
      <td>CAGGTGAAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>394.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.191027</td>
      <td>394.000000</td>
    </tr>
  </tbody>
</table>
<p>5421 rows × 8 columns</p>
</div>




```python
High_affinity_df=seq_df_clean.nlargest(50,"Affinity").sort_values(by=["Affinity"])
```


```python
High_affinity_df.sort_values(by=["Affinity"], ascending=False)
```




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
      <th>sequence</th>
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Match</th>
      <th>Design</th>
      <th>Percentage of input pool</th>
      <th>Percentage of output pool</th>
      <th>Affinity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>42</th>
      <td>CAGGTGAAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>394.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.191027</td>
      <td>394.000000</td>
    </tr>
    <tr>
      <th>1803</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>6.0</td>
      <td>469.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.003987</td>
      <td>0.227390</td>
      <td>78.166667</td>
    </tr>
    <tr>
      <th>6713</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>52.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.025212</td>
      <td>52.000000</td>
    </tr>
    <tr>
      <th>1135</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>10.0</td>
      <td>482.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.006646</td>
      <td>0.233692</td>
      <td>48.200000</td>
    </tr>
    <tr>
      <th>4645</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>11.0</td>
      <td>471.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007310</td>
      <td>0.228359</td>
      <td>42.818182</td>
    </tr>
    <tr>
      <th>8000</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>15.0</td>
      <td>546.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009969</td>
      <td>0.264722</td>
      <td>36.400000</td>
    </tr>
    <tr>
      <th>10543</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>12.0</td>
      <td>426.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.206541</td>
      <td>35.500000</td>
    </tr>
    <tr>
      <th>5265</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>34.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.016485</td>
      <td>34.000000</td>
    </tr>
    <tr>
      <th>6089</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>16.0</td>
      <td>534.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.010633</td>
      <td>0.258904</td>
      <td>33.375000</td>
    </tr>
    <tr>
      <th>9948</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>12.0</td>
      <td>393.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.190542</td>
      <td>32.750000</td>
    </tr>
    <tr>
      <th>2647</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>12.0</td>
      <td>376.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.182299</td>
      <td>31.333333</td>
    </tr>
    <tr>
      <th>9569</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>15.0</td>
      <td>465.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009969</td>
      <td>0.225450</td>
      <td>31.000000</td>
    </tr>
    <tr>
      <th>10670</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>30.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.014545</td>
      <td>30.000000</td>
    </tr>
    <tr>
      <th>5120</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>11.0</td>
      <td>314.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007310</td>
      <td>0.152239</td>
      <td>28.545455</td>
    </tr>
    <tr>
      <th>281</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>15.0</td>
      <td>416.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009969</td>
      <td>0.201693</td>
      <td>27.733333</td>
    </tr>
    <tr>
      <th>8332</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>16.0</td>
      <td>443.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.010633</td>
      <td>0.214784</td>
      <td>27.687500</td>
    </tr>
    <tr>
      <th>11066</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>15.0</td>
      <td>412.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009969</td>
      <td>0.199754</td>
      <td>27.466667</td>
    </tr>
    <tr>
      <th>8727</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>8.0</td>
      <td>218.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.005317</td>
      <td>0.105695</td>
      <td>27.250000</td>
    </tr>
    <tr>
      <th>10701</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>17.0</td>
      <td>458.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011298</td>
      <td>0.222056</td>
      <td>26.941176</td>
    </tr>
    <tr>
      <th>5527</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>2.0</td>
      <td>53.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001329</td>
      <td>0.025696</td>
      <td>26.500000</td>
    </tr>
    <tr>
      <th>1799</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>12.0</td>
      <td>311.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.007975</td>
      <td>0.150785</td>
      <td>25.916667</td>
    </tr>
    <tr>
      <th>8630</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>21.0</td>
      <td>544.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.013956</td>
      <td>0.263752</td>
      <td>25.904762</td>
    </tr>
    <tr>
      <th>12256</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>14.0</td>
      <td>358.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009304</td>
      <td>0.173572</td>
      <td>25.571429</td>
    </tr>
    <tr>
      <th>3049</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>5.0</td>
      <td>124.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.003323</td>
      <td>0.060120</td>
      <td>24.800000</td>
    </tr>
    <tr>
      <th>7367</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>4.0</td>
      <td>99.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.002658</td>
      <td>0.047999</td>
      <td>24.750000</td>
    </tr>
    <tr>
      <th>11935</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>3.0</td>
      <td>74.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001994</td>
      <td>0.035878</td>
      <td>24.666667</td>
    </tr>
    <tr>
      <th>7559</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>2.0</td>
      <td>49.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001329</td>
      <td>0.023757</td>
      <td>24.500000</td>
    </tr>
    <tr>
      <th>9193</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>24.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.011636</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>9477</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>17.0</td>
      <td>405.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011298</td>
      <td>0.196360</td>
      <td>23.823529</td>
    </tr>
    <tr>
      <th>5763</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>4.0</td>
      <td>95.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.002658</td>
      <td>0.046060</td>
      <td>23.750000</td>
    </tr>
    <tr>
      <th>10695</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>3.0</td>
      <td>71.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001994</td>
      <td>0.034424</td>
      <td>23.666667</td>
    </tr>
    <tr>
      <th>7010</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>22.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.010666</td>
      <td>22.000000</td>
    </tr>
    <tr>
      <th>10493</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>2.0</td>
      <td>44.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001329</td>
      <td>0.021333</td>
      <td>22.000000</td>
    </tr>
    <tr>
      <th>11409</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>13.0</td>
      <td>286.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.008639</td>
      <td>0.138664</td>
      <td>22.000000</td>
    </tr>
    <tr>
      <th>3092</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>16.0</td>
      <td>350.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.010633</td>
      <td>0.169694</td>
      <td>21.875000</td>
    </tr>
    <tr>
      <th>683</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>21.0</td>
      <td>447.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.013956</td>
      <td>0.216723</td>
      <td>21.285714</td>
    </tr>
    <tr>
      <th>12895</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTNGTCAAGCCTGGAG...</td>
      <td>22.0</td>
      <td>468.0</td>
      <td>False</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.014621</td>
      <td>0.226905</td>
      <td>21.272727</td>
    </tr>
    <tr>
      <th>7832</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>14.0</td>
      <td>296.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.009304</td>
      <td>0.143512</td>
      <td>21.142857</td>
    </tr>
    <tr>
      <th>2607</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>3.0</td>
      <td>63.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001994</td>
      <td>0.030545</td>
      <td>21.000000</td>
    </tr>
    <tr>
      <th>8953</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>18.0</td>
      <td>377.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011962</td>
      <td>0.182784</td>
      <td>20.944444</td>
    </tr>
    <tr>
      <th>4253</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>3.0</td>
      <td>60.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001994</td>
      <td>0.029090</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>1281</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>3.0</td>
      <td>59.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.001994</td>
      <td>0.028606</td>
      <td>19.666667</td>
    </tr>
    <tr>
      <th>4377</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>18.0</td>
      <td>342.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.011962</td>
      <td>0.165815</td>
      <td>19.000000</td>
    </tr>
    <tr>
      <th>12109</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>4.0</td>
      <td>75.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.002658</td>
      <td>0.036363</td>
      <td>18.750000</td>
    </tr>
    <tr>
      <th>9253</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>25.0</td>
      <td>452.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.016614</td>
      <td>0.219147</td>
      <td>18.080000</td>
    </tr>
    <tr>
      <th>1351</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>5.0</td>
      <td>90.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.003323</td>
      <td>0.043636</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>8689</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>1.0</td>
      <td>18.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.000665</td>
      <td>0.008727</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>6781</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>10.0</td>
      <td>179.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.006646</td>
      <td>0.086786</td>
      <td>17.900000</td>
    </tr>
    <tr>
      <th>2578</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>4.0</td>
      <td>71.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.002658</td>
      <td>0.034424</td>
      <td>17.750000</td>
    </tr>
    <tr>
      <th>8487</th>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>4.0</td>
      <td>71.0</td>
      <td>True</td>
      <td>CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAG...</td>
      <td>0.002658</td>
      <td>0.034424</td>
      <td>17.750000</td>
    </tr>
  </tbody>
</table>
</div>



Distribution after cleaning


```python
ax1 = seq_df_clean.read_count_in_input_library.plot.hist(title="Input Read Count Distribution")
ax1.set_xlabel("Read count")
```




    Text(0.5, 0, 'Read count')




![png](output_49_1.png)



```python
ax2 = seq_df_clean.read_count_in_output_library.plot.hist(title="Output Read Count Distribution")
ax2.set_xlabel("Read count")
```




    Text(0.5, 0, 'Read count')




![png](output_50_1.png)



```python
seq_df_clean.describe()

```




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
      <th>read_count_in_input_library</th>
      <th>read_count_in_output_library</th>
      <th>Percentage of input pool</th>
      <th>Percentage of output pool</th>
      <th>Affinity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5421.000000</td>
      <td>5421.000000</td>
      <td>5421.000000</td>
      <td>5421.000000</td>
      <td>5421.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>12.779745</td>
      <td>37.008301</td>
      <td>0.008493</td>
      <td>0.017943</td>
      <td>3.364440</td>
    </tr>
    <tr>
      <th>std</th>
      <td>4.156865</td>
      <td>35.892266</td>
      <td>0.002763</td>
      <td>0.017402</td>
      <td>6.290456</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000665</td>
      <td>0.000485</td>
      <td>0.055556</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>10.000000</td>
      <td>21.000000</td>
      <td>0.006646</td>
      <td>0.010182</td>
      <td>1.600000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>13.000000</td>
      <td>30.000000</td>
      <td>0.008639</td>
      <td>0.014545</td>
      <td>2.450000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>15.000000</td>
      <td>43.000000</td>
      <td>0.009969</td>
      <td>0.020848</td>
      <td>3.900000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>31.000000</td>
      <td>546.000000</td>
      <td>0.020602</td>
      <td>0.264722</td>
      <td>394.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
seq_df_clean["Affinity"].value_counts().plot(kind='bar',xticks= ([0, 200, 400, 600,800]), title= "Binding affinity of proteins")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7ff4ca5669a0>




![png](output_52_1.png)



```python
seq_df_clean.quantile(0.99)
```




    read_count_in_input_library      23.000000
    read_count_in_output_library    139.800000
    Match                             1.000000
    Percentage of input pool          0.015285
    Percentage of output pool         0.067781
    Affinity                         16.492308
    Name: 0.99, dtype: float64




```python
protein1= High_affinity_df.iloc[0,0]
protein2= High_affinity_df.iloc[1,0]
protein3= High_affinity_df.iloc[2,0]
```


```python
protein1
```




    'CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTCTCCCCCGCCTGCTACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGTGTCTTGGTCTCCACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA'




```python
protein2
```




    'CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTCCGCGCGGCCTACTACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGTGGCTAGGAGTTCACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA'




```python
protein3
```




    'CAGGTGCAGCTGGTGGAGTCTGGGGGAGGCTTGGTCAAGCCTGGAGGGTCCCTGAGACTCTCCTGTGCAGCCTCTGGATTCGTCGACTGCTTCTACTACATGAGCTGGATCCGCCAGGCTCCAGGGAAGGGGCTGGAGTGGGTTTCATACATTAGTGTCGGCTCCTGCACCATATACTACGCAGACTCTGTGAAGGGCCGATTCACCATCTCCAGGGACAACGCCAAGAACTCACTGTATCTGCAAATGAACAGCCTGAGAGCCGAGGACACGGCCGTGTATTACTGTGCGAGAGA'


