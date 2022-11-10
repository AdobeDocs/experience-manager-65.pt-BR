---
title: Pré-requisitos para integração com o Adobe Target
seo-title: Prerequisites for Integrating with Adobe Target
description: Descubra os pré-requisitos para integração com o Adobe Target.
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 7%

---

# Pré-requisitos para integração com o Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte do [integração do AEM e do Adobe Target](/help/sites-administering/target.md), você precisa se registrar no Adobe Target, configurar o agente de replicação e as configurações de atividade segura no nó de publicação.

## Registro no Adobe Target {#registering-with-adobe-target}

Para integrar o AEM com o Adobe Target, você deve ter uma conta válida do Adobe Target. Essa conta deve ter **aprovador** permissões de nível mínimo. Ao se registrar no Adobe Target, você recebe um código de cliente. Você precisa do código de cliente e do nome de logon e senha da Adobe Target para se conectar AEM Adobe Target.

O Código do cliente identifica a conta do cliente do Adobe Target ao chamar o servidor do Adobe Target.

>[!NOTE]
>
>Sua conta também deve estar habilitada pela equipe do Target para usar a integração.
>
>Se não for o caso, entre em contato com o [Atendimento ao cliente do Adobe](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Ativar o agente de replicação do Target {#enabling-the-target-replication-agent}

O teste e o direcionamento [agente de replicação](/help/sites-deploying/replication.md) deve ser ativado na instância do autor. Observe que esse agente de replicação não será habilitado por padrão se você tiver usado a variável [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) modo de execução para instalar o AEM. Para obter mais informações sobre como proteger seu ambiente de produção, consulte a [Lista de verificação de segurança](/help/sites-administering/security-checklist.md).

1. Na AEM página inicial, clique ou toque em **Ferramentas** > **Implantação** > **Replicação**.
1. Clique ou toque em **Agentes No Autor**.
1. Clique ou toque no **Test and Target (teste e target)** agente de replicação e, em seguida, clique ou toque em **Editar**.
1. Selecione a opção Ativado e clique ou toque em **OK**.

   >[!NOTE]
   >
   >Quando você configura o agente de replicação do Test e do Target, no **Transportes** , o URI é definido por padrão como **tnt:///**. Não substitua este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Observe que, se você tentar testar a conexão com o **tnt:///**, isso gerará um erro. Esse comportamento é esperado, pois esse URI é somente para uso interno e não deve ser usado com **Testar conexão**.

## Proteção do nó Configurações da atividade {#securing-the-activity-settings-node}

Você deve proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.

O **cq:ActivitySettings** nó está disponível no CRXDE lite em `/content/campaigns/*nameofbrand*`* *nas atividades jcr:content node;* *por exemplo `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Esse nó só é criado depois de direcionar um componente.

O **cq:ActivitySettings** nó sob a atividade jcr:content é protegido pelas seguintes ACLs:

* Negar tudo para todos
* Permitir jcr:read,rep:write para &quot;target-activity-authors&quot; (o autor é um membro deste grupo pronto para uso)
* Permitir jcr:read,rep:write para &quot;targetservice&quot;

Essas configurações garantem que os usuários normais não tenham acesso às propriedades do nó. Use as mesmas ACLs no autor e na publicação. Consulte [Administração e segurança do usuário](/help/sites-administering/security.md) para obter mais informações.

## Configurar o AEM Link Externalizer {#configuring-the-aem-link-externalizer}

Ao editar uma atividade no Adobe Target, o URL aponta para **localhost** a menos que você altere o URL no nó do autor do AEM. Você pode configurar o AEM Link Externalizer se deseja que o conteúdo exportado aponte para um *publicar* domínio.

>[!NOTE]
>
>Consulte também [Adicionar a configuração da nuvem](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Para configurar o AEM externalizador:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Exteriorização de URLs](/help/sites-developing/externalizer.md).

1. Navegue até o console da Web OSGi em **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Localizar **Externalizador de links CQ do dia** e insira o domínio do nó do autor.

   ![chlimage_1-120](assets/aem-externalizer-01.png)
