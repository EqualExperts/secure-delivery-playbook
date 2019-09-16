# Organise

## Scaling Security

### Embed Security Champions in all teams

[Security Champions](https://wiki.mozilla.org/Security/Champions) are widely recognised as the most effective way to scale security. While remaining primarily skilled as developers, testers, architects, business analysts, etc., they act as a voice for security within a team and bring a foundational knowledge of security into daily discussions. They identify when more expertise is required and engage with Security Engineering.

All teams should have a Security Champion who regularly interacts with Security Engineering and ensures the team receives the support they need to meet security needs.

### Co-locate technical security specialists alongside delivery teams

Working from the same physical location can confer advantages that are hard to replicate remotely. While we value the flexibility we get from communications tools like Slack, having technical security specialists physically present brings significant benefits. It allows them to get hands on, pairing with developers and testers or running threat modelling sessions increases their impact substantially and often reduces the time to resolve critical issues. It also has a very positive effect on the relationship between Security Engineering and delivery teams.

When an engagement spans multiple locations, technical security specialists should be available to meet delivery teams in person wherever possible.

## Vulnerability Management

### Monitor published vulnerabilities in third party products

Vulnerabilities in third party products or libraries are a significant risk to organisations. A Security Engineering Team should actively monitor relevant vulnerability databases for newly discovered / published vulnerabilities and alert the impacted delivery teams of new risks.

It should also actively monitor a wide range of public vulnerability data sources \(e.g. using a threat intelligence feed\) to gain early warning of any new vulnerabilities that might impact the organisation. Automated tooling is available to enable the matching of the data against any software used / developed by the organisation.

### Introduce a vulnerability remediation process

In order to respond to identified vulnerabilities effectively, a process should be put in place to help teams understand the steps that should be taken and where they can go for help. Risk assessment forms an important part of this process as it helps determine how best to respond. It can be helpful to model the impact of previous relevant incidents within the organisation, including product stakeholders in this process, and also drawing on threat intelligence on the wider industry. Many organisations and standards bodies have produced guides and standards that can aid this process.

* [Factor Analysis of Information Risk \(FAIR\)](https://www.fairinstitute.org/)
* [Mozilla Rapid Risk Assessment \(RRA\)](https://infosec.mozilla.org/guidelines/risk/rapid_risk_assessment.html)
* [Common Vulnerability Scoring System \(CVSS\)](https://www.first.org/cvss/specification-document)
* [OWASP Risk Rating Methodology](https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology)
* [DREAD](https://en.wikipedia.org/wiki/DREAD_%28risk_assessment_model%29)
* [MITRE ATT&CK](https://attack.mitre.org/)

### Promote visibility and transparency

In some organisations, security is kept behind closed doors and not readily shared with delivery teams. This leads to a complicated relationship between security and delivery, as delivery teams aren't given sufficient information to adequately address security issues. A common example of this problem is when security logs are sent to a separate SIEM \(Security Information and Event Management\) tool that isn't made available to the teams that are responsible for the software being monitored.

Security engineers should work openly and collaboratively with delivery teams at all times, ensuring that security logs and metrics are visible to everyone involved in delivery. This can be achieved through dashboards in observability tools and sharing access to all security operations data in real time with delivery teams. After every incident, a blameless post-mortem should be conducted \(including all relevant representatives\) to identify areas for improvement. These improvements should be shared with the rest of the organisation to ensure it also benefits.

### Encourage effective use of penetration testing

Penetration testing is an opportunity to identify security issues. It's most effective when the testing is goal focused \(i.e. steal sensitive data\) and the tester works in conjunction with the team, explaining issues as they're discovered and providing recommendations on how to fix the issue. This gives the opportunity for the team to fix some issues during the penetration test, and ensures that the final report is well understood. It is least effective when only a vulnerability scan is performed, as that could be automated in the delivery pipeline instead.

Penetration testing is a useful indicator of the success of the practices in Build & Operate.

### Manage external security researchers & bug bounties

Some organisations operate bug bounty schemes to encourage independent security researchers to help identify and fix security issues. Regardless of whether you operate a bug bounty, external security researchers expect all companies to provide a well signposted security contact where they can disclose vulnerabilities they've discovered.

Poor handling of disclosed vulnerabilities can lead to uncontrolled public disclosure and bad publicity. Good handling of this can lead to substantial security improvements at a very low cost. That's why organisations need to cultivate good relationships with security researchers, ensuring they're paid promptly, kept informed and not treated with suspicion. Publishing a vulnerability disclosure policy so that security researchers have clear expectations about the disclosure process can be helpful.

Examples:

* [HackerOne](https://www.hackerone.com/)
* [Bugcrowd](https://www.bugcrowd.com/)
* [Security.txt](https://securitytxt.org/)

### Evaluate third party vendor / product security

Most organisations require a formal security evaluation before adopting new products or technologies. To do this, it needs technical security expertise to identify risks within the product and any supporting processes \(e.g. not just the technical implementation of the product, but also the way the vendor handles security issues and their expertise in security\).

Security Engineering should be actively involved in evaluating any third party suppliers & products. This should not be seen as a yes/no assessment, but rather as a way to highlight potential weaknesses and recommend approaches to mitigate that risk.

## Incident Response

### Plan and rehearse incident response activities

Every organisation should have a comprehensive approach to incident response so that it can be ready when something goes wrong. Modern data protection laws and regulations also require an active approach to incident response \(i.e. breach detection and notification requirements in GDPR\). For incident response plans to be valuable they need to be regularly tested, including all parts of the organisation, to ensure the organisation as a whole is able to respond under pressure. For example, GDPR gives only 72 hours to determine whether a breach should be reported to the ICO \(Information Commissioner's Office\).

Security Engineers should be actively involved in defining the incident response plans and following these plans when an incident occurs. The incident response plans must be tested and rehearsed to ensure they address the risk faced by the organisation adequately. This can be achieved through approaches such as tabletop exercises, chaos engineering, and red/blue or purple team exercises that allow teams to identify how they respond under pressure in critical situations. The Security Engineering team must involve stakeholders across the organisation \(e.g. customer relations, PR, legal, engineering, etc.\) to ensure all parties know their role and are ready to assist when required.

Links:

* [PagerDuty IR Checklist](https://response.pagerduty.com/during/security_incident_response/)

### Collaborate on active security incidents

When a security incident arises, teams across the organisation should collaborate openly and share information to ensure the incident is responded to quickly and effectively. When this is centrally managed by a single team \(e.g. Security Engineering\) and there is no engagement with the delivery team, the effectiveness of the response is reduced and the time to resolve the incident is increased.

Engaging the delivery team is an important opportunity to learn and improve the security of future product delivery. We should use blameless post-mortems to share learnings more widely within the organisation. A culture of open information sharing around security incidents will lead to greater risk reduction to the organisation, as teams are better informed and motivated to avoid similar incidents in the future.

## Training

### Provide role-specific training

Each individual on a delivery team has a part to play, and should understand how security applies in their context. Although it may appear that security training should be focused on software engineers, it's important to provide training for all roles in a team including developer / engineering, BAs, POs, DLs, etc. For example, a Product Owner should understand the risk that the product is exposed to without appropriate security controls, and should be empowered to challenge security requirements that are not well defined.

Examples:

* [Hacksplaining](https://www.hacksplaining.com/)
* [Immersive Labs](https://www.immersivelabs.com/)
* [Security Journey](https://www.securityjourney.com/)
* [Secure Code Warrior](https://securecodewarrior.com/)

### Provide specialist consulting to teams

Delivery teams don't always have the experience or skills required to address more specialist areas of security. This leads to suboptimal solutions or increased risk or complexity. Security Engineering should provide specialists in order to assist delivery teams when the team lacks the skills to complete a particular feature \(for example when implementing features that require cryptography\).

Security Engineering should also be available to conduct or facilitate threat modelling sessions, and use this as an opportunity to teach this skill to others.

## Compliance & Policy

### Understand compliance context

It's important to understand where compliance requirements originate from so that appropriate controls can be put in place. Excessive controls can negatively impact productivity or encourage teams to work around them in order to complete their work. It can also increase time to market and overall cost of delivery. Insufficient controls can leave the organisation exposed to risk, potentially resulting in fines or other sanctions from regulators. Therefore it's critical to ensure that the principles behind the compliance requirements are well understood so that they can be efficiently adapted to the organisation.

### Enforce policy as code

Wherever possible, policies should be written as code that is executed automatically. This applies to both software development \(e.g. preventing deployment of an application containing a critical vulnerability\) and infrastructure \(e.g. detecting policy violations such as public S3 buckets\). The use of automated tools allows a good balance between delivery team productivity and policy compliance. Automated tools allow the Security Engineering team to scale as delivery teams can implement and execute policy compliance on a regular basis without individual compliance audits.

Examples of automated tooling include:

* [Inspec](https://www.inspec.io/)
* [Forseti Security](https://forsetisecurity.org/)
* [Sysdig Falco](https://sysdig.com/opensource/falco/) \([Sysdig Secure](https://sysdig.com/products/secure/)\)
* [Turbot](https://turbot.com/)
* [Datree](https://datree.io/)
* [Open Policy Agent](https://www.openpolicyagent.org/)

## Intelligence

### Make security visible in the software catalogue

The organisation should provide a central view of all software products they create, including relevant metadata \(e.g. owning team, deployed versions, links to operability dashboards, source repo, build jobs, etc.\). This should be automatically kept up to date, preferably by pulling the information directly from the relevant systems \(e.g. GitHub, Jenkins, Grafana, Kibana, deployment tooling, etc.\).

Security Engineering should ensure that security tooling is integrated with the software catalogue or inventory so that teams can be easily informed of the security issues in their services and understand the issues they are accountable for. This also provides a high-level view of where the greatest risk is and which projects need more assistance from Security Engineering.

### Conduct a post-mortem after security incidents

Security Engineering should ensure that blameless post-mortems are conducted after every security incident, involving representatives across the organisation. A post-mortem is a written record of an incident, its impact, the actions taken to mitigate or resolve it, the root cause\(s\), and the follow-up actions to prevent the incident from recurring.

The post-mortem should be shared within the organisation so that other teams can learn valuable lessons and to encourage a culture of openness and disclosure.

Examples of other companies that have done this publicly:

* [Gentoo GitHub admin compromise](https://wiki.gentoo.org/wiki/Project:Infrastructure/Incident_Reports/2018-06-28_Github)
* [GitHub DDoS attack](https://github.blog/2018-03-01-ddos-incident-report/)
* [Homebrew GitHub personal access token leak](https://brew.sh/2018/08/05/security-incident-disclosure/)
* [Parity hacked via security bug introduced during refactoring](https://www.parity.io/the-multi-sig-hack-a-postmortem/)
* [Insider bitcoin theft from ShapeShift](http://moneyandstate.com/looting-of-the-fox/)
