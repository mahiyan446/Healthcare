##  Hospital Admission Analysis

The two files are
• diabetic_data.csv
• IDs_mapping.csv

### Project Overview

 It includes over 50 features representing patient and hospital outcomes. Information was extracted from the database for encounters that satisfied the following criteria.
• It is an inpatient encounter (a hospital admission). It is a diabetic encounter, that is, one during which any kind of diabetes was entered to the
system as a diagnosis.
• The length of stay was at least 1 day and at most 14 days.
• Laboratory tests were performed during the encounter.
• Medications were administered during the encounter.

The data contains such attributes as patient number, race, gender, age, admission type, time
in hospital, medical specialty of admitting physician, number of lab tests performed, HbA1c test
result, diagnosis, number of medications, diabetic medications, 
number of outpatient, inpatient, and
emergency visits in the year before the hospitalization, etc.


### Data Source
The dataset was downloaded from the UCI ML repository. Since the URL changes frequently, if you
want to
https://archive.ics.uci.edu/ml/datasets/diabetes+130-us+hospitals+for+years+1999-2008


### Initial Exploration
* Total Records - 101,766
* Average Length of Stay - 4.39 days
* Total Discharges: 26,286

## 1. Genderwise Admission type

```sql
SELECT
  admission_type_id,
  MAX(CASE WHEN gender = 'Female' THEN total_patients END) AS female_total,
  MAX(CASE WHEN gender = 'Male' THEN total_patients END) AS male_total
FROM (
  SELECT
    admission_type_id,
    gender,
    COUNT(*) AS total_patients
  FROM diabetic_data
  GROUP BY admission_type_id, gender
) AS SourceTable
GROUP BY admission_type_id
ORDER BY admission_type_id;

```
### Results:
![image](https://github.com/mahiyan446/Healthcare/assets/138512359/ec37750e-afbe-4dff-bc9e-48adf403187e)


## 2. Finding Missing value in medical_speciality

```sql
select distinct medical_specialty ,
count(*) as total 
from diabetic_data 
where medical_specialty = '?'
group by  medical_specialty ;

```

Result: 

![image](https://github.com/mahiyan446/Healthcare/assets/138512359/022fc010-b171-4306-9ec5-67a5a9fac71b)

## 3. Counting which medical_speciality is Admitted the most
```sql
select medical_specialty,
count(*) as total_num
from diabetic_data 
group by medical_specialty 
order by  total_num desc ;

```
## Result
![image](https://github.com/mahiyan446/Healthcare/assets/138512359/9831e577-356e-402b-86c3-46d5937ed80e)


