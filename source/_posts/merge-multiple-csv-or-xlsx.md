---
title: merge-multiple-csv-or-xlsx
date: 2023-02-27 15:00:31
tags: csv, xlsx
---
### 合并多个列相同的文件到同一个，eg：csv，xlsx文件
生活中总有那么一种问题，丢你几十上百个csv，或者xlsx文件，让你筛选里面的条件达到某一个取出。今日的我就遇到了，手工达人是不可能手工达人的，我们要实现全自动化！

#### 合并多个csv
未实际操作的方案（因为我是windows党...）， linux系统的copy csv方案。

```shell
cd /{your all csv dir}
cat *.csv all.csv
```

实操了2种方案 (本人实际操作过，都可以。速度也还能接受)

1. windows 复制多个csv到同一个

操作路径：
打开cmd（注意一定要是cmd，powershell是不会成功滴）
然后进入到你的所有csv存在的目录下

```shell
copy *.csv all.csv   ----  对的，就这一行命令。搞定！无需任何安装，无需编码环境。高手中的高手~、
```

2. 若你是开发者，还可以看看python 的pandas操作。
```python
import os
import glob
import pandas as pd
# set working directory
os.chdir("csv_1")

# find all csv files in the folder
# use glob pattern matching -> extension = 'csv'
# save result in list -> all_filenames
extension = 'csv'
all_filenames = [i for i in glob.glob('*.{}'.format(extension))]
# print(all_filenames)

# combine all files in the list, encoding need to change for yourself actual 
combined_csv = pd.concat([pd.read_csv(f, encoding='ANSI')
                         for f in all_filenames]) 

# combine all files in the list
# combined_xlsx = pd.read_excel
# export to csv
combined_csv.to_csv("combined_csv.csv", index=False, encoding='utf-8-sig')

```


#### 合并多个xlsx
这个就没有找到cmd的操作方案了，不过pandas依旧yyds

祭出代码
```python
import os
import glob
import pandas as pd

os.chdir("xlsx_1")


extension = 'xlsx'
all_filenames = [i for i in glob.glob('*.{}'.format(extension))]

combined_csv = pd.concat(
    [
        pd.read_excel(f)
        for f in all_filenames
    ]
)


combined_csv.to_excel("combined_result.xlsx", index=False)
```