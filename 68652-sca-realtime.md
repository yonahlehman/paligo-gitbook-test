# sca-realtime

The `scan sca-realtime` command is used to **create and run a new sca scan** on the contents of a folder. The SCA realtime scan is a free feature which does not require a Checkmarx account. Anyone can download the CLI tool and run this command without need for authentication. The results are returned in the response body as a JSON object.


{% hint style="warning" %}
Even for users with a Checkmarx account, the realtime scan results are not synced with the user's Checkmarx account.
{% endhint %}


For info about which languages and package managers are supported for the SCA scanner, see [SCA Scanner - Supported Languages and Package Managers](https://docs.checkmarx.com/en/34965-130976-sca-scanner---supported-languages-and-package-managers.html).


{% hint style="warning" %}
In order for this tool to be effective, you need to install all relevant package managers on your local environment, see [Installing Supported Package Managers for Resolver](https://docs.checkmarx.com/en/34965-19198-installing-supported-package-managers-for-resolver.html).
{% endhint %}


## Usage
```
./cx scan sca-realtime [flags]
```


## Flags
**`--project-dir <string>, -p <string>` Required**

Path to the project folder on which the SCA scan will run.

{% hint style="warning" %}
This must point to a regular project folder and NOT a zip archive.
{% endhint %}


## Examples
**Scanning a folder - Sample command**

```
./cx scan sca-realtime --project-dir C:\goatlin
```

<details>

<summary>Sample response</summary>

```
{
  "results": [
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "This affects the package mpath before 0.8.4. A type confusion vulnerability can lead to a bypass of CVE-2018-16490. In particular, the condition ignoreProperties.indexOf(parts[i]) !== -1 returns -1 if parts[i] is ['__proto__']. This is because the method that has been called if the input is an array is Array.prototype.indexOf() and not String.prototype.indexOf(). They behave differently depending on the type of the input.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-p92x-r36w-9395"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/aheckmann/mpath/pull/13"
          }
        ],
        "packageIdentifier": "mpath",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2021-23438",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2021-23438",
        "cvssScore": 9.800000190734863,
        "cveName": "CVE-2021-23438",
        "cvss": {
          "version": 4,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "HIGH",
          "attackComplexity": "LOW",
          "integrityImpact": "HIGH",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "lib/utils.js in mquery before 3.2.3 allows a pollution attack because a special property (e.g., __proto__) can be copied during a merge or clone operation.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-45q2-34rf-mr94"
          }
        ],
        "packageIdentifier": "mquery",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2020-35149",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2020-35149",
        "cvssScore": 5.300000190734863,
        "cveName": "CVE-2020-35149",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "NONE",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "LOW",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The mergeClone function in the node.js mquery package before 3.2.5 is vulnerable to prototype pollution.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Disclosure",
            "url": "https://www.huntr.dev/bounties/1-npm-mquery"
          }
        ],
        "packageIdentifier": "mquery",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cxc8ffd605-ddff",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cxc8ffd605-ddff",
        "cvssScore": 5.300000190734863,
        "cveName": "Cxc8ffd605-ddff",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "NONE",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "LOW",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Disputed",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The package `body-parser` is vulnerable to prototype pollution, as it does no sanitation to the values received via the incoming JSON data. A remote attacker can inject a `__proto__` object to the application, which would successfully be parsed on the server side. This affects the integrity of the application.\n\n",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Other",
            "url": "https://gist.github.com/rgrove/3ea9421b3912235e978f55e291f19d5d/revisions"
          },
          {
            "type": "Issue",
            "url": "https://github.com/expressjs/body-parser/issues/347"
          }
        ],
        "packageIdentifier": "body-parser",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx14b19a02-387a",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx14b19a02-387a",
        "cvssScore": 6.5,
        "cveName": "Cx14b19a02-387a",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "LOW",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "LOW",
      "description": "The package `bluebird` is vulnerable to memory leak, when running the function longStackTraces() with the flag `--expose_gc`. This causes a significant increase in the memory usage, affecting the server's availability.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/petkaantonov/bluebird/issues/1080"
          }
        ],
        "packageIdentifier": "bluebird",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cxda14f253-4e52",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cxda14f253-4e52",
        "cvssScore": 3.700000047683716,
        "cveName": "Cxda14f253-4e52",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "HIGH",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "Mongoose before 5.12.2 is vulnerable to prototype pollution.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/Automattic/mongoose/issues/10035"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/Automattic/mongoose/pull/10053"
          }
        ],
        "packageIdentifier": "mongoose",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cxba0aa4f8-fd76",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cxba0aa4f8-fd76",
        "cvssScore": 7.5,
        "cveName": "Cxba0aa4f8-fd76",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "NONE",
          "confidentiality": "HIGH",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "Mongoose is a MongoDB object modeling tool designed to work in an asynchronous environment. Mongoose versions prior to 6.4.6 are vulnerable to Prototype Pollution. The \"Schema.path()\" and \"Schema.add()\" function is vulnerable to prototype pollution when setting the schema object. This vulnerability allows modification of the Object prototype and could be manipulated into a Denial of Service (DoS) attack.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-f825-f98c-gj3g"
          },
          {
            "type": "Disclosure",
            "url": "https://huntr.dev/bounties/055be524-9296-4b2f-b68d-6d5b810d1ddd"
          },
          {
            "type": "Issue",
            "url": "https://github.com/Automattic/mongoose/issues/12085"
          },
          {
            "type": "Release Note",
            "url": "https://github.com/Automattic/mongoose/releases/tag/6.4.6"
          }
        ],
        "packageIdentifier": "mongoose",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2022-2564",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2022-2564",
        "cvssScore": 9.800000190734863,
        "cveName": "CVE-2022-2564",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "HIGH",
          "attackComplexity": "LOW",
          "integrityImpact": "HIGH",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "The qs package as used in Express through 4.17.3 and other products, allows attackers to cause a Node process hang for an Express application because an \"__ proto__ key\" can be used. In many typical Express use cases, an unauthenticated remote attacker can place the attack payload in the query string of the URL that is used to visit the application, such as \"a[__proto__]=b&a[__proto__]&a[length]=100000000\". This vulnerability affects qs versions through 6.2.3, 6.3.0 through 6.3.2, 6.4.0, 6.5.0 through 6.5.2, 6.6.0, 6.7.0 through 6.7.2, 6.8.0 through 6.8.2, 6.9.0 through 6.9.6 and 6.10.0 through 6.10.2  (and therefore Express 4.17.3, which has \"deps: qs@6.9.7\" in its release description, is not vulnerable).",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-hrpp-h998-j3pp"
          },
          {
            "type": "Disclosure",
            "url": "https://github.com/n8tz/CVE-2022-24999"
          },
          {
            "type": "Release Note",
            "url": "https://github.com/expressjs/express/releases/tag/4.17.3"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/ljharb/qs/pull/428"
          }
        ],
        "packageIdentifier": "qs",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2022-24999",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2022-24999",
        "cvssScore": 7.5,
        "cveName": "CVE-2022-24999",
        "cvss": {
          "version": 1,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "In NPM `debug`, the `enable` function accepts a regular expression from user input without escaping it. Arbitrary regular expressions could be injected to cause a Denial of Service attack on the user's browser, otherwise known as a ReDoS (Regular Expression Denial of Service). This is a different issue than CVE-2017-16137.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/debug-js/debug/issues/737"
          },
          {
            "comment": "Roadmap that mentions issue",
            "type": "Other",
            "url": "https://github.com/debug-js/debug/issues/656"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/brunodays/POCs/blob/master/debug/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx8bc4df28-fcf5",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx8bc4df28-fcf5",
        "cvssScore": 7.5,
        "cveName": "Cx8bc4df28-fcf5",
        "cvss": {
          "version": 4,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The package debug is vulnerable to memory leakage when instance is created inside a function. The function `debug` in the file `common.js` does not free up used memory unless there's a call to `destroy()` function. This affects the availability.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/699"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx65603961-769c",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx65603961-769c",
        "cvssScore": 5.300000190734863,
        "cveName": "Cx65603961-769c",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "NPM `debug` prior to 4.3.0 has a Memory Leak when creating `debug` instances inside a function which can have a significant impact in the Availability. This happens since the function `debug` in the file `src/common.js` does not free up used memory.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/MarioTeixeiraCx/POCs/blob/main/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx89601373-08db",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx89601373-08db",
        "cvssScore": 7.5,
        "cveName": "Cx89601373-08db",
        "cvss": {
          "version": 3,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "In NPM `debug`, the `enable` function accepts a regular expression from user input without escaping it. Arbitrary regular expressions could be injected to cause a Denial of Service attack on the user's browser, otherwise known as a ReDoS (Regular Expression Denial of Service). This is a different issue than CVE-2017-16137.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/debug-js/debug/issues/737"
          },
          {
            "comment": "Roadmap that mentions issue",
            "type": "Other",
            "url": "https://github.com/debug-js/debug/issues/656"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/brunodays/POCs/blob/master/debug/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx8bc4df28-fcf5",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx8bc4df28-fcf5",
        "cvssScore": 7.5,
        "cveName": "Cx8bc4df28-fcf5",
        "cvss": {
          "version": 4,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The package debug is vulnerable to memory leakage when instance is created inside a function. The function `debug` in the file `common.js` does not free up used memory unless there's a call to `destroy()` function. This affects the availability.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/699"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx65603961-769c",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx65603961-769c",
        "cvssScore": 5.300000190734863,
        "cveName": "Cx65603961-769c",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "NPM `debug` prior to 4.3.0 has a Memory Leak when creating `debug` instances inside a function which can have a significant impact in the Availability. This happens since the function `debug` in the file `src/common.js` does not free up used memory.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/MarioTeixeiraCx/POCs/blob/main/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx89601373-08db",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx89601373-08db",
        "cvssScore": 7.5,
        "cveName": "Cx89601373-08db",
        "cvss": {
          "version": 3,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    }
  ],
  "totalCount": 14,
  "scanID": ""
}
```

</details>

