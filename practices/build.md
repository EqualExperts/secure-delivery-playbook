# Build

## Inception

This is an early opportunity to identify security requirements and areas of risk before development gets underway. The main objective of inception is to de-risk delivery. Inception should include the delivery team and stakeholders to ensure everyone understands the part they play in delivering a secure product.

### Agree on risk appetite

Security should be balanced against other competing concerns, such as usability or time to market. It is important to understand the importance of security for the product being developed. For example, a payments system may require much higher security than a company blog. Security is important in both of these products, but the context determines how much risk the organisation is willing to accept.

A clear understanding of the risk appetite, agreed upon by all participants, can ensure that an appropriate amount of effort is spent securing the product. When designing or building a feature, you can incorporate the right controls that satisfy the risk appetite without spending more than is needed.

A process that can be used to manage risk appetite is:

1. Stakeholders should identify the level of risk acceptable to them, ideally quantitatively
2. [Threat modelling](https://en.wikipedia.org/wiki/Threat_model) to understand what controls are likely to ensure the risk appetite is met
3. [Measurement]() to understand whether the risk has been adequately addressed and to adapt the threat model and required controls as needed

### Agree on roles & responsibilities

It is important to establish early on who is ultimately responsible for the security of the product. In some environments, the Product Owner is fully accountable and responsible for all aspects of it, but in other environments the central security team retains responsibility.

Knowing this at the start of the delivery will ensure that the team understands who has the authority to make decisions about security trade-offs and who approves production deployments. Ideally, the Product Owner should have full responsibility for both the features and the security of the product, as they have the full knowledge of the product to make trade-offs on behalf of the organisation.

### Understand the shared responsibility model

The team should understand the shared responsibility model between the product and any services they're using, whether they're internal services \(e.g. a centrally managed Kubernetes cluster or PaaS\) or external cloud services.

The overall accountability for security of the product falls on the delivery team. They're accountable for ensuring any services they rely on meet their security needs, even those they're not responsible for. For example, the delivery team may be accountable for their choice of cloud provider, even though they're not responsible for implementing the cloud provider's data-center security controls. Where it's not clear under a shared responsibility model that a particular area is being covered \(e.g. VM hardening\), the team needs to take ownership to ensure that is covered. This ensures the team is aware of their responsibilities for securing the product and the need to ensure these responsibilities are assigned within the team. If any of the responsibilities can't be assigned within the roles in the delivery team, the team should be fully supported by Security Engineering so it can deliver the expected level of security.

### Produce an architectural threat model

Threat modelling is a useful activity for examining what we're going to build and what could go wrong. This should begin during inception, before any software has been built, and [continue throughout the life of the product](). Threat modelling helps to identify areas of risk, and consequently the potential controls or design changes that the organisation feels are needed. This brings security issues to light early on, allowing them to be more easily factored into architectural decisions before they've been implemented.

The architectural threat model provides an overview of the high-level threats and risks for the whole product. There's value in keeping this up to date as the architecture evolves, so that the overall product risk can be easily understood and managed.

### Include security in Definition of Done

A Definition of Done \(DoD\) allows everyone to share a common view of what it means to complete a story. The most effective way to produce secure software is to make it secure from the start. Including security aspects in your DoD ensures that security is built in, rather than being bolted on later \(or not at all\).

The delivery team should agree how they will include security in their DoD. For example, security requirements implemented and covered by passing automated tests.

### Explicitly identify security requirements

Threat models are helpful to identify areas of risk within the product we're building and the controls required to address these risks. However, this alone is insufficient as it doesn't capture external influences such as organisational policy or legislation. For example, data retention requirements wouldn't likely be highlighted by a threat model, but are often required for compliance with internal policies or legislation such as GDPR.

Explicitly identifying these requirements early on ensures the team is aware of what needs to be built before committing to a particular design. This allows for the greatest flexibility in determining how best to meet those needs.

Examples:

* [OWASP Application Security Verification Standard \(ASVS\)](https://github.com/OWASP/ASVS)
* [Core Infrastructure Initiative Best Practices Criteria](https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md#security)

## Stories & Epics

### Consider security needs on every story or epic

The Security Champion should be actively involved in defining security needs within user stories. Security Champions should help the team define the security acceptance criteria and engage with Security Engineers for more specialist support when required. For example, implementing features using cryptography may require assistance or review from a Security Engineer. Consideration should be given to defining sufficient test cases to meet the security needs, e.g. ensuring an unauthenticated user is not able to access protected functionality. Consideration should also be given to whether any known risks for the product are impacted by this change, which should be updated as appropriate.

The Security Champion should be responsible for ensuring that security is considered for every story. This is an opportunity for Security Champions to develop their knowledge and experience with assistance from Security Engineers, and will gradually make the delivery team more independent. It will also help the Security Engineers to focus their time on the most critical or complex cases where specialist support is needed.

### Iterative and incremental threat modelling

We should do threat modelling whenever there's a significant change to the product. When creating epics and stories, we must consider whether the architectural threat model needs to be updated or whether there needs to be a specific threat model created for this change. The objective is to identify whether any security controls need to change or be added to maintain the security of the product.

Creating threat models in response to each change ensures the activity is focused. Consider timeboxing threat modelling activity to ensure maximum effectiveness - teams are more likely to continue with this practice if it is not too time consuming.

Also consider whether any known risks for the product are impacted by this change, and update the risks as appropriate.

### Security Engineers should review security-critical changes

Some code has a higher impact on the security of the product, such as code handling authentication. In addition, some changes are more complex and require specialist experience to ensure it is secure, such as cryptography. Defining sufficient test cases can be difficult, and often benefits from having someone with security experience available to help.

Sections of security-critical code should be reviewed by experienced Security Engineers. It is possible to integrate this into source control to prevent security-critical code from being merged until it has been reviewed, for example by tagging associated stories. Alternatively, this can also be achieved by having a good close working relationship with Security Engineers so they are aware and available to help when needed.

## Security in the Pipeline

### Avoid using sensitive production data in test environments

Often the easiest way of obtaining a set of representative test data is to take a copy of a production database. When we use a copy of sensitive production in a test environment, this environment needs the same level of security controls as the environment where it was designed to be stored. These controls increase the financial and operational cost of running a test environment, which is why it's often significantly cheaper and easier to operate a system with fake or reliably anonymised test data.

When integrating with third parties that don't provide a test environment or test accounts, suitable controls need to be put in place to ensure that access to that data is adequately protected. Ideally, a requirement should be raised for the third party to provide either a test environment or a test account that does not expose sensitive data.

### Avoid leaking sensitive data in source control

The delivery team should be trained to ensure that commits do not contain sensitive data. In addition, commits should be reviewed for sensitive data, ideally before the commit is pushed to a central repository. Consider using pre-commit hooks that automatically detect sensitive data to avoid this data entering source control systems. Alternatively, there are numerous tools available that scan popular source control systems for sensitive data such as API keys, credentials, private keys, etc.

When sensitive data has been detected, the team should be alerted so they can remove it from the source control history and rotate any credentials or keys that might have been exposed.

Examples:

* [GitRob](https://github.com/michenriksen/gitrob)
* [Datree](https://datree.io/)
* [Git-secrets](https://github.com/awslabs/git-secrets)
* [truffleHog](https://github.com/dxa4481/truffleHog)
* [GitHub Token Scanning](https://help.github.com/en/articles/about-token-scanning)

### Adopt the two-person rule

A person contributing to a product in isolation increases the opportunity for accidental or malicious vulnerabilities to be introduced.

Teams should adopt the two-person rule, meaning that two or more people are involved in making each change. This can be achieved ideally through pair programming or a code review i.e. via pull requests. This reduces the chance for errors, and increases the difficulty to introduce intentional damage because collusion would be required.

### Treat security tests like functional tests

When building any product feature, we always write accompanying tests to prove that the feature works correctly and is protected from regression. This applies equally to security features and controls, for example:

* Unit tests confirming input validation is correct and covers all cases
* Integration tests ensuring a protected feature requires valid authorisation

### Builds should be isolated from each other

To ensure that builds are repeatable and their dependencies come from known good locations, they should be isolated from each other and prevented from sharing state. For example, this can be achieved using ephemeral build slaves or running builds within independent Docker containers.

When a build is based on some shared state \(e.g. local Maven cache\), it's possible that a previous build or anyone with access to the build server can pollute the Maven cache with malicious code that could then be packaged into your artefact.

### Security analysis on every build

Continuous Integration / Continuous Delivery \(CI/CD\) pipelines provide a good opportunity to detect potential security vulnerabilities early in development by integrating with security analysis tools. There are numerous open source and commercial products covering a wide variety of languages and frameworks, and it's possible to write custom tools based on your own needs. These tools can be applied to application code, configuration files, Dockerfiles, Infrastructure-as-Code, and running applications.

Results from these tests should [feed into the software catalogue]() to promote visibility and ensure that security vulnerabilities are being responded to in a timely manner.

Some tools include threat intelligence data, which provides an indication of how potential vulnerabilities / weaknesses are being used in the wild. This data therefore provides a useful mechanism to further prioritise the resolution of identified vulnerabilities.

There are multiple different approaches to security analysis, including static analysis, dynamic analysis, interactive analysis and dependency checking.

**Static analysis \(SAST\)**

Static analysis inspects source code to detect vulnerabilities through data flow analysis and other pattern matching rules. It relies on knowledge of where data comes in \(sources\) and where it flows out \(sinks\) of the application. It is good at identifying certain types of vulnerabilities, such as injection attacks and insecure use of cryptography, by inspecting your code. These types of vulnerabilities can be identified quite accurately compared to dynamic analysis.

Static analysis should be run on every build to scan for known weaknesses. A suitable scan policy should be defined to ensure accuracy and efficiency, which helps delivery teams focus on high-value issues. This maintains developer confidence in the tool, as alerts are only raised for important, valid findings.

Examples:

* [Checkmarx](https://www.checkmarx.com/)
* [Veracode](https://www.veracode.com/)
* [Brakeman](https://brakemanscanner.org/)
* [Find Security Bugs](https://find-sec-bugs.github.io/)

**Dynamic analysis \(DAST\)**

Dynamic analysis inspects the inputs and outputs of your running application to identify vulnerabilities that are visible when using an application. Dynamic analysis can easily identify issues such as common security-related HTTP headers and markup issues. However, it is typically less effective at detecting SQL injection or command injection attacks because it has to rely on heuristics, unlike static analysis which has full visibility of the source code.

Dynamic analysis can be relatively easily embedded in passive mode alongside existing integration tests, allowing it to detect security issues without significant investment. Active mode can also be considered to see how the application responds to known malicious inputs. However, active mode may not identify additional vulnerabilities that static analysis hasn't already detected.

Examples:

* [Veracode](https://www.veracode.com/)
* [OWASP ZAP](https://github.com/zaproxy/zaproxy)
* [Burp Suite](https://portswigger.net/burp)
* [Rapid7](https://www.rapid7.com/products/insightappsec/)

**Interactive analysis \(IAST\)**

Interactive analysis combines both static analysis and dynamic analysis by instrumenting your running application, allowing it to see your source code while also observing inputs and outputs. This potentially allows it to detect more issues with greater accuracy than either static analysis or dynamic analysis on their own.

Interactive security testing is possibly the most valuable form of testing to consider as it combines multiple security testing approaches into a single product, including SAST, DAST and SCA. These products can be embedded as part of existing integration tests in the CI pipeline. They can also be used in production to alert or block live attacks. This is known as runtime application security protection \(RASP\).

Examples:

* [Contrast Security](https://www.contrastsecurity.com/)

**Dependency checking**

Dependency checking \(also known as source composition analysis, SCA\) looks for known vulnerabilities and license issues in third party dependencies.

Third-party dependencies in applications and the underlying container or virtual machine can introduce vulnerabilities into the product. Every build should use the latest available vulnerability information to check that it's not producing an artefact that contains known vulnerabilities or licenses that conflict with organisational policy \(e.g. GPL\).

Free tools are available that can meet this need. However, commercial products exist that leverage a more comprehensive set of vulnerability data than what can be found in public sources such as [NIST NVD](https://nvd.nist.gov/) \(National Vulnerability Database\), and are often more accurate in matching CVEs to dependencies.

Examples:

* [SourceClear](https://www.sourceclear.com/)
* [Checkmarx](https://www.checkmarx.com/)
* [OWASP Dependency Check](https://jeremylong.github.io/DependencyCheck/)
* [Snyk](https://snyk.io/)
* [Sonatype](https://www.sonatype.com/)
* [Clair](https://github.com/coreos/clair)

### Ensure availability and consistency of artefacts

Delivery teams produce a number of different types of artefacts that need to be deployed. It is important to ensure that the artefacts are available to be deployed on demand. This reduces the likelihood of downtime and ensures we can recover from failure.

It's also important to ensure that the same artefact is consistently deployable across different environments: for example, we should only deploy the exact artefact that was tested, and not a separately built copy of the artefact. This guarantees that any dependencies have not changed since the artefact was tested \(e.g. when depending on ‘latest' versions\).

### Ensure provenance of first-party artefacts

We need to reliably establish that any deployed artefact or dependency has been produced by the delivery team. Establishing provenance in this way avoids malicious or otherwise vulnerable code from being introduced into the product. There are many ways to achieve this depending on the environment.

One popular approach is to use a secure, central repository with strong access controls and fine-grained permissions. This ensures that only authorised individuals have uploaded artefacts to the central repository, and relies on suitable namespacing to isolate teams.

Another approach is to sign artefacts and verify these signatures whenever an artefact is pulled from the repository. This can be taken a step further with GPG signed commits, ensuring traceability back to the individual that committed the code.

### Establish provenance of third-party components

Using third-party components is essential in software delivery. However, this can potentially introduce vulnerabilities.

When selecting a third party component to use, you should evaluate the trustworthiness of the artefact and its author. This includes an assessment of both the author and the artefact itself, including their reputation, how well they test the artefact, how well they protect their user accounts, and whether there's a strong community supporting or using it. For example, using a Docker image produced by an unknown individual is problematic, as you have no evidence to suggest the person has the skills or motivation not to introduce vulnerabilities.

Once you've established that the author and artefact are suitable, then you need to establish the provenance of the artefact. This can be gained through confidence in the security and access control of the repository the artefact comes from. Alternatively, or in addition, signed artefacts can provide assurance in the provenance of the artefact when the signature is validated. An example of this is [Docker Content Trust](https://docs.docker.com/engine/security/trust/content_trust/).

Examples of where this has caused problems:

* [Ruby rest-client](https://github.com/rest-client/rest-client/issues/713)
* [Npm event-stream](https://snyk.io/blog/malicious-code-found-in-npm-package-event-stream/)

### Automate pipeline progression based on policy

As we begin to introduce security checks into the pipeline, it's important that we know when to fail the build and when to allow it through. This requires an up-front decision about policy and ensuring that the security checks are configured to meet that policy.

In some cases, we can detect critical security issues that should prevent the build from progressing any further until they have been addressed. For example, identifying a critical vulnerability in a dependency can be one of the first steps in a build. This is analogous to a failing unit test that can be picked up very early.

In other cases, we may identify security issues that need to be fixed, but are not severe enough to warrant blocking the pipeline. In these cases, it is important to ensure the issue is resolved without preventing the release of business value to the customer.

Automating these policies helps direct delivery teams towards the issues they are required to fix prior to a production release, and still highlights other issues that also need to be addressed although less urgently.

## Periodic Review

### Get an independent perspective on the product delivery

Sometimes we can get a bit too close to the detail to see the issues we need to address. A second opinion from someone we trust and respect can help validate our decisions, assumptions and designs. Explaining our solution to someone else often helps us better understand our own product. These independent reviews shouldn't be seen as a gate that requires approval, but rather as a regular opportunity to ensure we're heading in the right direction and solving problems in the best way possible.

This also ensures we regularly review and update our architectural threat model and any other high-level artefacts to make sure they still represent what is being delivered. Over time, the product and context evolve \(e.g. more data, more users, change in business process, etc.\). If security controls don't evolve alongside, hidden risks and threats can emerge in the product.

It can be helpful to involve a Security Engineer in these reviews, as they can bring insight on security issues faced by other teams or in the wider industry that may have a bearing on the product.

### Review known risks

Risk evolves over time as the product, context and risk appetite changes. Known risks should be regularly reviewed to ensure they are still within the agreed risk appetite. Even risks that have previously been accepted should be reviewed to ensure the basis for their acceptance is still valid.

### Use code as evidence for auditors

Where you're required to provide evidence to auditors for compliance \(e.g. PCI DSS\), use automated systems as evidence rather than creating separate documents that will get out of date. For example:

* Source control shows traceability of code and changes \(this can also be linked to change tracking systems such as Jira\)
* Infrastructure-as-code combined with immutable infrastructure means that no changes can be made outside of that audit trail
* Deployments / build tools can provide an audit of changes to production

When providing evidence in this form, it provides value to the delivery team as well as auditors \(e.g. Terraform scripts that show firewall configuration for PCI DSS\). This avoids creating lengthy documents that require continual effort to maintain, and instead relies on code that defines the way the system works. This also avoids contradiction between what the documentation says and what happens in reality.
