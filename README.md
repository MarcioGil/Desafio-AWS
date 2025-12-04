# Desafio DIO: Gerenciamento de Instâncias EC2 na AWS

## 🚀 Descrição do Desafio

Este repositório documenta a experiência e os conhecimentos adquiridos durante o laboratório prático de gerenciamento de instâncias EC2 (Elastic Compute Cloud) na Amazon Web Services (AWS), conforme proposto pelo desafio da DIO. O objetivo principal é consolidar o aprendizado, aplicar os conceitos abordados nas aulas e criar um material de apoio estruturado para estudos futuros.

## 🎯 Objetivos de Aprendizagem

Ao concluir este desafio, os seguintes objetivos foram alcançados:

1.  **Aplicar os conceitos aprendidos** em um ambiente prático de nuvem AWS.
2.  **Documentar processos técnicos** de forma clara e estruturada, utilizando o Markdown.
3.  **Utilizar o GitHub** como ferramenta para compartilhamento e versionamento de documentação técnica.

## 💡 Conceitos Chave de Gerenciamento EC2

O gerenciamento eficaz de instâncias EC2 envolve a compreensão de vários componentes e práticas essenciais:

| Conceito | Descrição |
| :--- | :--- |
| **Instância EC2** | Servidor virtual (máquina virtual) na Nuvem AWS que fornece capacidade de computação escalável. O tipo de instância define o hardware (CPU, memória, armazenamento, rede). |
| **Amazon Machine Image (AMI)** | Um modelo que contém a configuração de software (sistema operacional, servidor de aplicativos e aplicativos) necessária para iniciar sua instância. |
| **Pares de Chaves (Key Pairs)** | Credenciais de segurança compostas por uma chave pública (armazenada na AWS) e uma chave privada (mantida pelo usuário), usadas para provar sua identidade ao se conectar à instância via SSH. |
| **Grupos de Segurança (Security Groups)** | Atuam como um firewall virtual para controlar o tráfego de entrada e saída da instância. São essenciais para garantir que apenas o tráfego autorizado possa acessar a instância. |
| **Elastic IP (EIP)** | Um endereço IP público estático projetado para computação em nuvem dinâmica. Permite que você mascare a falha de uma instância remapeando o endereço IP para outra instância em sua conta. |
| **Ciclo de Vida da Instância** | O gerenciamento das instâncias envolve estados como `pending` (pendente), `running` (em execução), `stopping` (parando), `stopped` (parada) e `terminated` (encerrada). |
| **AWS Systems Manager** | Serviço que ajuda a visualizar e controlar sua infraestrutura na AWS, facilitando a automação de tarefas operacionais e o gerenciamento de instâncias, mesmo sem acesso SSH direto. |

## 📝 Anotações e Insights da Prática

Esta seção é dedicada às anotações detalhadas e aos insights adquiridos durante a prática de gerenciamento de instâncias EC2 na AWS.

### 1. Lançamento e Configuração Inicial

*   **Escolha da AMI:** Foi utilizada a **Ubuntu Server 22.04 LTS (HVM), SSD Volume Type**. Esta AMI foi escolhida por ser uma distribuição Linux amplamente utilizada e familiar para desenvolvimento e testes, além de estar disponível no Free Tier.
*   **Tipo de Instância:** O tipo de instância selecionado foi **t2.micro**. Esta é a opção mais básica e gratuita (Free Tier), ideal para o propósito de aprendizado e testes do desafio, oferecendo recursos suficientes para a prática de gerenciamento.
*   **Criação do Par de Chaves:** O par de chaves foi criado no console da AWS e o arquivo de chave privada (`.pem`) foi baixado e protegido. Este arquivo é essencial para a autenticação segura via SSH, garantindo que apenas o usuário com a chave privada correspondente possa acessar a instância.

### 2. Conexão e Gerenciamento

*   **Comando de Conexão SSH:** Para acessar a instância de forma segura, o seguinte comando SSH foi utilizado, após garantir que o arquivo `.pem` tivesse as permissões corretas (`chmod 400`):
    ```bash
    ssh -i "nome-do-par-de-chaves.pem" ubuntu@seu-ip-publico
    ```
*   **Configuração de Segurança:** Foi criado um **Grupo de Segurança (Security Group)** permitindo tráfego de entrada (Inbound) na porta **22 (SSH)** a partir do meu endereço IP (ou de qualquer lugar, `0.0.0.0/0`, para fins de teste, com a ressalva de que o ideal é restringir ao máximo). Opcionalmente, a porta **80 (HTTP)** foi aberta para simular a hospedagem de um serviço web simples.

### 3. Gerenciamento do Ciclo de Vida

*   **Ações Práticas:** Foram executadas as ações de `Stop` (Parar), `Start` (Iniciar) e `Terminate` (Encerrar). O insight principal foi observar que ao `Parar` e `Iniciar` a instância, o **IP Público dinâmico é alterado**, o que reforça a necessidade de um **Elastic IP (EIP)** para ambientes de produção que precisam de um endereço IP fixo.

### 4. Insights Adicionais

*   **Segurança é Primordial:** O uso de **Security Groups** e a gestão correta dos **Pares de Chaves** são as primeiras linhas de defesa. Nunca se deve expor a chave privada ou abrir portas desnecessárias.
*   **Otimização de Custos:** É crucial **encerrar (`Terminate`)** instâncias que não estão em uso para evitar cobranças desnecessárias, especialmente fora do Free Tier. O estado `Stopped` (Parado) ainda pode gerar custos de armazenamento (EBS).
*   **Automação:** Para gerenciamento em escala, o **AWS Systems Manager** é uma ferramenta poderosa que permite executar comandos e gerenciar instâncias sem a necessidade de conexão SSH direta.

## 📂 Estrutura do Repositório

*   `README.md`: Este arquivo, contendo a documentação completa do desafio.
*   `/images`: Pasta opcional para armazenar capturas de tela relevantes da console AWS ou da linha de comando.
*   `[Outros arquivos relevantes]`: Arquivos de configuração, scripts ou diagramas que complementam a documentação.

## 🔗 Recursos Úteis

*   **Documentação Oficial AWS:**
    *   [Gerenciando EC2 instâncias da Amazon - Documentação AWS](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
*   **Materiais Complementares sobre GitHub e Markdown:**
    *   [GitHub Quick Start](https://docs.github.com/pt/get-started/quickstart)
    *   [GitBook: Formação GitHub Certification](https://www.gitbook.com/book/github/certification/details)
    *   [Documentação do GitHub, Guia completo para uso do GitHub](https://docs.github.com/pt)
    *   [GitHub Markdown, Guia específico para Markdown no GitHub](https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
