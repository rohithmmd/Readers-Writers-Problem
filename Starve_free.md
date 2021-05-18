It's also called as Third Readers-Writers problem where no thread shall be allowed to starve i.e.
by the operation of obtaining a lock on the shared data, will always terminate in a bounded amount of time.

Semaphores & Variables used:
```
/*Data-set*/

semaphore in =1; //This semaphore is used to check which process is going to enter critical section.
semaphore mutex = 1; // This semaphore is used for mutual exculsion in reading processes while updating read_count.
semaphore rw_mutex =1; // This semaphore is used for mutual exclusion between two writing processes.

int readCount=0; // This semaphore is used to count no of reading process
```

Structure of Writer process:
```
do{
  wait(in);            //Lock enter semaphore to prevent reader process from reading
  wait(rw_mutex);          //Lock rwMutex to prevent other writing processes from writing
  
  //Writing is done here
  //After writing release the semaphores resource access for next reader/writer.
  
  signal(rw_mutex);
  signal(in);
}while(true);
```

Structure of Reader process:
```
do{
  wait(in);           //Wait if there are any writers using enter. 
  wait(mutex);          //Lock mutex to update readCount 
  readCount++;
  if(readCount==1) wait(rw_mutex); //if it is the first reader lock rwMutex to prevent writers from writing.
  signal(mutex);         //Release enter and mutex 
  signal(in);
  
  //Reading is done here
  
  wait(mutex);          //lock mutex to update readCount
  readCount--;
  if(readCount==0)  signal(rwMutex); //if it is last reading process release rwMutex to allow other writers to write
  signal(mutex);
}while(true);
```

Overview
```
Writer Process : 
Lock 'in' semaphore so as to prevent reader process from reading and then Lock 'rw_mutex' to prevent other writing processes from writing. 
Now, perform the writing and then release the semaphores. 
Reader can now stop writers by locking 'rw_mutex' if readers obtained permission to read first.
Reader Process : 
Wait if there's any writer using 'in'. Lock 'mutex' to update readCount and if its the first reader, lock 'rw_mutex' to prevent writers from writing.
Release in and mutex. Do the reading.
Again lock mutex to update 'readCount' and if its last reading process release 'rw_mutex' to allow writers to write.
```
