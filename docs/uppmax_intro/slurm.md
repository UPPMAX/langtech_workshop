# Submitting jobs

!!! question
    - This is a short introduction in how to reach the calculation nodes

## Slurm, sbatch, the job queue
- Problem: 1000 users, 500 nodes, 10k cores
- Need a queue:

![Image](../img/queue1.png)
- x-axis: cores, one thread per core
- y-axis: time
<br/><br/>
- [Slurm](https://slurm.schedmd.com/) is a jobs scheduler
- Plan your job and but in the slurm job batch (sbatch)
    `sbatch <flags> <program>` or
    `sbatch <job script>`

- Easiest to schedule *single-threaded*, short jobs

![Image](../img/queue2.png)
![Image](../img/queue3.png)

- Left: 4 one-core jobs can run immediately (or a 4-core wide job).
    - The jobs are too long to fit in core number 9-13.
- Right: A 5-core job has to wait.
    - Too long to fit in cores 9-13 and too wide to fit in the last cores.
How to submit a job to Slurm?

```bash
sbatch  -A naiss2023-22-247 -t 10:00  -p core  -n 10  my_job.sh
```

What should a jobscript contain?
  
- project number
- max time
- partition
- number or core and/or nodes
- job name
- special features
  
### A typical job script:

```bash
#!/bin/bash
#SBATCH -A naiss2023-22-247
#SBATCH -p node
#SBATCH -N 1
#SBATCH -t 24:00:00

module load software/version

./my-script.sh
```

Useful SBATCH options:

- `--mail-type=BEGIN,END,FAIL,TIME_LIMIT_80`
- `--output=slurm-%j.out`
- `--error=slurm-%j.err `


Useful commands:

- `jobinfo -p devel`
- `sinfo -p node - M snowy`
- `jobinfo -u username --state=running`
- `jobinfo -u username --state=pending`
- `salloc -A naiss2023-22-247 --begin=2023-03-24T08:00:00` starts an interactive job earliest tomorrow at 08:00

### How to cancel jobs?
- `scancel <jobid>`

## Job dependencies
- `sbatch jobscript.sh`   submitted job with jobid1
- `sbatch anotherjobscript.sh`  submitted job with jobid2
- `--dependency=afterok:jobid1:jobid2` job will only start running after the successful end of jobs jobid1:jobid2
- very handy for clearly defined workflows
- One may also use `--dependency=afternotok:jobid` in case you’d like to resubmit a failed job, OOM for example, to a node with a higher memory: `-C mem215GB` or `-C mem1TB`


## GPU flags

```bash
#SBATCH -M snowy
#SBATCH --gres=gpu:1
#SBATCH --gpus-per-node=1
```

!!! Example of a job running on part of a GPU node
    ```bash
    #!/bin/bash
    #SBATCH -J GPUjob
    #SBATCH -A snic2023-22-247
    #SBATCH -t 03-00:00:00
    #SBATCH -p core
    #SBATCH -n 16
    #SBATCH -M snowy
    #SBATCH --gres=gpu:1
    #SBATCH --gpus-per-node=1

    module use /sw/EasyBuild/snowy/modules/all/
    module load intelcuda/2019b
    ```

## I/O intensive jobs: use the scratch local to the node

!!! Example
    ```bash
    #!/bin/bash
    #SBATCH -J jobname
    #SBATCH -A naiss2023-22-247
    #SBATCH -p core
    #SBATCH -n 1
    #SBATCH -t 10:00:00

    module load bioinfo-tools
    module load bwa/0.7.17 samtools/1.14

    export SRCDIR=$HOME/path-to-input

    cp $SRCDIR/foo.pl $SRCDIR/bar.txt $SNIC_TMP/.
    cd $SNIC_TMP

    ./foo.pl bar.txt

    cp *.out $SRCDIR/path-to-output/.
    ```


## Profiling on the GPUs
- `nvidia-smi`

    - `nvidia-smi dmon -o DT`
    - `nvidia-smi --format=noheader,csv --query-compute-apps=timestamp,gpu_name,pid,name,used_memory --loop=1 -f sample_run.log`
    - `nvidia-smi --help` or `man nvidia-smi`

- `module load nvtop`

    - `nvtop`


## Additional information

- [UPPMAX webpage](https://www.uppmax.uu.se/)
- [Slurm](https://www.uppmax.uu.se/support/user-guides/slurm-user-guide/)
- [Snowy](https://www.uppmax.uu.se/support/user-guides/snowy-user-guide/)
- [GPU:s on Snowy](https://www.uppmax.uu.se/support/user-guides/using-the-gpu-nodes-on-snowy/)
- [TensorFlow on Snowy/Bianca](https://www.uppmax.uu.se/support/user-guides/tensorflow-user-guide/)

 
!!! info "Keypoints"
    - You are always in the login node unless you:
        - start an interactive session
        - start a batch job
    - Slurm is a job scheduler
        - add flags to describe your job.
 

