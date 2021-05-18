Readers - Writers Problem
```
In Readers-Writers Problem,
We are preventing more than one thread modifying the shared resource simultaneously and allowing the access of the shared resource to two or more readers at the same time.

It can be done by these methods :
1. Writers Starve //where no Reader,once added to the queue shall be kept waiting
2. Readers Starve - //where no Writer,once added to the queue shall be kept waiting
3. Starve-Free or No starve - //where no thread shall be allowed to wait

Basic information of Readers-Writers problems is in the 'pdf' file.
```
The Code and description of Starve free Readers-Writers Problem is provided in 'Starve_free.md' file which is within the repository.
