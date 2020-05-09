### Linux or HPC command lines 
1. view csv file in format: 
```cat yourfile.csv | sed 's/,/ ,/g' | column -t -s, | less -S```

2. submit an interactive job 

**in HSDA:**
```salloc --ntasks=1 --mem-per-cpu=16GB --time=01:00:00```

3. output the number of lines in a text file (e.g. csv file): 
```wc -l < mytextfile```

4. in vi environment  
```:w``` : save current file you are vi-ing  
```:q``` : exit 
```:(number of lines to go to)``` : go to a specific line  

5. move, rename, and copy files  
```mv filename destination_directory```: move a file in current directory to another directory  

6. run python code 

7. install python packages 

8. download non-text files from HPC (on-campus ethernet connection required)  
on a windows machine:  
1) go to Windows Menu -> Windows PowerShell -> Windows PowerShell (x86) -> right click -> Run as Administrator  
2) ```Start-Service sshd```: to start OpenSSH Server to allow remote file transfer    
3) ```Get-Service sshd```: to check if the OpenSHH Server is running  
4) on HPC login, use ```scp file_to_be_downloaded your_username_on_windows@your_windows_ip:/download_place_on_windows```  
*if using GBW desktop, a typical command line would be: ```scp file_to_be_downloaded your_username_on_desktop@desktop_ip:/D:/Data```*  
5) check if the file is downloaded  
