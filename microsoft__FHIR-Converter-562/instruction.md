# Issue

**Title:** Treat datetime values as Strings during json deserialization in Json…

## Description

[JsonDataParser](https://github.com/microsoft/FHIR-Converter/blob/main/src/Microsoft.Health.Fhir.Liquid.Converter/Parsers/JsonDataParser.cs#L25) currently uses the default Newtonsoft datetime [deserialization](https://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_DateParseHandling.htm) behavior, which is to turn datetime strings into .Net DateTime objects. This causes reformatting of the supplied value as well as loss of timezone details. This updated value is what is supplied to Liquid. The converted value may not be desired by end users and could cause further issues downstream. 

This PR makes several changes:

- Updates the JsonDataParser to treat DateTime strings as .Net strings by default
- Allows end users to JsonDataParser classes which can change the serialization behavior
- Updates JsonParser to allow different implementations of IDataParser to be supplied during construction
- Updated test data to include datetime value, and ensure that they are converted correctly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `575fd14eb890`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.