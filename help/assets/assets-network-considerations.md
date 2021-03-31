---
title: Considerações e requisitos de rede
description: Discute considerações de rede ao projetar uma implantação  [!DNL Adobe Experience Manager Assets] .
contentOwner: AG
role: Arquiteto, Administrador
feature: Ferramentas do desenvolvedor
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# [!DNL Assets] considerações de rede  {#assets-network-considerations}

Entender sua rede é tão importante quanto entender [!DNL Adobe Experience Manager Assets]. A rede pode afetar as experiências de upload, download e usuário. Diagramando sua topologia de rede, você pode identificar pontos de estrangulamento e áreas subotimizadas na rede que você deve corrigir para melhorar o desempenho da rede e a experiência do usuário.

Certifique-se de incluir o seguinte no diagrama de rede:

* Conectividade do dispositivo cliente (por exemplo, computador, dispositivo móvel e tablet) à rede.
* Topologia da rede corporativa.
* Faça o upload para a Internet a partir da rede corporativa e do ambiente [!DNL Experience Manager].
* Topologia do ambiente [!DNL Experience Manager].
* Defina consumidores simultâneos da interface de rede [!DNL Experience Manager].
* Fluxos de trabalho definidos da implantação [!DNL Experience Manager].

## Conectividade do dispositivo cliente para a rede corporativa {#connectivity-from-the-client-device-to-the-corporate-network}

Comece diagramando a conectividade entre os dispositivos clientes individuais e a rede corporativa. Neste estágio, identifique recursos compartilhados, como conexões WiFi, em que vários usuários acessam o mesmo ponto ou switch ethernet para fazer upload e download de ativos.

![chlimage_1-353](assets/chlimage_1-353.png)

Os dispositivos cliente se conectam à rede corporativa de várias maneiras, como WiFi compartilhado, ethernet a um switch compartilhado e VPN. Identificar e entender pontos de ancoragem nessa rede é importante para o planejamento [!DNL Assets] e modificar a rede.

Na parte superior esquerda do diagrama, três dispositivos são descritos como compartilhando um ponto de acesso WiFi de 48 Mbps. Se todos os dispositivos forem carregados simultaneamente, a largura de banda da rede WiFi será compartilhada entre os dispositivos. Comparado ao sistema como um todo, um usuário pode encontrar um ponto de estrangulamento diferente para os três clientes nesse canal dividido.

É um desafio medir a velocidade real de uma rede WiFi porque um dispositivo lento pode afetar outros clientes no ponto de acesso. Se você planeja usar o WiFi para interações com ativos, faça um teste de velocidade de vários clientes simultaneamente para avaliar a taxa de transferência.

A parte inferior esquerda do diagrama descreve dois dispositivos conectados à rede corporativa por meio de canais independentes. Portanto, cada dispositivo pode utilizar uma velocidade mínima de 10 Mbps e 100 Mbps.

O computador exibido à direita tem um upstream limitado à rede corporativa por meio de uma VPN com velocidade de 1 Mbps. A experiência do usuário para a conexão de 1Mbps é muito diferente da experiência do usuário com a conexão de 1Gbps. Dependendo do tamanho dos ativos com os quais os usuários interagem, o uplink de VPN pode ser inadequado para a tarefa.

## Topologia da rede corporativa {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

O diagrama exibe velocidades de uplink mais altas dentro da rede corporativa do que o geralmente usado. Essas tubulações são recursos compartilhados. Se for esperado que o switch compartilhado manipule 50 clientes, ele pode ser um ponto de estrangulamento. No diagrama inicial, apenas dois computadores compartilham a conexão específica.

## Faça o upload para a Internet a partir da rede corporativa e do [!DNL Experience Manager] ambiente {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

É importante considerar fatores desconhecidos na Internet e na conexão VPC, pois a largura de banda na Internet pode ser prejudicada devido a picos de carga ou paralisações de provedores em grande escala. Em geral, a conectividade com a Internet é confiável. No entanto, pode por vezes introduzir pontos de estrangulamento.

No uplink de uma rede corporativa para a Internet, pode haver outros serviços usando a largura de banda. É importante entender quanto da largura de banda pode ser dedicada ou priorizada para os Ativos. Por exemplo, se um link de 1 Gbps já estiver em 80% de utilização, você só poderá alocar um máximo de 20% da largura de banda para [!DNL Experience Manager Assets].

firewalls e proxies empresariais também podem moldar a largura de banda de várias maneiras diferentes. Esse tipo de dispositivo pode priorizar a largura de banda usando qualidade de serviço, limitações de largura de banda por usuário ou limitações de taxa de bits por host. Esses são pontos de estrangulamento importantes a serem examinados, pois podem afetar significativamente a experiência do usuário [!DNL Assets].

Neste exemplo, a empresa tem um uplink de 10 Gbps. Deve ser grande o suficiente para vários clientes. Além disso, o firewall impõe um limite de taxa de host de 10 Mbps. Essa limitação pode, potencialmente, reduzir o tráfego para um único host para 10 Mbps, mesmo que o uplink para a Internet seja de 10 Gbps.

Este é o menor ponto de estrangulamento orientado para o cliente. No entanto, é possível avaliar uma alteração ou configurar uma lista de permissões com o grupo de operações de rede responsável por esse firewall.

A partir dos diagramas de amostra, você pode concluir que seis dispositivos compartilham um canal conceitual de 10 Mbps. Dependendo do tamanho dos ativos aproveitados, isso pode ser inadequado para atender às expectativas do usuário.

## Topologia do ambiente [!DNL Experience Manager] {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

A criação da topologia do ambiente [!DNL Experience Manager] requer conhecimento detalhado da configuração do sistema e de como a rede é conectada no ambiente do usuário.

O cenário de amostra inclui um farm de publicação com cinco servidores, uma loja binária S3 e Dynamic Media configurados.

O dispatcher compartilha sua conexão de 100 Mbps com duas entidades, o mundo externo e a implantação [!DNL Experience Manager]. Para operações simultâneas de upload e download, você deve dividir esse número por dois. O armazenamento externo anexado usa uma conexão separada.

A implantação [!DNL Experience Manager] compartilha sua conexão de 1Gbps com vários serviços. Da perspectiva de topologia de rede, é equivalente a compartilhar um único canal com diferentes serviços.

Revisando a rede do dispositivo cliente para a implantação [!DNL Experience Manager], o menor ponto de estrangulamento parece ser o controle de firewall corporativo de 10 Mbit. Você pode usar esses valores na calculadora de dimensionamento no [Guia de dimensionamento de ativos](assets-sizing-guide.md) para determinar a experiência do usuário.

## Fluxos de trabalho definidos da implantação [!DNL Experience Manager] {#defined-workflows-of-the-aem-deployment}

Ao considerar o desempenho da rede, pode ser importante considerar os fluxos de trabalho e a publicação que ocorrerão no sistema. Além disso, o S3 ou outro armazenamento conectado à rede usado e as solicitações de E/S consomem largura de banda da rede. Portanto, mesmo em uma rede totalmente otimizada, o desempenho pode ser limitado pela E/S do disco.

Para simplificar os processos de assimilação de ativos (especialmente ao fazer upload de um grande número de ativos), explore os fluxos de trabalho de ativos e entenda mais sobre sua configuração.

Ao avaliar a topologia de workflow interno, você deve analisar o seguinte:

* Procedimentos para escrever um ativo
* Fluxos de trabalho/eventos que são acionados quando o ativo/metadados é modificado
* Procedimentos que leem um ativo

Estes são alguns itens a serem considerados:

* Leitura/write-back de metadados de XMP
* Ativação e replicação automáticas
* Aplicação de marca d&#39;água
* Assimilação/extração de página de subconjunto
* Fluxos de trabalho sobrepostos.

Este é um exemplo de cliente para a definição de um fluxo de trabalho de ativo.

![chlimage_1-357](assets/chlimage_1-357.png)
