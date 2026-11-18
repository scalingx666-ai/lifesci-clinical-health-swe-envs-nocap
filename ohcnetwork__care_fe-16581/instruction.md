# Issue

**Title:** Fix "Show on Map" link oversized clickable area

## Description

## Summary
Fixes an issue where the "Show on Map" link in facility cards had a clickable area larger than its visible text/icon, causing accidental navigation when clicking nearby empty space.



## Problem
The link used `flex`, which stretched it to fill the full width of its parent container — making the empty space beside the text clickable too.

## Solution
Added `w-fit` to constrain the link to its actual content width, while keeping `flex` so the layout (position below the address, icon alignment) stays unchanged.

**Before:**

https://github.com/user-attachments/assets/0fd91e1a-5e46-46ac-9344-b626ff1a2f3e



**After:**


https://github.com/user-attachments/assets/fbe291fc-f618-4a67-8623-86523375f2fa


## Testing
- Clicked directly on "Show on Map" text/icon — opens map as expected.
- Clicked empty space beside it — no longer triggers navigation.
- Verified layout unchanged (link still sits below the address, matching existing card design).

## Merge Checklist
- [x] Tested locally in browser
- [ ] Added/updated tests for changed code
- [ ] Added/updated documentation
- [ ] All CI checks pass

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Style**
  * Updated the facility map link styling to better fit its content by adjusting its rendered width behavior.
  * Preserved existing link behavior, layout, and hover styling.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `addeaa55b3eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.