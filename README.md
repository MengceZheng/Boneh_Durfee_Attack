# Boneh-Durfee Attack

## Introduction
This is a Python implementation of Boneh-Durfee attack[^BD] on RSA. It is based on [Joachim Vandersmissen's crypto-attacks](https://github.com/jvdsn/crypto-attacks) and I make several improvements.

## Requirements
* [SageMath](https://www.sagemath.org/) with Python 3.9
* [PyCryptodome](https://pycryptodome.readthedocs.io/)

You can check your SageMath Python version using the following command:
```
$ sage -python --version
Python 3.9.0
```
Note: If your SageMath Python version is older than 3.9.0, some features in some scripts might not work.

## Usage
To run this attack, you can simply execute the Python file **attack.py** with Sage using `sage -python attack.py` and then input several specific attack parameters:
```commandline
Boneh_Durfee_Attack$ sage -python attack.py
Input prime bit-length: 128
Input delta: 0.266
Input attack times: 5
Input m: 5
INFO:root:Test for delta=0.266 with 5 times:
INFO:root:Generating RSA instance with 256-bit modulus and 69-bit private key d...
INFO:root:Trying m = 5, t = 2...
INFO:root:Failed!
INFO:root:Test 1 costs 5.502517 seconds
INFO:root:Generating RSA instance with 256-bit modulus and 69-bit private key d...
INFO:root:Trying m = 5, t = 2...
INFO:root:Succeeded!
INFO:root:Found p = 280289040924252858969937221371106912643
INFO:root:Found q = 308538008689784114925137574181258730927
INFO:root:Test 2 costs 0.248769 seconds
INFO:root:Generating RSA instance with 256-bit modulus and 69-bit private key d...
INFO:root:Trying m = 5, t = 2...
INFO:root:Failed!
INFO:root:Test 3 costs 5.736360 seconds
INFO:root:Generating RSA instance with 256-bit modulus and 69-bit private key d...
INFO:root:Trying m = 5, t = 2...
INFO:root:Failed!
INFO:root:Test 4 costs 5.598221 seconds
INFO:root:Generating RSA instance with 256-bit modulus and 69-bit private key d...
INFO:root:Trying m = 5, t = 2...
INFO:root:Succeeded!
INFO:root:Found p = 300194396566568635876010132028924633371
INFO:root:Found q = 325358021261498496102928905737189898419
INFO:root:Test 5 costs 1.062334 seconds
INFO:root:The success rate for delta=0.266 using m=5 is 40.0% and average time is 0.655552 seconds
```

## Notes
The parameters `m` and `t` as shown in the output log deserve special attention. These parameters are used in many lattice-based (small roots) algorithms to tune the lattice size. Conceptually, `m` and `t` represent the number of "shifts" used in the lattice, which is roughly equal or proportional to the number of rows. Therefore, increasing `m` and `t` will increase the size of the lattice, which also increases the time required to perform lattice reduction (currently using LLL). On the other hand, if `m` and `t` are too low, it is possible that the lattice reduction will not result in appropriate vectors, therefore wasting the time spent reducing. Hence, this is a trade-off. In the current version of the attack, `t` can, in some cases, be computed based on the specific small roots method used by the attack. 

[^BD]: Boneh D., Durfee G., "Cryptanalysis of RSA with Private Key d Less than N^0.292" | [HTML](https://ieeexplore.ieee.org/abstract/document/850673) [PDF](https://staff.emu.edu.tr/alexanderchefranov/Documents/CMSE491/Fall2019/BonehIEEETIT2000%20Cryptanalysis%20of%20RSA.pdf)
