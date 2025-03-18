---
created_at: '2018-05-21T03:28:20Z'
tags:
- mahuika
- slurm
vote_count: 11
vote_sum: 9
zendesk_article_id: 360000204076
zendesk_section_id: 360000030876
---

## General Limits

- No individual job can request more than 20,000 CPU hours. This has
    the consequence that a job can request more CPUs if it is shorter
    (short-and-wide vs long-and-skinny).
- No user can have more than 1,000 jobs in the queue at a time.

These limits are defaults and can be altered on a per-account basis if
there is a good reason. For example we will increase the limit on queued
jobs for those who need to submit large numbers of jobs, provided that
they undertake to do so with job arrays.

## Partitions

A partition can be specified via the appropriate [sbatch option](../../Getting_Started/Cheat_Sheets/Slurm-Reference_Sheet.md),
e.g.:

``` sl
#SBATCH --partition=compute
```

However on eRI there is generally no need to do so, since the
default behaviour is that your job will be assigned to the most suitable
partition(s) automatically, based on the resources it requests,
including particularly its memory/CPU ratio and time limit.

If you do specify a partition and your job is not a good fit for that
partition then you may receive a warning, please do not ignore this.
E.g.:

```out
sbatch: `hugemem` is not the most appropriate partition for this job, which would otherwise default to `large`. If you believe this is incorrect then contact support and quote the Job ID number.
```

<table><tbody>
<tr>
<th>Name</th>
<th>Max Walltime</th>
<th>Nodes</th>
<th>CPUs/Node</th>
<th>GPUs/Node</th>
<th>Available Mem/CPU</th>
<th>Available Mem/Node</th>
<th>Max CPUs/job</th>
<th>Description</th>
</tr>
<tr>
<td>compute</td>
<td>14 days</td>
<td>6</td>
<td>256</td>
<td>-</td>
<td>? MB</td>
<td>1 T</td>
<td>?</td>
<td>Default partition.</td>
</tr>
<tr>
<td>gpu</td>
<td>14 days</td>
<td>1</td>
<td>96</td>
<td>-</td>
<td>? MB</td>
<td>-</td>
<td>?</td>
<td></td>
</tr>
<tr>
<td>hugemem</td>
<td>14 days</td>
<td>2</td>
<td>256</td>
<td>-</td>
<td>-</td>
<td>4 T</td>
<td>-</td>
<td>Very large amounts of memory.</td>
</tr>
<tr>
<td>interactive</td>
<td>60 days</td>
<td>3<br/></td>
<td>8</td>
<td>-</td>
<td>-</td>

<td>15 G</td>
<td>?</td>
<td></td>
</tr>
<tr>
<td>vgpu</td>
<td>60 days</td>
<td>4</td>
<td>32</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>Virtual GPUs.</td>
</tr>
</tbody>
</table>

## Quality of Service

Orthogonal to the partitions, each job has a "Quality of Service", with
the default QoS for a job being determined by the allocation class of
its project. There are other QoSs which you can select with the
`--qos`option:

### Interactive

Specifying `--qos=interactive` will give the job very high priority, but
is subject to some limits: up to 4 jobs, 16 hours duration, 4 CPUs, 128
GB, and 1 GPU.

## Requesting GPUs

|                        |                                                                                                                                                |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **GPU code**           | **GPU type**                                                                                                                                   |

| A100 (`gpu` partition) | NVIDIA Tesla A100 PCIe 40GB cards                                                                                                              |
| vgpu | NVIDIA A10 GPGPU, PCIe 24GB cards                                              |

The default GPU type is P100, of which you can request 1 or 2 per node. The vgpu partition contains four virtualised compute nodes, each with a single NVIDIA A10 GPGPU, PCIe 24GB cards.

``` sl
#SBATCH --gpus-per-node=1     # or equivalently, P100:1
```

To request A100 GPUs, use instead:

``` sl
#SBATCH --gpus-per-node=A100:1
```

See [GPU use on NeSI](../../Scientific_Computing/Running_Jobs_on_Maui_and_Mahuika/GPU_use_on_NeSI.md)
for more details about Slurm and CUDA settings.

### Limits on GPU Jobs

- There is a per-project limit of 6 GPUs being used at a time.
- There is also a per-project limit of 360 GPU-hours being allocated
    to running jobs. This reduces the number of GPUs available for
    longer jobs, so for example you can use 2 GPUs at a time if your
    jobs run for a week, 5 GPUs for two days, or 6 GPUs for one day
    jobs. The intention is to guarantee that all users can get their GPU
    debugging jobs running in a reasonably timely manner.
- Each GPU job can use no more than 64 CPUs. This is to ensure that
    GPUs are not left idle just because their node has no remaining free
    CPUs.
