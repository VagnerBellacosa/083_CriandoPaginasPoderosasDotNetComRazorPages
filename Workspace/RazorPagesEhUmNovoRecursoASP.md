As **Razor Pages** é um um novo recurso da ASP.NET Core MVC que torna a codificação de cenários focados em páginas mais fácil e mais produtiva.

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | Todos os tipos de Razor Pages e seus recursos estão presentes no assembly **Microsoft.AspNetCore.Mvc.RazorPages** sendo que o pacote MVC - **Microsoft.AspNetCore.Mvc** inclui o conjunto das Razor Pages. Isso significa que você pode usar as Razor Pages fora da caixa com o MVC. |

Uma das vantagens das Razor Pages é que sua configuração é bem direta e simplificada. Basta criar um novo projeto vazio, adicionar a pasta **Pages**, criar uma página, e dai você apenas escreve código e a marcação dentro de seu arquivo **.cshtml.**

Para poder usar este recurso você deve instalar o .NET Core 2.0.0 ou superior, e, se estiver usando o Visual Studio deve instalar o VS 2017 versão 15.3 ou superior com os seguintes workloads:

- **ASP.NET and web development**
- **.NET Core cross-platform development**

Uma vez que a Razor Pages faz parte da pilha MVC, podemos usar qualquer recurso que inclua o MVC (*como as tag-helpers*) dentro das páginas Razor Pages.

*'Bora'* criar logo um projeto Razor Pages...

**Recursos usados:**

- [Visual Studio 2017 Community](https://www.visualstudio.com/pt-br/downloads/)

Criando o projeto no VS 2017

Abra o VS 2017 Community e crie um novo projeto ASP .NET Core usando o template **Empty**.

- **Create New Project;**
- Visual **C# -> Web -> ASP .NET Core Web Application;**
- Informe o nome **AspnRazorPage1**
- Selecione o template **Web Application**, marque ASP .NET Core 2.0 e .NET Core;

> ![img](http://www.macoratti.net/18/02/aspcore_rzpg11.png)

Confirme as opções clicando em OK para criar o projeto.

Ao final teremos o projeto criado com a seguinte estrutura:

| ![img](http://www.macoratti.net/18/02/aspcore_rzpg12.png) | Observe que a estrutura do projeto é diferente da estrutura do projeto MVC.No projeto Razor Pages você não tem as pastas Models, Views, Controllers , Services, Data.Temos apenas as pastas **wwwroot** onde ficam os arquivos estáticos nas subpastas: css, images, js e libTemos também a pasta **Pages** contendo as páginas da aplicação e os arquivos: _Layout.cshtml, _ViewImports.chtml e _ViewStart.cshtm usados para configurar a aplicação.Além disso temos os arquivos :  **appsettings.json** - arquivo de configuração contendo a string de conexão para o banco de dados**Program.cs** - arquivo de entrada da aplicação**Startup.cs** - arquivo de inicialização da aplicação**Nota**: *Se você criar o projeto Razor Pages com autenticação será criada a pasta **Controllers** com o controlador **AccountController** e uma pasta **Account** dentro da pasta **Pages**.* |
| --------------------------------------------------------- | ------------------------------------------------------------ |
|                                                           |                                                              |

Abrindo o arquivo **Startup.cs** do projeto criado veremos o seguinte código:

```
using Microsoft.AspNetCore.Builder; using Microsoft.AspNetCore.Hosting; using Microsoft.Extensions.Configuration; using Microsoft.Extensions.DependencyInjection;``namespace AspnRazorPage1 {    public class Startup    {        public Startup(IConfiguration configuration)        {            Configuration = configuration;        }``        public IConfiguration Configuration { get; }``        // This method gets called by the runtime. Use this method to add services to the container.        public void ConfigureServices(IServiceCollection services)        {            **services.AddMvc();**        }``        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.        public void Configure(IApplicationBuilder app, IHostingEnvironment env)        {            if (env.IsDevelopment())            {                app.UseBrowserLink();                app.UseDeveloperExceptionPage();            }            else            {                app.UseExceptionHandler("/Error");            }``            **app.UseStaticFiles();**``            **app.UseMvc();**        }    } }
```

Notamos que a configuração padrão habilita os recursos do MVC e da utilização dos arquivos estáticos.

Vamos abrir o arquivo **About.cshtml** e o seu arquivo code-behind **About.cshtml.cs** e visualizar a estrutura destes arquivos lado a lado:

| `@page @model AboutModel @{    ViewData["Title"] = "About"; } <h2>@ViewData["Title"]</h2> <h3>@Model.Message</h3>``<p>Use this area to provide additional information.</p>` | `using **Microsoft.AspNetCore.Mvc.RazorPages;**``namespace AspnRazorPage1.Pages {    public class **AboutModel** : **PageModel**    {        public string Message { get; set; }``        public void **OnGet()**        {            Message = "Your application description page.";        }    } }` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

Note que no arquivo **About.cshtml,** no topo da página temos a diretiva **@page** que informa ao Razor que este arquivo **.cshtml** representa uma Razor Page.

A diretiva **@page** torna o arquivo uma Action MVC, o que significa que ele pode tratar requisições diretamente, sem passar pelo controlador. Esta diretiva afeta o comportamento de outras construções Razor.

A diretiva **@model AboutModel** informa ao ASP .NET Core para vincular esta página com uma instância de **AboutModel**.

Por convenção o arquivo da classe **PageModel** tem o mesmo nome que o arquivo da página Razor com a extensão .cs.

Neste caso a Razor Page About.cshtml contém a diretiva **@model AboutModel** e o arquivo About.cshtml.cs contém a classe **AboutModel** que herda da classe **PageModel**.

Observe que no arquivo About.cshtml.cs a classe **AboutModel** possui o método **OnGet()** que é o método padrão para operação **GET**.

O Model Binding que já conhecemos do MVC também funciona com a Razor Pages. Assim como os métodos Actions dos Controllers MVC, temos na Razor Pages os **Handlers**.

Usamos os **Handlers** ou manipuladores como métodos para lidar com solicitações HTTP (GET, POST, PUT, DELETE ...). Podemos ter os seguintes métodos:

- **OnGet / OnGetAsync**
- **OnPost / OnPostAsync**
- **OnDelete / OnDeleteAsync**

Estes métodos serão automaticamente utilizados pela ASP.NET Core com base no tipo de solicitação HTTP.

Desta forma assim que você abrir a página **About.cshtml** o método **OnGet()** será executado. Da mesma forma em uma página contendo o método **OnPost()** este método será executado ao submeter a página.

Podemos ainda mover estes métodos para a página Razor **About.cshtml** usando a diretiva **@functions** :

```
@page @model AboutModel @{    ViewData["Title"] = "About"; } <h2>@ViewData["Title"]</h2> <h3>@Model.Message</h3>``<p>Use this area to provide additional information.</p> **@functions{**``    public string Message { get; set; }``    public void OnGet()    {        Message = "Your application description page.";    } }
```

Neste caso não precisaríamos do arquivo code-behind **About.cshtml.cs**.

As associações de caminhos de URL para páginas são determinadas pela localização da página no sistema de arquivos.

A tabela a seguir mostra um caminho da Página Razor e o URL correspondente:

| Nome do arquivo e caminho       | URL correspondente         |
| ------------------------------- | -------------------------- |
| **/Pages/Index.cshtml**         | **/ ou /Index**            |
| **/Pages/Contact.cshtml**       | **/Contact**               |
| **/Pages/Store/Contact.cshtml** | **/Store/Contact**         |
| **/Pages/Store/Index.cshtml**   | **/Store ou /Store/Index** |

Para incluir novas Razor Page em nosso projeto podemos usar o **Scaffolding** do Visual Studio clicando com o botão direito do mouse sobre a pasta **Pages** e selecionar a opção **Razor Page**:

![img](http://www.macoratti.net/18/02/aspcore_rzpg14.png)

A seguir veremos a janela **Add Scaffold** mostrando as opções :

![img](http://www.macoratti.net/18/02/aspcore_rzpg15.png)

Note que podemos usar o Entity Framework e gerar os métodos CRUD com EF Core.

Para concluir vamos executar a nossa aplicação, onde iremos obter o seguinte resultado:

![img](http://www.macoratti.net/18/02/aspcore_rzpg13.png)

Na [próxima parte do artigo](http://www.macoratti.net/18/02/aspcore_rzpg2.htm) iremos criar uma aplicação Razor Pages incluindo funcionalidades e mostrar como podemos usar este recurso.

*(disse Jesus)* **'Todavia digo-vos a verdade, que vos convém que eu vá; porque, se eu não for, o Consolador não virá a vós; mas, quando eu for, vo-lo enviarei.'**
**João 16:7**

[Veja os ](http://www.macoratti.net/destaque.htm)[Destaques e novidades do SUPER DVD Visual Basic (sempre atualizado) : clique e confira !](http://www.macoratti.net/destaques.htm)**Quer migrar para o VB .NET ?**Veja mais sistemas completos para a plataforma .NET no **[Super DVD .NET](http://www.macoratti.net/superdvd.htm)** , confira...[**Curso Básico VB .NET - Vídeo Aulas**](http://www.macoratti.net/curso_vbnet_basico.htm)**Quer aprender C# ??**Chegou o **[Super DVD C#](http://www.macoratti.net/superdvdc.htm)** com exclusivo material de suporte e vídeo aulas com curso básico sobre C#.[**Curso C# Basico - Video Aulas**](http://www.macoratti.net/curso_cshp_basico.htm)**Quer aprender os conceitos da Programação Orientada a objetos ?****[Curso Fundamentos da Programação Orientada a Objetos com VB .NET](http://www.macoratti.net/18/02/curso_fundamentos_oop.htm)** ![img](http://www.macoratti.net/new.gif)**Quer aprender o gerar relatórios com o ReportViewer no VS 2013 ?****[ Curso - Gerando Relatórios com o ReportViewer no VS 2013 - Vídeo Aulas](http://www.macoratti.net/curso_reportviewer.htm)**


**Referências:**

- [Seção VB .NET do Site Macoratti.net](http://www.macoratti.net/pageview.aspx?catid=1)
- [Super DVD .NET - A sua porta de entrada na plataforma .NET](http://www.macoratti.net/superdvd.htm)
- [Super DVD Vídeo Aulas - Vídeo Aula sobre VB .NET, ASP .NET e C#](http://www.macoratti.net/Vendas/Produtos.aspx?ID=22)
- [Seção C# do site Macoratti.net](http://www.macoratti.net/pageview.aspx?catid=18)
- [Super DVD C#](http://www.macoratti.net/superdvdc.htm)
- [Super DVD Visual Basic](http://www.macoratti.net/supercd.htm)
- [Curso Básico VB .NET - Vídeo Aulas](http://www.macoratti.net/curso_vbnet_basico.htm)
- [Curso C# Básico - Vídeo Aulas](http://www.macoratti.net/curso_cshp_basico.htm)
- [ASP .NET Core - Criando uma aplicação com Angular 2 - Macoratti.net](http://www.macoratti.net/17/04/aspcore_ang21.htm)
- [ASP .NET Core - Criando uma aplicação Web no ... - Macoratti.net](http://www.macoratti.net/17/01/aspnc_prj2.htm)
- [ASP .NET Core - Macoratti.net](http://www.macoratti.net/17/04/aspcore_mvcfilme1.htm)
- https://docs.microsoft.com/en-us/aspnet/core/mvc/razor-pages/?tabs=visual-studio