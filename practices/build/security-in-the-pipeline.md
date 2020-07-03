# Security in the Pipeline

## Avoid using sensitive production data in test environments

Often the easiest way of obtaining a set of representative test data is to take a copy of a production database. When we use a copy of sensitive production in a test environment, this environment needs the same level of security controls as the environment where it was designed to be stored. These controls increase the financial and operational cost of running a test environment, which is why it's often significantly cheaper and easier to operate a system with fake or reliably anonymised test data.

When integrating with third parties that don't provide a test environment or test accounts, suitable controls need to be put in place to ensure that access to that data is adequately protected. Ideally, a requirement should be raised for the third party to provide either a test environment or a test account that does not expose sensitive data.

## Avoid leaking sensitive data in source control

The delivery team should be trained to ensure that commits do not contain sensitive data. In addition, commits should be reviewed for sensitive data, ideally before the commit is pushed to a central repository. Consider using pre-commit hooks that automatically detect sensitive data to avoid this data entering source control systems. Alternatively, there are numerous tools available that scan popular source control systems for sensitive data such as API keys, credentials, private keys, etc.

When sensitive data has been detected, the team should be alerted so they can remove it from the source control history and rotate any credentials or keys that might have been exposed.

Examples:

* [GitRob](https://github.com/michenriksen/gitrob)
* [Datree](https://datree.io/)
* [Git-secrets](https://github.com/awslabs/git-secrets)
* [truffleHog](https://github.com/dxa4481/truffleHog)
* [GitHub Token Scanning](https://help.github.com/en/articles/about-token-scanning)

## Adopt the two-person rule

A person contributing to a product in isolation increases the opportunity for accidental or malicious vulnerabilities to be introduced.

Teams should adopt the two-person rule, meaning that two or more people are involved in making each change. This can be achieved ideally through pair programming or a code review i.e. via pull requests. This reduces the chance for errors, and increases the difficulty to introduce intentional damage because collusion would be required.

## Treat security tests like functional tests

When building any product feature, we always write accompanying tests to prove that the feature works correctly and is protected from regression. This applies equally to security features and controls, for example:

* Unit tests confirming input validation is correct and covers all cases
* Integration tests ensuring a protected feature requires valid authorisation

## Builds should be isolated from each other

To ensure that builds are repeatable and their dependencies come from known good locations, they should be isolated from each other and prevented from sharing state. For example, this can be achieved using ephemeral build slaves or running builds within independent Docker containers.

When a build is based on some shared state \(e.g. local Maven cache\), it's possible that a previous build or anyone with access to the build server can pollute the Maven cache with malicious code that could then be packaged into your artefact.

## Security analysis on every build

Continuous Integration / Continuous Delivery \(CI/CD\) pipelines provide a good opportunity to detect potential security vulnerabilities early in development by integrating with security analysis tools. There are numerous open source and commercial products covering a wide variety of languages and frameworks, and it's possible to write custom tools based on your own needs. These tools can be applied to application code, configuration files, Dockerfiles, Infrastructure-as-Code, and running applications.

Results from these tests should [feed into the software catalogue](../organise/intelligence.md#make-security-visible-in-the-software-catalogue) to promote visibility and ensure that security vulnerabilities are being responded to in a timely manner.

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
* [Cryptosense Analyzer](https://cryptosense.com/analyzer/)

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
* [Meterian](https://meterian.com)

## Ensure availability and consistency of artefacts

Delivery teams produce a number of different types of artefacts that need to be deployed. It is important to ensure that the artefacts are available to be deployed on demand. This reduces the likelihood of downtime and ensures we can recover from failure.

It's also important to ensure that the same artefact is consistently deployable across different environments: for example, we should only deploy the exact artefact that was tested, and not a separately built copy of the artefact. This guarantees that any dependencies have not changed since the artefact was tested \(e.g. when depending on ‘latest' versions\).

## Ensure provenance of first-party artefacts

We need to reliably establish that any deployed artefact or dependency has been produced by the delivery team. Establishing provenance in this way avoids malicious or otherwise vulnerable code from being introduced into the product. There are many ways to achieve this depending on the environment.

One popular approach is to use a secure, central repository with strong access controls and fine-grained permissions. This ensures that only authorised individuals have uploaded artefacts to the central repository, and relies on suitable namespacing to isolate teams.

Another approach is to sign artefacts and verify these signatures whenever an artefact is pulled from the repository. This can be taken a step further with GPG signed commits, ensuring traceability back to the individual that committed the code.

## Establish provenance of third-party components

Using third-party components is essential in software delivery. However, this can potentially introduce vulnerabilities.

When selecting a third party component to use, you should evaluate the trustworthiness of the artefact and its author. This includes an assessment of both the author and the artefact itself, including their reputation, how well they test the artefact, how well they protect their user accounts, and whether there's a strong community supporting or using it. For example, using a Docker image produced by an unknown individual is problematic, as you have no evidence to suggest the person has the skills or motivation not to introduce vulnerabilities.

Once you've established that the author and artefact are suitable, then you need to establish the provenance of the artefact. This can be gained through confidence in the security and access control of the repository the artefact comes from. Alternatively, or in addition, signed artefacts can provide assurance in the provenance of the artefact when the signature is validated. An example of this is [Docker Content Trust](https://docs.docker.com/engine/security/trust/content_trust/).

Examples of where this has caused problems:

* [Ruby rest-client](https://github.com/rest-client/rest-client/issues/713)
* [Npm event-stream](https://snyk.io/blog/malicious-code-found-in-npm-package-event-stream/)

## Automate pipeline progression based on policy

As we begin to introduce security checks into the pipeline, it's important that we know when to fail the build and when to allow it through. This requires an up-front decision about policy and ensuring that the security checks are configured to meet that policy.

In some cases, we can detect critical security issues that should prevent the build from progressing any further until they have been addressed. For example, identifying a critical vulnerability in a dependency can be one of the first steps in a build. This is analogous to a failing unit test that can be picked up very early.

In other cases, we may identify security issues that need to be fixed, but are not severe enough to warrant blocking the pipeline. In these cases, it is important to ensure the issue is resolved without preventing the release of business value to the customer.

Automating these policies helps direct delivery teams towards the issues they are required to fix prior to a production release, and still highlights other issues that also need to be addressed although less urgently.

