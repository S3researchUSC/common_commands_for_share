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
