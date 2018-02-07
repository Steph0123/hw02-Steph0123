#c Homework 02
- Due date: Feb 5, 2018
- Points: 50 pt.
- Final contents of your repository (no other files/folders should be included):
  - ```README.md```
  - ```task1.txt```
  - ```task2.txt```
  - ```task3.txt```
---
The purpose of your this homework assignment is to practice with basic concepts and commands in a Linux environment, including manipulating files, users, permissions, and I/O redirection.

You should provide answers to questions for each task in a separate text file named after the task (```task1.txt```, ```task2.txt```, and ```task3.txt```). For each question in a task, start on a new line, indicate the question number followed by a dot and space (e.g., ```1. ```). Then, provide answer to the question on the same line (regardless of the length of your answer). For instance, the first four lines of your ```task3.txt``` should look like below. Task 1 and 2 have three questions each. Task 3 has thirteen questions. 

    1. command1 arg1 arg2 ...
    2. command2 arg1 arg2 ...
    3. command3 arg1 arg2 ...
    4. command4 arg1 arg2 ...

---
## Task 0: Review the readings
In case you did not get to completely read the assigned chapters for the past week(s), make sure you do it now. Remember that it is always more fun and fruitful when you actually practice what you are reading (try examples from the chapter; think about and implement other cool things you can do based on what you just learned.) 

## Task 1: Expansions (12 pt.)
Write one-line commands that perform the followings.
1. List all files in the sub-directories of ```/etc``` that end with ```.conf``` . For example, it should list ```/etc/cups/cupsd.conf```, but should not list ```/etc/host.conf``` .
2. Create a set of directories in the current directory named based on three-letter month and four-digit year between 2015 and 2018. Directories should be named ```Jan2015```, ```Feb2015```, ..., ```Nov2018```, ```Dec2018```.
3. Calculate and show the result for a simple multiplication (such as ```2*3```) provided in a file named ```multiply.txt```. You can only use ```cat``` and ```echo``` commands for performing this.

## Task 2: I/O redirection (12 pt.)
Write one-line commands that determine and print the following desired output:
1. The total word count in files ```file1.txt```, ```file2.txt```, and ```file3.txt``` combined (assume the three files exist in the current directory).
2. How many user accounts are not allowed to log in to the system. You need to calculate the number of users in file ```/etc/passwd``` that include ```/nologin``` on their line.
3. The name of the 6 largest files in ```/usr/bin```, while suppressing any errors.

## Task 3: Permission management (26 pt.)
In the class, we discussed briefly about users and permissions in Linux. Let's practice how users and security is managed in this environment using a realistic scenario. For this exercise, you have to use your own Linux environment as we modify users/groups in the system. *This task cannot be performed on itsunix machine.*

Linux is a multi-user environment where users have the power to share (or not to share) resources with each other. The goal of this task is to set up a shared space between some users. Assume you want to work on a project together with another user on your machine, and you want that only the two of you be able to read the project documents. In the rest of this task, we assume your user is named ```john```. Perform a mental replace-all as you perform the steps. Our second user will be named ```user01```, for whom we will create a new account. Our approach in this task will rely on dedicated Linux group for the project shared by ```john``` and ```user01``` (and no one else).

> **Hint:** In the rest of this exercise you need to use the following commands (in addition to basic file-related commands). We suggest that you review the assigned book chapters, consult the manual pages (```man command-name```), and check out the [ArchWiki's article on user and group management](https://wiki.archlinux.org/index.php/users_and_groups) to learn more about them.
> - ```chown```: change file owner and group
> - ```chmod```: change permissions of a file
> - ```useradd```: create a new user
> - ```passwd```: change user password
> - ```groupadd```: create a new group 
> - ```gpasswd```: administer groups (e.g., add a user)
> - ```umask```: get or set the file mode creation mask
> - ```wget```: The non-interactive network downloader

> **Note:** You need to perform this task on your own Linux environment, not itsunix. 

> **Note:** Many steps of this exercise (and not all) need to be done via superuser privileges. Rather than switching to ```root``` account, you should use ```sudo``` command. We mention it for the steps that you need to use ```sudo```. Remember that when running ```sudo``` you need to provide your own account password to authenticate, not your ```root``` account password.

1. Log in as ```john```
2. Create a new group called ```project1``` (needs ```sudo```).
    > **Q1:** Report your command.
2. Add ```john``` to group ```project1``` (needs ```sudo```). Note that ```project1``` will be your additional group. Your primary group will still be ```john```.
    > **Q2:** Report your command.
3. At this point, you need to log out and log in again as ```john```. This step ensures that the system knows about your updated group membership. Failure to do so may create problems later in this task.
3. Create new user ```user01``` using the following command (needs ```sudo```). The ```-m``` option creates a home directory for the new user.

    ```$ sudo useradd -m user01```
4. Set password for ```user01``` using the following command (needs ```sudo```).

    ```$ sudo passwd user01```
2. Add ```user01``` to group ```project1``` (needs ```sudo```).
    > **Q3:** Report your command.
5. Create a new directory ```project1``` inside ```/home``` directory (needs ```sudo```).
    > **Q4:** Report your command.
6. Set the permissions of ```/home/project1``` such that owner and group have full access (read/write/execute), and others have no access (needs ```sudo```).
    > **Q5:** Report your command.
6. Change the owner and group of  ```/home/project1``` to ```john``` and ```project1```, respectively (needs ```sudo```).
    > **Q6:** Report your command.
7. Set your umask to 0027.
    > **Q7:** Report your command.
    >
    > **Q8:** What is the effect of the above command on newly created files by your user?
8. Download the latest Pro Git book as your first document in the project folder via the following command:

    ```$ wget https://github.com/progit/progit2/releases/download/2.1.32/progit.pdf -P /home/project1```
6. Log out as ```john``` and log in as ```user01```.
7. Try copying the downloaded file ```/home/project1/progit.pdf``` to ```user01``` home folder.
    > **Q9:** Why can't you copy the file?
    >
    > **Q10:** What is the error message you received?
6. Log out as ```user01``` and log in as ```john```.
7. Change the group of the downloaded file ```/home/project1/progit.pdf``` to ```project1```.
    > **Q11:** Report your command.
6. Now, log out again as ```john``` and log in as ```user01```.
7. Try copying the downloaded file ```/home/project1/progit.pdf``` to ```user01``` home folder.
    > **Q12:** Explain why you are successful this time.
8. How can you make sure that future files created in ```/home/project1``` will be available to ```project1``` members without needing to change ownership explicitly for every downloaded file?
    > **Q13:** Report your command.


Congratulations! You now know how to share files between different accounts on a Linux machine. In addition to collaboration between human users, this type of setup is useful if you want to share access with certain processes that run via their dedicated accounts (e.g., database systems or media servers) and you do not want to compromise security by giving access to everyone.
