# Singularity

This serves as an example of creating a Singularity container from an environment.yaml file. In this instance, the latex-full package is installed within the container. You can replace or add additional packages as necessary. This method allows you to utilize software on the cluster that typically requires root permissions for installation.


Create the singularity container:

    sudo singularity build container_name.sif Singularity


It might be necessary to explicitly set a cache and tmp dir in case you run out of space:

    sudo SINGULARITY_CACHEDIR=/path/to/some/directory/with/enough/space SINGULARITY_TMPDIR=/path/to/some/directory/with/enough/space singularity build container_name.sif Singularity
