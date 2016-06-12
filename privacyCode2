import csv
import numpy as np
from pylab import *
import matplotlib.pyplot as plt
import re
from collections import Counter
import pandas as pd
import random
import scipy.stats as stats
from scipy.stats import norm
from mpl_toolkits.mplot3d import Axes3D


f=open(r'D:\userdata\shalal\Desktop\homeCapture1.csv','r')
reader = csv.DictReader(f)

t7=[]
t8=[]
t9=[]
t10=[]
z=[]
y=[]
b=[]
length=[]
protocol=[]
time=[]
No=[]
time1=[]
pos = arange(4)+.5
width = 0.35

def perCheck(per):
    if per >=60:
        ans = per+(np.random.rand()+(per*15/100))
        return ans
    elif per >=30:
        ans = per+(np.random.rand()+(per*20/100))
        return ans
    elif per >=20:
        ans = per+(np.random.rand()+(per*15/100))
        return ans
    elif per >=10:
        ans = per+(np.random.rand()+(per*10/100))
        return ans
    elif per <10:
        ans = per+(np.random.rand()+(per*10/100))
        return ans

def extractIP(row, field):
    l = re.split('(.*)\.(.*)\.(.*)\.(.*)', row[field])
    l= l[1:-1]
    a = array(l, dtype=int)
    if (a[0] >= 1) and (a[0] <= 126):
        return 'Class A'
    elif (a[0] >= 128) and (a[0] <= 191):
        return 'Class B'
    elif a[0] >= 192 and a[0] <= 223:
        return 'Class C'
    elif a[0] >= 224 and a[0] <= 239:
        return 'Class D'
    elif a[0] >= 240 and a[0] <= 254:
        return 'Class E'
    elif a[0] == 255:
        return 'Class Broadcast'
    elif a[0] == 127:
        return 'loopback'
    else:
        return 'Invalid IP'

for i in reader:
    field1=i['Protocol']
    field2=i['Length']
    field3=i['Time']
    field4=i['No.']
    i=extractIP(i, 'Source')
    protocol.append(field1)
    length.append(field2)
    time.append(field3)
    No.append(field4)
    z.append(i)

a=array(length, dtype=int)
time=array(time, dtype=float)
c=array(No, dtype=int)

a=a[:1000]
time=time[:1000]
c=c[:1000]

for p in a:
    epslon=0.01
    ans = p +(random.randint(1,1/epslon))
    b.append(ans)
    
for u in time:
    epslon=0.01
    ans = u +(random.randint(1,1/epslon))
    time1.append(ans)    

for q in protocol:
    if q=='TCP' or q=='UDP':
        t7.append(q)
    elif q=='SSL' or q=='TLSv1.2':
        t8.append(q)
    elif q=='DNS' or q=='HTTPS' or q=='ICMP':
        t9.append(q)
    else:
        t10.append(q) 

fracs = [len(t7)*100/len(protocol),len(t8)*100/len(protocol),len(t9)*100/len(protocol), len(t10)*100/len(protocol)]


TCPnUDP=perCheck(fracs[0])
TLSnSSL=perCheck(fracs[1])
HTTPnDNS=perCheck(fracs[2])
Bitrorent=perCheck(fracs[3])

fracs2=[TCPnUDP,TLSnSSL,HTTPnDNS,Bitrorent]



fig = plt.figure(0)
ax = Axes3D(fig)

ax.plot(xs=c, ys=time, zs=a, zdir='z', label='ys=0, zdir=z')
ax.set_xlabel('No. of Packets')
ax.set_ylabel('Time in seconds')
ax.set_zlabel('packet length')
plt.show()
