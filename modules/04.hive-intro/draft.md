
## Example 1: Payment history table (of database):

id,IBAN_from,IBAN_to,amount,timestamp

1,FR143564545,FR35678904,1000.65,1577836800
2,FR143564545,FR35678904,1000.65,1577836800 
3,FR143564545,FR35678904,1000.65,1580515200
4,FB324563,FR35678904,200.43,...
5,FR143564545,FR35678904,1000.65
...
n,FR143564545,FR35678904,1000.65
n+1,FR143564545,FR35678904,1000.65


## Example 2: bank customers

**Schema:**

name,age,gender,bankaccount,company_id

**Data (in CSV format) - 10 Gb:**

sergei,30,m,35678899032,0
jules,27,m,15466765432,0
prisca,44,f,76545657687,0
david,42,m,345766564343,12
...

### Optimising the file

1. Transpose file (from row oriented to column oriented)

```
sergei,jules,prisca,david
30,27,44,42
10032,10031,10067,10034
0,0,0,12
```
  
2. Calculate metadata and keep it

{name:0:26,age:27:39,...}
  
3. Compress **sparse values**

```
sergei,jules,prisca,david
30,27,44,42
10032,10031,10067,10034
3:0,12
```

4. Use binary formats

Integer value is 2 byte

Example: 
- 32767 (integer) -> 2 bytes
- 32767 (string) -> 5 bytes
