# OSINT_CyberChef_Recipes
A collection of cyberchef recipes for use in OSINT investigations.


## Introduction:
This repo was inspired by [MattnotMax's cyberchef recipe collection](https://github.com/mattnotmax/cyberchef-recipes) and created to serve as a collaborative effort to collect and develop cyberchef recipies that would be especially useful during OSINT investigations. Some of the recipies will be original content, and others will be ones I find online (I will be sure to indicate which are which)

## Importing / Exporting Recipies Into CyberChef
_Coming Soon_



## Recipies

**Index**
Number | Recipe | Author |
| --- | --- | --- |
| 00 | [Defang All](#00---defang-all) | IntelCorgi
| 01 | [Refang All](#01---refang-all) | IntelCorgi
| 02 | [SHA256 hash list to VTI livehunt](#02---SHA256-hash-list-to-VTI-livehunt) | IntelCorgi
----------------------

### 00 - Defang All
**Author:** IntelCorgi

**Purpose:** Any data input into CyberChef will be defanged.

Defanging is commonly used when sharing threat information, such as a malicious URL. By defanging the observable, sharing malicous URLs in reports or slack won't accidentally reach out to the URL during the creation of a hyperline.

**Recipe:**
```
Defang_URL(true,true,true,'Valid domains and full URLs')
Defang_IP_Addresses()
```
### 01 - Refang All
**Author:** IntelCorgi

**Purpose:** Sometimes refanging is necessary to put IOCs back into a threat intelligence platform like MISP.

**Recipe**
```
Find_/_Replace({'option':'Simple string','string':'[.]'},'.',true,false,true,false)
Find_/_Replace({'option':'Simple string','string':'hxxp'},'http',true,false,true,false)
Find_/_Replace({'option':'Simple string','string':'[@]'},'@',true,false,true,false)
Find_/_Replace({'option':'Simple string','string':'[://]'},'://',true,false,true,false)
```
### 02 - SHA256 hash list to VTI livehunt
**Author:** IntelCorgi

**Purpose:** Useful when you're developing a Livehunt rule to alert when files with a certain hash are uploaded to VirusTotal. Since Livehunt uses YARA for detection, working with a huge list of hashes can get a little out of hand. Copy and paste the result of this receipie in the conditions section of the rule. You will have to edit the beginning and ending of the list. If you are using a different type of hash, just replace the "sha256" part.

**Recipe**
```
Find_/_Replace({'option':'Extended (\\n, \\t, \\x...)','string':'\\n'},'" \\n vt.metadata.sha256 == "',true,false,true,false)
```