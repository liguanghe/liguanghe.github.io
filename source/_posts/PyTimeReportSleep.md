---
title:  Atom Time Report1 时间账单报告自动化1 
date: 2017/10/15 08:45:32
categories: 
- python


tags: 
- python
- Record
- time
- report
- TimeReport
- thinking
- skill
- atl4dama
- lghPR

---
Sleep

## Achievement

- Base on Atl4dama/DataCleaning
- summation weekly sleep time
- noon + night = sleep_time
- limit sleep_time to 59h, =< true

After

| n  | week | noon | night | sleep_time | -59h  | 
|----|------|------|-------|------------|-------| 
| 0  | 13   | 0.0  | 7.4   | 7.4        | True  | 
| 1  | 14   | 4.6  | 46.4  | 51.0       | True  | 
| 2  | 15   | 13.3 | 64.3  | 77.6       | False | 
| 3  | 16   | 6.6  | 53.0  | 59.6       | False | 
| 4  | 17   | 7.3  | 53.6  | 60.9       | False | 
| 5  | 18   | 7.9  | 46.3  | 54.2       | True  | 
| 6  | 19   | 4.4  | 65.6  | 70.0       | False | 
| 7  | 20   | 9.7  | 44.3  | 54.0       | True  | 
| 8  | 21   | 4.7  | 58.2  | 62.9       | False | 
| 9  | 22   | 13.3 | 53.1  | 66.4       | False | 
| 10 | 23   | 8.0  | 65.0  | 73.0       | False | 
| 11 | 24   | 4.8  | 46.7  | 51.5       | True  | 
| 12 | 25   | 0.6  | 65.2  | 65.8       | False | 
| 13 | 26   | 5.4  | 60.6  | 66.0       | False | 
| 14 | 27   | 2.1  | 47.1  | 49.2       | True  | 
| 15 | 28   | 6.0  | 50.9  | 56.9       | True  | 
| 16 | 29   | 4.7  | 69.6  | 74.3       | False | 
| 17 | 30   | 9.5  | 49.7  | 59.2       | False | 
| 18 | 31   | 0.0  | 44.7  | 44.7       | True  | 
| 19 | 32   | 7.2  | 53.1  | 60.3       | False | 
| 20 | 33   | 8.5  | 44.6  | 53.1       | True  | 
| 21 | 34   | 8.5  | 49.2  | 57.7       | True  | 
| 22 | 35   | 9.2  | 48.6  | 57.8       | True  | 
| 23 | 36   | 5.3  | 60.7  | 66.0       | False | 
| 24 | 37   | 4.4  | 53.5  | 57.9       | True  | 
| 25 | 38   | 8.6  | 48.1  | 56.7       | True  | 
| 26 | 39   | 11.7 | 44.1  | 55.8       | True  | 
| 27 | 40   | 3.8  | 55.0  | 58.8       | True  | 
| 28 | 41   | 8.4  | 50.4  | 58.8       | True  | 

Before 

week|noon|sleep|↓  
----|----|----|----
0|4|53|- 
1|13|54|↑ 
2|6|54|↓
3|6.5|54|- 
4|7.5|54|↑
5|4.5|57|-
6|6.5|46|↓
7|4.5|57|-
8|11.5|53|↑
9|5|54|- 
10|0.5|51.5|↓
11|4.5|64|↑
12|3|56.5|-
13|4|50|↓
14|7|62|↑
15|9.5|50|-
16|0|52.5|↓
17|6.5|40.5|↓
18|8|46|↓
19|5.5|47|↓
20|10|52|↑
21|7|53|-
22|4.5|54|-
23|8.5|48|-

## Code
- Python3
    + list.append()
- Pandas
- Numpy

```
#!/usr/bin/python
# -*- coding: utf-8 -*-
'''
- use all data to sleep_time in week
- every week night_sleep + noon_sleep - 59h <= 0 -> true
- write to .md

'''
__version__ = "v17.10.10.1827"
__author__ = 'lgh'
__license__ = 'MIT@2017-10'

import pandas as pd
import numpy as np
import sys

def WeekTime(cvsf):
    df = pd.read_csv(cvsf)
    df['du_time'] = df.apply(lambda x: x.du_end-x.du_start, axis=1)

    sl = df[df['act_type'].isin(['12.sleep'])]
    tr = df[df['act_type'].isin(['12.sleep:noonsleep'])]
    Uniqueweeks = df.wn4y.unique()
    w = []
    h = []
    n = []
    for i in Uniqueweeks:
        w.append(i)
        h.append((np.sum((sl[sl['wn4y'].isin([i])])['du_time'])/60/60))
        n.append((np.sum((tr[tr['wn4y'].isin([i])])['du_time'])/60/60))
        d = {'week': w,
             'night':h,
             'noon':n}
    st = pd.DataFrame(d)
    u = st.sort_index(axis=1, ascending=False).round(1)

    u['sleep_time'] = u.apply(lambda x: x.night+x.noon, axis=1).round(1)
    u['-59h'] = u.apply(lambda x: x.sleep_time-59<=0, axis=1)
    c = pd.DataFrame.to_csv(u)

    
    with open('TimeReport.md', 'a') as the_file:
        the_file.write('\n ## 睡眠\n')
        the_file.write('N'+str(c))

        
if __name__ == '__main__':
    print(__version__)

    if 2 != len(sys.argv) :
        print('''Usage:
        $ python lgh7.py path/2/XXX.csv
                #''')
    else:
        _csv = sys.argv[1]
        WeekTime(_csv)
```
