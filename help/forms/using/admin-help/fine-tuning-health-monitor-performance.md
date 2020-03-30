---
title: Ajuste do desempenho do Monitor de Integridade
seo-title: Ajuste do desempenho do Monitor de Integridade
description: Saiba como ajustar o desempenho do Monitor de integridade
seo-description: Saiba como ajustar o desempenho do Monitor de integridade
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Ajuste do desempenho do Monitor de Integridade{#fine-tuning-health-monitor-performance}

A coleta de estatísticas do sistema que preenchem o Monitor de integridade afeta o desempenho do ambiente de formulários do AEM. Esse impacto pode ser controlado pela configuração das opções de Java listadas abaixo no servidor de aplicativos.

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
   <td><p>adobe.saudável.monitor.enabled</p></td>
   <td><p>Ativar ou desativar a thread do Monitor de Integridade</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Ativar ou desativar o cache do Gemfire</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
  <tr>
   <td><p>adobe.saudmonitor.refresh-range</p></td>
   <td><p>O intervalo em milissegundos após o qual o thread do Monitor de Integridade coleta as estatísticas</p></td>
   <td><p>10 minutos (600.000 milissegundos)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>A porta de multicast usada para se comunicar com outros membros do sistema distribuído. Se definido como zero, o multicast será desativado para detecção e distribuição de membros. </p><p>Observação: Selecione endereços e portas de multicast diferentes para sistemas distribuídos diferentes. Não use somente endereços diferentes.</p></td>
   <td><p>Nenhum valor padrão. Os valores válidos variam de 0 a 65535.</p></td>
  </tr>
  <tr>
   <td><p>taxa de amostragem estatística</p></td>
   <td><p>A taxa em milissegundos na qual as estatísticas são amostradas. As estatísticas do sistema operacional só são atualizadas quando uma amostra é coletada.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.saudmonitor.enabled</p></td>
   <td><p>Essa propriedade ativa ou desativa a coleta estatística do Gerenciador de Trabalho, como a contagem de itens de trabalho ou de trabalho.</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
 </tbody>
</table>

## Adicionar opções Java a JBoss {#add-java-options-to-jboss}

1. Pare o servidor de aplicativos JBoss.
1. Abra o *[appserver root]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) em um editor e adicione qualquer uma das opções Java conforme necessário.
1. Reinicie o servidor.

## Adicionar opções Java ao WebLogic {#add-java-options-to-weblogic}

1. Start o console de administração WebLogic digitando https://[host name]:&#39;port&#39;/console na linha URL de um navegador da Web.
1. Digite o nome de usuário e a senha que você criou para o domínio do WebLogic Server e clique em Registrar em Change Center (Centro de alterações) e clique em Bloquear e editar.
1. Em Estrutura do domínio, clique em Ambiente > Servidores e, no painel direito, clique no nome do servidor gerenciado.
1. Na tela seguinte, clique na guia Configuração > guia Start do servidor.
1. Na caixa Argumentos, anexe os argumentos necessários ao final do conteúdo atual. Por exemplo, adicionar - `Dadobe.healthmonitor.enabled=false` desativa o Monitor de integridade.
1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

## Adicionar opções Java ao WebSphere {#add-java-options-to-websphere}

1. Na árvore de navegação do Console administrativo do WebSphere, faça o seguinte para o servidor de aplicativos:

   (WebSphere 6.x) Clique em Servidores > Servidores de aplicativos

   (WebSphere 7.x) Clique em Servidores > Tipos de servidor > Servidores de aplicativos WebSphere

1. No painel direito, clique no nome do servidor.
1. Em Infraestrutura do servidor, clique em Java e fluxo de trabalho dos formulários > Definição do processo.
1. Em Propriedades adicionais, clique em Java Virtual Machine.
1. Na caixa Argumentos JVM genéricos, digite os argumentos necessários.
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração mestre.

