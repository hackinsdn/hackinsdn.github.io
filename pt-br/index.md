O HackInSDN oferece um ambiente completo de capacitação em segurança cibernética, com ferramentas avançadas como detecção de anomalias com IA, contenção de ataques e simulação de ameaças. Utilizando a programabilidade de redes, o projeto opera na infraestrutura de testbeds da RNP para formar profissionais em tópicos avançados de cibersegurança.


## Infraestrutura programável em testbed para ensino de redes e segurança GT HACKINSDN

O HackInSDN combina teoria e prática para formar profissionais em segurança cibernética, utilizando uma infraestrutura de testbeds. Com ferramentas avançadas, como detecção de anomalias com IA, contenção de ataques e simulação de ameaças, o projeto oferece uma capacitação completa em redes e segurança. Operando na infraestrutura distribuída da RNP, o HackInSDN prepara especialistas para lidar com cenários reais de cibersegurança.


## O projeto opera na infraestrutura distribuída da RNP, oferecendo um serviço contínuo e prático de formação em cibersegurança.

### Destaques do HackInSDN:

    Detecção de intrusão e anomalias
    Ferramentas para simulação de ataques
    Inteligência de ameaças e contenção de ataques


# Visão Geral

A Figura abaixo apresenta uma visão geral do HackInSDN.

![HackInSDN big picture](/assets/img/hackinsdn.png){:.centered}

Os principais módulos da ferramenta são:
- **[AI-Powered Anomaly Detection](./anomaly-detection.html)**: este componente será integrado ao Orquestrador de redes e receberá uma série de métricas de rede para então processar algoritmos de detecção de anomalias via Aprendizagem de Máquina Estatística e então gerar Alertas de Anômalia.
- **[Suricata](./suricata.html)**: Suricata é uma ferramenta de alta performance que pode funcionar como IDS (Sistema de Detecção de Intrusão) ou IPS (Sistema de Prevenção de Intrusão) e promove monitoramento de segurança de rede. É um software open source mantido por uma fundação sem fins lucrativos administrada pela comunidade, a Open Information Security Foundation (OISF). O Suricata é desenvolvido pela OISF.
- **[Programmable Network Orchestrator - Kytos-ng](./kytos-info.html)** o Orquestrador de Redes programável desempenha papel central na arquitetura provendo os serviços de gerenciamento e provisionamento da rede, e também integrando os demais componentes. O Kytos-ng (https://kytos-ng.github.io) é a plataforma de orquestração SDN que será usada como base no HackInSDN, pois incorpora uma solução de controle SDN escalável, flexível e altamente customizável/programável.
- **Adaptive Mirroring**: este módulo será desenvolvido no contexto do projeto HackInSDN para permitir o espelhamento de tráfego granular e elástico nos serviços de rede provisionados pelo Orquestrador.
- **[Intelligent Containment and Filtering](./containment-filtering.html)**: o papel deste módulo é prover serviços de contenção e filtragem de ataques a partir das anomalias e alertas detectados, ou a partir da solicitação do operador de redes.
- **MISP Threat Intelligence and Sharing**: mecanismos de inteligência de ameaça e compartilhamento de informações de segurança são essenciais para defesa e pesquisa em segurança atualmente.
- **[Adversary Simulator](./adversary-simulator.html)**: um conjunto de ferramentas do estado da arte e voltadas para offensive security será disponibilizada como parte do projeto HackInSDN para ser utilizadas na perspectiva de hacking ético e simular tráfego malicioso no ambiente descrito acima.

# Instituições parceiras

[![UFBA logo](/assets/img/ufba.png)](https://www.ufba.br)
[![IFBA logo](/assets/img/ifba.png)](https://www.ifba.edu.br)
[![FIU logo](/assets/img/fiu.png)](https://www.fiu.edu)

[![INSERT logo](/assets/img/insert.png)](http://insert.ufba.br)
[![Amlight Logo](/assets/img/amlight.png)](https://www.amlight.net)


# Agradecimentos

O projeto HackInSDN foi contemplado na Chamada Hackers do Bem, [chamada pública para Pesquisa e Desenvolvimento 2023](https://www.rnp.br/noticias/hackers-do-bem-resultado-da-chamada-publica-para-pesquisa-e-desenvolvimento-2023).

Leia mais sobre o [Projeto Hackers do Bem](https://hackersdobem.org.br).

# Mais informações

 - [Download, Instalação e Execução](./getting-started.html)
 - [Publicações](./publications.html)
 - [Tutoriais e documentações de uso](./technical-guides.html)
 - [Equipe de desenvolvimento](./hackinsdn-team.html)
 - [Código-fonte e Licenciamento](./source-code-license.html)

# Suporte

Encontrou um bug ou quer requisitar uma funcionalidade? [Reporte aqui!](https://github.com/hackinsdn/hackinsdn/issues)

Para manter contato com a equipe de desenvolvimento, escreva para **hackinsdn [@] ufba.br**.
