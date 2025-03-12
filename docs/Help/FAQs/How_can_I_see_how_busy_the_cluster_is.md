---
created_at: '2019-09-22T20:20:07Z'
tags: []
title: How can I see how busy the cluster is?
vote_count: 0
vote_sum: 0
zendesk_article_id: 360001176756
zendesk_section_id: 360000039036
---

You can get the current status of all nodes on a cluster using the
command `sinfo`, you will get a printout like the following.

```sh
$ sinfo
PARTITION AVAIL JOB_SIZE  TIMELIMIT   CPUS  S:C:T   NODES STATE      NODELIST
compute*  up    1-infini 14-00:00:0    256 2:64:2       1 down*      compute-5
compute*  up    1-infini 14-00:00:0    256 2:64:2       4 mixed      compute-[0-2,4]
compute*  up    1-infini 14-00:00:0    256 2:64:2       1 idle       compute-3
gpu       up    1-infini 14-00:00:0     96 2:24:2       1 idle       gpu-0
hugemem   up    1-infini 14-00:00:0    256 2:64:2       1 mixed      hugemem-1
hugemem   up    1-infini 14-00:00:0    256 2:64:2       1 idle       hugemem-0
interacti up    1-infini 60-00:00:0      8  8:1:1       3 idle       interactive-[0-2]
vgpu      up    1-infini 60-00:00:0     32 32:1:1       2 drained    vgpu-[0-1]
vgpu      up    1-infini 60-00:00:0     32 32:1:1       1 allocated  vgpu-2
vgpu      up    1-infini 60-00:00:0     32 32:1:1       1 idle       vgpu-3
```

Each partition has a row for every state it's nodes are currently in.

For example, the `compute` partition currently has  **1** `down` node, 
**4** `mixed` nodes,  **no** `allocated` nodes and  **0** `idle`
nodes.

The most common node states you are likely to see are:

|  State      | Description                                                                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `idle`      | All CPUs on this node are unallocated and available for use.                                                                                              |
| `allocated` | All CPUs on this node are currently allocated.                                                                                                            |
| `mixed`     | Some CPUs on this node are unallocated, smaller jobs are likely to land here.                                                                             |
| `down`      | The node is unavailable for use                                                                                                                           |
| `reserved`  | This node has been reserved, and is only available for some users (in the case of the igpu partition, please contact NeSI support if you wish to use it). |
| `draining`  | Jobs are currently running on this node, but is not available for new jobs.                                                                               |

A full list of node states can be found
[here](https://slurm.schedmd.com/sinfo.html#lbAG).

If you are interested in the state of one partition in particular you
may want to use the command `squeue -p <partition>` to get the current
queue of the partition `<partition> `.
