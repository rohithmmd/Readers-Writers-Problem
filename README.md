Readers - Writers Problem
```
In Readers-Writers Problem,
We are preventing more than one thread modifying the shared resource simultaneously and allowing access of the shared resource to two or more readers at the same time.

It can be done by these methods :
1. Writers Starve //No Reader,once added to the queue shall be kept waiting
2. Readers Starve - //No Writer,once added to the queue shall be kept waiting
3. Starve-Free or No starve - //No thread shall be allowed to wait
```
