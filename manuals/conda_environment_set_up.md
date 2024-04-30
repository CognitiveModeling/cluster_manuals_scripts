### Set-up

1. Install mamba
	1. download file: https://github.com/conda-forge/miniforge#mambaforge (Mac OS: brew install miniforge https://naolin.medium.com/conda-on-m1-mac-with-miniforge-bbc4e3924f2b ???)
	2. Use compute node for package installation: `srun --pty bash`
	3. Install with `bash Miniforge3-Linux-x86_64.sh`
	4. pick install directory to your work folder, your work directory is at `/mnt/qb/work/goswami/gkd...`
	5. Type yes to add mamba to .bashrc
	6. If you already have a conda installation (not recommended but as is the case at the mlcloud slurm), delete conda sourcing in `~/.bashrc` file

2. Create Environment by
	`mamba create -n $envname -python=3.xxxx`
3. Install all needed packages using

	`mamba activate $envname`

	`mamba install $packagename1 $packagename2 ...`

4. Back up environemnts using

	`conda env export --from-history > <filename.yml>`
 
	Double check whether packages are listed correctly!
  
5. Recreate environment from backup

	`mamba create -n $envname -python=3.xxxx`

	`mamba env update -n $envname --file <filename.yml>` 

	The `--from-history` flag makes sure that only those enviroenments are listed in the .yml that have been installed manually. Without this flag all dependencies are listed which in practice tends to cause trouble when trying to rebuild the environment.

#### Migrate environments from local to cluster / between machines with different hardware
	
When migrating environemnts between machines (i.e. from local to cluster) make sure to remove hardware dependent packages such as torch from the .yml and manually install them before updating from the .yml:

1.	Write local environment to .yml

	`conda env export --from-history > <filename.yml>`

2.	Remove hardware dependent packagas such as torch from .yml
3.	Create environment on remote

	`mamba create -n $envname -python=3.xxxx`


4. Install hardware dependent packages such as torch from .yml (Pay attention to correct cuda version!)

	`mamba activate $envname`

	i.e.: `mamba install pytorch torchvision torchaudio pytorch-cuda=xx.x -c pytorch -c nvidia`

5.	Update environment from .yml

	`mamba env update -n $envname --file <filename.yml>`
