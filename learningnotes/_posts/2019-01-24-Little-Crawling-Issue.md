---
image:
  teaser: DataCrawling.jpeg

layout: article
title: Little Crawling Issue
date: 2019-01-24
categories: notes
author: chunyi_hsiao
tags: [Crawling, Python]
share: true

---

Today I probably did the rehearsal for my end-term defense (still to tired to believe this shit through). And EVENTUALLY I can start to study and to build the quantitative trading and system. But, after knowing a bit of this work, I convince myself and start the big shit from now on. 

Thereby the first try is to prepare(crawling) the data for the traiiiiiiiiiiiiiiiiiiiiining, yup it is a long way to run.

So, the best thing of in this moment is that you can find approximately everything on Google. Thankfully, I quickly found a [tutorial](https://www.youtube.com/watch?v=IqrFMiJfHBU) (In Chinese). This is suit to me because I need to crawling the stock information from the [Taiwan Stock Exchange Corporation](http://www.twse.com.tw/zh/) as well. 

Then, after I code the same as what he coded in the video, I got a *UnicodeEncodeError*. 
The original code: 
```python
import requests
import json
import csv

url = 'website_url'
res = requests.get(url)
s = json.loads(res.text)
dir = './directory/'

outputfile = open(dir, 'w', newline='')
outputwriter = csv.writer(outputfile)
outputwriter.writerow(s['fields'])
for data in (s['data']):
	outputwriter.writerow(data)
	pass
outputfile.close()
```

Then this error popped up |UnicodeEncodeError: 'ascii' codec can't encode character '\u5e74' in position 6: ordinal not in range(128)|

This dirty bug points to the **outputwriter.writerow(s['title'])**. Seems like the character in the **s['title']** cannot be encoded and written into .csv file due to the wrong codec. So I checked the my encoding setting of IDE(PyCharm), and it is the UTF-8. (Wait? I definitely select UTF-8, what's the matter to ASCII?).

Fortunately, a solution in stackoverflow gives an explanation and I modify the code by simply adding *'utf-8'* in open():
```python
with open(output_dir, 'w', encoding='utf-8',  newline='') as file:
    out_writer = csv.writer(file)
    out_writer.writerow(a['fields'])
    for data in (a['data']):
        out_writer.writerow(data)
        pass
    pass
file.close()
```
And it works.

However, there's one thing I'm really curious is **Why I already select the UTF-8 encoding in PyCharms, but the csv function still use ASCII to encode it?**

Perhaps a mystery.


### *Learned Today*
- Be aware of your codec setting
- Never trust your IDE 😂
