# Detection & Response

## Centralise monitoring and alerting

Logging and monitoring provide visibility into the runtime behaviour of the product. Centralising logging and monitoring data makes it easier to understand and manage the product. It also makes it harder for an attacker to cover their tracks. Propagating relevant identifiers throughout logging and monitoring data ensures events can be accurately correlated, for example, for a user, virtual machine, session, request, etc.

All systems that a team is responsible for should feed application and infrastructure logs into their centralised monitoring system, and alerts should be configured to notify the delivery team when exceptional behaviour occurs.

## Use intrusion detection

Application and infrastructure logs provide a rich set of data to operate the product, but don't always highlight when patterns of behaviour resemble a potential security incident. Using intrusion detection tools increases your ability to spot and alert on suspicious behaviour as early as possible.

When running in a cloud platform, it is valuable to consume the cloud provider's native security monitoring services, such as [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/) and [AWS GuardDuty](https://aws.amazon.com/guardduty/). In addition, other tools are available such as [Sysdig Secure](https://sysdig.com/products/secure/), [Sysdig Falco](https://sysdig.com/opensource/falco/), [Twistlock](https://www.twistlock.com/), [Aqua Security](https://www.aquasec.com/), [OSSEC](https://www.ossec.net/), [Osquery](https://osquery.io/), etc.

## Use honeypots for active detection

Sometimes it can be hard to separate out the signal from the noise, and it's difficult to know for certain whether some activity was conducted maliciously. Honeypots, and various similar techniques, give you a strong indication of malicious behaviour as they involve setting up resources that would never be accessed or used under normal conditions. When honeypots are accessed or used, analysis of the attacker's activity can be gathered to improve understanding of attacks and spot attacks against other normal resources. They also provide additional evidence to support legal proceedings.

Numerous techniques can be used to lure attackers into traps that immediately alert you to their presence. Examples include decoy login or payment forms, fake nodes on the network that present themselves as potential targets for attack, and even entire networks that are exclusively used to detect attackers conducting network reconnaissance.

Examples:

* [Thinkst Canary](https://canary.tools/)
* [Canarytokens](https://canarytokens.org/generate)
* [CyberChaff](https://galois.com/project/cyberchaff/)

