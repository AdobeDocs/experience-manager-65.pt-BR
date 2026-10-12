---
title: Metadados C2PA [!DNL Experience Manager Assets]
description: Saiba como o [!DNL Experience Manager Assets] detecta metadados C2PA em ativos carregados, os sinaliza na interface do usuário e assina as representações geradas para ativos da Gen AI.
role: User, Admin, Developer
feature: Asset Management, Metadata, Renditions, Workflow, Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: f47205896ed512deadb4d31acbfe0fafa18515e7
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 6%
---

# Metadados C2PA em [!DNL Experience Manager Assets] {#c2pa-metadata}

As marcas estão mais preocupadas do que nunca com a transparência de conteúdo, a divulgação do uso de IA e a prevenção da adulteração de ativos. A Content Authenticity Initiative (CAI) na Adobe cria ferramentas em conformidade com o padrão técnico [Coalizão para Proveniência e Autenticidade de Conteúdo](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) (C2PA). Os metadados C2PA, um novo tipo de metadados invioláveis, ajudam os visualizadores a entender a linhagem do conteúdo e garantir a integridade dos ativos da marca. Elas podem incluir uma grande variedade de dados de origem que oferecem insights sobre o histórico de um ativo digital.

Essa informação inclui:

* **Emissor ou Signatário:** informações sobre a entidade ou empresa que emitiu a assinatura digital do ativo.
* **Data de Emissão:** a data em que os metadados C2PA foram aplicados ao ativo.
* **Processo:** registros de qualquer edição ou modificação feita no ativo.
* **Detalhes do dispositivo:** informações sobre o aplicativo ou dispositivo usado para criar ou editar o ativo.
* **Ferramenta de IA usada:** Se a IA gerativa foi usada para editar ou criar o ativo, o nome do modelo usado foi incluído.
* **Outras Informações Pertinentes:** Dados adicionais que oferecem mais contexto sobre o histórico de um ativo.

Para obter mais informações sobre o histórico de um ativo, consulte [Verificar](https://contentcredentials.org/verify).

O [!DNL Adobe Experience Manager Assets] detecta metadados C2PA ao carregar ou atualizar um ativo, sinaliza esses ativos na interface do usuário [!DNL Assets] e mantém a divulgação da Gen AI intacta nas representações geradas pelo [!DNL Experience Manager]. Sempre que o [!DNL Experience Manager] cria ou modifica uma representação de um ativo Gen AI, como uma miniatura, uma representação da Web, uma cópia com marca d&#39;água ou uma transcodificação de vídeo, o [!DNL Experience Manager] assina essa representação com um novo metadado C2PA que faz referência ao ativo original como seu pai. As representações baixadas, publicadas ou compartilhadas mantêm sua origem.

## Pré-requisitos {#Prerequisites}

O suporte a metadados C2PA requer o [!DNL Adobe Experience Manager] 6.5 Service Pack. No Service Pack 6.5.25.0, instale o [AEM 6.5 SP25 - hotfix de conformidade C2PA GenAI](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-ASSETS-75868-SP25-1.0.zip).

## Formatos e plataformas compatíveis {#supported-formats}

### Formatos {#formats}

[!DNL Experience Manager] assina representações nos formatos para os quais a [especificação C2PA](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) dá suporte para manifestos inseridos.

| Tipo | Formatos | Tipos de MIME |
|---|---|---|
| Imagem | JPEG, PNG, GIF, TIFF, DNG, WebP, JPEG XL, AVIF, HEIC/HEIF, SVG | `image/jpeg`, `image/png`, `image/gif`, `image/tiff`, `image/x-adobe-dng`, `image/webp`, `image/jxl`, `image/avif`, `image/heic`, `image/heif`, `image/svg+xml` |
| Vídeo | MP4, MOV, AVI | `video/mp4`, `video/quicktime`, `video/x-msvideo` |
| Áudio | MP3, M4A, WAV, FLAC | `audio/mpeg`, `audio/mp4`, `audio/wav`, `audio/flac` |

[!DNL Experience Manager] também reconhece aliases comuns, como `image/jpg`, `image/pjpeg`, `image/x-png` e `video/mov`. [!DNL Experience Manager] verifica se há um manifesto em cada ativo carregado, independentemente do formato de arquivo. As representações em outros formatos, como PSD ou EPS, não são assinadas.

### Plataformas {#platforms}

O suporte a metadados C2PA depende de um componente C2PA nativo que é enviado dentro do pacote `cq-dam-core`, com uma compilação para cada plataforma compatível. Quando o serviço é iniciado, o [!DNL Experience Manager] extrai a compilação da sua plataforma (`adobe_c2patool` ou `adobe_c2patool.exe` no Windows) para a pasta de dados privada do pacote, verifica a soma de verificação SHA-256 e a executa como um processo separado. Você não precisa instalar nada nem alterar `PATH`.

| Sistema operacional | Arquitetura |
|---|---|
| Linux (glibc 2.28 ou posterior, incluindo Red Hat Enterprise Linux 8) | `x86_64`, `aarch64` |
| macOS | `x86_64`, `aarch64` (silício Apple) |
| Windows | `x86_64` |

Funciona da mesma forma em [!DNL Adobe Managed Services] e implantações locais. Verifique se o processo [!DNL Experience Manager] pode iniciar esse executável. Se você usa `noexec` montagens, antivírus ou software de segurança de ponto de extremidade, permita que o `adobe_c2patool` seja executado da pasta `crx-quickstart`. Caso contrário, o suporte a metadados C2PA falhará ao iniciar.

## Como os metadados do C2PA funcionam {#how-c2pa-metadata-works}

O suporte a metadados C2PA tem duas partes: detecção quando um ativo é carregado ou atualizado e assinatura novamente sempre que [!DNL Experience Manager] gera ou modifica uma representação.

### Configuração do fluxo de trabalho {#workflow}

A etapa **[!UICONTROL Detectar Credencial C2PA]** mostrada em [Detectar metadados C2PA](#detect) faz parte do modelo de fluxo de trabalho padrão **[!UICONTROL Ativo de Atualização DAM]**. Se você usar uma cópia personalizada desse modelo, adicione a etapa você mesmo:

1. Na interface do [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]** e abra seu modelo no ![ícone Editar](assets/edit.svg) **[!UICONTROL modo Editar]**.
1. Adicione a etapa **[!UICONTROL Detectar Credencial C2PA]** após **[!UICONTROL Processador de Metadados]**, antes que qualquer etapa gere as representações.
1. Selecione **[!UICONTROL Sincronizar]** para salvar o modelo.

As etapas de representação assinam a saída somente se a detecção já tiver sido executada no ativo. Se a detecção for executada após eles, suas representações permanecerão sem assinatura até que o fluxo de trabalho seja executado novamente.

### Detectar metadados C2PA {#detect}

O fluxo de trabalho do **[!UICONTROL Ativo de atualização do DAM]** inclui uma etapa **[!UICONTROL Detectar credencial C2PA]**, que é executada após a etapa **[!UICONTROL Processador de metadados]**, como mostrado na figura abaixo. Ele lê o binário original do ativo e registra o resultado no nó de metadados do ativo `jcr:content/metadata`.

![Fluxo de trabalho](assets/workflow.png)

A tabela a seguir lista as propriedades dos metadados principais no workflow de metadados C2PA.

| Propriedade | Tipo | Descrição |
|---|---|---|
| `dam:hasC2PAManifest` | `boolean` | `true`, se o binário original tiver um manifesto C2PA inserido. É sempre escrito. |
| `dam:isAiGenerated` | `boolean` | `true`, se o manifesto colocar o ativo no escopo para rotulagem da Gen AI. Ela é gravada somente quando um manifesto está presente. |
| `dam:c2paValidationState` | `string` | Ele descreve o estado de validação do manifesto: `TRUSTED`, `VALID`, `INVALID` ou `UNKNOWN`. Ela é gravada somente quando um manifesto está presente. |

Quando um manifesto está presente, [!DNL Experience Manager] também o armazena como a representação `c2pa-manifest.json` (`application/json`).

Se você substituir o ativo original por um binário que não tem manifesto, a próxima execução de fluxo de trabalho definirá `dam:hasC2PAManifest` como `false` e removerá a representação `dam:isAiGenerated`, `dam:c2paValidationState` e `c2pa-manifest.json`.

>[!NOTE]
>
>Uma falha de detecção nunca bloqueia a assimilação de um ativo. Se a leitura do manifesto atingir o tempo limite ou falhar, [!DNL Experience Manager] registrará o erro, deixará os metadados inalterados e continuará com o restante do fluxo de trabalho.

### Exibir metadados C2PA na interface do usuário [!DNL Assets] {#view-c2pa-metadata}

O Assets que tem metadados C2PA exibe o selo **cr** (metadados C2PA) na interface do usuário [!DNL Assets]. Navegue até **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]** e procure o selo no canto inferior esquerdo de:

* A miniatura do ativo na **[!UICONTROL Exibição de cartão]**.
* A miniatura do ativo na **[!UICONTROL Exibição de coluna]**. Selecione o ativo para mostrar sua miniatura.
* A área de visualização da página de detalhes do ativo.

O selo **cr** mostrado na figura a seguir indica se um ativo contém metadados C2PA. Ele não mostra o manifesto em si. Para exibir o manifesto completo, baixe o ativo e abra-o em [Verificar](https://contentcredentials.org/verify).

![selo de crachá](assets/cr.png)

[!DNL Experience Manager] armazena o manifesto detectado como uma representação `c2pa-manifest.json` no ativo. Esta representação é interna. Ele não aparece no painel **[!UICONTROL Representações]** da página de detalhes do ativo ou no seletor de representações.

### Assinar representações {#sign-renditions}

Uma representação é um novo binário, portanto, o manifesto incorporado no ativo original não o cobre. Para manter intacta a divulgação da Gen AI, [!DNL Experience Manager] assina cada representação qualificada como a última etapa do processo que a produz. Os novos metadados do C2PA:

* Faz referência ao ativo original como seu ingrediente **pai**.
* Registra como a representação foi derivada do ativo original, como uma das ações C2PA `c2pa.resized`, `c2pa.transcoded` ou `c2pa.edited`.
* Nomeia `Adobe Experience Manager` como agente de software.

[!DNL Experience Manager] assina uma representação somente quando todos os itens a seguir são `true`:

* O ativo de origem tem `dam:isAiGenerated` definido como `true`. A Assets que possui um manifesto, mas não é gerada por meio da IA ainda mostra o símbolo **cr**, mas [!DNL Experience Manager] não assina novamente suas representações.
* O manifesto de origem é legível e seu estado de validação não é `INVALID`. [!DNL Experience Manager] nunca encadeia uma nova assinatura em um manifesto com falha na validação, por exemplo, depois que o ativo foi violado.
* O formato de representação é compatível com um manifesto C2PA incorporado. Para obter mais informações, consulte [Formatos com suporte](#supported-formats). [!DNL Experience Manager] ignora os formatos sem suporte sem um erro.

As seguintes etapas do fluxo de trabalho **[!UICONTROL Atualização de Ativo DAM concluída]** mostradas em [Detectar metadados C2PA](#detect) assinam sua saída.

| Etapa do fluxo de trabalho | Representações assinadas | Ação C2PA registrada |
|---|---|---|
| **[!UICONTROL Miniaturas do processo]** | Representações de miniatura e a imagem habilitada para a Web. | `c2pa.resized` e `c2pa.transcoded` quando o formato é alterado. |
| **[!UICONTROL Miniaturas do EPS (ativado por ImageMagick)]** | Saída principal, miniaturas derivadas e representações da Web. | `c2pa.resized`, `c2pa.transcoded` ou `c2pa.edited` |
| **[!UICONTROL Miniaturas de FFmpeg]** | Quadros e miniaturas do pôster do vídeo. | `c2pa.resized` e `c2pa.transcoded` |
| **[!UICONTROL Transcodificação de FFmpeg]** | Codificações de vídeo. | `c2pa.transcoded` |
| **[!UICONTROL Rasterizar representação da exibição de imagens do PDF/AI]** | Visualizar representação. (`cqdam.preview.png`) | `c2pa.transcoded` |

Os seguintes processos de fluxo de trabalho também assinam sua saída quando você os usa no fluxo de trabalho **[!UICONTROL Fluxo de trabalho de ativos de atualização do DAM concluído]**, em outro fluxo de trabalho ou em um modelo de fluxo de trabalho personalizado. Selecione-as na lista **[!UICONTROL Processar Miniaturas]** de uma etapa do fluxo de trabalho, conforme mostrado em [Detectar metadados C2PA](#detect).

| Processo de fluxo de trabalho | Representações assinadas | Ação C2PA registrada |
|---|---|---|
| **[!UICONTROL Criar miniatura]** | Representações de miniatura. | `c2pa.resized` e `c2pa.transcoded` quando o formato é alterado. |
| **[!UICONTROL Criar Imagem Habilitada Para A Web]** | Representações da Web. | `c2pa.resized` e `c2pa.transcoded` quando o formato é alterado. |
| **[!UICONTROL Linha de comando]**, por exemplo, com [!DNL ImageMagick] | Saída principal, miniaturas derivadas e representações da Web. | `c2pa.resized`, `c2pa.transcoded` ou `c2pa.edited` |
| **[!UICONTROL Processo de marca d&#39;água da imagem]** | Representação de marca d&#39;água ou a representação original quando a marca d&#39;água está em vigor. Para obter mais informações, consulte [Marca d&#39;água em seus ativos](/help/assets/watermarking.md). | `c2pa.edited` |
| **[!UICONTROL Criar storyboard de vídeo]** | Quadros principais do storyboard. | `c2pa.transcoded` |
| **[!UICONTROL Writeback XMP]** | A representação original, após a gravação dos metadados. Para obter mais informações, consulte [Writeback para representações do XMP](/help/assets/xmp-writeback.md). | `c2pa.edited` |

### Proteger o binário original durante o write-back do XMP {#xmp-writeback}

O write-back do XMP reescreve o binário original, o que quebra seu manifesto incorporado. Para ativos com `dam:hasC2PAManifest` definido como `true`, [!DNL Experience Manager] altera o comportamento da etapa **[!UICONTROL Processo de Writeback do XMP]** do fluxo de trabalho **[!UICONTROL Writeback de metadados do DAM]** da seguinte maneira:

* **Ativos de IA de Geração** (`dam:isAiGenerated` é `true`): [!DNL Experience Manager] grava a XMP e assina novamente o binário original, com o binário de pré-write-back como o pai. Ele salva o write-back e a nova assinatura juntos. Se a nova assinatura falhar, ele descarta e falha na etapa.
* **Outros ativos que contêm um manifesto**: [!DNL Experience Manager] ignora o write-back do XMP e registra o motivo. O binário original e seu manifesto permanecem inalterados.

### Modo de assinatura {#signing-mode}

[!DNL Experience Manager] assina representações localmente, na instância que as produz, com um certificado efêmero e autoassinado gerado por ele mesmo. A assinatura não precisa de acesso à rede e nenhum certificado ou configuração de chave privada.

>[!NOTE]
>
>Você não pode configurar seu próprio certificado de autenticação. Validadores como [Verificar](https://contentcredentials.org/verify) mostram a divulgação da Gen AI da representação e o link para o original, mas não identificam sua organização como signatária.

## Configurar metadados C2PA {#configure}

O suporte a metadados C2PA é ativado por padrão. Não é necessário instalar ou configurar nada.

### Configuração OSGi {#osgi-configuration}

Para alterar a configuração padrão, configure o **[!UICONTROL Day CQ DAM C2PA Service]** (PID `com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl`) no Configuration Manager em `https://[aem_server]:[port]/system/console/configMgr`, como mostrado na figura abaixo, ou adicione uma configuração OSGi ao seu projeto. Para obter mais informações, consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md).

![Configuração OSGi](assets/OSGi.png)

A tabela abaixo lista as propriedades na configuração OSGi do seu projeto.

| Propriedade | Nome no Configuration Manager | Padrão | Descrição |
|---|---|---|---|
| `enabled` | **[!UICONTROL Habilitado]** | `true` | Ativa ou desativa o suporte aos metadados C2PA. Quando desativado, o [!DNL Experience Manager] não detecta manifestos e não assina representações. |
| `timeoutMillis` | **[!UICONTROL Tempo limite da CLI (ms)]** | `30000` | Especifica o tempo máximo, em milissegundos, que [!DNL Experience Manager] aguarda uma única operação de leitura ou assinatura em um arquivo antes de tratá-lo como tempo limite. Aumente esse valor para vídeos grandes ou arquivos de imagem de alta resolução. |

Por exemplo, adicione uma configuração OSGi em `/apps/<your-project>/config/com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl.config`.

```text
enabled=B"true"
timeoutMillis=L"60000"
```

### Desativar suporte a metadados C2PA {#disable}

Na configuração **[!UICONTROL Day CQ DAM C2PA Service]** mostrada em [Configuração OSGi](#osgi-configuration), desabilite a opção **[!UICONTROL Habilitada]** e salve as alterações. A alteração entra em vigor imediatamente sem uma reinicialização:

* A etapa **[!UICONTROL Detectar Credencial C2PA]** mostrada em [Detectar metadados C2PA](#detect) torna-se não operacional.
* As etapas do fluxo de trabalho criam representações sem assiná-las.
* O Assets processado anteriormente mantém a propriedade `dam:hasC2PAManifest` e ainda mostra o símbolo **cr**.

>[!CAUTION]
>
>Após desabilitar a opção **[!UICONTROL Habilitada]**, as representações de ativos da Gen AI não contêm metadados C2PA. Se quiser cumprir com os regulamentos de divulgação da Gen AI, habilite a opção **[!UICONTROL Habilitado]**.

## Personalizar o pipeline de processamento {#customize}

Para adicionar, remover ou reordenar etapas no **[!UICONTROL Ativo de atualização do DAM]** e ainda manter intacta a divulgação da Gen AI, siga estas regras:

* **Executar detecção primeiro.** Mantenha **[!UICONTROL Detectar Credencial C2PA]** à frente de cada etapa que cria ou modifica as representações.
* **Assinar por último.** Qualquer alteração em um binário após a assinatura invalida sua assinatura. Não execute etapas que modificam uma representação após a etapa que a assinou.
* **Use as etapas que assinam.** As etapas internas listadas em [Assinar representações](#sign-renditions) assinam sua saída. As etapas personalizadas e as ferramentas de terceiros por meio das quais você executa qualquer coisa diferente do processo de **[!UICONTROL Linha de Comando]** não assinarão a saída, a menos que a assinatura seja explicitamente adicionada. Para obter mais informações, consulte [Processar ativos usando manipuladores de mídia e fluxos de trabalho](/help/assets/media-handlers.md).
* **Não modifique o original no local**, a menos que a etapa o assine novamente, como faz o **[!UICONTROL Writeback do XMP]** e o **[!UICONTROL Processo de Marca D&#39;Água de Imagem]**.

### Assinar representações de uma etapa de fluxo de trabalho personalizada {#custom-step}

As etapas de fluxo de trabalho personalizadas que produzem representações podem assiná-las por meio do serviço OSGi `com.day.cq.dam.api.c2pa.C2PASigner`. Ela aplica as mesmas regras de qualificação que as etapas internas, mas relata o resultado como um `C2PASigningOutcome`.

```java
import java.util.Collections;

import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.component.annotations.ReferencePolicy;

import com.day.cq.dam.api.Asset;
import com.day.cq.dam.api.Rendition;
import com.day.cq.dam.api.c2pa.C2PAAction;
import com.day.cq.dam.api.c2pa.C2PAConstants;
import com.day.cq.dam.api.c2pa.C2PASigner;
import com.day.cq.dam.api.c2pa.C2PASigningOutcome;

// Inside your WorkflowProcess implementation:

@Reference(cardinality = ReferenceCardinality.OPTIONAL, policy = ReferencePolicy.DYNAMIC)
private volatile C2PASigner c2paSigner;

private void signRendition(Asset asset, Rendition rendition) {
    C2PASigner signer = c2paSigner;
    if (signer == null) {
        return;
    }
    C2PASigningOutcome outcome = signer.signIfEligible(asset, rendition,
            Collections.singletonList(
                    new C2PAAction(C2PAConstants.ACTION_RESIZED, C2PAConstants.SOFTWARE_AGENT, null)));
    if (outcome == C2PASigningOutcome.FAILED) {
        // Log, retry, or alert an operator.
    }
}
```

Ligue para `signIfEligible` somente depois que a etapa terminar de gravar a representação. O serviço OSGi fornece os métodos conforme listados na tabela abaixo.

| Método | Use-o para |
|---|---|
| `signIfEligible(Asset, Rendition, List<C2PAAction>)` | Assine uma nova representação, com o ativo de origem como seu pai. |
| `signIfEligible(Asset, Map<Rendition, List<C2PAAction>>)` | Assinar várias representações derivadas do mesmo ativo. Este método lê o manifesto de origem uma vez. |
| `captureResignState(Asset)` | Tire uma imagem do ativo original antes que sua etapa o modifique no lugar. Este método retorna `null` se o ativo não estiver qualificado. |
| `resign(Asset, Rendition, List<C2PAAction>)` | Assine novamente o ativo original após uma alteração no local, com a imagem como principal. |
| `discardResignState(Rendition)` | Coloque uma imagem que você tenha tirado, mas que não será usada, por exemplo, porque sua alteração falhou. |

Os valores de `C2PASigningOutcome` são mencionados na tabela abaixo.

| Resultado | Descrição |
|---|---|
| `SIGNED` | [!DNL Experience Manager] assinou a representação. |
| `SKIPPED_SOURCE_NOT_AI_GENERATED` | O ativo de origem não é sinalizado como um ativo gerado pela IA. |
| `SKIPPED_FORMAT_NOT_ELIGIBLE` | O formato de representação não suporta o manifesto C2PA incorporado. |
| `SKIPPED_MANIFEST_UNREADABLE` | [!DNL Experience Manager] não foi encontrado nenhum manifesto no ativo de origem. |
| `SKIPPED_MANIFEST_NOT_VALID` | Falha na validação do manifesto de origem. |
| `SKIPPED_SERVICE_UNAVAILABLE` | O suporte a metadados C2PA está desativado ou indisponível. |
| `FAILED` | Falha na leitura do manifesto de origem ou na assinatura da representação. |

Para verificar a qualificação antes de gerar uma representação cara, chame `C2PASupportedFormats.isEligible(...)`.

## Resolução de problemas {#troubleshooting}

Ao solucionar problemas, defina os seguintes agentes de log como `DEBUG` na **[!UICONTROL Configuração do agente de log do Apache Sling]**.

* `com.day.cq.dam.core.impl.c2pa`: extração do componente C2PA nativo, leituras de manifesto e assinatura.
* `com.day.cq.dam.core.process.DetectC2PACredentialProcess`: detecção.

| Sintoma | Causa possível | Resolução |
|---|---|---|
| Nenhum ativo mostra a medalha **cr**. | O suporte a metadados C2PA está desativado ou o modelo de fluxo de trabalho não inclui a etapa de detecção. | Verifique se **[!UICONTROL Habilitado]** está habilitado na configuração **[!UICONTROL Day CQ DAM C2PA Service]** e se o seu modelo **[!UICONTROL Ativo de Atualização do DAM]** inclui **[!UICONTROL Detectar Credencial C2PA]**. |
| Um ativo que você sabe que tem um manifesto, mas não mostra nenhuma medalha. | O ativo foi carregado antes do recurso estar disponível. | Execute o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** no ativo novamente, por exemplo, em **[!UICONTROL Linha do tempo]** > **[!UICONTROL Iniciar fluxo de trabalho]**. |
| O serviço não é iniciado. O log de erros relata que `adobe_c2patool` não pode ser extraído ou marcado como executável. | Não existe nenhum binário para o sistema operacional ou a arquitetura, ou o sistema de arquivos bloqueia os executáveis. | Use uma plataforma compatível. Permitir que o processo [!DNL Experience Manager] execute os executáveis de sua pasta `crx-quickstart`. |
| O log de erros relata `GLIBC_2.xx not found`. | O host Linux executa uma versão glibc anterior à 2.28. | Atualize o sistema operacional do host. |
| Tempo limite da detecção ou da assinatura esgotado. | Arquivos grandes demoram mais do que o tempo limite padrão de 30 segundos. | Aumentar **[!UICONTROL Tempo limite da CLI (ms)]**. |
| As representações de um ativo da Gen AI não são assinadas. | O formato não é suportado, o manifesto é `INVALID` ou a detecção foi executada após a etapa de representação. | Verificar `dam:c2paValidationState` e o formato da representação. Mova **[!UICONTROL Detectar Credencial C2PA]** para frente das etapas de representação. |
| O Writeback XMP não atualiza um ativo. | O ativo carrega um manifesto, mas não é gerado por meio da IA, portanto, [!DNL Experience Manager] mantém seu original inalterado. | Esse é um comportamento esperado. Para obter mais informações, consulte [Proteger o original durante o write-back do XMP](#xmp-writeback). |

## Limitações {#limitations}

* A interface do usuário [!DNL Assets] mostra apenas se há metadados C2PA. Não há painel para os detalhes do manifesto.
* [!DNL Experience Manager] assina novamente as representações somente para ativos gerados por meio da IA. As representações de outros ativos que carregam um manifesto são criadas sem metadados C2PA.
* [!DNL Experience Manager] assina com um certificado efêmero e autoassinado. Não há suporte para certificados de assinatura personalizados ou específicos da organização.


>[!MORELIKETHIS]
>
>* [Metadados C2PA no modo de exibição Assets de [!DNL Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/assets-view/c2pa-metadata-assets-view)
>* [Metadados C2PA em [!DNL Experience Manager Assets Essentials]](https://experienceleague.adobe.com/pt-br/docs/experience-manager-assets-essentials/help/content-credentials)
>* [Metadados C2PA em [!DNL Dynamic Media]](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/c2pa-metadata)
>* [Writeback XMP para representações](/help/assets/xmp-writeback.md)
>* [Marcar seus ativos com uma marca d&#39;água](/help/assets/watermarking.md)
>* [Content Authenticity Initiative](https://contentauthenticity.org/)
>* [Verificar](https://contentcredentials.org/verify)
