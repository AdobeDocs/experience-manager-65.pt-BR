---
title: Redução de problemas de serialização no AEM Forms JEE | ADOBE EXPERIENCE MANAGER
description: Saiba como atenuar problemas de desserialização Java no AEM Forms JEE executado no JDK 8.
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---


# Redução de problemas de serialização no AEM Forms JEE {#mitigating-serialization-issues-in-aem-forms-jee}

O AEM Forms JEE inclui um firewall de desserialização que adiciona uma verificação de comprovação antes de qualquer tentativa de desserializar um objeto. Essa verificação testa um nome de classe em relação a um incluo na lista de permissões no estilo de firewall, ou ambos, e rejeita classes que são conhecidas por serem exploráveis por meio de ataques de desserialização Java™. O agente subjacente é a distribuição modificada da Adobe do projeto de código aberto [NotSoSerial](https://github.com/kantega/notsoserial), licenciado sob a [licença do Apache 2](https://www.apache.org/licenses/LICENSE-2.0).

Em instalações que executam o **JDK 11 ou posterior**, essa proteção é ativada pela filtragem de serialização nativa da plataforma e não requer etapas manuais. Nas instalações que executam o **JDK 8**, a filtragem de serialização nativa não é eficaz, portanto, o agente deve ser anexado explicitamente ao JVM na inicialização. Este artigo descreve como fazer isso.

>[!NOTE]
>
>Se a verificação de integridade do filtro de desserialização já relatar como ativo em seu servidor (consulte [Verificando a ativação do agente](#verifying-the-agents-activation)), seu servidor de aplicativos já estará protegido e você poderá ignorar as etapas restantes neste documento.

## Antes de começar {#before-you-begin}

Confirme a versão do Java™ com a qual seu servidor de aplicativos é executado:

```shell
java -version
```

Se a versão reportada for `1.8.x` (JDK 8), as etapas deste artigo se aplicam. Se for 11 ou posterior, nenhuma ação manual será necessária; verifique a proteção usando a verificação de integridade descrita em [Verificando a ativação do agente](#verifying-the-agents-activation).

Nas etapas a seguir, `<jee-installation-directory>` refere-se à raiz da instalação do AEM Forms JEE.

## Aplicando o agente {#applying-the-agent}

>[!IMPORTANT]
>
>Essas etapas exigem uma reinicialização do servidor de aplicativos. Aplique-as em cada instância afetada.

1. **Validar o estado atual.** Navegue até a verificação de integridade do filtro de desserialização:

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   Se a verificação relatar como ativa, a instância já estará protegida e nenhuma outra ação será necessária. Se estiver falhando, continue com as etapas a seguir.

1. **Verifique se o JAR do agente já está presente.** Verificar `notsoserial.jar` no seguinte local:

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **Adicione o JAR se ele estiver ausente.** Baixe [`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar) e copie-o para a pasta acima em cada instância:

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Substitua essa etapa pelo local de download oficial do Adobe para a distribuição do Forms JEE do agente antes da publicação.

1. **Atualize os parâmetros de inicialização do JVM** do seu servidor de aplicativos para anexar o agente. Adicione a seguinte opção à linha de execução do Java™:

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   O local exato da linha de execução do Java™ depende do seu servidor de aplicativos (por exemplo, JBoss, WebLogic ou WebSphere®). Adicione a opção às opções da JVM usadas para iniciar o servidor de aplicativos do AEM Forms JEE.

1. **Reinicie o servidor JEE** para que o agente seja carregado na inicialização do JVM.

1. **Revalidar.** Navegue novamente para a verificação de integridade:

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   A verificação de integridade agora deve relatar como íntegra.

## Verificando a ativação do agente {#verifying-the-agents-activation}

Você pode verificar a configuração do agente de desserialização a qualquer momento navegando até o seguinte URL:

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

Será exibida uma lista de verificações de integridade relacionadas ao agente. Se as verificações forem aprovadas, o agente será ativado corretamente. Se estiverem falhando em uma instância do JDK 8, o agente não foi carregado e você deve anexá-lo manualmente usando as etapas em [Aplicando o agente](#applying-the-agent).

## Configurar o agente {#configuring-the-agent}

As etapas abaixo se aplicam se a versão Java™ do seu servidor de aplicativos estiver sendo executada com o JDK 8. Você pode configurar o agente depois de anexar e carregá-lo usando as etapas em [Aplicando o agente](#applying-the-agent).

A configuração padrão é adequada para a maioria das instalações. Ele inclui um incluo na lista de permissões de classes conhecidas que podem ser exploradas remotamente e um conjunto de pacotes em que a desserialização de dados confiáveis é segura. A inclui na lista de bloqueios ➡ é aplicada antes de qualquer entrada incluída na lista de permissões.

A configuração do firewall é dinâmica e pode ser alterada a qualquer momento:

1. Vá para o Console da Web em `https://<server>:<port>/system/console/configMgr`.

1. Procure e clique em **Configuração do firewall de desserialização**.

Essa configuração contém as opções incluir na lista de permissões, atualizar e de log de diagnóstico:

* **Lista de permissões** - classes ou prefixos de pacote permitidos para desserialização. Se você desserializar suas próprias classes, adicione as classes ou pacotes relevantes aqui.
* **Lista de bloqueios** - classes que nunca são permitidas para desserialização. O conjunto inicial é limitado a classes consideradas vulneráveis a ataques de execução remota.
* **Log de diagnóstico** - opções para registrar quando ocorrer a desserialização. O padrão **class-name-only** relata as classes que estão sendo desserializadas. A opção **pilha completa** registra uma pilha do Java™ para a primeira tentativa de desserialização, o que é útil para localizar e remover a desserialização não confiável em seu uso. Essas opções são registradas somente no primeiro uso.

## Outras considerações {#other-considerations}

* O agente deve mitigar as classes vulneráveis conhecidas no momento. Se o seu projeto desserializar dados não confiáveis, ele ainda poderá ser exposto a ataques de negação de serviço, memória insuficiente ou desserialização futura desconhecida.
* Se você executar em um JRE (Java™ Runtime Environment) em vez de um JDK (Java™ Development Kit), as ferramentas necessárias para o carregamento dinâmico do agente não estarão disponíveis e o agente deverá ser anexado manualmente na inicialização, conforme descrito em [Aplicando o agente](#applying-the-agent).
* Se estiver executando em uma IBM® JVM, reveja a documentação sobre suporte para a API Java™ Attach.
