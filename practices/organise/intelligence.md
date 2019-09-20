# Intelligence

## Make security visible in the software catalogue

The organisation should provide a central view of all software products they create, including relevant metadata \(e.g. owning team, deployed versions, links to operability dashboards, source repo, build jobs, etc.\). This should be automatically kept up to date, preferably by pulling the information directly from the relevant systems \(e.g. GitHub, Jenkins, Grafana, Kibana, deployment tooling, etc.\).

Security Engineering should ensure that security tooling is integrated with the software catalogue or inventory so that teams can be easily informed of the security issues in their services and understand the issues they are accountable for. This also provides a high-level view of where the greatest risk is and which projects need more assistance from Security Engineering.

## Conduct a post-mortem after security incidents

Security Engineering should ensure that blameless post-mortems are conducted after every security incident, involving representatives across the organisation. A post-mortem is a written record of an incident, its impact, the actions taken to mitigate or resolve it, the root cause\(s\), and the follow-up actions to prevent the incident from recurring.

The post-mortem should be shared within the organisation so that other teams can learn valuable lessons and to encourage a culture of openness and disclosure.

Examples of other companies that have done this publicly:

* [Gentoo GitHub admin compromise](https://wiki.gentoo.org/wiki/Project:Infrastructure/Incident_Reports/2018-06-28_Github)
* [GitHub DDoS attack](https://github.blog/2018-03-01-ddos-incident-report/)
* [Homebrew GitHub personal access token leak](https://brew.sh/2018/08/05/security-incident-disclosure/)
* [Parity hacked via security bug introduced during refactoring](https://www.parity.io/the-multi-sig-hack-a-postmortem/)
* [Insider bitcoin theft from ShapeShift](http://moneyandstate.com/looting-of-the-fox/)

