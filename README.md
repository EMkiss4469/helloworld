# helloworld
the project  aim to
# -*- coding: utf-8 -*-
"""
Created on Mon Jul 23 14:25:09 2018
作业10：
1、获取2300所学校的编号
2、获取31所城市的编号
3、获取142600数据，31/10，每个组3个城市数据，后面组装在一起
4、将142600数据用spark统计
@author: JinF
"""
#1、获取2300所学校的编号
#获取142600数据，31/10，每个组3个城市数据，后面组装在一起
ls=open('C:/Users/JinF/Desktop/all_school.txt',encoding='utf-8').readlines()
schoolls=[]
for line in ls: 
    s=line.split('-jianjie-')[1]
    s=s.split('.')[0]
    schoolls.append(s)
import urllib.request as r
url='http://www.gaokaopai.com/university-ajaxGetMajor.html'
headers={
        'User-Agent':' Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36',
        'X-Requested-With': 'XMLHttpRequest'
        }
f=open('全国招生人数.txt','a',encoding='utf-8')
print('学校编号为：')
for schoolid in schoolls:   
     try:   
        req=r.Request(url,data='id={}&type=1&city=13&state=1'.format(schoolid).encode(),headers=headers)  
        d=r.urlopen(req).read().decode('utf-8','ignore')
        if d.startswith("{"):
            f.write(d+"\n")
            print(schoolid)
        else:
            print('网址出错'+schoolid)
     except Exception as err:  
           print('此行有误')
      
f.close()
#3、获取142600数据，31/10，每个组3个城市数据，后面组装在一起
f2=open('C:/Users/JinF/Desktop/大数据实训/XML高考派城市.txt',encoding='gbk').readlines()
print('31所城市编号为：\n')
for k in range(1,32): 
    print(f2[k].split('<li data-val="')[1].split('" data-id=')[0]+':'+f2[k].split('claimCity')[1].split(',')[1].split(')">')[0])
f2.close()

f3=open('C:/Users/JinF/Desktop/大数据实训/全国大学文科河北录取人数.txt',encoding='gbk').readlines()
f4 = open("1.txt",'w',encoding="utf-8")

for i in f3: 
    f4.write('\''+i.split('(')[1].split(',')[0]+'\''+',')
f4.close()

f5 = open("2.txt",'w',encoding="utf-8")
data1=[]
data2=[]
file2=open('C:/Users/JinF/Desktop/大数据实训/全国大学文科河北录取人数.txt',encoding='gbk').readlines()
for j in range(len(f3)): 
    data1.append('\''+file2[j].split('(')[1].split(',')[0]+'\''+',')
    data2.append(file2[j].split(',')[1].split(')')[0]+',')

    #f5.write(str(i.split(',')[1].split('(')[0])+',')
f5.close()


f3.close()
