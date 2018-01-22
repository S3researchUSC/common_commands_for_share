### Linux or HPC command lines 
1. view csv file in format: 
```cat yourfile.csv | sed 's/,/ ,/g' | column -t -s, | less -S```

2. submit an interactive job **in normal account:** 
```qsub -I –l nodes=2:ppn=8 –l walltime=01:00:00```
**in HSDA:**
```qsub -A your_account_name```

3. output the number of lines in a text file (e.g. csv file) 
```wc -l < mytextfile```
