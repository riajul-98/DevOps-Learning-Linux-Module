# Over The Wire Bandit

## Level 0
To initially ssh into the level 0 server, run the command `ssh [username]@[server] -p[portnumber]`. Details can be found at https://overthewire.org/wargames/bandit/bandit0.html

## Level 0 -> Level 1
The password for the next level is found in a file called 'readme' in the home directory. I used `cat readme` to obtain the password.

## Level 1 -> Level 2
The password for the next level is in a file called '-'. I used `cat ./-` to read the file.

## Level 2 -> Level 3
The password for the next level is located in a file called 'spaces in this filename'. I used backwards slashes to open this file. Using the following command, I was able to open the file; 
`cat spaces\ in\ this\ filename`

## Level 3 -> Level 4
The password file is a hidden file, located in a directory named 'inhere'. First I ran the command `cd inhere`, followed by `ls -a` which revealed a file called '...Hiding-From-You'. I then ran `cat ...Hiding-From-You` to read the file contents.

## Level 4 -> Level 5
In this level there were 9 files in the 'inhere' directory and the password was the only human-readable file according to the website. First I ran the command `cd inhere` and then ran the command `cat ./-file0{0..9}` to open all the contents of the files. Only one line was human-readable.

## Level 5 -> Level 6
According to the website, the password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

First I ran the command `cd inhere` and then ran the command `ls -lR | grep 1033` which did not give any results so I ran `ls -laR | grep 1033` which showed the file would be a hidden file called '.file2' in the 'maybeinhere07' directory. I then used the cat command to read the contents.

## Level 6 -> Level 7
According to the website, the password is somewhere on the server with the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

As this was the case, I changed to the root directory using the `cd /` command. I then ran the `find -type f -user bandit7 -group bandit6 -size 33` command after reading the man pages for the find command. I got a lot of permission denies errors for files so I changed the command to `find -type f -user bandit7 -group bandit6 -size 33 2>/dev/null` which gave me the file and location and I read the file using the cat command.

## Level 7 -> Level 8
First I changed into the root directory and ran the `find -name data.txt 2> /dev/null` command which told me there is a data.txt file in the bandit7 to bandit12 directories. I then ran the command `cat /home/bandit{7..12}/data.txt | grep millionth`

## Level 8 -> Level 9
This one was a lot simpler as the file was located in the users home directory. To find the only unique line, I used `cat data.txt | sort | uniq -u`.

## Level 9 -> Level 10
For this one, I used the `cat data.txt | strings | grep =` command.

## Level 10 -> Level 11
For this one, the password was encoded and I had to decode it using the `cat data.txt | base64 -d` command.

## Level 11 -> Level 12
This one took a bit of googling as I did not find the man pages of tr very useful. I used the command `cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'`.

## Level 12 -> Level 13
This one required a lot of man pages and google searches. using gzip, tar, xxd and bzip2, I was able to obtain the password.

## Level 13 -> Level 14
This one was fairly simple. There is a private key on in the home directory and we need to ssh into the server as bandit14 to get the next password.

## Level 14 -> Level 15
Login to the previous level and look in the file provided. Use the nc command with port 30000 and then enter that password.

## Level 15 -> Level 16
With this level, I used the openssl command with s_client and -connect options and then providing the password found in the previous level.

## Level 16 -> Level 17
First I used the nmap command to scan ports between 31000 to 320000. I gota few results but one of them was unknown and required a password. I then used the same openssl command from the previous level and entered the password. This provides a private key which we create into a file and move onto the next level.

## Level 17 -> Level 18
Used diff command to compare files. 2 passwords were shown, one with > and one with <. Checked man and > is new.

## Level 18 > Level 19
This one is a weird one. You cannot ssh like normal but need to add -t followed by /bin/sh.

## Level 19 -> Level 20
There is a file in the home directory which allows you to act as another user. Used this to read the password file.