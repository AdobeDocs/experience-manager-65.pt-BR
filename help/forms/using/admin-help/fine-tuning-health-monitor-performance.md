---
title: Ajustando o desempenho do Monitor de Integridade
description: Saiba como ajustar o desempenho do Monitor de integridade. Controlar as estatísticas do sistema que afetam o desempenho do ambiente de formulários usando a opção de configuração JAVA.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Ajustando o desempenho do Monitor de Integridade{#fine-tuning-health-monitor-performance}

Coletar as estatísticas do sistema que preenchem o Health Monitor tem algum impacto no desempenho do seu ambiente de formulários AEM. Esse impacto pode ser controlado definindo as opções de Java listadas abaixo em seu servidor de aplicativos.

<table>
 <thead>
  <tr>
   <th><p>Propriedade</p></th>
   <th><p>Propósito</p></th>
   <th><p>Valor padrão</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>Ativar ou desativar thread do Monitor de Integridade</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Ativar ou desativar o armazenamento em cache do Gemfire</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>O intervalo em milissegundos após o qual o thread do Monitor de Integridade coleta as estatísticas</p></td>
   <td><p>10 minutos (600.000 milissegundos)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>A porta multicast usada para se comunicar com outros membros do sistema distribuído. Se definido como zero, o multicast será desabilitado para descoberta e distribuição de membros. </p><p>Observação: selecione portas e endereços de multicast diferentes para sistemas distribuídos diferentes. Não use somente endereços diferentes.</p></td>
   <td><p>Nenhum valor padrão. Os valores válidos variam de 0 a 65535.</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>A taxa em milissegundos em que as estatísticas são amostradas. As estatísticas do sistema operacional só são atualizadas quando uma amostra é coletada.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Essa propriedade ativa ou desativa a coleta de estatísticas do Work Manager, como contagem de itens de trabalho ou de jobs.</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
 </tbody>
</table>

## Adicionar opções Java ao JBoss {#add-java-options-to-jboss}

1. Interrompa o servidor da aplicação JBoss.
1. Abra o *[raiz do appserver]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) em um editor e adicione qualquer uma das opções de Java, conforme necessário.
1. Reinicie o servidor.

## Adicionar opções Java ao WebLogic {#add-java-options-to-weblogic}

1. Inicie o console de administração do WebLogic digitando https://[nome do host]:&#39;port&#39;/console na linha URL de um navegador da web.
1. Digite o nome de usuário e a senha criados para o domínio do WebLogic Server e clique em Registrar no Centro de Alterações, em Bloquear e Editar.
1. Em Estrutura do domínio, clique em Ambiente > Servidores e, no painel direito, clique no nome do servidor gerenciado.
1. Na próxima tela, clique na guia Configuração > na guia Início do servidor.
1. Na caixa Argumentos, anexe os argumentos necessários ao final do conteúdo atual. Por exemplo, adicionar - `Dadobe.healthmonitor.enabled=false` desabilita o Monitor de Integridade.
1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

## Adicionar opções de Java ao WebSphere {#add-java-options-to-websphere}

1. Na árvore de navegação do Console administrativo do WebSphere, faça o seguinte para o servidor de aplicativos:

   (WebSphere 6.x) Clique em Servidores > Servidores de aplicativos

   (WebSphere 7.x) Clique em Servidores > Tipos de servidor > Servidores de aplicativos WebSphere

1. No painel direito, clique no nome do servidor.
1. Em Infraestrutura do servidor, clique em Fluxo de trabalho de formulários e Java > Definição de processo.
1. Em Propriedades adicionais, clique em Java Virtual Machine.
1. Na caixa Generic JVM arguments, digite os argumentos necessários.
1. Clique em OK ou em Aplicar e, em seguida, clique em Salvar diretamente na configuração-mestre.
