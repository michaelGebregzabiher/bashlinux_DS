Linux & Bash
9. Examination
This exam is divided into 2 exercises:

The first concerns the bash language (Mandatory to valid the exam)
The second concerns the jq tool (Optional part)
9.1 Examination : Bash - MANDATORY
Setting up the API
In this course, we've seen how a Linux system works. We could have gone into even more detail, but we've laid the foundations for the rest of the course. Follow the instructions below to complete the exercise.

Exercise to be performed obligatorily on the Linux machine provided.
Log on to your machine and run the following command to retrieve the API

wget --no-cache https://dst-de.s3.eu-west-3.amazonaws.com/bash_fr/api.tar
You now have a file with the extension .tar. This is simply an archive, like a zip compressed file, but specific to Linux. To manipulate this file, we use the tar command (for _tape archiver_). For all tar-based formats, you will see that the tar options are the same:

c : creates the archive
x : extract archive
f: uses the file given as a parameter
v: activates verb mode.
Uncompress the archive with the following command:

tar -xvf api.tar
The archive extract reveals the _api_ script

Run the api script after granting execution rights:

chmod +x api
./api &
Our API now runs at localhost (0.0.0.0) on port 5000.

It's perfectly possible to run the API without running it in the background, but running it will block any manipulation of your VM. You will then have to open a 2nd terminal and reconnect to the VM, working with the 2nd terminal only.
9.2 Examination
This API reveals the sales per minute of the largest graphics card reseller on the rtx3060, rtx3070, rtx3080, rtx3090 and rx6700 models. It is possible to retrieve this information using the cURL command. However, you may not have cURL on your machine. To remedy this, we use apt on Linux.

Order apt
apt is a package manager containing various software packages that you can install quite easily with a single line of code. We can do this as follows:

apt install software_name
In older versions of Ubuntu, you needed to use apt-get instead of apt. In most cases, you need sudo to force software installation rights.

To ensure that packages are up to date, you can use sudo apt update . To update software, you can use sudo apt upgrade . You can add or remove certain packages and completely remove software using the apt purge function.

Install curl with apt.

sudo apt-get update

sudo apt-get install curl
Now that we have curl, let's explain the tool.

Command curl
cURL, which stands for client URL, is a command-line tool for transferring files using URL syntax. It supports a number of protocols (HTTP, HTTPS, FTP, and many others). HTTP/HTTPS makes it an excellent candidate for interacting with APIs.

For example, rtx3060 sales can be retrieved using the following command.

curl "http://0.0.0.0:5000/rtx3060"
Create an exam_NAME folder, where NAME is your surname.

In this folder, create an exam_bash folder

Create a bash script inside the folder named exam.sh with execution rights -rwx---r-x.

The bash script will retrieve the sales figures for the various graphics cards and write the information to a sales.txt file in the form :

Scraping date
rtx3060:No. of sales
rtx3070:No. of sales
...

Here's an example of a sales.txt file:

Thu Apr 1 00:05:01 UTC 2021
rtx3060:18
rtx3070:20
rtx3080:20
rtx3090:2
rx6700:12
Thu Apr 1 00:06:01 UTC 2021
rtx3060:6
rtx3070:15
rtx3080:15
rtx3090:1
rx6700:15
...
...
To retrieve the current date and write it to the file, enter the following line in your exam:

echo "$(date)" >> sales.txt
Constraint: use of a function and a loop (for or while) is mandatory.

Create a Cron Job that runs your script only every minute from 7 AM to 9 PM during the months of March, June and November from monday to friday (copy the Cron Job to a cron.txt file in the folder)

Rendering : Bash
This gives us the following files and folders:

exam_NAME/exam_bash/exam.sh
exam_NAME/exam_bash/sales.txt
exam_NAME/exam_bash/cron.txt
One remaining exercise to do to validate this module!

9.2 Examination : JQ - OPTIONAL PART
Set up
You will enter the commands in an executable file (with execute permission +x) named exam_jq.sh. In order to validate the exercise, you must submit the exam_jq.sh file as well as a res_jq.txt file using the command ./exam_jq.sh > res_jq.txt. Don't forget that a human being will correct your files, so remember to clearly present your results in your 2 files.

Create in your exam_NOM folder, the exam_jq folder

Go there, and create an exam_jq.sh file like this:

#!/bin/bash

echo "1. Statement of question 1"
<command to respond>
echo "Command: <command to respond>"
echo "Answer: answer question 1 if asked"
echo -e "\n--------------------------------------\n"
...

echo "n. Question statement n"
<command to respond>
echo "Command: <command to respond>"
echo "Answer: answer question 1 if asked"
echo -e "\n--------------------------------------\n"
: place the command linked to the question in order to have the result of the command in the res_jq.txt file.
Complete the fields according to the questions of course. The Answer is not the result of the code but your interpretation of it.

Questions
Here is the link to download the json file for the exam:

wget https://dst-de.s3.eu-west-3.amazonaws.com/bash_fr/people.json
Only questions 1, 2 and 4 require an interpreted Answer.

Display the number of attributes per document as well as the name attribute. How many attribute do they have ? Display only the first 12 lines with the head command (notebook #2).

How many "unknown" values are there for the "birth_year" attribute ? Use the tail command to isolate the response.

Display each character's creation date and name. The creation date must be of this form: the year, the month and the day. Display only the first 10 lines (No response expected).

Some characters are born at the same time. Find all the pairs of ids (2 ids) of the characters born at the same time.

Return the number of the first movie (of the list) each character was seen in followed by the character's name. Display only the first 10 lines (No response expected).

Bonus
Add this command to separate the mandatory part and the optional part.

echo -e "\n----------------BONUS----------------\n"
No Answer is requested.

Save each of the commands in files in the format: people_<question_number>.json These files should be in a bonus/ folder.

Do not add anything to the res_jq.txt file. You must redirect the jq queries from the eval_jq.sh file to this file res_jq.txt.

The questions are to be carried out from the file created in the previous question except for question 6.

Delete documents where the height attribute is not a number.

Transform the height attribute into a number.

Return only characters whose height is between 156 and 171.

Return the smallest individual from people_8.json and display this sentence in one command: "<character_name> is <height> tall" Return the command in a people_9.txt file and not .json.

Rendering : JQ
Here is an example of the folders and files:

exam_NAME/exam_jq/exam_jq.sh
exam_NAME/exam_jq/res_jq.txt
exam_NAME/exam_jq/bonus/people_<6 to 9>.<json or txt>
Final render
Create an exam_NAME.tar archive

tar -cvf exam_NOM.tar exam_NOM
Command scp
The scp command is used to securely transfer a file or archive (folders are not transferable) via an SSH connection.

You can download your archive by running the following command on a terminal on your own machine.

scp -i "data_enginering_machine.pem" ubuntu@YOUR_IP:~/exam_NAME.tar .
More details about the above order:

- When you open your terminal on your local computer to transfer your archive from the VM, specify the absolute path to your data_enginering_machine.pem file

- Your archive will be downloaded into the same folder as your data_enginering_machine.pem file.
