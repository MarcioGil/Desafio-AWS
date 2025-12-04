Desafio DIO: Gerenciamento de Instâncias EC2 na AWS

Este repositório reúne toda a documentação produzida durante o laboratório de Gerenciamento de Instâncias EC2 na AWS, proposto pela DIO. O objetivo deste material é consolidar os conceitos estudados, registrar a experiência prática adquirida e servir como referência para futuros projetos em nuvem.

🚀 Descrição Geral

Durante o desafio, foram aplicados na prática os principais temas abordados nas aulas, incluindo o provisionamento, configuração, conexão e gerenciamento completo de uma instância EC2 na AWS. Este repositório funciona como um guia estudantil e um portfólio técnico organizado, demonstrando domínio dos conceitos fundamentais de computação em nuvem.

🎯 Objetivos de Aprendizagem Alcançados

Aplicar, na prática, os conceitos essenciais do serviço EC2 da AWS.

Documentar processos técnicos de forma clara, objetiva e estruturada.

Utilizar o GitHub como ferramenta de versionamento e documentação profissional.

Compreender a importância de segurança, custos e automação no gerenciamento de instâncias.

🏗 Arquitetura do Ambiente (como solicitado na aula)

Abaixo está a representação da arquitetura utilizada durante o laboratório. O bloco está corretamente delimitado por três crases para evitar problemas na renderização do GitHub:

┌──────────────────────────────────────────────────────────────┐
│                        AWS Cloud                             │
│                                                              │
│   ┌────────────────────────────────────────────────────────┐ │
│   │                    VPC (Rede Virtual)                  │ │
│   │                                                      │ │
│   │  ┌──────────────────────────────────────────────────┐ │ │
│   │  │                Subnet Pública                    │ │ │
│   │  │                                                  │ │ │
│   │  │  ┌────────────────────────────────────────────┐ │ │ │
│   │  │  │              Instância EC2                 │ │ │ │
│   │  │  │  - Ubuntu Server 22.04 (AMI)               │ │ │ │
│   │  │  │  - Tipo t2.micro (Free Tier)               │ │ │ │
│   │  │  │  - Chave SSH (.pem)                        │ │ │ │
│   │  │  │  - Security Group: Porta 22 e opcional 80  │ │ │ │
│   │  │  └────────────────────────────────────────────┘ │ │ │
│   │  │                                                  │ │ │
│   │  └──────────────────────────────────────────────────┘ │ │
│   │                                                      │ │
│   └────────────────────────────────────────────────────────┘ │
│                                                              │
│  Internet ←──── Elastic IP (opcional) ────→ Instância EC2    │
└──────────────────────────────────────────────────────────────┘


Resumo da Arquitetura:

Instância EC2 Ubuntu 22.04 LTS em Subnet Pública.

Acesso via SSH com Key Pair.

Security Group permitindo apenas o tráfego necessário (porta 22 e, opcionalmente, porta 80).

Elastic IP opcional para manter endpoint fixo em ambientes de produção.

💡 Conceitos-Chave do Gerenciamento EC2
Conceito	Descrição
Instância EC2	Servidor virtual escalável na nuvem da AWS, configurável conforme a necessidade.
AMI	Imagem que contém sistema operacional e configuração base da instância.
Key Pair	Par de chaves usado para autenticação segura via SSH.
Security Group	Firewall virtual que controla tráfego de entrada e saída.
Elastic IP	Endereço IP público estático ideal para ambientes de produção.
Ciclo de Vida	Estados: pending → running → stopping → stopped → terminated.
AWS Systems Manager	Ferramenta para automação, análise e gestão centralizada de servidores.
📝 Anotações e Insights da Prática
1. Lançamento e Configuração Inicial

AMI utilizada: Ubuntu Server 22.04 LTS — estável e compatível com Free Tier.

Tipo de instância: t2.micro — suficiente para testes técnicos.

Par de chaves: criado via Console AWS; arquivo .pem protegido e com permissões ajustadas (chmod 400).

2. Conexão e Acesso Seguro

Use o comando abaixo (bloco de código corretamente delimitado):

ssh -i "nome-do-par.pem" ubuntu@SEU-IP-PUBLICO


Boas práticas de segurança:

Liberar porta 22 apenas para IPs confiáveis.

Evitar 0.0.0.0/0 para SSH em ambientes de produção.

Abrir porta 80 somente quando necessário para testes web.

3. Ciclo de Vida da Instância

Stop → Start: o IP público muda se não houver Elastic IP.

Terminate: remove instância e dados do volume raiz (se não houver backup/snapshot).

Insight: para ambientes críticos, utilize Elastic IPs e snapshots/AMIs para garantir disponibilidade e recuperação.

4. Insights Adicionais

Segurança: nunca compartilhe o arquivo .pem. Security Groups devem seguir o princípio do menor privilégio.

Custos: instâncias paradas ainda geram custo de armazenamento (EBS). Evite deixar instâncias running desnecessariamente.

Automação: o AWS Systems Manager permite executar comandos e administrar instâncias sem acessar via SSH — ideal para escala.

📂 Estrutura Sugerida do Repositório
/
├── README.md
├── images/
│   ├── ec2-dashboard.png
│   ├── ssh-connection.png
│   └── architecture-diagram.png
└── arquivos-adicionais/
    ├── scripts/
    │   └── setup.sh
    └── configs/
        └── security-group.json

🔗 Recursos Úteis

Documentação AWS: Gerenciamento de instâncias EC2 – AWS Docs

GitHub & Markdown: GitHub Quick Start, Guia de Markdown do GitHub, Formação GitHub Certification (GitBook)

(Substitua os nomes dos recursos por links reais no seu README, se desejar.)

👤 Autor

Márcio Gil
Embaixador do DIO Campus Expert & Estudante de Engenharia de Software
Apaixonado por tecnologia, aprendizado contínuo e construção de soluções que geram impacto social. Este repositório é parte da minha jornada em computação em nuvem e desenvolvimento profissional.