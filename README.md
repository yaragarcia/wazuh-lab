# wazuh-lab
Projeto de monitoramento de segurança com Wazuh (SIEM)

## Introdução
Este projeto tem como objetivo a implementação de um ambiente de monitoramento de segurança utilizando o Wazuh, atuando como uma solução SIEM (Security Information and Event Management).

O laboratório foi desenvolvido com foco na detecção de atividades maliciosas em um ambiente controlado, por meio da simulação de ataques comuns, como varredura de rede e tentativas de acesso não autorizado.

Os testes foram realizados a partir de uma máquina atacante (Kali Linux), permitindo avaliar a capacidade do Wazuh em coletar e analisar os eventos de segurança.

## Instalação
O ambiente foi implementado utilizando máquinas virtuais, simulando uma rede com múltiplos hosts.

O Wazuh foi instalado em uma máquina Ubuntu dedicada (192.168.0.112), atuando como servidor central da solução. 
Foi utilizada a instalação do tipo All-in-One, incluindo:

- Wazuh Manager  
- Wazuh Indexer  
- Wazuh Dashboard  

O servidor e o agente foram configurados em máquinas separadas, permitindo uma simulação mais próxima de um ambiente real.

Após a instalação, foi realizado o acesso ao dashboard e verificação dos serviços, confirmando o funcionamento do ambiente.

## Arquitetura do Ambiente
O ambiente foi estruturado em uma rede local virtualizada, composta por três máquinas com funções distintas: 

- Kali Linux: Responsável pela simulação de ataques. 

- Ubuntu (Wazuh Server) – 192.168.0.112: Máquina onde a stack do Wazuh foi instalada, responsável pela coleta, análise e visualização dos eventos de segurança. 

- Ubuntu (Wazuh Agent) – 192.168.0.113: Máquina monitorada pelo Wazuh, responsável pelo envio de logs e eventos para o servidor.

## Fluxograma
imagem

## Ataques Simulados
Com o ambiente devidamente configurado, foram realizados testes de segurança a partir da máquina Kali Linux, simulando atividades maliciosas no ambiente monitorado.

### Varredura de Rede (Nmap)

Foi executado um scan do tipo SYN utilizando o Nmap, técnica amplamente utilizada para reconhecimento discreto de serviços expostos.

```bash
nmap -sS 192.168.0.113
```

Esse tipo de varredura não completa o handshake TCP, tornando a detecção mais difícil e simulando um comportamento mais próximo de um atacante real.

imagem

### Ataque de Força Bruta (Hydra)

Foi realizado um ataque de força bruta contra o serviço SSH da máquina alvo utilizando Hydra, com múltiplas threads para aumentar a velocidade das tentativas.

```bash
hydra -l <usuario> -P <wordlist> -t <threads> ssh://192.168.0.113
```
Onde:

- `-l` define o usuário alvo  
- `-P` define a lista de senhas  
- `-t` define o número de threads simultâneas  


A utilização de múltiplas threads intensifica o volume de requisições, simulando ataques automatizados em larga escala.

Durante a execução, foram geradas múltiplas tentativas de autenticação inválida, criando eventos relevantes para análise, conforme evidenciado nos registros do Wazuh.

imagem

