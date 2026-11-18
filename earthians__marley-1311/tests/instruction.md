# Issue

**Title:** fix(patient-appointment): keep Patient Appointment print action working on Frappe develop and version-16 (backport #1184)

## Description

In the Patient Appointment payment dialog, the secondary print action was defined using inline SVG as secondary_action_label.
That worked on Frappe version-16, because Dialog.set_secondary_action_label() renders the label with .html(...).

It breaks on current Frappe develop after the dialog footer button refactor in commit 7aa1006736 from July 31, 2026:
feat(ui): migrate modal footer buttons to espresso (#41444)

After that change, dialog button labels are treated as text via the new button dressing flow, so the raw SVG label is shown as literal markup instead of rendering as an icon.

Changes Applied:-

1. In patient_appointment.js :-

    - added a small capability check:const supports_icon_button = Boolean(frappe.ui?.button?.dress);
    - changed secondary_action_label to:
                 - use __("Print") when the newer button API exists
                - fall back to the original inline SVG when it does not
    - after dialog creation, added:
           - frappe.ui.button.dress(d.get_secondary_btn(), { icon: "printer", title: __("Print") })
          - only when supports_icon_button is available

Flow On Frappe Develop:-
- supports_icon_button is true
- dialog label is set to plain Print
- after dialog creation, the secondary button is dressed into an icon-only printer button
- result:no raw SVG text appears
- print button matches the expected modern UI

Flow On Frappe Version-16

- supports_icon_button is false
- dialog keeps using the original inline SVG label
- frappe.ui.button.dress(...) is not called
- result:old behavior is preserved
- no regression for instances still on Frappe version-16

Before:-
<img width="656" height="453" alt="image" src="https://github.com/user-attachments/assets/9316f451-8009-4186-8087-a64c11a4ae6d" />


After:-
<img width="621" height="409" alt="image" src="https://github.com/user-attachments/assets/3eb52213-2882-4bca-9dbd-d403fc5d32d0" />


After clicking create invoice, print icon enabled:-
<img width="652" height="480" alt="image" src="https://github.com/user-attachments/assets/f1dd13f6-4be9-4c3c-850a-386b3ee7d692" />


It then navigates to preview print format display<hr>This is an automatic backport of pull request #1184 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a87e4e55e1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.