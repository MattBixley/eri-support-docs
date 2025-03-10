---
created_at: '2019-09-15T23:36:59Z'
description: eRI's scratch automatic deletion of old data.
tags:
- nobackup
- cleaning
vote_count: 4
vote_sum: 2
zendesk_article_id: 360001162856
zendesk_section_id: 360000033936
---

The automatic cleaning feature is a programme of regular deletion of
selected files from directories in on the **scratch** file system.
We do this to optimise the availability of this file system for active
research computing workloads and to ensure eRI can reliably support
large-scale compute and analytics workflows.

Files are deleted if they meet **all** of the following criteria:

- The file was first created more than 120 days ago, and has not been
    accessed, and neither its data nor its metadata has been modified,
    for at least 120 days.
- The file was identified as a candidate for deletion two weeks
    previously, and as such is listed in a the project's
    scratch `scratch_<project_id>_autocleaner` directory.

The general process will follow a schedule as follows:

- **Notify** (at 106 days), then two weeks later **Delete** (at 120
    days).

- Every fortnight on Tuesday morning, we will be reviewing files
    stored in the nobackup filesystem and identifying candidates for
    expiry.

- Teams will be notified by email if they have file candidates
    for deletion. Emails will be sent two weeks in advance of any
    deletion taking place.

!!! warning
     Due to the nature of email, we cannot guarantee that any
     particular email message will be successfully delivered and
     received, for instance our emails could be blocked by your mail
     server or your inbox could be too full. We suggest that you check
     `/scratch/<project_id>/scratch_<project_id>_autocleaner/` (see below) for a list of
     deletion candidates, for each of your projects, whether you
     received an email from us or not.

- Immediately after deletion is complete, a new set of candidate files
  will be identified for expiry during the next automated cleanup.
  These candidate files are all files within the project's nobackup
  that have not been created, accessed or modified within the last 106
  days.

A file containing the list of candidates for deletion during the next
cleanup, along with the date of the next cleanup, will be created in a
directory called `scratch_<project_id>_autocleaner` inside the project's scratch
directory. For example, the candidates for future deletion  from the
directory `/scratch/2024_agr12345` are recorded in
`/scratch/2024_agr12345/scratch_2024_agr12345_autocleaner/flagged_files_log_<date>`. Project team members are able to view the contents of `scratch_2024_agr12345_autocleaner` (but not delete or modify those contents).

!!! warning
     Objects other than files, such as directories and symbolic links, are
     not deleted under this policy, even if at deletion time they are
     empty, broken, or otherwise redundant. These entities typically take
     up no disk space apart from a small amount of metadata, but still
     count towards the project's inode (file count) quota.

## What should I do with expiring data on the scratch filesystem?

If the data is transient and no longer required for continued processing
on eRI, we would appreciate if you deleted it yourself, but you can
also let the automated process do this.

If you have files identified as candidates for deletion that you need to
keep beyond the scheduled expiry date, you have four options:

- Move the file to your persistent project directory,
    e.g., `/project/2024_agr12345`. You may need to request more disk
    space, more inodes, or both, in your persistent project directory
    before you can do this. {% include "partials/support_request.html" %}. We
    assess such requests on a case-by-case basis.  Note:  You can save
    space by compressing data.  Standard tools such as `gzip`
    `bzip2` etc are available.

- **Modify** the file before the deletion date, in which case the file
    will not be deleted even though it is listed in `.policy`. This must
    only be done in cases where you expect to begin active use of the
    data again within the next month.

- Note: Accessing (Open/Close and Open/Save) or Moving (`mv`) does
    not update the timestamp of the file. Copying (`cp`) does create a
    new timestamped file.

## Where should I put my data?

| How often will my team's HPC jobs be accessing the data? | How often will my team's HPC jobs be modifying the data? | Recommended option                                                                                         |
| -------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Often                                                    | Often (at least once every two months)                   | Leave in the scratch directory (but ensure key result data is copied to the persistent project directory) |
| Often                                                    | Seldom                                                   | Put in the persistent project directory                                                                    |
| Seldom                                                   | Seldom                                                   | Store the data elsewhere (e.g. at your institution)                                                        |

In general, the persistent project directory should be used for
reference data, tools, and job submission and management scripts. The
nobackup directory should be used for holding large reference working
datasets (e.g., an extraction of compressed input data) and as a
destination for writing and modifying temporary data. It can also be
used to build and edit code, provided that the code is under version
control and changes are regularly checked into upstream revision control
systems.

## If I need a file that was deleted from scratch, what should I do?

Depending on when the file was deleted, it may be possible to recover the file. A record when files were deleted by the autocleaner can be found in `/scratch/<project_id>/scratch_<project_id>_autocleaner/`. This directory contains a number of files:

  - `deleted_files_log.latest` - lists all of the files that were most recently deleted
  - `deleted_files_summary.latest` - summary of all of the files that were most recently deleted
  - `flagged_files_log.latest` - files marked for deletion in the next cycle
  - `deleted_files_summary_<date>` - summary of deleted files on the specified date
  - `deleted_files_log_<date>` - files that were deleted on the specified date
  - `flagged_files_log_<date>` - files that were marked for deletion on the specified date



Please {% include "partials/support_request.html" %} as soon as
possible after you find that the file is missing.
To reduce the risk of this outcome again in future,
please {% include "partials/support_request.html" %} so that we
can discuss your data storage options with you.

## I have research data on scratch that I can't store in my project directory or at my institution right now. What should I do?

Projects are intended for active/ongoing work whereas Datasets are to enable collaboration on, sharing of, and reference to research data. A single research activity/project might require both a Project and one or more Datasets on the eResearch Infrastructure. At the end of a research activity, a final step might involve turning the Project into a Dataset for archive.

A Dataset will include a dataset directory only, no scratch storage, no computing/analysis resources. Datasets have an owner/custodian and a team of contributors, where each member of the team will have full access to the contents of the dataset’s storage. Datasets also have read-only access, either to a defined group of individuals or for all AgResearch users.

Please {% include "partials/support_request.html" %} if you need a Dataset to store your research data. 

