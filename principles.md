# Principles

Delivering secure software is about a lot more than just writing secure code. Security is not a product that can be purchased after development is complete, or a set of features that can be easily added on later: it's an integral part of everything we build, balanced by risk.

The following principles guide our everyday work and are the foundation of the practices we adopt.

## Good Security is Collaborative

[We deliver as a team of equals](https://www.equalexperts.com/our-people/our-values/). While we may work on a relatively small delivery team, we recognise that we play an important part of a much bigger team that has collective responsibility to the organisation. We must remember that the whole product delivery team is accountable and responsible for the software they create, while receiving support from Security Engineering. Security is not exclusively a technology problem; it requires cooperation and collaboration across disciplines, including product, engineering, security and other stakeholders.

A successful software security initiative depends on strong collaboration between everyone involved, including Security Engineering, product and delivery teams, together with support from senior management.

> Security is everyone's job now, not just the security team's. With continuous integration and continuous deployment, all developers have to be security engineers, we move too fast for there to be time for reviews by the security team beforehand.
>
> * Werner Vogels \(CTO, Amazon\)

## Good Security is Continuous

In order to be effective, security should be a consideration during all activities involved in delivery, including:

* Inception
* Requirements gathering
* Architecture and design
* Development
* Testing
* Deployment
* Operations
* Decommissioning

This means that we consider the security implications of the work we're doing throughout delivery, rather than leaving it to the end. [We practice constant verification, not wishful thinking](https://www.equalexperts.com/our-people/our-values/?=1). Applied to security, this means we build security in right from the start with tests to verify the quality of what we've delivered; we don't wait for a penetration test or security review just before release and hope for the best. We take steps to ensure that - as much as is possible - every iteration of the software is subject to the right level of security review, enabling the continuous delivery of secure software that creates value as early as possible. We aim to have completed all relevant security testing by the point that a feature is functionally ready for deployment.

## Good Security is Contextual

Security is a response to risks faced by the organisation. This means we must first understand those risks in order to respond appropriately. These risks can impact an organisation in many ways, such as:

* Reduction in profitability \(either through direct customer loss, or failure to win new customers\)
* Reputational damage
* Financial damage \(regulatory fines or compensation of affected users\)
* Regulatory non-compliance
* Data / system compromise
* Availability

We balance the need for security to reduce risk alongside other organisational needs, such as:

* Feature delivery
* Performance
* Operability
* Usability
* Accessibility

This doesn't mean we satisfy one organisational need at the expense of the others. It means we find the best balance of all of the competing priorities in order to deliver the most suitable product for the organisation. Where we recommend or implement a tradeoff, the process by which we arrived at this is made clear so that the organisation is aware of the risks and expected impact.

## Good Security is Cumulative

Security is best achieved in layers. Don't rely on a single practice or tool to meet all your security needs, but instead adopt multiple complementary practices and tools to provide layers of protection.

This ensures that if a single tool or process fails to identify a vulnerability, or a single control fails, there will be other layers of security to avoid compromise. No single tool, process or control provides complete security, which is why the cumulative effect of multiple layers of security is paramount.

