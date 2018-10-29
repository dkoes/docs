# Cluster

https://www.csb.pitt.edu/using-the-cluster/


## Running many small jobs

An easy way to run a lot of jobs that are described by a commandline is to generat a file containing all the commands you want to run and then use the following PBS script to launch them as an array job.  Each array index corresponds to a line (command) in your `cmds` file.

```
#!/bin/bash
#PBS -N I_forgot_to_name_my_job
#PBS -j oe
##may want to specify gpus=1
#PBS -l nodes=1:ppn=1
#PBS -l walltime=24:00:00
#PBS -q dept_24_core

echo Running on `hostname`
echo workdir $PBS_O_WORKDIR
echo ld_library_path $LD_LIBRARY_PATH

cd $PBS_O_WORKDIR
#the following extracts the PBS_ARRAYID'th line from cmds, prints the command and runs it
cmd=`sed -n "${PBS_ARRAYID}p" cmds`
echo $cmd
$cmd 

exit
```


## Sample MD script

This script assumes the prefix of your files (generated with prepare_amber.py) is the same as 
the directory you are running from.

```
#!/bin/bash
#PBS -N I_forgot_to_name_my_job
#PBS -j oe
#PBS -l nodes=1:ppn=1:gpus=1
#PBS -l walltime=24:00:00:00
#PBS -q dept_gpu


echo Running on `hostname`
echo workdir $PBS_O_WORKDIR
echo ld_library_path $LD_LIBRARY_PATH

#for some reason when the job starts on the node, it auto-cd's to your home dir
cd $PBS_O_WORKDIR

#scratch drive folder to work in
SCRDIR=/scr/$PBS_JOBID

#if the scratch drive doesn't exist (it shouldn't) make it.
if [[ ! -e $SCRDIR ]]; then
        mkdir $SCRDIR
fi

chmod +rX $SCRDIR

echo scratch drive ${SCRDIR}

cp $PBS_O_WORKDIR/*.in ${SCRDIR}
cp $PBS_O_WORKDIR/*.prmtop ${SCRDIR}
cp $PBS_O_WORKDIR/*_md2.rst ${SCRDIR}
cp $PBS_O_WORKDIR/*.inpcrd ${SCRDIR}

cd ${SCRDIR}

#amber setup
AMBERHOME=/usr/local/amber18
PATH=/usr/local/amber18/bin:$PATH

#setup to copy files back to working dir on exit
trap "mv *md3.nc $PBS_O_WORKDIR" EXIT

#run the MD
i=${PBS_O_WORKDIR##*/}
pmemd.cuda -O -i ${i}_md3.in -o $PBS_O_WORKDIR/${i}_md3.out -p ${i}.prmtop -c ${i}_md2.rst -r ${i}_md3.rst -x ${i}_md3.nc -inf $PBS_O_WORKDIR/mdinfo  

exit
```
