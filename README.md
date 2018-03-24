# Bash Learning Notes
## Echo 
1 `echo $?` print the return state of last command, 0 success, 1 failed__  

2 `echo $PATH` show default path__

3  `which <command name or scrit name>` show path of command/script__

4  Build in Command no need to load from disk, external command load from disk, build in command get use first if an external command has same name.  

5  to validate if a command is build in command `type <command name>`  

## Define variable 

1 `export VARNAME=name`, define varibale which can be accessed outside the current shell

2 `read A`, read input from user and assign the value to A 

## Debug 

1 `Bash -x <script Name>` to see the each steps of script running  

## Read Input 
1 `$1 $2` refer to the 1st ,2nd input parameter  
2 `$?` refer to all input parameters, used in for loop  
3 `$#` count the input varibale number  
## string verification 
1 `-z $1` check if the first parameter is empty e.g [if -z $1 -eq 1]  
2 `[[-z $1]] && exit 1`  '&&' only execute the 2nd command if the frist command is true  
3 `[[-z $1]] || exit 1` , `||` only execute the 2nd command if the frit command is false 
## Substitution
1  `echo ${DATA:-word}`  //return word if DATA not exist, but not set DATA  
2   `echo ${DATA:=word}` //return word if DATA not exist and set DATA=word  
3 >>D=$(date)
  >>echo $D  
  >>Thu 22 Mar 2018 18:28:48 GMT  
  >>echo ${D:0:2}  
  >>Th 
 
## Wall command
1 `wall << a` will boardcast all the followed command until it see string `a`  

