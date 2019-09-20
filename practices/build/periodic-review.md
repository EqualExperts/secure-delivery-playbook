# Periodic Review

## Get an independent perspective on the product delivery

Sometimes we can get a bit too close to the detail to see the issues we need to address. A second opinion from someone we trust and respect can help validate our decisions, assumptions and designs. Explaining our solution to someone else often helps us better understand our own product. These independent reviews shouldn't be seen as a gate that requires approval, but rather as a regular opportunity to ensure we're heading in the right direction and solving problems in the best way possible.

This also ensures we regularly review and update our architectural threat model and any other high-level artefacts to make sure they still represent what is being delivered. Over time, the product and context evolve \(e.g. more data, more users, change in business process, etc.\). If security controls don't evolve alongside, hidden risks and threats can emerge in the product.

It can be helpful to involve a Security Engineer in these reviews, as they can bring insight on security issues faced by other teams or in the wider industry that may have a bearing on the product.

## Review known risks

Risk evolves over time as the product, context and risk appetite changes. Known risks should be regularly reviewed to ensure they are still within the agreed risk appetite. Even risks that have previously been accepted should be reviewed to ensure the basis for their acceptance is still valid.

## Use code as evidence for auditors

Where you're required to provide evidence to auditors for compliance \(e.g. PCI DSS\), use automated systems as evidence rather than creating separate documents that will get out of date. For example:

* Source control shows traceability of code and changes \(this can also be linked to change tracking systems such as Jira\)
* Infrastructure-as-code combined with immutable infrastructure means that no changes can be made outside of that audit trail
* Deployments / build tools can provide an audit of changes to production

When providing evidence in this form, it provides value to the delivery team as well as auditors \(e.g. Terraform scripts that show firewall configuration for PCI DSS\). This avoids creating lengthy documents that require continual effort to maintain, and instead relies on code that defines the way the system works. This also avoids contradiction between what the documentation says and what happens in reality.

