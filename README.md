# survival-analysis-_-use-2014-03-21-data
survival analysis: because EDW linked national death until 2014/03/21, only death status before that are reliable. I editted sql script from Anna, 
to get hf patients who are disagnosed as hf before 2014/03/21 by adding the following command: 

```
where df.HF_index_date< cast('20140321' as DATE)
```
get a new dataset to have hf patients diagnosed as hf before 20140309 only, there are 414 patients on this dataset, save the file on: 
"H:\limited HF Patients Cohort\Limited HF Patients Cohort CASES  Demographics_death_before_2014"
##set the followup time until 20140309, do survival analysis 

