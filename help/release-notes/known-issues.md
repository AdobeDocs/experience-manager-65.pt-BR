---
title: Problemas conhecidos
description: Notas de versão específicas dos problemas conhecidos com o Adobe Experience Manager 6.5
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 0a55ed44cb7fe3320b2196df38fe8492ee03912d
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 57%

---


# Problemas conhecidos {#known-issues}

Esta página apresenta uma lista de problemas conhecidos do Adobe Experience Manager 6.5, lançado em abril de 2019.

[Entre em contato com o suporte](https://helpx.adobe.com/br/support/experience-manager.html) se precisar de mais informações sobre os problemas conhecidos.

## Plataforma {#platform}

* Um problema é reportado onde o CRX-Quickstart e seu conteúdo são excluídos.

   Em cada uma dessas ações, verifique se a propriedade &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; nunca é uma string vazia:

   1. Chamando &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
   2. Atualização para o AEM 6.5.
   3. Execução da &quot;migração de conteúdo lento&quot; no AEM 6.5.

   Um artigo da [Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) de conhecimento está disponível com mais detalhes e a solução alternativa para esse problema.

* Se você estiver usando o JDK 11 com a instância do AEM 6.5, algumas páginas podem ser exibidas em branco após a implantação de alguns pacotes. A seguinte mensagem de erro é exibida no arquivo de log:

   ```
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Para resolver esse erro:

1. Pare a instância do AEM. Vá até `<aem_server_path_on_server>crx-quickstart\conf` e abra o `sling.properties` arquivo. A Adobe recomenda fazer um backup desse arquivo.

2. Pesquisar `org.osgi.framework.bootdelegation=`. Adicione `jdk.internal.reflect,jdk.internal.reflect.*` propriedades para exibir o resultado como:

   ```
   org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
   ```

3. Salve o arquivo e reinicie a instância do AEM.

## Assets {#assets}

* **Pesquisar:** A pesquisa não resultará em nenhum retorno se a string de pesquisa contiver espaços à esquerda ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadados de pasta**: depois de adicionar um botão de escolha, os campos ID e Valor não são renderizados como esperado e a funcionalidade de exclusão não funciona. (CQ-4261144)
* Ao renomear um ativo, não é possível usar um espaço em branco no nome do ativo. (CQ-4266403)

## Forms {#forms}

* Quando os formulários do AEM são instalados no sistema operacional do Linux, a assinatura digital com o módulo de segurança de hardware não funciona. (CQ-4266721)
* (Formulários do AEM somente na WebSphere) A opção **Fluxo de trabalho de formulários** > **Pesquisa de tarefas** não retorna nenhum resultado se você pesquisar por um **Administrador** com o **nome de usuário** como o critério de pesquisa. (CQ-4266457)

* Os formulários AEM não conseguem converter arquivos .tif e .tiff com compactação JPEG em documentos PDF. (CQ-4265972)
* As opções **Scanner de ativos do AEM Forms** e **Carta para migração de comunicação interativa** não funcionam na página **Migração do AEM Forms**. (CQ-4266572)

* (Somente para JBoss 7) Quando você atualiza de uma versão anterior para o AEM 6.5 Forms e a versão anterior tinha processos (.lca) que criavam e usavam uma cópia do processo padrão de envio ou renderização, o HTML5 Forms usando tais processos (.lca) não executa as ações necessárias. (CQ-4243928)
* Em um formulário adaptável, quando um serviço de modelo de dados do formulário é chamado a partir do editor de regras para atualizar valores dinamicamente do componente de escolha de imagem, os valores do componente de escolha de imagem não são atualizados. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/pt-br/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/pt-br/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Certifique-se de que os pacotes de tempo de execução redistribuíveis mencionados acima estão instalados antes de iniciar a instalação. (CQ-4265668)

* O Gerador de PDF não suporta autenticação baseada em smart card.  Quando um administrador ativa a Política de grupo `Interactive Logon: Require Smart card` em um servidor Windows, todos os usuários existentes do Gerador de PDF são invalidados.

* Quando um formulário adaptável é configurado para atualizar dinamicamente valores de um componente e a instância de publicação que hospeda o formulário é acessada por meio do distribuidor, a funcionalidade para atualizar dinamicamente os valores de um campo para de funcionar. Para solucionar o problema, na instância de publicação, abra o CRXDE, navegue até /libs/fd/af/runtime/clientlibs/guideChartReducer e crie a propriedade listada abaixo. 

   * Nome: allowProxy
   * Tipo: booliano
   * Valor: true
   * Protegido: false
   * Obrigatório: false
   * Vários: false
   * Criado automaticamente: false

   A propriedade habilita as bibliotecas de clientes na pasta de tempo de execução para acessar proxies. (CQ-4268679)

* 
   * Quando o AEM Forms for iniciado, o `SAX Security Manager could not be setup` aviso será exibido.