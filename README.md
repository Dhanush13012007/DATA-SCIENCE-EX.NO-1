#EX.NO:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output:

SAMPLEIDS.csv
```
import pandas as pd
df= pd.read_csv("SAMPLEIDS.csv")
df

df.head()
df.tail()

df.isnull()
df.notnull()
df.isnull().sum()
df.isnull().any()

df.dropna()
df.dropna(axis = 1)
df.fillna(0)
df.fillna (method = 'ffill')
df.fillna (method = 'bfill')
```

<img width="820" height="521" alt="image" src="https://github.com/user-attachments/assets/4359db11-031f-4bf9-8e5c-a7693a261328" />
<img width="776" height="145" alt="image" src="https://github.com/user-attachments/assets/3ad6604f-3126-439d-b2af-81654da3aa15" />
<img width="934" height="185" alt="image" src="https://github.com/user-attachments/assets/5a46534b-16ae-4ce6-9dc2-dc66b79645e1" />
<img width="747" height="526" alt="Screenshot 2026-05-22 205318" src="https://github.com/user-attachments/assets/560f3466-8f3d-440e-99d5-14663ec814f2" />
<img width="708" height="531" alt="Screenshot 2026-05-22 205330" src="https://github.com/user-attachments/assets/79fed8a3-f9b5-4d12-98ed-16a29b67974c" />
<img width="387" height="508" alt="Screenshot 2026-05-22 205342" src="https://github.com/user-attachments/assets/fd4fa049-9618-4bee-901f-d87445b77282" />
<img width="811" height="348" alt="Screenshot 2026-05-22 205751" src="https://github.com/user-attachments/assets/537c246b-edde-4f86-83d6-e00805e2b971" />
<img width="402" height="527" alt="Screenshot 2026-05-22 205758" src="https://github.com/user-attachments/assets/9a6fbc24-54d9-47b2-b8ce-80b1d780cd2a" />
<img width="758" height="515" alt="Screenshot 2026-05-22 205809" src="https://github.com/user-attachments/assets/152729a6-f761-4ade-b268-51338792ee11" />
<img width="830" height="520" alt="Screenshot 2026-05-22 205816" src="https://github.com/user-attachments/assets/34f9e097-a238-4259-9957-fff346c6b1e6" />
<img width="777" height="525" alt="Screenshot 2026-05-22 205823" src="https://github.com/user-attachments/assets/f7adf885-af6b-4ddf-961d-8c6798253959" />


Loan_data.csv
'''
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt
df = pd.read_csv('Loan_data.csv')
print(df.head(),"\n")


df.info()
print()

print(df.describe(),"\n")

df.isnull()
print(df.isnull().sum())
print()



df_fill_0 = df.fillna(0)
print(df_fill_0,"\n")

df_ffill = df.ffill()
print(df_ffill,"\n")

df_bfill = df.bfill()
print(df_bfill,"\n")


df['LoanAmount'] = df['LoanAmount'].fillna(df['LoanAmount'].mean())
print(df,"\n")

df_dropna = df.dropna()
print(df_dropna,"\n")

sns.boxplot(x=df['LoanAmount'])
plt.show()
print()


Q1 = df['LoanAmount'].quantile(0.25)
Q3 = df['LoanAmount'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR,"\n")

outliers_iqr = df[
    (df['LoanAmount'] < (Q1 - 1.5 * IQR)) |
    (df['LoanAmount'] > (Q3 + 1.5 * IQR))
]
print(outliers_iqr,"\n")

ir_cleaned = df[
    ~((df['LoanAmount'] < (Q1 - 1.5 * IQR)) |
      (df['LoanAmount'] > (Q3 + 1.5 * IQR)))
]
print(ir_cleaned,"\n")

df_z = df['LoanAmount'].dropna()
z_scores = np.abs(stats.zscore(df_z))
print(z_scores,"\n")

threshold = 3
outliers_z = df_z[z_scores > threshold]
print("Outliers:",outliers_z,"\n")
     
df_z_cleaned = df_z[z_scores <= threshold]
print(df_z_cleaned,"\n")

```
<img width="634" height="400" alt="image" src="https://github.com/user-attachments/assets/c66ad58b-9c32-40e7-a1ac-251dcabf36ae" />
<img width="581" height="759" alt="image" src="https://github.com/user-attachments/assets/8d5fedd1-4393-4ec0-8a52-8cd531b4aa7a" />
<img width="553" height="566" alt="Screenshot 2026-05-22 211053" src="https://github.com/user-attachments/assets/91d3ecd9-a0cd-4070-9c95-be9cf5e1093a" />
<img width="598" height="577" alt="Screenshot 2026-05-22 211153" src="https://github.com/user-attachments/assets/44b3075f-4b0e-4bdf-bf2a-c807d96e7ec3" />
<img width="536" height="572" alt="Screenshot 2026-05-22 211222" src="https://github.com/user-attachments/assets/1194b4da-37ef-4fbe-aac2-a84aa7672fd6" />
<img width="534" height="575" alt="Screenshot 2026-05-22 211515" src="https://github.com/user-attachments/assets/746bafe4-2a9a-4390-b123-8d4b8d02039f" />
<img width="558" height="583" alt="Screenshot 2026-05-22 211522" src="https://github.com/user-attachments/assets/58ab5058-4f3f-4f0a-ae23-a87b9bf88555" />
<img width="448" height="355" alt="Screenshot 2026-05-22 211532" src="https://github.com/user-attachments/assets/865a46c0-4018-4dcd-857e-c6e4fbd42996" />
<img width="514" height="114" alt="Screenshot 2026-05-22 211810" src="https://github.com/user-attachments/assets/5d07b79d-b2f7-4c26-9073-ee93cec8b361" />
<img width="635" height="914" alt="Screenshot 2026-05-22 211857" src="https://github.com/user-attachments/assets/c8b650a1-ba01-429d-9bd0-114c626f88b0" />
<img width="567" height="618" alt="Screenshot 2026-05-22 211929" src="https://github.com/user-attachments/assets/45b9fe38-4bf2-4f2d-a728-8eda528cf5f3" />
<img width="353" height="479" alt="Screenshot 2026-05-22 212104" src="https://github.com/user-attachments/assets/faf54500-41e2-4c4e-8546-1275a5ce0acc" />


Data_set.csv
```


import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv('Data_set.csv')
print(df.head(),"\n")


df.info()
print()


print(df.describe(),"\n")


df.isnull()
print(df.isnull().sum())
print()


df_fill_0 = df.fillna(0)
print(df_fill_0,"\n")


df_ffill = df.ffill()
print(df_ffill,"\n") 


df_bfill = df.bfill()
print(df_bfill,"\n")


df['rating'] = df['rating'].fillna(df['rating'].mean())
print(df,"\n")

df_dropna = df.dropna()
print(df_dropna,"\n")


sns.boxplot(x=df['rating'])
plt.show()
print()

Q1 = df['rating'].quantile(0.25)
Q3 = df['rating'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR,"\n")

outliers_iqr = df[
    (df['rating'] < (Q1 - 1.5 * IQR)) |
    (df['rating'] > (Q3 + 1.5 * IQR))
]
print(outliers_iqr,"\n")

ir_cleaned = df[
    ~((df['rating'] < (Q1 - 1.5 * IQR)) |
      (df['rating'] > (Q3 + 1.5 * IQR)))
]
print(ir_cleaned,"\n")

df_z = df['rating'].dropna()

z_scores = np.abs(stats.zscore(df_z))
print(z_scores,"\n")

threshold = 3
outliers_z = df_z[z_scores > threshold]
print("Outliers:",outliers_z,"\n")
     
df_z_cleaned = df_z[z_scores <= threshold]
print(df_z_cleaned,"\n")


```
<img width="552" height="285" alt="Screenshot 2026-05-22 212459" src="https://github.com/user-attachments/assets/8261e0fb-2618-4190-a065-a005ff72cb38" />
<img width="459" height="681" alt="Screenshot 2026-05-22 212535" src="https://github.com/user-attachments/assets/39f0e669-023d-4654-b91d-5d43021560d2" />
<img width="540" height="576" alt="Screenshot 2026-05-22 212609" src="https://github.com/user-attachments/assets/efeba4f8-83f2-449f-a48a-2c67478b0659" />
<img width="577" height="581" alt="Screenshot 2026-05-22 212632" src="https://github.com/user-attachments/assets/efa392f8-96e7-4335-901b-9ad46d1133fd" />
<img width="528" height="582" alt="Screenshot 2026-05-22 212651" src="https://github.com/user-attachments/assets/a613cf04-250f-435b-8ebf-b403bb4da069" />
<img width="552" height="583" alt="Screenshot 2026-05-22 212723" src="https://github.com/user-attachments/assets/0f354c20-c305-47db-947c-f6d690a8260d" />
<img width="526" height="581" alt="Screenshot 2026-05-22 212745" src="https://github.com/user-attachments/assets/f4cefb3d-e083-429b-a0ef-35fe3dba9eff" />
<img width="477" height="350" alt="Screenshot 2026-05-22 212813" src="https://github.com/user-attachments/assets/934d1cc3-4004-42c7-9e42-dd8554346f7c" />
<img width="241" height="119" alt="Screenshot 2026-05-22 212833" src="https://github.com/user-attachments/assets/c346dc78-08c7-4663-9d5f-b186e6085a94" />
<img width="720" height="342" alt="Screenshot 2026-05-22 212901" src="https://github.com/user-attachments/assets/f2b504a2-439a-4e3f-8282-5aeccd5b4140" />
<img width="631" height="655" alt="Screenshot 2026-05-22 212932" src="https://github.com/user-attachments/assets/9e5b1545-59d5-4516-b587-90011dc6e2eb" />
<img width="404" height="450" alt="Screenshot 2026-05-22 212956" src="https://github.com/user-attachments/assets/66ae7854-f3a0-4b12-9114-7a7d0d6dcf71" />


heights.csv
```

import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt


df = pd.read_csv('heights.csv')
print(df.head(),"\n")

df.info()
print()

print(df.describe(),"\n")

df.isnull()
print(df.isnull().sum())
print()

df_fill_0 = df.fillna(0)
print(df_fill_0,"\n")

df_ffill = df.ffill()
print(df_ffill,"\n")

df_bfill = df.bfill()
print(df_bfill,"\n")

df['height'] = df['height'].fillna(df['height'].mean())
print(df,"\n")

df_dropna = df.dropna()
print(df_dropna,"\n")

sns.boxplot(x=df['height'])
plt.show()
print()

Q1 = df['height'].quantile(0.25)
Q3 = df['height'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR,"\n")

outliers_iqr = df[
    (df['height'] < (Q1 - 1.5 * IQR)) |
    (df['height'] > (Q3 + 1.5 * IQR))
]
print(outliers_iqr,"\n")

ir_cleaned = df[
    ~((df['height'] < (Q1 - 1.5 * IQR)) |
      (df['height'] > (Q3 + 1.5 * IQR)))
]
print(ir_cleaned,"\n")

df_z = df['height']

z_scores = np.abs(stats.zscore(df_z))
print(z_scores,"\n")

threshold = 3
outliers_z = df_z[z_scores > threshold]
print("Outliers:",outliers_z,"\n")
     
df_z_cleaned = df_z[z_scores <= threshold]
print(df_z_cleaned,"\n")

```
<img width="345" height="275" alt="Screenshot 2026-05-22 213801" src="https://github.com/user-attachments/assets/50aeeb82-ca74-4848-b274-f5ee80108dc1" />
<img width="260" height="470" alt="Screenshot 2026-05-22 213830" src="https://github.com/user-attachments/assets/b5318487-cc64-455d-999e-ede9d393e9e1" />
<img width="224" height="523" alt="Screenshot 2026-05-22 213954" src="https://github.com/user-attachments/assets/964fc3f0-6e81-45e1-b1df-8404932fb9b6" />
<img width="257" height="506" alt="Screenshot 2026-05-22 214017" src="https://github.com/user-attachments/assets/7b824179-243d-406c-a7b0-36ba4e2f38a7" />
<img width="553" height="404" alt="Screenshot 2026-05-22 214036" src="https://github.com/user-attachments/assets/17d368e0-f038-4c5b-a81c-9bea6a94cc13" />
<img width="298" height="267" alt="Screenshot 2026-05-22 214102" src="https://github.com/user-attachments/assets/0be20b9b-21ed-4bbe-bbc2-20fc5e4ddeab" />
<img width="364" height="769" alt="Screenshot 2026-05-22 214140" src="https://github.com/user-attachments/assets/0b9dffed-959f-442c-8400-43d537e6712b" />


iris.csv
```

import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt


df = pd.read_csv('iris.csv')
print(df.head(),"\n")

df.info()
print()

print(df.describe(),"\n")

df.isnull()
print(df.isnull().sum())
print()

df_fill_0 = df.fillna(0)
print(df_fill_0,"\n")

df_ffill = df.ffill()
print(df_ffill,"\n")

df_bfill = df.bfill()
print(df_bfill,"\n")

df['sepal_length'] = df['sepal_length'].fillna(df['sepal_length'].mean())
print(df,"\n")

df_dropna = df.dropna()
print(df_dropna,"\n")

sns.boxplot(x=df['sepal_width'])
plt.show()
print()

Q1 = df['sepal_width'].quantile(0.25)
Q3 = df['sepal_width'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR,"\n")

outliers_iqr = df[
    (df['sepal_width'] < (Q1 - 1.5 * IQR)) |
    (df['sepal_width'] > (Q3 + 1.5 * IQR))
]
print(outliers_iqr,"\n")

ir_cleaned = df[
    ~((df['sepal_width'] < (Q1 - 1.5 * IQR)) |
      (df['sepal_width'] > (Q3 + 1.5 * IQR)))
]
print(ir_cleaned,"\n")

df_z = df['sepal_width']

z_scores = np.abs(stats.zscore(df_z))
print(z_scores,"\n")

threshold = 3
outliers_z = df_z[z_scores > threshold]
print("Outliers:",outliers_z,"\n")
     
df_z_cleaned = df_z[z_scores <= threshold]
print(df_z_cleaned,"\n")
```
<img width="536" height="473" alt="Screenshot 2026-05-22 214516" src="https://github.com/user-attachments/assets/4cee5bc3-1671-4235-a35e-4c8c4c25d320" />
<img width="538" height="356" alt="Screenshot 2026-05-22 214539" src="https://github.com/user-attachments/assets/c1ad66f2-532f-489c-9077-ab4214d37e95" />
<img width="590" height="470" alt="Screenshot 2026-05-22 214555" src="https://github.com/user-attachments/assets/57925508-0b75-48a9-9c3b-69cb72c45e53" />
<img width="590" height="485" alt="Screenshot 2026-05-22 214611" src="https://github.com/user-attachments/assets/54072d51-ccf7-4646-8ae6-48c89d6422d4" />
<img width="568" height="431" alt="Screenshot 2026-05-22 214626" src="https://github.com/user-attachments/assets/1bab1cc5-c4d5-406a-ac03-4f3b48d356f8" />
<img width="554" height="310" alt="Screenshot 2026-05-22 214644" src="https://github.com/user-attachments/assets/27c9699c-a4df-44da-975d-1aa67a97cea5" />
<img width="599" height="712" alt="Screenshot 2026-05-22 214806" src="https://github.com/user-attachments/assets/fc6c9214-84f7-4765-9dc7-cdb7a6ffa2b3" />


# Result
The given data has been successfully read, cleaned by handling duplicates and missing values, and saved to a new file named cleaned_data.csv.
