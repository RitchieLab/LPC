# LPC Documentation for the Ritchie Lab

*Written by members (and friends) of the Moore lab (https://github.com/EpistasisLab) and modified by the Ritchie Lab.*

## Contents

- [LPC Documentation for the Ritchie Lab](#lpc-documentation-for-the-ritchie-lab)
  * [Introduction](#introduction)
  * [Links and other resources](#links-and-other-resources)
  * [Getting Started (e.g., new students)](#getting-started--eg--new-students-)
  * [Logging into the LPC](#logging-into-the-lpc)
    + [Logging in from Linux/Mac Terminal:](#logging-in-from-linux-mac-terminal-)
    + [Logging in from Windows](#logging-in-from-windows)
    + [Logging in from MacOS](#logging-in-from-macos)
      - [Using Cyberduck](#using-cyberduck)
  * [Navigating the LPC from a command line](#navigating-the-lpc-from-a-command-line)
  * [Customizing your environment](#customizing-your-environment)
  * [Using queues](#using-queues)
  * [Submitting Jobs](#submitting-jobs)
  * [Best practices & Miscellaneous tips](#best-practices---miscellaneous-tips)
  * [Troubleshooting](#troubleshooting)
  * [LPC Commands Cheat Sheet](#lpc-commands-cheat-sheet)
    + [LSF (job scheduling system) commands](#lsf--job-scheduling-system--commands)
    + [PMACS software module commands](#pmacs-software-module-commands)
    + [Miscellaneous commands](#miscellaneous-commands)
    + [Sample job script](#sample-job-script)
    + [Frequently asked questions](#frequently-asked-questions)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Introduction

The LPC (Limited Performance Computing) is a shared computing resource with a large number of processing cores upon which different computational tasks can be run.
The LPC can be used to run computing processes that require a larger amount of memory that most PCs or laptops have available, as well as to run many processes simultaneously (on separate computing cores) and thus parallelize a large number of computational tasks.
Each computing process (e.g., running a machine learning algorithm on a dataset), can be submitted (as a 'job') to an appropriate LPC queue (i.e. a program that manages the running of jobs from different users on cores of the LPC.
Each user of the LPC is set up with a home directory within which they can put the code or data they wish to run, and within which job outputs can be saved.
In order to use the LPC you will need to learn how to access it, how to navigate to your home directory, basic unix/linux commands, how to set up your 'environment' (so that the software, coding languages, and packages you will need are available to run your job, how to submit a job to a queue, how to manage and monitor your jobs, and best practices for LPC use.

## Links and other resources

- [PMACS Wiki - LPC](https://wiki.pmacs.upenn.edu/pub/LPC)

- [PMACS Wiki - LSF Basics](https://wiki.pmacs.upenn.edu/pub/LSF_Basics)

- [PMACS Wiki - Batch Computing](https://wiki.pmacs.upenn.edu/pub/Batch_Computing)

- [Ritchie Lab Wiki - Unix Tutorial](https://ritchielab.org/wiki) (Pennkey required)

- [Unix Tutorial From Binglan Li](https://docs.google.com/presentation/d/1Xx5ztakEVnGDImlTOkspCy1yRAvqe_esSIuTfV3KYv0/edit#slide=id.p)

## Getting Started (e.g., new students)

- **Step 1: Get your PennKey and request LPC account access.** If you don't yet have a PennKey, please email medhelp@pennmedicine.upenn.edu to request one. Then, you can contact Anastasia to help you request access to the LPC. You will be assigned an account username which will serve as the name of your home directory as well as be used to log onto the LPC.
- **Step 2: Set up VPN for off campus LPC access**.
Notes:The LPC can no longer be accessed from AirPennNet. In order to connect on or off campus you will first need to connect to campus with a virtual private network (VPN).
  - First, make sure you enroll in [DUO Two-factor authentication](https://wiki.pmacs.upenn.edu/pub/HSRDC_Getting_Started#Duo_Two-Factor_Authentication). This is needed to access most online UPenn resources from off campus.
  - Next install the [Pulse Secure Software from DART](https://www.med.upenn.edu/dart/assets/user-content/documents/manually-install-and-setup-vpn-on-mac.pdf). Detailed instructions can be found [here](https://www.isc.upenn.edu/sites/default/files/pulse_secure_vpn_cc.pdf).


When each of these are complete, you should be able to log into the LPC using the instructions that follow. Note: You'll need to log into the VPN prior to logging into LPC.

## Logging into the LPC

To login to the LPC (and reach your home directory) you will need either a terminal program (i.e. command line) or (if preferred) a graphical user interface (GUI) program. These programs differ if you have Windows, Mac or Linux Machine. Please see the following link for your appropriate operating system and style of login:
https://wiki.pmacs.upenn.edu/pub/LPC  (Under 'Login Software Installation')
A specific Windows example is provided later in this section.
Once you have an appropriate program, you will use it to log on to a server (based on who you are affiliated with). This file server/host is a head node, from which you can navigate the LPC directories (including your home) and submit jobs.  

The Ritchie Lab has its own server on LPC, which can be used to run small and non-resource interactive interactive jobs. The full instructions for accessing this server, including a basic overview of the folder structure and how to set up the Ritchie Lab environment, are currently located in the Ritchie Lab orientation materials on the shared Box folder and pinned to the #general Slack channel. 

In addition, there are 3 other servers relevant to this group for the below tasks, but you cannot submit jobs to the LPC from these servers:

- sciget (sciget.pmacs.upenn.edu): you can ssh to it and it has outbound network access. Primarily useful for wget, git, svn, etc.
- transfer (transfer.pmacs.upenn.edu) is used for transferring files from LPC to a local machine (sftp, scp and rsync). You cannot ssh to it.
- scisub (scisub.pmacs.upenn.edu) is the submit host used by many other LPC user groups. It is open to the world (SSH only – i.e. a secure remote login protocol). Be aware that scisub is a virtual host with limited computing power and does not currently mount project or home directories. It cannot be used to run local processes or manually install environment packages. For this reason, you will mostly not use this 


### Logging in from Linux/Mac Terminal:
`ssh username@servername.pmacs.upenn.edu`

### Logging in from Windows

It is useful to install both the terminal and GUI software below.
The terminal is best for submitting jobs and the GUI is best for navigating and managing the file hierarchy and copying files to and from the LPC.

- **Windows (Terminal): [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/)**
- **Windows (GUI): [WinSCP](https://winscp.net/eng/download.php)**
- **Windows (All-in-One): [MobaXterm](https://wiki.pmacs.upenn.edu/public/MobaXterm)**

**Logging in with PuTTY:**
- Ensure you are connected to VPN via PulseSecure.
- Open the putty .exe file
- In the 'Session' window, enter `servername.pmacs.upenn.edu` under 'Host Name'
- Confirm `'Port' = 22` and `'Connection type' = SSH`
- [For convenience] In the 'Connection/Data' window put the LPC username you were assigned into 'auto-login username'
- [For convenience] Go back to the 'Session' window and type in any session 'name' into 'Saved Sessions'. E.g. 'LPC_sarlacc'
- [For convenience] Click save, and this information will be available to be loaded your next time opening Putty
- Make sure you session is loaded and click 'Open' at bottom of the window
- A terminal will open up requesting your username (if you didn't save it in step 5).
- Lastly you will be prompted for your password.

**Logging in with WinSCP:**
- Ensure you are connected to VPN via PulseSecure.
- Open WinSCP software
- In the 'Session' window, enter `servername.pmacs.upenn.edu` under 'Host Name'
- Confirm `'Port' = 22`, `'Connection type' = SSH`, and `'File protocol' = SFTP`
- Enter your username and password where indicated
- [For convenience] Click Save and give your session any name for future use.
- Click 'Login' to connect, and a GUI will open up allowing you to view both your local PC's directory as well as the directory on the LPC (it should open you up to your home directory the first time logging on).

Note that it is also possible to configure WinSCP to automatically open a putty terminal upon connection.

**Logging in with MobaXterm:**
- This is the PMACS preferred method to interact with LPC.
- MobaXterm can be downloaded from https://mobaxterm.mobatek.net/, see https://mobaxterm.mobatek.net/documentation.html#2 for additional documentation
- Please consult the instructions on the PMACS wiki for more details regardig usage and installation 

### Logging in from MacOS

As mentioned in the above section, while MacOS built-in terminal is sufficient for submitting jobs, the Cyberduck GUI can be helpful for navigating the file structure.

#### Using Cyberduck
- [Download](https://cyberduck.io/download/) Cyberduck
- Ensure you are connected to VPN via PulseSecure
- Open Cyberduck
- Select `Open Connection` on the top left
- In this window, select `SFTP (SSH File Transfer Protocol)`
- Enter `servername.pmacs.upenn.edu` under `'Server'`
- Confirm `'Port' = 22`
- Enter your PMACS username and password
- Click `Connect`, and a GUI will open up allowing you to view the directory on the LPC (it should open you up to your home directory the first time logging on).

<img src="images/cyberduck.png" width="700">

## Navigating the LPC from a command line

Linux commands are needed to navigate the LPC from a terminal (e.g. PuTTY).
See the following link for an overview of basic Linux commands:

https://wiki.pmacs.upenn.edu/pub/Linux_Basics

Some of the most commonly used basic commands include:

- `ls` (lists contents of current directory)
- `ls -a` (lists contents of current directory including hidden files)
- `cd somedirectory` (move from current directory to 'somedirectory')
- `cd ..` (move back one level in the folder hierarchy towards the root folder)
- `mkdir somedirectory` (make a new directory called `somedirectory`)
- `head myfile.txt` (show the beginning of a file)

A great tutorial on how to effectively use a Unix command line is available at https://missing.csail.mit.edu/.

## Customizing your environment

Depending on what you want to run on the LPC, you may need to install various applications, packages, programming language versions, etc.
To avoid confusion and keep things centralized, PMACS installs and manages common applications in a shared central directory that are available to all the hosts in our cluster.
The LPC terms these environmental elements as 'modules'.
Modules can be loaded or unloaded to be made available in your run environment.
This means that these modules will be available if you were to run a program locally or when you submit a job from a given host.
Terminal commands for working with modules are available at this link:

https://wiki.pmacs.upenn.edu/pub/LPC#Modules

Alternatively if some application or package is not available or (for some reason) can't be installed by PMACS under modules, you can install such packages or applications in your home directory.
Be advised that PMACS provides very limited (if any) support when loading or using such installations on your own.

## Using queues

The first thing to understand before trying to schedule jobs are 'queues'.
At face value, a queue represents a set of pending jobs (i.e. a 'container' for jobs).
On the LPC different queues are available to different user groups allowing them to run their jobs.
You must be associated with, and have permission from, a specific user group in order to submit jobs to their associated queue.
Each queue is set up by PMACS with their own set of rules, defaults, and access to specific execute hosts (i.e. the servers comprised of computing cores where individual jobs are run).

More detail on the Ritchie Lab queues including template submission scripts can be found in the Ritchie Lab orientaion materials on the shared Box folder and pinned to the #general Slack channel.

There are a few general queue types:

- `normal`: For most jobs.
- `long`: For long running jobs (more than 24 hr).
- `interactive`: For jobs that are run interactively.

More information on queues in general is available here:

https://wiki.pmacs.upenn.edu/pub/LSF_Basics

## Submitting Jobs

High performance parallel computing codes generally run in "batch" mode.
Batch jobs are controlled by scripts written by the user and submitted to a batch system that manages the compute resource and schedules the job to run based on a set of policies.
We use the term "job" to refer to a "batch job".

Computing 'jobs' can be submitted individually from the command line, or you can write and run an executable script to submit multiple jobs to a queue simultaneously.

**IBM's LSF documentation is available here:**
https://www.ibm.com/support/knowledgecenter/en/SSWRJV_10.1.0/lsf_welcome/lsf_welcome.html

Additionally, if you are planning to submit a large number of resource intensive jobs, it is recommended to post in the #support-lpc Slack channel with an estimate of the number of nodes the jobs will occupy and amount time they will take to complete. This helps us coordinate schedules among lab members.

## Best practices & Miscellaneous tips

To avoid accidental deletion or overwriting of files it is recommended that you put these aliases in your .bashrc:

- alias rm='rm -i'
- alias mv='mv -i'
- alias cp='cp -i'

Each of these will prompt linux to ask you confirmation for the corresponding action.

To avoid filling up our disk space, plan to direct large job outputs and easily generated intermediate files to `/project/scratch/`. You can check the disk you are working on by using `realpath .` or `pwd -P` and the amount of space left by using `df -h`. Note that scratch space is not backed up, so you should not use it for long term storage of data that is near and dear to you!!!

## Troubleshooting

If you have any question, you can post in the #support-lpc Slack channel and, if necessary, submit a ticket at https://helpdesk.pmacs.upenn.edu/

It's also a good idea to provide your ip address when asking a question regarding connection: http://www.med.upenn.edu/myip.


## LPC Commands Cheat Sheet

### LSF (job scheduling system) commands

| Command | Description |
|---------|-------------|
| `bjobs` | Show unfinished jobs |
| `bjobs -sum` | Summarize active jobs |
| `bjobs -u ryanurb` | Show jobs for user `ryanurb` |
| `bkill 12345` | Kill job with ID `12345` |
| `bkill 0` | Kill all jobs that belong to you |
| `bhosts doi_exe` | Show server hosts |
| `bhosts` | Show all hosts |
| `bswitch` | Switch a job to a different queue |

Some other LSF commands can be found [here](https://www.med.upenn.edu/hpc/assets/user-content/documents/lsf-quick-reference_user_commands.pdf).

### PMACS software module commands

| Command | Description |
|---------|-------------|
| `module list` | List loaded modules |
| `module avail` | List all available modules |
| `module avail python` | List available python modules |
| `module load python/3.7` | Loads the module named `python/3.7` |
| `module unload python/2.7.10` | Unloads the module named `python/2.7.10` |
| `module switch gcc/4.9.4 gcc/6.2.0` | Swap out module `gcc/4.9.4` for `gcc/6.2.0` (useful for changing software versions) |

### Miscellaneous commands

| Command | Description |
|---------|-------------|
| `df -h` | Get current disk usage and total disk capacity |
| `du -hs` | Get size of current directory |

*Please note that at the request of PMACS, `du` commands should be used sparingly to avoid catastrophic burden on the filesystem*

### Sample job script

```bash
#!/bin/bash
#BSUB -J myjobname
#BSUB -o outputfile.%J.out
#BSUB -e errorfile.%J.err
#BSUB -q epistasis_normal
#BSUB -M 10000
module add python/3.7
cd /project/moore/users/myhomedirectory
python3.7 script.py -parA 0 -parB value
```

Assuming this is saved to a file named `script.sh` or `script.bsub`, you can submit the job by running:

```bash
$ bsub < script.sh
$ bsub < script.bsub
```
### Frequently asked questions

1. **My jobs have been stuck in the queue with `PENDING` status forever and I need them to start running!**
   
   Unfortunately, if many other people are also running jobs, you may just have to wait your turn. You can check how many jobs are waiting in our queues using the command
   `bjobs -u "all" |grep "epistasis"`

   However, even if there are many jobs waiting, there are some ways that you might be able to reduce how long your job sits in the queue. Sometime people will request much more memory, walltime, and/or nodes than the job actually needs to run. Your job cannot start until the resources you request are available, so the more you request, potentially the longer it could take to start. If you have ran a similar job before, check the resource usage to see the max memory and time it took to run. You may be able to reduce your current resource requests based on what you find. Also make sure that the program or function you are running is actually able to take advantage of multiple nodes. For example, requesting 16 nodes to run an Rscript that you haven't parallized will reserve 15 extra nodes for nothing.
   
   Remember if you are running an analysis that requires a lot of resources, it's a good idea to post in #support-lpc with a summary of your compute needs and time it will take to complete so that all lab members can know and plan accordingly and make sure there are no deadline conflicts.

2. **I calculated how long my jobs will take to run on LPC and it is months of compute time!**
   
   You may ask Marylyn about possibly moving your analysis, or a portion or your analysis, to DNAnexus. If you want to use DNAnexus to run an analysis, generally you will need to do some cost scoping to have a rough idea of the total compute costs before you submit. 
   
   Remember that you can auto-launch jobs on DNANexus similar to how you would run a job array on LPC using `dx clone`. For example, if you have a number of vcf input files you would like to run the using the same BioBin parameters, you can run the job once, then clone the job for each additional input file in a certain directory, etc. An example command to run BioBin using the same phenotype file and parameters with multiple VCF inputs (named by gene and position) would be something like this
   
   ```for i in $(dx ls); do fileid=$(dx describe  $i | grep "ID" | awk '{print $2}'); gene=$(echo $i | cut -d"." -f3); positions=$(echo $i | cut -d"." -f3,5 | sed 's/\./_/g');dx run biobin --clone job-jobid -ivcf_file=${fileid}  -iphenotype_file="file-fileid" -ibiobin_args="-F 0.01 --weight-loci Y --bin-pathways N --bin-regions Y --bin-minimum-size 1 --bin-interregion N --genomic-build 37 --include-region-names ${gene}" -ioutput_prefix="biobin_${positions}" --name "Biobin - Latest - ${positions}" --destination "project-projectid:/Output_Folder/${gene}" -y; done;```

3. **How can I run the same job on a bunch of different input files or with a bunch of different parameters without creating a `bsub` script for each one?**
   
   This is a perfect scenario for subitting an array job! The array index is saved into a variable called `LSB_JOBINDEX`. Say you want to run `bcftools norm` for 3 chromosomes with in files named `chr1.vcf`, `chr2.vcf`, and `chrX.vcf`. You could make the following changes to your script
  
  ```bash
   #!/bin/bash
   #BSUB -J jobname[1-3]
   #other BSUB options as normal

   #job commands
   myArray=("1" "2" "X") 
   myValue="${myArray[${LSB_JOBINDEX} - 1]}"  # to access each element in the array
   bcftools norm -m -any /path/to/file/chr${myValue}.vcf -Ou | bcftools view -Q 0.05:minor -c 20:minor -Ov > chr${myValue}"_norm.vcf"
   ```

   If all of your chromosome file names contain integers, you could even simplify this to just using the `LSB_JOBINDEX` variable directly like
   
   ```bash
   #!/bin/bash
   #BSUB -J jobname[1-22]
   #other BSUB options as normal

   #job commands
   bcftools norm -m -any /path/to/file/chr${LSB_JOBINDEX}.vcf -Ou | bcftools view -Q 0.05:minor -c 20:minor -Ov > chr${LSB_JOBINDEX}"_norm.vcf"
   ```
   

   Another tip is that you can also use a command to get the array. For example if you have a list of chr files called `chr1.vcf` etc., you can do something like      
   ```bash
   #!/bin/bash
   #BSUB -J jobname[1-3]
   #other BSUB options as normal

   #job commands
   myArray=(`ls -1 /path/to/input/files/chr*vcf`) # you can chain sed, cut, etc. commands here using pipes if you want to format the values in the array!
   myValue="${myArray[${LSB_JOBINDEX} - 1]}" 
   bcftools norm -m -any ${myValue} -Ou | bcftools view -Q 0.05:minor -c 20:minor -Ov > ${myValue}".norm.vcf"
   ```

4. **My job finished but it didn't output anything. What happened?**

   First, make sure you have enabled the options to get a resource summary emailed to you and to output the `.err` file. Commonly a few things could have happened.

   1. The job produced an error of some sort and you will need to fix your script.
   2. The job ran out of walltime or memory. You can look at the resource usage e-mail to see if this happened. 
   3. The job ran fine, but there was no disk space to write the output file. If you didn't get any errors and the resource usage looks fine, you can check which disk you were writing the output file to using `pwd -P` and how much space is left on the disk using `df -h`. If there is limited space, you may need to either temporarily direct your output to a `scratch` disk or work with other lab members to move files around. 

5. **I can't get my R package to install.**

   There are a number of reasons why this may happen. If you get an error such as
   `ModuleCmd_Load.c(208):ERROR:105: Unable to locate a modulefile for []`
   the issue may be as simple as quitting the R session, loading a module for the library that you are getting an error about, and restarting R. `gcc`, `boost`, `mpfr`, and `mpc` are common offenders.

6. **LPC is running very slowly!**

   First, you might want to check with others in the lab to see if they are experiencing similar issues and it's not just a glitch or momentary network problem. You might also want to have a look at the current running processes using `top`. If you or someone else is running a resource intensive process from the log in node, it might be best to kill the process and start an `ibash` session.
   
7. **How do I deal with all of these job notification emails?**

   It can be helpful to set a filter in Outlook to direct job notification emails to a folder other than your Inbox. You should be able to filter all jobs from sender "LSF" or similar. 

8. **I'm getting an error or have a problem that wasn't mentioned here and I don't know what it means or how to fix it.**
   
   Well the first thing we usually want to do in this case is the classic Google/StackOverflow combination. _Most_ of the time, you probably haven't broken something beyond repair and instead just found a common bug that has already been solved by many other people on the internet. 
   
   If Google doesn't work, you may want to search for keywords from your error in the lab's Slack to see if any other lab members have come across the problem before. If you can't find it, you can post the error in #support-lpc. It is great practice to post the full error message along with the line of code or command that you were running. If you have a problem with a script another lab member wrote for you, it's also great to provide a small, reproducible example that they can run and try to troubleshoot.

   Lastly, if you are having an issue with something like installing a software package or a bizarre problem with a job submission and have exhausted all the other options, you can try submitting a ticket to DART at [helpdesk.pmacs.upenn.edu](helpdesk.pmacs.upenn.edu). Again they will best be able to help you if you give them all the relevant detail mentioned above. 

   
