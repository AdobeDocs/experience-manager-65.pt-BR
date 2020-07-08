---
title: Considerações e requisitos de rede dos ativos
description: Discute as considerações de rede ao projetar uma implantação do Adobe Experience Manager Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---


# Considerações sobre a rede de ativos {#assets-network-considerations}

Compreender sua rede é tão importante quanto entender os ativos Adobe Experience Manager. A rede pode afetar as experiências de upload, download e usuário. O diagrama da topologia de rede ajuda a identificar pontos de estrangulamento e áreas sub-otimizadas na rede que você deve corrigir para melhorar o desempenho da rede e a experiência do usuário.

Certifique-se de incluir o seguinte no diagrama de rede:

* Conectividade do dispositivo cliente (por exemplo, computador, dispositivo móvel e tablet) à rede.
* Topologia da rede corporativa.
* Faça upload para a Internet a partir da rede corporativa e do ambiente Experience Manager.
* Topologia do ambiente Experience Manager.
* Defina consumidores simultâneos da interface de rede Experience Manager.
* workflows definidos da implantação do Experience Manager.

## Conectividade do dispositivo cliente à rede corporativa {#connectivity-from-the-client-device-to-the-corporate-network}

Comece com a diagramação da conectividade entre os dispositivos cliente individuais e a rede corporativa. Neste estágio, identifique recursos compartilhados, como conexões WiFi, onde vários usuários acessam o mesmo ponto ou switch ethernet para fazer upload e download de ativos.

![chlimage_1-353](assets/chlimage_1-353.png)

Os dispositivos cliente se conectam à rede corporativa de várias maneiras, como WiFi compartilhado, ethernet a um switch compartilhado e VPN. Identificar e entender pontos de interrupção nesta rede é importante para o planejamento de ativos e para modificar a rede.

Na parte superior esquerda do diagrama, três dispositivos são descritos como compartilhando um ponto de acesso WiFi de 48 Mbps. Se todos os dispositivos forem carregados simultaneamente, a largura de banda da rede WiFi será compartilhada entre os dispositivos. Comparado ao sistema como um todo, um usuário pode encontrar um ponto de estrangulamento diferente para os três clientes em relação a esse canal dividido.

É um desafio medir a velocidade real de uma rede WiFi, pois um dispositivo lento pode afetar outros clientes no ponto de acesso. Se você planeja usar o WiFi para interações com ativos, execute um teste de velocidade de vários clientes simultaneamente para avaliar a throughput.

A parte inferior esquerda do diagrama descreve dois dispositivos conectados à rede corporativa por meio de canais independentes. Portanto, cada dispositivo pode utilizar uma velocidade mínima de 10 Mbps e 100 Mbps.

O computador exibido à direita tem um valor upstream limitado para a rede corporativa através de uma VPN com velocidade de 1 Mbps. A experiência do usuário para a conexão de 1Mbps é muito diferente da experiência do usuário na conexão de 1Gbps. Dependendo do tamanho dos ativos com os quais os usuários interagem, o uplink VPN pode ser inadequado para a tarefa.

## Topologia da rede corporativa {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

O diagrama exibe velocidades de uplink mais altas dentro da rede corporativa do que o geralmente é usado. Esses tubos são recursos compartilhados. Se for esperado que o switch compartilhado trate de 50 clientes, ele poderá ser um ponto de bloqueio. No diagrama inicial, apenas dois computadores compartilham a conexão específica.

## Faça upload para a Internet a partir da rede corporativa e do ambiente Experience Manager {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

É importante considerar fatores desconhecidos na Internet e na conexão VPC, pois a largura de banda na Internet pode ser prejudicada devido ao pico de carga ou a interrupções do provedor em grande escala. Em geral, a conectividade com a Internet é confiável. No entanto, pode por vezes introduzir pontos de estrangulamento.

No uplink de uma rede corporativa para a Internet, pode haver outros serviços usando a largura de banda. É importante entender quanto da largura de banda pode ser dedicada ou priorizada aos Ativos. Por exemplo, se um link de 1 Gbps já estiver em uma utilização de 80%, você só poderá alocar um máximo de 20% da largura de banda para os Ativos de Experience Manager.

firewalls e proxies corporativos também podem moldar a largura de banda de várias maneiras diferentes. Esse tipo de dispositivo pode priorizar a largura de banda usando qualidade de serviço, limitações de largura de banda por usuário ou limitações de taxa de bits por host. Esses são pontos de interrupção importantes a serem examinados, pois podem afetar significativamente a experiência do usuário do Assets.

Neste exemplo, a empresa tem um uplink de 10 Gbps. Deve ser grande o suficiente para vários clientes. Além disso, o firewall impõe um limite de taxa de host de 10 Mbps. Essa limitação pode, potencialmente, limitar o tráfego para um único host a 10 Mbps, mesmo que o uplink para a Internet seja de 10 Gbps.

Este é o menor ponto de estrangulamento orientado para o cliente. No entanto, você pode avaliar se há uma alteração ou configuração de uma lista de permissões com o grupo de operações de rede responsável por esse firewall.

A partir de exemplos de diagramas, você pode concluir que seis dispositivos compartilham um canal conceitual de 10 Mbps. Dependendo do tamanho dos ativos alavancados, isso pode ser inadequado para atender às expectativas do usuário.

## Topologia do ambiente Experience Manager {#topology-of-the-aem-environment}

![chlimage_1-354](assets/chlimage_1-356.png)

A concepção da topologia do ambiente exige um conhecimento detalhado da configuração do sistema e de como a rede é conectada no ambiente do usuário.

O cenário de amostra inclui um farm de publicação com cinco servidores, uma loja binária S3 e Dynamic Media configurados.

O dispatcher compartilha sua conexão de 100 Mbps com duas entidades, o mundo externo e a implantação do Experience Manager. Para operações simultâneas de upload e download, você deve dividir esse número por dois. O armazenamento externo conectado usa uma conexão separada.

A implantação do Experience Manager compartilha sua conexão de 1Gbps com vários serviços. Do ponto de vista da topologia da rede, equivale a compartilhar um único canal com diferentes serviços.

Revisando a rede do dispositivo cliente para a implantação do Experience Manager, o menor ponto de estrangulamento parece ser a limitação do firewall corporativo de 10 Mbit. Você pode usar esses valores na calculadora de dimensionamento no Guia [de dimensionamento de](assets-sizing-guide.md) ativos para determinar a experiência do usuário.

## workflows definidos da implantação de Experience Manager {#defined-workflows-of-the-aem-deployment}

Ao considerar o desempenho da rede, pode ser importante considerar os workflows e a publicação que ocorrerão no sistema. Além disso, o S3 ou outro armazenamento conectado à rede que você usa e as solicitações de E/S consomem largura de banda da rede. Portanto, mesmo em uma rede totalmente otimizada, o desempenho pode ser limitado pela E/S do disco.

Para simplificar os processos de ingestão de ativos (especialmente ao fazer upload de um grande número de ativos), explore os workflows de ativos e saiba mais sobre a configuração deles.

Ao avaliar a topologia interna do fluxo de trabalho, você deve analisar o seguinte:

* Procedimentos para escrever um ativo
* Workflows/eventos que são acionados quando ativos/metadados são modificados
* Procedimentos que leem um ativo

Estes são alguns itens a serem considerados:

* Leitura/gravação de metadados XMP
* ativação automática e replicação
* Aplicação de marca d&#39;água
* Inclusão/extração de página
* workflows sobrepostos.

Este é um exemplo de cliente para a definição de um fluxo de trabalho de ativos.

![chlimage_1-357](assets/chlimage_1-357.png)
