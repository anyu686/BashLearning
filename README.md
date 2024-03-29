#Bash Learning Notes

## Echo 
1 `echo $?` print the return state of last command, 0 success, 1 failed__  

2 `echo $PATH` show default path__

3  `which <command name or scrit name>` show path of command/script__

4  Build in Command no need to load from disk, external command load from disk, build in command get use first if an external command has same name.  

5  to validate if a command is build in command `type <command name>`  

## Define variable 

1 `export VARNAME=name`, define varibale which can be accessed outside the current shell

2 `read A`, read input from user and assign the value to A 

3 `a=$(command)` e.g `a=$(date)`  
## Debug 

1 `Bash -x <script Name>` to see the each steps of script running, `+` indicate code which is excuted, without `+` is the output of shell    

## Read Input 
1 `$1 $2` refer to the 1st ,2nd input parameter  
2 `$?` refer to all input parameters, used in for loop  
3 `$#` count the input varibale number  
## string verification 
1 `-z $1` check if the first parameter is empty, return true if it is empyt,  e.g [if -z $1 -eq 1]  
2 `[[-z $1]] && exit 1`  '&&' only execute the 2nd command if the frist command is true  
3 `[[-z $1]] || exit 1` , `||` only execute the 2nd command if the frit command is false 
4 `[ -f $a ]`, check if $a is a file  
5 `[ -d $a ]`, check if $a is a directory  
6 `if [ $a -gt $b ] `or `if (( $a>$b ))`, `-lt` = `<`   
7 `[ -e $a ]`, check if file exist regardless if it is aregular file  
## Substitution
To do subsitution for the lines in a file, use for loop e.g ```for i in $(cat <filename>) ; do <substitution>; done```   
1  `echo ${DATA:-word}`  //return word if DATA not exist, but not set DATA  
2   `echo ${DATA:=word}` //return word if DATA not exist and set DATA=word  
3 
```
  D=$(date)  
  echo $D  
  Thu 22 Mar 2018 18:28:48 GMT  
  echo ${D:0:2}  
  Th
```
 4
 ```
 MB17598:~ yu.an$ DATA=   
 B17598:~ yu.an$ echo ${DATA:?Error}    
-bash: DATA: Error  
```
## Wall command
1 `wall << a` will boardcast all the followed command until it see string `a`  
## Pattern Matching
1 `${VAR#pattern}` //serach for pattern form beginning of varibable's vaule, delete the shortest path that match,  `##` match the longest path and retrunt the left part  
```
MB17598:~ yu.an$ Date=$(date)
MB17598:~ yu.an$ echo ${Date#*2}
4 Mar 2018 22:07:58 GMT
MB17598:~ yu.an$ echo ${Date##*2}
:07:58 GMT
```
2 ${VAR%pattern}  search the pattern from the end of string  
```
MB17598:~ yu.an$ echo ${Date%2*}  
Sat 24 Mar 2018 2  
MB17598:~ yu.an$ echo ${Date%%2*}  
Sat  
```
## Regular Expression 
## Caculation
1 `echo $((1+1))`  
2 `bc` deal with non-integers caculation `echo "scale=9; 10/3" | bc`     
## Grep
1 capture mutile matching , string1 or string B `grep -e string1 -e string 2`   
       
## cut   
1 `cut -f 1 -d : <file>` , `-f 1` first filed, `-d :`, delimater is `:`   
2 To cut string , use `echo "abc def" | cut -f 2 -d ' '`          
## awk    
`awk -F <delimater> : '/search pattern/ {Action}'` <Path to File> 
1 `awk -F : '{print $4}' /etc/passwd`  
2 `awk -F : '/user/ {print $4}' /etc/passwd`    
3 `awk -F : '$3>200' /etc/passwd` , print line if the 3rd filed > 200  
4 `awk -F : '$NF ~ /bin/' /etc/passwd`,print line if the last filed contatined `bin`  
5 Use awk in string, `echo "abc def" | awk '{ print $2 }'`    
## tr 
1 `echo hello | tr [a-z] [A-Z]`  
2 `echo hello | tr [:lower:] [:upper:]`  
## if 
```
   if expression  
   then 
       command 
   elif 
   then  
      command 
   fi   
``` 
## && and || 
`&&` and  , `[ -z $1 ] && echo variable $1 not exist`   
`||` or  , `[ -z $1 ] && echo variable $1 not exist || not exist``  
## for 
```
for i in something   
do   
	command1
	command2
done 
```   
e.g 
```
for i in {1..5}  
do   
	ping -c 1 192.168.0.$1  >/dev/null && echo 192.168.0.$ is pingable   
done    
```   
## case 
```
case $var in  
<string1>)  
echo string1 ;;  
<string2>|<string3>)  
echo string2 or string 3 ;;  
*)    
echo other string 
;;  
esac 
```  
## while
```
while condition  
do  
	command  
done  
```  
e.g
```
while [ $a> 4 ]; do  a=$(($a-1)) && echo $a; done
```  
## Functions
```
function help   
{  
 echo hi
}   
```  
or   
``` 
help ()  
{
echo hi  
}  
``` 
To include the functions from another script, use `source /path/to/script`   
## Arrays
1 `names=(linda lisa larua)`  `names[3]=<name>`, `echo ${names[2]}`  
2 `echo ${names[@]}`  show all elements  
3 `echo ${#names[@]}` count the number of element  
## Menu Interface  
```
#! /usr/bin/env bash
echo select from below 
select DIR in /var /var/log /etc
do  
	case $REPLY in  
	1 ) cd /var/;;  	
	2 ) cd /var/log ;;  
	3 ) cd /etc ;;  
done  
```  
note: use `$REPLAY` to refer to the unser input value;  
 
## Trap
`trap "echo quit" INT`  `INT is signal of Ctrl + C`   
