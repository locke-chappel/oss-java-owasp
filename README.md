OSS OWASP Suppression Rules
==
This artifact contains verified false positive definitions for all projects in the com.github.lc.oss package space.

### Special Build Note
To simplify configuration and to ensure downstream projects always use the latest CVE configurations, the build process for this artifact has a special pre-build step - all XML files in src/main/resources are merged into src/main/resources/all.xml. This all.xml files does not exist in the raw source code but is instead compiled at build time as a resource for the maven build process. This pre-compile process helps ensure a single version of the truth for all CVE rules.

**Build Steps**
1. Merge XML files into "all.xml"

``` bash
echo '<?xml version="1.0" encoding="UTF-8"?>' > all.xml
echo '<suppressions xmlns="https://jeremylong.github.io/DependencyCheck/dependency-suppression.1.3.xsd">' >> all.xml
xmllint --xpath '/*[1]/*' src/main/resources/*.xml >> all.xml
echo '</suppressions>' >> all.xml
mv all.xml src/main/resources/all.xml
```
2. Run maven build as usual

_Note: Do **NOT** commit the all.xml file back to version control - this is intended to be a temporary file used only at build time._
