---
title: Considerações e requisitos de rede
description: Discute as considerações de rede ao projetar um [!DNL Adobe Experience Manager Assets] implantação.
contentOwner: AG
role: Architect, Admin
feature: Developer Tools
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# [!DNL Assets] considerações de rede {#assets-network-considerations}

Compreender a sua rede é tão importante quanto entender [!DNL Adobe Experience Manager Assets]. A rede pode afetar o upload, o download e as experiências do usuário. O diagramamento da topologia de rede ajuda a identificar pontos de bloqueio e áreas subotimizadas na rede que você deve corrigir para melhorar o desempenho da rede e a experiência do usuário.

Certifique-se de incluir o seguinte no diagrama de rede:

* Conectividade do dispositivo cliente (por exemplo, computador, dispositivo móvel e tablet) com a rede.
* Topologia da rede corporativa.
* Uplink para a Internet a partir da rede corporativa e do [!DNL Experience Manager] ambiente.
* Topologia do [!DNL Experience Manager] ambiente.
* Definir consumidores simultâneos do [!DNL Experience Manager] interface de rede.
* Fluxos de trabalho definidos do [!DNL Experience Manager] implantação.

## Conectividade do dispositivo cliente à rede corporativa {#connectivity-from-the-client-device-to-the-corporate-network}

Comece diagramando a conectividade entre os dispositivos cliente individuais e a rede corporativa. Nesse estágio, identifique os recursos compartilhados, como conexões WiFi, onde vários usuários acessam o mesmo ponto ou comutador ethernet para carregar e baixar ativos.

![chlimage_1-353](assets/chlimage_1-353.png)

Os dispositivos cliente conectam-se à rede corporativa de várias maneiras, como WiFi compartilhado, ethernet a um switch compartilhado e VPN. Identificar e entender os pontos de bloqueio nessa rede é importante para [!DNL Assets] e modificar a rede.

Na parte superior esquerda do diagrama, três dispositivos estão compartilhando um ponto de acesso WiFi de 48 Mbps. Se todos os dispositivos forem carregados simultaneamente, a largura de banda da rede WiFi será compartilhada entre os dispositivos. Em comparação com o sistema como um todo, um usuário pode encontrar um ponto de bloqueio diferente para os três clientes nesse canal dividido.

É um desafio medir a verdadeira velocidade de uma rede WiFi porque um dispositivo lento pode afetar outros clientes no ponto de acesso. Se você planeja usar o WiFi para interações de ativos, execute um teste de velocidade de vários clientes simultaneamente para avaliar a taxa de transferência.

A parte inferior esquerda do diagrama mostra dois dispositivos conectados à rede corporativa por canais independentes. Portanto, cada dispositivo pode utilizar uma velocidade mínima de 10 Mbps e 100 Mbps.

O computador exibido à direita tem um upstream limitado à rede corporativa através de uma VPN com uma velocidade de 1 Mbps. A experiência do usuário para a conexão de 1Mbps é muito diferente da experiência do usuário para a conexão de 1Gbps. Dependendo do tamanho dos ativos com os quais os usuários interagem, o uplink de VPN pode ser inadequado para a tarefa.

## Topologia da rede corporativa {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

O diagrama exibe velocidades de uplink mais altas na rede corporativa do que as geralmente usadas. Esses pipes são recursos compartilhados. Se for esperado que o switch compartilhado lide com 50 clientes, ele pode ser potencialmente um ponto de obstrução. No diagrama inicial, apenas dois computadores compartilham a conexão específica.

## Uplink para a Internet a partir da rede corporativa e [!DNL Experience Manager] ambiente {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

É importante considerar fatores desconhecidos na Internet e na conexão VPC, pois a largura de banda na Internet pode ser prejudicada devido ao pico de carga ou interrupções do provedor em larga escala. Em geral, a conectividade com a Internet é confiável. No entanto, às vezes pode introduzir pontos de estrangulamento.

No uplink de uma rede corporativa para a Internet, pode haver outros serviços usando a largura de banda. É importante entender quanto da largura de banda pode ser dedicada ou priorizada para o Assets. Por exemplo, se um link de 1 Gbps já estiver com 80% de utilização, você só poderá alocar um máximo de 20% da largura de banda para [!DNL Experience Manager Assets].

Firewalls e proxies corporativos também podem moldar a largura de banda de várias maneiras diferentes. Esse tipo de dispositivo pode priorizar a largura de banda usando qualidade de serviço, limitações de largura de banda por usuário ou limitações de taxa de bits por host. Esses são pontos de bloqueio importantes a serem examinados, pois podem afetar significativamente [!DNL Assets] experiência do usuário.

Neste exemplo, a empresa tem um uplink de 10 Gbps. Ele deve ser grande o suficiente para vários clientes. Além disso, o firewall impõe um limite de taxa de host de 10 Mbps. Essa limitação pode reduzir o tráfego para um único host para 10 Mbps, mesmo que o uplink para a Internet esteja em 10 Gbps.

Esse é o menor ponto de bloqueio orientado ao cliente. No entanto, você pode avaliar se há uma alteração ou configuração de uma lista de permissões com o grupo de operações de rede responsável por esse firewall.

A partir dos diagramas de amostra, é possível concluir que seis dispositivos compartilham um canal conceitual de 10 Mbps. Dependendo do tamanho dos ativos usados, isso pode ser inadequado para atender às expectativas do usuário.

## Topologia do [!DNL Experience Manager] ambiente {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

Projetando a topologia do [!DNL Experience Manager] O ambiente exige conhecimento detalhado da configuração do sistema e de como a rede está conectada no ambiente do usuário.

O cenário de exemplo inclui um farm de publicação com cinco servidores, um armazenamento binário S3 e o Dynamic Media configurado.

O dispatcher compartilha sua conexão de 100 Mbps com duas entidades, o mundo externo e o [!DNL Experience Manager] implantação. Para operações simultâneas de upload e download, você deve dividir esse número por dois. O armazenamento externo conectado usa uma conexão separada.

A variável [!DNL Experience Manager] O compartilha sua conexão de 1 Gbps com vários serviços. Do ponto de vista da topologia de rede, é equivalente ao compartilhamento de um único canal com diferentes serviços.

Examinando a rede do dispositivo cliente para o [!DNL Experience Manager] , o menor ponto de bloqueio parece ser o controle do firewall corporativo de 10 Mbit. Você pode usar esses valores na calculadora de dimensionamento na [Guia de dimensionamento de ativos](assets-sizing-guide.md) para determinar a experiência do usuário.

## Fluxos de trabalho definidos do [!DNL Experience Manager] implantação {#defined-workflows-of-the-aem-deployment}

Ao considerar o desempenho da rede, pode ser importante considerar os workflows e a publicação que ocorrerão no sistema. Além disso, o S3 ou outro armazenamento conectado à rede que você usa e as solicitações de E/S consomem largura de banda da rede. Portanto, mesmo em uma rede totalmente otimizada, o desempenho pode ser limitado pela E/S de disco.

Para simplificar os processos em torno da assimilação de ativos (especialmente ao fazer upload de um grande número de ativos), explore os fluxos de trabalho de ativos e entenda mais sobre a configuração deles.

Ao avaliar a topologia interna do fluxo de trabalho, você deve analisar o seguinte:

* Procedimentos que gravam um ativo
* Fluxos de trabalho/eventos que são acionados quando o ativo/metadados é modificado
* Procedimentos que leem um ativo

Estes são alguns itens a serem considerados:

* Leitura/gravação de metadados de XMP
* Ativação e replicação automáticas
* Marca d&#39;água
* Assimilação de subativos/extração de página
* Fluxos de trabalho sobrepostos.

Este é um exemplo de cliente para a definição de um fluxo de trabalho de ativo.

![chlimage_1-357](assets/chlimage_1-357.png)
