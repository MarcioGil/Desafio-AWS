# ☁️ Desafio DIO: Gerenciamento de Instâncias EC2 na AWS

Este repositório documenta a experiência prática adquirida durante o laboratório de **Gerenciamento de Instâncias EC2 na AWS**, proposto pela Digital Innovation One (DIO). O objetivo principal é consolidar os conhecimentos sobre o serviço EC2, registrar os processos técnicos e servir como um guia de referência para futuros projetos em nuvem.

---

## 🎯 Atendimento aos Objetivos de Aprendizagem

Este projeto foi desenvolvido seguindo todos os requisitos do desafio, com foco em demonstrar proficiência em três pilares principais:

| Objetivo de Aprendizagem | Demonstração no Repositório |
| :--- | :--- |
| **Aplicar conceitos em ambiente prático** | Documentação completa do processo de provisionamento, conexão e ciclo de vida da EC2. |
| **Documentar processos técnicos** | Utilização de blocos de código (`ssh`), listas e tabelas para estruturar as anotações e insights. |
| **Utilizar o GitHub para documentação** | Repositório público, organizado com um `README.md` detalhado e, opcionalmente, uma estrutura de pastas (`/images`). |

---

## 📝 Anotações e Insights do Laboratório

### 🛠 Configuração do Ambiente EC2

| Item | Detalhes da Configuração |
| :--- | :--- |
| **AMI (Sistema Operacional)** | Ubuntu Server 22.04 LTS (Estável e ideal para testes). |
| **Tipo de Instância** | `t2.micro` (Selecionado por ser elegível ao **Free Tier**). |
| **Key Pair** | Chave SSH (`.pem`) criada e protegida localmente com o comando `chmod 400`. |
| **Security Group (Regras de Entrada)** | Porta **22** (SSH) para acesso de gerenciamento e porta **80** (HTTP) opcional para testes web. |

### 🔑 Acesso Seguro via SSH

A conexão com a instância EC2 foi realizada utilizando o terminal e o arquivo Key Pair gerado.

**Comando de Conexão:**

```bash
ssh -i "caminho/para/sua-chave.pem" ubuntu@SEU-IP-PUBLICO-AQUI

Boas Práticas de Segurança Observadas:

🔒 Restrição de IP: Para SSH (porta 22), evitei usar 0.0.0.0/0 (acesso liberado para qualquer IP), restringindo o acesso apenas ao meu endereço IP público para maior segurança.

🔑 Proteção da Chave: O arquivo .pem nunca deve ser compartilhado e suas permissões foram ajustadas para que apenas o proprietário possa lê-lo.

🔄 Ciclo de Vida e Gerenciamento
O gerenciamento da instância trouxe importantes insights sobre o seu ciclo de vida:

Stop vs. Terminate: Ao parar (stop) a instância, o IP público dinâmico é alterado. Ao encerrar (terminate), todos os dados do volume raiz são excluídos permanentemente (se não houver snapshot).

Custos: Instâncias paradas (stopped) não são cobradas pelo tempo de computação, mas o armazenamento EBS (Volume Raiz) continua gerando custos.

Elastic IP (EIP): É um recurso fundamental em produção, pois garante que o endereço IP público permaneça fixo, mesmo após uma operação de stop e start.

🏗 Arquitetura do Ambiente
A representação a seguir ilustra o ambiente provisionado, destacando os componentes essenciais:

Plaintext

┌──────────────────────────────────────────────────────────────┐
│ AWS Cloud                                                    │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ VPC (Rede Virtual)                                     │  │
│  │                                                        │  │
│  │  ┌──────────────────────────────────────────────────┐  │  │
│  │  │ Subnet Pública                                   │  │  │
│  │  │                                                  │  │  │
│  │  │  ┌────────────────────────────────────────────┐  │  │  │
│  │  │  │ Instância EC2                              │  │  │  │
│  │  │  │ - Ubuntu Server 22.04                      │  │  │  │
│  │  │  │ - Tipo t2.micro                            │  │  │  │
│  │  │  │ - Security Group (22/80)                   │  │  │  │
│  │  │  └────────────────────────────────────────────┘  │  │  │
│  │  │                                                  │  │  │
│  │  └──────────────────────────────────────────────────┘  │  │
│  │                                                        │  │
│  └────────────────────────────────────────────────────────┘  │
│                                                              │
│ Internet <---- (Acesso via Key Pair) ----> Instância EC2      │
└──────────────────────────────────────────────────────────────┘
📂 Estrutura do Repositório (Entrega)
A estrutura de arquivos sugerida para atender o desafio é:

.
├── README.md              # Documentação detalhada do projeto (Este arquivo).
├── images/                # (Opcional) Capturas de tela relevantes da prática.
│   ├── ec2-dashboard.png
│   └── ssh-connection-log.png
└── arquivos-adicionais/   # (Opcional) Scripts ou configurações auxiliares.
    └── setup-web.sh       # Exemplo de script de inicialização para webserver.
🔗 Recursos Úteis e Referências
Gerenciando EC2 instâncias da Amazon - Documentação AWS

GitHub Quick Start - Repositório com Link para Aulas de Git e GitHub

Guia Completo de Markdown no GitHub

👤 Autor
Márcio Gil

Perfil DIO: [https://web.dio.me/users/marciopaivagil?tab=achievements]

LinkedIn: [linkedin.com/in/márcio-gil-1b7669309]

Este projeto é parte da minha jornada de aprendizado em Computação em Nuvem e Desenvolvimento Profissional, através das formações oferecidas pela DIO.