# Teste-Hogwarts — O Portão de Hogwarts

## 1. Sobre o projeto

**O Portão de Hogwarts** é um jogo educativo desenvolvido para facilitar o aprendizado de conceitos de segurança de redes, utilizando analogias inspiradas no universo de Harry Potter.

A atividade tem como objetivo ajudar os alunos a compreender como funcionam as Listas de Controle de Acesso (ACLs), os firewalls e o Zone-Based Policy Firewall (ZPF), relacionando esses mecanismos a situações do cotidiano de Hogwarts.

Durante o jogo, cada participante assume o papel de Argus Filch, responsável por controlar a entrada no castelo. Para decidir quem pode passar pelo portão, o jogador precisa analisar as regras de segurança e as informações de cada visitante.

A proposta é transformar conceitos técnicos em decisões práticas, estimulando o raciocínio lógico, a interpretação de regras e a compreensão de como os dispositivos de segurança protegem uma rede.

## 2. Como funciona a analogia com Hogwarts?

Imagine que Hogwarts seja uma rede de computadores. O castelo possui áreas protegidas, visitantes, funcionários e informações que não podem ser acessadas livremente por qualquer pessoa.

O portão representa um ponto de controle de acesso. Cada visitante tenta entrar, mas sua entrada depende das regras estabelecidas pelo responsável pela segurança.

No jogo, os elementos representam:

- **Hogwarts:** a rede que precisa ser protegida.
- **Portão do castelo:** o ponto de entrada e controle do tráfego.
- **Argus Filch:** o responsável por verificar as regras e tomar decisões de acesso.
- **Alunos, professores e visitantes:** os dispositivos, usuários ou origens de tráfego que tentam acessar a rede.
- **Regras de segurança:** as políticas que determinam quais acessos são permitidos ou negados.
- **Áreas restritas do castelo:** os recursos e serviços que exigem controles específicos.
- **Visitantes suspeitos ou não autorizados:** conexões que não atendem aos critérios definidos pela política de segurança.

A analogia tem uma finalidade didática: na prática, os equipamentos de rede processam pacotes e conexões, e não pessoas. Cada regra deve ser interpretada de acordo com os campos e as condições que ela realmente verifica.

## 3. Conceitos de segurança de redes

### 3.1. ACL — Access Control List (Lista de Controle de Acesso)

Uma ACL é uma lista de regras utilizada para permitir ou negar tráfego de rede com base em critérios específicos.

Esses critérios podem incluir endereços IP de origem e destino, protocolos e portas, dependendo do tipo de ACL.

**Analogia com Hogwarts:** Filch possui uma lista de regras na qual verifica quem pode passar pelo portão. Um visitante pode ser autorizado por atender aos critérios estabelecidos, enquanto outro pode ter a entrada negada.

Por exemplo:

- Alunos autorizados podem entrar no castelo.
- Visitantes não autorizados não podem entrar.
- Determinadas conexões podem acessar apenas serviços específicos.

No contexto de redes, uma regra poderia permitir que um computador acessasse um servidor web, mas negar o acesso a outro serviço.

**Principais conceitos:**

- **Permit:** permite o tráfego que corresponde à regra.
- **Deny:** bloqueia o tráfego que corresponde à regra.
- **Ordem das regras:** em ACLs tradicionais Cisco, as entradas são verificadas sequencialmente, e a primeira correspondência determina a decisão.
- **Critérios de correspondência:** definem quais pacotes são avaliados por cada regra.
- **Negação implícita:** nas ACLs Cisco tradicionais, existe uma negação implícita ao final da lista, caso nenhuma entrada anterior corresponda ao pacote.

Isso significa que a ausência de uma regra permitindo determinado tráfego não deve ser interpretada automaticamente como autorização.

### 3.2. Firewall

Um firewall é um mecanismo de segurança que controla o tráfego de rede conforme uma política definida. Ele pode permitir, bloquear ou, conforme seus recursos, inspecionar conexões e pacotes.

**Analogia com Hogwarts:** O portão mágico do castelo funciona como uma barreira de segurança. Não basta alguém querer entrar: o acesso precisa respeitar as regras de proteção.

Em uma rede, o firewall pode controlar, por exemplo:

- Conexões entre a rede interna e a internet.
- Acesso a servidores e aplicações.
- Tráfego entre diferentes segmentos de rede.
- Conexões que atendem ou não à política de segurança.

Existem diferentes tipos e implementações de firewall. Alguns filtram principalmente informações dos pacotes; outros também acompanham o estado das conexões e realizam inspeções mais avançadas.

**Importante:** um firewall não substitui todas as outras medidas de segurança. Ele faz parte de uma estratégia de proteção que pode incluir autenticação, atualização de sistemas, monitoramento e outros controles.

### 3.3. ZPF — Zone-Based Policy Firewall

O Zone-Based Policy Firewall é um recurso de firewall utilizado em roteadores Cisco que organiza as interfaces de rede em zonas e define políticas para controlar o tráfego entre elas.

Em vez de tratar cada interface de maneira isolada, o ZPF permite estabelecer políticas de segurança de acordo com as zonas envolvidas e o sentido do tráfego.

**Analogia com Hogwarts:** imagine que o castelo esteja dividido em áreas:

- Pátio externo.
- Salões comuns.
- Biblioteca restrita.
- Sala de artefatos mágicos.

Cada área possui regras próprias. Uma pessoa que pode circular pelo salão principal não necessariamente tem autorização para entrar na biblioteca restrita ou na sala de artefatos.

Em uma rede, essas áreas podem representar a internet, a rede interna, uma rede de servidores ou uma zona de acesso restrito.

**Principais conceitos:**

- **Zona de segurança:** agrupamento lógico de interfaces que compartilham uma classificação de segurança.
- **Zone pair:** combinação de uma zona de origem e uma zona de destino para a qual se aplica uma política.
- **Class map:** identifica o tráfego que corresponde a determinados critérios.
- **Policy map:** define a ação aplicada ao tráfego identificado.
- **Inspect:** permite inspecionar o tráfego e acompanhar o estado das conexões, conforme a política configurada.
- **Pass:** permite o encaminhamento do tráfego correspondente, sem a inspeção com estado proporcionada por `inspect`.
- **Drop:** descarta o tráfego correspondente.
- **Política entre zonas:** determina como o tráfego pode circular de uma zona para outra.

No ZPF tradicional da Cisco, o tráfego entre zonas diferentes é bloqueado por padrão quando não existe uma política que o autorize. O tráfego dentro da mesma zona e o tráfego destinado ao próprio roteador possuem tratamentos específicos.

Dessa forma, o ZPF permite criar uma política de segurança mais organizada para diferentes partes de uma rede.

## 4. Qual é a diferença entre ACL, firewall e ZPF?

Embora estejam relacionados, esses conceitos não são sinônimos.

**ACL:** funciona como uma lista ordenada de critérios e decisões de permissão ou negação. Pode ser utilizada em diferentes funções, inclusive no controle de tráfego.

**Firewall:** é um mecanismo de segurança que aplica políticas para controlar o tráfego entre redes, sistemas ou zonas. Pode utilizar ACLs e outros recursos para executar esse controle.

**ZPF:** é uma abordagem de firewall baseada em zonas, na qual políticas específicas controlam o tráfego entre elas.

Na analogia:

- A ACL é a lista de regras que Filch consulta.
- O firewall é o sistema de segurança que controla o acesso ao castelo.
- O ZPF é a organização da segurança por áreas, estabelecendo quais deslocamentos entre elas são permitidos.

## 5. Como jogar?

1. Abra o jogo pelo GitHub Pages ou pelo arquivo `index.html` no navegador.
2. Leia as informações do visitante ou da tentativa de acesso apresentada.
3. Analise a lista de regras disponível.
4. Verifique quais critérios correspondem à situação apresentada.
5. Decida se o acesso deve ser permitido ou negado.
6. Confira o resultado e utilize a explicação para entender a lógica da decisão.

O objetivo não é apenas acertar a resposta, mas compreender por que determinada regra permite ou bloqueia um acesso.

## 6. Objetivos de aprendizagem

Ao final da atividade, espera-se que os alunos consigam:

- Compreender a finalidade das ACLs na segurança de redes.
- Identificar regras de permissão e negação.
- Entender a importância da ordem das entradas em ACLs tradicionais.
- Reconhecer a função de um firewall no controle do tráfego.
- Diferenciar filtragem por regras de políticas de firewall baseadas em zonas.
- Compreender como zonas e políticas de tráfego são utilizadas no ZPF.
- Desenvolver raciocínio lógico para analisar situações de acesso.
- Relacionar conceitos teóricos a situações práticas de segurança de redes.

## 7. Considerações finais

O projeto **Teste-Hogwarts — O Portão de Hogwarts** utiliza uma abordagem lúdica para tornar o estudo da segurança de redes mais acessível e interativo.

Ao assumir o papel de Filch, o aluno precisa interpretar regras, avaliar condições e tomar decisões de acesso, exercitando habilidades importantes para a administração e a proteção de redes.

A atividade demonstra que a segurança não depende apenas de bloquear tudo o que parece suspeito, mas de estabelecer políticas coerentes, compreender o tráfego e permitir somente as comunicações compatíveis com as necessidades e os requisitos de segurança da rede.
