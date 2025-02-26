Step 1. $ make
Step 2. $ ./mts test1.txt

Internal Logic Overview
1. Open File & Create Queue Mutex

- The program opens the specified input file (e.g., test1.txt) and creates a mutex to ensure that only one train is added to the queue at a time.
2. Read Train Data

- Uses fscanf to read each train’s direction, loading time, and crossing time from the file.
3. Create Nodes & Threads

- For each set of train data, the program creates a new node and spawns a new train thread (handled in the train method).
4. Create Dispatcher Thread

- After all train threads are created, the program starts a dedicated dispatcher thread.
6. Dispatcher Broadcast

- The dispatcher sends a broadcast signal to all train threads to begin their loading phase.
7. Priority Queue Monitoring

- The dispatcher continuously checks whether the priority queue contains pending trains.
8. Conditional Signaling

-When a train is ready for processing, the dispatcher sends a conditional signal so the corresponding thread can run and complete its task.
9. Completion & Dispatcher Exit

-After all trains have been processed and the queue is empty, the dispatcher thread finishes and returns control to main.
10. Thread Cleanup

-The main thread rejoins the dispatcher thread and closes any remaining mutexes.
11. Program Exit

- Once all threads complete and resources are released, the program terminates.
![image](https://github.com/user-attachments/assets/f683459d-5a87-4d42-b427-2b1146ce19f6)
