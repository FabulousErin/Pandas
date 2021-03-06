# Pandas
Trusted
Jupyter Server: local
Python 3: Idle
[99]



#dependencies
import matplotlib.pyplot as plt
import sklearn.datasets as dta
from scipy import stats
import numpy as np
import pandas as pd
import scipy.stats as st
[100]



#store filepath in a variable
school_data_to_load = "schools_complete.csv"
student_data_to_load = "students_complete.csv"
[101]



#read datapath with pandas and display heading of school info
school=pd.read_csv(school_data_to_load)
school.head()
School ID	school_name	type	size	budget
0	0	Huang High School	District	2917	1910635
1	1	Figueroa High School	District	2949	1884411
2	2	Shelton High School	Charter	1761	1056600
3	3	Hernandez High School	District	4635	3022020
4	4	Griffin High School	Charter	1468	917500
[102]



#read datapath with pandas and display heading of student info
students=pd.read_csv(student_data_to_load)
students.head()
Student ID	student_name	gender	grade	school_name	reading_score	math_score
0	0	Paul Bradley	M	9th	Huang High School	66	79
1	1	Victor Smith	M	12th	Huang High School	94	61
2	2	Kevin Rodriguez	M	12th	Huang High School	90	60
3	3	Dr. Richard Scott	M	12th	Huang High School	67	58
4	4	Bonnie Ray	F	9th	Huang High School	97	84
[179]



#sum schools, students and budget
total_schools = len(school["school_name"].unique())
total_students = (students["Student ID"]).()
total_budget = sum(school["budget"])
#calculate students' average score on math and reading
avg_math = students[["math_score"]].mean()
avg_reading=students[["reading_score"]].mean()
total_students

39170
[186]



#create a dataframe for only students with math scores >= 65 for math and a data frame for only students with reading scores >= 65
mathpass_df = students.loc[students["math_score"] >= 65, :]
readpass_df = students.loc[students["reading_score"] >= 65, :]
students_math=mathpass_df.count()
students_read=readpass_df.count()
[188]



#sum the number of students with passing math scores and passing reading scores
mathpass_students=(mathpass_df["math_score"]).count()
readpass_students=(readpass_df["reading_score"]).count()
print(f"There are {mathpass_students} students passing math and {readpass_students} passing reading.")
There are 33188 students passing math and 37681 passing reading.
[195]



#calculate what percentage of students are passing math and reading
percent_math_pass = mathpass_students/total_students
percent_read_pass = readpass_students/total_students
print(f"There are {percent_math_pass*100}% students passing math and {percent_read_pass*100}% passing reading.")
There are 84.72810824610671% students passing math and 96.19862139392393% passing reading.
[197]



#create a datafram for only students passing BOTH math and reading, show heading
bothpass_df = students.loc[(students["math_score"] >=65) & (students["reading_score"] >=65)]
bothpass_df

Student ID	student_name	gender	grade	school_name	reading_score	math_score
0	0	Paul Bradley	M	9th	Huang High School	66	79
4	4	Bonnie Ray	F	9th	Huang High School	97	84
5	5	Bryan Miranda	M	9th	Huang High School	94	94
6	6	Sheena Carter	F	11th	Huang High School	82	80
7	7	Nicole Baker	F	12th	Huang High School	96	69
...	...	...	...	...	...	...	...
39165	39165	Donna Howard	F	12th	Thomas High School	99	90
39166	39166	Dawn Bell	F	10th	Thomas High School	95	70
39167	39167	Rebecca Tanner	F	9th	Thomas High School	73	84
39168	39168	Desiree Kidd	F	10th	Thomas High School	99	90
39169	39169	Carolyn Jackson	F	11th	Thomas High School	95	75
32028 rows × 7 columns

[198]



#sum the students who passed both math and reading
total_pass = (bothpass_df["Student ID"]).count()
total_pass
32028
[202]



#calculate the percentage of students who are passing both math and reading
overall_pass=total_pass/total_students
print(f"There are {total_students} students. There are {mathpass_students} students passing math and {readpass_students} passing reading. There are {total_pass} students passing both math and reading which is {overall_pass*100}% of all students.")

There are 39170 students. There are 33188 students passing math and 37681 passing reading. There are 32028 students passing both math and reading which is 81.76665815675261% of all students.
[261]



#create summary table
districtsum_df = pd.DataFrame({"Total Schools":[total_schools],"Total Students":total_students,"Total Budget":total_budget,"Average Math Score":[[avg_math]],"Average Reading Score":avg_reading,"% Passing Math":percent_math_pass,"% Passing Reading":percent_read_pass,"% Passing Overall":overall_pass})

districtsum_df

Total Schools	Total Students	Total Budget	Average Math Score	Average Reading Score	% Passing Math	% Passing Reading	% Passing Overall
reading_score	15	39170	24649428	[[78.98537145774827]]	81.87784	0.847281	0.961986	0.817667
[262]



students.groupby("school_name").count()
Student ID	student_name	gender	grade	reading_score	math_score
school_name						
Bailey High School	4976	4976	4976	4976	4976	4976
Cabrera High School	1858	1858	1858	1858	1858	1858
Figueroa High School	2949	2949	2949	2949	2949	2949
Ford High School	2739	2739	2739	2739	2739	2739
Griffin High School	1468	1468	1468	1468	1468	1468
Hernandez High School	4635	4635	4635	4635	4635	4635
Holden High School	427	427	427	427	427	427
Huang High School	2917	2917	2917	2917	2917	2917
Johnson High School	4761	4761	4761	4761	4761	4761
Pena High School	962	962	962	962	962	962
Rodriguez High School	3999	3999	3999	3999	3999	3999
Shelton High School	1761	1761	1761	1761	1761	1761
Thomas High School	1635	1635	1635	1635	1635	1635
Wilson High School	2283	2283	2283	2283	2283	2283
Wright High School	1800	1800	1800	1800	1800	1800
[263]



student_counts = students["school_name"].value_counts()
student_counts
Bailey High School       4976
Johnson High School      4761
Hernandez High School    4635
Rodriguez High School    3999
Figueroa High School     2949
Huang High School        2917
Ford High School         2739
Wilson High School       2283
Cabrera High School      1858
Wright High School       1800
Shelton High School      1761
Thomas High School       1635
Griffin High School      1468
Pena High School          962
Holden High School        427
Name: school_name, dtype: int64
[268]



merged_df = pd.merge(school, students, on="school_name", how="outer")
merged_df.head()
School ID	school_name	type	size	budget	count_by_school	Student ID	student_name	gender	grade	reading_score	math_score
0	0	Huang High School	District	2917	1910635	NaN	0	Paul Bradley	M	9th	66	79
1	0	Huang High School	District	2917	1910635	NaN	1	Victor Smith	M	12th	94	61
2	0	Huang High School	District	2917	1910635	NaN	2	Kevin Rodriguez	M	12th	90	60
3	0	Huang High School	District	2917	1910635	NaN	3	Dr. Richard Scott	M	12th	67	58
4	0	Huang High School	District	2917	1910635	NaN	4	Bonnie Ray	F	9th	97	84
[273]



schoolsum_df =(merged_df["school_name"]).count()
schoolsum_df
39170
[282]



col_list = list(merged_df.columns)
print(col_list)
['School ID', 'school_name', 'type', 'size', 'budget', 'count_by_school', 'Student ID', 'student_name', 'gender', 'grade', 'reading_score', 'math_score']


[-]




school_sum_columns = ["school_name", "type", "pledged", "state", "country", "staff_pick", "backers_count", "spotlight"]
short_df = df[kick_columns]
short_df.head(2)










