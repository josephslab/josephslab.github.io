---
title: "Josephs Lab - Wiki"
layout: gridlay
excerpt: "Josephs Lab: Wiki"
sitemap: false
permalink: /wiki/
---

# Lab Wiki

**The absolute path to the Josephs’ lab shared folder is /mnt/research/josephslab**

### Connecting to HPCC using ssh key:

In terminal, enter:
```
ssh [username]@hpcc.msu.edu
```

You’ll be prompted to enter your password. For security reasons, nothing will show onscreen as you type. If it is your first time logging on, you may be asked if you would like to continue connecting because the authenticity of the address has not been verified. Double check that the address is correct and continue.

You are now in the **GATEWAY**.

You can do very limited things in gateway like moving files around and moving through directories.

To do more complicated things, you’ll need to move to a **DEVELOPMENT NODE**.

You can choose a development node yourself and move to it. 

For example, if you wanted to move to _dev-intel14.i_, the command would be
```
ssh dev-intel14
```

The second way is to have the least burdened node chosen for you. You will need to first load the module powetools
```
module load powertools
```

Then, move to the least burdened node
```
dev
```

From a development node, you can run scripts that take less than 2 hours to complete, submit jobs to SLURM etc.

### Submitting a Job to SLURM

If you’d like to do something that takes a significant amount of memory, or longer than two hours to complete, you will need to submit a job to SLURM.

More information on submitting and altering jobs can be found [here](https://wiki.hpcc.msu.edu/display/ITH/Job+Scheduling+by+SLURM “Job Scheduling by SLURM”) on the MSU HPCC wiki website. 

To successfully submit a job, your job script will need a header that provides job information which influences where in the queue your job will be.

Here is an example of a basic header for a bash script:

```
  #!/bin/bash
  #
  #SBATCH --job-name=something that makes sense to you
  #SBATCH --mem=how much memory is needed
  #SBATCH --time=days-hours:minutes:seconds  (ex 1-10:00:00 is one day and 10 hours)
  #SBATCH --mail-type=ALL (the kind of notifications you’d like to receive for the job)
  #SBATCH --mail-user=[netid]@msu.edu
  #SBATCH --nodes=how many nodes needed
  #SBATCH --ntasks-per-node= how many tasks on each node
  #SBATCH -c how many cores per node
  #SBATCH --output=path/to/slurm/output_folder/
  #
  #
```

Below the header will be the commands for your job.

Once your script is written, you can submit the script to SLURM using the _sbatch_ command.
```
sbatch my_cool_script.sh
```

The terminal will then print a job number for you to keep track of your job in the queue, check it’s status when running, and troubleshoot output.

### Checking on submitted jobs

To check the status of your job, 
```
sacct -j [job number]
```

To see a list of submitted or running jobs by you
```
qstat -u [netid]
```

### Job Arrays

A job array is a useful way to run multiple identical jobs in parallel in a single script. A job array will add a few changes to a regular job header.
Firstly, you’ll need to add an array specifier to your header
```
#SBATCH --array=1-totaltasknumber%tasksatatime
```

The first range of numbers after the “=” gives the number of task IDs to be assigned to the job and the number after the “%” gives the number of tasks to run at a time. 

For example, to run a job with 45 total tasks, and 5 tasks at a time, the header line would look like this:
```
#SBATCH --array=1-45%5
```

The second header change is to the SLURM output line. When you submit a job, the job number printed is represented by the capital *A*. The task represented by the little *a*.

```
 #SBATCH --output=path/to/slurm/output_folder/slurm-%A_%a.out
```

The above code is naming the slurm output to make it easier to troubleshoot code. 

For example, the output file for Job Number 360075 and task 14 of that job will be titled __slurm-360075_14.out__.
