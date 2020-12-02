---
title: Informações sobre o sistema de visualização
seo-title: Informações sobre o sistema de visualização
description: Saiba como você pode visualização gráficos de monitoramento de recursos e informações sobre o servidor que está executando AEM formulários.
seo-description: Saiba como você pode visualização gráficos de monitoramento de recursos e informações sobre o servidor que está executando AEM formulários.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Informações do sistema de visualização {#view-system-information}

A guia Sistema exibe gráficos de monitoramento de recursos e informações sobre o servidor que está executando AEM formulários. Para acessar essas informações, no console de administração, clique em Monitor de integridade no canto superior direito da página. Se você estiver executando AEM formulários em um ambiente agrupado, as informações exibidas serão para o nó selecionado na lista do servidor.

Para salvar as informações atuais do sistema como um arquivo de propriedades, clique em Salvar.

O painel direito da guia Sistema exibe representações gráficas das seguintes informações:

* Itens de trabalho e contagem de trabalho
* Uso de heap e heap confirmado
* Uso não heap e não heap confirmado

Você pode arrastar o ponteiro ao longo da linha do tempo para obter valores para um ponto específico no tempo.

>[!NOTE]
>
>Os dados do gráfico, os valores das informações do servidor e o tempo do relógio são atualizados a cada 10 minutos. As informações não são exibidas em tempo real.

O painel esquerdo da guia Sistema exibe as seguintes informações sobre o servidor ou nó:

**Máquina virtual:versão JVM (** Java Virtual Machine) no servidor.

**Fornecedor de Máquina Virtual:** Fabricante da JVM.

**Versão da Máquina Virtual:número da versão** JVM

**Nome da máquina: nome do** host do servidor no qual os formulários AEM estão instalados.

**Tempo de funcionamento:** o tempo, em horas e minutos, em que o servidor está em execução.

**Compilador just-in-time:** o nome do compilador que está sendo usado.

**Tempo de compilação:** A quantidade de tempo gasto na compilação.

**Número de Threads em tempo real:** O número total de threads presentes atualmente no sistema de formulários AEM.

**Número de Threads Máximo:** Maior número de threads ativos já gravados no sistema.

**Número de classes carregadas:** número de classes carregadas na JVM.

**Número de classes descarregadas:** número de classes descarregadas da JVM.

**Heap mínimo:** a quantidade mínima de heap usada.

**Heap máximo:** a quantidade máxima de heap usada.

**Nome do sistema operacional:** o nome do sistema operacional em execução no servidor de formulários AEM.

**Versão do sistema operacional:número** da versão do sistema operacional em execução no servidor de formulários AEM.

**Arch do sistema operacional:** a arquitetura do sistema operacional em que a JVM está sendo executada.

**Número de processadores:** O número de processadores no sistema.

**Argumentos de Máquina Virtual:** O argumento usado pela JVM.

**Caminho da classe:** o caminho da classe usado pela JVM.

**Caminho da biblioteca:** o caminho da biblioteca usado pela JVM.

**Caminho da classe de inicialização:** o caminho da classe de inicialização usado pela JVM.

**Tipo de servidor de aplicativos:** Tipo de servidor de aplicativos usado para executar formulários AEM.

**Versão do servidor de aplicativos:número de** versão do servidor de aplicativos usado para executar formulários AEM.

**Fornecedor do servidor de aplicativos:** Fabricante do servidor de aplicativos usado para executar formulários AEM.

**Data de instalação:** Data (no formato aaaa-mm-dd) em que os formulários AEM foram instalados.

**Versão dos formulários AEM:** Versão dos formulários AEM instalados.

**Versão do patch:** AEM número do patch dos formulários.

**Nome do banco de dados:** Tipo de banco de dados usado por formulários AEM.

**Versão do banco de dados:número de** versão do banco de dados usado por formulários AEM.

**Nome da unidade de banco de dados:** o nome do driver usado pela JVM para conexão com o banco de dados.

**Versão do driver do banco de dados:** a versão do driver usada pela JVM para conexão com o banco de dados.

O botão **Salvar** permite salvar essas informações do sistema em um arquivo de propriedade.
