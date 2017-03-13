# survival-analysis-_-use-2014-03-21-data
survival analysis: because EDW linked national death until 2014/03/21, only death status before that are reliable. I editted sql script from Anna, 
to get hf patients who are disagnosed as hf before 2014/03/21 by adding the following command: 

```
where df.HF_index_date< cast('20140321' as DATE)
```
get a new dataset to have hf patients diagnosed as hf before 20140309 only, there are 414 patients on this dataset, save the file on: 
"H:\limited HF Patients Cohort\Limited HF Patients Cohort CASES  Demographics_death_before_2014"
##set the followup time until 20140309, do survival analysis 
```
#survival analysis, set the end of study date till 2014-03-21
import os 
import pandas as pd 
import numpy as np 
os.chdir("H:\limited HF Patients Cohort")
df=pd.read_csv("LimitedHFPatientsCohortCASES _Demographics_death_before_2014.csv",header=None)
df.rename( columns={10:'dts'}, inplace=True)
df['end_dts']=np.repeat('2014-03-21 00:00:00',414,axis=0)
df['dts']=pd.to_datetime(df['dts'])
df['end_dts']=pd.to_datetime(df['end_dts'])
df[['dts','end_dts']].min(axis=1) #get the date that earlier date btw 2014-03-21 and death date 
df['datediff']=(pd.to_datetime(df['end_dts'])-pd.to_datetime(df[5])).dt.days
df['E']=np.where(pd.to_datetime(df['dts'])< pd.to_datetime(df['end_dts']),1,0)
df.rename(columns={'datediff':'T'},inplace=True)


#get phenotype membership file 
df1=pd.read_csv("HF-only_alpha_1.0_gamma_0.001_0.08_0.07-7.dat_patient_id.csv",header=None)
df1.columns=['group','mrd_id']
merge=pd.merge(df1,df2,how='inner',left_on='mrd_id',right_on=1)
```
