# Issue

**Title:** [ENH] Cross platform deployment scripts, accepting linkage option, callable from anywhere and segregating deploy and packing.

## Description

During everyday tasks, I find myself using more and more this script. 
Want to make them to be able to be used from anywhere. 
Also, usually, I don't want to have the zip folder created so I've offloaded that specific task to another script. 

@LorenzE @gabrielbmotta , could you take a look, even a more thorough than usual, to [this part](https://github.com/juangpc/mne-cpp/blob/b5eaabf8b1071ed53b7bb5abda0326ce0d4a09f4/.github/workflows/release.yml#L219)?
```
    - name: Deploy binaries
      run: |
        ./tools/deployment/deploy_win_static.bat
    - name: Generate zip file from bin folder contents
      run: |
        ./tools/deployment/save_bin_folder_content_as_zip_file.bat   
```

and [this](https://github.com/juangpc/mne-cpp/blob/b5eaabf8b1071ed53b7bb5abda0326ce0d4a09f4/.github/workflows/release.yml#L416): 
```
    - name: Deploy binaries (Windows)
      run: |
        ./tools/deployment/deploy_win.bat
    - name: Generate zip file from bin folder contents
      run: |
        ./tools/deployment/save_bin_folder_content_as_zip_file.bat
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f86fda1e2b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.