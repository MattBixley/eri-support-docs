---
created_at: '2018-05-17T23:35:36Z'
tags: []
title: Job prioritisation
vote_count: 1
vote_sum: 1
zendesk_article_id: 360000201636
zendesk_section_id: 360000030876
---

Each queued job has a priority score.  Jobs start when sufficient
resources (CPUs, GPUs, memory, licenses) are available and not already
reserved for jobs with a higher priority.

To see the priorities of your currently pending jobs you can use the
command `sprio -u $USER`.

## Factors

Priority scores are determined by a number of factors:

### Fair Share

How does it work on eRI

### Job Age

Job priority slowly rises with time as a pending job gets older -1
point per hour for up to 3 weeks.

### Job Size or "TRES" (Trackable RESources)

This slightly favours jobs which request a larger count of CPUs (or
memory or GPUs) as a means of countering their otherwise inherently
longer wait times.

### Nice values

It is possible to give a job a "nice" value which is subtracted from its
priority. You can do that with the `--nice` option of `sbatch` or the
`scontrol update` command.  The command `scontrol top <jobid>` adjusts
nice values to increase the priority of one of your jobs at the expense
of any others you have in the same partition.

### Holds

Jobs with a priority of 0 are in a "held" state and will never start
without further intervention.  You can hold jobs with the command
`scontrol hold <jobid>` and release them with
`scontrol release <jobid>`.  Jobs can also end up in this state when
they get requeued after a node failure.

## Backfill

Backfill is a scheduling strategy that allows small, short jobs to run
immediately if by doing so they will not delay the expected start time
of any higher-priority jobs. Since the expected start time of pending
jobs depends upon the expected completion time of running jobs it is
important that you set reasonably accurate job time limits if backfill
is to work well.

While the kinds of jobs that can be backfilled will also get a low job
size score, it is our general experience that an ability to be
backfilled is on the whole more useful when it comes to getting work
done on the HPCs.

More information about backfill can be found [here](https://slurm.schedmd.com/sched_config.html).
