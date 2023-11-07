---
title: Pré-requisitos para integração com o Adobe Target
description: Saiba mais sobre os pré-requisitos para integração com o Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 7%

---

# Pré-requisitos para integração com o Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte da [integração do AEM e do Adobe Target](/help/sites-administering/target.md), você precisa se registrar no Adobe Target, definir o agente de replicação e as configurações de atividade segura no nó de publicação.

## Registro no Adobe Target {#registering-with-adobe-target}

Para integrar o AEM ao Adobe Target, é necessário ter uma conta válida do Adobe Target. Esta conta deve ter **aprovador** no mínimo, permissões de nível. Ao se registrar na Adobe Target, você recebe um código de cliente. Você precisa do código de cliente e seu nome de logon e senha do Adobe Target para se conectar ao AEM ao Adobe Target.

O código do cliente identifica a conta de cliente do Adobe Target ao chamar o servidor do Adobe Target.

>[!NOTE]
>
>Sua conta também deve ser habilitada pela equipe do Target para usar a integração.
>
>Se não for o caso, entre em contato com [Atendimento ao cliente Adobe](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Habilitar o Agente de replicação de destino {#enabling-the-target-replication-agent}

O teste e o target [agente de replicação](/help/sites-deploying/replication.md) deve ser ativado na instância do autor. Observe que esse agente de replicação não estará ativado por padrão se você tiver usado o [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) modo de execução para instalação do AEM. Para obter mais informações sobre como proteger seu ambiente de produção, consulte [Lista de verificação de segurança](/help/sites-administering/security-checklist.md).

1. Na página inicial do AEM, clique ou toque em **Ferramentas** > **Implantação** > **Replicação**.
1. Clique ou toque **Agentes Sobre O Autor**.
1. Clique ou toque no **Teste e Target (teste e target)** e, em seguida, clique ou toque em **Editar**.
1. Selecione a opção Ativado e clique ou toque em **OK**.

   >[!NOTE]
   >
   >Ao configurar o agente de replicação de Teste e Destino, na variável **Transporte** , o URI é definido por padrão como **tnt:///**. Não substituir este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Se você tentar testar a conexão com o **tnt:///**, ele emite um erro. Esse comportamento é esperado, pois esse URI é somente para uso interno; não use com **Testar conexão**.

## Protegendo o nó de configurações da atividade {#securing-the-activity-settings-node}

Você deve proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.

A variável **cq:ActivitySettings** O nó está disponível no CRXDE lite em `/content/campaigns/*nameofbrand*`* *no nó activities jcr:content;* *por exemplo, `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Esse nó só é criado depois de direcionar um componente.

A variável **cq:ActivitySettings** no jcr:content da atividade é protegido pelas seguintes ACLs:

* Negar tudo para todos
* Permitir jcr:read,rep:write para &quot;target-activity-author&quot; (o autor é um membro desse grupo pronto para uso)
* Permitir jcr:read,rep:write para &quot;targetservice&quot;

Essas configurações garantem que os usuários normais não tenham acesso às propriedades do nó. Use as mesmas ACLs no autor e na publicação. Consulte [Administração e segurança do usuário](/help/sites-administering/security.md) para obter mais informações.

## Configurar o Externalizador de links de AEM {#configuring-the-aem-link-externalizer}

Ao editar uma atividade no Adobe Target, o URL aponta para **localhost** a menos que você altere o URL no nó do autor AEM. Você pode configurar o Externalizador de links AEM se quiser que o conteúdo exportado aponte para um *publicar* domínio.

>[!NOTE]
>
>Consulte também [Adicionar a configuração da nuvem](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Para configurar o externalizador de AEM:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Externalizar URLs](/help/sites-developing/externalizer.md).

1. Navegue até o console OSGi da Web em **https://&lt;server>:&lt;port>/system/console/configMgr**
1. Localizar **Day CQ Link Externalizer** e insira o domínio para o nó do autor.

   ![Day CQ Link Externalizer](assets/aem-externalizer-01.png)
