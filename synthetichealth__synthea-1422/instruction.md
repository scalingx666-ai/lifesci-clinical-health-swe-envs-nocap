# Issue

**Title:** Better handling of lists in Flexporter

## Description

This PR adds better handling of lists in the flexporter. Currently as seen in #1421, adding multiple items to a list requires awkward "where" syntax which won't be apparent to users. This PR enables a couple options that should be more intuitive.

These 3 actions should now produce equivalent results (though the ordering of the items in the first instance is not guaranteed)

```yaml
 - name: testSetValues_where
   set_values:
     - applicability: Encounter 
       fields: 
         - location: Encounter.serviceType.coding.where(code='229')
           value: 
             system: http://terminology.hl7.org/CodeSystem/service-type
         - location: Encounter.serviceType.coding.where(code='355')
           value: 
             system: http://terminology.hl7.org/CodeSystem/service-type


 - name: testSetValues_indexed
   set_values:
     - applicability: Encounter 
       fields: 
         - location: Encounter.serviceType.coding[0]
           value: 
             system: http://terminology.hl7.org/CodeSystem/service-type
             code: "229"
         - location: Encounter.serviceType.coding[1]
           value: 
             system: http://terminology.hl7.org/CodeSystem/service-type
             code: "355"


 - name: testSetValues_list
   set_values:
     - applicability: Encounter 
       fields: 
         - location: Encounter.serviceType.coding
           value:
             - system: http://terminology.hl7.org/CodeSystem/service-type
               code: "229"
             - system: http://terminology.hl7.org/CodeSystem/service-type
               code: "355"
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6fa1b4b11084`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.