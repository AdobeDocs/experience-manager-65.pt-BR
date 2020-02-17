---
title: Pré-requisitos para integração com o Adobe Target
seo-title: Pré-requisitos para integração com o Adobe Target
description: Descubra os pré-requisitos para integração com o Adobe Target.
seo-description: Descubra os pré-requisitos para integração com o Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Pré-requisitos para integração com o Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte da [integração do AEM e do Adobe Target](/help/sites-administering/target.md), você precisa se registrar no Adobe Target, configurar o agente de replicação e as configurações de atividade segura no nó de publicação.

## Registrar-se no Adobe Target {#registering-with-adobe-target}

Para integrar o AEM ao Adobe Target, é necessário ter uma conta válida do Adobe Target. Esta conta deve ter no mínimo permissões de nível de **aprovador** . Ao se registrar no Adobe Target, você recebe um código de cliente. Você precisa do código do cliente e do nome de logon e senha do Adobe Target para conectar o AEM ao Adobe Target.

O Código do cliente identifica a conta do cliente do Adobe Target ao chamar o servidor do Adobe Target.

>[!NOTE]
>
>Sua conta também deve ser ativada pela equipe do Target para usar a integração.
>
>
>Caso contrário, entre em contato com o Atendimento ao cliente [do Adobe Target](https://marketing.adobe.com/resources/help/en_US/target/target/r_problem.html).

## Ativação do agente de replicação do Target {#enabling-the-target-replication-agent}

O agente [de](/help/sites-deploying/replication.md) replicação Test e Target deve estar habilitado na instância do autor. Observe que esse agente de replicação não estará habilitado por padrão se você tiver usado o modo de execução [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) para instalar o AEM. Para obter mais informações sobre como proteger seu ambiente de produção, consulte a Lista de verificação [de](/help/sites-administering/security-checklist.md)segurança.

1. Na página inicial do AEM, clique ou toque em **Ferramentas** > **Implantação** > **Replicação**.
1. Clique ou toque em **Agentes no autor**.
1. Clique ou toque no agente de replicação do **Test and Target (teste e destino)** e clique ou toque em **Editar**.
1. Selecione a opção Ativado e clique ou toque em **OK**.

   >[!NOTE]
   >
   >Ao configurar o agente de replicação Test e Target, na guia **Transporte** , o URI é definido por padrão como **tnt:///**. Não substitua este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Observe que se você tentar testar a conexão com **tnt:///**, ocorrerá um erro. Esse comportamento é esperado, pois esse URI é apenas para uso interno e não deve ser usado com o **Test Connection**.

## Protegendo o nó de configurações da atividade {#securing-the-activity-settings-node}

You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.

**O nó** cq:ActivitySettings`/content/campaigns/*nameofbrand*` está disponível na lista CRXDE em *** sob as atividades jcr:content node; *por exemplo `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Esse nó é criado somente depois que você direciona um componente.

O nó **cq:ActivitySettings** sob o jcr:content da atividade é protegido pelas seguintes ACLs:

* Negar tudo para todos
* Permitir jcr:read,rep:write para &quot;target-activity-author&quot; (o autor é um membro deste grupo fora da caixa)
* Permitir jcr:read,rep:write para &quot;targetservice&quot;

Essas configurações garantem que os usuários normais não tenham acesso às propriedades do nó. Use as mesmas ACLs no autor e na publicação. Consulte Administração e segurança [do](/help/sites-administering/security.md) usuário para obter mais informações.

## Configuração do externalizador de links AEM {#configuring-the-aem-link-externalizer}

Ao editar uma atividade no Adobe Target, o URL aponta para **localhost** , a menos que você altere o URL no nó do autor do AEM. Você pode configurar o Externalizador de links AEM se desejar que o conteúdo exportado aponte para um domínio de *publicação* específico.

>[!NOTE]
>
>Consulte também [Adicionar a configuração](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)da nuvem.

Para configurar o externalizador do AEM:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Externalização de URLs](/help/sites-developing/externalizer.md).

1. Navegue até o console da Web OSGi em **https://&lt;servidor>:&lt;porta>/system/console/configMgr.**
1. Localize o Externalizador **de links CQ de** dia e insira o domínio do nó do autor.

   ![chlimage_1-120](assets/aem-externalizer-01.png)

