---
created_at: '2018-05-22T01:49:31Z'
tags: []
title: File Recovery
vote_count: 9
vote_sum: 7
---

Data on the filesystem is backed up via the Data Management Framework (DMF) or weekly snapshots. If you need to recover data in `/home`, `projects` or `datasets`, please {% include "partials/support_request.html" %}. Backups for files in `scratch` may be found in one of weekly snapshots.

## Scratch Snapshots
Snapshots are read only copies of the file system. Weekly snapshots of the scratch directory are taken each week on Friday morning. Please note that a maximum of 4 weeks worth of snapshots will be retained at any one time.

The snapshots can be found in the `mnt/gpfs/scratch/.snapshots` directory and are named "scratch@<timestamp>", where the timestamp is the date and time in GMT.

```
login-0:/mnt/gpfs/scratch/.snapshots$ ls
scratch@GMT-2025.01.31-09.00.02  scratch@GMT-2025.02.14-09.00.03
scratch@GMT-2025.02.07-09.00.03  scratch@GMT-2025.02.21-09.00.04
```
The most recent snapshot here is `/mnt/gpfs/scratch/.snapshots/scratch@GMT-2025.02.21-09.00.04/projects`

To recover a file or directory, you can either copy or rsync it back
```
# copy file to project directory
cp /mnt/gpfs/scratch/.snapshots/scratch@GMT-2025.02.21-09.00.04/projects/<project_id>/file.txt /agr/persist/projects/<project_id>/

# rsync directory to project directory
rsync -avi --stats /mnt/gpfs/scratch/.snapshots/scratch@GMT-2025.02.21-09.00.04/projects/<project_id>/my_directory /agr/persist/projects/<project_id>/

```



!!! Tip
     For copying directories use the flag -ir or just -r if you don't want to be prompted before overwriting
