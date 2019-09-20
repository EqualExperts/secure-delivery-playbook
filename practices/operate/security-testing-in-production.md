# Security Testing in Production

## Automate production vulnerability scanning

It's beneficial to automatically review your public-facing product for deviations from security best practice. For example, TLS and other web security best practices are published and updated regularly by reputable organisations. Automatically scanning your public-facing site allows you to ensure that you are continually up-to-date with the latest practices. It also highlights issues that can easily go unnoticed, such as certificates that are due to expire soon.

This type of scanning is important because the infrastructure that hosts or exposes your product, such as Apigee, Akamai or AWS ELBs, may not have been included in your pipeline security scanning.

For example, [Mozilla Observatory](https://observatory.mozilla.org/), [Qualys SSL Labs](https://www.ssllabs.com/ssltest/) and [Hardenize](https://www.hardenize.com/) provide a score based on good web security practices. This can be automated to ensure your site continually provides the right level of protection for your users.

## Automate production dependency checking

Even when dependency checking is performed on every build, the product running in production should be regularly scanned for newly-discovered vulnerabilities, because new vulnerabilities are being discovered every day.

## Use chaos engineering

Chaos engineering helps to identify vulnerabilities and weaknesses in a product by testing how the system behaves under failure or undesired conditions. It allows the delivery team to ensure compromises are detected and prevented, and whether additional security controls are required. It is important that the effectiveness of controls are observable to enable both controls and the understanding of risk to be improved over time.

In addition to detecting and preventing compromises, chaos engineering allows delivery teams and stakeholders to regularly practise and improve incident management.

There are many different approaches to incorporating chaos engineering into delivery. Some teams set aside some time for Chaos Days or Game Days, where certain individuals deliberately introduce chaos into perceived weak points. Other mechanisms include tools that automatically introduce chaos, such as by killing VMs or containers at random.

Examples:

* [Equal Experts blog: A day of chaos](https://www.equalexperts.com/blog/our-thinking/chaos-day/)
* [Chaos Monkey](https://github.com/Netflix/SimianArmy/wiki/Chaos-Monkey)
* [kube-monkey](https://github.com/asobti/kube-monkey)

## Use purple team exercises

Purple team exercises help to identify vulnerabilities and weaknesses in a product by simulating the behaviours and techniques of malicious attackers in the most realistic way possible. It allows the delivery team to ensure compromises are detected and prevented, and whether additional security controls are required. It is important that the effectiveness of controls are observable to enable both controls and the understanding of risk to be improved over time.

In addition to detecting and preventing compromises, purple team exercises give delivery teams and stakeholders the opportunity to practise and improve incident management.

Purple team exercises are preferred over Red/Blue Team because they focus on improving the skills and learning of the Blue Team rather than separating the two teams in the simulation. This shortens the feedback loop between the attacker and the defender to improve the speed to identify improvements.

Examples:

* [The Difference Between Red, Blue, and Purple Teams](https://danielmiessler.com/study/red-blue-purple-teams/)

## Use penetration testing

Independent assessment of the security of the product through effective penetration testing enables validation of security controls and monitoring used to detect attempts to compromise the product. Having an independent assessment reduces the likelihood that issues will be missed due to bias or over-familiarity with the product. These types of assessments are a real measure of how well the risk appetite for the product has been met.

Penetration testing can more accurately simulate how a real attacker may try to circumvent security controls, which makes them an invaluable addition to your security testing capabilities. They should be appropriately scoped to ensure maximum value and to avoid focusing on areas beyond the scope of the delivery team. While narrowly-scoped penetration tests can reduce time and improve focus, we should ensure that the test is conducted under realistic conditions. For example, testing multiple services in isolation will not reveal security issues that are only present when combining the services together as they would be in a real environment.

## Use bug bounties

Bug bounties provide an opportunity to discover vulnerabilities and weaknesses from independent security researchers based on a real attacker's view of your product. Compared to penetration testing and purple team exercises, bug bounties allow independent evaluation of the security of the product from an outsider's perspective.

Even when not operating bug bounties, you should use well known approaches, such as [security.txt](https://securitytxt.org/), to guide security researchers that want to report issues. This ensures you get early warning of issues and avoid lengthy delays while outsiders try to navigate your internal communication structures.

Examples:

* [HackerOne](https://www.hackerone.com/)
* [Bugcrowd](https://www.bugcrowd.com/)
* [Security.txt](https://securitytxt.org/)

