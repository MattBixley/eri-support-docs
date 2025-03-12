---
created_at: '2022-06-15T00:53:58Z'
tags: []
title: Where should I store my data on NeSI systems?
vote_count: 0
vote_sum: 0
zendesk_article_id: 4975669783951
zendesk_section_id: 360000039036
---

| Frequency of data being read | Frequency of data being written        | Recommended option                                                                                                            |
| ---------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Often                        | Often (at least once every two months) | Store in your `/scratch/<projectcode>` directory (but ensure key result data is copied to the persistent project directory). |
| Often                        | Seldom                                 | Store in your `/project/<projectcode>` directory.                                                                             |
| N/A                       | Seldom                                 | If this is a dataset, apply for a Dataset allocation.                |

In general, the **project directory** should be used for reference data,
tools, and job submission and management scripts. The **scratch
directory** should be used for holding large reference working datasets
(e.g., an extraction of compressed input data) and as a destination for
writing and modifying temporary data. The scratch directory can also be
used to build and edit code, provided that the code is under version
control and changes are regularly checked into upstream revision control
systems.

**Datasets** are to enable collaboration on, sharing of, and reference to research data. A single research activity/project might require both a Project and one or more Datasets on the eResearch Infrastructure. At the end of a research activity, a final step might involve turning the Project into a Dataset for archive (after some tidy up and additional description work).
