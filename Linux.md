### Linux or HPC command lines 
A guide is available through USC's CARC at the link below:
https://www.carc.usc.edu/user-guides  
A guide from CARC specifically for Python (which we tend to use most often). This is really useful to reference for running interactive or batch jobs or installing packages:  
https://www.carc.usc.edu/user-guides/advanced-hpc-programming/programming-languages/python  
This link also contains some information on running code in parallel which could be useful.  

# Command Commands in Linux Operating System <br>
Cheat sheet of commands most frequently used:  
1. move directories: ```cd directoryname``` or ```cd ~``` to move to home directory or ```cd ../``` to move one level up from current directory
2. print working directory: ```pwd``` prints the directory currently in
3. list files: ```ls``` lists the files in current directory, ```ls -l``` lists files with owner, size, date last edited
4. create a directory: ```mkdir directory name```
5. create a file: ```vi yourfile.py```
6. view file: ```vi yourfile.py``` or ```vim yourfile.py```
7. exit out of file view: quit without saving ```:q!``` or save ```:wq```
8. edit file in vi: ```i``` and press escape to leave edit mode
9. remove file: ```rm filename``` or ```rm filename*``` to remove all files that start with "filename", can also put asterick in the middle
10. remove directory: ```rmdir directoryname``` if directory is empty, ```rmdir -p directoryname``` to force delete a non-empty directory but be careful with this
11. move to a specific line in file: ```n shift+g```(when not in edit mode) where n is the line number
12. view first 5 lines of file ```head yourfile.csv```
13. search for word in files:  ```grep -irl search word``` will return all files in current directory that contain the word you searched for
14. check storage:  ```df -H``` shows how much of avaialable memory is used
15. print number of files in directory: ```ls -1 | wc -l```
16. view csv file in format: 
```cat yourfile.csv | sed 's/,/ ,/g' | column -t -s, | less -S```
17. output the number of lines in a text file (e.g. csv file): 
```wc -l < mytextfile```
18. move, rename, and copy files  
```mv filename destination_directory```: move a file in current directory to another directory
```mv filename newfilename```: rename filename to newfilename
```cp filename destination_directory```: create a copy of a file in current directory to another directory


Additionally, here is a link to common commands in Linux:  
https://www.geeksforgeeks.org/basic-linux-commands/  
Otherwise, if you can't figure out how to do something you can always search linux operating system commands! Tip many of the commands can be adjusted by adding flags at the end. For example ```-c``` combined with ```grep``` to make ```grep -c wordsearch``` will count the number of times the word shows up.  

**in HSDA:**
```salloc --ntasks=1 --mem-per-cpu=16GB --time=01:00:00```




6. run python code 

7. install python packages 

# Downloading and transferring files from HSDA
Need to download the application WinSCP  
## Download from HSDA to local drive:
1.  In the HSDA: ```scp -r filename or folder username@hpc-transfer1.usc.edu:~/```
2.  Open WinSCP on local drive
3.  Hostname: hpc-transfer1.usc.edu, username: yourusername, password: yourhsdapassword
4.  In local drive (left side), navigate to desired folder
5.  Select file from hpc to download, right click and select download
DO NOT DOWNLOAD OR TRANSFER ANY DATA THAT DOES NOT MEET AGREEMENTS OF NDA. hpc-transfer1.usc.edu is NOT a secure environment, and secure data should not be stored there.

## Upload from local drive to HSDA
1. Open WinSCP
2. In local drive (left side), navigate to desired folder
3. Right click on desired file/folder and select upload
4. In the HSDA: ```scp -r peplinsk@hpc-transfer1.usc.edu:~/filename/ destinationfolder```

## This was the old way to do it for reference, but haven't used this method in a while
8. download non-text files from HPC (on-campus ethernet connection required)  
on a windows machine:  
1) go to Windows Menu -> Windows PowerShell -> Windows PowerShell (x86) -> right click -> Run as Administrator  
2) ```Start-Service sshd```: to start OpenSSH Server to allow remote file transfer    
3) ```Get-Service sshd```: to check if the OpenSSH Server is running  
4) on HPC login, use:  
```scp file_to_be_downloaded your_username_on_windows@your_windows_ip:/download_place_on_windows```  
*if using GBW desktop, a typical command line would be:  
```scp file_to_be_downloaded your_username_on_desktop@desktop_ip:/D:/Data```  
*if using GBW laptop, a typical command line would be:  
```scp file_to_be_downloaded mo@laptop_ip:/C:/Users/mo/Downloads```  
5) check if the file is downloaded  
6) it is recommended to stop the OpenSSH Server after necessary download for security purposes: in PowerShell: ```Stop-Service sshd```  
7) ```Get-Service sshd```: to double check if the OpenSSH Server has stopped  

# Running jobs in parallel with python <br>
By default, Python only uses one core, but it also supports implicit and explicit parallel programming to enable full use of multi-core processors and compute nodes. This includes the use of shared memory on a single node or distributed memory on multiple nodes. On CARC systems, 1 thread=1 core= 1 logical CPU.

Implicit Parallelism
Some Python pacakges and their functions use implicit parallelism, so you do not need to call for it in your Python code. These packages will automatically detect the available number of cores. Multiple cores can be requested in the Slurm job with the '''--cpus-per-task''' option.

Explicit Parallelism
Explicit parallelism refers to explicitly calling for parallel computation in your Python code. Many Python pacakges exist for explicit parallelism. Multiple cores will still need to be requested through the '''--cpus-per-task''' option in the Slurm job.

Further, one Slurm job can have multiple tasks that are sent to different nodes to all run at the same time.
