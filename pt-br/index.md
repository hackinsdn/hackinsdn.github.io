O HackInSDN tem como objetivo prover mecanismos de capacitação em temas de segurança cibernética utilizando ambientes de testbeds. Trata-se de um pacote de ferramentas que oferecerá um ambiente mais robusto e completo para capacitação em tópicos avançados de segurança, através da programabilidade de redes. Além dos sistemas de detecção de intrusão, o HackInSDN incorpora outras características como mecanismos de detecção de anomalias apoiados pela Inteligência Artificial, mecanismos de contenção e filtragem de ataques dinâmicos, ferramental para simulação de ataques, base de dados para inteligência de ameaças dentre outros.

HackInSDN está projetada para ser operada no ambiente distribuído de testbeds da RNP, beneficiando o sistema RNP com um serviço de capacitação em segurança cibernética que adotará a sua infraestrutura de testbeds.

## Infraestrutura programável em testbed para ensino de redes e segurança GT HACKINSDN

O processo de capacitação em segurança cibernética é bastante desafiador, dados os requisitos de conhecimentos em diferentes subáreas da computação. 
Por tais motivos, um amplo conjunto de metodologias e estratégias propõe a conciliação entre a teoria e a prática no ensino dos diversos temas existentes, 
na perspectiva de reduzir a curva de absorção de conceitos técnicos que, muitas vezes, são difíceis de serem materializados.

Nossa proposta tem como objetivo desenvolver a arquitetura HackInSDN, que visa a expandir a capacitação em temas de segurança cibernética em ambientes de testbeds. Trata-se de um pacote de ferramentas que oferecerá um ambiente mais robusto e completo para capacitação emtópicos avançados de segurança por meio da programabilidade de redes.

A HackInSDN abrangerá tópicos que vão além dos sistemas de detecção de intrusão, incorporando outras características — como mecanismos de detecção de novidades e anomalias apoiados pela Inteligência Artificial, outros de contenção e filtragem de ataques dinâmicos, ferramental para simulação de ataques, base de dados para
inteligência de ameaças, entre outros.

HackInSDN está projetada para ser operada no ambiente distribuído de testbeds da RNP, beneficiando o sistema RNP com um serviço de capacitação em segurança cibernética que adotará a sua infraestrutura de testbeds.

## HACKINSDN AGREGA UM SERVIÇO DE CAPACITAÇÃO EM SEGURANÇA CIBERNÉTICA AOS TESTBEDS DA RNP


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
