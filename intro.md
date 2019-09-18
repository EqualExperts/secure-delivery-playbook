# Introduction

This playbook defines a set of principles and practices that Equal Experts recommends for delivery of secure software. Our approach is based on a combination of first-hand experience and industry best practice.

We hold a similar view to that of the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) \(emphasis added\):

> ... we prefer to distribute capabilities into teams rather than having a centralized team with that capability. There are risks when you choose to distribute decision making authority, for example, ensuring that teams are meeting internal standards. We mitigate these risks in two ways. First, **we have practices that focus on enabling each team to have that capability**, and **we provide access to experts who ensure that teams raise the bar on the standards they need to meet**. Second, **we put in place mechanisms that carry out automated checks to ensure standards are being met**.

The practices defined are technology and vendor agnostic, allowing each team to determine the best way to adopt them in their specific context.

## Who's this playbook for?

We've created this playbook to help teams work together to deliver secure software. It's not just for software engineers; it is for everyone involved in delivering software. It's also not prescriptive about how each of the practices should be adopted, but allows you to determine which practices are appropriate for you and the best way to implement them.

## How is this different to... ?

The practices in this playbook have focused on ensuring the important principles are achieved without being too low level or prescriptive. This ensures they can be applied across a wide range of environments and technologies, and are more resilient to the changes in the way we deliver and operate software. We have avoided using a scoring system, which can be manipulated or become the objective, so that the focus is on secure software.

We have outlined other well known resources and how this playbook differs from each of them.

### Secure coding standards

We've deliberately used the term 'Secure Delivery' because software security encompasses a lot more than just writing code. Addressing coding standards without considering delivery in its wider context would be failing to address security overall. It would also fail to emphasise the importance of every individual, regardless of role, in the delivery of secure software. Elements of this playbook can be used to inform secure coding standards, but we advise against using secure coding standards in isolation.

### OWASP SAMM and BSIMM

Both [OWASP SAMM](https://www.owasp.org/index.php/OWASP_SAMM_Project) and [BSIMM](https://www.bsimm.com/) are maturity models that allow you to measure the maturity of your organisation against a set of practices. While SAMM provides a set of community-curated practices, BSIMM practices are derived from an annual industry survey. SAMM is measuring maturity against a prescriptive set of practices whereas BSIMM allows you to measure the maturity of your organisation relative to its peers.

The Secure Delivery Playbook is not intended to be a maturity model. While SAMM "defines three maturity levels as objectives" for each practice, we don't believe a 'maturity score' should be the objective. It's easy to manipulate scoring systems and demonstrate 'maturity' while still being insecure. Instead, our objective is to deliver secure software. The practices exist only to facilitate the delivery of secure software - they're not valuable in and of themselves.

### OWASP ASVS and Proactive Controls

The [OWASP ASVS](https://github.com/OWASP/ASVS) provides a comprehensive set of potential security requirements that can be used in building software, and can be very helpful either as a starting point for defining your own requirements or for validating whether you've identified all the appropriate requirements for your product.

The [OWASP](https://www.owasp.org/index.php/OWASP_Proactive_Controls) [Proactive Controls](https://www.owasp.org/index.php/OWASP_Proactive_Controls) lists a combination of controls and techniques that should be applied in every software project. This is somewhere in between the ASVS and the Secure Delivery Playbook, as it does describe techniques or practices you can adopt but also describes controls you should implement. It's unclear why the list is limited to ten items, other than perhaps to align to the [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) project.

The Secure Delivery Playbook does not attempt to provide a prescriptive low level of detail, but instead acts as a guide for delivery practices you should consider adopting to deliver secure software. We have however, referenced the ASVS as a valuable source of information when defining security requirements, and we see this as complementary to the playbook.

### Core Infrastructure Initiative Best Practices

The [Linux Foundation Core Infrastructure Initiative Best Practices](https://bestpractices.coreinfrastructure.org/en) project has defined a set of criteria for open source projects to demonstrate that they're following best practice. Many of the criteria don't necessarily apply to internal corporate projects, but others are more generally applicable.

We've found resources like this to be helpful for determining whether the practices we adopt are inline with industry norms, and whether new practices have emerged that we should consider including in our own projects.

However, the Secure Delivery Playbook is not a scoring system and will not earn you an independently verifiable badge. We choose not to be prescriptive, but instead to provide guidance that allows teams to select which practices are most suitable in their context. This also ensures teams think about the practices critically and with an eye on business value, rather than being influenced to achieve a silver or gold badge.

## Security Engineers and Security Champions

In this playbook we refer to both Security Engineers and Security Champions. These are quite different roles but the distinction may be unclear to you if you've not heard of them before. We explain below what each of these roles looks like and the kind of skills required to be successful in them.

### Security Engineer

The best security engineers are software security people, but software security people are often impossible to find. When you need to grow the number of security engineers in your organisation by developing existing people, start with developers and teach them about security. Starting with network security people and attempting to teach them about software, compilers, SDLCs, bug tracking, and everything else in the software universe usually fails to produce the desired results. Unfortunately, no amount of traditional security knowledge can overcome a lack of experience building software.

Security engineers come in a variety of shapes and sizes. All good security engineering teams include both people with deep coding experience and people with architectural experience. Software security can't only be about finding specific bugs such as the OWASP Top Ten. Code review is an important best practice, and to perform code review you must actually understand code \(not to mention the huge piles of security bugs\). However, the best code reviewers sometimes make poor software architects, and asking them to perform an architecture risk analysis will only result in blank stares. Make sure you cover architectural capabilities in your security engineering team in the same way that you cover code. Finally, a security engineer is often asked to mentor, train, and work directly with hundreds of developers. Communications skills, teaching capability, and consulting practical knowledge are must-haves for at least a portion of the security engineering team.

{% hint style="info" %}
Our description of a Security Engineer is based on what [BSIMM](https://www.bsimm.com/) defines as a _Software Security Group_. We have made some minor changes to better align with our terminology and culture.
{% endhint %}

### Security Champions

Security Champions are essential to scale security effectively. The ratio of security specialists to developers tends to be very low; it's not unusual to operate on a ratio of 1:100 or less. To be effective, we can't rely on a central team for all security activity, and we must empower delivery teams to own the security of their own products in a meaningful way. Security Champions are widely recognised as the best solution to this problem.

To quote [Mozilla](https://wiki.mozilla.org/Security/Champions):

* Security Champions are active members of a team that make help to make decisions about when to engage the Security Team
* Act as the "voice" of security for the given product or team
* Assist in the triage of security bugs for their team or area
