import csv
from pylab import *
import re
import hashlib
import random


f=open(r'D:\userdata\shalal\Desktop\Original_capture.csv','r')
reader = csv.DictReader(f)

#Function to obfuscate last octet of ip address

def extractIP(row, field):
    num=row[field].split('.')
    if not len(num)==4:
        pass
        row[field]==row[field]
    else:
        l = re.split('(.*)\.(.*)\.(.*)\.(.*)', row[field])
        l= l[1:-1]
        a=array(l,dtype=int)
        if a[0] >= 1 and a[0] <= 126:
            u= (str(a[0]),str(a[1]),str(a[2]),'*')
            row[field] = '.'.join(u)
            return row
        elif a[0] >= 128 and a[0] <= 191:
            u= (str(a[0]),str(a[1]),str(a[2]),'*')
            row[field] = '.'.join(u)
            return row
        elif a[0] >= 192 and a[0] <= 223:
            u= (str(a[0]),str(a[1]),str(a[2]),'*')
            row[field] = '.'.join(u)
            return row
        elif a[0] >= 224 and a[0] <= 239:
            u= (str(a[0]),str(a[1]),str(a[2]),'*')
            row[field] = '.'.join(u)
            return row
        elif a[0] >= 240 and a[0] <= 254:
            u= (str(a[0]),str(a[1]),str(a[2]),'*')
            row[field] = '.'.join(u)
            return row
        elif a[0] == 255:
            row[field]= 'Broadcast'
            return row
        elif a[0] == 127:
            row[field]= 'Loopback adress'
            return row
        else:
            row[field]= 'Invalid Address'
            return row

#Function to supress the field by given suppression character

def suppressField(row,field,suppressionCharacter):
    row[field] = suppressionCharacter
    return row

#Function to hash the fields by SHA256 algorithm

def hashField(row, Field):
    row[Field]=hashlib.sha256(row[Field]).hexdigest()
    return row

#Function to add random laplace noise between o and b to the fields where b = Δf / ε  using differential privacy algorithm.

def addJitter(row, Field):
    epslon=0.01
    sensitivity=1
    row[Field] = int(row[Field]) +(random.randint(0,sensitivity/epslon))
    return row



ip_anonymise = []
noise_addition=[]
field_supression=[]
hashing=[]
protocol_eqv_class=[]

# Iterating over the raw data to execute the anonymisation functions
for i in reader:
    i= extractIP(i, 'Source')
    i= extractIP(i, 'Destination')
    ip_anonymise.append(i)
 

for m in ip_anonymise:
    m= addJitter(m, 'Length')
    noise_addition.append(m)


for e in noise_addition:
   e= hashField(e,'Time')
   hashing.append(e)


for k in hashing:
    k = suppressField(k,'Info','*')
    field_supression.append(k)

field_supression=field_supression[:-1]

# Writing down the output CSV file

with open('D:\userdata\shalal\Desktop\outputtest.csv','wb') as csvfile:
    dw = csv.DictWriter(csvfile,delimiter=',',fieldnames=field_supression[0].keys())
    dw.writer.writerow(dw.fieldnames)	
    for r in field_supression:
        dw.writerow(r)
        print r 
