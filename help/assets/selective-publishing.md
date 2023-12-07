---
title: Trabalhar com publicação seletiva no Dynamic Media
description: Você pode optar por publicar ou cancelar a publicação de ativos para ou provenientes do Adobe Experience Manager ou Dynamic Media no nível da pasta. Você pode usar Gerenciar publicação ou Publicação rápida, em vez de depender exclusivamente da Configuração do Dynamic Media, cujas configurações são globais para todas as pastas na instância do Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# Configurar a publicação seletiva no nível da pasta no Dynamic Media {#selective-publish-configure-folder}

Você pode optar por publicar ou cancelar a publicação de ativos para ou provenientes do Adobe Experience Manager ou Dynamic Media no nível da pasta. Você pode usar **[!UICONTROL Gerenciar publicação]** ou **[!UICONTROL Publicação rápida]** em vez de se basear exclusivamente no **[!UICONTROL Configuração do Dynamic Media]** cujas configurações são globais para todas as pastas na instância do Dynamic Media.

Por exemplo, com a publicação seletiva, é possível trabalhar em ativos para produtos que ainda não estão online. Nesse caso, uma equipe de marketing pode acessar imagens de recorte inteligente e representações dinâmicas que são sincronizadas com o Dynamic Media. Eles podem criar materiais promocionais, tudo sem precisar publicar esses ativos no Dynamic Media para entrega global.

>[!IMPORTANT]
>
>A Publicação seletiva só está disponível no modo Dynamic Media - Scene7.

>[!NOTE]
>
>*Copiar* os ativos de e para pastas limpam o estado de publicação desses ativos. No entanto, quando você *mover* ativos de e para pastas cuja propriedade da pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

Se decidir alterar posteriormente a **[!UICONTROL Publicação seletiva]** em uma pasta, essas alterações afetam somente os novos ativos que você fizer upload para essa pasta a partir desse ponto. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente de **[!UICONTROL Publicação rápida]** ou o **[!UICONTROL Gerenciar publicação]** caixa de diálogo.

O nível da pasta **[!UICONTROL Modo de publicação do Dynamic Media]** sempre assume como padrão o valor encontrado na variável **[!UICONTROL Publicar ativos]** configuração no seu **[!UICONTROL Configuração do Dynamic Media]**. As etapas a seguir neste tópico, no entanto, mostram como alterar manualmente esse valor padrão no nível da pasta (conforme descrito nas etapas a seguir) para substituir o **[!UICONTROL Configuração do Dynamic Media]** valor.

Independentemente de você confiar em qualquer um dos seguintes:

* **[!UICONTROL Publicar ativos]** valor definido em **[!UICONTROL Configuração do Dynamic Media]**.
* **[!UICONTROL Modo de publicação do Dynamic Media]** valor definido nas propriedades no nível da pasta.

Você pode escolher **[!UICONTROL Imediatamente]**, **[!UICONTROL Na ativação]** ou **[!UICONTROL Publicação seletiva]**. Por exemplo, você pode definir a variável **[!UICONTROL Publicar ativos]** valor no seu **[!UICONTROL Configuração do Dynamic Media]** para **[!UICONTROL Na ativação]**, mas defina o **[!UICONTROL Dynamic Media Publish]** valor do modo no nível da pasta para **[!UICONTROL Publicação seletiva]** e vice-versa.

Depois de configurar a publicação seletiva em uma pasta, siga um destes procedimentos:

* [Publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação](#selective-publish-manage-publication).
* [Cancelar a publicação de ativos seletivamente do Dynamic Media ou do Experience Manager usando Gerenciar publicação](#selective-unpublish-manage-publication).
* [Publicar ativos no Dynamic Media ou no Experience Manager usando a Publicação rápida](#quick-publish-aem-dm).
* [Publicar ou cancelar a publicação de ativos de maneira seletiva por meio dos resultados da pesquisa](#selective-publish-unpublish-search-results).

**Para configurar a publicação seletiva no nível da pasta no Dynamic Media:**

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas ) e, em seguida, selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Siga uma das seguintes opções:
   * Editar as propriedades de uma pasta existente - Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, navegue até uma pasta cujas propriedades você deseja editar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
   * Editar as propriedades de uma nova pasta - Em **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, próximo ao canto superior direito da página, selecione **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**. No **[!UICONTROL Criar pasta]** , insira um título (obrigatório) para a pasta e selecione **[!UICONTROL Criar]**. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.

1. No **[!UICONTROL Modo de sincronização]** selecione uma das seguintes opções:

   | Modo de sincronização | Descrição |
   | --- | --- |
   | **[!UICONTROL Herdado]** | Nenhum valor de sincronização explícito na pasta. Em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão definido no **[!UICONTROL Configuração do Dynamic Media]**. O status detalhado de **[!UICONTROL Herdado]** é exibido por meio de uma dica de ferramenta. |
   | **[!UICONTROL Sincronizar tudo nesta subárvore de pastas com o Dynamic Media]** | Para que a publicação no Dynamic Media tenha êxito, os ativos devem ser sincronizados com o Dynamic Media. Selecionar essa opção inclui todos os ativos nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem a configuração padrão no **[!UICONTROL Configuração do Dynamic Media]**. |
   | **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** | Excluir todos os ativos nesta subárvore da sincronização com o Dynamic Media. |

   ![Publicação seletiva no nível da pasta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. No **[!UICONTROL Modo de publicação do Dynamic Media]** selecione uma opção. A variável **[!UICONTROL Modo de publicação do Dynamic Media]** sempre assume como padrão o valor definido na variável **[!UICONTROL Configuração do Dynamic Media]**. No entanto, você pode substituir esse padrão manualmente **[!UICONTROL Configuração do Dynamic Media]** usando uma das opções a seguir.

   >[!IMPORTANT]
   >
   >Independentemente da opção do Modo de publicação do Dynamic Media selecionada, as atualizações feitas posteriormente em um ativo que é *já* publicadas, essas atualizações são publicadas imediatamente, sem qualquer outra ação do usuário.
   >
   >Se um vídeo publicado for atualizado, ele deverá ser publicado novamente para refletir as alterações no delivery.

   | Opção Modo de publicação do Dynamic Media | Descrição |
   | --- | --- |
   | **[!UICONTROL Imediatamente]** | Quando os ativos são carregados para essa pasta, o sistema assimila os ativos no Experience Manager e fornece instantaneamente o URL/Incorporar. Essa opção está vinculada somente à publicação no Experience Manager e não há necessidade de intervenção do usuário para publicar ativos.<br>Essa opção é *não* disponível se você selecionou **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** in **[!UICONTROL Modo de sincronização]** na etapa anterior. |
   | **[!UICONTROL Na ativação]** | Quando os ativos são carregados para essa pasta, você deve publicar explicitamente o ativo primeiro, antes que um link de URL/Incorporação seja fornecido. Essa opção está vinculada somente à publicação de Experience Manager.<br>Essa opção é *não* disponível se você selecionou **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** in **[!UICONTROL Modo de sincronização]** na etapa anterior. |
   | **[!UICONTROL Publicação seletiva]** | Os ativos são publicados à sua escolha de Experience Manager ou no Dynamic Media para entrega no domínio público. Ambos os métodos de publicação são mutuamente exclusivos. Ou seja, você pode publicar ativos no DMS7 para usar recursos como Recorte inteligente ou representações dinâmicas. Ou você pode publicar ativos exclusivamente no Experience Manager para visualização segura; esses mesmos ativos são *não* publicado no DMS7 para entrega no domínio público. Esta opção não estará disponível se você tiver selecionado **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização do Dynamic Media]** in **[!UICONTROL Modo de sincronização]** na etapa anterior. |

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]** e selecione **[!UICONTROL OK]** para retornar ao Experience Manager Assets.

## Publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação{#selective-publish-manage-publication}

Antes que você possa usar **[!UICONTROL Gerenciar publicação]** para publicar seletivamente ativos no Dynamic Media ou no Experience Manager, verifique se você definiu um dos seguintes itens:

* A variável **[!UICONTROL Publicar ativos]** opção em **[!UICONTROL Configuração do Dynamic Media]** para **[!UICONTROL Publicação seletiva]**
* Publicação seletiva configurada no nível da pasta.

Consulte [Criar uma configuração do Dynamic Media](#configuring-dynamic-media-cloud-services) ou [Configurar a publicação seletiva no nível da pasta no Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>A Publicação seletiva só está disponível no modo Dynamic Media - Scene7.

>[!NOTE]
>
>*Copiar* os ativos de e para pastas limpam o estado de publicação desses ativos. No entanto, quando você *mover* ativos de e para pastas cuja propriedade da pasta está definida como **[!UICONTROL Publicação seletiva]**, o estado de publicação desses ativos é mantido.

**Para publicar ativos seletivamente no Dynamic Media ou no Experience Manager usando Gerenciar publicação:**

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas ) e, em seguida, selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Entrada **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, execute um dos procedimentos a seguir:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Uso **[!UICONTROL Exibição de lista]** para que você possa verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Uso **[!UICONTROL Exibição de lista]** assim, você pode verificar mais facilmente o status de publicação de um ativo específico.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gerenciar publicação]** não for vista na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu da lista.

1. No **[!UICONTROL Gerenciar publicação - Opções]** página, em **[!UICONTROL Ação]**, selecione o tipo de ativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Publish]** (para Experience Manager) | Selecione esta opção para publicar ativos no Experience Manager para visualização segura. |
   | **[!UICONTROL Publicar no Dynamic Media]** | Selecione esta opção para publicar ativos no Dynamic Media para entrega no domínio público ou para usar recursos como Recorte inteligente ou representações dinâmicas.<br>Essa opção só estará disponível se **[!UICONTROL Modo de publicação do Dynamic Media]** está definida como **[!UICONTROL Publicação seletiva]** nas propriedades da pasta. |

1. Em **[!UICONTROL Agendar]**, defina o tempo de publicação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para publicar os ativos imediatamente. |
   | **[!UICONTROL Mais tarde]** | Selecione para publicar os ativos em uma data e hora específicas. |

1. No canto superior direito da **[!UICONTROL Gerenciar publicação]** selecione **[!UICONTROL Próxima]**.
1. No **[!UICONTROL Gerenciar publicação - Escopo]** execute um dos procedimentos a seguir:

   * Se necessário, selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito da **[!UICONTROL Gerenciar publicação - Escopo]** selecione **[!UICONTROL Publish]** ou **[!UICONTROL Publicar no Dynamic Media]**.
1. Selecionar **[!UICONTROL OK]**.

### Cancelar a publicação de ativos seletivamente do Dynamic Media ou do Experience Manager usando Gerenciar publicação {#selective-unpublish-manage-publication}

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo, selecione o ícone Navegação (logo acima do ícone Ferramentas ) e, em seguida, selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Entrada **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, execute um dos procedimentos a seguir:
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Uso **[!UICONTROL Exibição de lista]** para que você possa verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Uso **[!UICONTROL Exibição de lista]** assim, você pode verificar mais facilmente o status de publicação de um ativo específico.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gerenciar publicação]** não for vista na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu da lista.

1. No **[!UICONTROL Gerenciar publicação - Opções]** página, em **[!UICONTROL Ação]**, selecione o tipo de desativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Cancelar publicação]** (do Experience Manager) | Selecione essa opção se desejar cancelar a publicação de ativos do Experience Manager. |
   | **[!UICONTROL Cancelar publicação no Dynamic Media]** | Selecione essa opção se desejar cancelar a publicação de ativos do Dynamic Media.<br>Essa opção só estará disponível se **[!UICONTROL Modo de publicação do Dynamic Media]** está definida como **[!UICONTROL Publicação seletiva]** nas propriedades da pasta. |

1. Em **[!UICONTROL Agendar]**, defina o tempo de desativação.

   | Programação | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para cancelar a publicação dos ativos imediatamente. |
   | **[!UICONTROL Mais tarde]** | Selecione para desfazer a publicação dos ativos em uma data e hora específicas. |

1. No canto superior direito da **[!UICONTROL Gerenciar publicação]** selecione **[!UICONTROL Próxima]**.
1. No **[!UICONTROL Gerenciar publicação - Escopo]** execute um dos procedimentos a seguir:
   * Selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito da **[!UICONTROL Gerenciar publicação - Escopo]** selecione **[!UICONTROL Cancelar publicação]** ou **[!UICONTROL Cancelar publicação no Dynamic Media]**.
1. Selecionar **[!UICONTROL OK]**.

## Publicar ativos no Dynamic Media ou no Experience Manager usando a Publicação rápida {#quick-publish-aem-dm}

Você pode usar **[!UICONTROL Publicação rápida]** para casos de ativação de ativos simples. **[!UICONTROL Publicação rápida]** O publica os ativos selecionados imediatamente, sem qualquer outra interação com o usuário. Por causa dessa ação, todas as referências não publicadas também são publicadas automaticamente.

>[!NOTE]
>
>Para usar **[!UICONTROL Publicação rápida]** para publicar ativos no Dynamic Media ou no Experience Manager, verifique se **[!UICONTROL Publicação seletiva]** está ativado no seu **[!UICONTROL Configuração do Dynamic Media]** ou nas propriedades da pasta selecionada.

**Para publicar ativos no Dynamic Media ou Experience Manager usando a Publicação rápida:**

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas) e, no lado direito da página, selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Entrada **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]**, execute um dos procedimentos a seguir:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Uso **[!UICONTROL Exibição de lista]** para que você possa verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Uso **[!UICONTROL Exibição de lista]** assim, você pode verificar mais facilmente o status de publicação de um ativo específico.

     >[!NOTE]
     >
     >Se **[!UICONTROL Publicação rápida]** não for vista na barra de ferramentas, selecione o botão de reticências e selecione **[!UICONTROL Publicação rápida]** no menu da lista.

     ![Publicação rápida no nível de pasta no Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selecione uma das seguintes opções no **[!UICONTROL Publicação rápida]** lista de menus.

   | opção Publicação rápida | O que faz |
   | --- | --- | 
   | Publicar no Experience Manager | Publica os ativos selecionados imediatamente no Experience Manager. |
   | Publicar no Brand Portal | Publica os ativos selecionados imediatamente no **[!UICONTROL Brand Portal]**.<br>Essa opção só estará disponível se sua instância do Experience Manager Assets tiver **[!UICONTROL Brand Portal]** já está configurado. |
   | Publicar no Dynamic Media | Publica os ativos selecionados imediatamente no Dynamic Media.<br>Um ativo deve ser sincronizado com o Dynamic Media. Se necessário, assegurar que **[!UICONTROL Modo de sincronização]** nas propriedades de uma pasta já está definida como **[!UICONTROL Sincronizar tudo nesta subárvore de pastas com o Dynamic Media]**. |

1. Selecionar **[!UICONTROL OK]** e selecione **[!UICONTROL Fechar]**.

## Publicar ou cancelar a publicação de ativos de maneira seletiva por meio dos resultados da pesquisa {#selective-publish-unpublish-search-results}

Os resultados da pesquisa podem mostrar ativos de várias pastas de ativos que têm configurações de publicação diferentes do Dynamic Media. Quando você seleciona vários ativos nos resultados da pesquisa e cada ativo tem diferentes configurações de modo de publicação do Dynamic Media, é possível acionar **[!UICONTROL Gerenciar publicação]** na barra de ferramentas, para publicar ou desfazer a publicação.

Consulte também [Pesquisar ativos no Experience Manager](/help/assets/search-assets.md).

**Para publicar ou cancelar a publicação de ativos de forma seletiva por meio dos resultados da pesquisa:**

1. No Experience Manager, no canto superior esquerdo da página, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas ) e, em seguida, selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Na barra de ferramentas, próximo ao canto superior direito da página, selecione o ícone Pesquisar (lupa).
1. No **[!UICONTROL Digite para pesquisar]** campo de texto, insira uma palavra-chave e pressione **[!UICONTROL Enter]**.
1. Próximo ao canto superior direito da página, selecione a **[!UICONTROL Exibição de lista]** ícone.
1. Próximo ao canto superior esquerdo da página, selecione a **[!UICONTROL Filtros]** ícone.

   ![Exibição de lista e Filtros nos resultados da pesquisa](/help/assets/assets-dm/select-publish-search-result.png)

1. No painel esquerdo, expanda **[!UICONTROL Status]**, em seguida expanda a variável **[!UICONTROL Dynamic Media]** pesquisar predicado.
1. Use o **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]** caixas de seleção para refinar ainda mais os resultados da pesquisa com base no estado publicado do Dynamic Media assets.
Como opção, você pode usar essas caixas de seleção com a **[!UICONTROL Publish]** predicado de pesquisa para refinar os resultados da pesquisa de **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]** ativos Experience Manager.
1. Siga uma das seguintes opções:
   * Selecione um ou mais ativos que deseja publicar ou cancelar a publicação.
   * Próximo ao canto superior direito do **[!UICONTROL Resultados da pesquisa]** selecione **[!UICONTROL Selecionar tudo]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**. Selecione o ícone de reticências na barra de ferramentas para poder abrir **[!UICONTROL Gerenciar publicação]**.
1. No **[!UICONTROL Gerenciar publicação - Opções]** selecione a ação desejada.

   | Ação selecionada | Configuração Publicar ativos na configuração do Dynamic Media | Os ativos são |
   | --- | --- | --- |
   | Publicação | Imediatamente ou Após ativação | Publicado no Experience Manager e no Dynamic Media. |
   | Publicação | Publicação seletiva | Publicado somente no Experience Manager. |
   | Desfazer publicação | Imediatamente ou Após ativação | Publicação cancelada no Experience Manager e no Dynamic Media. |
   | Desfazer publicação | Publicação seletiva | Publicação cancelada somente no Experience Manager. |
   | Publicar no Dynamic Media | Imediatamente ou Após ativação | Não publicado no Experience Manager, Dynamic Media ou ambos. |
   | Publicar no Dynamic Media | Publicação seletiva | Publicado somente no Dynamic Media. |
   | Desfazer publicação no Dynamic Media | Imediatamente ou Após ativação | Não ter a publicação desfeita do Experience Manager, do Dynamic Media ou de ambos. |
   | Desfazer publicação no Dynamic Media | Publicação seletiva | Publicação cancelada somente no Dynamic Media. |

1. Em **[!UICONTROL Agendar]**, defina o tempo de desativação.

   | Agendamento selecionado | O que acontece |
   | --- | --- |
   | Agora | A ação selecionada é executada imediatamente. |
   | Posteriomente | A ação selecionada é executada na data e hora específicas selecionadas. |

1. No canto superior direito da **[!UICONTROL Gerenciar publicação - Opções]** selecione **[!UICONTROL Próxima]**.
1. (Opcional) Na **[!UICONTROL Gerenciar publicação - Escopo]** , revise a **[!UICONTROL Destino de publicação]** na tabela para os ativos selecionados.

   | Configuração Publicar ativos na configuração do Dynamic Media | Ação selecionada | Direcionamento da publicação |
   | --- | --- | --- |
   | Imediatamente ou <br>Na ativação | Publicação | EXPERIENCE MANAGER e DYNAMIC MEDIA |
   | Imediatamente ou <br>Na ativação | Publicar no Dynamic Media | Nenhum |
   | Publicação seletiva | Publicação | Experience Manager |
   | Publicação seletiva | Publicar no Dynamic Media | Dynamic Media |
   | Imediatamente ou <br>Na ativação | Desfazer publicação | EXPERIENCE MANAGER e DYNAMIC MEDIA |
   | Imediatamente ou <br>Na ativação | Desfazer publicação no Dynamic Media | Nenhum |
   | Publicação seletiva | Desfazer publicação | Experience Manager |
   | Publicação seletiva | Desfazer publicação no Dynamic Media | Dynamic Media |

1. No **[!UICONTROL Gerenciar publicação - Escopo]** execute um dos procedimentos a seguir:
   * Selecione um ou mais ativos que deseja remover da publicação ou do cancelamento da publicação.
   * No canto superior direito da **[!UICONTROL Gerenciar publicação - Escopo]** selecione **[!UICONTROL Publish]** ou **[!UICONTROL Cancelar publicação]** para iniciar a ação.
1. Selecionar **[!UICONTROL OK]**.

## Verificar o status de publicação de um ativo {#check-publish-status-of-asset}

Você pode usar **[!UICONTROL Linha do tempo]** com **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]** no Experience Manager para verificar rapidamente o estado de publicação de um ativo.

**Para verificar o status de publicação de um ativo:**

1. No Experience Manager, no canto superior esquerdo da página, selecione o logotipo Experience Manager para acessar o console de navegação global. No lado esquerdo da página, selecione o ícone Navegação (logo acima do ícone Ferramentas ) e, em seguida, selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Entrada **[!UICONTROL Exibição de cartão]**, **[!UICONTROL Exibição de coluna]** ou **[!UICONTROL Exibição de lista]** (a captura de tela abaixo mostra o **[!UICONTROL Exibição de lista]**), abra uma pasta que contenha ativos publicados ou não.
1. Selecione um ativo para que ele apareça com uma marca de seleção. Consulte a captura de tela abaixo para obter um exemplo.
1. Próximo ao canto superior esquerdo da página, no menu suspenso, selecione **[!UICONTROL Linha do tempo]**. A variável **[!UICONTROL Status]** A região no painel esquerdo mostra o estado de publicação do ativo selecionado.
Quando você usa **[!UICONTROL Exibição de lista]**, uma coluna extra para **[!UICONTROL Dynamic Media]** estado de publicação é exibido.
   * Uma pasta configurada para sincronização com o Dynamic Media exibe a variável **[!UICONTROL Dynamic Media]** por padrão.
   * Uma pasta que é *não* configurado para sincronizar com o Dynamic Media não exibe a coluna Dynamic Media.
     ![Exibição de lista e linha do tempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solução de problemas de publicação seletiva {#selective-publish-troubleshoot}

Um ativo que não está sincronizado com o Dynamic Media, mas tem uma ação de publicação do Dynamic Media acionada nele, resulta na seguinte mensagem de erro e solução:

![Erro de publicação seletiva](/help/assets/assets-dm/selective-publish-error.png)
