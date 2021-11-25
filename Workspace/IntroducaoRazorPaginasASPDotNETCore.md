# Introdução às Razor páginas no ASP.NET Core

- 09/11/2021
- 9 minutos para o fim da leitura
- - [![img](https://github.com/Rick-Anderson.png?size=32)](https://github.com/Rick-Anderson)
  - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)
  - [![img](https://github.com/LisandroSu.png?size=32)](https://github.com/LisandroSu)
  - [![img](https://github.com/albertocosta.png?size=32)](https://github.com/albertocosta)

Esta página é útil?

De [Rick Anderson](https://twitter.com/RickAndMSFT)

Este é o primeiro tutorial de uma série que ensina os conceitos básicos da criação de um aplicativo Web ASP.NET Core Razor Pages.

Para obter uma introdução mais avançada destinada a desenvolvedores que estão familiarizados com controladores e exibições, consulte [Introdução às Razor Páginas](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0).

Se você não estiver ASP.NET Core desenvolvimento e não tiver certeza de qual ASP.NET Core de interface do usuário da Web melhor se ajustará às suas necessidades, consulte [escolher uma interface do usuário do ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/choose-web-ui?view=aspnetcore-6.0) .

No final da série, você terá um aplicativo que gerencia um banco de dados de filmes.

Neste tutorial, você:

- Crie um Razor aplicativo Web pages.
- Execute o aplicativo.
- Examinar os arquivos de projeto.

No final deste tutorial, você terá um aplicativo Web de Páginas em funcionamento que será Razor aprimorado em tutoriais posteriores.

![Home ou Index page](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start/_static/5/home5.png?view=aspnetcore-6.0)

## Pré-requisitos

- [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_5_visual-studio)
- [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_5_visual-studio-code)
- [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_5_visual-studio-mac)

- [Visual Studio 2022](https://visualstudio.microsoft.com/vs/#download) com a **ASP.NET e** a carga de trabalho de desenvolvimento web.

## Criar um Razor aplicativo Web pages

- [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_6_visual-studio)
- [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_6_visual-studio-code)
- [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_6_visual-studio-mac)

1. Inicie Visual Studio 2022 e **selecione Criar um novo projeto.**

   ![Criar um novo projeto na janela inicial](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start/_static/6/start-window-create-new-project.png?view=aspnetcore-6.0)

2. Na caixa **de diálogo Criar um novo** projeto, selecione ASP.NET Core Web **e,** em seguida, **selecione Próximo.**

   ![Criar um aplicativo Web do ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start/_static/6/np.png?view=aspnetcore-6.0)

3. Na caixa **de diálogo Configurar seu novo** projeto, insira para Project `RazorPagesMovie` **nome**. É importante nomear o projeto *Razor PagesMovie*, incluindo a correspondência da capitalização, de modo que os namespaces corresponderão quando você copiar e colar o código de exemplo.

   ![Configure seu novo projeto](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start/_static/6/config.png?view=aspnetcore-6.0)

4. Selecione **Avançar**.

5. Na caixa **de diálogo Informações** adicionais, selecione **.NET 6.0 (suporte a longo prazo)** e, em seguida, **selecione Criar**.

   ![Informações adicionais](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start/_static/6/additional-info.png?view=aspnetcore-6.0)

   O seguinte projeto inicial é criado:

   ![Gerenciador de Soluções](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start/_static/6/se.png?view=aspnetcore-6.0)

## Executar o aplicativo

- [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_7_visual-studio)
- [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_7_visual-studio-code)
- [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_7_visual-studio-mac)

Selecione **Razor PagesMovie** em **Gerenciador de soluções** e pressione CTRL + F5 para executar sem o depurador.

Visual Studio exibirá a caixa de diálogo a seguir quando um projeto ainda não estiver configurado para usar SSL:

![Este projeto é configurado para usar SSL. Para evitar avisos de SSL no navegador, você pode optar por confiar no certificado autoassinado que o IIS Express gerou. Você deseja confiar no certificado SSL do IIS Express?](https://docs.microsoft.com/pt-br/aspnet/core/getting-started/_static/trustcertvs22.png?view=aspnetcore-6.0)

Selecione **Sim** se você confia no certificado SSL do IIS Express.

A seguinte caixa de diálogo é exibida:

![Caixa de diálogo de aviso de segurança](https://docs.microsoft.com/pt-br/aspnet/core/getting-started/_static/cert.png?view=aspnetcore-6.0)

Selecione **Sim** se você concordar com confiar no certificado de desenvolvimento.

Para obter informações sobre como confiar no navegador Firefox, consulte [Firefox SEC_ERROR_INADEQUATE_KEY_USAGE erro de certificado](https://docs.microsoft.com/pt-br/aspnet/core/security/enforcing-ssl?view=aspnetcore-6.0#trust-ff).

Visual Studio:

- Executa o aplicativo, que inicia o [servidor Kestrel](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-6.0).
- Inicia o navegador padrão em `https://localhost:5001` , que exibe a interface do usuário dos aplicativos.

## Examinar os arquivos de projeto

As seções a seguir contêm uma visão geral das pastas e dos arquivos principais do projeto com os quais você trabalhará nos tutoriais posteriores.

### Pasta Páginas

Contém Razor páginas e arquivos de suporte. Cada Razor página é um par de arquivos:

- Um arquivo *. cshtml* que tem marcação HTML com código C# usando a Razor sintaxe.
- Um arquivo *. cshtml. cs* que tem código C# que manipula eventos de página.

Arquivos de suporte têm nomes que começam com um sublinhado. Por exemplo, o arquivo *_Layout.cshtml* configura os elementos de interface do usuário comuns a todas as páginas. Esse arquivo define o menu de navegação na parte superior da página e a notificação de direitos autorais na parte inferior da página. Para obter mais informações, consulte [Layout no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0).

### Pasta wwwroot

Contém ativos estáticos, como arquivos HTML, arquivos JavaScript e arquivos CSS. Para obter mais informações, consulte [Arquivos estáticos no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/static-files?view=aspnetcore-6.0).

### appsettings.json

Contém dados de configuração, como cadeias de conexão. Para obter mais informações, consulte [Configuração no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0).

### Module.vb

Contém o código a seguir:

C#Copiar

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Error");
    // The default HSTS value is 30 days. You may want to change this for production
    // scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapRazorPages();

app.Run();
```

As linhas de código a seguir neste arquivo criam um `WebApplicationBuilder` com padrões pré-configurados, adicionam Razor páginas ao contêiner de injeção de [dependência (di)](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-6.0)e compilam o aplicativo:

C#Copiar

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.DependencyInjection;
using RazorPagesMovie.Data;
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();

builder.Services.AddDbContext<RazorPagesMovieContext>(options => 
       options.UseSqlServer(builder.Configuration.GetConnectionString("RazorPagesMovieContext")));

var app = builder.Build();
```

O código realçado a seguir habilita a página de exceção do desenvolvedor quando o aplicativo está em execução no modo de desenvolvimento:

C#Copiar

```csharp
// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Error");
    // The default HSTS value is 30 days. You may want to change this for production
    // scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}
```

A página de exceção do desenvolvedor fornece informações úteis sobre exceções. Os aplicativos de produção não devem ser executados no modo de desenvolvimento porque a página de exceção do desenvolvedor pode vazar informações confidenciais.

O código realçado a seguir define o ponto de extremidade de exceção como `/Error` e habilita o [HSTS (protocolo de segurança de transporte estrito) http](https://docs.microsoft.com/pt-br/aspnet/core/security/enforcing-ssl?view=aspnetcore-6.0#http-strict-transport-security-protocol-hsts) quando o aplicativo ***não*** está em execução no modo de desenvolvimento:

C#Copiar

```csharp
// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Error");
    // The default HSTS value is 30 days. You may want to change this for production
    // scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}
```

Por exemplo, o código anterior é executado quando o aplicativo está no modo de produção ou de teste. Para obter mais informações, consulte [usar vários ambientes em ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/environments?view=aspnetcore-6.0).

O código a seguir permite vários [middlewares](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/middleware/?view=aspnetcore-6.0):

- `app.UseHttpsRedirection();` : Redireciona as solicitações HTTP para HTTPS.
- `app.UseStaticFiles();` : Permite que arquivos estáticos, como HTML, CSS, imagens e JavaScript sejam atendidos. Para obter mais informações, consulte [Arquivos estáticos no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/static-files?view=aspnetcore-6.0).
- `app.UseRouting();` : Adiciona a correspondência de rota ao pipeline de middleware. Para obter mais informações, consulte [Roteamento no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/routing?view=aspnetcore-6.0).
- `app.MapRazorPages();`: Configura o roteamento de ponto de extremidade para Razor páginas.
- `app.UseAuthorization();` : Autoriza um usuário a acessar recursos seguros. Esse aplicativo não usa autorização, portanto, essa linha pode ser removida.
- `app.Run();` : Executa o aplicativo.

## Solução de problemas com o exemplo concluído

Se você encontrar um problema que não possa resolver, compare seu código com o projeto concluído. [Exibir ou baixar o projeto concluído](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie60) ([como baixar](https://docs.microsoft.com/pt-br/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-6.0#how-to-download-a-sample)).

## Próximas etapas

[Em seguida: adicionar um modelo](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/model?view=aspnetcore-6.0)

------

## Conteúdo recomendado

- [Tutorial: criar um Razor aplicativo Web de páginas com ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/)

  Esta série de tutoriais explica as noções básicas de criação de um Razor aplicativo Web de páginas.

- [Parte 2, adicionar um modelo](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/model)

  Parte 2 da série de tutoriais em Razor páginas. Nesta seção, as classes de modelo são adicionadas.

- [Introdução ao ASP.NET Core MVC](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/first-mvc-app/start-mvc)

  Saiba como começar a usar o ASP.NET Core MVC.

- [Parte 3, páginas com scaffolding Razor](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/page)

  Parte 3 da série de tutoriais em Razor Páginas.

Mostrar mais