<p align="center">
<img src=https://github.com/brion4/linux-command-and-shell-scripting-assignment/assets/94459111/4e41cb5c-fc24-4cb8-b4e8-15cbf59d164c>
</p>

 # *Hands-on lab: Scheduled Backup Script*


## Scenario
- Imagine that you are a lead Linux developer at the top-tech company ABC International Inc. ABC currently suffers from a huge bottleneck: each day, interns must painstakingly access encrypted password files on core servers and back up any files that were updated within the last 24 hours. This process introduces human error, lowers security, and takes an unreasonable amount of work.

- As one of ABC Inc.'s most trusted Linux developers, you have been tasked with creating a script called backup.sh which runs every day and automatically backs up any encrypted password files that have been updated in the past 24 hours.

## Learning Objectives
By completing this final project, you will:

- Demonstrate your advanced shell scripting skills in a real-world scenario

- Apply the knowledge you've gained to reviewing and grading technical work submtted by your peers

## Deliverables
You will need to submit the following items for peer review:
Screenshots clearly displaying both the code and the output for each task
Your completed script file





# *Linux Commands and Shell Scripting - Final Project*

- Estimated time needed: 90 minutes

- Welcome to the hands-on lab for the final project!

- In this scenario, you are a lead Linux developer at the top-tech company ABC International Inc. As one of ABC Inc.'s most trusted Linux developers, you have been tasked with creating a script called backup.sh which runs every day and automatically backs up any encrypted password files that have been updated in the past 24 hours.

- Please complete the following tasks, and be sure to follow the directions as you go. Don't forget to save your work.


## Task 0
- Open a new terminal by clicking on the menu bar and selecting Terminal->New Terminal:

- Download the template file backup.sh by running the command below:

  `wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-LX0117EN-SkillsNetwork/labs/Final%20Project/backup.sh`

- Open the file in the IDE by clicking File-> then click on the file, which should have been downloaded to your project directory:


- About the template script backup.sh
You will notice the template script contains comments (lines starting with the # symbol). Do not delete these.
The ones that look like # [TASK {number}] will be used by your grader:

- Also, please do not modify any existing code above # [TASK 1] in the script.

## Task 1
- Navigate to # [TASK 1] in the code.

- Set two variables equal to the values of the first and second command line arguments, as follows:

- Set targetDirectory to the first command line argument
  
- Set destinationDirectory to the second command line argument
  
- This task is meant to help with code readability.

- The command line arguments interpreted by the script can be accessed via $1 (first argument) and $2 (second argument).

## Task 2
- Display the values of the two command line arguments in the terminal.

- Remember, you can use the command echo as a print command.

Example: `echo "The year is $year"`

## Task 3
- Define a variable called currentTS as the current timestamp, expressed in seconds.

- Remember you can customize the output format of the date command.

- To set a variable equal to the output of a command you can use command substitution: $() or \` \`

For example: `currentYear=$(date +%Y)`

## Task 4
- Define a variable called backupFileName to store the name of the archived and compressed backup file that the script will create.
The variable backupFileName should have the value "backup-[$currentTS].tar.gz"

- For example, if currentTS has the value 1634571345, then backupFileName should have the value backup-1634571345.tar.gz.

## Task 5
- Define a variable called origAbsPath with the absolute path of the current directory as the variable's value.
  
- You can get the absolute path of the current directory using the pwd command.

## Task 6
- Define a variable called destAbsPath whose value equals the absolute path of the destination directory.

- First use cd to go to destinationDirectory, then use the same method you used in Task 5.

## Task 7
- Change directories from the current working directory to the target directory targetDirectory.

- cd into the original directory origAbsPath and then cd into targetDirectory.

## Task 8
- You need to find files that have been updated within the past 24 hours. This means you need to find all files whose last-modified date was 24 hours ago or less.

- Define a numerical variable called yesterdayTS as the timestamp (in seconds) 24 hours prior to the current timestamp, currentTS.

Math can be done using $(()), for example:
`zero=$((3 * 5 - 6 - 9))`

- Thus, to get the timestamp in seconds of 24 hours in the future, you would use:
`tomorrowTS=$(($currentTS + 24 * 60 * 60))`


Note on arrays
- In the script, you will notice the line:
`declare -a toBackup`

- This line declares a variable called toBackup, which is an array. An array contains a list of values, and you can append items to arrays using the following syntax:
`myArray+=($myVariable)`

- When you print or echo an array, you will see its string representation, which is simply all of its values separated by spaces:

```
$ declare -a myArray
$ myArray+=("Linux")
$ myArray+=("is")
$ myArray+=("cool!")
$ echo ${myArray[@]}
```
`Linux is cool`

- This will be useful later in the script where you will pass the array $toBackup, consisting of the names of all files that need to be backed up, to the tar command. This will archive all files at once!

## Task 9
- Within the $() expression inside the for loop, write a command that will return all files and directories in the current folder.

- There is a very clean way of doing this using ls.

## Task 10
- Inside the for loop, you want to check whether the $file was modified within the last 24 hours.
- To get the last-modified date of a file in seconds, use `date -r $file +%s` then compare the value to yesterdayTS.

- `if [[ $file_last_modified_date > $yesterdayTS ]]` then the file was updated within the last 24 hours!

- Since much of this wasn’t covered in the course, for this task you may copy the code below and paste it into the double round brackets (()):
`date -r $file +%s > $yesterdayTS`

## Task 11
- In the if-then statement, add the $file that was updated in the past 24-hours to the toBackup array.
  
- Since much of this wasn’t covered in the course, you may copy the code below and place after the then statement for this task:
`toBackup+=($file)`

## Task 12
- After the for loop, compress and archive the files, using the $toBackup array of filenames, to a file with the name backupFileName.

## Task 13
- Now the file $backupFileName is created in the current working directory.

- Move the file backupFileName to the destination directory located at destAbsPath.

Congratulations! You are now done the coding portion of the lab!

## Task 14
- Open a new terminal by clicking on the menu bar and selecting Terminal->New Terminal

## Task 15
- Save the backup.sh file you're working on and make it executable.

- Verify the file is executable using the ls command with the `ls -l` option:
`ls -l backup.sh`

## Task 16
- Download the following .zip file with the wget command:
`wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-LX0117EN-SkillsNetwork/labs/Final%20Project/important-documents.zip`

- Unzip the archive file:
`unzip -DDo important-documents.zip`
Note: -DDo overwrites without restoring original modified date.

- Update the file’s last-modified date to now:
`touch important-documents/*`

- Test your script using the following command:
`./backup.sh important-documents .`

- This should have created a file called backup-[CURRENT_TIMESTAMP].tar.gz in your current directory.

## Task 17
- Copy the backup.sh script into the /usr/local/bin/ directory. (Do not use mv.)
 Note: You may need to use sudo cp in order to create a file in /usr/local/bin/.

- Test the cronjob to see if the backup script is getting triggered by scheduling it for every 1 minute.

`*/1 * * * * /usr/local/bin/backup.sh /home/project/important-documents /home/project`
Please note that since the Theia Lab is a virtual environment, we need to explicitly start the cron service using the below command:
`sudo service cron start`
Once the cron service is started, check in the directory /home/project to see if the .tar files are being created.

- If they are, then stop the cron service using the below command, otherwise it will continue to create .tar files every minute:
`sudo service cron stop`

- Using crontab, schedule your /usr/local/bin/backup.sh script to backup the important-documents folder every 24 hours to the directory /home/project.

## Task 18
- Save the current working file backup.sh with CTRL+s Windows/Linux, CMD+s MAC or by navigating to File->Save as seen below:

- Download the file to your local computer by navigating to File->Download as seen below:

- You may save the file as backup.sh




 **Authors** :
  Sam Prokopchuk

 **Other Contributors** :
  Rav Ahuja

 **Change Log** : 
| Date (YYYY-MM-DD) 	| Version 	| Changed By     	| Change_Description            	|
|-------------------	|---------	|----------------	|-------------------------------	|
| 2023-04-28        	| 1.3     	| Nick Yi        	| QA Pass                       	|
| 2023-04-24        	| 1.2     	| Nick Yi        	| ID Review                     	|
| 2023-03-20        	| 1.1     	| Jeff Grossman  	| Extract  LOs, Intro, Overview 	|
| 2022-04-05        	| 1.0     	| Sam Prokopchuk 	| Create lab, exercises         	|


Copyright (c) 2022-23 IBM Corporation. All rights reserved.
