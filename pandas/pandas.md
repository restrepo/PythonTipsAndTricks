## Pandas

### Data-Frames (`df`)
##### Drop duplicates:
<code>df.drop_duplicates(subset=['column_name']).reset_index(drop=True)</code>
#### False positive in `df.loc[row_index,col_indexer]`
<code>pd.options.mode.chained_assignment = None  # default='warn'</code>
#### drop colums
<code>
udea.drop(['dict_doi','match'],axis='columns')
</code>
#### Drop DF entries from a list of indices:
<code>df.drop(df.index[list(mi)]</code>
#### `df1` DataFrame with `df2` indexes
<code>if df1.shape[0]==df2.shape[0]: # df1.index!=df2.index
   df1.index=df2.index.values</code>
#### Rename columns of DF
<code>df.rename_axis({'OLD':'NEW'}, axis = 'columns')</code>
#### Rename index of DF
    
    df.rename(index={0:'hello',1:'world'})
    
#### Check duplicates of a DF
<code>df[df.duplicated()]</code>
or
<code>df[df.duplicated('column')]</code>
#### Changing columns inside function: pass always as `df.copy()`
If a df is passed as a function argument, a column change could propagate outsided the function. To avoid problems
pass a hard copy of the df to the function through `df.copy()`
#### Drop duplicate entries after manipulations
<code>df_all=df[df.duplicated('KEY',keep=False)]
df_unique=df.drop_duplicates('KEY')]
for i in df_unique.index:
    mtch=df[df['KEY']==df_all.loc[i,'KEY']
    if mctch.shape[0]:
       .....
</code>
#### Combine two Pandas dataframes with the same index
<code>pandas.concat([df1, df2], axis=1)</code>
#### df  query
<code>
from numpy.random import randn
from pandas import DataFrame
df = DataFrame(randn(10, 2), columns=list('ab'))
df.query('a > b')
df[df.a > df.b]  # same result as the previous expression</code>
#### Merge
<code>
import pandas as pd
l=pd.DataFrame()
l=l.append(pd.Series({'T':'A','W':10}),ignore_index=True)
l=l.append(pd.Series({'T':'B','W':1}),ignore_index=True)
r=pd.DataFrame()
r=r.append(pd.Series({'T':'A','S':2}),ignore_index=True)
r=r.append(pd.Series({'T':'C','S':1}),ignore_index=True)
print(l.merge(r,on='T',how='outer').fillna(0))
print('='*15)
print(l.merge(r,on='T',how='left').fillna(0))
print('='*15)
print(l.merge(r,on='T',how='right').fillna(0))
print('='*15)
print(l.merge(r,on='T',how='inner').fillna(0))
   T     W    S
0  A  10.0  2.0
1  B   1.0  0.0
2  C   0.0  1.0
===============
   T     W    S
0  A  10.0  2.0
1  B   1.0  0.0
===============
   T     W    S
0  A  10.0  2.0
1  C   0.0  1.0
===============
   T     W    S
0  A  10.0  2.0
</code>
