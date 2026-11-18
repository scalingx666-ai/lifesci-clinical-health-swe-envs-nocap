# Issue

**Title:** fix(stock): reset the stock UOM factor before the stock UOM rate is set (backport #67458)

## Description

**Problem:** `StockController.validate` sets the stock UOM rate with the factor the client sent and only then resets the factor of a stock UOM row to 1. A Delivery Note row of 1 Nos (the stock UOM) at factor 5 and rate 100 saves factor 1 but Rate of Stock UOM 20.

**Fix:** reset the factor before the stock UOM rate is set.

A row in another UOM keeps the factor the client sends (1 Box at factor 1 saves Stock Qty 1). The factor is editable on some forms (Purchase Receipt, Sales Invoice) and mapped rows carry their source's factor, so I left that unchanged; checking it against the item's UOM table would block a deliberately changed factor.

### Steps to reproduce
1. Through the API, insert a Delivery Note (or Purchase Receipt) row of qty 1, UOM = the item's stock UOM, conversion factor 5, rate 100.

Before: conversion factor 1, Rate of Stock UOM 20. After: conversion factor 1, Rate of Stock UOM 100.

<hr>This is an automatic backport of pull request #67458 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0583a07af9ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.