### 第8章-数据处理的两个基本问题
#### 实验七 寻址方式在结构化数据访问中的应用

Power idea 公司从1975年成立一直到1995年的基本收入情况如下。

年份 | 收入(千美元) | 雇员(人) | 人均收入(千美元) |
:-: | :-: | :-: | :-:
1975 | 16 | 3 | ?
1976 | 22 | 7 | ?
1977 | 382 | 9 | ?
1978 | 1356 | 13 | ?
1979 | 2390 | 28 | ?
1980 | 8000 | 38 | ?
... |
1995 | 5937000 | 17800 | ?

下面的程序中，已经定义好列这些数据：

```asm
assume cs:codesg

data segment
    ; 21年的字符串
    db '1975', '1976', '1977', '1978', '1979', '1980', '1981', '1982', '1983', '1984'
    db '1985', '1986', '1987', '1988', '1989', '1990', '1991', '1992', '1993', '1994'
    db '1995'

    ; 21年公司总收入的21个doword型数据
    dd 0000016, 000022, 000382, 001356, 002390, 0008000, 0016000, 0024486, 0050065, 0097479
    dd 0140417, 197514, 345980, 590827, 803530, 1183000, 1843000, 2759000, 3753000, 4649000
    dd 5937000

    ; 21年公司雇员人数的21个word型数据
    dw 00003, 0007, 0009, 0013, 0028, 0038, 0130, 00220, 00476, 00778
    dw 01001, 1442, 2258, 2793, 4037, 5635, 8226, 11542, 14430, 15257
    dw 17800
data ends

table segment
    db 21 dup ('year summ ne ?? ')
table ends
```

编程，将data段中的数据按如下格式写入到table段中，并计算21年中的人均收入（取整），结果也按照下面段格式保存在table中。

一年占一行 行内地址