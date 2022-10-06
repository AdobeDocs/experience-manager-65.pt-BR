---
title: Exibir informações do sistema
seo-title: View system information
description: Saiba como visualizar gráficos de monitoramento de recursos e informações sobre o servidor que está executando AEM formulários.
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Exibir informações do sistema {#view-system-information}

A guia Sistema exibe gráficos de monitoramento de recursos e informações sobre o servidor que está executando AEM formulários. Para acessar essas informações, no console de administração, clique em Monitor de integridade no canto superior direito da página. Se você estiver executando AEM formulários em um ambiente em cluster, as informações exibidas serão para o nó selecionado na lista Servidor.

Para salvar as informações atuais do sistema como um arquivo de propriedades, clique em Salvar.

O painel direito da guia Sistema exibe representações gráficas das seguintes informações:

* Itens de Contagem de Trabalho e Trabalho
* Uso de heap e heap confirmado
* Uso de não heap e não heap confirmado

Você pode arrastar o ponteiro ao longo da linha do tempo para obter valores para um ponto específico no tempo.

>[!NOTE]
>
>Os dados do gráfico, os valores de informações do servidor e o tempo do relógio são atualizados a cada 10 minutos. As informações não são exibidas em tempo real.

O painel esquerdo da guia Sistema exibe as seguintes informações sobre o servidor ou nó:

**Máquina Virtual:** Versão da JVM (Java Virtual Machine) no servidor.

**Fornecedor de Máquina Virtual:** Fabricante da JVM.

**Versão da Máquina Virtual:** Número de versão da JVM

**Nome da Máquina:** Nome do host do servidor onde AEM formulários está instalado.

**Tempo de ativação:** O tempo, em horas e minutos, que o servidor está sendo executado.

**Compilador just-in-time:** O nome do compilador que está sendo usado.

**Hora da compilação:** A quantidade de tempo gasto na compilação.

**Número de Threads Live:** O número total de threads presentes atualmente no sistema de formulários AEM.

**Número de Threads Picos:** Maior número de threads ativos já registrados no sistema.

**Número de classes carregadas:** Número de classes carregadas na JVM.

**Número de classes não carregadas:** Número de classes descarregadas da JVM.

**Heap mínimo:** A quantidade mínima de heap que foi usada.

**Heap máximo:** A quantidade máxima de heap que foi usada.

**Nome do sistema operacional:** O nome do sistema operacional em execução no servidor de formulários AEM.

**Versão do sistema operacional:** Número de versão do sistema operacional em execução no servidor de formulários AEM.

**Arco do sistema operacional:** A arquitetura do sistema operacional em que a JVM está sendo executada.

**Número de processadores:** O número de processadores no sistema.

**Argumentos da Máquina Virtual:** O argumento usado pela JVM.

**Caminho da classe:** O caminho de classe usado pela JVM.

**Caminho da biblioteca:** O caminho da biblioteca usado pela JVM.

**Caminho da classe de inicialização:** O caminho da classe de inicialização usado pela JVM.

**Tipo de Servidor de Aplicações:** Tipo de servidor de aplicativos usado para executar AEM formulários.

**Versão do Servidor de Aplicativos:** Número de versão do servidor de aplicativos usado para executar AEM formulários.

**Fornecedor do Servidor de Aplicações:** Fabricante do servidor de aplicativos usado para executar formulários AEM.

**Data de instalação:** Data (em formato aaaa-mm-dd) em que AEM formulários foi instalado.

**Versão dos formulários AEM:** Versão de AEM formulários que está instalada.

**Versão do patch:** Número do patch para formulários AEM.

**Nome do Banco de Dados:** Tipo de banco de dados usado por formulários AEM.

**Versão do Banco de Dados:** Número de versão do banco de dados usado por formulários AEM.

**Nome da Unidade de Banco de Dados:** O nome do driver usado pela JVM para conexão com o banco de dados.

**Versão do driver do banco de dados:** A versão do driver usada pela JVM para se conectar ao banco de dados.

O **Salvar** permite salvar essas informações do sistema em um arquivo de propriedade.
