# Issue

**Title:** J#59625 Made the <Bundle> opening tag and parameters one line so that the renderer for the html pages would display them correctly

## Description

The HL7/kindling ResourceParser.java function is causing an issue with the html rendering of the <Bundle tag if the example is multiline, it adds ">" at the end of the line and the rest of the <Bundle parameters are not in proper format

For example, https://build.fhir.org/composition-operation-document.html is rendering it as:
```
<Bundle>
 xsi:schemaLocation="http://hl7.org/fhir ../../schema/bundle.xsd"
 xmlns="http://hl7.org/fhir">
```

Even though the example in the .xml file has:
```
<Bundle xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://hl7.org/fhir ../../schema/bundle.xsd"
 xmlns="http://hl7.org/fhir">

```

**Notice how the renderer added a ">" at the end of the opening Bundle tag before the rest of the Bundle tag parameters.**

How it was intended to be rendered based on the Java function logic:
```
<Bundle>
```

So there are two ways to fix this, either fix the HL7/kindling function, or what **I committed here** was have the opening <Bundle tag and all the parameters be one line. So I fixed it for the Composition example to render correctly on the page and have the HL7/kindling Java function act as intended. I also updated the two other examples so that the opening <Bundle> tag and all their parameters are one line. (besides all the invariant-tests ones, I don't think those are needed to be updated?)

The **HL7/kindling ResourceParser.java** function that's causing the issue:

```
  private void process(StringBuilder content, int indent, String s) {
    String pfx = Utilities.padLeft("",  ' ', indent);
    String[] lines = s.trim().split("\\r?\\n");
    for (String l : lines)
      if (l.contains("xmlns:xsi=")) {
        content.append(pfx+Utilities.escapeXml(l.substring(0, l.indexOf("xmlns:xsi=")-1)));
        content.append(">\r\n");
      } else {
        content.append(pfx+Utilities.escapeXml(l));
        content.append("\r\n");
      }
  }
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa1aba83ed39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.