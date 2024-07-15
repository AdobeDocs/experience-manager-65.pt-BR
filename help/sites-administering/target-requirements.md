---
title: Pré-requisitos para integração com o Adobe Target
description: Saiba mais sobre os pré-requisitos para integração com o Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---

# Pré-requisitos para integração com o Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte da [integração de AEM e Adobe Target](/help/sites-administering/target.md), é necessário se registrar no Adobe Target, definir o agente de replicação e as configurações de atividade segura no nó de publicação.

## Registro no Adobe Target {#registering-with-adobe-target}

Para integrar o AEM ao Adobe Target, é necessário ter uma conta válida do Adobe Target. Esta conta deve ter no mínimo o nível de permissões **aprovador**. Ao se registrar na Adobe Target, você recebe um código de cliente. Você precisa do código de cliente e seu nome de logon e senha do Adobe Target para se conectar ao AEM ao Adobe Target.

O código do cliente identifica a conta de cliente do Adobe Target ao chamar o servidor do Adobe Target.

>[!NOTE]
>
>Sua conta também deve ser habilitada pela equipe do Target para usar a integração.
>
>Se esse não for o caso, entre em contato com o [Atendimento ao cliente do Adobe](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Habilitar o Agente de replicação de destino {#enabling-the-target-replication-agent}

O [agente de replicação](/help/sites-deploying/replication.md) de Teste e Destino deve estar habilitado na instância do autor. Observe que esse agente de replicação não está habilitado por padrão se você usou o modo de execução [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) para instalar o AEM. Para obter mais informações sobre como proteger seu ambiente de produção, consulte a [Lista de Verificação de Segurança](/help/sites-administering/security-checklist.md).

1. Na página inicial do AEM, clique em **Ferramentas** > **Implantação** > **Replicação**.
1. Clique Em **Agentes No Autor**.
1. Clique no agente de replicação **Testar e Destino (teste e destino)** e em **Editar**.
1. Selecione a opção Habilitado e clique em **OK**.

   >[!NOTE]
   >
   >Ao configurar o agente de replicação de Teste e Destino, na guia **Transporte**, o URI é definido por padrão como **tnt:///**. Não substitua este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Se você tentar testar a conexão com **tnt:///**, ocorrerá um erro. Este comportamento é esperado, pois este URI é somente para uso interno; não use com **Testar Conexão**.

## Protegendo o nó de configurações da atividade {#securing-the-activity-settings-node}

Proteja o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que não possa ser acessado por usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.

O nó **cq:ActivitySettings** está disponível no CRXDE lite em `/content/campaigns/*nameofbrand*`* *no nó jcr:content de atividades;* *por exemplo, `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Esse nó só é criado depois de direcionar um componente.

O nó **cq:ActivitySettings** no jcr:content da atividade está protegido pelas seguintes ACLs:

* Negar tudo para todos
* Permitir jcr:read,rep:write para &quot;target-activity-author&quot; (o autor é um membro desse grupo pronto para uso)
* Permitir jcr:read,rep:write para &quot;targetservice&quot;

Essas configurações garantem que os usuários normais não tenham acesso às propriedades do nó. Use as mesmas ACLs no autor e na publicação. Consulte [Administração e Segurança do Usuário](/help/sites-administering/security.md) para obter mais informações.

## Configurar o Externalizador de links de AEM {#configuring-the-aem-link-externalizer}

Ao editar uma atividade no Adobe Target, a URL aponta para **localhost**, a menos que você altere a URL no nó do autor AEM. Você pode configurar o Externalizador de links AEM se quiser que o conteúdo exportado aponte para um domínio *publicar* específico.

>[!NOTE]
>
>Consulte também [Adicionar a configuração da nuvem](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Para configurar o externalizador de AEM:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Externalizar URLs](/help/sites-developing/externalizer.md).

1. Navegue até o console da Web do OSGi em **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Localize o **Day CQ Link Externalizer** e insira o domínio para o nó do autor.

   ![Externalizador de links CQ de dias](assets/aem-externalizer-01.png)
