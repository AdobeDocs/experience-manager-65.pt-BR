---
title: Solução de problemas e perguntas frequentes do MSM
description: Descubra como solucionar os problemas mais comuns relacionados ao MSM e obter respostas para as perguntas mais comuns relacionadas ao MSM.
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
source-git-commit: 289c4644063504ec3c8e02d930933ad7260600f0
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 100%

---

# Solução de problemas e perguntas frequentes do MSM {#troubleshooting-msm}

## Primeiras etapas da solução de problemas {#first-steps}

Se você estiver enfrentando o que acredita ser um comportamento incorreto ou um erro no MSM, antes de começar e solucionar problemas detalhados, certifique-se de:

* Verificar as [Perguntas frequentes sobre o MSM](#faq), dado que os seus problemas ou dúvidas podem já ter sido abordados lá.
* Verificar o [Artigo de práticas recomendadas do MSM](msm-best-practices.md), dado que algumas dicas são oferecidas lá, juntamente com esclarecimentos sobre vários equívocos.

## Encontrar informações avançadas sobre seu blueprint e status da Live Copy {#advanced-info}

O MSM registra vários servlets que podem ser solicitados com seletores nos URLs do recurso. Eles são usados pela interface, mas também podem ser solicitados diretamente para ver os status de MSM computados avançados adicionais para suas páginas:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Use isso em uma página de blueprint para recuperar a lista de todas as Live Copies vinculadas a ela, com informações adicionais sobre o status da Live Copy.
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Use isso nas páginas de Live Copy para recuperar informações avançadas sobre suas conexões com as páginas de blueprint. Se a página não for uma Live Copy, nada será retornado.

Esses servlets geram mensagens de log DEBUG por meio do logger `com.day.cq.wcm.msm`, que também pode ser útil.

## Verificar informações específicas do MSM no repositório {#checking-repo}

Os servlets anteriores retornavam informações computadas com base nos nós e mixins específicos do MSM. As informações são armazenadas no repositório da seguinte maneira.

* Tipo de mixin `cq:LiveSync`
   * Isso é configurado em nós `jcr:content` e define páginas raiz da Live Copy.
   * Essas páginas terão um nó filho `cq:LiveSyncConfig` do tipo `cq:LiveCopy`, que conterá informações básicas e obrigatórias sobre a Live Copy por meio das seguintes propriedades:
      * `cq:master` aponta para a página de blueprint da Live Copy.
      * `cq:rolloutConfigs` indica as configurações de implementação ativas aplicadas à Live Copy.
      * `cq:isDeep` é verdadeiro se as páginas secundárias desta página raiz da Live Copy estiverem incluídas na Live Copy.
* Tipo de mixin `cq:LiveRelationship`
   * Qualquer página da Live Copy tem um tipo de mixin em seu nó `jcr:content`.
   * Caso contrário, em algum momento, a página foi desconectada ou criada manualmente por meio da interface de criação fora de uma ação de Live Copy (criar ou implantar).
* Tipo de mixin `cq:LiveSyncCancelled`
   * Adicionado aos nós `jcr:content` de páginas de Live Copy que foram suspensas.
   * Se a suspensão também for eficaz para páginas secundárias, uma propriedade `cq:isCancelledForChildren` é definida como verdadeira no mesmo nó.

As informações presentes nessas propriedades devem ser refletidas na interface, no entanto, ao solucionar problemas, pode ser útil observar o comportamento do MSM diretamente no repositório, à medida que as ações do MSM ocorrem.

Conhecer essas propriedades também pode ser útil para consultar seu repositório e descobrir conjuntos de páginas que estão em estados específicos. Por exemplo:

* `select * from cq:LiveSync` retorna todas as páginas raiz da Live Copy.

## Perguntas frequentes {#faq}

Aqui estão algumas perguntas frequentes relacionadas ao MSM e Live Copy.

### Por que algumas propriedades (por exemplo, título, anotações) não são atualizadas durante uma implantação do MSM? {#missing-properties}

As ações de sincronização do MSM são altamente configuráveis. Quais propriedades ou componentes são modificados durante as implantações dependem diretamente das propriedades dessas configurações.

Consulte [este artigo](msm-best-practices.md) para obter mais informações sobre este tópico.

### Como posso remover as permissões de implantação de um grupo de autores? {#remove-rollout-permissions}

Não há privilégio de **implantação** que possa ser definido ou removido para entidades principais do AEM (usuários ou grupos).

Como alternativa, você pode:

* Personalizar a interface do produto para ocultar as ações de implantação de um determinado principal.
* Remover privilégios de gravação da árvore da Live Copy para autores que não têm permissão de implantação.

### Por que vejo páginas da Live Copy com o sufixo “_msm_moved”? {#moved-pages}

Se uma página de blueprint for implantada, ela atualizará sua página da Live Copy ou criará uma nova página da Live Copy se ainda não existir (por exemplo, quando ela for implantada pela primeira vez ou a página da Live Copy for excluída manualmente).

Nesse último caso, no entanto, se uma página sem uma propriedade `cq:LiveRelationship` existir com o mesmo nome, ela será renomeada de acordo, antes que a página da Live Copy seja criada.

Por padrão, a implantação espera uma página vinculada da Live Copy, para a qual as atualizações dos blueprints serão implantadas ou nenhuma página, quando uma página da Live Copy for criada.

Se uma página “independente” for encontrada, o MSM optará por renomear esta página e criar uma página separada e vinculada da Live Copy.

Essa página independente, em uma subárvore da Live Copy, geralmente é o resultado de uma operação **Desconectar**, ou a antiga página da Live Copy foi excluída manualmente por um autor e depois recriada com o mesmo nome.

Para evitar isso, use o recurso **Suspender** da Live Copy, em vez de **Desconectar**. Veja mais detalhes sobre a ação **Desconectar** [neste artigo.](msm-livecopy.md)
