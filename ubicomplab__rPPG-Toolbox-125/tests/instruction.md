# Issue

**Title:** Use rindex instead of index for split_idx

## Description

As the title suggests. I think this makes more sense than how it currently is based on [how input files get saved in the first place](https://github.com/ubicomplab/rPPG-Toolbox/blob/main/dataset/data_loader/BaseLoader.py#L326). `rindex` basically finds the last occurrence of a specified value. Since input{chunk_id} is guaranteed to be at the end of the input filename, `rindex` makes more sense to use in case a passed in item_path_filename ever had more than one `_` in it and `index` returned an erroneous `split_idx` because it just happened to find the `_` in something like `subject_c`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e69e149f574`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.