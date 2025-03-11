---
created_at: '2024-11-18T21:21:50Z'
tags: [gquery]
title: How to run gquery
---

# How to run gquery

The gquery client suite is now supported on eRI.

## Summary

```
login-0$ kinit
login-0$ module load gquery
login-0$ gquery -t sources
login-0$ gquery -t accessions D70077
```

To use gquery from a Slurm job it is necessary to have acquired the Kerberos ticket and module loaded gquery on the login node first.

### Kerberos ticket expiry

The Kerberos tickets which is needed for database access are issued by AgResearch Active Directory, and have an expiry time of 10 hours. 

The current tickets can be seen with `klist`


```
it23677> kinit
it23677> klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: guestsi@AGRESEARCH.CO.NZ

Valid starting       Expires              Service principal
08/14/2024 17:18:35  08/15/2024 03:18:35  krbtgt/AGRESEARCH.CO.NZ@AGRESEARCH.CO.NZ
        renew until 08/21/2024 17:18:30        
```

Note the 10 hour expiry time visible here.

When using the `krb5cc.home` module version `0.2.0` or later (which is a default dependency of gquery as of 4/9/2024), tickets are automatically renewed every 4 hours up to 7 days.  Note that each renewal will only last 10 hours.  Note that the current modules may be seen with `module list`.

Beyond 7 days, the user needs to `kinit` a new ticket, which may be picked up by the existing ticket renewal process, or a new `module load gquery` may be required.

### Explanation

Historically on legacy HPC, database credentials were stored in the filesystem, and users were probably oblivious to the fact that they were being fetched on their behalf to authenticate with the database.

On eRI authentication is fine-grained per-user, making use of Kerberos tickets. Therefore a Kerberos ticket is required before attempting to run `gquery`.

The current Kerberos tickets may be viewed using `klist`.  To obtain a ticket in the first instance, it is necessary to pass it through with `ssh -o GSSAPIDelegateCredentials=yes` (which may only work on WSL, not native Windows ssh nor putty nor MobaXTerm) or request after login with `kinit`.

Tickets are made available to compute nodes via a Kerberos credentials cache in the user’s home directory, which is set up during `module load gquery`.  The updated cache location is visible in `klist`.

### Interactive Example

On Login Node

```
login-0$ kinit
login-0$ module load gquery
login-0$ srun --nodelist=compute --pty bash
```

On Compute Node, you do not need to run `module load gquery` again.


```
compute-0 ~ $ gquery -t sources
....
physicalsourceuri       datasourcetype  createddate     lastupdateddate
/bifo/active/gseq_processing/bin/gquery_dev/gquery/unit_tests/mf_test1a.csv     GBS CSV Masterfile      2024-02-01      None
/dataset/deer_GBS/active/2024_Chinook_salmon_production_temp/SanfordAll20180418.csv     GBS CSV Masterfile      2024-10-24      2024-11-07
.....
```
