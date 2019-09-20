# Environment Provisioning

## Automate infrastructure hardening

Hardening involves reducing the attack surface of your server infrastructure by removing components and privileges that you don't need and securely configuring those that you do. It also means keeping up to date with the latest security patches that are relevant to your environment. Where appropriate, consider using cloud services that address many of the lower-level hardening requirements for you. Keep in mind, however, that using cloud services doesn't entirely remove the need for infrastructure hardening, but it can reduce the amount of effort on your part.

All infrastructure should be hardened according to vendor and industry guidelines, where available, including [CIS benchmarks](https://www.cisecurity.org/cis-benchmarks/) and product specific security guides \(e.g. AWS, Kubernetes, Docker, etc.\). Hardening should be applied to all infrastructure, including virtual machines, containers, language runtimes, and any cloud infrastructure / services that you may be using. For example, S3 buckets should be hardened to prevent accidental public access.

Infrastructure hardening is not a one-off event, but should rather be driven by an automated set of rules to validate that it meets your requirements. These checks should be run on a regular basis to detect when the infrastructure drifts from the intended configuration, and before any changes are promoted through environments to identify regressions.

Examples:

* VM / network scanning tools \([Nessus](https://www.tenable.com/products/nessus), [Qualys](https://www.qualys.com/), etc.\)
* CIS benchmark scanners \(e.g. [Docker Bench](https://github.com/docker/docker-bench-security), [Kube Bench](https://github.com/aquasecurity/kube-bench), etc.\)
* Attack tools \(e.g. [Metasploit](https://www.metasploit.com/), [Kube Hunter](https://kube-hunter.aquasec.com/), [Pacu](https://rhinosecuritylabs.com/aws/pacu-open-source-aws-exploitation-framework/), etc.\)
* Cloud tools \(e.g. [Turbot](https://turbot.com/), [Forseti Security](https://forsetisecurity.org/), [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/), [AWS Inspector](https://aws.amazon.com/inspector/), [Azure Security Centre](https://azure.microsoft.com/en-gb/services/security-center/), [GCP Cloud Security Command Center](https://cloud.google.com/security-command-center/), [ScoutSuite](https://github.com/nccgroup/ScoutSuite), etc.\)
* Certificate validation \(e.g. [Qualys SSL Labs](https://www.ssllabs.com/ssltest/), etc.\)

## Limit the blast radius of an attack

Segregation should be used to minimise the impact of an attack. Network & infrastructure segmentation limits the attacker's ability to traverse laterally in the event of a compromise. Secret segmentation separates keys or credentials, limiting the impact when secrets are compromised and facilitating easy revocation and rotation.

Least privilege also ensures that a compromise is contained to a limited set of infrastructure. For example, an application should only have limited access to the database it needs to talk to. It should not have access to the entire database server, including other unrelated databases.

## Securely configure third-party products

Many software products are not secure by default. Out-of-the-box and quickstart guides and configurations will often lead an insecure system with easily-discovered vulnerabilities. Insecure configuration of software is one of the most common causes of system compromise, and can potentially lead to significant impact to the organisation. This has resulted in [Security Misconfiguration](https://github.com/OWASP/Top10/blob/master/2017/en/0xa6-security-misconfiguration.md) being included at position 6 in the OWASP Top 10 2017.

All software should be configured to enable security features such as authentication and access control, and to remove unsafe defaults such as default administrative credentials \(following vendor security documentation where available\).

A good example is the easy discovery of [publicly exposed Jenkins servers](https://www.shodan.io/search?query=jenkins+200) on Shodan. Attackers use tools like this to discover likely easy targets, where default admin credentials will probably succeed.

## Centralised and automated secret management

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

## Always deploy via the pipeline

It should only be possible to deploy software that has been produced through the pipeline, rather than allowing uncontrolled deployments that cannot be verified.

The pipeline gives repeatability, traceability and an audit of all changes that have made all the way through to production. It ensures that all the necessary due diligence, such as security and functional testing, has been completed successfully to avoid issues being introduced into production. This is particularly important under emergency scenarios where there's pressure to release rapid fixes, because this same pressure increases the chance of introducing vulnerabilities or defects.

