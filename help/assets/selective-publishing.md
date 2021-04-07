---
title: Trabalho com Publicação seletiva no Dynamic Media
description: Informações sobre como trabalhar com a Publicação seletiva no Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publicação
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 4%

---

# Configuração da publicação seletiva no nível da pasta no Dynamic Media {#selective-publish-configure-folder}

Você pode optar por publicar ou cancelar a publicação de ativos de ou para AEM ou Dynamic Media no nível da pasta, usando **[!UICONTROL Gerenciar publicação]** ou **[!UICONTROL Publicação rápida]** em vez de depender exclusivamente da **[!UICONTROL Configuração do Dynamic Media]** cujas configurações são globais para todas as pastas na instância do Dynamic Media.

Por exemplo, com a publicação seletiva, você pode trabalhar com ativos para produtos que ainda não estão ativos. Nesse caso, uma equipe de marketing pode acessar imagens de recorte inteligente e representações dinâmicas que são sincronizadas com o Dynamic Media para que possam criar materiais promocionais, tudo sem a necessidade de publicar esses ativos no Dynamic Media para entrega global.

>[!IMPORTANT]
>
>A Publicação seletiva só está disponível no modo Dynamic Media - Scene7 .

>[!NOTE]
>
>** Copiar ativos de e para pastas limpa o estado de publicação desses ativos. No entanto, quando você *move* ativos de e para pastas cuja propriedade de pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

Se posteriormente decidir alterar as configurações de **[!UICONTROL Publicação seletiva]** em uma pasta, essas alterações afetarão somente os novos ativos que você fizer upload para essa pasta a partir desse ponto. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente da caixa de diálogo **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]**.

A opção de nível de pasta **[!UICONTROL Modo de publicação do Dynamic Media]** sempre assume o padrão do valor encontrado na configuração **[!UICONTROL Publicar ativos]** em sua **[!UICONTROL Configuração do Dynamic Media.]** As etapas a seguir neste tópico, no entanto, mostram como alterar manualmente esse valor padrão no nível da pasta (conforme descrito nas etapas a seguir) para substituir o valor de  **[!UICONTROL Configuração do Dynamic Media]** .

Independentemente de você depender do valor **[!UICONTROL Publicar ativos]** definido em **[!UICONTROL Configuração do Dynamic Media]**, ou do valor **[!UICONTROL Modo de publicação do Dynamic Media]** definido nas propriedades no nível da pasta, você ainda poderá escolher **[!UICONTROL Imediatamente]**, **[!UICONTROL Após a ativação]**, ou &lt;a 10/>Publicação seletiva.**** Por exemplo, você pode definir o valor  **[!UICONTROL Publicar]** ativos na sua configuração do  **[!UICONTROL Dynamic Media como]** Na ativação **[!UICONTROL , mas definir o valor do]** Dynamic Media  **[!UICONTROL Publishmode no nível da pasta como Publicação]** seletiva ****, vice-versa e assim por diante.

Depois de configurar a publicação seletiva em uma pasta, você pode executar qualquer um dos seguintes procedimentos:

* [Publicar ativos no Dynamic Media ou AEM de maneira seletiva usando Gerenciar publicação.](#selective-publish-manage-publication)
* [Cancele a publicação seletiva de ativos do Dynamic Media ou do AEM usando Gerenciar publicação.](#selective-unpublish-manage-publication)
* [Publicar ativos no Dynamic Media ou AEM usando a Publicação rápida.](#quick-publish-aem-dm)
* [Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa.](#selective-publish-unpublish-search-results)

**Para configurar a publicação seletiva no nível da pasta no Dynamic Media**

1. Em AEM, toque no logotipo do AEM para acessar o console de navegação global. No lado esquerdo, toque no ícone Navegação (logo acima do ícone Ferramentas) e toque em **[!UICONTROL Ativos > Arquivos.]**
1. Faça uma das seguintes opções:
   * Editar as propriedades de uma pasta existente - Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, navegue até uma pasta cujas propriedades deseja editar. Selecione a pasta e, em seguida, na barra de ferramentas, toque em **[!UICONTROL Propriedades.]**
   * Edite as propriedades de uma nova pasta - Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, próximo ao canto superior direito da página, toque em **[!UICONTROL Criar > Pasta.]** Na caixa de diálogo  **[!UICONTROL Criar]** pasta, insira um título (obrigatório) para a pasta e toque em  **[!UICONTROL Criar.]** Selecione a pasta e, na barra de ferramentas, toque em  **[!UICONTROL Propriedades.]**

1. Na lista suspensa **[!UICONTROL Sync mode]**, selecione uma das seguintes opções:

   | Modo de sincronização | Descrição |
   | --- | --- |
   | **[!UICONTROL Herdado]** | Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão definido em sua **[!UICONTROL Configuração do Dynamic Media.]** O status detalhado de  **** Herdado é exibido por meio de uma dica de ferramenta. |
   | **[!UICONTROL Sincronizar tudo nesta subárvore da pasta à mídia dinâmica]** | Para que a publicação no Dynamic Media seja bem-sucedida, os ativos devem ser sincronizados com o Dynamic Media. Selecionar essa opção incluirá todos os ativos nesta subárvore para sincronizar com o Dynamic Media. As configurações específicas da pasta substituem a configuração padrão na **[!UICONTROL Configuração do Dynamic Media.]** |
   | **[!UICONTROL Excluir tudo nesta subárvore de pastas da sincronização de dynamicmedia]** | Exclua todos os ativos nesta subárvore da sincronização com o Dynamic Media. |

   ![Publicação seletiva no nível da pasta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Na lista suspensa **[!UICONTROL Dynamic Media Publish mode]** , selecione uma opção. Esteja ciente de que a opção **[!UICONTROL Dynamic Media Publish mode]** sempre assume o valor padrão definido na **[!UICONTROL Dynamic Media Configuration.]** No entanto, você pode substituir manualmente esse valor padrão de  **[!UICONTROL Dynamic Media]** Configuration usando uma das opções a seguir.

   >[!IMPORTANT]
   >
   >Esteja ciente de que, independentemente da opção do modo de Publicação do Dynamic Media selecionada, quaisquer atualizações feitas posteriormente em um ativo *já* publicado, essas atualizações são publicadas imediatamente sem nenhuma ação adicional do usuário.

   | Opção do modo de publicação do Dynamic Media | Descrição |
   | --- | --- |
   | **[!UICONTROL Imediatamente]** | Quando os ativos são carregados nessa pasta, o sistema assimila os ativos no AEM e fornece o URL/Incorporação instantaneamente. Essa opção está vinculada AEM publicação somente e não há intervenção do usuário necessária para publicar ativos.<br>Essa opção  ** não estará disponível se você tiver selecionado  **[!UICONTROL Excluir tudo nesta subárvore de pastas da]** sincronização de dinamicmedia no modo  **[!UICONTROL Sincronizar]** na etapa anterior. |
   | **[!UICONTROL Por ativação]** | Quando os ativos são carregados nessa pasta, é necessário publicar explicitamente o ativo primeiro antes que um link de URL/Incorporar seja fornecido. Essa opção está vinculada apenas AEM publicação.<br>Essa opção  ** não estará disponível se você tiver selecionado  **[!UICONTROL Excluir tudo nesta subárvore de pastas da]** sincronização de dinamicmedia no modo  **[!UICONTROL Sincronizar]** na etapa anterior. |
   | **[!UICONTROL Publicação seletiva]** | Os ativos são publicados à sua escolha do AEM ou da Dynamic Media para entrega no domínio público. Ambos os métodos de publicação são mutuamente exclusivos.  Ou seja, você pode publicar ativos no DMS7 para usar recursos como Recorte inteligente ou representações dinâmicas. Ou, você pode publicar ativos exclusivamente para AEM para pré-visualização segura; esses mesmos ativos são *not* publicados no DMS7 para entrega no domínio público. Essa opção não estará disponível se você tiver selecionado **[!UICONTROL Exclude all in this folder sub-tree from dynamicmedia sync]** em **[!UICONTROL Sync mode]** na etapa anterior. |

1. No canto superior direito da página, toque em **[!UICONTROL Salvar e fechar]** e toque em **[!UICONTROL OK]** para retornar ao AEM Assets.

## Publicar ativos no Dynamic Media ou AEM de maneira seletiva usando Gerenciar publicação{#selective-publish-manage-publication}

Antes de usar **[!UICONTROL Gerenciar publicação]** para publicar ativos seletivamente no Dynamic Media ou para AEM, certifique-se de ter definido a opção **[!UICONTROL Publicar ativos]** em **[!UICONTROL Configuração do Dynamic Media]** para **[!UICONTROL Publicação seletiva]** ou configurado a publicação seletiva no nível da pasta.

Consulte [Criação de uma Configuração do Dynamic Media](#configuring-dynamic-media-cloud-services) ou [Configuração da publicação seletiva no nível da pasta no Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>A Publicação seletiva só está disponível no modo Dynamic Media - Scene7 .

>[!NOTE]
>
>** Copiar ativos de e para pastas limpa o estado de publicação desses ativos. No entanto, quando você *move* ativos de e para pastas cuja propriedade de pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

**Para publicar ativos seletivamente no Dynamic Media ou AEM usando Gerenciar publicação**

1. Em AEM, toque no logotipo do AEM para acessar o console de navegação global. No lado esquerdo, toque no ícone Navegação (logo acima do ícone Ferramentas) e toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, siga um destes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]**  Você pode achar útil usar a  **[!UICONTROL Visualização de]** lista para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]** Você pode achar útil usar a  **[!UICONTROL Visualização de]** lista para verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gerenciar publicação]** não for exibido na barra de ferramentas, toque no botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu da lista.

1. Na página **[!UICONTROL Gerenciar publicação - Opções]**, em **[!UICONTROL Ação]**, selecione o tipo de ativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Publicar]**  (para AEM) | Selecione essa opção para publicar ativos no AEM para pré-visualização segura. |
   | **[!UICONTROL Publicar no Dynamic Media]** | Selecione essa opção para publicar ativos no Dynamic Media para entrega no domínio público ou para usar recursos como Recorte inteligente ou representações dinâmicas.<br>Essa opção só estará disponível se o modo de Publicação do  **[!UICONTROL Dynamic Media estiver definido como]** Publicação  **** seletiva nas propriedades da pasta. |

1. Em **[!UICONTROL Schedule]**, defina o tempo da publicação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para publicar os ativos imediatamente. |
   | **[!UICONTROL Posteriomente]** | Selecione para publicar os ativos em uma data e hora específica. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação]**, toque em **[!UICONTROL Próximo.]**
1. Na página **[!UICONTROL Gerenciar publicação - Escopo]** , siga um destes procedimentos:

   * Se necessário, selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar publicação - Escopo]**, toque em **[!UICONTROL Publicar]** ou **[!UICONTROL Publicar no Dynamic Media.]**
1. Toque em **[!UICONTROL OK.]**

### Cancelar a publicação seletiva de ativos do Dynamic Media ou do AEM usando Gerenciar publicação {#selective-unpublish-manage-publication}

1. Em AEM, toque no logotipo do AEM para acessar o console de navegação global. No lado esquerdo, toque no ícone Navegação (logo acima do ícone Ferramentas) e toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, siga um destes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]**  Você pode achar útil usar a  **[!UICONTROL Visualização de]** lista para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]** Você pode achar útil usar a  **[!UICONTROL Visualização de]** lista para verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gerenciar publicação]** não for exibido na barra de ferramentas, toque no botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu da lista.

1. Na página **[!UICONTROL Gerenciar publicação - Opções]**, em **[!UICONTROL Ação]**, selecione o tipo de desativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Cancelar publicação]**  (do AEM) | Selecione essa opção para cancelar a publicação de ativos do AEM. |
   | **[!UICONTROL Desfazer publicação no Dynamic Media]** | Selecione essa opção para cancelar a publicação de ativos do Dynamic Media.<br>Essa opção só estará disponível se o modo de Publicação do  **[!UICONTROL Dynamic Media estiver definido como]** Publicação  **** seletiva nas propriedades da pasta. |

1. Em **[!UICONTROL Schedule]**, defina o tempo da desativação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para cancelar a publicação dos ativos imediatamente. |
   | **[!UICONTROL Posteriomente]** | Selecione para desfazer a publicação dos ativos em uma data e hora específica. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação]**, toque em **[!UICONTROL Próximo.]**
1. Na página **[!UICONTROL Gerenciar publicação - Escopo]** , siga um destes procedimentos:
   * Selecione um ou mais ativos que deseja remover do cancelamento da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar publicação - Escopo]**, toque em **[!UICONTROL Cancelar publicação]** ou **[!UICONTROL Cancelar publicação do Dynamic Media.]**
1. Toque em **[!UICONTROL OK.]**

## Publicar ativos no Dynamic Media ou AEM usando a Publicação rápida {#quick-publish-aem-dm}

Você pode usar **[!UICONTROL Publicação rápida]** para casos simples de ativação de ativos. **[!UICONTROL A]** Publicação rápida publica os ativos selecionados imediatamente, sem qualquer outra interação do usuário. Por isso, todas as referências não publicadas também são publicadas automaticamente.

>[!NOTE]
>
>Para usar **[!UICONTROL Publicação rápida]** para publicar ativos no Dynamic Media ou AEM, certifique-se de que **[!UICONTROL Publicação seletiva]** esteja ativada em seu **[!UICONTROL Configuração do Dynamic Media]** ou nas propriedades da pasta da pasta selecionada.

**Publicar ativos no Dynamic Media ou AEM usando a Publicação rápida**

1. Em AEM, toque no logotipo do AEM para acessar o console de navegação global. No lado esquerdo da página, toque no ícone Navegação (logo acima do ícone Ferramentas) e, no lado direito da página, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, siga um destes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Publicação rápida.]**  Você pode achar útil usar a  **[!UICONTROL Visualização de]** lista para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, toque em **[!UICONTROL Publicação rápida.]** Você pode achar útil usar a  **[!UICONTROL Visualização de]** lista para verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >Se **[!UICONTROL Publicação rápida]** não for exibido na barra de ferramentas, toque no botão de reticências e selecione **[!UICONTROL Publicação rápida]** no menu da lista.

      ![Publicação rápida em nível de pasta no Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selecione uma das seguintes opções na lista de menu **[!UICONTROL Publicação rápida]**.

   | Opção Publicação rápida | O que ele faz |
   | --- | --- | 
   | Publicar no AEM | Publica os ativos selecionados imediatamente no AEM. |
   | Publicar no Brand Portal | Publica os ativos selecionados imediatamente no **[!UICONTROL Brand Portal.]**<br>Essa opção só estará disponível se a instância do AEM Assets tiver o**[!UICONTROL  Brand ]**Portalial configurado. |
   | Publicar no Dynamic Media | Publica os ativos selecionados imediatamente no Dynamic Media.<br>Um ativo já deve ser sincronizado com o Dynamic Media. Se necessário, verifique se **[!UICONTROL Modo de sincronização]** nas propriedades de uma pasta já está definido como **[!UICONTROL Sincronizar tudo nesta subárvore de pasta para dynamicmedia.]** |

1. Toque em **[!UICONTROL OK]** e toque em **[!UICONTROL Fechar.]**

## Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa {#selective-publish-unpublish-search-results}

Os resultados da pesquisa podem mostrar ativos de várias pastas de ativos que têm diferentes configurações de publicação do Dynamic Media. Onde você selecionou um ou mais ativos dos resultados da pesquisa e os ativos têm configurações diferentes do modo de publicação do Dynamic Media, é possível acionar **[!UICONTROL Gerenciar publicação]** na barra de ferramentas para publicar ou desfazer a publicação.

Consulte também [Pesquisar ativos no AEM.](/help/assets/search-assets.md)

**Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa**

1. Em AEM, no canto superior esquerdo da página, toque no logotipo do AEM para acessar o console de navegação global. No lado esquerdo da página, toque no ícone Navegação (logo acima do ícone Ferramentas) e toque em **[!UICONTROL Ativos > Arquivos.]**
1. Na barra de ferramentas, próximo ao canto superior direito da página, toque no ícone Pesquisar (lupa).
1. No campo de texto **[!UICONTROL Type to search]**, digite uma palavra-chave e pressione **[!UICONTROL Enter.]**
1. Próximo ao canto superior direito da página, toque no ícone **[!UICONTROL Exibição de lista]**.
1. Próximo ao canto superior esquerdo da página, toque no ícone **[!UICONTROL Filters]**.

   ![Exibição de lista e filtros em resultados de pesquisa](/help/assets/assets-dm/select-publish-search-result.png)

1. No painel esquerdo, expanda **[!UICONTROL Status]** e expanda o **[!UICONTROL predicado de pesquisa do Dynamic Media]**.
1. Use as caixas de seleção **[!UICONTROL Published]** e **[!UICONTROL Unpublished]** para refinar ainda mais os resultados da pesquisa com base no estado publicado dos ativos do Dynamic Media.
Como opção, você pode usar essas caixas de seleção junto com o predicado de pesquisa **[!UICONTROL Publicar]** para refinar os resultados da pesquisa dos ativos de AEM **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]**.
1. Faça uma das seguintes opções:
   * Selecione um ou mais ativos que deseja publicar ou cancelar a publicação.
   * Próximo ao canto superior direito da página **[!UICONTROL Resultados da Pesquisa]**, toque em **[!UICONTROL Selecionar Tudo.]**
1. Na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]** Talvez seja necessário tocar no ícone de reticências na barra de ferramentas para ver  **[!UICONTROL Gerenciar publicação.]**
1. Na página **[!UICONTROL Gerenciar publicação - Opções]**, selecione a ação desejada.

   | Ação selecionada | Publicar ativos na configuração do Dynamic Media | Os ativos são |
   | --- | --- | --- |
   | Publicação | Imediatamente ou após a ativação | Publicado no AEM e no Dynamic Media. |
   | Publicação | Publicação seletiva | Publicado somente em AEM. |
   | Desfazer publicação | Imediatamente ou após a ativação | Não publicado do AEM e Dynamic Media. |
   | Desfazer publicação | Publicação seletiva | Não publicado somente no AEM. |
   | Publicar no Dynamic Media | Imediatamente ou após a ativação | Não publicado no AEM, no Dynamic Media ou em ambos. |
   | Publicar no Dynamic Media | Publicação seletiva | Publicado somente no Dynamic Media. |
   | Desfazer publicação no Dynamic Media | Imediatamente ou após a ativação | Não foi cancelada a publicação do AEM, Dynamic Media ou ambos. |
   | Desfazer publicação no Dynamic Media | Publicação seletiva | Não publicado somente no Dynamic Media. |

1. Em **[!UICONTROL Schedule]**, defina o tempo da desativação.

   | Horário selecionado | O que acontece |
   | --- | --- |
   | Agora | A ação selecionada é executada imediatamente. |
   | Posteriomente | A ação selecionada é executada na data e hora específicas selecionadas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação - Opções]**, toque em **[!UICONTROL Próximo.]**
1. (Opcional) Na página **[!UICONTROL Gerenciar publicação - Escopo]**, revise a coluna **[!UICONTROL Publicar meta]** na tabela para os ativos selecionados.

   | Publicar ativos na configuração do Dynamic Media | Ação selecionada | Direcionamento da publicação |
   | --- | --- | --- |
   | Imediatamente ou <br>Após ativação | Publicação | AEM e Dynamic Media |
   | Imediatamente ou <br>Após ativação | Publicar no Dynamic Media | Nenhum |
   | Publicação seletiva | Publicação | AEM |
   | Publicação seletiva | Publicar no Dynamic Media | Dynamic Media |
   | Imediatamente ou <br>Após ativação | Desfazer publicação | AEM e Dynamic Media |
   | Imediatamente ou <br>Após ativação | Desfazer publicação no Dynamic Media | Nenhum |
   | Publicação seletiva | Desfazer publicação | AEM |
   | Publicação seletiva | Desfazer publicação no Dynamic Media | Dynamic Media |

1. Na página **[!UICONTROL Gerenciar publicação - Escopo]** , siga um destes procedimentos:
   * Selecione um ou mais ativos que deseja remover da publicação ou do cancelamento da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar publicação - Escopo]**, toque em **[!UICONTROL Publicar]** ou **[!UICONTROL Cancelar publicação]** para iniciar a ação.
1. Toque em **[!UICONTROL OK.]**

## Verificar o status de publicação de um ativo {#check-publish-status-of-asset}

Você pode usar **[!UICONTROL Linha do tempo]** com **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]** no AEM para verificar rapidamente o estado de publicação de um ativo.

**Para verificar o status de publicação de um ativo**

1. Em AEM, no canto superior esquerdo da página, toque no logotipo do AEM para acessar o console de navegação global. No lado esquerdo da página, toque no ícone Navegação (logo acima do ícone Ferramentas) e toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]** (captura de tela abaixo mostra a **[!UICONTROL Exibição de lista]**), abra uma pasta que contenha ativos publicados ou não publicados.
1. Selecione um ativo para que ele seja exibido com uma marca de seleção. Veja a captura de tela abaixo, por exemplo.
1. Próximo ao canto superior esquerdo da página, no menu suspenso, selecione **[!UICONTROL Linha do tempo.]** A  **** região Status no painel esquerdo mostra o estado de publicação do ativo selecionado.
Quando você usa **[!UICONTROL Exibição de lista]**, uma coluna adicional para **[!UICONTROL Dynamic Media]** estado de publicação é exibida.
   * Uma pasta configurada para sincronizar com o Dynamic Media exibirá a coluna **[!UICONTROL Dynamic Media]** por padrão.
   * Uma pasta *not* configurada para sincronizar com o Dynamic Media não exibirá a coluna Dynamic Media.
      ![Exibição de lista e linha do tempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solução de problemas de publicação seletiva {#selective-publish-troubleshoot}

Um ativo que não está sincronizado com o Dynamic Media, mas tem uma ação de publicação do Dynamic Media acionada nele, resulta na seguinte mensagem de erro e solução:

![Erro de publicação seletiva](/help/assets/assets-dm/selective-publish-error.png)
