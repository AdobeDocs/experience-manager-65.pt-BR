---
title: Acesso WebDAV
seo-title: Acesso WebDAV
description: Saiba mais sobre o acesso ao WebDAV no AEM.
seo-description: Saiba mais sobre o acesso ao WebDAV no AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Acesso WebDAV{#webdav-access}

Para conectar-se a AEM via WebDAV com o KDE:

AEM suporte ao oferta WebDAV que permite exibir e editar o conteúdo do repositório. A conexão via WebDAV fornece acesso direto ao repositório de conteúdo por meio de sua área de trabalho. Os arquivos de texto e PDF que são adicionados ao repositório por meio da conexão WebDAV são indexados automaticamente por texto completo e podem ser pesquisados com as interfaces de pesquisa padrão e por meio das APIs Java padrão.

## Geral {#general}

[Instruções detalhadas por ](/help/sites-administering/webdav-access.md#connecting-via-webdav) sistema operacional estão incluídas neste documento, mas o principal para conectar-se ao seu repositório usando o protocolo WebDAV é apontar seu cliente WebDAV para o seguinte local:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Este URL, quando conectado a partir do nível do sistema operacional, fornece acesso WebDAV ao espaço de trabalho padrão ( `crx.default`). Embora seja mais simples para o usuário, não oferece a ele a flexibilidade adicional de especificar nomes de espaço de trabalho, que podem ser obtidos usando [URLs WebDAV](/help/sites-administering/webdav-access.md#webdav-urls) adicionais.

AEM exibe o conteúdo do repositório da seguinte maneira:

* Um nó do tipo `nt:folder` é exibido como uma pasta. Os nós abaixo do nó `nt:folder` são exibidos como o conteúdo da pasta.

* Um nó do tipo `nt:file` é exibido como um arquivo. Os nós abaixo do nó `nt:file` não são exibidos, mas formam o conteúdo do arquivo.

Quando você usa o WebDAV para criar e editar pastas e arquivos, AEM cria e edita os nós `nt:folder` e `nt:file` necessários. Se você planeja usar o WebDAV para importar e exportar conteúdo, tente trabalhar com os tipos de nó `nt:file` e `nt:folder` o máximo possível.

>[!NOTE]
>
>Antes de configurar o WebDAV, verifique os [Requisitos técnicos](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URLs WebDAV {#webdav-urls}

O URL do servidor WebDAV tem a seguinte estrutura:

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Descrição</strong></td>
   <td>Host e porta em que AEM é executado</td>
   <td>Caminho para o aplicativo Web do repositório AEM</td>
   <td>Caminho para o qual o servlet WebDAV está mapeado</td>
   <td>Nome do espaço de trabalho</td>
  </tr>
 </tbody>
</table>

Ao alterar o elemento do espaço de trabalho no caminho, é possível mapear espaços de trabalho diferentes do padrão ( `crx.default`). Por exemplo, para mapear um espaço de trabalho chamado `staging`, use o seguinte URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Conexão via WebDAV {#connecting-via-webdav}

[Como mencionado acima](/help/sites-administering/webdav-access.md#general), para se conectar ao repositório usando o protocolo WebDAV, você aponta seu cliente WebDAV para o local do repositório. No entanto, dependendo do SO, as etapas envolvidas para conectar seu cliente diferem e pode haver configuração do SO necessário.

São fornecidas instruções sobre como conectar os seguintes sistemas operacionais:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Para conectar com êxito um sistema do Microsoft Windows 7 (e superior) a uma instância AEM que não esteja protegida com SSL, a opção para estabelecer a autenticação básica em uma rede não segura deve estar explicitamente ativada no Windows. Isso requer uma alteração no Registro do Windows do WebClient.

Depois que o registro é atualizado, a instância AEM pode ser mapeada como uma unidade.

#### Windows 7 e configuração superior {#windows-and-greater-configuration}

Para atualizar o registro para permitir a autenticação básica em uma rede não segura:

1. Localize a seguinte subchave do Registro:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Defina a subchave de entrada do registro `BasicAuthLevel` como um valor `2` ou superior.

   Se ele não estiver presente, adicione a subchave.

1. É necessário reiniciar o sistema para que a alteração do registro tenha efeito.

Consulte [Base de conhecimento do suporte da Microsoft 841215](https://support.microsoft.com/default.aspx/kb/841215) para obter mais informações sobre esta alteração no registro.

Consulte [KB de suporte da Microsoft 2445570](https://support.microsoft.com/kb/2445570) para obter informações sobre como melhorar a capacidade de resposta do cliente WebDav no Windows.

>[!NOTE]
>
>O Adobe recomenda que você crie um usuário do Windows com as mesmas credenciais que o usuário do repositório; caso contrário, você poderá encontrar conflitos de permissão.

#### Configuração do Windows 8 {#windows-configuration}

No Windows 8, também é necessário alterar a entrada do registro [conforme descrito para o Windows 7 e posterior](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). No entanto, antes que você possa fazer isso, a Experiência de desktop deve estar ativada para que a entrada do registro seja exibida.

Para habilitar a Experiência de desktop, abra **Gerenciador de servidores**, **Recursos**, **Adicionar recursos** e, em seguida, **Experiência de desktop**.

Depois de reiniciar a entrada do registro descrita para o Windows 7 e posterior está disponível. Modifique-o conforme descrito para o Windows 7 e posterior.

#### Conexão no Windows {#connecting-in-windows}

Para conectar-se a AEM via WebDAV em um ambiente do Windows:

1. Abra **Windows Explorer** ou **Explorador de Ficheiros** e clique em **Computador** ou **Este PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Clique em **Mapear unidade de rede** para start do assistente.
1. Insira os detalhes do mapeamento:

   * **Unidade**: Escolha qualquer carta disponível
   * **Pasta**:  `http://localhost:4502`
   * Verificar **Ligar utilizando credenciais diferentes**

   Clique em Concluir

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Se AEM estiver localizado em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` pelo respectivo nome de servidor ou endereço IP.

1. Digite o nome de usuário `admin` e a senha `admin`. O Adobe recomenda que você use a conta de administrador pré-configurada para teste.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. O assistente é fechado e a unidade recém-mapeada é aberta em uma janela do Windows Explorer ou do Explorador de Arquivos.

   ![chlimage_1-114](assets/chlimage_1-115a.png)

O Windows agora mapeou AEM como uma unidade via WebDAV e você pode usá-la como qualquer outra unidade.

### macOS {#macos}

Não há etapas de configuração necessárias para a conexão via WebDAV no MacOS. Basta conectar-se ao servidor WebDAV.

1. Navegue até qualquer janela **Localizador** e clique em **Ir** e **Ligar ao Servidor**, ou prima **Command+k**.
1. Na janela **Ligar ao Servidor**, introduza o local AEM:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Se AEM estiver localizado em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` pelo respectivo nome de servidor ou endereço IP.

1. Quando for solicitada a autenticação, digite o nome de usuário `admin` e a senha `admin`. O Adobe recomenda que você use a conta de administrador pré-configurada para teste.

o MacOS agora se conectou ao AEM via WebDAV e você pode usá-lo como qualquer outra pasta no Mac.

### Linux {#linux}

A conexão via WebDAV no Linux não requer nenhuma configuração, mas envolve algumas etapas para fazer a conexão que variam dependendo do seu ambiente para desktop.

#### GNOME {#gnome}

Para conectar-se a AEM via WebDAV com GNOME:

1. No Nautilus (explorador de arquivos), selecione **Locais** e selecione **Ligar ao Servidor**.
1. Na janela **Ligar ao Servidor**, selecione WebDAV (HTTP) em Tipo de Serviço.

1. Em **Servidor**, introduza `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM estiver localizado em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` pelo respectivo nome de servidor ou endereço IP.

1. Em **Pasta**, digite `/dav`
1. Digite o nome de usuário `admin`. O Adobe recomenda que você use a conta de administrador pré-configurada para teste.
1. Deixe a porta em branco e insira qualquer nome para sua conexão.
1. Clique em **Connect**. AEM solicita sua senha.
1. Digite a senha `admin` e clique em **Connect**.

O GNOME agora montou AEM como um volume e você pode usá-lo como qualquer outro volume.

#### KDE {#kde}

1. Abra o assistente de pasta de rede.
1. Selecione **WebFolder**(webdav) e clique em Avançar.
1. Em **Name**, digite um nome de conexão.
1. Em **User**, insira `admin.` Adobe recomenda que você use a conta de administrador pré-configurada.
1. Em **Servidor**, introduza `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM estiver localizado em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` pelo nome do servidor ou endereço IP respectivo

1. Em **Pasta**, digite `dav`

1. Clique em **Salvar e Conectar**.
1. Quando for solicitada sua senha, digite a senha `admin` e clique em **Connect**.

O KDE agora montou AEM como um volume e você pode usá-lo como qualquer outro volume.
