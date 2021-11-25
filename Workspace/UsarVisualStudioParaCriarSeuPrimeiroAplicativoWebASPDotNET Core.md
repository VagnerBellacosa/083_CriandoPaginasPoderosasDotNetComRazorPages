# Usar o Visual Studio para criar seu primeiro aplicativo Web ASP.NET Core

- 15/11/2021
- - [![img](https://github.com/anandmeg.png?size=32)](https://github.com/anandmeg)
  - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)

Esta página é útil?

Nesta introdução de 5 a 10 minutos que mostra como usar o Visual Studio, você criará um aplicativo Web "Olá, Mundo" simples usando um modelo de projeto ASP.NET e a linguagem de programação C#.

## Antes de começar

### Instalar o Visual Studio

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

## Criar um projeto

Para começar, você criará um projeto de aplicativo Web ASP.NET Core. O tipo de projeto vem com todos os arquivos de modelo para criar um aplicativo Web, antes mesmo de você adicionar alguma coisa!

1. Na janela inicial, escolha **Criar um novo projeto.**

   ![Captura de tela mostrando a janela de início Visual Studio com a opção &quot;Criar um novo projeto&quot; realçada.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/create-new-project-dark-theme.png?view=vs-2022)

2. Na janela **Criar um novo projeto,** escolha **C#** na lista Idioma. Em seguida, **Windows** na lista Plataforma e **Web** na lista de tipos de projeto.

   Depois de aplicar os filtros de tipo de projeto, plataforma e idioma, escolha o modelo ASP.NET Core **Aplicativo Web** e escolha **Próximo.**

   ![Captura de tela mostrando a janela 'Criar um novo projeto' filtrada em 'C#', 'Windows' e 'Web'. O modelo de projeto &quot;ASP.NET Core Aplicativo Web&quot; realçada.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-create-new-project-aspnet-core.png?view=vs-2022)

    Observação

   Se você não vir o modelo **ASP.NET Core Aplicativo Web,** poderá instalá-lo na janela Criar **um novo** projeto. Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**.

   ![Captura de tela mostrando o link &quot;Instalar mais ferramentas e recursos&quot; realçada na mensagem &quot;Não encontrando o que você está procurando&quot;.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/not-finding-what-looking-for.png?view=vs-2022)

   Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento Web e ASP.NET**.

   ![Captura de tela mostrando a carga de trabalho de desenvolvimento de plataforma cruzada do .NET Core no Instalador do Visual Studio.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/aspnet-core-web-dev-workload.png?view=vs-2022)

   Depois disso, escolha o botão **Modificar** no Instalador do Visual Studio. Se você for solicitado a salvar seu trabalho, faça isso. Em seguida, escolha **Continuar** para instalar a carga de trabalho. Em seguida, retorne para a etapa 2 deste procedimento para "[Criar um projeto](https://docs.microsoft.com/pt-br/visualstudio/ide/quickstart-aspnet-core?view=vs-2022#create-a-project)".

3. Na janela **Configurar seu novo projeto**, digite ou insira *OláMundo* na caixa **Nome do projeto**. Em seguida, escolha **Próximo.**

   ![Captura de tela mostrando a janela &quot;Configurar seu novo projeto&quot; com &quot;HelloWorld&quot; inserido no campo Project nome.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-name-your-aspnet-hello-world-project.png?view=vs-2022)

4. Na janela **Informações adicionais,** verifique se **o .NET 6.0** aparece no **campo** Estrutura. Observe que você pode optar por habilitar o suporte do Docker verificando a caixa. Você também pode adicionar suporte à autenticação selecionando um valor na listada do Tipo de autenticação. Lá, escolha entre:

   - Nenhum: sem autenticação.
   - Contas individuais: essas autenticações são armazenadas em um banco de dados local ou baseado no Azure.
   - plataforma de identidade da Microsoft: essa opção usa o Active Directory, o Azure AD ou Microsoft 365 para autenticação.
   - Windows: adequado para aplicativos de intranet.

   Deixe a **caixa Habilitar Docker** desmarcada e selecione **Nenhum para** Tipo de autenticação. Em seguida, selecione **Criar**.

   ![Captura de tela mostrando a janela Informações adicionais com '.NET 6.0' selecionado no campo Estrutura.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/aspnet-core-additional-information.png?view=vs-2022)

   Visual Studio abrirá seu novo projeto.

## Criar e executar o aplicativo

1. No **Gerenciador de soluções**, expanda a pasta **páginas** e, em seguida, escolha **index. cshtml**.

   ![Captura de tela mostrando ' index. cshtml ' selecionado na pasta páginas expandidas na Gerenciador de Soluções.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-aspnet-index-page-cshtml-file.png?view=vs-2022)

   Esse arquivo corresponde a uma página chamada **Home** no aplicativo Web, que é executado em um navegador da Web.

   ![Captura de tela mostrando a home page do aplicativo Web na janela do navegador.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-aspnet-index-page.png?view=vs-2022)

   No editor, você verá o código HTML para o texto que aparece na **Home** Page.

   ![captura de tela mostrando o arquivo Index. cshtml para a Home page no editor de código Visual Studio.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-aspnet-index-cshtml.png?view=vs-2022)

2. Altere o texto "bem-vindo" para ler "**Olá, mundo!**".

   ![captura de tela mostrando o arquivo ' Index. cshtml ' no editor de código de Visual Studio com o texto ' Welcome ' alterado para ' Olá, Mundo! '.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-aspnet-index-cshtml-page-hello-world.png?view=vs-2022)

3. selecione **IIS Express** ou pressione **Ctrl** + **F5** para executar o aplicativo e abri-lo em um navegador da web.

   ![captura de tela mostrando o botão IIS Express realçado em Visual Studio.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-aspnet-generic-iis-button.png?view=vs-2022)

    Observação

   Se você receber uma mensagem de erro informando **Não é possível conectar ao servidor Web 'IIS Express'** ou uma mensagem de erro que mencione um certificado SSL, feche o Visual Studio. Em seguida, abra o Visual Studio usando a opção **Executar como administrador** no menu de contexto acessado ao clicar com o botão direito do mouse. Em seguida, execute o aplicativo novamente.

4. No navegador da Web, verifique se a **Home** Page inclui o texto atualizado.

   ![Captura de tela mostrando a home page do aplicativo Web na janela do navegador com a mensagem atualizada ' Olá, Mundo! '.](https://docs.microsoft.com/pt-br/visualstudio/ide/media/vs-2022/csharp-aspnet-index-page-hello-world.png?view=vs-2022)

5. Feche o navegador da Web.

## Próximas etapas

para saber mais sobre como criar ASP.NET aplicativos web, continue com o tutorial a seguir:

[Introdução a C# e ASP.NET no Visual Studio](https://docs.microsoft.com/pt-br/visualstudio/get-started/csharp/tutorial-aspnet-core?view=vs-2022)

Ou saiba como colocar seu aplicativo Web em contêineres com o Docker:

[Ferramentas de Contêiner no Visual Studio](https://docs.microsoft.com/pt-br/visualstudio/containers/overview?view=vs-2022)

## Confira também

[Publicar seu aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio](https://docs.microsoft.com/pt-br/visualstudio/deployment/quickstart-deploy-to-azure?view=vs-2022)