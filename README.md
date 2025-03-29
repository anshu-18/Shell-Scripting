# Shell-Scripting
	- Shell script consist of set of commands to perform a task.
	- It is a user interface use to perform a set of commands and interact with kernel.
	- It can be used to automate the task, ex: we can create a .sh file and include the sequence of commands which needs to executed time and again.
	- >echo $0 [cmd to find the type of shell script being used] 
	- Creating a script file:
		○ #!/bin/bash [shebang line , to specify which shell to use]
		○ How to run a script file ?
			§ Script should have rwx permission
			§ Run: ./script.sh OR bash script.sh OR /path/script.sh
		○ Single-line comment:- # [02_basic.sh]
		○ Multi-line comment:-  <<comment
						Add_comment
						Comment
		○ VARIABLES: [03_variables.sh]
			§ VAR_NAME=value
			§ VAR_NAME=$(pwd) [to store the output of linux command in a variable]
			§ echo $VAR_NAME
			§ Constant variables
				□ Syntax: readonly var_name="hello"
				
		○ ARRAYS
			§ Syntax: arr=(1 2 3 hey "hello anshu") [double quotes for more than one characters]
			§ echo "${arr[0]}" //too access value
			§ echo "${arr[*]}" [to print all the values of array]
			§ echo "${#arr[*]}" [to get the length of an array]
			§ echo "${arr[*]:1:3}" [to get the 3 values starting from idx 1 ]
			§ echo "${arr[*]:1}" [to get all the values starting from idx 1 to end of array]
			§ arr+=(5 7 8) [to add more elements inside array]
			§ Arrays key-value :
				□ Syntax:
					® declare -A arr
					® arr=( [name]=tom [age]=45)
					® echo "${arr[name]}"
		○ STRINGS
	- USER-INTERACTION:
		○ Taking input from the user
		○ Syntax: 1. read <name_of_variable>
			2. read -p "enter your msg that you want to display on screen " <name_of_variable>

	- ARITHMETIC OPERATIONS
		○ Using let cmd
		○ Syntax: let var_name=$a+$b
		○ echo "addition of a and  b is $var_name"
		○ OR
		○ echo "subtraction: $((a-b))"
		○ DOUBLE BRACES technique works on binary operators only not uniary operator
		
	- IF-ELSE Condition
		○ Syntax:
		○ ![image](https://github.com/user-attachments/assets/46e0025f-5bf8-42ea-9931-2338e83c019e)

		        
		
		
			
		
	- 
	- CASE
	- Ternary operator:
		○ Syntax: Condition1 && condition2 || condition3
		○ If condition1 is true then condition2 will get executed else condition3
		
	- LOOPS
		1. FOR loop
			Syntax: for i in 1 2 3 4 5 6
			              do
			                    echo "number is $1"
			             done
			
			OR
			Syntax: for i in {1..20} [to print the range of values from 1 to 20 (use of wildcards)]
			
			OR
			Syntax: for name in tom ron joy harry
			
			OR
			For loop with array
			arr=(1 2 3 harry)
			Len=${#arr[*]}
			for ((int i=0; i<$len; i++))
			
			- Example: iterate values from a file
				Items="/home/anshu/name.txt"
			          for var in $(cat $Items)
				do
				         echo $var
				done
				
		2. WHILE Loop
			Syntax: 
       num=10
			       count=0
			     
			      while [ $count -le $num ]
			      do
			               echo  "number: $count"
			               let count++
			     done
			
			Example: to read content from a file
				Syntax:
				    while read <variable>
				    do
				            echo $<variable>
				   done < file_name
				
			Example: to read content from csv file
			    Syntax:  IFS=internal field separator
			 
			         while IFS="," read c1 c2 c3
			         do
			               echo "$c1   |   $c2  |   $c3"
			        done < file.csv
			
			NOTE:- read about awk command in linux
			
		3. UNTIL Loop
			Opposite of while loop
			It will continue to run until condition is false, will exit once cond become true.
			Syntax:  
				val=10
				until [ $val -le 5 ]
				do
				       echo "val is $val"
				       val=$((val - 1))
				done 
				
		4. INFINITE Loop
			Syntax:
			    while true
			    do
			           echo "hello"
			           sleep 2s
			   done
			
	- FUNCTIONS
		Syntax:
			 function <func_name> {
			      //line of codes
			     echo "hello $1"
			     echo "age $2"
			}
			
			OR
			
			<func_name>() {
			      //line of codes
			}
			
			To call the function: 
				<func_name> <argument_1> <argument_2>
				
	- ARGUMENTS PASSING
		
		
		Example: 
		    for <var_name> in $@
		    do
		           echo "value: $<var_name>"
		   done
		○ Shifting Arguments
			- Shift is used to combine multiple arguments 
			- Example:
				echo "first argument: $1"
				
				shift
				echo "sec argument: $@"
				
			Output: 
			[anshu@fedora LearnShellScripting]$ ./20_shift_args.sh hello this is shifting argument
			first argument: hello
			sec argument: this is shifting argument
			
	-  exit command is used to exit from a script.
	-  exit status $? - gives you the status of previous cmd if that was successful 
	- Linux cmds:
		1. basename cmd: strip the directory info and only give filename
		2. dirname cmd: strip the filename and gives directory path
		3. realpath cmd: gives you full path for a file
		
		
		
	- BASH VARIABLES
		○ Predefined variables present in shell
		1. RANDOM - random integer b/w 0 and 32767 is generated. echo $RANDOM
		2. UID - user ID of the user logged in
		
	- REDIRECTION in Scripts
		○ > [override the content of file]
		○ >> [append the content inside a file]
		date > date.txt
		pwd >> date.txt
		
	- What is /DEV/NULL
		○ In case if you don't wanna print the output of a command on terminal or write in a file, we can redirect the output to /dev/null.
		○ Ex: cd /root &> /dev/null
		○ Ex: pwd &> /dev/null
		
	- PRINT NAME OF THE SCRIPT
		${0}
		echo "the name of the script is : ${0}"
		
	- LOG MESSAGES
		○ If you want to maintain the logging for your script, you can use logger inside script
		○ These logs are present inside /var/log/messages
		○ Ex: #logger "hey , collecting log"
		
	- DEBUGGING SCRIPTS
		○ Add set -x  in beginning of script to know what all line of commands has been executed.
		○ We can use set -e to exit the script when a command fail
		
	- RUNNING SCRIPT IN BACKGROUND
		○ Execute cmd :  nohup ./script.sh &
		
	- AUTOMATE SCRIPT
		○ Using At or Crontab command
		1. For scheduling only one time, use AT
			   at  12:09 PM
			          <your command>
			   Ctrl+D
			
			  atq is used to chk scheduled job
			  atrm <id> is used to remove the schedule
			
		2. For scheduling the task on regular interval, use Crontab
			  crontab -l is used to chk the existing jobs
			  crontab -e  is used to add new job
				 -> inside crontab -e write the command in editor to schedule the task based on you time frame.
				
	- PROJECTS
		○ Read about FILE SYSTEM in linux
POSTFIX is used to send mail from linux to gmail. And it uses SMTP protocol![image](https://github.com/user-attachments/assets/45ba0ebd-49bc-4d3e-a1c0-49d25ad92099)
