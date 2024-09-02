### Where to store data on the cluster?
! This only applies to the old QB file system, not to the new LustR file system ! 
- Slow HDD storage: `/mnt/qb/butz/`
- quick SSD storage `/mnt/qb/work2/butz1/`
- even faster SSD storage (quicker connection to the compute nodes) `/mnt/qb/datasets/STAGING/butz/` Only for small training data that is currently being used (check `qinfo quota`, we have `~ 1TB` there)