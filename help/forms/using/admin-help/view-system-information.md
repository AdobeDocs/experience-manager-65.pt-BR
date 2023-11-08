---
title: Exibir informações do sistema
seo-title: View system information
description: Saiba como visualizar gráficos de monitoramento de recursos e informações sobre o servidor que está executando formulários AEM.
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Exibir informações do sistema {#view-system-information}

A guia Sistema exibe gráficos de monitoramento de recursos e informações sobre o servidor que está executando formulários AEM. Para acessar essas informações, no console de administração, clique em Monitor de integridade no canto superior direito da página. Se você estiver executando formulários AEM em um ambiente em cluster, as informações exibidas serão para o nó selecionado na lista Servidor.

Para salvar as informações atuais do sistema como um arquivo de propriedades, clique em Salvar.

O painel direito da guia Sistema exibe representações gráficas das seguintes informações:

* Itens de Trabalho e Contagem de Trabalho
* Uso de Heap e Heap Comprometido
* Uso de Não-heap e Não-heap Confirmado

Você pode arrastar seu ponteiro ao longo da linha do tempo para obter valores para um determinado momento.

>[!NOTE]
>
>Os dados do gráfico, os valores das informações do servidor e a hora do relógio são atualizados a cada 10 minutos. As informações não são exibidas em tempo real.

O painel esquerdo da guia Sistema exibe as seguintes informações sobre o servidor ou nó:

**Máquina Virtual:** Versão da Java Virtual Machine (JVM) no servidor.

**Fornecedor da Máquina Virtual:** Fabricante da JVM.

**Versão da Máquina Virtual:** Número da versão da JVM

**Nome da máquina:** Nome do host do servidor onde o AEM Forms está instalado.

**Tempo de Atividade:** O tempo, em horas e minutos, em que o servidor esteve em execução.

**Compilador Just-In-Time:** O nome do compilador que está sendo usado.

**Tempo de compilação:** O tempo gasto na compilação.

**Número de Threads ao vivo:** O número total de threads presentes atualmente no sistema de formulários AEM.

**Número de pico de Threads:** Maior número de threads ativos já registrados no sistema.

**Número de classes carregadas:** Número de classes carregadas na JVM.

**Número de classes descarregadas:** Número de classes descarregadas da JVM.

**Heap mínimo:** A quantidade mínima de heap que foi usada.

**Heap máximo:** A quantidade máxima de heap que foi usada.

**Nome do sistema operacional:** O nome do sistema operacional em execução no servidor do AEM Forms.

**Versão do sistema operacional:** Número da versão do sistema operacional em execução no AEM Forms Server.

**Arco do sistema operacional:** A arquitetura do sistema operacional em que a JVM está sendo executada.

**Número de processadores:** O número de processadores no sistema.

**Argumentos da Máquina Virtual:** O argumento usado pela JVM.

**Caminho da classe:** O caminho de classe usado pela JVM.

**Caminho da biblioteca:** O caminho da biblioteca usado pela JVM.

**Caminho da classe de inicialização:** O caminho da classe de inicialização usado pela JVM.

**Tipo de servidor de aplicativo:** Tipo de servidor de aplicativos usado para executar formulários AEM.

**Versão do Servidor de Aplicativos:** Número de versão do servidor de aplicativos usado para executar formulários AEM.

**Fornecedor do servidor de aplicativos:** Fabricante do servidor de aplicativos usado para executar formulários AEM.

**Data da instalação:** Data (no formato aaaa-mm-dd) em que os formulários AEM foram instalados.

**AEM Forms Versão:** Versão do AEM Forms instalada.

**Versão do Patch:** Número de correção de formulários AEM.

**Nome do banco de dados:** Tipo de banco de dados usado por formulários AEM.

**Versão do Banco de Dados:** Número de versão do banco de dados usado por formulários AEM.

**Nome da Unidade do Banco de Dados:** O nome do driver usado pela JVM para conectar-se ao banco de dados.

**Versão do Driver do Banco de Dados:** A versão do driver usada pela JVM para se conectar ao banco de dados.

A variável **Salvar** O botão permite salvar essas informações do sistema em um arquivo de propriedades.
