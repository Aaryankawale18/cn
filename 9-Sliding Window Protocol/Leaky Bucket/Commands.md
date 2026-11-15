Command 1 : lab-03-17@lab-03-17-OptiPlex-3280-AIO:~$ vim leaky_bucket_1290.c

Steps : Press i -> Paste code -> Press esc -> Type :wq -> Press enter  


Command 2 : lab-03-17@lab-03-17-OptiPlex-3280-AIO:~$ gcc leaky_bucket_1290.c -o leaky_bucket
Command 3 : lab-03-17@lab-03-17-OptiPlex-3280-AIO:~$ ./leaky_bucket

Output : 

Enter bucket size: 10
Enter output rate (leak rate): 3
Enter number of packets to incoming queue: 4
Enter packet size for packet 1: 4
Enter packet size for packet 2: 5
Enter packet size for packet 3: 2
Enter packet size for packet 4: 3

--- Simulation ---
Incoming packet of size 4. Bucket status: 4/10
Incoming packet of size 5. Bucket status: 9/10
Incoming packet of size 2. Bucket overflow! Dropped packet of size 2.
Incoming packet of size 3. Bucket overflow! Dropped packet of size 3.

Leaking packets...
Leaked 3 packets. Remaining in bucket: 6
Leaked 3 packets. Remaining in bucket: 3
Leaked 3 packets. Remaining in bucket: 0
