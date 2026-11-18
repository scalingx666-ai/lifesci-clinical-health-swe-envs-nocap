# Issue

**Title:** Fix: Diagnostic Report note icon rendering across Frappe develop and version-16

## Description

Issue Description:-
On Diagnostic Report, the note button for each observation was not visible on instances running Frappe develop, even though it appeared correctly on instances running Frappe version-16.

Root cause:
- Healthcare observation widget was using the SVG icon #icon-small-message
- That icon exists in Frappe version-16
- It does not exist in current Frappe develop, which uses a different icon set
- As a result, the note button rendered with a missing SVG reference on develop, so the icon appeared blank or invisible
   This is why the same Healthcare code behaved differently across the two instances.

Fix Applied:-
1.Updated observation_widget.js to use a one-line runtime fall back.
                    const note_icon_href = document.getElementById("icon-small-message") ? "#icon-small-message" : "#icon-message-square";

2.Then note button SVG uses:
                     <use xlink:href="${note_icon_href}"></use>

Before:
          - code always expected #icon-small-message
          - worked on version-16
          - failed on develop

After:
                  - if old icon exists, use it
                  - otherwise use #icon-message-square

Post-Fix Flow:-
1. For Frappe version-16:
- page loads Diagnostic Report
- observation widget checks document.getElementById("icon-small-message")
- icon exists
- note button uses #icon-small-message
- icon displays normally

2. For Frappe develop:
- page loads Diagnostic Report
- observation widget checks document.getElementById("icon-small-message")
- icon does not exist
- fallback uses #icon-message-square
- note button displays with the Lucide-based icon


Before:-
<img width="1008" height="430" alt="image" src="https://github.com/user-attachments/assets/0095056c-9ce6-4949-9319-b29e2b58e84d" />


After:
<img width="938" height="409" alt="image" src="https://github.com/user-attachments/assets/2678ceeb-6509-47ad-895c-91748a22519c" />

<img width="750" height="648" alt="image" src="https://github.com/user-attachments/assets/358680a6-5ba1-4101-af22-cd8ba248434a" />


Notes:-
Frappe (develop branch) 
Commit: 9a5aea3197a500b3329c3bde5bf26c1eade00300
Date: July 3, 2026
Message: fix(ui): make icons consistent (#40571)
- deleted frappe/public/icons/timeless/icons.svg
- that old sprite contained icon-small-message
- current develop now uses the Lucide sprite instead

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1e4abd20d7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.