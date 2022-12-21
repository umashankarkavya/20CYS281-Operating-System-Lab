# 20CYS281 - Operating System Lab
![](https://img.shields.io/badge/Batch-CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-OS-blue)

## MultiThreading in C 

### Header files
```
#include <pthread.h>
```

### Function 
```
pthread_create(&thread_id, attr, myFunc, parameters);

&thread_id - pointer to thread_id 
attr - thread attributes or NULL for default attributes
myFunc - Function to be called once the thread is created
parameters - parameters to the function (myFunc) called or NULL 

```

### Example 

```
#include <pthread.h>
#include <stdlib.h>
#include <stdio.h> 
void *printWelcomeMessage(void *names) {
    
   sleep(2);    
   char *name = (char *)names;    
   printf("\n[THREAD] Hello, Welcome %s.", name);
   pthread_exit(NULL);
   
}

int main () {
   pthread_t threads[5];
   char names[10][15] = {"Amritha","Praveen","Saurabh","Sangeetha","Lakshmy","Srinivasan","Ramaguru"};
   int rc;
   int i;
   for( i = 0; i < 7; i++ ) {
      printf("\n[MAIN] Creating thread, %d", i);
      rc = pthread_create(&threads[i], NULL, printWelcomeMessage, (void *)names[i]);
      if (rc) {
         printf("Error:unable to create thread, %d ", rc);
         exit(-1);
      }
   }
   pthread_exit(NULL);
}
```