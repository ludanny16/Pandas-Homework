
# PyCity Schools Analysis

Trend 1 Regardless of School Type, high school students perform better on Reading than Math.

Trend 2 Charter School overall have better performance than District School.

Trend 3 When comparing to large size school, small size school have higher passing percentage rate.

# Part I


```python
# Import Pandas module
import pandas as pd
```


```python
# load CSV
schools = "schools_complete.csv"
students = "students_complete.csv"
```


```python
# Read with pandas--low_memory required to suppress errors about mixed data types
schools_pd = pd.read_csv(schools, encoding='iso-8859-1', low_memory=False)
```


```python
# Read with pandas--low_memory required to suppress errors about mixed data types/student csv
students_pd= pd.read_csv(students, encoding='iso-8859-1', low_memory=False)
```


```python
# Inspect all columns for schools
schools_pd.columns
```




    Index(['School ID', 'name', 'type', 'size', 'budget'], dtype='object')




```python
#rename school csv column
schools_pd = schools_pd.rename(columns={"name":"School Name",
                                       "type":"School Type",
                                       "size":"School Size",
                                       "budget":"Budget"})
schools_pd.columns
```




    Index(['School ID', 'School Name', 'School Type', 'School Size', 'Budget'], dtype='object')




```python
# Inspect all columns for students
students_pd.columns
```




    Index(['Student ID', 'name', 'gender', 'grade', 'school', 'reading_score',
           'math_score'],
          dtype='object')




```python
#rename student csv column
students_pd = students_pd.rename(columns={"name":"Student Name",
                                       "gender":"Gender",
                                       "grade":"Grade",
                                       "school":"School Name",
                                       "reading_score":"Reading Score",
                                        "math_score":"Math Score"})
students_pd.columns
```




    Index(['Student ID', 'Student Name', 'Gender', 'Grade', 'School Name',
           'Reading Score', 'Math Score'],
          dtype='object')




```python
# Performing an inner merge on the two dataframes, using the "School Name" field
inner_merge_df = pd.merge(schools_pd, students_pd, on="School Name")
inner_merge_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>School Name</th>
      <th>School Type</th>
      <th>School Size</th>
      <th>Budget</th>
      <th>Student ID</th>
      <th>Student Name</th>
      <th>Gender</th>
      <th>Grade</th>
      <th>Reading Score</th>
      <th>Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
#total school count in District
type_df = inner_merge_df.groupby("School Type")
d_school_df = type_df["School Name"].nunique()
d_school_df
```




    School Type
    Charter     8
    District    7
    Name: School Name, dtype: int64




```python
# total students in district school
inner_merge_df['School Type'].value_counts()
```




    District    26976
    Charter     12194
    Name: School Type, dtype: int64




```python
# count number of total students
inner_merge_df['Student Name'].count()
```




    39170




```python
# Calculate the number of unique schools in the DataFrame
school_count = len(inner_merge_df['School Name'].unique())
school_count
```




    15




```python
# Show only District type school
District = "District"
district_school_df = inner_merge_df.loc[inner_merge_df["School Type"] == District]
district_school_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>School Name</th>
      <th>School Type</th>
      <th>School Size</th>
      <th>Budget</th>
      <th>Student ID</th>
      <th>Student Name</th>
      <th>Gender</th>
      <th>Grade</th>
      <th>Reading Score</th>
      <th>Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calculate total budget
total_d_budget=district_school_df['Budget'].unique().sum()
total_d_budget
```




    17347923




```python
# Calculate total district school
u_district_school_df=len(district_school_df['School Name'].value_counts())
u_district_school_df
```




    7




```python
# Calculate average reading score
average_Reading_Score = district_school_df['Reading Score'].mean()
average_Reading_Score
```




    80.96248517200475




```python
# Calculate average math score
average_Math_Score = district_school_df['Math Score'].mean()
average_Math_Score
```




    76.98702550415184




```python
# Calculate how many student
total_student = district_school_df["Reading Score"].count()
print(total_student)
```

    26976



```python
# Calculate number of student passing reading
percentage_r=(district_school_df["Reading Score"] >=70).value_counts()
percentage_r
```




    True     21825
    False     5151
    Name: Reading Score, dtype: int64




```python
# change it into dataframe
percentage_rd = pd.DataFrame(percentage_r)
percentage_rd1=percentage_rd.reset_index()
pass_r=percentage_rd1.drop(percentage_rd1.index[1])
pass_r
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>True</td>
      <td>21825</td>
    </tr>
  </tbody>
</table>
</div>




```python
#define number of passing student
pass_num=21825
print(pass_num)
```

    21825



```python
# Calculate percentage of student passing reading
passing_percentage_r=(pass_num/total_student)*100
passing_percentage_r
```




    80.905249110320284




```python
# Calculate number of student passing Math
percentage_m=(district_school_df["Math Score"] >=70).value_counts()
percentage_m
```




    True     17944
    False     9032
    Name: Math Score, dtype: int64




```python
# change it into dataframe
percentage_md = pd.DataFrame(percentage_m)
percentage_md1=percentage_md.reset_index()
pass_m=percentage_md1.drop(percentage_md1.index[1])
pass_m
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>True</td>
      <td>17944</td>
    </tr>
  </tbody>
</table>
</div>




```python
#define number of passing student
pass_num_m=17944
print(pass_num_m)
```

    17944



```python
# Calculate percentage of student passing math
passing_percentage_m=(pass_num_m/total_student)*100
passing_percentage_m
```




    66.518386714116247




```python
# Calculate overalll passing percentage
overall_percentage=(passing_percentage_r+passing_percentage_m)/2
overall_percentage
```




    73.711817912218265




```python
# Create a new table consolodating above calculations
district_summary = pd.DataFrame({"Total School": [u_district_school_df],
                                   "Total Student": [total_student],
                                   "Total Budget": [total_d_budget],
                                   "Avg. Math Score": [average_Math_Score],
                                   "Avg. Reading Score": [average_Reading_Score],
                                   "% Passing Math":[passing_percentage_m],
                                   "% Passing Reading":[passing_percentage_r],
                                   "% Overall Passing Rate": [overall_percentage]
})
district_summary = district_summary[["Total School", 
                                         "Total Student", 
                                         "Total Budget", 
                                         "Avg. Math Score", 
                                         "Avg. Reading Score", 
                                         "% Passing Math", 
                                         "% Passing Reading",
                                         "% Overall Passing Rate"]]
district_summary = district_summary.round(2)

```

# Disctrict Summary


```python
# Improve formatting before outputting spreadsheet
district_summary["Total Budget"] = district_summary["Total Budget"].map("${0:,.0f}".format)
district_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total School</th>
      <th>Total Student</th>
      <th>Total Budget</th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>26976</td>
      <td>$17,347,923</td>
      <td>76.99</td>
      <td>80.96</td>
      <td>66.52</td>
      <td>80.91</td>
      <td>73.71</td>
    </tr>
  </tbody>
</table>
</div>



# Part II


```python
# load only specific columns
cut_school_df=inner_merge_df.iloc[:,1:5]
```


```python
# remove duplicates on row
total_school_df=cut_school_df.drop_duplicates(['School Name'], keep='last')
```


```python
# Check Cloumn Index
total_school_df.columns
```




    Index(['School Name', 'School Type', 'School Size', 'Budget'], dtype='object')




```python
# Rename Cloumn Index
total_school_df = total_school_df.rename(columns={'Budget':'Total School Budget'
                                       })
total_school_df.columns
```




    Index(['School Name', 'School Type', 'School Size', 'Total School Budget'], dtype='object')




```python
# Reset index
total_school_df = total_school_df.reset_index(drop=True)
```


```python
# Calculate Per Student Budget
total_school_df['Per Student Budget'] = (total_school_df['Total School Budget'] / total_school_df['School Size'])
```


```python
# Calculate Mean and Reset index for Reading 
high_school_df = inner_merge_df.groupby("School Name")
sum_reading_school_df = pd.DataFrame(high_school_df["Reading Score"].mean())
sum_reading_school_df = sum_reading_school_df.reset_index()
```


```python
# Calculate Mean and Reset index for Math
high_school_df = inner_merge_df.groupby("School Name")
sum_math_school_df = pd.DataFrame(high_school_df["Math Score"].mean())
sum_math_school_df = sum_math_school_df.reset_index()
```


```python
# Join AVG Reading and Math score table
new_school_merge_df = pd.merge(total_school_df, sum_reading_school_df, on="School Name")
```


```python
# Join AVG Reading and Math score table
new2_school_merge_df = pd.merge(new_school_merge_df, sum_math_school_df, on="School Name")
```


```python
# Count pass score >= 70
percentage_r_all=(inner_merge_df['Reading Score'] >=70).value_counts()
percentage_r_all
```




    True     33610
    False     5560
    Name: Reading Score, dtype: int64




```python
# Count pass score >= 70
percentage_m_all=(inner_merge_df["Math Score"] >=70).value_counts()
percentage_m_all
```




    True     29370
    False     9800
    Name: Math Score, dtype: int64




```python
# Group by School Name
new_df= inner_merge_df.groupby("School Name")
total_unique = pd.DataFrame(new_df["Math Score"].value_counts())
```


```python
#rename
math_work = total_unique.rename(columns={"Math Score":"Num of Student"})
```


```python
#reset index
math_work = math_work.reset_index()
```


```python
#Sum of passing student per school
pass_0 = math_work[math_work['Math Score']>=70].groupby(['School Name']).sum()
```


```python
#Drop column and reset index
pass_01=pass_0.drop('Math Score', axis=1)
pass_02=pass_01.reset_index()
```


```python
#Merge Table
new3_school_merge_df = pd.merge(new2_school_merge_df, pass_02, on="School Name")
```


```python
# Calculate %Passing and create new column
new3_school_merge_df['% Passing Math'] = (new3_school_merge_df['Num of Student'] / new3_school_merge_df['School Size'])*100
```


```python
# Group by School Name
new_df= inner_merge_df.groupby("School Name")
total_unique_r = pd.DataFrame(new_df["Reading Score"].value_counts())
```


```python
# rename, reset index and sum of passing student per school
reading_work = total_unique_r.rename(columns={"Reading Score":"Num of Student_R"})
reading_work = reading_work.reset_index()
rpass_0 = reading_work[reading_work['Reading Score']>=70].groupby(['School Name']).sum()
```


```python
# drop column, reset index and merge new table
rpass_01=rpass_0.drop('Reading Score', axis=1)
rpass_02=rpass_01.reset_index()
new4_school_merge_df = pd.merge(new3_school_merge_df, rpass_02, on="School Name")
```


```python
# Calculate %Passing and create new column
new4_school_merge_df['% Passing Reading'] = (new4_school_merge_df['Num of Student_R'] / new4_school_merge_df['School Size'])*100
```


```python
# Calculate overall %Passing and create new column
new4_school_merge_df['% Overall Passing'] = ((new4_school_merge_df['% Passing Math']+new4_school_merge_df['% Passing Reading'])/2)
```


```python
# Rename Column
new5_school_merge_df = new4_school_merge_df.rename(columns={"Reading Score":"Average Reading Score",
                                       "Math Score":"Average Math Score"})
new5_school_merge_df.columns
```




    Index(['School Name', 'School Type', 'School Size', 'Total School Budget',
           'Per Student Budget', 'Average Reading Score', 'Average Math Score',
           'Num of Student', '% Passing Math', 'Num of Student_R',
           '% Passing Reading', '% Overall Passing'],
          dtype='object')




```python
# Drop Column
school_01=new5_school_merge_df.drop('Num of Student', axis=1)
school_02=school_01.drop('Num of Student_R', axis=1)
```

# School Summary


```python
# School Summary
school_02.set_index('School Name')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>School Size</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Name</th>
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
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
  </tbody>
</table>
</div>



# Part III

# Top Performing Schools (By Passing Rate)


```python
# set index to School Name
result = school_02.set_index('School Name')
```


```python
# sorting
top_result = result.sort_values(by='% Overall Passing', ascending=0)
top_result.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>School Size</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Name</th>
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
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
  </tbody>
</table>
</div>



# Bottom Performing Schools (By Passing Rate)


```python
# sorting
bottom_result = result.sort_values(by='% Overall Passing')
bottom_result.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>School Size</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Name</th>
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
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
  </tbody>
</table>
</div>




# Reading Scores by Grade


```python
# Group by
new2_df= inner_merge_df.groupby(["School Name","Grade"])
total_unique_r1 = pd.DataFrame(new2_df["Reading Score"].mean())
```


```python
# reset index
total_unique_r2=total_unique_r1.reset_index()
```


```python
# change row and column
total_unique_r3 = total_unique_r2.pivot_table('Reading Score', ['School Name'], 'Grade')
```


```python
# rearrange column
cols = total_unique_r3.columns.tolist()
cols
```




    ['10th', '11th', '12th', '9th']




```python
# rearrange column
cols = cols[-1:] + cols[:-1]
cols
```




    ['9th', '10th', '11th', '12th']




```python
# Reading Scores by Grade
total_unique_r3= total_unique_r3[cols]
total_unique_r3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Grade</th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>



# Math Scores by Grade


```python
# Group by, calculate mean, reset index, change column and row, rearrange column
new2_df= inner_merge_df.groupby(["School Name","Grade"])
total_unique_m1 = pd.DataFrame(new2_df["Math Score"].mean())
total_unique_m2 = total_unique_m1.reset_index()
total_unique_m3 = total_unique_m2.pivot_table('Math Score', ['School Name'], 'Grade')
cols = total_unique_m3.columns.tolist()
cols = cols[-1:] + cols[:-1]
total_unique_m3= total_unique_m3[cols]
total_unique_m3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Grade</th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Spending



```python
# Rename
Spending= result.rename(columns={"Per Student Budget":"Budget(Per Student)"})
```


```python
# Create bins and bin labels for the Budget column

hp_bins = [0,585, 615, 645, 675]
hp_labels = ["<$585", "$585-615", "$615-645", "$645-675"]
pd.cut(Spending["Budget(Per Student)"], hp_bins, labels=hp_labels)
```




    School Name
    Huang High School        $645-675
    Figueroa High School     $615-645
    Shelton High School      $585-615
    Hernandez High School    $645-675
    Griffin High School      $615-645
    Wilson High School          <$585
    Cabrera High School         <$585
    Bailey High School       $615-645
    Holden High School          <$585
    Pena High School         $585-615
    Wright High School          <$585
    Rodriguez High School    $615-645
    Johnson High School      $645-675
    Ford High School         $615-645
    Thomas High School       $615-645
    Name: Budget(Per Student), dtype: category
    Categories (4, object): [<$585 < $585-615 < $615-645 < $645-675]




```python
#append bins
Spending["Spending Ranges (Per Student)"] = pd.cut(Spending["Budget(Per Student)"], hp_bins, labels=hp_labels)
```


```python
# Scores by School Spending
grouped_b_df = Spending.groupby("Spending Ranges (Per Student)")
grouped_b_df["Average Reading Score", "Average Math Score", "% Passing Math", 
             "% Passing Reading", "% Overall Passing"].mean()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.933814</td>
      <td>83.455399</td>
      <td>93.460096</td>
      <td>96.610877</td>
      <td>95.035486</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.885211</td>
      <td>83.599686</td>
      <td>94.230858</td>
      <td>95.900287</td>
      <td>95.065572</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>81.891436</td>
      <td>79.079225</td>
      <td>75.668212</td>
      <td>86.106569</td>
      <td>80.887391</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>81.027843</td>
      <td>76.997210</td>
      <td>66.164813</td>
      <td>81.133951</td>
      <td>73.649382</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Size


```python
# Create bins and bin labels for the School Size column

hp_bins = [0,1000, 2000, 5000]
hp_labels = ["Small(<1000)", "Medium(1000-2000)", "Large(2000-5000)"]
pd.cut(Spending["School Size"], hp_bins, labels=hp_labels)
```




    School Name
    Huang High School         Large(2000-5000)
    Figueroa High School      Large(2000-5000)
    Shelton High School      Medium(1000-2000)
    Hernandez High School     Large(2000-5000)
    Griffin High School      Medium(1000-2000)
    Wilson High School        Large(2000-5000)
    Cabrera High School      Medium(1000-2000)
    Bailey High School        Large(2000-5000)
    Holden High School            Small(<1000)
    Pena High School              Small(<1000)
    Wright High School       Medium(1000-2000)
    Rodriguez High School     Large(2000-5000)
    Johnson High School       Large(2000-5000)
    Ford High School          Large(2000-5000)
    Thomas High School       Medium(1000-2000)
    Name: School Size, dtype: category
    Categories (3, object): [Small(<1000) < Medium(1000-2000) < Large(2000-5000)]




```python
#append bins
Spending["School Size"] = pd.cut(Spending["School Size"], hp_bins, labels=hp_labels)
```


```python
#Scores by School Size
grouped_s1_Spending_df = Spending.groupby("School Size")
grouped_s1_Spending_df[["Average Reading Score", "Average Math Score", "% Passing Math", "% Passing Reading",
                        "% Overall Passing" ]].mean()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small(&lt;1000)</th>
      <td>83.929843</td>
      <td>83.821598</td>
      <td>93.550225</td>
      <td>96.099437</td>
      <td>94.824831</td>
    </tr>
    <tr>
      <th>Medium(1000-2000)</th>
      <td>83.864438</td>
      <td>83.374684</td>
      <td>93.599695</td>
      <td>96.790680</td>
      <td>95.195187</td>
    </tr>
    <tr>
      <th>Large(2000-5000)</th>
      <td>81.344493</td>
      <td>77.746417</td>
      <td>69.963361</td>
      <td>82.766634</td>
      <td>76.364998</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Type


```python
#Scores by School Type
grouped_s2_Spending_df = Spending.groupby("School Type")
grouped_s2_Spending_df[["Average Reading Score", "Average Math Score", "% Passing Math", "% Passing Reading",
                        "% Overall Passing" ]].mean()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.896421</td>
      <td>83.473852</td>
      <td>93.620830</td>
      <td>96.586489</td>
      <td>95.103660</td>
    </tr>
    <tr>
      <th>District</th>
      <td>80.966636</td>
      <td>76.956733</td>
      <td>66.548453</td>
      <td>80.799062</td>
      <td>73.673757</td>
    </tr>
  </tbody>
</table>
</div>



# END
