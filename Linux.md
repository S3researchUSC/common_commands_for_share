### Linux or HPC command lines 
A guide is available through USC's CARC at the link below:
https://www.carc.usc.edu/user-information/user-guides/software-and-programming

# Creating/Editing/Viewing files <br>
1. create a file: ```vi yourfile.py```
2. view file: ```vi yourfile.py``` or ```vim yourfile.py```
3. exit out of file view: quit without saving ```:q!``` or save ```:wq```
4. edit file in vi: ```i``` and press escape to leave edit mode
5. move to a specific line in file: ```n shift+g```(when not in edit mode)
6. view first 5 lines of file ```head yourfile.csv```
7. view csv file in format: 
```cat yourfile.csv | sed 's/,/ ,/g' | column -t -s, | less -S```
8. output the number of lines in a text file (e.g. csv file): 
```wc -l < mytextfile```
9. move, rename, and copy files  
```mv filename destination_directory```: move a file in current directory to another directory  
10. print as it is running in slurm file,
    in print statement: ```flush=True```
10. submit an interactive job 

**in HSDA:**
```salloc --ntasks=1 --mem-per-cpu=16GB --time=01:00:00```



4. in vi environment  
```:w``` : save current file you are vi-ing  
```:q``` : exit 
```:(number of lines to go to)``` : go to a specific line  


6. run python code 

7. install python packages 

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
