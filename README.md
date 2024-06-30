# DAL 
Developed a predictive model for hill and valley detection using the Logistic Regression method. 
This dataset was taken from the StatLib.library which is maintained 
This is entirely done on Google Colab

Import library
[ ]
import pandas as pd
[ ]
import numpy as np
Import data

[ ]
df = pd.read_csv('https://github.com/YBI-Foundation/Dataset/raw/main/Hill%20Valley%20Dataset.csv')
[ ]
df.head()

[ ]
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1212 entries, 0 to 1211
Columns: 101 entries, V1 to Class
dtypes: float64(100), int64(1)
memory usage: 956.5 KB
Describe data

[ ]
df.describe()

Data Visualization

[ ]
df.columns
Index(['V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V8', 'V9', 'V10',
       ...
       'V92', 'V93', 'V94', 'V95', 'V96', 'V97', 'V98', 'V99', 'V100',
       'Class'],
      dtype='object', length=101)
[ ]
print(df.columns.tolist())
['V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V8', 'V9', 'V10', 'V11', 'V12', 'V13', 'V14', 'V15', 'V16', 'V17', 'V18', 'V19', 'V20', 'V21', 'V22', 'V23', 'V24', 'V25', 'V26', 'V27', 'V28', 'V29', 'V30', 'V31', 'V32', 'V33', 'V34', 'V35', 'V36', 'V37', 'V38', 'V39', 'V40', 'V41', 'V42', 'V43', 'V44', 'V45', 'V46', 'V47', 'V48', 'V49', 'V50', 'V51', 'V52', 'V53', 'V54', 'V55', 'V56', 'V57', 'V58', 'V59', 'V60', 'V61', 'V62', 'V63', 'V64', 'V65', 'V66', 'V67', 'V68', 'V69', 'V70', 'V71', 'V72', 'V73', 'V74', 'V75', 'V76', 'V77', 'V78', 'V79', 'V80', 'V81', 'V82', 'V83', 'V84', 'V85', 'V86', 'V87', 'V88', 'V89', 'V90', 'V91', 'V92', 'V93', 'V94', 'V95', 'V96', 'V97', 'V98', 'V99', 'V100', 'Class']
Data Preprocessing

[ ]
df.shape
(1212, 101)
[ ]
df['Class'].value_counts()
0    606
1    606
Name: Class, dtype: int64
[ ]
df.groupby('Class').mean()

Define Target variable(y)

[ ]
y = df['Class']
[ ]
y.shape
(1212,)
[ ]
y
0       0
1       1
2       1
3       0
4       0
       ..
1207    1
1208    0
1209    1
1210    1
1211    0
Name: Class, Length: 1212, dtype: int64
Define Feature variable(X)

[ ]
X = df[['V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V8', 'V9', 'V10', 'V11', 'V12', 'V13', 'V14', 'V15', 'V16', 'V17', 'V18', 'V19', 'V20', 'V21', 'V22', 'V23', 'V24', 'V25', 'V26', 'V27', 'V28', 'V29', 'V30', 'V31', 'V32', 'V33', 'V34', 'V35', 'V36', 'V37', 'V38', 'V39', 'V40', 'V41', 'V42', 'V43', 'V44', 'V45', 'V46', 'V47', 'V48', 'V49', 'V50', 'V51', 'V52', 'V53', 'V54', 'V55', 'V56', 'V57', 'V58', 'V59', 'V60', 'V61', 'V62', 'V63', 'V64', 'V65', 'V66', 'V67', 'V68', 'V69', 'V70', 'V71', 'V72', 'V73', 'V74', 'V75', 'V76', 'V77', 'V78', 'V79', 'V80', 'V81', 'V82', 'V83', 'V84', 'V85', 'V86', 'V87', 'V88', 'V89', 'V90', 'V91', 'V92', 'V93', 'V94', 'V95', 'V96', 'V97', 'V98', 'V99', 'V100']]
[ ]
X = df.drop('Class', axis = 1)
[ ]
X.shape
(1212, 100)
[ ]
X

Import Train Test Split

[ ]
from sklearn.model_selection import train_test_split
[ ]
X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=0.3, stratify = y, random_state=2529)
[ ]
X_train.shape, X_test.shape, y_train.shape, y_test.shape
((848, 100), (364, 100), (848,), (364,))
Modelling

[ ]
from sklearn.linear_model import LogisticRegression
[ ]
lr = LogisticRegression()
Model Evaluation

[ ]
lr.fit(X_train, y_train)

Prediction

[ ]
y_pred = lr.predict(X_test)
[ ]
y_pred.shape
(364,)
[ ]
y_pred
array([0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1,
       0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1,
       0, 1, 1, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, 1,
       0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0,
       1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 1, 1,
       1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0,
       0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0,
       0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1,
       0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 1,
       1, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1,
       0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1,
       0, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0,
       1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0,
       1, 1, 1, 0, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0,
       1, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0, 0,
       0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 1, 0, 0, 0,
       0, 1, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1])
[ ]
lr.predict_proba(X_test)
array([[1.00000000e+000, 9.79892438e-084],
       [1.44980731e-007, 9.99999855e-001],
       [1.00000000e+000, 2.10296309e-117],
       [1.17920074e-003, 9.98820799e-001],
       [3.82913563e-002, 9.61708644e-001],
       [6.34551814e-001, 3.65448186e-001],
       [2.38041494e-001, 7.61958506e-001],
       [1.00000000e+000, 3.92122501e-262],
       [9.85433421e-001, 1.45665790e-002],
       [9.95262593e-001, 4.73740668e-003],
       [3.31102876e-002, 9.66889712e-001],
       [9.99999960e-001, 3.97297756e-008],
       [1.00000000e+000, 0.00000000e+000],
       [9.94685028e-001, 5.31497227e-003],
       [1.00000000e+000, 9.75775486e-030],
       [1.00000000e+000, 0.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [3.80894701e-002, 9.61910530e-001],
       [4.29245109e-001, 5.70754891e-001],
       [5.25543081e-001, 4.74456919e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [5.28184881e-001, 4.71815119e-001],
       [0.00000000e+000, 1.00000000e+000],
       [6.33165320e-001, 3.66834680e-001],
       [4.30569599e-003, 9.95694304e-001],
       [7.23053445e-001, 2.76946555e-001],
       [1.80871375e-008, 9.99999982e-001],
       [4.81787277e-001, 5.18212723e-001],
       [2.13833626e-002, 9.78616637e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 1.44264516e-012],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 0.00000000e+000],
       [5.22413478e-001, 4.77586522e-001],
       [5.02749688e-001, 4.97250312e-001],
       [5.19258270e-001, 4.80741730e-001],
       [4.00169445e-001, 5.99830555e-001],
       [9.99999988e-001, 1.22625206e-008],
       [1.00000000e+000, 5.00751650e-084],
       [4.75058982e-001, 5.24941018e-001],
       [1.00000000e+000, 6.51229539e-022],
       [0.00000000e+000, 1.00000000e+000],
       [7.75814297e-006, 9.99992242e-001],
       [1.00000000e+000, 1.61665320e-030],
       [0.00000000e+000, 1.00000000e+000],
       [2.36476476e-001, 7.63523524e-001],
       [3.26827010e-010, 1.00000000e+000],
       [9.58715329e-011, 1.00000000e+000],
       [6.27568416e-001, 3.72431584e-001],
       [5.10889158e-001, 4.89110842e-001],
       [1.00000000e+000, 7.10243398e-052],
       [4.10852494e-001, 5.89147506e-001],
       [7.84805272e-003, 9.92151947e-001],
       [1.00000000e+000, 2.91454899e-013],
       [4.42946941e-001, 5.57053059e-001],
       [4.94325797e-001, 5.05674203e-001],
       [4.06990731e-001, 5.93009269e-001],
       [1.00000000e+000, 3.92771256e-133],
       [0.00000000e+000, 1.00000000e+000],
       [2.60758044e-006, 9.99997392e-001],
       [4.73794282e-001, 5.26205718e-001],
       [4.85916253e-001, 5.14083747e-001],
       [0.00000000e+000, 1.00000000e+000],
       [9.73310025e-001, 2.66899752e-002],
       [4.35935728e-001, 5.64064272e-001],
       [1.00000000e+000, 3.16309649e-083],
       [0.00000000e+000, 1.00000000e+000],
       [5.47146569e-001, 4.52853431e-001],
       [0.00000000e+000, 1.00000000e+000],
       [7.81748402e-001, 2.18251598e-001],
       [4.96715479e-001, 5.03284521e-001],
       [9.99796291e-001, 2.03709367e-004],
       [2.87095651e-001, 7.12904349e-001],
       [9.33634962e-001, 6.63650377e-002],
       [1.00000000e+000, 4.62565257e-131],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 0.00000000e+000],
       [1.00000000e+000, 3.03889065e-062],
       [4.59824170e-001, 5.40175830e-001],
       [5.09985517e-001, 4.90014483e-001],
       [1.22876861e-001, 8.77123139e-001],
       [0.00000000e+000, 1.00000000e+000],
       [4.59241598e-001, 5.40758402e-001],
       [1.50939924e-006, 9.99998491e-001],
       [5.15704004e-001, 4.84295996e-001],
       [8.66581013e-001, 1.33418987e-001],
       [4.63125347e-001, 5.36874653e-001],
       [1.34706626e-003, 9.98652934e-001],
       [1.00000000e+000, 0.00000000e+000],
       [5.13973370e-001, 4.86026630e-001],
       [9.97413706e-001, 2.58629387e-003],
       [1.00000000e+000, 3.49310807e-031],
       [4.90419681e-001, 5.09580319e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 1.09493221e-195],
       [5.45773338e-001, 4.54226662e-001],
       [1.00000000e+000, 6.88240287e-089],
       [1.00000000e+000, 6.44629434e-019],
       [4.44089210e-016, 1.00000000e+000],
       [1.00000000e+000, 7.33421093e-087],
       [8.10785227e-001, 1.89214773e-001],
       [5.26713582e-006, 9.99994733e-001],
       [1.00000000e+000, 0.00000000e+000],
       [3.58448291e-001, 6.41551709e-001],
       [4.81286566e-010, 1.00000000e+000],
       [4.89323001e-001, 5.10676999e-001],
       [9.56397036e-002, 9.04360296e-001],
       [0.00000000e+000, 1.00000000e+000],
       [3.25729914e-001, 6.74270086e-001],
       [7.53744722e-001, 2.46255278e-001],
       [5.50456221e-001, 4.49543779e-001],
       [1.00000000e+000, 2.62177266e-176],
       [0.00000000e+000, 1.00000000e+000],
       [2.12646204e-001, 7.87353796e-001],
       [1.06314514e-008, 9.99999989e-001],
       [1.00000000e+000, 0.00000000e+000],
       [1.00000000e+000, 4.07249673e-015],
       [9.97276047e-001, 2.72395324e-003],
       [0.00000000e+000, 1.00000000e+000],
       [5.33781304e-001, 4.66218696e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.62866438e-001, 4.37133562e-001],
       [5.61236343e-001, 4.38763657e-001],
       [3.98695153e-002, 9.60130485e-001],
       [9.99999114e-001, 8.86282112e-007],
       [9.64362956e-001, 3.56370445e-002],
       [1.00000000e+000, 5.06598485e-043],
       [1.87043776e-005, 9.99981296e-001],
       [1.00000000e+000, 9.30765770e-058],
       [8.20574118e-001, 1.79425882e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 2.29430314e-069],
       [4.20409967e-001, 5.79590033e-001],
       [9.99999993e-001, 6.94328018e-009],
       [4.50882397e-001, 5.49117603e-001],
       [0.00000000e+000, 1.00000000e+000],
       [3.99586281e-002, 9.60041372e-001],
       [4.72283847e-001, 5.27716153e-001],
       [1.00000000e+000, 3.04057517e-238],
       [6.00020540e-001, 3.99979460e-001],
       [9.92355338e-001, 7.64466237e-003],
       [6.91603994e-001, 3.08396006e-001],
       [1.00000000e+000, 5.78343357e-013],
       [4.98219918e-001, 5.01780082e-001],
       [1.00000000e+000, 0.00000000e+000],
       [6.13993450e-001, 3.86006550e-001],
       [5.25942153e-001, 4.74057847e-001],
       [4.47762272e-001, 5.52237728e-001],
       [5.24645958e-001, 4.75354042e-001],
       [1.00000000e+000, 0.00000000e+000],
       [5.24275850e-001, 4.75724150e-001],
       [5.17588835e-001, 4.82411165e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.18644778e-001, 4.81355222e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 3.11627120e-046],
       [9.99999999e-001, 7.82231601e-010],
       [5.40208711e-001, 4.59791289e-001],
       [1.00000000e+000, 0.00000000e+000],
       [9.99493139e-001, 5.06860936e-004],
       [9.34342960e-001, 6.56570398e-002],
       [3.86231859e-001, 6.13768141e-001],
       [1.00000000e+000, 4.93087857e-218],
       [1.00000000e+000, 1.93788307e-092],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 3.75738639e-018],
       [9.95846453e-001, 4.15354671e-003],
       [9.99997984e-001, 2.01576954e-006],
       [5.73323540e-001, 4.26676460e-001],
       [1.00000000e+000, 3.09913854e-242],
       [8.82419944e-001, 1.17580056e-001],
       [1.00000000e+000, 4.80333724e-070],
       [8.55115978e-012, 1.00000000e+000],
       [1.00000000e+000, 0.00000000e+000],
       [5.19285470e-001, 4.80714530e-001],
       [1.00000000e+000, 0.00000000e+000],
       [1.00000000e+000, 1.82788401e-065],
       [8.11300717e-001, 1.88699283e-001],
       [6.01802788e-001, 3.98197212e-001],
       [4.63623605e-001, 5.36376395e-001],
       [1.00000000e+000, 0.00000000e+000],
       [4.96494314e-001, 5.03505686e-001],
       [7.87576875e-001, 2.12423125e-001],
       [0.00000000e+000, 1.00000000e+000],
       [9.99999980e-001, 2.00926008e-008],
       [1.09338292e-003, 9.98906617e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.09770090e-001, 4.90229910e-001],
       [0.00000000e+000, 1.00000000e+000],
       [3.47100126e-012, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [4.58297030e-001, 5.41702970e-001],
       [8.27184300e-001, 1.72815700e-001],
       [1.00000000e+000, 1.39756991e-012],
       [3.30191510e-006, 9.99996698e-001],
       [1.43263759e-004, 9.99856736e-001],
       [4.95561832e-004, 9.99504438e-001],
       [5.22931414e-001, 4.77068586e-001],
       [1.00000000e+000, 1.18321730e-030],
       [1.00000000e+000, 4.51037216e-021],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [1.50549523e-001, 8.49450477e-001],
       [4.91293832e-001, 5.08706168e-001],
       [3.48512361e-001, 6.51487639e-001],
       [4.70615517e-001, 5.29384483e-001],
       [1.00000000e+000, 8.13524272e-076],
       [1.00000000e+000, 1.33577067e-143],
       [3.85562417e-001, 6.14437583e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 1.09385850e-186],
       [0.00000000e+000, 1.00000000e+000],
       [5.18506056e-001, 4.81493944e-001],
       [3.64168555e-001, 6.35831445e-001],
       [5.16228474e-001, 4.83771526e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [5.22178575e-001, 4.77821425e-001],
       [2.13505491e-007, 9.99999786e-001],
       [1.00000000e+000, 5.54172182e-223],
       [0.00000000e+000, 1.00000000e+000],
       [5.05802166e-001, 4.94197834e-001],
       [0.00000000e+000, 1.00000000e+000],
       [4.72021428e-001, 5.27978572e-001],
       [1.57739722e-001, 8.42260278e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.26869830e-001, 4.73130170e-001],
       [0.00000000e+000, 1.00000000e+000],
       [4.47176565e-001, 5.52823435e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [8.34001285e-001, 1.65998715e-001],
       [1.00000000e+000, 1.04751016e-022],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [2.73642469e-001, 7.26357531e-001],
       [7.96329942e-001, 2.03670058e-001],
       [0.00000000e+000, 1.00000000e+000],
       [2.33005017e-003, 9.97669950e-001],
       [1.00000000e+000, 0.00000000e+000],
       [1.11022302e-015, 1.00000000e+000],
       [4.34208851e-001, 5.65791149e-001],
       [9.99702529e-001, 2.97470851e-004],
       [1.00000000e+000, 1.04185015e-294],
       [1.90052202e-003, 9.98099478e-001],
       [1.27471981e-007, 9.99999873e-001],
       [5.14540398e-001, 4.85459602e-001],
       [5.27537237e-001, 4.72462763e-001],
       [0.00000000e+000, 1.00000000e+000],
       [4.06852730e-001, 5.93147270e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.04841348e-001, 4.95158652e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 1.94541000e-058],
       [5.10261222e-001, 4.89738778e-001],
       [4.79115611e-001, 5.20884389e-001],
       [7.70211184e-001, 2.29788816e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 1.68905018e-055],
       [3.59712260e-014, 1.00000000e+000],
       [5.16740257e-001, 4.83259743e-001],
       [7.72137342e-004, 9.99227863e-001],
       [1.71187086e-002, 9.82881291e-001],
       [4.23439380e-001, 5.76560620e-001],
       [5.04769519e-001, 4.95230481e-001],
       [1.00000000e+000, 1.62057426e-183],
       [4.92858827e-001, 5.07141173e-001],
       [2.21253726e-001, 7.78746274e-001],
       [3.91545588e-001, 6.08454412e-001],
       [9.99998914e-001, 1.08555734e-006],
       [5.45061325e-001, 4.54938675e-001],
       [2.58833001e-003, 9.97411670e-001],
       [0.00000000e+000, 1.00000000e+000],
       [4.54169441e-001, 5.45830559e-001],
       [1.00000000e+000, 0.00000000e+000],
       [4.84217991e-001, 5.15782009e-001],
       [4.54806553e-001, 5.45193447e-001],
       [4.64100426e-001, 5.35899574e-001],
       [4.81058143e-001, 5.18941857e-001],
       [1.00000000e+000, 8.26925871e-012],
       [9.40321597e-001, 5.96784032e-002],
       [9.30280788e-001, 6.97192124e-002],
       [9.99985537e-001, 1.44634314e-005],
       [4.86293495e-001, 5.13706505e-001],
       [4.83620879e-001, 5.16379121e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.18281205e-001, 4.81718795e-001],
       [9.60398281e-001, 3.96017192e-002],
       [8.82909189e-001, 1.17090811e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.04468116e-001, 4.95531884e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 1.97398402e-030],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [4.34564272e-001, 5.65435728e-001],
       [0.00000000e+000, 1.00000000e+000],
       [3.01242927e-001, 6.98757073e-001],
       [5.00275748e-001, 4.99724252e-001],
       [4.92565011e-001, 5.07434989e-001],
       [6.52830789e-009, 9.99999993e-001],
       [2.32227425e-003, 9.97677726e-001],
       [0.00000000e+000, 1.00000000e+000],
       [5.14616047e-001, 4.85383953e-001],
       [0.00000000e+000, 1.00000000e+000],
       [8.17351722e-002, 9.18264828e-001],
       [5.05428197e-001, 4.94571803e-001],
       [6.19886664e-001, 3.80113336e-001],
       [3.37263011e-005, 9.99966274e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [4.95515895e-001, 5.04484105e-001],
       [9.99473050e-001, 5.26950107e-004],
       [1.00000000e+000, 0.00000000e+000],
       [6.07083833e-001, 3.92916167e-001],
       [5.87437776e-001, 4.12562224e-001],
       [6.74626098e-001, 3.25373902e-001],
       [0.00000000e+000, 1.00000000e+000],
       [4.80435513e-001, 5.19564487e-001],
       [0.00000000e+000, 1.00000000e+000],
       [7.56738046e-001, 2.43261954e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [1.99840144e-015, 1.00000000e+000],
       [1.00000000e+000, 0.00000000e+000],
       [7.08044289e-001, 2.91955711e-001],
       [1.00000000e+000, 1.85797288e-263],
       [7.69182585e-001, 2.30817415e-001],
       [0.00000000e+000, 1.00000000e+000],
       [0.00000000e+000, 1.00000000e+000],
       [9.99968245e-001, 3.17551713e-005],
       [0.00000000e+000, 1.00000000e+000],
       [3.32923826e-001, 6.67076174e-001],
       [1.00000000e+000, 1.62314341e-015],
       [9.48752574e-001, 5.12474263e-002],
       [1.00000000e+000, 0.00000000e+000],
       [5.99059985e-001, 4.00940015e-001],
       [1.00000000e+000, 1.42930712e-022],
       [1.00000000e+000, 4.76450603e-283],
       [3.69432386e-001, 6.30567614e-001],
       [0.00000000e+000, 1.00000000e+000],
       [1.00000000e+000, 5.86623071e-289],
       [2.64316783e-006, 9.99997357e-001],
       [9.98722571e-001, 1.27742879e-003],
       [5.55240240e-007, 9.99999445e-001],
       [9.73949152e-001, 2.60508480e-002],
       [6.12533448e-001, 3.87466552e-001],
       [7.79811273e-001, 2.20188727e-001],
       [1.00000000e+000, 1.15872222e-051],
       [3.99680289e-015, 1.00000000e+000],
       [5.61000379e-001, 4.38999621e-001],
       [0.00000000e+000, 1.00000000e+000],
       [9.75329693e-004, 9.99024670e-001],
       [5.15104680e-001, 4.84895320e-001],
       [1.00000000e+000, 0.00000000e+000],
       [5.48029744e-001, 4.51970256e-001],
       [4.58225522e-001, 5.41774478e-001],
       [0.00000000e+000, 1.00000000e+000],
       [2.54686035e-001, 7.45313965e-001],
       [0.00000000e+000, 1.00000000e+000]])
Explaination
To predict a model to predict Hill and Valley using Logistic Regression method. The prediction model proposed deep learning algorithm which demonstrated better prediction accuracy and provided a quite systematic way for further analysis.
