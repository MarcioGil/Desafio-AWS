Desafio DIO: Gerenciamento de Instâncias EC2 na AWS

Este repositório reúne toda a documentação produzida durante o laboratório de Gerenciamento de Instâncias EC2 na AWS, proposto pela DIO.
O objetivo deste material é consolidar os conceitos estudados, registrar a experiência prática adquirida e servir como referência para futuros projetos em nuvem.

🚀 Descrição Geral

Durante o desafio, foram aplicados na prática os principais temas abordados nas aulas, incluindo o provisionamento, configuração, conexão e gerenciamento completo de uma instância EC2 na AWS.
Este repositório funciona como um guia estudantil e um portfólio técnico organizado, demonstrando domínio dos conceitos fundamentais de computação em nuvem.

🎯 Objetivos de Aprendizagem Alcançados

Aplicar, na prática, os conceitos essenciais do serviço EC2 da AWS.

Documentar processos técnicos de forma clara, objetiva e estruturada.

Utilizar o GitHub como ferramenta de versionamento e documentação profissional.

Compreender a importância de segurança, custos e automação no gerenciamento de instâncias.

🏗️ Arquitetura do Ambiente (Como solicitado na aula)

Abaixo está a representação da arquitetura utilizada durante o laboratório, conforme o padrão ensinado:

┌──────────────────────────────────────────────────────────────┐
│                        AWS Cloud                             │
│                                                              │
│   ┌────────────────────────────────────────────────────────┐  │
│   │                    VPC (Rede Virtual)                  │  │
│   │                                                      │ │  │
│   │  ┌──────────────────────────────────────────────────┐ │  │
│   │  │                Subnet Pública                    │ │  │
│   │  │                                                  │ │  │
│   │  │  ┌────────────────────────────────────────────┐ │ │  │
│   │  │  │              Instância EC2                 │ │ │  │
│   │  │  │  - Ubuntu Server 22.04 (AMI)               │ │ │  │
│   │  │  │  - Tipo t2.micro (Free Tier)               │ │ │  │
│   │  │  │  - Chave SSH (.pem)                        │ │ │  │
│   │  │  │  - Security Group: Porta 22 e opcional 80  │ │ │  │
│   │  │  └────────────────────────────────────────────┘ │ │  │
│   │  │                                                  │ │  │
│   │  └──────────────────────────────────────────────────┘ │  │
│   │                                                      │ │  │
│   └────────────────────────────────────────────────────────┘  │
│                                                              │
│  Internet ←──── Elastic IP (opcional) ────→ Instância EC2    │
└──────────────────────────────────────────────────────────────┘


Resumo da Arquitetura:

Uma instância EC2 Ubuntu 22.04 LTS dentro de uma Subnet Pública.

Acesso configurado via SSH usando par de chaves.

Security Group controlando portas essenciais (22 e, opcionalmente, 80).

Conexão via IP Público ou Elastic IP, dependendo da necessidade.

💡 Conceitos-Chave do Gerenciamento EC2
| Conceito | Descrição |

|----------|------------|
| Instância EC2 | Servidor virtual escalável na nuvem da AWS, configurável conforme a necessidade. |
| AMI | Imagem que contém o sistema operacional e as configurações base da instância. |
| Key Pair | Par de chaves usado para autenticação segura via SSH. |
| Security Group | Firewall virtual que controla tráfego de entrada e saída. |
| Elastic IP | Endereço IP público estático ideal para ambientes de produção. |
| Ciclo de Vida | Estados: pending → running → stopping → stopped → terminated. |
| AWS Systems Manager | Ferramenta para automação, análise e gestão centralizada de servidores. |

📝 Anotações e Insights da Prática
1. Lançamento e Configuração Inicial

AMI usada: Ubuntu Server 22.04 LTS – robusta, estável e compatível com Free Tier.

Tipo de instância: t2.micro – suficiente para testes técnicos.

Par de chaves: Criado via console e armazenado com segurança; permissões ajustadas com chmod 400.

2. Conexão e Acesso Seguro

Comando utilizado após o ajuste de permissões da chave:

ssh -i "nome-do-par.pem" ubuntu@SEU-IP-PUBLICO

Configurações de segurança:

Porta 22 (SSH) liberada apenas para meu IP — quando possível.

Porta 80 (HTTP) aberta opcionalmente para testes web.

Observação: exposições amplas (0.0.0.0/0) devem ser evitadas fora do ambiente educacional.

3. Ciclo de Vida da Instância

Foi possível observar, na prática, como cada ação afeta a infraestrutura:

Stop → Start: O IP público é alterado (caso não haja Elastic IP).

Terminate: A instância e o volume raiz são destruídos permanentemente.

Insight: Em ambientes críticos, Elastic IP é obrigatório para evitar perda de endpoint.

4. Insights Adicionais Importantes
🔒 Segurança

Nunca compartilhar o arquivo .pem.

Evitar portas desnecessárias.

Security Groups devem seguir o princípio de menor privilégio.

💰 Custos

Instâncias paradas ainda geram custo através do EBS.

Instâncias esquecidas running fora do Free Tier podem gerar cobranças rápidas.

🤖 Automação

O AWS Systems Manager possibilita executar comandos sem SSH.

Excelente para ambientes corporativos e multi-instâncias.

📂 Estrutura do Repositório
/
├── README.md
├── images/
│   ├── ec2-dashboard.png
│   ├── ssh-connection.png
│   └── architecture-diagram.png
└── arquivos-adicionais/
    └── (scripts, configs, outputs)

🔗 Recursos Úteis
Documentação Oficial AWS

Gerenciamento de instâncias EC2 – AWS Docs

GitHub & Markdown

GitHub Quick Start

Formação GitHub Certification (GitBook)

Guia Completo do GitHub

Guia de Markdown do GitHub

Se quiser incluir sua apresentação pessoal no final do README, aqui está a versão pronta:

👤 Autor

Márcio Gil
Embaixador do DIO Campus Expert & Estudante de Engenharia de Software
Apaixonado por tecnologia, aprendizado contínuo e construção de soluções que geram impacto social.
Este repositório é parte da minha jornada em computação em nuvem e desenvolvimento profissional.