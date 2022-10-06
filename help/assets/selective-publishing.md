---
title: Trabalhar com publicação seletiva no Dynamic Media
description: Você pode optar por publicar ou cancelar a publicação de ativos de ou para o Adobe Experience Manager ou Dynamic Media no nível da pasta. Você pode usar a opção Gerenciar publicação ou Publicação rápida em vez de depender exclusivamente da Configuração do Dynamic Media cujas configurações são globais para todas as pastas na instância do Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 664e22cc4c6acd74f285a4ec1a0dbd7d301240b7
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 4%

---

# Configurar publicação seletiva no nível da pasta no Dynamic Media {#selective-publish-configure-folder}

Você pode optar por publicar ou cancelar a publicação de ativos de ou para o Adobe Experience Manager ou Dynamic Media no nível da pasta. Você pode usar **[!UICONTROL Gerenciar publicação]** ou **[!UICONTROL Publicação rápida]** em vez de depender exclusivamente da **[!UICONTROL Configuração do Dynamic Media]** cujas configurações são globais para todas as pastas na instância do Dynamic Media.

Por exemplo, com a publicação seletiva, você pode trabalhar com ativos para produtos que ainda não estão ativos. Nesse caso, uma equipe de marketing pode acessar imagens de recorte inteligente e representações dinâmicas que são sincronizadas com o Dynamic Media. Eles podem criar materiais promocionais, tudo sem a necessidade de publicar esses ativos na Dynamic Media para entrega global.

>[!IMPORTANT]
>
>A Publicação seletiva só está disponível no modo Dynamic Media - Scene7 .

>[!NOTE]
>
>*Copiando* os ativos de e para pastas apaga o estado de publicação desses ativos. No entanto, quando você *mover* ativos de e para pastas cuja propriedade de pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

Se você decidir alterar posteriormente a variável **[!UICONTROL Publicação seletiva]** em uma pasta, essas alterações afetam somente os novos ativos que você faz upload dessa pasta a partir desse ponto. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente de **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]** caixa de diálogo.

O nível da pasta **[!UICONTROL Modo de publicação do Dynamic Media]** sempre assume o padrão do valor encontrado na variável **[!UICONTROL Publicar ativos]** na sua **[!UICONTROL Configuração do Dynamic Media]**. No entanto, as etapas a seguir neste tópico mostram como alterar manualmente esse valor padrão no nível da pasta (conforme descrito nas etapas a seguir) para substituir a variável **[!UICONTROL Configuração do Dynamic Media]** valor.

Independentemente de você depender de uma das seguintes opções:

* **[!UICONTROL Publicar ativos]** valor definido em **[!UICONTROL Configuração do Dynamic Media]**.
* **[!UICONTROL Modo de publicação do Dynamic Media]** conjunto de valores em propriedades no nível da pasta.

Você pode escolher **[!UICONTROL Imediatamente]**, **[!UICONTROL Na ativação]** ou **[!UICONTROL Publicação seletiva]**. Por exemplo, é possível definir a variável **[!UICONTROL Publicar ativos]** no seu **[!UICONTROL Configuração do Dynamic Media]** para **[!UICONTROL Na ativação]**, mas defina a variável **[!UICONTROL Publicação no Dynamic Media]** valor do modo no nível da pasta para **[!UICONTROL Publicação seletiva]** e, por outro lado.

Depois de configurar a publicação seletiva em uma pasta, você pode executar qualquer um dos seguintes procedimentos:

* [Publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação](#selective-publish-manage-publication).
* [Cancelar a publicação seletiva de ativos do Dynamic Media ou do Experience Manager usando Gerenciar publicação](#selective-unpublish-manage-publication).
* [Publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida](#quick-publish-aem-dm).
* [Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa](#selective-publish-unpublish-search-results).

**Para configurar a publicação seletiva no nível da pasta no Dynamic Media:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas) e selecione **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Siga uma das seguintes opções:
   * Edite as propriedades de uma pasta existente - Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, navegue até uma pasta cujas propriedades deseja editar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
   * Edite as propriedades de uma nova pasta - Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, próximo ao canto superior direito da página, selecione **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**. No **[!UICONTROL Criar pasta]** , insira um título (obrigatório) para a pasta e selecione **[!UICONTROL Criar]**. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.

1. No **[!UICONTROL Modo de sincronização]** selecione uma das seguintes opções:

   | Modo de sincronização | Descrição |
   | --- | --- |
   | **[!UICONTROL Herdado]** | Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão definido em seu **[!UICONTROL Configuração do Dynamic Media]**. O status detalhado de **[!UICONTROL Herdado]** é exibido por meio de uma dica de ferramenta. |
   | **[!UICONTROL Sincronizar tudo nesta subárvore de pastas com o Dynamic Media]** | Para que a publicação no Dynamic Media seja bem-sucedida, os ativos devem ser sincronizados com o Dynamic Media. A seleção dessa opção inclui todos os ativos nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem a configuração padrão no **[!UICONTROL Configuração do Dynamic Media]**. |
   | **[!UICONTROL Excluir tudo nesta subárvore de pastas da sincronização Dynamic Media]** | Exclua todos os ativos nesta subárvore da sincronização com o Dynamic Media. |

   ![Publicação seletiva no nível da pasta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. No **[!UICONTROL Modo de publicação do Dynamic Media]** selecione uma opção na lista suspensa. O **[!UICONTROL Modo de publicação do Dynamic Media]** sempre assume o padrão do valor definido na variável **[!UICONTROL Configuração do Dynamic Media]**. No entanto, você pode substituir manualmente esse padrão **[!UICONTROL Configuração do Dynamic Media]** usando uma das opções a seguir.

   >[!IMPORTANT]
   >
   >Independentemente da opção do modo de Publicação do Dynamic Media selecionada, as atualizações que você fizer posteriormente em um ativo que seja *já* publicadas, essas atualizações são publicadas imediatamente sem nenhuma outra ação do usuário.
   >
   >Se um vídeo publicado for atualizado, ele deverá ser publicado novamente para refletir as alterações no delivery.

   | Opção do modo de publicação do Dynamic Media | Descrição |
   | --- | --- |
   | **[!UICONTROL Imediatamente]** | Quando os ativos são carregados nessa pasta, o sistema assimila os ativos no Experience Manager e fornece o URL/Incorporação instantaneamente. Essa opção está vinculada apenas à publicação do Experience Manager e não há necessidade de intervenção do usuário para publicar ativos.<br>Esta opção é *not* disponível se você selecionou **[!UICONTROL Excluir tudo nesta subárvore de pastas da sincronização Dynamic Media]** em **[!UICONTROL Modo de sincronização]** na etapa anterior. |
   | **[!UICONTROL Por ativação]** | Quando os ativos são carregados nessa pasta, você deve publicar explicitamente o ativo primeiro antes que um link URL/Incorporar seja fornecido. Essa opção está vinculada apenas à publicação do Experience Manager.<br>Esta opção é *not* disponível se você selecionou **[!UICONTROL Excluir tudo nesta subárvore de pastas da sincronização Dynamic Media]** em **[!UICONTROL Modo de sincronização]** na etapa anterior. |
   | **[!UICONTROL Publicação seletiva]** | Os ativos são publicados à sua escolha do Experience Manager ou da Dynamic Media para entrega no domínio público. Ambos os métodos de publicação são mutuamente exclusivos. Ou seja, você pode publicar ativos no DMS7 para usar recursos como Recorte inteligente ou representações dinâmicas. Ou, você pode publicar ativos exclusivamente no Experience Manager para visualização segura; esses mesmos ativos *not* publicado no DMS7 para entrega no domínio público. Essa opção não estará disponível se você tiver selecionado **[!UICONTROL Excluir tudo nesta subárvore de pastas da sincronização Dynamic Media]** em **[!UICONTROL Modo de sincronização]** na etapa anterior. |

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**, em seguida selecione **[!UICONTROL OK]** para retornar ao Experience Manager Assets.

## Publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação{#selective-publish-manage-publication}

Antes de utilizar **[!UICONTROL Gerenciar publicação]** para publicar ativos seletivamente no Dynamic Media ou no Experience Manager, certifique-se de definir um dos seguintes itens:

* O **[!UICONTROL Publicar ativos]** em **[!UICONTROL Configuração do Dynamic Media]** para **[!UICONTROL Publicação seletiva]**
* Configuração da publicação seletiva no nível da pasta.

Consulte [Criar uma configuração do Dynamic Media](#configuring-dynamic-media-cloud-services) ou [Configurar publicação seletiva no nível da pasta no Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>A Publicação seletiva só está disponível no modo Dynamic Media - Scene7 .

>[!NOTE]
>
>*Copiando* os ativos de e para pastas apaga o estado de publicação desses ativos. No entanto, quando você *mover* ativos de e para pastas cuja propriedade de pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

**Para publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas) e selecione **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, execute um dos seguintes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Use **[!UICONTROL Exibição de lista]** para que você possa verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Use **[!UICONTROL Exibição de lista]** assim, você pode verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >If **[!UICONTROL Gerenciar publicação]** não é visto na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu da lista.

1. No **[!UICONTROL Gerenciar publicação - Opções]** página, em **[!UICONTROL Ação]**, selecione o tipo de ativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Publicar]** (para Experience Manager) | Selecione essa opção para publicar ativos no Experience Manager para visualização segura. |
   | **[!UICONTROL Publicar no Dynamic Media]** | Selecione essa opção para publicar ativos no Dynamic Media para entrega no domínio público ou para usar recursos como Corte inteligente ou representações dinâmicas.<br>Essa opção só estará disponível se **[!UICONTROL Modo de publicação do Dynamic Media]** está definida como **[!UICONTROL Publicação seletiva]** nas propriedades da pasta. |

1. Em **[!UICONTROL Agendar]**, defina o tempo da publicação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para publicar os ativos imediatamente. |
   | **[!UICONTROL Posteriomente]** | Selecione para publicar os ativos em uma data e hora específica. |

1. No canto superior direito do **[!UICONTROL Gerenciar publicação]** página, selecione **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Gerenciar publicação - Escopo]** siga um destes procedimentos:

   * Se necessário, selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito do **[!UICONTROL Gerenciar publicação - Escopo]** página, selecione **[!UICONTROL Publicar]** ou **[!UICONTROL Publicar no Dynamic Media]**.
1. Selecionar **[!UICONTROL OK]**.

### Cancelar a publicação seletiva de ativos do Dynamic Media ou do Experience Manager usando Gerenciar publicação {#selective-unpublish-manage-publication}

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas) e selecione **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, execute um dos seguintes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Use **[!UICONTROL Exibição de lista]** para que você possa verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Use **[!UICONTROL Exibição de lista]** assim, você pode verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >If **[!UICONTROL Gerenciar publicação]** não é visto na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu da lista.

1. No **[!UICONTROL Gerenciar publicação - Opções]** página, em **[!UICONTROL Ação]**, selecione o tipo de desativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Cancelar publicação]** (de Experience Manager) | Selecione essa opção se desejar desfazer a publicação de ativos do Experience Manager. |
   | **[!UICONTROL Desfazer publicação no Dynamic Media]** | Selecione essa opção se desejar desfazer a publicação de ativos do Dynamic Media.<br>Essa opção só estará disponível se **[!UICONTROL Modo de publicação do Dynamic Media]** está definida como **[!UICONTROL Publicação seletiva]** nas propriedades da pasta. |

1. Em **[!UICONTROL Agendar]**, defina o tempo da desativação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para cancelar a publicação dos ativos imediatamente. |
   | **[!UICONTROL Posteriomente]** | Selecione para desfazer a publicação dos ativos em uma data e hora específica. |

1. No canto superior direito do **[!UICONTROL Gerenciar publicação]** página, selecione **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Gerenciar publicação - Escopo]** siga um destes procedimentos:
   * Selecione um ou mais ativos que deseja remover do cancelamento da publicação.
   * No canto superior direito do **[!UICONTROL Gerenciar publicação - Escopo]** página, selecione **[!UICONTROL Cancelar publicação]** ou **[!UICONTROL Cancelar publicação do Dynamic Media]**.
1. Selecionar **[!UICONTROL OK]**.

## Publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida {#quick-publish-aem-dm}

Você pode usar **[!UICONTROL Publicação rápida]** para casos de ativação de ativos simples. **[!UICONTROL Publicação rápida]** O publica os ativos selecionados imediatamente sem qualquer outra interação do usuário. Por causa dessa ação, todas as referências não publicadas também são publicadas automaticamente.

>[!NOTE]
>
>Para usar **[!UICONTROL Publicação rápida]** para publicar ativos no Dynamic Media ou no Experience Manager, tenha certeza **[!UICONTROL Publicação seletiva]** está ativada em seu **[!UICONTROL Configuração do Dynamic Media]** ou nas propriedades da pasta selecionada.

**Para publicar ativos no Dynamic Media ou no Experience Manager usando a Publicação rápida:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e, no lado direito da página, selecione **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, execute um dos seguintes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Use **[!UICONTROL Exibição de lista]** para que você possa verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Use **[!UICONTROL Exibição de lista]** assim, você pode verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >If **[!UICONTROL Publicação rápida]** não é visto na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Publicação rápida]** no menu da lista.

      ![Publicação rápida em nível de pasta no Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selecione uma das opções a seguir no **[!UICONTROL Publicação rápida]** lista de menus.

   | Opção Publicação rápida | O que faz |
   | --- | --- | 
   | Publicar no Experience Manager | Publica os ativos selecionados imediatamente no Experience Manager. |
   | Publicar no Brand Portal | Publica os ativos selecionados imediatamente em **[!UICONTROL Brand Portal]**.<br>Essa opção só estará disponível se a instância do Experience Manager Assets tiver **[!UICONTROL Brand Portal]** já está configurado. |
   | Publicar no Dynamic Media | Publica os ativos selecionados imediatamente no Dynamic Media.<br>Um ativo deve ser sincronizado com o Dynamic Media. Se necessário, assegure que **[!UICONTROL Modo de sincronização]** nas propriedades de uma pasta já está definido como **[!UICONTROL Sincronizar tudo nesta subárvore de pastas com o Dynamic Media]**. |

1. Selecionar **[!UICONTROL OK]**, em seguida selecione **[!UICONTROL Fechar]**.

## Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa {#selective-publish-unpublish-search-results}

Os resultados da pesquisa podem mostrar ativos de várias pastas de ativos que têm diferentes configurações de publicação do Dynamic Media. Quando você seleciona vários ativos dos resultados da pesquisa e cada ativo tem diferentes configurações do modo de publicação do Dynamic Media, é possível acionar **[!UICONTROL Gerenciar publicação]** na barra de ferramentas, para publicar ou desfazer a publicação.

Consulte também [Pesquisar ativos no Experience Manager](/help/assets/search-assets.md).

**Para publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa:**

1. No Experience Manager, no canto superior esquerdo da página, selecione o logotipo do Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e selecione **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Na barra de ferramentas, próximo ao canto superior direito da página, selecione o ícone Pesquisar (lupa).
1. No **[!UICONTROL Digite para pesquisar]** campo de texto, digite uma palavra-chave e pressione **[!UICONTROL Enter]**.
1. Ao lado do canto superior direito da página, selecione o **[!UICONTROL Exibição de lista]** ícone .
1. Ao lado do canto superior esquerdo da página, selecione o **[!UICONTROL Filtros]** ícone .

   ![Exibição de lista e filtros em resultados de pesquisa](/help/assets/assets-dm/select-publish-search-result.png)

1. No painel esquerdo, expanda **[!UICONTROL Status]** em seguida, expanda a **[!UICONTROL Dynamic Media]** predicado de pesquisa.
1. Use o **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]** caixas de seleção para refinar mais os resultados da pesquisa com base no estado publicado dos ativos do Dynamic Media.
Como opção, você pode usar essas caixas de seleção com a variável **[!UICONTROL Publicar]** predicado de pesquisa para refinar os resultados de pesquisa de **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]** Experience Manager assets.
1. Siga uma das seguintes opções:
   * Selecione um ou mais ativos que deseja publicar ou cancelar a publicação.
   * Próximo ao canto superior direito do **[!UICONTROL Resultados da pesquisa]** página, selecione **[!UICONTROL Selecionar tudo]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Selecione o ícone de reticências na barra de ferramentas para abrir **[!UICONTROL Gerenciar publicação]**.
1. No **[!UICONTROL Gerenciar publicação - Opções]** selecione a ação desejada.

   | Ação selecionada | Publicar ativos na configuração do Dynamic Media | Os ativos são |
   | --- | --- | --- |
   | Publicação | Imediatamente ou após a ativação | Publicado no Experience Manager e Dynamic Media. |
   | Publicação | Publicação seletiva | Publicado somente no Experience Manager. |
   | Desfazer publicação | Imediatamente ou após a ativação | Não publicado do Experience Manager e Dynamic Media. |
   | Desfazer publicação | Publicação seletiva | Não publicado somente no Experience Manager. |
   | Publicar no Dynamic Media | Imediatamente ou após a ativação | Não publicado no Experience Manager, Dynamic Media ou em ambos. |
   | Publicar no Dynamic Media | Publicação seletiva | Publicado somente no Dynamic Media. |
   | Desfazer publicação no Dynamic Media | Imediatamente ou após a ativação | Não foi cancelada a publicação do Experience Manager, Dynamic Media ou ambos. |
   | Desfazer publicação no Dynamic Media | Publicação seletiva | Não publicado somente no Dynamic Media. |

1. Em **[!UICONTROL Agendar]**, defina o tempo da desativação.

   | Horário selecionado | O que acontece |
   | --- | --- |
   | Agora | A ação selecionada é executada imediatamente. |
   | Posteriomente | A ação selecionada é executada na data e hora específicas selecionadas. |

1. No canto superior direito do **[!UICONTROL Gerenciar publicação - Opções]** página, selecione **[!UICONTROL Próximo]**.
1. (Opcional) Na seção **[!UICONTROL Gerenciar publicação - Escopo]** revisar a página **[!UICONTROL Publicar Target]** na tabela para os ativos selecionados.

   | Publicar ativos na configuração do Dynamic Media | Ação selecionada | Direcionamento da publicação |
   | --- | --- | --- |
   | Imediatamente ou <br>Após ativação | Publicação | Experience Manager e Dynamic Media |
   | Imediatamente ou <br>Após ativação | Publicar no Dynamic Media | Nenhum |
   | Publicação seletiva | Publicação | Experience Manager |
   | Publicação seletiva | Publicar no Dynamic Media | Dynamic Media |
   | Imediatamente ou <br>Após ativação | Desfazer publicação | Experience Manager e Dynamic Media |
   | Imediatamente ou <br>Após ativação | Desfazer publicação no Dynamic Media | Nenhum |
   | Publicação seletiva | Desfazer publicação | Experience Manager |
   | Publicação seletiva | Desfazer publicação no Dynamic Media | Dynamic Media |

1. No **[!UICONTROL Gerenciar publicação - Escopo]** siga um destes procedimentos:
   * Selecione um ou mais ativos que deseja remover da publicação ou do cancelamento da publicação.
   * No canto superior direito do **[!UICONTROL Gerenciar publicação - Escopo]** página, selecione **[!UICONTROL Publicar]** ou **[!UICONTROL Cancelar publicação]** para iniciar a ação.
1. Selecionar **[!UICONTROL OK]**.

## Verificar o status de publicação de um ativo {#check-publish-status-of-asset}

Você pode usar **[!UICONTROL Linha do tempo]** com **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]** no Experience Manager para verificar rapidamente o estado de publicação de um ativo.

**Para verificar o status de publicação de um ativo:**

1. No Experience Manager, no canto superior esquerdo da página, selecione o logotipo do Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e selecione **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]** (a captura de tela abaixo mostra a variável **[!UICONTROL Exibição de lista]**), abra uma pasta que contenha ativos que você publicou ou não publicou.
1. Selecione um ativo para que ele seja exibido com uma marca de seleção. Veja a captura de tela abaixo, por exemplo.
1. Próximo ao canto superior esquerdo da página, no menu suspenso, selecione **[!UICONTROL Linha do tempo]**. O **[!UICONTROL Status]** no painel esquerdo, mostra o estado de publicação do ativo selecionado.
Ao utilizar **[!UICONTROL Exibição de lista]**, uma coluna extra para **[!UICONTROL Dynamic Media]** o estado de publicação é exibido.
   * Uma pasta configurada para sincronizar com o Dynamic Media exibe a variável **[!UICONTROL Dynamic Media]** por padrão.
   * Uma pasta que é *not* configurado para sincronizar com o Dynamic Media não exibe a coluna Dynamic Media .
      ![Exibição de lista e linha do tempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solução de problemas de publicação seletiva {#selective-publish-troubleshoot}

Um ativo que não está sincronizado com o Dynamic Media, mas tem uma ação de publicação do Dynamic Media acionada nele, resulta na seguinte mensagem de erro e solução:

![Erro de publicação seletiva](/help/assets/assets-dm/selective-publish-error.png)
