# Problem Statement 


## 1. ASK
Co-Founder: Dhaval Patel & HR: Pinali Mandalia    

### Questions:
- Working preference of the people? WFH or WFO
- What could be the reason behind taking work from home either on monday or friday?
- How much % of the people are present in the given week/month?
- What could be the reason behind frequent sick leave?


## 2. PREPARE  
### Data Storage:
The public dataset is completely available on the Code basis website platform where it stores and consolidates all available datasets for analysis. The specific individual datasets at hand can be obtained at this link below: https://codebasics.io/resources/resume-project-data-analytics

### Data Organized:
The dataset is taken from the AtliQ. Thanks to the AtliQ for providing datasets for public access which is a great learning asset - feel free to explore them. This dataset contains only 1 excel file.


## 3. PROCESS
### Tools Used:
- Power BI

### Data Used:
Attendance Sheet

### About Data:  
Column Description for attendance sheet:  
* Employee Code: Unique identifier for each employee.
* Name: Name of the employee.
* [Date Columns]: Each date represents a day. Entries under these columns indicate the attendance status of the employee for that day:
  - P: Present
  - A: Absent
  - SL: Sick Leave
  - PL: Paid Leave
  - WO: Weekly Off
  - WFH: Work From Home
  - BL: Birthday Leave
  - FFL: Floating Festival Leave
  - BRL: Bereavement Leave
  - LWP: Leave Without Pay
  - HO: Holidays Off
  - ML: Menstrual Leave
* Total Present Days: Total number of days the employee was present during the period.
* Present: Number of days marked as present.
* Work from home: Number of days the employee worked from home.
* Paid Leave: Number of paid leave days taken by the employee.
* Sick Leave: Number of sick leave days taken by the employee.
* Birthday Leave: Number of birthday leave days taken by the employee.
* Floating Festival Leave: Number of floating festival leave days taken by the employee.
* Bereavement Leave: Number of bereavement leave days taken by the employee.
* Leave without pay: Number of leave without pay days taken by the employee.
* Weekly Off: Number of weekly off days for the employee.
* Holidays Off: Number of holidays off for the employee.
* Menstrual Leave: Number of menstrual leave days taken by the employee.


### Data Cleaning & Transformation
- Combining Data From Multiple Worksheets In The Same Excel Workbook.
- Created a template by unpivoting the other columns except employee no & name just to automate.
- Removed errors & perform proper data validation
- Transforming data in a dynamic way using google [Reference Link](https://blog.crossjoin.co.uk/2018/07/09/power-bi-combine-multiple-excel-worksheets/)

## 4. ANALYZE
Data Analyzing  
Power BI was used to analyze data.

### Key Metrics:    
#### Calculated Columns:
- WFH Count = SWITCH(TRUE(),'Final Data'[Value]="WFH", 1, 'Final Data'[Value]="HWFH", 0.5, 0)
- Month = STARTOFMONTH('Final Data'[Date])
- SL Count = SWITCH(TRUE(), 'Final Data'[Value]="SL", 1, 'Final Data'[Value]="HSL", 0.5, 0)

#### Measures:
- Presence % = DIVIDE([Present Days],[Total Working Days],0)
- Present Days = VAR _presentdays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value]="P") RETURN presentdays + [WFH Count]
- SL % = DIVIDE([SL Count], [Total Working Days], 0)
- SL Count = SUM('Final Data'[SL Count])
- Total Working Days = VAR _totaldays = COUNT('Final Data'[Value]) VAR _nonworkingdays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] IN {"WO", "HO"}) RETURN _totaldays-_nonworkingdays
- WFH % = DIVIDE([WFH Count], [Present Days], 0)
- WFH Count = SUM('Final Data'[WFH Count])

## 5. SHARE 











