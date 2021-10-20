---
title: Problemas conhecidos
description: Notas de versão específicas dos problemas conhecidos com o Adobe Experience Manager 6.5
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: e0f024c2e1dc9fc7908382d406844575b4b38363
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 43%

---

# Problemas conhecidos {#known-issues}

Esta página apresenta uma lista de problemas conhecidos do Adobe Experience Manager 6.5, lançado em abril de 2019.

[Entre em contato com o suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) se precisar de mais informações sobre os problemas conhecidos.

## Plataforma {#platform}

* Um problema é reportado onde o CRX-Quickstart e seu conteúdo são excluídos.

   Em cada uma dessas ações, verifique se a propriedade `htmllibmanager.fileSystemOutputCacheLocation` não é uma string vazia:

   1. Chamada `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Atualização para o AEM 6.5.
   3. Execução de &quot;migração de conteúdo lento&quot; no AEM 6.5.

   A [Base de dados de conhecimento](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) o artigo está disponível com mais detalhes e a solução alternativa para esse problema.

* Se você estiver usando o JDK 11 com AEM instância 6.5, algumas páginas poderão ser exibidas em branco após a implantação de alguns pacotes. A seguinte mensagem de erro é exibida no arquivo de log:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Para resolver este erro:

1. Pare a instância de AEM. Ir para `<aem_server_path_on_server>crx-quickstart\conf` e abra o `sling.properties` arquivo. O Adobe recomenda fazer um backup desse arquivo.

1. Pesquisar `org.osgi.framework.bootdelegation=`. Adicionar `jdk.internal.reflect,jdk.internal.reflect.*` propriedades para exibir o resultado como.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salve o arquivo e reinicie a instância de AEM.

## Ativos {#assets}

* **Pesquisar:** A pesquisa não resulta em retornos se a string de pesquisa contiver espaço à esquerda ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadados de pasta**: depois de adicionar um botão de escolha, os campos ID e Valor não são renderizados como esperado e a funcionalidade de exclusão não funciona. (CQ-4261144)
* Ao renomear um ativo, não é possível usar um espaço em branco no nome do ativo. (CQ-4266403)

## Forms {#forms}

* Quando o AEM Forms é instalado no sistema operacional Linux, a assinatura digital com o módulo de segurança de hardware não funciona. (CQ-4266721)
* (AEM Forms somente na WebSphere) A opção **Fluxo de trabalho de formulários** > **Pesquisa de tarefas** não retorna nenhum resultado se você pesquisar por um **Administrador** com o **nome de usuário** como o critério de pesquisa. (CQ-4266457)

* O AEM Forms não converte arquivos TIF e TIFF com compactação JPEG para Documentos PDF. (CQ-4265972)
* As opções **Scanner de ativos do AEM Forms** e **Carta para migração de comunicação interativa** não funcionam na página **Migração do AEM Forms**. (CQ-4266572)

* (Somente JBoss 7) Quando você atualiza de uma versão anterior para AEM 6.5 Forms e a versão anterior tinha processos (.lca) que criaram e usaram uma cópia do processo de envio ou renderização padrão, o HTML5 Forms que usa esses processos (.lca) não executa as ações necessárias. (CQ-4243928)
* Em um formulário adaptável, quando um serviço de modelo de dados do formulário é chamado a partir do editor de regras para atualizar valores dinamicamente do componente de escolha de imagem, os valores do componente de escolha de imagem não são atualizados. (CQ-4254754)
* O instalador do AEM Forms Designer requer a versão de 32 bits do [Pacote de tempo de execução redistribuível do Visual C++ 2012](https://support.microsoft.com/pt-br/help/2977003/the-latest-supported-visual-c-downloads) e [Pacotes de tempo de execução redistribuíveis do Visual C++ 2013](https://support.microsoft.com/pt-br/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Certifique-se de que os pacotes de tempo de execução redistribuíveis mencionados acima estão instalados antes de iniciar a instalação. (CQ-4265668)

* O Gerador de PDF não suporta autenticação baseada em smart card.  Quando um administrador ativa a Política de Grupo `Interactive Logon: Require Smart card` em um servidor Windows, todos os usuários existentes do PDF Generator são invalidados.

* Quando um formulário adaptável é configurado para atualizar dinamicamente valores de um componente e a instância de publicação que hospeda o formulário é acessada por meio do distribuidor, a funcionalidade para atualizar dinamicamente os valores de um campo para de funcionar. Para resolver o problema, na instância de publicação, abra o CRXDE, navegue até `/libs/fd/af/runtime/clientlibs/guideChartReducer`e crie a propriedade listada abaixo.

   * Nome: allowProxy
   * Tipo: booliano
   * Valor: true
   * Protegido: false
   * Obrigatório: false
   * Vários: false
   * Criado automaticamente: Falso

   A propriedade habilita as bibliotecas de clientes na pasta de tempo de execução para acessar proxies. (CQ-4268679)

* Quando o AEM Forms for iniciado, a variável `SAX Security Manager could not be setup` for exibido.
* Ao abrir um PDF protegido com a Segurança de documento da AEM Forms em um Apple iOS ou iPadOS executando a versão 20.10.00 do Adobe Acrobat Reader.
* Às vezes, ao enviar um formulário contendo um campo de carregamento HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 bytes é recebido na outra extremidade. O Apple iOS 15.1 fornece uma correção para o problema.
