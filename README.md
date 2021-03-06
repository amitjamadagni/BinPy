-----------
# BinPy
-----------

[![Build Status](https://travis-ci.org/BinPy/BinPy.png?branch=develop)](https://travis-ci.org/BinPy/BinPy)

 * [About](#about)
 * [Installation](#installation)
 * [Available Resources](#resources)
 * [Documentation](#documentation)
 * [Contribute](#contribute)


<a id="about"></a>
What is BinPy?
---------------
This package will serve as a base to develop circuit based applications or logical games on top of it. 
This package does not depend on any external library other than pure Python.

How to use
----------

Here's an example of SR latch constructed from a pair of cross-coupled NOR gates
![SR latch | Source: Wikipedia](https://upload.wikimedia.org/wikipedia/commons/c/c6/R-S_mk2.gif)

```python
from BinPy import *

NOR1 = Nor('NOR1')  #First NOR gate
NOR2 = Nor('NOR2')  #Second NOR gate

NOR2.C.connect(NOR1.B)  #Connecting output of second NOR with input of first NOR
NOR1.C.connect(NOR2.A)  #Connecting output of first NOR with input of second NOR

# Set state
NOR1['A'] = 1
NOR2['B'] = 0
print 'Q: ',NOR2['C'], '\t','Q\': ',NOR1['C']

NOR1['A'] = 0
NOR2['B'] = 1
print 'Q: ',NOR2['C'], '\t','Q\': ',NOR1['C']

# Hold state
NOR1['A'] = 0
NOR2['B'] = 0
print 'Q: ',NOR2['C'], '\t','Q\': ',NOR1['C']

# Invalid State
NOR1['A'] = 1
NOR2['B'] = 1
print 'Q: ',NOR2['C'], '\t','Q\': ',NOR1['C']
```

<strong>Output</strong>
```python
Q:  True 	Q':  False
Q:  False 	Q':  True
Q:  False 	Q':  True
Q:  False 	Q':  False
```
<strong>Operations, Combinatonal Logic and Algorithms</strong>

```python
from BinPy import *

#Operations
operator = Operation()
print operator.add([1,0,1,1],[1,1])
print operator.subtract([1,0,1,1],[1,1])

#Combinational Logic
myMUX = MUX()
print "MUX Out: ", myMUX.run([1,0,0,0,1,1,1,1],[0,0,1])

#Algorithms 
#Includes the Quine-McCluskey algorithm for solving K-Maps
FinalEquation = QM(['A','B'])
print "Minimized Boolean Equation : " , FinalEquation.get_function(qm.solve([0,1,2],[])[1])


#IC
myIC = IC_7400()
p = {1:1,2:0,4:0,5:0,7:0,10:1,9:1,13:0,12:0,14:1}
myIC.setIC(p)
print "IC_7400 Out: ", myIC.run()

myIC1 = IC_7401()
p = {2:0,3:1,5:0,6:0,7:0,8:1,9:1,11:0,12:0,14:1}
myIC1.setIC(p)
print "IC_7401 Out: ", myIC1.run()
```
<strong>Output</strong><br/>
```python
{'carry': 0, 'sum': [1, 1, 1, 0]}
{'carry': 1, 'difference': [1, 0, 0, 0]}
MUX Out:  0
IC_7400 Out:  {8: 0, 11: 1, 3: 1, 6: 1}
IC_7401 Out:  {1: 1, 10: 0, 4: 1, 13: 1}
Minimized Boolean Equation : ((NOT B) OR (NOT A))
```

<a id="resources"></a>
Available Resources
-------------------
* All basic logic gates (NOT, OR, NOR, AND, NAND, XOR, XNOR)
* Combinational logics
	* Adder
	* Subtractor
	* Multiplier
	* MUX (2:1, 4:1, 8:1, 16:1)
	* DEMUX (1:2, 1:4, 1:8, 1:16)
	* Encoder
	
* IC
	* 7400
	* 741G00
	* 7401
	* 7402
	* 741G02
	* 7403
	* 741G03
	* 7404
	* 741G04
	* 7405
	* 741G05
	* 7408
	* 741G08
	* 7410
	* 7411
	* 7442
	* 7443
	* 7444
	* 7451
	* 7454
	* 7455
	* 7458
* Algorithms
	* Quine-McCluskey Algorithm (To find minimized Boolean Equation)
	* Moore Machine Optimizer

<a id="documentation"></a>
Documentation
-------------
Auto-generated documentation is available for reference at [BinPy docs](http://packages.python.org/BinPy/index.html)

<a id="installation"></a>
Installation
------------

### Linux

Install with **pip**

    sudo apt-get install pip setuptools ipython
    sudo pip install https://github.com/BinPy/BinPy/zipball/master

Install using **git**

    sudo apt-get install git setuptools ipython
    git clone https://github.com/BinPy/BinPy.git
    cd BinPy/
    sudo python setup.py install

    

Future Works
------------
* Introduction of all ICs
* Introduction of problem solving algorithms
* Addition of Microprocessors and Analog Devices
* Graphical representation of the circuit
* ...

<a id="contribute"></a>

How To Contribute
-----------------

 - [Report Bugs and Issues](https://github.com/BinPy/BinPy/issues)
 - [Solve Bugs and Issues](https://github.com/BinPy/BinPy/issues?page=1&state=open)
 - Write Tutorials, Examples and Documentation

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/mrsud/binpy/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

