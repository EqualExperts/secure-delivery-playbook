# Operate

## Environment Provisioning

**Automate infrastructure hardening**

Hardening involves reducing the attack surface of your server infrastructure by removing components and privileges that you don't need and securely configuring those that you do. It also means keeping up to date with the latest security patches that are relevant to your environment. Where appropriate, consider using cloud services that address many of the lower-level hardening requirements for you. Keep in mind, however, that using cloud services doesn't entirely remove the need for infrastructure hardening, but it can reduce the amount of effort on your part.

All infrastructure should be hardened according to vendor and industry guidelines, where available, including [CIS benchmarks](https://www.cisecurity.org/cis-benchmarks/) and product specific security guides \(e.g. AWS, Kubernetes, Docker, etc.\). Hardening should be applied to all infrastructure, including virtual machines, containers, language runtimes, and any cloud infrastructure / services that you may be using. For example, S3 buckets should be hardened to prevent accidental public access.

Infrastructure hardening is not a one-off event, but should rather be driven by an automated set of rules to validate that it meets your requirements. These checks should be run on a regular basis to detect when the infrastructure drifts from the intended configuration, and before any changes are promoted through environments to identify regressions.

Examples:

* VM / network scanning tools \([Nessus](https://www.tenable.com/products/nessus), [Qualys](https://www.qualys.com/), etc.\)
* CIS benchmark scanners \(e.g. [Docker Bench](https://github.com/docker/docker-bench-security), [Kube Bench](https://github.com/aquasecurity/kube-bench), etc.\)
* Attack tools \(e.g. [Metasploit](https://www.metasploit.com/), [Kube Hunter](https://kube-hunter.aquasec.com/), [Pacu](https://rhinosecuritylabs.com/aws/pacu-open-source-aws-exploitation-framework/), etc.\)
* Cloud tools \(e.g. [Turbot](https://turbot.com/), [Forseti Security](https://forsetisecurity.org/), [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/), [AWS Inspector](https://aws.amazon.com/inspector/), [Azure Security Centre](https://azure.microsoft.com/en-gb/services/security-center/), [GCP Cloud Security Command Center](https://cloud.google.com/security-command-center/), [ScoutSuite](https://github.com/nccgroup/ScoutSuite), etc.\)
* Certificate validation \(e.g. [Qualys SSL Labs](https://www.ssllabs.com/ssltest/), etc.\)

**Limit the blast radius of an attack**

Segregation should be used to minimise the impact of an attack. Network & infrastructure segmentation limits the attacker's ability to traverse laterally in the event of a compromise. Secret segmentation separates keys or credentials, limiting the impact when secrets are compromised and facilitating easy revocation and rotation.

Least privilege also ensures that a compromise is contained to a limited set of infrastructure. For example, an application should only have limited access to the database it needs to talk to. It should not have access to the entire database server, including other unrelated databases.

**Securely configure third-party products**

Many software products are not secure by default. Out-of-the-box and quickstart guides and configurations will often lead an insecure system with easily-discovered vulnerabilities. Insecure configuration of software is one of the most common causes of system compromise, and can potentially lead to significant impact to the organisation. This has resulted in [Security Misconfiguration](https://github.com/OWASP/Top10/blob/master/2017/en/0xa6-security-misconfiguration.md) being included at position 6 in the OWASP Top 10 2017.

All software should be configured to enable security features such as authentication and access control, and to remove unsafe defaults such as default administrative credentials \(following vendor security documentation where available\).

A good example is the easy discovery of [publicly exposed Jenkins servers](https://www.shodan.io/search?query=jenkins+200) on Shodan. Attackers use tools like this to discover likely easy targets, where default admin credentials will probably succeed.

**Centralised and automated secret management**

We want to reduce the risk of compromised secrets, increase visibility of the use of secrets through auditing, and increase our ability to respond if secrets are compromised. Having a system that makes it easy to manage secrets means we can offer fine-grained secrets that also reduce the blast radius when a secret is compromised.

For example, using automated certificate management through services such as [LetsEncrypt](https://letsencrypt.org/) allows you to provision short-lived certificates that automatically renew, reducing the risk of downtime due to certificate expiry and the impact of certificate compromise.

We should aim for centralised, automated secrets management that can provide features such as:

* Easy rotation
  * Rapid response when a secret is comprised
  * Rotation when there could be a compromise \(e.g. a team member leaves\)
  * Reducing the lifespan of a secret
* Access controls
  * Based on policy or roles \(e.g. delivery team can write secrets, but only the product can read them\)
  * Based on environment \(e.g. production secrets can only be retrieved from within the production environment\)
* Auditing
  * Record who has accessed what secrets when, and whether they were successful
  * Record of all administrative activities \(e.g. creating new access policies\)

Examples of secrets include:

* Credentials \(e.g. API keys, usernames and passwords, private keys, etc.\)
* Encryption keys \(e.g. symmetric keys and asymmetric private keys\)
* Certificates \(e.g. private keys and associated certificates presented by web servers\)

Links:

* [Hashicorp Vault](https://www.vaultproject.io/)
* [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)
* [Azure Key Vault](https://azure.microsoft.com/en-gb/services/key-vault/)
* [LetsEncrypt](https://letsencrypt.org/)

**Always deploy via the pipeline**

It should only be possible to deploy software that has been produced through the pipeline, rather than allowing uncontrolled deployments that cannot be verified.

The pipeline gives repeatability, traceability and an audit of all changes that have made all the way through to production. It ensures that all the necessary due diligence, such as security and functional testing, has been completed successfully to avoid issues being introduced into production. This is particularly important under emergency scenarios where there's pressure to release rapid fixes, because this same pressure increases the chance of introducing vulnerabilities or defects.

## Security of the Pipeline

The pipeline produces the product artefacts that are deployed into production. In order to trust that these artefacts have been correctly produced without vulnerabilities or malicious code being introduced, the security of the pipeline needs to be as good as the security of the product itself.

**Harden the pipeline as a production system**

In addition to [infrastructure hardening](), build pipelines have unique characteristics that must be addressed in order to preserve their security. Failing to do this can lead to a compromise of the build system.

For example, builds should not be allowed to run on Jenkins master nodes as this has [serious security implications](https://wiki.jenkins.io/display/JENKINS/Security+implication+of+building+on+master) and been used to compromise Jenkins administrator accounts in the past. Relevant security controls should be enabled and default user accounts should be changed on all pipeline systems. All build plugins should be carefully vetted to avoid introducing vulnerabilities in a [similar way to all product dependencies](). These should be kept up to date with the latest security patches.

**Monitor the pipeline as a production system**

Pipelines are production systems in their own right, and therefore warrant the same attention to monitoring and alerting as any live system would. Failing to do this prevents you from identifying anomalous behaviour \(such as failed login attempts, etc.\) and hinders your ability to investigate in the event of an incident.

CI/CD pipelines should have a centralised logging and monitoring infrastructure in place that all components \(e.g. source control, build servers, artefact repositories, etc.\) feed into, so that suspicious behaviour can be detected and alerted on.

**Manage secrets securely**

Pipelines require access to various external systems, such as source repositories, artefact repositories and target environments for deployment. This provides an attacker with the ability to control infrastructure or deployments, access secrets, or anything else involved in building, packaging and deploying code.

Wherever possible, avoid the need to manage secrets directly and use native platform features that handle this on your behalf. For example, cloud providers offer identity and access management features, such as AWS IAM and GCP Cloud Identity and Access Management, that enable workloads to be authorised while automatically handling key/credential rotation, auditing, etc.

Within the pipeline, all secrets should be stored and managed securely, ideally using a [secrets management system](). Where it's not possible to use a central secrets management system, it's important to understand what controls are provided by the pipeline tools and their limitations.

The principle of least privilege should be applied for secrets \(e.g. read only access to source control\). This includes using unique credentials for the build pipeline, so that it can be traced back if suspicious activity is detected.

Be aware that secrets may be accidentally or intentionally exposed via build logs, and mechanisms should be put in place to detect this or prevent it from happening if possible.

## Security Testing in Production

**Automate production vulnerability scanning**

It's beneficial to automatically review your public-facing product for deviations from security best practice. For example, TLS and other web security best practices are published and updated regularly by reputable organisations. Automatically scanning your public-facing site allows you to ensure that you are continually up-to-date with the latest practices. It also highlights issues that can easily go unnoticed, such as certificates that are due to expire soon.

This type of scanning is important because the infrastructure that hosts or exposes your product, such as Apigee, Akamai or AWS ELBs, may not have been included in your pipeline security scanning.

For example, [Mozilla Observatory](https://observatory.mozilla.org/), [Qualys SSL Labs](https://www.ssllabs.com/ssltest/) and [Hardenize](https://www.hardenize.com/) provide a score based on good web security practices. This can be automated to ensure your site continually provides the right level of protection for your users.

**Automate production dependency checking**

Even when dependency checking is performed on every build, the product running in production should be regularly scanned for newly-discovered vulnerabilities, because new vulnerabilities are being discovered every day.

**Use chaos engineering**

Chaos engineering helps to identify vulnerabilities and weaknesses in a product by testing how the system behaves under failure or undesired conditions. It allows the delivery team to ensure compromises are detected and prevented, and whether additional security controls are required. It is important that the effectiveness of controls are observable to enable both controls and the understanding of risk to be improved over time.

In addition to detecting and preventing compromises, chaos engineering allows delivery teams and stakeholders to regularly practise and improve incident management.

There are many different approaches to incorporating chaos engineering into delivery. Some teams set aside some time for Chaos Days or Game Days, where certain individuals deliberately introduce chaos into perceived weak points. Other mechanisms include tools that automatically introduce chaos, such as by killing VMs or containers at random.

Examples:

* [Equal Experts blog: A day of chaos](https://www.equalexperts.com/blog/our-thinking/chaos-day/)
* [Chaos Monkey](https://github.com/Netflix/SimianArmy/wiki/Chaos-Monkey)
* [kube-monkey](https://github.com/asobti/kube-monkey)

**Use purple team exercises**

Purple team exercises help to identify vulnerabilities and weaknesses in a product by simulating the behaviours and techniques of malicious attackers in the most realistic way possible. It allows the delivery team to ensure compromises are detected and prevented, and whether additional security controls are required. It is important that the effectiveness of controls are observable to enable both controls and the understanding of risk to be improved over time.

In addition to detecting and preventing compromises, purple team exercises give delivery teams and stakeholders the opportunity to practise and improve incident management.

Purple team exercises are preferred over Red/Blue Team because they focus on improving the skills and learning of the Blue Team rather than separating the two teams in the simulation. This shortens the feedback loop between the attacker and the defender to improve the speed to identify improvements.

Examples:

* [The Difference Between Red, Blue, and Purple Teams](https://danielmiessler.com/study/red-blue-purple-teams/)

**Use penetration testing**

Independent assessment of the security of the product through effective penetration testing enables validation of security controls and monitoring used to detect attempts to compromise the product. Having an independent assessment reduces the likelihood that issues will be missed due to bias or over-familiarity with the product. These types of assessments are a real measure of how well the risk appetite for the product has been met.

Penetration testing can more accurately simulate how a real attacker may try to circumvent security controls, which makes them an invaluable addition to your security testing capabilities. They should be appropriately scoped to ensure maximum value and to avoid focusing on areas beyond the scope of the delivery team. While narrowly-scoped penetration tests can reduce time and improve focus, we should ensure that the test is conducted under realistic conditions. For example, testing multiple services in isolation will not reveal security issues that are only present when combining the services together as they would be in a real environment.

**Use bug bounties**

Bug bounties provide an opportunity to discover vulnerabilities and weaknesses from independent security researchers based on a real attacker's view of your product. Compared to penetration testing and purple team exercises, bug bounties allow independent evaluation of the security of the product from an outsider's perspective.

Even when not operating bug bounties, you should use well known approaches, such as [security.txt](https://securitytxt.org/), to guide security researchers that want to report issues. This ensures you get early warning of issues and avoid lengthy delays while outsiders try to navigate your internal communication structures.

Examples:

* [HackerOne](https://www.hackerone.com/)
* [Bugcrowd](https://www.bugcrowd.com/)
* [Security.txt](https://securitytxt.org/)

## Detection & Response

**Centralise monitoring and alerting**

Logging and monitoring provide visibility into the runtime behaviour of the product. Centralising logging and monitoring data makes it easier to understand and manage the product. It also makes it harder for an attacker to cover their tracks. Propagating relevant identifiers throughout logging and monitoring data ensures events can be accurately correlated, for example, for a user, virtual machine, session, request, etc.

All systems that a team is responsible for should feed application and infrastructure logs into their centralised monitoring system, and alerts should be configured to notify the delivery team when exceptional behaviour occurs.

**Use intrusion detection**

Application and infrastructure logs provide a rich set of data to operate the product, but don't always highlight when patterns of behaviour resemble a potential security incident. Using intrusion detection tools increases your ability to spot and alert on suspicious behaviour as early as possible.

When running in a cloud platform, it is valuable to consume the cloud provider's native security monitoring services, such as [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/) and [AWS GuardDuty](https://aws.amazon.com/guardduty/). In addition, other tools are available such as [Sysdig Secure](https://sysdig.com/products/secure/), [Sysdig Falco](https://sysdig.com/opensource/falco/), [Twistlock](https://www.twistlock.com/), [Aqua Security](https://www.aquasec.com/), [OSSEC](https://www.ossec.net/), [Osquery](https://osquery.io/), etc.

**Use honeypots for active detection**

Sometimes it can be hard to separate out the signal from the noise, and it's difficult to know for certain whether some activity was conducted maliciously. Honeypots, and various similar techniques, give you a strong indication of malicious behaviour as they involve setting up resources that would never be accessed or used under normal conditions. When honeypots are accessed or used, analysis of the attacker's activity can be gathered to improve understanding of attacks and spot attacks against other normal resources. They also provide additional evidence to support legal proceedings.

Numerous techniques can be used to lure attackers into traps that immediately alert you to their presence. Examples include decoy login or payment forms, fake nodes on the network that present themselves as potential targets for attack, and even entire networks that are exclusively used to detect attackers conducting network reconnaissance.

Examples:

* [Thinkst Canary](https://canary.tools/)
* [Canarytokens](https://canarytokens.org/generate)
* [CyberChaff](https://galois.com/project/cyberchaff/)
