# Inception

This is an early opportunity to identify security requirements and areas of risk before development gets underway. The main objective of inception is to de-risk delivery. Inception should include the delivery team and stakeholders to ensure everyone understands the part they play in delivering a secure product.

## Agree on risk appetite

Security should be balanced against other competing concerns, such as usability or time to market. It is important to understand the importance of security for the product being developed. For example, a payments system may require much higher security than a company blog. Security is important in both of these products, but the context determines how much risk the organisation is willing to accept.

A clear understanding of the risk appetite, agreed upon by all participants, can ensure that an appropriate amount of effort is spent securing the product. When designing or building a feature, you can incorporate the right controls that satisfy the risk appetite without spending more than is needed.

A process that can be used to manage risk appetite is:

1. Stakeholders should identify the level of risk acceptable to them, ideally quantitatively
2. [Threat modelling](https://en.wikipedia.org/wiki/Threat_model) to understand what controls are likely to ensure the risk appetite is met
3. [Measurement](../operate/detection-and-response.md) to understand whether the risk has been adequately addressed and to adapt the threat model and required controls as needed

## Agree on roles & responsibilities

It is important to establish early on who is ultimately responsible for the security of the product. In some environments, the Product Owner is fully accountable and responsible for all aspects of it, but in other environments the central security team retains responsibility.

Knowing this at the start of the delivery will ensure that the team understands who has the authority to make decisions about security trade-offs and who approves production deployments. Ideally, the Product Owner should have full responsibility for both the features and the security of the product, as they have the full knowledge of the product to make trade-offs on behalf of the organisation.

## Understand the shared responsibility model

The team should understand the shared responsibility model between the product and any services they're using, whether they're internal services \(e.g. a centrally managed Kubernetes cluster or PaaS\) or external cloud services.

The overall accountability for security of the product falls on the delivery team. They're accountable for ensuring any services they rely on meet their security needs, even those they're not responsible for. For example, the delivery team may be accountable for their choice of cloud provider, even though they're not responsible for implementing the cloud provider's data-center security controls. Where it's not clear under a shared responsibility model that a particular area is being covered \(e.g. VM hardening\), the team needs to take ownership to ensure that is covered. This ensures the team is aware of their responsibilities for securing the product and the need to ensure these responsibilities are assigned within the team. If any of the responsibilities can't be assigned within the roles in the delivery team, the team should be fully supported by Security Engineering so it can deliver the expected level of security.

## Produce an architectural threat model

Threat modelling is a useful activity for examining what we're going to build and what could go wrong. This should begin during inception, before any software has been built, and [continue throughout the life of the product](stories-and-epics.md#iterative-and-incremental-threat-modelling). Threat modelling helps to identify areas of risk, and consequently the potential controls or design changes that the organisation feels are needed. This brings security issues to light early on, allowing them to be more easily factored into architectural decisions before they've been implemented.

The architectural threat model provides an overview of the high-level threats and risks for the whole product. There's value in keeping this up to date as the architecture evolves, so that the overall product risk can be easily understood and managed.

## Include security in Definition of Done

A Definition of Done \(DoD\) allows everyone to share a common view of what it means to complete a story. The most effective way to produce secure software is to make it secure from the start. Including security aspects in your DoD ensures that security is built in, rather than being bolted on later \(or not at all\).

The delivery team should agree how they will include security in their DoD. For example, security requirements implemented and covered by passing automated tests.

## Explicitly identify security requirements

Threat models are helpful to identify areas of risk within the product we're building and the controls required to address these risks. However, this alone is insufficient as it doesn't capture external influences such as organisational policy or legislation. For example, data retention requirements wouldn't likely be highlighted by a threat model, but are often required for compliance with internal policies or legislation such as GDPR.

Explicitly identifying these requirements early on ensures the team is aware of what needs to be built before committing to a particular design. This allows for the greatest flexibility in determining how best to meet those needs.

Examples:

* [OWASP Application Security Verification Standard \(ASVS\)](https://github.com/OWASP/ASVS)
* [Core Infrastructure Initiative Best Practices Criteria](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md#security)

