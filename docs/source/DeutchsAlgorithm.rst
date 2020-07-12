Deutsch's Algorithm
===================

Deutsch's Algorithm is an algorithm for solving Deutsch's Problem, one of the simplest problems where quantum algorithms outperform regular algortithms.

Let's say we have a function f(x), that takes possible inputs of 0 and 1, and gives possible outputs of 0 and 1. If f(0) = f(1), the function is constant, as the output is the same for both inputs. If f(0) ≠ f(1), the function is balanced.  

In this algorithm, two qubits with initial values |xy⟩ = |01⟩ each pass through a Hadamard gate. Then (x,y) passes through an oracle gate that outputs (x, y ⊕ f(x)). Finally, (x) passes through a hadamard gate.

.. image:: images/deutsch.png
    :width: 100%
    
When |xy⟩ = |01⟩ pass through the intital Hadamard gates, the system is in quantum superposition:

:math: \frac{1}{\sqrt{2}} (|0⟩ + |1⟩)  \frac{1}{\sqrt{2}} (|0⟩ - |1⟩)  

Passing through the oracle, this gives:

:math:  |x⟩ \frac{1}{\sqrt{2}} (|0 ⊕ f(x)⟩ - |1 ⊕f(x)⟩)  

(|x⟩ is in a superposition, for simplicity we will write it as |x⟩)

If f(x) = 0, the system is now in the state:

:math: |x⟩  \frac{1}{\sqrt{2}} (|0 ⊕ 0)⟩ - |1 ⊕ 0⟩)  
:math: = |x⟩  \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩)  

If f(x) = 1, the system is now in the state:

:math: |x⟩  \frac{1}{\sqrt{2}} (|0 ⊕ 1)⟩ - |1 ⊕ 1⟩)  
:math: = |x⟩ (|0⟩ + |1⟩)  \frac{1}{\sqrt{2}} (|1)⟩ - |0⟩)  

This can be generalized as:

:math:  |x⟩  \frac{(-1)^f(x)}{\sqrt{2}} (|0)⟩ - |1⟩) 
:math:  = (-1)^f(x)|x⟩  \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩) 
:math:  = \frac{1}{\sqrt{2}} ((-1)^f(0)|0⟩ + (-1)^f(1)|1⟩)  \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩) 

Now, we have:

:math:  = \frac{(±1)}{\sqrt{2}} (|0⟩ + |1⟩) \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩)  if f(x) is constant (either (f(0),f(1)) = (0,0) or (f(0),f(1)) = (1,1) 
:math:  = \frac{(±1)}{\sqrt{2}} (|0⟩ - |1⟩) \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩)  if f(x) is balanced (either (f(0),f(1)) = (0,1), or (f(0),f(1)) = (1,0) 

Finally, applying a Hadamard gate to the first qubit will return:

:math:  = \±1}|0⟩ \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩)  if f(x) is constant
:math:  = \±1}|1⟩ \frac{1}{\sqrt{2}} (|0)⟩ - |1⟩)  if f(x) is balanced

Now we can take a measurement of the first qubit, which will return 0 if f(x) is constant, and 1 f(x) is balanced. 

The code for Deutsch's Algortihm in qcircuits is below:

**Code**:

.. literalinclude:: ../../examples/deutsch_algorithm.py
