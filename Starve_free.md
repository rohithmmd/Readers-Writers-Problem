It's also called as Third Readers-Writers problem where no thread shall be allowed to starve i.e.
by the operation of obtaining a lock on the shared data, will always terminate in a bounded amount of time.

Semaphores & Variables used:
```
/*DataSet*/

//Below semaphores initialised to '1'
semaphore in; //Used to check the critical section entering process.
semaphore mutex; // For mutual exculsion in reading processes while updating readCount.
semaphore rw_mutex; // For mutual exclusion between two writing processes.

int readCount=0; // This semaphore is used to count no of reading process
```

Structure of Writer process:
```
do{

  wait(in); //Lock 'in' semaphore to prevent reader process from reading
  wait(rw_mutex); //Lock 'rw_mutex' to prevent other writing processes from writing
  
  //Writing is done now.
  //Then, release the semaphores for next reader/writer.
  
  signal(rw_mutex);
  signal(in);
  
}while(true);
```

Structure of Reader process:
```
do{

  wait(in); //Lock 'in' to check and if there are any writers entering. 
  wait(mutex);  //Lock 'mutex' to update readCount
  readCount+=1; //Update readCount
  if(readCount==1) wait(rw_mutex); //if it's the first reader, Lock 'rw_mutex' to prevent writers from writing.
  
  //Now release the semaphores 'in' & 'mutex' 
  
  signal(mutex);         
  signal(in);
  
  //Reader performs the reading
  
  wait(mutex);  //Lock 'mutex' to update readCount
  readCount-=1; //Update readCount
  
  if(readCount==0)  signal(rw_mutex); //if it is last reading process, release 'rw_mutex' to allow other writers to write
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
