# Issue

**Title:** Custom Exporters

## Description

This is a proof of concept for supporting drop-in custom exporters.

This approach takes advantage of the [Java ServiceLoader](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) to load in JARs containing classes that implement a certain interface. I've defined two interfaces here, PatientExporter and PostCompletionExporter. (The existing exporters weren't modified here but they could easily extend these interfaces as well)

A template for building a custom exporter is here: https://github.com/dehall/custom-exporter-template

And an example Postgres loader which loads Patient basic info and Conditions into simple tables: https://github.com/dehall/example-exporter-postgres

(Documentation is limited on those new repos, apologies)

Note this has not yet been tested with the uberJar, but I believe it should be possible to get it working. I suspect instead of `java -jar synthea-with-dependencies.jar` though you will have to run something along the lines of `java -cp synthea-with-dependencies.jar:new-exporter.jar App`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0a3b685695c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.