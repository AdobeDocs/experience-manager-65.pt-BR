---
title: Ajustando o desempenho do Monitor de Integridade
seo-title: Fine-tuning Health Monitor performance
description: Saiba como ajustar o desempenho do Monitor de integridade
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# Ajustando o desempenho do Monitor de Integridade{#fine-tuning-health-monitor-performance}

A coleta das estatísticas do sistema que preenchem o Monitor de integridade afeta o desempenho do ambiente de formulários AEM. Esse impacto pode ser controlado definindo as opções de Java listadas abaixo no servidor de aplicativos.

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
   <td><p>Ativar ou desativar thread do Monitor de Estado de Funcionamento</p></td>
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
   <td><p>A porta de multicast usada para se comunicar com outros membros do sistema distribuído. Se definida como zero, a multicast será desativada para detecção e distribuição de membros. </p><p>Observação: Selecione diferentes endereços e portas multicast para diferentes sistemas distribuídos. Não use somente endereços diferentes.</p></td>
   <td><p>Nenhum valor padrão. Os valores válidos variam de 0 a 65535.</p></td>
  </tr>
  <tr>
   <td><p>taxa de amostra de estatística</p></td>
   <td><p>A taxa em milissegundos à qual as estatísticas são amostradas. As estatísticas do sistema operacional só são atualizadas quando uma amostra é coletada.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Essa propriedade ativa ou desativa a coleta de estatísticas do Gerenciador de Trabalho, como a contagem de tarefas ou de itens de trabalho.</p></td>
   <td><p>verdadeiro</p></td>
  </tr>
 </tbody>
</table>

## Adicionar opções Java ao JBoss {#add-java-options-to-jboss}

1. Pare o servidor de aplicativos JBoss.
1. Abra o *[raiz do appserver]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) em um editor e adicione qualquer uma das opções do Java, conforme necessário.
1. Reinicie o servidor.

## Adicionar opções de Java ao WebLogic {#add-java-options-to-weblogic}

1. Inicie o console de administração do WebLogic digitando https://[nome do host]:&#39;port&#39;/console na linha do URL de um navegador da Web.
1. Digite o nome de usuário e a senha que você criou para o domínio do WebLogic Server e clique em Registrar no Change Center, clique em Bloquear e editar.
1. Em Estrutura de domínio, clique em Ambiente > Servidores e, no painel direito, clique no nome do servidor gerenciado.
1. Na próxima tela, clique na guia Configuração > Início do servidor .
1. Na caixa Argumentos , anexe os argumentos necessários ao final do conteúdo atual. Por exemplo, adicionar - `Dadobe.healthmonitor.enabled=false` desativa o Monitor de integridade.
1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado do WebLogic.

## Adicionar opções Java ao WebSphere {#add-java-options-to-websphere}

1. Na árvore de navegação do Console Administrativo do WebSphere, faça o seguinte para o servidor de aplicativos:

   (WebSphere 6.x) Clique em Servidores > Servidores de aplicativos

   (WebSphere 7.x) Clique em Servidores > Tipos de Servidor > Servidores de Aplicativos WebSphere

1. No painel direito, clique no nome do servidor.
1. Em Infraestrutura do servidor, clique em Java e fluxo de trabalho de formulários > Definição do processo.
1. Em Additional Properties, clique em Java Virtual Machine.
1. Na caixa Generic JVM arguments, digite os argumentos necessários.
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração principal.
