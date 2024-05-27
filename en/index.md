HackInSDN is a framework that provides programmable infrastructure for teaching/learning networking and cybersecurity using testbed environments. Leveraging the network programmability provided by SDN environments, along with modern and classic network security tools, the HackInSDN framework enables an enriched teaching and learning environment for advanced topics in Cybersecurity and Networking. Some areas for studying, experimenting, and researching using HackInSDN include Intrusion Detection Systems, Anomaly Detection supported by Artificial Intelligence and Machine Learning, Dynamic Attack Mitigation, Isolated attacks simulation, Threat Intelligence information sharing, etc.

The HackInSDN can be instantiated on distributed testbed environments such as RNP's infrastructure and other testbed environments.

# Overview

The picture that follows illustrates the overall HackInSDN architecture.

![HackInSDN big picture](/assets/img/hackinsdn.png){:.centered}

The main components are presented below:

- **[Programmable Network Orchestrator - Kytos-ng](./kytos-info.html)**: The network Orchestrator plays a central role in HackInSDN architecture by enabling provisioning, management, and monitoring services andating all other components. The Kytos-ng (https://kytos-ng.github.io) SDN orchestrator is used in the HackInSDN framework because it provides at-scale production-grade SDN orchestration and a robust and flexible software layer.
- **Adaptive Mirroring**: This component will be developed to allow granular traffic mirroring of the services provisioned by the network Orchestrator for traffic inspection and monitoring.
- **Intelligent Containment and Filtering**: The goal here is to enable attack mitigation and filtering based on the anomaly events and alerts detected or network operator requests through the API.
- **[AI-Powered Anomaly Detection](./anomaly-detection.html)**: the AI-powered Anomaly Detection component integrates with the Network Orchestrator to receive measurements and generate anomaly alerts. Different network metrics will be analyzed using Machine Learning algorithms (supervised and unsupervised) to indicate perturbations on the normal behavior.
- **[Suricata](./suricata.html)**: Suricata is a high-performance Network IDS, IPS, and Network Security Monitoring engine. It is open source and owned by a community-run non-profit foundation, the Open Information Security Foundation (OISF). Suricata is developed by the OISF.
- **MISP Threat Intelligence and Sharing**: HackInSDN will provide means for sharing, storing, and correlating Indicators of Compromises of targeted attacks. Leveraging the MISP threat intelligence platform, defensive security teams (blue teams) will be able to share threat indicators, threat intelligence, and IP/DNS/URL reputation to enable automated detection and responsiveness to attacks.

- **[Adversary Simulator](./adversary-simulator.html)**: leveraging a variety of state-of-the-art tools and methodologies, this component provides means to replicate attack scenarios, including basic and common adversary tactics as well as sophisticated targeted attacks. Using the adversary simulator, students will benefit from different perspectives: gain knowledge of offensive security tools and methodologies, evaluate defensive security systems, exercise methodologies for incident handling, and gain practical experience in responding to skilled attacks.

# Partern Organizations

{:.text-align-center}
[![UFBA logo](/assets/img/ufba.png)](https://www.ufba.br)
[![IFBA logo](/assets/img/ifba.png)](https://www.ifba.edu.br)
[![FIU logo](/assets/img/fiu.png)](https://www.fiu.edu)

{:.text-align-center}
[![INSERT logo](/assets/img/insert.png)](http://insert.ufba.br)
[![Amlight Logo](/assets/img/amlight.png)](https://www.amlight.net)


# Acknowledgements

HackInSDN is funded by *Chamada Hackers do Bem* open call, [chamada pública para Pesquisa e Desenvolvimento 2023](https://www.rnp.br/noticias/hackers-do-bem-resultado-da-chamada-publica-para-pesquisa-e-desenvolvimento-2023){:target="_blank"}.

Read more about the [Hackers do Bem project](https://hackersdobem.org.br){:target="_blank"}.

# Additional information

 - [Getting started](./getting-started.html)
 - [Publications](./publications.html)
 - [Technical guides](./technical-guides.html)
 - [HackInSDN team](./hackinsdn-team.html)
 - [Source code and Licensing](./source-code-license.html)

# Support

Have you found a bug or wants to request a feature? [Open an issue!](https://github.com/hackinsdn/hackinsdn/issues)

To contact our team, send an e-mail to **hackinsdn [AT] ufba.br**.
