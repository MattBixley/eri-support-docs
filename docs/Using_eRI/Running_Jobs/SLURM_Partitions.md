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
sbatch: `hugemem` is not the most appropriate partition for this job, which would otherwise default to `compute`. If you believe this is incorrect then contact support and quote the Job ID number.
```

<table><tbody>
<tr>
<th>Partition</th>
<th>Max Walltime</th>
<th>Nodes</th>
<th>CPUs/Node</th>
<th>Available Mem/CPU</th>
<th>Available Mem/Node</th>
<th>Description</th>
</tr>
<tr>
<td>compute</td>
<td>14 days</td>
<td>6</td>
<td>256</td>
<td>3.7 GB</td>
<td>950 GB</td>
<td>Default partition.</td>
</tr>
<tr>
<td>gpu</td>
<td>14 days</td>
<td>1</td>
<td>96</td>
<td>4.8 GB</td>
<td>470 GB</td>
<td>A100.</td>
</tr>
<tr>
<td>hugemem</td>
<td>14 days</td>
<td>2</td>
<td>256</td>
<td>14.9 GB</td>
<td>3800 GB</td>
<td>Very large amounts of memory.</td>
</tr>
<tr>
<td>interactive</td>
<td>60 days</td>
<td>3<br/></td>
<td>8</td>
<td>1.8 GB</td>
<td>14.5 GB</td>
<td>Partition for interactive jobs.</td>
</tr>
<tr>
<td>vgpu</td>
<td>60 days</td>
<td>4</td>
<td>32</td>
<td>13 GB</td>
<td>418 GB</td>
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

Specifying `--qos=interactive` will give a very high priority [interactive job](SLURM_Partitions.md).

## Requesting GPUs

|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **GPU code**           | **GPU type**                                                                                                                                   |
| A100 (`gpu` partition) | NVIDIA Tesla A100 PCIe 40GB cards                                                                                                              |
| vgpu | NVIDIA A10 GPGPU, PCIe 24GB cards                                              |

The default GPU type is A100. The vgpu partition contains four virtualised compute nodes, each with a single NVIDIA A10 GPGPU, PCIe 24GB cards.

To request for the A100 GPU:

``` sl
#SBATCH --partition     gpu
#SBATCH --gpus-per-node 1   # GPU resources required per node
```

To request for vGPUs, use instead:

``` sl
#SBATCH --partition     vgpu
#SBATCH --gpus-per-node 1
```
