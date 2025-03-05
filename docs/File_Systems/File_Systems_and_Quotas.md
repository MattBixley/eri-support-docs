---
created_at: '2025-04-03T04:06:16Z'
tags:
- info
- storage
- quota
- filesystem
title: eRI File Systems and Quotas
---

### File System Mount Points

The file system mount points are:

-  `/mnt/gpfs/persist/` for both `datasets` and `projects`
-  `/mnt/gpfs/scratch/` for projects temporary compute working space (`scratch`).

For Windows workstations these are mounted as:

-  M: -> `/agr/persist/projects`
-  S: -> `/agr/persist/datasets`

### File System Specifications


To query your actual usage and disk allocations using the following
command:

```sh
$ nn_storage_quota
Fileset quota report for filesets available to user test.user

Fileset                                 Available    Used     Use%   INodes
test.user                   home              20G     26G    0.00%   173055
2024_test_project           dataset            1P  283.9G    0.03%    37549
2024_test_project           project            1T  76.15G    7.44%   193201
2024_test_project           scratch          300T  522.6M    0.00%    42057
```

The values for `nn_storage_quota` are updated approximately every hour
and cached between updates.

## File System Specifications

| Filesystem     | `/home`                                                                                | `/projects`                                                                                                  | `/datasets` | `/scratch` |
| -------------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Default Disk Quota     | 20 GB                                                                                 | 1 TB                                                                                                     | 1 TB| 300 TB<br>Shared across all projects TB                                                                                                       |
| Usage  | User-specific files such as configuration files, environment setup, source code, etc. | Persistent project-related data, software, etc. | Medium- to long-term storage of research data, (past, present or planned projects) | Data created or used by compute jobs that is intended to be temporary |
| Capacity | 1.2PB (shared home, projects, datasets)||  | 300 TB |
| Data retention |                   |  |  | Untouched for 120 days. See Automatic cleaning of nobackup file system for more information |
| Data backup schedule      | DMF<sup>1</sup>                                                               | DMF<sup>1</sup>                                                                                        | DMF<sup>1</sup> | Weekly |
| Speed          | Moderate | Moderate | Moderate | Fast |
| Interfaces     | <ul><li>Native Mounts</li><li>SCP</li><ul> | <ul><li>Native mounts</li><li>SCP</li><li>Globus</li></ul> | <ul><li>Native Mounts</li><li>SCP</li><li>Globus</li> | <ul><li>Native Mounts</li><li>SCP</li><ul> |

<sup>1</sup>The storage system is connected to a Data Management Framework (DMF) with offers a disk based capacity of 3PB plus tape based capacity.

#### **Notes:**

- You may request an increase in storage if needed by
    a project. This may in turn be reduced as part of managing overall
    risk, where large amounts of quota aren't used for a long period (~6
    Months).
- If you need to compile or install a software package that is large
    or is intended for use by a project team, please build it
    in `/project/<project_code>` rather than `/home/<username>`.
- As the `/scratch` file system provides the highest
    performance, input files should be moved or copied to this file
    system before starting any job that makes use of them. Likewise, job
    scripts should be written so as to write output files to the
    `/scratch` file system. If you wish to keep your data for the
    long term, you can include as a final part of your job script an
    operation to copy or move the output data to the `/project`
    file system.

### /home

	@@ -103,7 +84,7 @@
your My NeSI account is active and you are a member of at least one
active project.

### /project

This filesystem is accessible from all login, compute and ancillary
nodes. Contents are backed up daily, via the Spectrum Protect backup
	@@ -120,12 +101,12 @@
Each NeSI project receives quota allocations for
`/nesi/project/<project_code>`, based on the requirements you tell us
about in your [application for a new NeSI
project](https://my.nesi.org.nz/html/request_project), and separately covering disk space and number of files.

### /scratch

The `/scratch` file system has the highest performance of all NeSI
file systems, with greater than 140 GB/s bandwidth from compute nodes to
disk. It provides access to a large (4.4 PB) resource for
short-term project usage.
	@@ -137,7 +118,7 @@
above table; if you require more temporary (scratch) space for your
project than the default quota allows for, you can discuss your
requirements with us during [the project application process](../../General/NeSI_Policies/How_we_review_applications.md),
or {% include "partials/support_request.html" %} at any time.

To ensure this file system remains fit-for-purpose, we have a regular
cleaning policy as described in
	@@ -150,85 +131,10 @@
The purpose of this policy is to ensure that any user will be able to
analyse datasets up to 1 PB in size.

## Snapshots

If you have accidentally deleted data you can recover it from
a [snapshot](../Data_Recovery/File_Recovery.md).
Snapshots are taken daily of `home/` and `project` directories If you
cannot find it in a snapshot, please ask us to recover it for you by
{% include "partials/support_request.html" %}

