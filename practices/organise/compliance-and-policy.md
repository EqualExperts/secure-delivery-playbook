# Compliance & Policy

## Understand compliance context

It's important to understand where compliance requirements originate from so that appropriate controls can be put in place. Excessive controls can negatively impact productivity or encourage teams to work around them in order to complete their work. It can also increase time to market and overall cost of delivery. Insufficient controls can leave the organisation exposed to risk, potentially resulting in fines or other sanctions from regulators. Therefore it's critical to ensure that the principles behind the compliance requirements are well understood so that they can be efficiently adapted to the organisation.

## Enforce policy as code

Wherever possible, policies should be written as code that is executed automatically. This applies to both software development \(e.g. preventing deployment of an application containing a critical vulnerability\) and infrastructure \(e.g. detecting policy violations such as public S3 buckets\). The use of automated tools allows a good balance between delivery team productivity and policy compliance. Automated tools allow the Security Engineering team to scale as delivery teams can implement and execute policy compliance on a regular basis without individual compliance audits.

Examples of automated tooling include:

* [Inspec](https://www.inspec.io/)
* [Forseti Security](https://forsetisecurity.org/)
* [Sysdig Falco](https://sysdig.com/opensource/falco/) \([Sysdig Secure](https://sysdig.com/products/secure/)\)
* [Turbot](https://turbot.com/)
* [Datree](https://datree.io/)
* [Open Policy Agent](https://www.openpolicyagent.org/)

