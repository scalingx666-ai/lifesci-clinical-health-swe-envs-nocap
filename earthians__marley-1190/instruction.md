# Issue

**Title:** fix(a11y): add alt text to patient/practitioner photo images

## Description

## Problem

Five patient/practitioner photos in the patient portal had no `alt` attribute.

## Fix

All five are avatar-next-to-name pairs — the appointment, booking, department, diagnostic, and practitioner-selector cards each already show the person's or department's name as visible text right beside the photo — so `alt=""`, matching the standard avatar-with-adjacent-name convention.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43216a673488`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.