# Introdução às Razor páginas no ASP.NET Core

- 16/08/2021
- 22 minutos para o fim da leitura
- - [![img](https://github.com/Rick-Anderson.png?size=32)](https://github.com/Rick-Anderson)
  - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)

Esta página é útil?

Por [Rick Anderson](https://twitter.com/RickAndMSFT) e [Ryan Nowak](https://github.com/rynowak)

Razor As páginas podem tornar cenários com foco na página de codificação mais fáceis e produtivos do que o uso de controladores e exibições.

Se você estiver procurando um tutorial que utiliza a abordagem Modelo-Exibição-Controlador, consulte a [Introdução ao ASP.NET Core MVC](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0).

Este documento fornece uma introdução às Razor Páginas. Este não é um tutorial passo a passo. Se você encontrar algumas das seções muito avançadas, [consulte Get started with Razor Pages](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0). Para obter uma visão geral do ASP.NET Core, consulte a [Introdução ao ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-6.0).

## Pré-requisitos

- [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_2_visual-studio)
- [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_2_visual-studio-code)
- [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_2_visual-studio-mac)

- [Visual Studio 2019 16.8 ou posterior](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) com a carga de trabalho de **desenvolvimento da Web e do ASP.NET**
- [SDK do .NET 5.0](https://dotnet.microsoft.com/download/dotnet/5.0)



## Criar um Razor projeto de Páginas

- [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_3_visual-studio)
- [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_3_visual-studio-code)
- [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_3_visual-studio-mac)

Consulte [Começar a usar páginas Razor para](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0) obter instruções detalhadas sobre como criar um Razor projeto de Páginas.

## Razor Páginas

RazorAs páginas estão habilitadas *em Startup.cs:*

C#Copiar

```csharp
public class Startup
{
    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public IConfiguration Configuration { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddRazorPages();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        else
        {
            app.UseExceptionHandler("/Error");
            app.UseHsts();
        }

        app.UseHttpsRedirection();
        app.UseStaticFiles();

        app.UseRouting();

        app.UseAuthorization();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapRazorPages();
        });
    }
}
```

Considere uma página básica:

CSHTMLCopiar

```cshtml
@page

<h1>Hello, world!</h1>
<h2>The time on the server is @DateTime.Now</h2>
```

O código anterior se parece muito com um arquivo [Razor de exibição](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-6.0) usado em um ASP.NET Core com controladores e exibições. O que o torna diferente é a [`@page`](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/razor?view=aspnetcore-6.0#page) diretiva . `@page` transforma o arquivo em uma ação do MVC – o que significa que ele trata solicitações diretamente, sem passar por um controlador. `@page` deve ser a primeira Razor diretiva em uma página. `@page` afeta o comportamento de outros [Razor](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/razor?view=aspnetcore-6.0) constructos. RazorOs nomes de arquivo de páginas *têm um sufixo .cshtml.*

Uma página semelhante, usando uma classe `PageModel`, é mostrada nos dois arquivos a seguir. O arquivo *Pages/Index2.cshtml*:

CSHTMLCopiar

```cshtml
@page
@using RazorPagesIntro.Pages
@model Index2Model

<h2>Separate page model</h2>
<p>
    @Model.Message
</p>
```

O modelo de página *Pages/Index2.cshtml.cs*:

C#Copiar

```csharp
using Microsoft.AspNetCore.Mvc.RazorPages;
using Microsoft.Extensions.Logging;
using System;

namespace RazorPagesIntro.Pages
{
    public class Index2Model : PageModel
    {
        public string Message { get; private set; } = "PageModel in C#";

        public void OnGet()
        {
            Message += $" Server time is { DateTime.Now }";
        }
    }
}
```

Por convenção, o `PageModel` arquivo de classe tem o mesmo nome que o arquivo Page com Razor *.cs* anexado. Por exemplo, a Razor página anterior é *Pages/Index2.cshtml*. O arquivo que contém a classe `PageModel` é chamado *Pages/Index2.cshtml.cs*.

As associações de caminhos de URL para páginas são determinadas pelo local da página no sistema de arquivos. A tabela a seguir mostra um Razor caminho de página e a URL correspondente:

| Caminho e nome do arquivo     | URL correspondente         |
| :---------------------------- | :------------------------- |
| */Pages/Index.cshtml*         | `/` ou `/Index`            |
| */Pages/Contact.cshtml*       | `/Contact`                 |
| */Pages/Store/Contact.cshtml* | `/Store/Contact`           |
| */Pages/Store/Index.cshtml*   | `/Store` ou `/Store/Index` |

Observações:

- O runtime procura arquivos Razor pages na pasta *Pages* por padrão.
- `Index` é a página padrão quando uma URL não inclui uma página.

## Escrever um formulário básico

Razor As páginas são projetadas para facilitar a implementação de padrões comuns usados com navegadores da Web ao criar um aplicativo. [Model binding,](https://docs.microsoft.com/pt-br/aspnet/core/mvc/models/model-binding?view=aspnetcore-6.0) [Auxiliares de Marca](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0)e auxiliares HTML *funcionam* apenas com as propriedades definidas em uma Razor classe Page. Considere uma página que implementa um formulário básico "Fale conosco" para o modelo `Contact`:

Para as amostras neste documento, o `DbContext` é inicializado no arquivo [Startup.cs](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/razor-pages/index/3.0sample/RazorPagesContacts/Startup.cs#L23-L24).

O banco de dados na memória requer o `Microsoft.EntityFrameworkCore.InMemory` NuGet pacote.

C#Copiar

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<CustomerDbContext>(options =>
                      options.UseInMemoryDatabase("name"));
    services.AddRazorPages();
}
```

O modelo de dados:

C#Copiar

```csharp
using System.ComponentModel.DataAnnotations;

namespace RazorPagesContacts.Models
{
    public class Customer
    {
        public int Id { get; set; }

        [Required, StringLength(10)]
        public string Name { get; set; }
    }
}
```

O contexto do banco de dados:

C#Copiar

```csharp
using Microsoft.EntityFrameworkCore;
using RazorPagesContacts.Models;

namespace RazorPagesContacts.Data
{
    public class CustomerDbContext : DbContext
    {
        public CustomerDbContext(DbContextOptions options)
            : base(options)
        {
        }

        public DbSet<Customer> Customers { get; set; }
    }
}
```

O arquivo de exibição *Pages/Create.cshtml*:

CSHTMLCopiar

```cshtml
@page
@model RazorPagesContacts.Pages.Customers.CreateModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<p>Enter a customer name:</p>

<form method="post">
    Name:
    <input asp-for="Customer.Name" />
    <input type="submit" />
</form>
```

O modelo de página *Pages/Create.cshtml.cs*:

C#Copiar

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;
using RazorPagesContacts.Data;
using RazorPagesContacts.Models;
using System.Threading.Tasks;

namespace RazorPagesContacts.Pages.Customers
{
    public class CreateModel : PageModel
    {
        private readonly CustomerDbContext _context;

        public CreateModel(CustomerDbContext context)
        {
            _context = context;
        }

        public IActionResult OnGet()
        {
            return Page();
        }

        [BindProperty]
        public Customer Customer { get; set; }

        public async Task<IActionResult> OnPostAsync()
        {
            if (!ModelState.IsValid)
            {
                return Page();
            }

            _context.Customers.Add(Customer);
            await _context.SaveChangesAsync();

            return RedirectToPage("./Index");
        }
    }
}
```

Por convenção, a classe `PageModel` é chamada de `<PageName>Model` e está no mesmo namespace que a página.

A classe `PageModel` permite separar a lógica de uma página da respectiva apresentação. Ela define manipuladores para as solicitações enviadas e os dados usados para renderizar a página. Essa separação permite:

- Gerenciamento de dependências de página por meio [da injeção de dependência](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-6.0).
- [Teste de unidade](https://docs.microsoft.com/pt-br/aspnet/core/test/razor-pages-tests?view=aspnetcore-6.0)

A página tem um *método de manipulador*`OnPostAsync`, que é executado em solicitações `POST` (quando um usuário posta o formulário). Métodos de manipulador para qualquer verbo HTTP podem ser adicionados. Os manipuladores mais comuns são:

- `OnGet` para inicializar o estado necessário para a página. No código anterior, o `OnGet` método exibe a Página *CreateModel.cshtml.* Razor
- `OnPost` para manipular envios de formulário.

O sufixo de nomenclatura `Async` é opcional, mas geralmente é usado por convenção para funções assíncronas. O código anterior é típico para Razor Páginas.

Se você estiver familiarizado com aplicativos ASP.NET usando controladores e exibições:

- O `OnPostAsync` código no exemplo anterior é semelhante ao código típico do controlador.
- A maioria dos primitivos do [MVC, como model binding](https://docs.microsoft.com/pt-br/aspnet/core/mvc/models/model-binding?view=aspnetcore-6.0), validação e resultados de ação, funcionam da mesma forma com Controladores e Razor Páginas.

O método `OnPostAsync` anterior:

C#Copiar

```csharp
public async Task<IActionResult> OnPostAsync()
{
    if (!ModelState.IsValid)
    {
        return Page();
    }

    _context.Customers.Add(Customer);
    await _context.SaveChangesAsync();

    return RedirectToPage("./Index");
}
```

O fluxo básico de `OnPostAsync`:

Verifique se há erros de validação.

- Se não houver nenhum erro, salve os dados e redirecione.
- Se houver erros, mostre a página novamente com as mensagens de validação. Em muitos casos, erros de validação seriam detectados no cliente e nunca enviados ao servidor.

O arquivo de exibição *Pages/Create.cshtml*:

CSHTMLCopiar

```cshtml
@page
@model RazorPagesContacts.Pages.Customers.CreateModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<p>Enter a customer name:</p>

<form method="post">
    Name:
    <input asp-for="Customer.Name" />
    <input type="submit" />
</form>
```

O HTML renderizado *de Pages/Create.cshtml:*

HTMLCopiar

```html
<p>Enter a customer name:</p>

<form method="post">
    Name:
    <input type="text" data-val="true"
           data-val-length="The field Name must be a string with a maximum length of 10."
           data-val-length-max="10" data-val-required="The Name field is required."
           id="Customer_Name" maxlength="10" name="Customer.Name" value="" />
    <input type="submit" />
    <input name="__RequestVerificationToken" type="hidden"
           value="<Antiforgery token here>" />
</form>
```

No código anterior, postando o formulário:

- Com dados válidos:

  - O `OnPostAsync` método do manipulador chama o método [RedirectToPage](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.redirecttopage) auxiliar. `RedirectToPage` retorna uma instância de [RedirectToPageResult](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.redirecttopageresult). `RedirectToPage`:
    - É um resultado da ação.
    - É semelhante a `RedirectToAction` ou `RedirectToRoute` (usado em controladores e exibições).
    - É personalizado para páginas. Na amostra anterior, ele redireciona para a página de Índice raiz (`/Index`). `RedirectToPage`é detalhado na seção [Geração de URL para Páginas.](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#url_gen)

- Com erros de validação que são passados para o servidor:

  - O `OnPostAsync` método do manipulador chama o método [Page](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagebase.page) auxiliar. `Page` retorna uma instância de [PageResult](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pageresult). Retornar `Page` é semelhante a como as ações em controladores retornam `View`. `PageResult` é o tipo de retorno padrão para um método de manipulador. Um método de manipulador que retorna `void` renderiza a página.
  - No exemplo anterior, postar o formulário sem valor resulta em [ModelState.IsValid retornando](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary.isvalid#Microsoft_AspNetCore_Mvc_ModelBinding_ModelStateDictionary_IsValid) false. Neste exemplo, nenhum erro de validação é exibido no cliente. A entrega de erro de validação é abordada posteriormente neste documento.

  C#Copiar

  ```csharp
  public async Task<IActionResult> OnPostAsync()
  {
      if (!ModelState.IsValid)
      {
          return Page();
      }
  
      _context.Customers.Add(Customer);
      await _context.SaveChangesAsync();
  
      return RedirectToPage("./Index");
  }
  ```

- Com erros de validação detectados pela validação do lado do cliente:

  - Os dados **não** são postados no servidor.
  - A validação do lado do cliente é explicada posteriormente neste documento.

A `Customer` propriedade usa o atributo para optar por [`[BindProperty\]`](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) model binding:

C#Copiar

```csharp
public class CreateModel : PageModel
{
    private readonly CustomerDbContext _context;

    public CreateModel(CustomerDbContext context)
    {
        _context = context;
    }

    public IActionResult OnGet()
    {
        return Page();
    }

    [BindProperty]
    public Customer Customer { get; set; }

    public async Task<IActionResult> OnPostAsync()
    {
        if (!ModelState.IsValid)
        {
            return Page();
        }

        _context.Customers.Add(Customer);
        await _context.SaveChangesAsync();

        return RedirectToPage("./Index");
    }
}
```

`[BindProperty]` não **deve** ser usado em modelos que contêm propriedades que não devem ser alteradas pelo cliente. Para obter mais informações, consulte [Overposting](https://docs.microsoft.com/pt-br/aspnet/core/data/ef-rp/crud?view=aspnetcore-6.0#overposting).

Razor Páginas, por padrão, vinculam propriedades somente a `GET` verbos não. A associação a propriedades remove a necessidade de escrever código para converter dados HTTP no tipo de modelo. A associação reduz o código usando a mesma propriedade para renderizar os campos de formulário (`<input asp-for="Customer.Name">`) e aceitar a entrada.

 Aviso

Por motivos de segurança, você deve aceitar associar os dados da solicitação `GET` às propriedades do modelo de página. Verifique a entrada do usuário antes de mapeá-la para as propriedades. Optar `GET` pela associação é útil ao abordar cenários que dependem de cadeias de caracteres de consulta ou valores de rota.

Para associar uma propriedade em `GET` solicitações, defina a [`[BindProperty\]`](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) Propriedade do atributo `SupportsGet` como `true` :

C#Copiar

```csharp
[BindProperty(SupportsGet = true)]
```

Para obter mais informações, consulte [ASP.NET Core Community encontros: associar em obter discussão (YouTube)](https://www.youtube.com/watch?v=p7iHB9V-KVU&feature=youtu.be&t=54m27s).

Revendo o *arquivo de exibição Pages/Create.cshtml:*

CSHTMLCopiar

```cshtml
@page
@model RazorPagesContacts.Pages.Customers.CreateModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<p>Enter a customer name:</p>

<form method="post">
    Name:
    <input asp-for="Customer.Name" />
    <input type="submit" />
</form>
```

- No código anterior, o auxiliar de [marca de entrada](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-6.0#the-input-tag-helper) vincula o elemento HTML à expressão de `<input asp-for="Customer.Name" />` `<input>` `Customer.Name` modelo.
- [`@addTagHelper`](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0#addtaghelper-makes-tag-helpers-available) disponibiliza os Auxiliares de Marca.

### Home page

*Index.cshtml* é o home page:

CSHTMLCopiar

```cshtml
@page
@model RazorPagesContacts.Pages.Customers.IndexModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<h1>Contacts home page</h1>
<form method="post">
    <table class="table">
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            @foreach (var contact in Model.Customer)
            {
                <tr>
                    <td> @contact.Id  </td>
                    <td>@contact.Name</td>
                    <td>
                        <a asp-page="./Edit" asp-route-id="@contact.Id">Edit</a> |
                        <button type="submit" asp-page-handler="delete"
                                asp-route-id="@contact.Id">delete
                        </button>
                    </td>
                </tr>
            }
        </tbody>
    </table>
    <a asp-page="Create">Create New</a>
</form>
```

A classe `PageModel` (*Index.cshtml.cs*) associada:

C#Copiar

```csharp
public class IndexModel : PageModel
{
    private readonly CustomerDbContext _context;

    public IndexModel(CustomerDbContext context)
    {
        _context = context;
    }

    public IList<Customer> Customer { get; set; }

    public async Task OnGetAsync()
    {
        Customer = await _context.Customers.ToListAsync();
    }

    public async Task<IActionResult> OnPostDeleteAsync(int id)
    {
        var contact = await _context.Customers.FindAsync(id);

        if (contact != null)
        {
            _context.Customers.Remove(contact);
            await _context.SaveChangesAsync();
        }

        return RedirectToPage();
    }
}
```

O *arquivo Index.cshtml* contém a seguinte marcação:

CSHTMLCopiar

```cshtml
<td>
```

O `<a /a>` [Auxiliar de Marca de Âncora](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/built-in/anchor-tag-helper?view=aspnetcore-6.0) usou o atributo para gerar um link para a página `asp-route-{value}` Editar. O link contém dados de rota com a ID de contato. Por exemplo, `https://localhost:5001/Edit/1`. [Os Auxiliares de Marca](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0) permitem que o código do lado do servidor participe da criação e renderização de elementos HTML em Razor arquivos.

O *arquivo Index.cshtml* contém marcação para criar um botão excluir para cada contato do cliente:

CSHTMLCopiar

```cshtml
<a asp-page="./Edit" asp-route-id="@contact.Id">Edit</a> |
<button type="submit" asp-page-handler="delete"
```

O HTML renderizado:

HTMLCopiar

```html
<button type="submit" formaction="/Customers?id=1&amp;handler=delete">delete</button>
```

Quando o botão excluir é renderizado em HTML, sua [formação](https://developer.mozilla.org/docs/Web/HTML/Element/button#attr-formaction) inclui parâmetros para:

- A ID de contato do cliente, especificada pelo `asp-route-id` atributo .
- O `handler` , especificado pelo atributo `asp-page-handler` .

Quando o botão é selecionado, uma solicitação de formulário `POST` é enviada para o servidor. Por convenção, o nome do método do manipulador é selecionado com base no valor do parâmetro `handler` de acordo com o esquema `OnPost[handler]Async`.

Como o `handler` é `delete` neste exemplo, o método do manipulador `OnPostDeleteAsync` é usado para processar a solicitação `POST`. Se `asp-page-handler` for definido como um valor diferente, como `remove`, um método de manipulador com o nome `OnPostRemoveAsync` será selecionado.

C#Copiar

```csharp
public async Task<IActionResult> OnPostDeleteAsync(int id)
{
    var contact = await _context.Customers.FindAsync(id);

    if (contact != null)
    {
        _context.Customers.Remove(contact);
        await _context.SaveChangesAsync();
    }

    return RedirectToPage();
}
```

O método `OnPostDeleteAsync`:

- Obtém o `id` da cadeia de caracteres de consulta.
- Consulta o banco de dados para o contato de cliente com `FindAsync`.
- Se o contato do cliente for encontrado, ele será removido e o banco de dados será atualizado.
- Chama [RedirectToPage](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.redirecttopage) para redirecionar para a página de índice de raiz (`/Index`).

### O arquivo Edit.cshtml

CSHTMLCopiar

```cshtml
@page "{id:int}"
@model RazorPagesContacts.Pages.Customers.EditModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers


<h1>Edit Customer - @Model.Customer.Id</h1>
<form method="post">
    <div asp-validation-summary="All"></div>
    <input asp-for="Customer.Id" type="hidden" />
    <div>
        <label asp-for="Customer.Name"></label>
        <div>
            <input asp-for="Customer.Name" />
            <span asp-validation-for="Customer.Name"></span>
        </div>
    </div>

    <div>
        <button type="submit">Save</button>
    </div>
</form>
```

A primeira linha contém a diretiva `@page "{id:int}"`. A restrição de `"{id:int}"` roteamento informa à página para aceitar solicitações para a página que contêm dados `int` de rota. Se uma solicitação para a página não contém dados de rota que podem ser convertidos em um `int`, o runtime retorna um erro HTTP 404 (não encontrado). Para tornar a ID opcional, acrescente `?` à restrição de rota:

CSHTMLCopiar

```cshtml
@page "{id:int?}"
```

O *arquivo Edit.cshtml.cs:*

C#Copiar

```csharp
public class EditModel : PageModel
{
    private readonly CustomerDbContext _context;

    public EditModel(CustomerDbContext context)
    {
        _context = context;
    }

    [BindProperty]
    public Customer Customer { get; set; }

    public async Task<IActionResult> OnGetAsync(int id)
    {
        Customer = await _context.Customers.FindAsync(id);

        if (Customer == null)
        {
            return RedirectToPage("./Index");
        }

        return Page();
    }

    public async Task<IActionResult> OnPostAsync()
    {
        if (!ModelState.IsValid)
        {
            return Page();
        }

        _context.Attach(Customer).State = EntityState.Modified;

        try
        {
            await _context.SaveChangesAsync();
        }
        catch (DbUpdateConcurrencyException)
        {
            throw new Exception($"Customer {Customer.Id} not found!");
        }

        return RedirectToPage("./Index");
    }

}
```

## Validação

Regras de validação:

- São especificados declarativamente na classe de modelo.
- São impostas em todos os lugares no aplicativo.

O namespace fornece um conjunto de atributos de validação integrados que [System.ComponentModel.DataAnnotations](https://docs.microsoft.com/pt-br/dotnet/api/system.componentmodel.dataannotations) são aplicados declarativamente a uma classe ou propriedade. DataAnnotations também contém atributos de formatação como que ajudam na formatação e [`[DataType\]`](https://docs.microsoft.com/pt-br/dotnet/api/system.componentmodel.dataannotations.datatypeattribute) não fornecem nenhuma validação.

Considere o `Customer` modelo:

C#Copiar

```csharp
using System.ComponentModel.DataAnnotations;

namespace RazorPagesContacts.Models
{
    public class Customer
    {
        public int Id { get; set; }

        [Required, StringLength(10)]
        public string Name { get; set; }
    }
}
```

Usando o seguinte *arquivo de exibição Create.cshtml:*

CSHTMLCopiar

```cshtml
@page
@model RazorPagesContacts.Pages.Customers.CreateModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<p>Validation: customer name:</p>

<form method="post">
    <div asp-validation-summary="ModelOnly"></div>
    <span asp-validation-for="Customer.Name"></span>
    Name:
    <input asp-for="Customer.Name" />
    <input type="submit" />
</form>

<script src="~/lib/jquery/dist/jquery.js"></script>
<script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
<script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
```

O código anterior:

- Inclui scripts de validação jQuery e jQuery.

- Usa os `<div />` `<span />` [Auxiliares de Marca e](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0) para habilitar:

  - Validação do lado do cliente.
  - Renderização de erro de validação.

- Gera o seguinte HTML:

  HTMLCopiar

  ```html
  <p>Enter a customer name:</p>
  
  <form method="post">
      Name:
      <input type="text" data-val="true"
             data-val-length="The field Name must be a string with a maximum length of 10."
             data-val-length-max="10" data-val-required="The Name field is required."
             id="Customer_Name" maxlength="10" name="Customer.Name" value="" />
      <input type="submit" />
      <input name="__RequestVerificationToken" type="hidden"
             value="<Antiforgery token here>" />
  </form>
  
  <script src="/lib/jquery/dist/jquery.js"></script>
  <script src="/lib/jquery-validation/dist/jquery.validate.js"></script>
  <script src="/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
  ```

Postar o formulário Criar sem um valor de nome exibe a mensagem de erro "O campo Nome é obrigatório". no formulário. Se o JavaScript estiver habilitado no cliente, o navegador exibirá o erro sem postar no servidor.

O `[StringLength(10)]` atributo é gerado no HTML `data-val-length-max="10"` renderizado. `data-val-length-max` impede que os navegadores entrem mais do que o comprimento máximo especificado. Se uma ferramenta como [o Fiddler](https://www.telerik.com/fiddler) for usada para editar e repetir a postagem:

- Com o nome maior que 10.
- A mensagem de erro "O nome do campo deve ser uma cadeia de caracteres com um comprimento máximo de 10". é retornado.

Considere o seguinte `Movie` modelo:

C#Copiar

```csharp
using System;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace RazorPagesMovie.Models
{
    public class Movie
    {
        public int ID { get; set; }

        [StringLength(60, MinimumLength = 3)]
        [Required]
        public string Title { get; set; }

        [Display(Name = "Release Date")]
        [DataType(DataType.Date)]
        public DateTime ReleaseDate { get; set; }

        [Range(1, 100)]
        [DataType(DataType.Currency)]
        [Column(TypeName = "decimal(18, 2)")]
        public decimal Price { get; set; }

        [RegularExpression(@"^[A-Z]+[a-zA-Z\s]*$")]
        [Required]
        [StringLength(30)]
        public string Genre { get; set; }

        [RegularExpression(@"^[A-Z]+[a-zA-Z0-9""'\s-]*$")]
        [StringLength(5)]
        [Required]
        public string Rating { get; set; }
    }
}
```

Os atributos de validação especificam o comportamento a ser aplicado nas propriedades do modelo às quais eles são aplicados:

- Os atributos e indicam que uma propriedade deve ter um valor, mas nada impede que um usuário entre em espaço em `Required` branco para atender a essa `MinimumLength` validação.
- O atributo `RegularExpression` é usado para limitar quais caracteres podem ser inseridos. No código anterior, "Gênero":
  - Deve usar apenas letras.
  - A primeira letra deve ser maiúscula. Espaços em branco, números e caracteres especiais não são permitidos.
- A "Classificação" `RegularExpression`:
  - Exige que o primeiro caractere seja uma letra maiúscula.
  - Permite caracteres especiais e números em espaços subsequentes. "PG-13" é válido para uma classificação, mas é um erro em "Gênero".
- O atributo `Range` restringe um valor a um intervalo especificado.
- O atributo define o comprimento máximo de uma propriedade de cadeia `StringLength` de caracteres e, opcionalmente, seu comprimento mínimo.
- Os tipos de valor (como `decimal`, `int`, `float`, `DateTime`) são inerentemente necessários e não precisam do atributo `[Required]`.

A página Criar para o `Movie` modelo mostra erros com valores inválidos:

![Formulário da exibição de filmes com vários erros de validação do lado do cliente do jQuery](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/validation/_static/val.png?view=aspnetcore-6.0)

Para obter mais informações, consulte:

- [Adicionar validação ao aplicativo Movie](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/validation?view=aspnetcore-6.0)
- [Validação de modelo ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/models/validation?view=aspnetcore-6.0).

## Manipular solicitações HEAD com um fallback de manipulador OnGet

`HEAD` solicitações permitem recuperar os headers de um recurso específico. Diferente das solicitações `GET`, as solicitações `HEAD` não retornam um corpo de resposta.

Geralmente, um manipulador `OnHead` é criado e chamado para solicitações `HEAD`:

C#Copiar

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("Head Test", "Handled by OnHead!");
}
```

Razor As páginas voltarão a chamar o `OnGet` manipulador se nenhum manipulador for `OnHead` definido.



## XSRF/CSRF e Razor páginas

RazorAs páginas são protegidas pela [validação antiforjada.](https://docs.microsoft.com/pt-br/aspnet/core/security/anti-request-forgery?view=aspnetcore-6.0) O [FormTagHelper](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-6.0#the-form-tag-helper) injeta tokens antiforjada em elementos de formulário HTML.



## Usando layouts, parciais, modelos e auxiliares de marca com Razor páginas

As páginas funcionam com todos os recursos do mecanismo Razor de exibição. Layouts, parciais, modelos, Auxiliares de Marca, *_ViewStart.cshtml* e *_ViewImports.cshtml* funcionam da mesma maneira que para exibições Razor convencionais.

Organizaremos essa página aproveitando alguns desses recursos.

Adicione uma [página de layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0) a *Pages/Shared/_Layout.cshtml*:

CSHTMLCopiar

```cshtml
<!DOCTYPE html>
<html>
<head>
    <title>RP Sample</title>
    <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.css" />
</head>
<body>
    <a asp-page="/Index">Home</a>
    <a asp-page="/Customers/Create">Create</a>
    <a asp-page="/Customers/Index">Customers</a> <br />

    @RenderBody()
    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
    <script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
</body>
</html>
```

O [Layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0):

- Controla o layout de cada página (a menos que a página opte por não usar o layout).
- Importa estruturas HTML como JavaScript e folhas de estilo.
- O conteúdo da Razor página é renderizado onde `@RenderBody()` é chamado.

Para obter mais informações, consulte [página de layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0).

A propriedade [Layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0#specifying-a-layout) é definida em *Pages/_ViewStart.cshtml*:

CSHTMLCopiar

```cshtml
@{
    Layout = "_Layout";
}
```

O layout está na pasta *Pages/Shared*. As páginas buscam outras exibições (layouts, modelos, parciais) hierarquicamente, iniciando na mesma pasta que a página atual. Um layout na pasta *páginas/compartilhadas* pode ser usado em qualquer Razor página na pasta *páginas* .

O arquivo de layout deve entrar na pasta *Pages/Shared*.

Recomendamos que você **não** coloque o arquivo de layout na pasta *Views/Shared*. *Views/Shared* é um padrão de exibições do MVC. Razor As páginas destinam-se a contar com a hierarquia de pastas, não com convenções de caminho.

Exibir pesquisa de uma Razor página inclui a pasta *páginas* . Os layouts, modelos e parciais usados com controladores MVC e Razor exibições convencionais *funcionam apenas*.

Adicione um arquivo *Pages/_ViewImports.cshtml*:

CSHTMLCopiar

```cshtml
@namespace RazorPagesContacts.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

`@namespace` é explicado posteriormente no tutorial. A diretiva `@addTagHelper` coloca os [auxiliares de marcas internos](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/built-in/?view=aspnetcore-6.0) em todas as páginas na pasta *Pages*.



A `@namespace` diretiva definida em uma página:

CSHTMLCopiar

```cshtml
@page
@namespace RazorPagesIntro.Pages.Customers

@model NameSpaceModel

<h2>Name space</h2>
<p>
    @Model.Message
</p>
```

A `@namespace` diretiva define o namespace para a página. A diretiva `@model` não precisa incluir o namespace.

Quando a diretiva `@namespace` está contida em *_ViewImports.cshtml*, o namespace especificado fornece o prefixo do namespace gerado na página que importa a diretiva `@namespace`. O restante do namespace gerado (a parte do sufixo) é o caminho relativo separado por ponto entre a pasta que contém *_ViewImports.cshtml* e a pasta que contém a página.

Por exemplo, a classe `PageModel`*Pages/Customers/Edit.cshtml.cs* define explicitamente o namespace:

C#Copiar

```csharp
namespace RazorPagesContacts.Pages
{
    public class EditModel : PageModel
    {
        private readonly AppDbContext _db;

        public EditModel(AppDbContext db)
        {
            _db = db;
        }

        // Code removed for brevity.
```

O arquivo *Pages/_ViewImports.cshtml* define o namespace a seguir:

CSHTMLCopiar

```cshtml
@namespace RazorPagesContacts.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

O namespace gerado para a página *pages/Customers/Edit. cshtml* Razor é o mesmo que a `PageModel` classe.

`@namespace`*também funciona com Razor exibições convencionais.*

Considere o arquivo de exibição *páginas/Create. cshtml* :

CSHTMLCopiar

```cshtml
@page
@model RazorPagesContacts.Pages.Customers.CreateModel
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<p>Validation: customer name:</p>

<form method="post">
    <div asp-validation-summary="ModelOnly"></div>
    <span asp-validation-for="Customer.Name"></span>
    Name:
    <input asp-for="Customer.Name" />
    <input type="submit" />
</form>

<script src="~/lib/jquery/dist/jquery.js"></script>
<script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
<script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
```

O arquivo de exibição *páginas/Create. cshtml* atualizado com *_ViewImports. cshtml* e o arquivo de layout anterior:

CSHTMLCopiar

```cshtml
@page
@model CreateModel

<p>Enter a customer name:</p>

<form method="post">
    Name:
    <input asp-for="Customer.Name" />
    <input type="submit" />
</form>
```

No código anterior, o *_ViewImports. cshtml* importou os auxiliares de namespace e de marca. O arquivo de layout importou os arquivos JavaScript.

O [Razor projeto inicial de páginas](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#rpvs17) contém as *páginas/_ValidationScriptsPartial. cshtml*, que conectam a validação do lado do cliente.

Para obter mais informações sobre exibições parciais, consulte [Exibições parciais no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/partial?view=aspnetcore-6.0).



## Geração de URL para Páginas

A página `Create`, exibida anteriormente, usa `RedirectToPage`:

C#Copiar

```csharp
public class CreateModel : PageModel
{
    private readonly CustomerDbContext _context;

    public CreateModel(CustomerDbContext context)
    {
        _context = context;
    }

    public IActionResult OnGet()
    {
        return Page();
    }

    [BindProperty]
    public Customer Customer { get; set; }

    public async Task<IActionResult> OnPostAsync()
    {
        if (!ModelState.IsValid)
        {
            return Page();
        }

        _context.Customers.Add(Customer);
        await _context.SaveChangesAsync();

        return RedirectToPage("./Index");
    }
}
```

O aplicativo tem a estrutura de arquivos/pastas a seguir:

- */Pages*
  - *Index.cshtml*
  - *Privacy. cshtml*
  - */Customers*
    - *Create.cshtml*
    - *Edit.cshtml*
    - *Index.cshtml*

As páginas *pages/Customers/Create. cshtml* e *pages/Customers/Edit. cshtml* redirecionam para *pages/Customers/index. cshtml* após o êxito. A cadeia de caracteres `./Index` é um nome de página relativo usado para acessar a página anterior. Ele é usado para gerar URLs para a página *pages/Customers/index. cshtml* . Por exemplo:

- `Url.Page("./Index", ...)`
- `<a asp-page="./Index">Customers Index Page</a>`
- `RedirectToPage("./Index")`

O nome de página absoluto `/Index` é usado para gerar URLs para a página *pages/index. cshtml* . Por exemplo:

- `Url.Page("/Index", ...)`
- `<a asp-page="/Index">Home Index Page</a>`
- `RedirectToPage("/Index")`

O nome da página é o caminho para a página da pasta raiz */Pages*, incluindo um `/` à direita (por exemplo, `/Index`). Os exemplos de geração de URL anteriores oferecem opções avançadas e recursos funcionais por meio da codificação de uma URL. A geração de URL usa [roteamento](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/routing?view=aspnetcore-6.0) e pode gerar e codificar parâmetros de acordo com o modo como a rota é definida no caminho de destino.

A Geração de URL para páginas dá suporte a nomes relativos. A tabela a seguir mostra qual página de índice é selecionada usando `RedirectToPage` parâmetros diferentes em *pages/Customers/Create. cshtml*.

| RedirectToPage(x)          | ?                       |
| :------------------------- | :---------------------- |
| RedirectToPage("/Index")   | *Pages/Index*           |
| RedirectToPage("./Index"); | *Pages/Customers/Index* |
| RedirectToPage("../Index") | *Pages/Index*           |
| RedirectToPage("Index")    | *Pages/Customers/Index* |

`RedirectToPage("Index")`, `RedirectToPage("./Index")` e `RedirectToPage("../Index")` são *nomes relativos*. O parâmetro `RedirectToPage` é *combinado* com o caminho da página atual para calcular o nome da página de destino.

Vinculação de nome relativo é útil ao criar sites com uma estrutura complexa. Quando nomes relativos são usados para vincular entre páginas em uma pasta:

- Renomear uma pasta não interrompe os links relativos.
- Os links não são desfeitos porque não incluem o nome da pasta.

Para redirecionar para uma página em uma [área](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/areas?view=aspnetcore-6.0) diferente, especifique essa área:

C#Copiar

```csharp
RedirectToPage("/Index", new { area = "Services" });
```

Para obter mais informações, consulte [Áreas no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/areas?view=aspnetcore-6.0) e [RazorDirecionamento de páginas e convenções de aplicativo no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/razor-pages-conventions?view=aspnetcore-6.0).

## Atributo ViewData

Os dados podem ser passados para uma página com [ViewDataAttribute](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute) . As propriedades com o `[ViewData]` atributo têm seus valores armazenados e carregados do [ViewDataDictionary](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) .

No exemplo a seguir, o `AboutModel` aplica o `[ViewData]` atributo à `Title` Propriedade:

C#Copiar

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

Na página Sobre, acesse a propriedade `Title` como uma propriedade de modelo:

CSHTMLCopiar

```cshtml
<h1>@Model.Title</h1>
```

No layout, o título é lido a partir do dicionário ViewData:

CSHTMLCopiar

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

## TempData

ASP.NET Core expõe o [TempData](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata#Microsoft_AspNetCore_Mvc_Controller_TempData) . Essa propriedade armazena dados até eles serem lidos. Os métodos [Keep](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.tempdatadictionary.keep) e [Peek](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.tempdatadictionary.peek) podem ser usados para examinar os dados sem exclusão. `TempData` é útil para redirecionamento, quando os dados são necessários para mais do que uma única solicitação.

Os conjuntos de código a seguir definem o valor de `Message` usando `TempData`:

C#Copiar

```csharp
public class CreateDotModel : PageModel
{
    private readonly AppDbContext _db;

    public CreateDotModel(AppDbContext db)
    {
        _db = db;
    }

    [TempData]
    public string Message { get; set; }

    [BindProperty]
    public Customer Customer { get; set; }

    public async Task<IActionResult> OnPostAsync()
    {
        if (!ModelState.IsValid)
        {
            return Page();
        }

        _db.Customers.Add(Customer);
        await _db.SaveChangesAsync();
        Message = $"Customer {Customer.Name} added";
        return RedirectToPage("./Index");
    }
}
```

A marcação a seguir no arquivo *Pages/Customers/Index.cshtml* exibe o valor de `Message` usando `TempData`.

CSHTMLCopiar

```cshtml
<h3>Msg: @Model.Message</h3>
```

O modelo de página *Pages/Customers/Index.cshtml.cs* aplica o atributo `[TempData]` à propriedade `Message`.

C#Copiar

```csharp
[TempData]
public string Message { get; set; }
```

Para obter mais informações, consulte [TempData](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/app-state?view=aspnetcore-6.0#tempdata).



## Vários manipuladores por página

A página a seguir gera marcação para dois manipuladores usando o auxiliar de marcação `asp-page-handler`:

CSHTMLCopiar

```cshtml
@page
@model CreateFATHModel

<html>
<body>
    <p>
        Enter your name.
    </p>
    <div asp-validation-summary="All"></div>
    <form method="POST">
        <div>Name: <input asp-for="Customer.Name" /></div>
        <input type="submit" asp-page-handler="JoinList" value="Join" />
        <input type="submit" asp-page-handler="JoinListUC" value="JOIN UC" />
    </form>
</body>
</html>
```

O formulário no exemplo anterior tem dois botões de envio, cada um usando o `FormActionTagHelper` para enviar para uma URL diferente. O atributo `asp-page-handler` é um complemento para `asp-page`. `asp-page-handler` gera URLs que enviam para cada um dos métodos de manipulador definidos por uma página. `asp-page` não foi especificado porque a amostra está vinculando à página atual.

O modelo de página:

C#Copiar

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;
using RazorPagesContacts.Data;

namespace RazorPagesContacts.Pages.Customers
{
    public class CreateFATHModel : PageModel
    {
        private readonly AppDbContext _db;

        public CreateFATHModel(AppDbContext db)
        {
            _db = db;
        }

        [BindProperty]
        public Customer Customer { get; set; }

        public async Task<IActionResult> OnPostJoinListAsync()
        {
            if (!ModelState.IsValid)
            {
                return Page();
            }

            _db.Customers.Add(Customer);
            await _db.SaveChangesAsync();
            return RedirectToPage("/Index");
        }

        public async Task<IActionResult> OnPostJoinListUCAsync()
        {
            if (!ModelState.IsValid)
            {
                return Page();
            }
            Customer.Name = Customer.Name?.ToUpperInvariant();
            return await OnPostJoinListAsync();
        }
    }
}
```

O código anterior usa *métodos de manipulador nomeados*. Métodos de manipulador nomeados são criados colocando o texto no nome após `On<HTTP Verb>` e antes de `Async` (se houver). No exemplo anterior, os métodos de página são OnPost **JoinList** Async e OnPost **JoinListUC** Async. Com *OnPost* e *Async* removidos, os nomes de manipulador são `JoinList` e `JoinListUC`.

CSHTMLCopiar

```cshtml
<input type="submit" asp-page-handler="JoinList" value="Join" />
<input type="submit" asp-page-handler="JoinListUC" value="JOIN UC" />
```

Usando o código anterior, o caminho da URL que envia a `OnPostJoinListAsync` é `https://localhost:5001/Customers/CreateFATH?handler=JoinList`. O caminho da URL que envia a `OnPostJoinListUCAsync` é `https://localhost:5001/Customers/CreateFATH?handler=JoinListUC`.

## Rotas personalizadas

Use a diretiva `@page` para:

- Especifique uma rota personalizada para uma página. Por exemplo, a rota para a página Sobre pode ser definida como `/Some/Other/Path` com `@page "/Some/Other/Path"`.
- Acrescente segmentos à rota padrão de uma página. Por exemplo, um segmento de "item" pode ser adicionado à rota padrão da página com `@page "item"`.
- Acrescente parâmetros à rota padrão de uma página. Por exemplo, um parâmetro de ID, `id`, pode ser necessário para uma página com `@page "{id}"`.

Há suporte para um caminho relativo à raiz designado por um til (`~`) no início do caminho. Por exemplo, `@page "~/Some/Other/Path"` é o mesmo que `@page "/Some/Other/Path"`.

Se você não gostar da cadeia de caracteres de consulta `?handler=JoinList` na URL, altere a rota para colocar o nome do manipulador na parte do caminho da URL. A rota pode ser personalizada adicionando um modelo de rota entre aspas duplas após a `@page` diretiva.

CSHTMLCopiar

```cshtml
@page "{handler?}"
@model CreateRouteModel

<html>
<body>
    <p>
        Enter your name.
    </p>
    <div asp-validation-summary="All"></div>
    <form method="POST">
        <div>Name: <input asp-for="Customer.Name" /></div>
        <input type="submit" asp-page-handler="JoinList" value="Join" />
        <input type="submit" asp-page-handler="JoinListUC" value="JOIN UC" />
    </form>
</body>
</html>
```

Usando o código anterior, o caminho da URL que envia a `OnPostJoinListAsync` é `https://localhost:5001/Customers/CreateFATH/JoinList`. O caminho da URL que envia a `OnPostJoinListUCAsync` é `https://localhost:5001/Customers/CreateFATH/JoinListUC`.

O `?` após `handler` significa que o parâmetro de rota é opcional.

## Configuração e configurações avançadas

A configuração e as configurações nas seções a seguir não são exigidas pela maioria dos aplicativos.

Para configurar opções avançadas, use a [AddRazorPages](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addrazorpages) sobrecarga que configura [RazorPagesOptions](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions) :

C#Copiar

```csharp
public void ConfigureServices(IServiceCollection services)
{            
    services.AddRazorPages(options =>
    {
        options.RootDirectory = "/MyPages";
        options.Conventions.AuthorizeFolder("/MyPages/Admin");
    });
}
```

Use o [RazorPagesOptions](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions) para definir o diretório raiz para páginas ou adicione convenções de modelo de aplicativo para páginas. Para obter mais informações sobre convenções, consulte [Razor páginas convenções de autorização](https://docs.microsoft.com/pt-br/aspnet/core/security/authorization/razor-pages-authorization?view=aspnetcore-6.0).

Para pré-compilar exibições, consulte [Razor Exibir compilação](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/view-compilation?view=aspnetcore-6.0).

### Especificar que Razor as páginas estão na raiz do conteúdo

Por padrão, Razor as páginas têm raiz no diretório */pages* Adicionar [WithRazorPagesAtContentRoot](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) para especificar que suas Razor páginas estão na [raiz do conteúdo](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/?view=aspnetcore-6.0#content-root) ( [ContentRootPath](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath#Microsoft_AspNetCore_Hosting_IHostingEnvironment_ContentRootPath) ) do aplicativo:

C#Copiar

```csharp
public void ConfigureServices(IServiceCollection services)
{            
    services.AddRazorPages(options =>
        {
            options.Conventions.AuthorizeFolder("/MyPages/Admin");
        })
        .WithRazorPagesAtContentRoot();
}
```

### Especificar que as Razor páginas estejam em um diretório raiz personalizado

Adicionar [WithRazorPagesRoot](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) para especificar que as Razor páginas estão em um diretório raiz personalizado no aplicativo (forneça um caminho relativo):

C#Copiar

```csharp
public void ConfigureServices(IServiceCollection services)
{            
    services.AddRazorPages(options =>
        {
            options.Conventions.AuthorizeFolder("/MyPages/Admin");
        })
        .WithRazorPagesRoot("/path/to/razor/pages");
}
```

## Recursos adicionais

- Consulte Introdução [às Razor páginas](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0), que se baseia nesta introdução.

- [Autorizar atributo e Razor páginas](https://docs.microsoft.com/pt-br/aspnet/core/security/authorization/simple?view=aspnetcore-6.0#aarp)

- [Baixar ou exibir código de exemplo](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/razor-pages/index/3.0sample)

- [Introdução ao ASP.NET CIntrodução às Razor páginas no ASP.NET Core

  - 16/08/2021
  - 22 minutos para o fim da leitura
  - - [![img](https://github.com/Rick-Anderson.png?size=32)](https://github.com/Rick-Anderson)
    - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)

  Esta página é útil?

  Por [Rick Anderson](https://twitter.com/RickAndMSFT) e [Ryan Nowak](https://github.com/rynowak)

  Razor As páginas podem tornar cenários com foco na página de codificação mais fáceis e produtivos do que o uso de controladores e exibições.

  Se você estiver procurando um tutorial que utiliza a abordagem Modelo-Exibição-Controlador, consulte a [Introdução ao ASP.NET Core MVC](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0).

  Este documento fornece uma introdução às Razor Páginas. Este não é um tutorial passo a passo. Se você encontrar algumas das seções muito avançadas, [consulte Get started with Razor Pages](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0). Para obter uma visão geral do ASP.NET Core, consulte a [Introdução ao ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-6.0).

  ## Pré-requisitos

  - [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_2_visual-studio)
  - [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_2_visual-studio-code)
  - [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_2_visual-studio-mac)

  - [Visual Studio 2019 16.8 ou posterior](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) com a carga de trabalho de **desenvolvimento da Web e do ASP.NET**
  - [SDK do .NET 5.0](https://dotnet.microsoft.com/download/dotnet/5.0)

  

  ## Criar um Razor projeto de Páginas

  - [Visual Studio](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_3_visual-studio)
  - [Visual Studio Code](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_3_visual-studio-code)
  - [Visual Studio para Mac](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#tabpanel_3_visual-studio-mac)

  Consulte [Começar a usar páginas Razor para](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0) obter instruções detalhadas sobre como criar um Razor projeto de Páginas.

  ## Razor Páginas

  RazorAs páginas estão habilitadas *em Startup.cs:*

  C#Copiar

  ```csharp
  public class Startup
  {
      public Startup(IConfiguration configuration)
      {
          Configuration = configuration;
      }
  
      public IConfiguration Configuration { get; }
  
      public void ConfigureServices(IServiceCollection services)
      {
          services.AddRazorPages();
      }
  
      public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
      {
          if (env.IsDevelopment())
          {
              app.UseDeveloperExceptionPage();
          }
          else
          {
              app.UseExceptionHandler("/Error");
              app.UseHsts();
          }
  
          app.UseHttpsRedirection();
          app.UseStaticFiles();
  
          app.UseRouting();
  
          app.UseAuthorization();
  
          app.UseEndpoints(endpoints =>
          {
              endpoints.MapRazorPages();
          });
      }
  }
  ```

  Considere uma página básica:

  CSHTMLCopiar

  ```cshtml
  @page
  
  <h1>Hello, world!</h1>
  <h2>The time on the server is @DateTime.Now</h2>
  ```

  O código anterior se parece muito com um arquivo [Razor de exibição](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-6.0) usado em um ASP.NET Core com controladores e exibições. O que o torna diferente é a [`@page`](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/razor?view=aspnetcore-6.0#page) diretiva . `@page` transforma o arquivo em uma ação do MVC – o que significa que ele trata solicitações diretamente, sem passar por um controlador. `@page` deve ser a primeira Razor diretiva em uma página. `@page` afeta o comportamento de outros [Razor](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/razor?view=aspnetcore-6.0) constructos. RazorOs nomes de arquivo de páginas *têm um sufixo .cshtml.*

  Uma página semelhante, usando uma classe `PageModel`, é mostrada nos dois arquivos a seguir. O arquivo *Pages/Index2.cshtml*:

  CSHTMLCopiar

  ```cshtml
  @page
  @using RazorPagesIntro.Pages
  @model Index2Model
  
  <h2>Separate page model</h2>
  <p>
      @Model.Message
  </p>
  ```

  O modelo de página *Pages/Index2.cshtml.cs*:

  C#Copiar

  ```csharp
  using Microsoft.AspNetCore.Mvc.RazorPages;
  using Microsoft.Extensions.Logging;
  using System;
  
  namespace RazorPagesIntro.Pages
  {
      public class Index2Model : PageModel
      {
          public string Message { get; private set; } = "PageModel in C#";
  
          public void OnGet()
          {
              Message += $" Server time is { DateTime.Now }";
          }
      }
  }
  ```

  Por convenção, o `PageModel` arquivo de classe tem o mesmo nome que o arquivo Page com Razor *.cs* anexado. Por exemplo, a Razor página anterior é *Pages/Index2.cshtml*. O arquivo que contém a classe `PageModel` é chamado *Pages/Index2.cshtml.cs*.

  As associações de caminhos de URL para páginas são determinadas pelo local da página no sistema de arquivos. A tabela a seguir mostra um Razor caminho de página e a URL correspondente:

  | Caminho e nome do arquivo     | URL correspondente         |
  | :---------------------------- | :------------------------- |
  | */Pages/Index.cshtml*         | `/` ou `/Index`            |
  | */Pages/Contact.cshtml*       | `/Contact`                 |
  | */Pages/Store/Contact.cshtml* | `/Store/Contact`           |
  | */Pages/Store/Index.cshtml*   | `/Store` ou `/Store/Index` |

  Observações:

  - O runtime procura arquivos Razor pages na pasta *Pages* por padrão.
  - `Index` é a página padrão quando uma URL não inclui uma página.

  ## Escrever um formulário básico

  Razor As páginas são projetadas para facilitar a implementação de padrões comuns usados com navegadores da Web ao criar um aplicativo. [Model binding,](https://docs.microsoft.com/pt-br/aspnet/core/mvc/models/model-binding?view=aspnetcore-6.0) [Auxiliares de Marca](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0)e auxiliares HTML *funcionam* apenas com as propriedades definidas em uma Razor classe Page. Considere uma página que implementa um formulário básico "Fale conosco" para o modelo `Contact`:

  Para as amostras neste documento, o `DbContext` é inicializado no arquivo [Startup.cs](https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/razor-pages/index/3.0sample/RazorPagesContacts/Startup.cs#L23-L24).

  O banco de dados na memória requer o `Microsoft.EntityFrameworkCore.InMemory` NuGet pacote.

  C#Copiar

  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {
      services.AddDbContext<CustomerDbContext>(options =>
                        options.UseInMemoryDatabase("name"));
      services.AddRazorPages();
  }
  ```

  O modelo de dados:

  C#Copiar

  ```csharp
  using System.ComponentModel.DataAnnotations;
  
  namespace RazorPagesContacts.Models
  {
      public class Customer
      {
          public int Id { get; set; }
  
          [Required, StringLength(10)]
          public string Name { get; set; }
      }
  }
  ```

  O contexto do banco de dados:

  C#Copiar

  ```csharp
  using Microsoft.EntityFrameworkCore;
  using RazorPagesContacts.Models;
  
  namespace RazorPagesContacts.Data
  {
      public class CustomerDbContext : DbContext
      {
          public CustomerDbContext(DbContextOptions options)
              : base(options)
          {
          }
  
          public DbSet<Customer> Customers { get; set; }
      }
  }
  ```

  O arquivo de exibição *Pages/Create.cshtml*:

  CSHTMLCopiar

  ```cshtml
  @page
  @model RazorPagesContacts.Pages.Customers.CreateModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  <p>Enter a customer name:</p>
  
  <form method="post">
      Name:
      <input asp-for="Customer.Name" />
      <input type="submit" />
  </form>
  ```

  O modelo de página *Pages/Create.cshtml.cs*:

  C#Copiar

  ```csharp
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Mvc.RazorPages;
  using RazorPagesContacts.Data;
  using RazorPagesContacts.Models;
  using System.Threading.Tasks;
  
  namespace RazorPagesContacts.Pages.Customers
  {
      public class CreateModel : PageModel
      {
          private readonly CustomerDbContext _context;
  
          public CreateModel(CustomerDbContext context)
          {
              _context = context;
          }
  
          public IActionResult OnGet()
          {
              return Page();
          }
  
          [BindProperty]
          public Customer Customer { get; set; }
  
          public async Task<IActionResult> OnPostAsync()
          {
              if (!ModelState.IsValid)
              {
                  return Page();
              }
  
              _context.Customers.Add(Customer);
              await _context.SaveChangesAsync();
  
              return RedirectToPage("./Index");
          }
      }
  }
  ```

  Por convenção, a classe `PageModel` é chamada de `<PageName>Model` e está no mesmo namespace que a página.

  A classe `PageModel` permite separar a lógica de uma página da respectiva apresentação. Ela define manipuladores para as solicitações enviadas e os dados usados para renderizar a página. Essa separação permite:

  - Gerenciamento de dependências de página por meio [da injeção de dependência](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-6.0).
  - [Teste de unidade](https://docs.microsoft.com/pt-br/aspnet/core/test/razor-pages-tests?view=aspnetcore-6.0)

  A página tem um *método de manipulador*`OnPostAsync`, que é executado em solicitações `POST` (quando um usuário posta o formulário). Métodos de manipulador para qualquer verbo HTTP podem ser adicionados. Os manipuladores mais comuns são:

  - `OnGet` para inicializar o estado necessário para a página. No código anterior, o `OnGet` método exibe a Página *CreateModel.cshtml.* Razor
  - `OnPost` para manipular envios de formulário.

  O sufixo de nomenclatura `Async` é opcional, mas geralmente é usado por convenção para funções assíncronas. O código anterior é típico para Razor Páginas.

  Se você estiver familiarizado com aplicativos ASP.NET usando controladores e exibições:

  - O `OnPostAsync` código no exemplo anterior é semelhante ao código típico do controlador.
  - A maioria dos primitivos do [MVC, como model binding](https://docs.microsoft.com/pt-br/aspnet/core/mvc/models/model-binding?view=aspnetcore-6.0), validação e resultados de ação, funcionam da mesma forma com Controladores e Razor Páginas.

  O método `OnPostAsync` anterior:

  C#Copiar

  ```csharp
  public async Task<IActionResult> OnPostAsync()
  {
      if (!ModelState.IsValid)
      {
          return Page();
      }
  
      _context.Customers.Add(Customer);
      await _context.SaveChangesAsync();
  
      return RedirectToPage("./Index");
  }
  ```

  O fluxo básico de `OnPostAsync`:

  Verifique se há erros de validação.

  - Se não houver nenhum erro, salve os dados e redirecione.
  - Se houver erros, mostre a página novamente com as mensagens de validação. Em muitos casos, erros de validação seriam detectados no cliente e nunca enviados ao servidor.

  O arquivo de exibição *Pages/Create.cshtml*:

  CSHTMLCopiar

  ```cshtml
  @page
  @model RazorPagesContacts.Pages.Customers.CreateModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  <p>Enter a customer name:</p>
  
  <form method="post">
      Name:
      <input asp-for="Customer.Name" />
      <input type="submit" />
  </form>
  ```

  O HTML renderizado *de Pages/Create.cshtml:*

  HTMLCopiar

  ```html
  <p>Enter a customer name:</p>
  
  <form method="post">
      Name:
      <input type="text" data-val="true"
             data-val-length="The field Name must be a string with a maximum length of 10."
             data-val-length-max="10" data-val-required="The Name field is required."
             id="Customer_Name" maxlength="10" name="Customer.Name" value="" />
      <input type="submit" />
      <input name="__RequestVerificationToken" type="hidden"
             value="<Antiforgery token here>" />
  </form>
  ```

  No código anterior, postando o formulário:

  - Com dados válidos:

    - O `OnPostAsync` método do manipulador chama o método [RedirectToPage](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.redirecttopage) auxiliar. `RedirectToPage` retorna uma instância de [RedirectToPageResult](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.redirecttopageresult). `RedirectToPage`:
      - É um resultado da ação.
      - É semelhante a `RedirectToAction` ou `RedirectToRoute` (usado em controladores e exibições).
      - É personalizado para páginas. Na amostra anterior, ele redireciona para a página de Índice raiz (`/Index`). `RedirectToPage`é detalhado na seção [Geração de URL para Páginas.](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#url_gen)

  - Com erros de validação que são passados para o servidor:

    - O `OnPostAsync` método do manipulador chama o método [Page](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagebase.page) auxiliar. `Page` retorna uma instância de [PageResult](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pageresult). Retornar `Page` é semelhante a como as ações em controladores retornam `View`. `PageResult` é o tipo de retorno padrão para um método de manipulador. Um método de manipulador que retorna `void` renderiza a página.
    - No exemplo anterior, postar o formulário sem valor resulta em [ModelState.IsValid retornando](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.modelstatedictionary.isvalid#Microsoft_AspNetCore_Mvc_ModelBinding_ModelStateDictionary_IsValid) false. Neste exemplo, nenhum erro de validação é exibido no cliente. A entrega de erro de validação é abordada posteriormente neste documento.

    C#Copiar

    ```csharp
    public async Task<IActionResult> OnPostAsync()
    {
        if (!ModelState.IsValid)
        {
            return Page();
        }
    
        _context.Customers.Add(Customer);
        await _context.SaveChangesAsync();
    
        return RedirectToPage("./Index");
    }
    ```

  - Com erros de validação detectados pela validação do lado do cliente:

    - Os dados **não** são postados no servidor.
    - A validação do lado do cliente é explicada posteriormente neste documento.

  A `Customer` propriedade usa o atributo para optar por [`[BindProperty\]`](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) model binding:

  C#Copiar

  ```csharp
  public class CreateModel : PageModel
  {
      private readonly CustomerDbContext _context;
  
      public CreateModel(CustomerDbContext context)
      {
          _context = context;
      }
  
      public IActionResult OnGet()
      {
          return Page();
      }
  
      [BindProperty]
      public Customer Customer { get; set; }
  
      public async Task<IActionResult> OnPostAsync()
      {
          if (!ModelState.IsValid)
          {
              return Page();
          }
  
          _context.Customers.Add(Customer);
          await _context.SaveChangesAsync();
  
          return RedirectToPage("./Index");
      }
  }
  ```

  `[BindProperty]` não **deve** ser usado em modelos que contêm propriedades que não devem ser alteradas pelo cliente. Para obter mais informações, consulte [Overposting](https://docs.microsoft.com/pt-br/aspnet/core/data/ef-rp/crud?view=aspnetcore-6.0#overposting).

  Razor Páginas, por padrão, vinculam propriedades somente a `GET` verbos não. A associação a propriedades remove a necessidade de escrever código para converter dados HTTP no tipo de modelo. A associação reduz o código usando a mesma propriedade para renderizar os campos de formulário (`<input asp-for="Customer.Name">`) e aceitar a entrada.

   Aviso

  Por motivos de segurança, você deve aceitar associar os dados da solicitação `GET` às propriedades do modelo de página. Verifique a entrada do usuário antes de mapeá-la para as propriedades. Optar `GET` pela associação é útil ao abordar cenários que dependem de cadeias de caracteres de consulta ou valores de rota.

  Para associar uma propriedade em `GET` solicitações, defina a [`[BindProperty\]`](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) Propriedade do atributo `SupportsGet` como `true` :

  C#Copiar

  ```csharp
  [BindProperty(SupportsGet = true)]
  ```

  Para obter mais informações, consulte [ASP.NET Core Community encontros: associar em obter discussão (YouTube)](https://www.youtube.com/watch?v=p7iHB9V-KVU&feature=youtu.be&t=54m27s).

  Revendo o *arquivo de exibição Pages/Create.cshtml:*

  CSHTMLCopiar

  ```cshtml
  @page
  @model RazorPagesContacts.Pages.Customers.CreateModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  <p>Enter a customer name:</p>
  
  <form method="post">
      Name:
      <input asp-for="Customer.Name" />
      <input type="submit" />
  </form>
  ```

  - No código anterior, o auxiliar de [marca de entrada](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-6.0#the-input-tag-helper) vincula o elemento HTML à expressão de `<input asp-for="Customer.Name" />` `<input>` `Customer.Name` modelo.
  - [`@addTagHelper`](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0#addtaghelper-makes-tag-helpers-available) disponibiliza os Auxiliares de Marca.

  ### Home page

  *Index.cshtml* é o home page:

  CSHTMLCopiar

  ```cshtml
  @page
  @model RazorPagesContacts.Pages.Customers.IndexModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  <h1>Contacts home page</h1>
  <form method="post">
      <table class="table">
          <thead>
              <tr>
                  <th>ID</th>
                  <th>Name</th>
                  <th></th>
              </tr>
          </thead>
          <tbody>
              @foreach (var contact in Model.Customer)
              {
                  <tr>
                      <td> @contact.Id  </td>
                      <td>@contact.Name</td>
                      <td>
                          <a asp-page="./Edit" asp-route-id="@contact.Id">Edit</a> |
                          <button type="submit" asp-page-handler="delete"
                                  asp-route-id="@contact.Id">delete
                          </button>
                      </td>
                  </tr>
              }
          </tbody>
      </table>
      <a asp-page="Create">Create New</a>
  </form>
  ```

  A classe `PageModel` (*Index.cshtml.cs*) associada:

  C#Copiar

  ```csharp
  public class IndexModel : PageModel
  {
      private readonly CustomerDbContext _context;
  
      public IndexModel(CustomerDbContext context)
      {
          _context = context;
      }
  
      public IList<Customer> Customer { get; set; }
  
      public async Task OnGetAsync()
      {
          Customer = await _context.Customers.ToListAsync();
      }
  
      public async Task<IActionResult> OnPostDeleteAsync(int id)
      {
          var contact = await _context.Customers.FindAsync(id);
  
          if (contact != null)
          {
              _context.Customers.Remove(contact);
              await _context.SaveChangesAsync();
          }
  
          return RedirectToPage();
      }
  }
  ```

  O *arquivo Index.cshtml* contém a seguinte marcação:

  CSHTMLCopiar

  ```cshtml
  <td>
  ```

  O `<a /a>` [Auxiliar de Marca de Âncora](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/built-in/anchor-tag-helper?view=aspnetcore-6.0) usou o atributo para gerar um link para a página `asp-route-{value}` Editar. O link contém dados de rota com a ID de contato. Por exemplo, `https://localhost:5001/Edit/1`. [Os Auxiliares de Marca](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0) permitem que o código do lado do servidor participe da criação e renderização de elementos HTML em Razor arquivos.

  O *arquivo Index.cshtml* contém marcação para criar um botão excluir para cada contato do cliente:

  CSHTMLCopiar

  ```cshtml
  <a asp-page="./Edit" asp-route-id="@contact.Id">Edit</a> |
  <button type="submit" asp-page-handler="delete"
  ```

  O HTML renderizado:

  HTMLCopiar

  ```html
  <button type="submit" formaction="/Customers?id=1&amp;handler=delete">delete</button>
  ```

  Quando o botão excluir é renderizado em HTML, sua [formação](https://developer.mozilla.org/docs/Web/HTML/Element/button#attr-formaction) inclui parâmetros para:

  - A ID de contato do cliente, especificada pelo `asp-route-id` atributo .
  - O `handler` , especificado pelo atributo `asp-page-handler` .

  Quando o botão é selecionado, uma solicitação de formulário `POST` é enviada para o servidor. Por convenção, o nome do método do manipulador é selecionado com base no valor do parâmetro `handler` de acordo com o esquema `OnPost[handler]Async`.

  Como o `handler` é `delete` neste exemplo, o método do manipulador `OnPostDeleteAsync` é usado para processar a solicitação `POST`. Se `asp-page-handler` for definido como um valor diferente, como `remove`, um método de manipulador com o nome `OnPostRemoveAsync` será selecionado.

  C#Copiar

  ```csharp
  public async Task<IActionResult> OnPostDeleteAsync(int id)
  {
      var contact = await _context.Customers.FindAsync(id);
  
      if (contact != null)
      {
          _context.Customers.Remove(contact);
          await _context.SaveChangesAsync();
      }
  
      return RedirectToPage();
  }
  ```

  O método `OnPostDeleteAsync`:

  - Obtém o `id` da cadeia de caracteres de consulta.
  - Consulta o banco de dados para o contato de cliente com `FindAsync`.
  - Se o contato do cliente for encontrado, ele será removido e o banco de dados será atualizado.
  - Chama [RedirectToPage](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.redirecttopage) para redirecionar para a página de índice de raiz (`/Index`).

  ### O arquivo Edit.cshtml

  CSHTMLCopiar

  ```cshtml
  @page "{id:int}"
  @model RazorPagesContacts.Pages.Customers.EditModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  
  <h1>Edit Customer - @Model.Customer.Id</h1>
  <form method="post">
      <div asp-validation-summary="All"></div>
      <input asp-for="Customer.Id" type="hidden" />
      <div>
          <label asp-for="Customer.Name"></label>
          <div>
              <input asp-for="Customer.Name" />
              <span asp-validation-for="Customer.Name"></span>
          </div>
      </div>
  
      <div>
          <button type="submit">Save</button>
      </div>
  </form>
  ```

  A primeira linha contém a diretiva `@page "{id:int}"`. A restrição de `"{id:int}"` roteamento informa à página para aceitar solicitações para a página que contêm dados `int` de rota. Se uma solicitação para a página não contém dados de rota que podem ser convertidos em um `int`, o runtime retorna um erro HTTP 404 (não encontrado). Para tornar a ID opcional, acrescente `?` à restrição de rota:

  CSHTMLCopiar

  ```cshtml
  @page "{id:int?}"
  ```

  O *arquivo Edit.cshtml.cs:*

  C#Copiar

  ```csharp
  public class EditModel : PageModel
  {
      private readonly CustomerDbContext _context;
  
      public EditModel(CustomerDbContext context)
      {
          _context = context;
      }
  
      [BindProperty]
      public Customer Customer { get; set; }
  
      public async Task<IActionResult> OnGetAsync(int id)
      {
          Customer = await _context.Customers.FindAsync(id);
  
          if (Customer == null)
          {
              return RedirectToPage("./Index");
          }
  
          return Page();
      }
  
      public async Task<IActionResult> OnPostAsync()
      {
          if (!ModelState.IsValid)
          {
              return Page();
          }
  
          _context.Attach(Customer).State = EntityState.Modified;
  
          try
          {
              await _context.SaveChangesAsync();
          }
          catch (DbUpdateConcurrencyException)
          {
              throw new Exception($"Customer {Customer.Id} not found!");
          }
  
          return RedirectToPage("./Index");
      }
  
  }
  ```

  ## Validação

  Regras de validação:

  - São especificados declarativamente na classe de modelo.
  - São impostas em todos os lugares no aplicativo.

  O namespace fornece um conjunto de atributos de validação integrados que [System.ComponentModel.DataAnnotations](https://docs.microsoft.com/pt-br/dotnet/api/system.componentmodel.dataannotations) são aplicados declarativamente a uma classe ou propriedade. DataAnnotations também contém atributos de formatação como que ajudam na formatação e [`[DataType\]`](https://docs.microsoft.com/pt-br/dotnet/api/system.componentmodel.dataannotations.datatypeattribute) não fornecem nenhuma validação.

  Considere o `Customer` modelo:

  C#Copiar

  ```csharp
  using System.ComponentModel.DataAnnotations;
  
  namespace RazorPagesContacts.Models
  {
      public class Customer
      {
          public int Id { get; set; }
  
          [Required, StringLength(10)]
          public string Name { get; set; }
      }
  }
  ```

  Usando o seguinte *arquivo de exibição Create.cshtml:*

  CSHTMLCopiar

  ```cshtml
  @page
  @model RazorPagesContacts.Pages.Customers.CreateModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  <p>Validation: customer name:</p>
  
  <form method="post">
      <div asp-validation-summary="ModelOnly"></div>
      <span asp-validation-for="Customer.Name"></span>
      Name:
      <input asp-for="Customer.Name" />
      <input type="submit" />
  </form>
  
  <script src="~/lib/jquery/dist/jquery.js"></script>
  <script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
  <script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
  ```

  O código anterior:

  - Inclui scripts de validação jQuery e jQuery.

  - Usa os `<div />` `<span />` [Auxiliares de Marca e](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-6.0) para habilitar:

    - Validação do lado do cliente.
    - Renderização de erro de validação.

  - Gera o seguinte HTML:

    HTMLCopiar

    ```html
    <p>Enter a customer name:</p>
    
    <form method="post">
        Name:
        <input type="text" data-val="true"
               data-val-length="The field Name must be a string with a maximum length of 10."
               data-val-length-max="10" data-val-required="The Name field is required."
               id="Customer_Name" maxlength="10" name="Customer.Name" value="" />
        <input type="submit" />
        <input name="__RequestVerificationToken" type="hidden"
               value="<Antiforgery token here>" />
    </form>
    
    <script src="/lib/jquery/dist/jquery.js"></script>
    <script src="/lib/jquery-validation/dist/jquery.validate.js"></script>
    <script src="/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
    ```

  Postar o formulário Criar sem um valor de nome exibe a mensagem de erro "O campo Nome é obrigatório". no formulário. Se o JavaScript estiver habilitado no cliente, o navegador exibirá o erro sem postar no servidor.

  O `[StringLength(10)]` atributo é gerado no HTML `data-val-length-max="10"` renderizado. `data-val-length-max` impede que os navegadores entrem mais do que o comprimento máximo especificado. Se uma ferramenta como [o Fiddler](https://www.telerik.com/fiddler) for usada para editar e repetir a postagem:

  - Com o nome maior que 10.
  - A mensagem de erro "O nome do campo deve ser uma cadeia de caracteres com um comprimento máximo de 10". é retornado.

  Considere o seguinte `Movie` modelo:

  C#Copiar

  ```csharp
  using System;
  using System.ComponentModel.DataAnnotations;
  using System.ComponentModel.DataAnnotations.Schema;
  
  namespace RazorPagesMovie.Models
  {
      public class Movie
      {
          public int ID { get; set; }
  
          [StringLength(60, MinimumLength = 3)]
          [Required]
          public string Title { get; set; }
  
          [Display(Name = "Release Date")]
          [DataType(DataType.Date)]
          public DateTime ReleaseDate { get; set; }
  
          [Range(1, 100)]
          [DataType(DataType.Currency)]
          [Column(TypeName = "decimal(18, 2)")]
          public decimal Price { get; set; }
  
          [RegularExpression(@"^[A-Z]+[a-zA-Z\s]*$")]
          [Required]
          [StringLength(30)]
          public string Genre { get; set; }
  
          [RegularExpression(@"^[A-Z]+[a-zA-Z0-9""'\s-]*$")]
          [StringLength(5)]
          [Required]
          public string Rating { get; set; }
      }
  }
  ```

  Os atributos de validação especificam o comportamento a ser aplicado nas propriedades do modelo às quais eles são aplicados:

  - Os atributos e indicam que uma propriedade deve ter um valor, mas nada impede que um usuário entre em espaço em `Required` branco para atender a essa `MinimumLength` validação.
  - O atributo `RegularExpression` é usado para limitar quais caracteres podem ser inseridos. No código anterior, "Gênero":
    - Deve usar apenas letras.
    - A primeira letra deve ser maiúscula. Espaços em branco, números e caracteres especiais não são permitidos.
  - A "Classificação" `RegularExpression`:
    - Exige que o primeiro caractere seja uma letra maiúscula.
    - Permite caracteres especiais e números em espaços subsequentes. "PG-13" é válido para uma classificação, mas é um erro em "Gênero".
  - O atributo `Range` restringe um valor a um intervalo especificado.
  - O atributo define o comprimento máximo de uma propriedade de cadeia `StringLength` de caracteres e, opcionalmente, seu comprimento mínimo.
  - Os tipos de valor (como `decimal`, `int`, `float`, `DateTime`) são inerentemente necessários e não precisam do atributo `[Required]`.

  A página Criar para o `Movie` modelo mostra erros com valores inválidos:

  ![Formulário da exibição de filmes com vários erros de validação do lado do cliente do jQuery](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/validation/_static/val.png?view=aspnetcore-6.0)

  Para obter mais informações, consulte:

  - [Adicionar validação ao aplicativo Movie](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/validation?view=aspnetcore-6.0)
  - [Validação de modelo ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/models/validation?view=aspnetcore-6.0).

  ## Manipular solicitações HEAD com um fallback de manipulador OnGet

  `HEAD` solicitações permitem recuperar os headers de um recurso específico. Diferente das solicitações `GET`, as solicitações `HEAD` não retornam um corpo de resposta.

  Geralmente, um manipulador `OnHead` é criado e chamado para solicitações `HEAD`:

  C#Copiar

  ```csharp
  public void OnHead()
  {
      HttpContext.Response.Headers.Add("Head Test", "Handled by OnHead!");
  }
  ```

  Razor As páginas voltarão a chamar o `OnGet` manipulador se nenhum manipulador for `OnHead` definido.

  

  ## XSRF/CSRF e Razor páginas

  RazorAs páginas são protegidas pela [validação antiforjada.](https://docs.microsoft.com/pt-br/aspnet/core/security/anti-request-forgery?view=aspnetcore-6.0) O [FormTagHelper](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-6.0#the-form-tag-helper) injeta tokens antiforjada em elementos de formulário HTML.

  

  ## Usando layouts, parciais, modelos e auxiliares de marca com Razor páginas

  As páginas funcionam com todos os recursos do mecanismo Razor de exibição. Layouts, parciais, modelos, Auxiliares de Marca, *_ViewStart.cshtml* e *_ViewImports.cshtml* funcionam da mesma maneira que para exibições Razor convencionais.

  Organizaremos essa página aproveitando alguns desses recursos.

  Adicione uma [página de layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0) a *Pages/Shared/_Layout.cshtml*:

  CSHTMLCopiar

  ```cshtml
  <!DOCTYPE html>
  <html>
  <head>
      <title>RP Sample</title>
      <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.css" />
  </head>
  <body>
      <a asp-page="/Index">Home</a>
      <a asp-page="/Customers/Create">Create</a>
      <a asp-page="/Customers/Index">Customers</a> <br />
  
      @RenderBody()
      <script src="~/lib/jquery/dist/jquery.js"></script>
      <script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
      <script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
  </body>
  </html>
  ```

  O [Layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0):

  - Controla o layout de cada página (a menos que a página opte por não usar o layout).
  - Importa estruturas HTML como JavaScript e folhas de estilo.
  - O conteúdo da Razor página é renderizado onde `@RenderBody()` é chamado.

  Para obter mais informações, consulte [página de layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0).

  A propriedade [Layout](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/layout?view=aspnetcore-6.0#specifying-a-layout) é definida em *Pages/_ViewStart.cshtml*:

  CSHTMLCopiar

  ```cshtml
  @{
      Layout = "_Layout";
  }
  ```

  O layout está na pasta *Pages/Shared*. As páginas buscam outras exibições (layouts, modelos, parciais) hierarquicamente, iniciando na mesma pasta que a página atual. Um layout na pasta *páginas/compartilhadas* pode ser usado em qualquer Razor página na pasta *páginas* .

  O arquivo de layout deve entrar na pasta *Pages/Shared*.

  Recomendamos que você **não** coloque o arquivo de layout na pasta *Views/Shared*. *Views/Shared* é um padrão de exibições do MVC. Razor As páginas destinam-se a contar com a hierarquia de pastas, não com convenções de caminho.

  Exibir pesquisa de uma Razor página inclui a pasta *páginas* . Os layouts, modelos e parciais usados com controladores MVC e Razor exibições convencionais *funcionam apenas*.

  Adicione um arquivo *Pages/_ViewImports.cshtml*:

  CSHTMLCopiar

  ```cshtml
  @namespace RazorPagesContacts.Pages
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

  `@namespace` é explicado posteriormente no tutorial. A diretiva `@addTagHelper` coloca os [auxiliares de marcas internos](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/tag-helpers/built-in/?view=aspnetcore-6.0) em todas as páginas na pasta *Pages*.

  

  A `@namespace` diretiva definida em uma página:

  CSHTMLCopiar

  ```cshtml
  @page
  @namespace RazorPagesIntro.Pages.Customers
  
  @model NameSpaceModel
  
  <h2>Name space</h2>
  <p>
      @Model.Message
  </p>
  ```

  A `@namespace` diretiva define o namespace para a página. A diretiva `@model` não precisa incluir o namespace.

  Quando a diretiva `@namespace` está contida em *_ViewImports.cshtml*, o namespace especificado fornece o prefixo do namespace gerado na página que importa a diretiva `@namespace`. O restante do namespace gerado (a parte do sufixo) é o caminho relativo separado por ponto entre a pasta que contém *_ViewImports.cshtml* e a pasta que contém a página.

  Por exemplo, a classe `PageModel`*Pages/Customers/Edit.cshtml.cs* define explicitamente o namespace:

  C#Copiar

  ```csharp
  namespace RazorPagesContacts.Pages
  {
      public class EditModel : PageModel
      {
          private readonly AppDbContext _db;
  
          public EditModel(AppDbContext db)
          {
              _db = db;
          }
  
          // Code removed for brevity.
  ```

  O arquivo *Pages/_ViewImports.cshtml* define o namespace a seguir:

  CSHTMLCopiar

  ```cshtml
  @namespace RazorPagesContacts.Pages
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

  O namespace gerado para a página *pages/Customers/Edit. cshtml* Razor é o mesmo que a `PageModel` classe.

  `@namespace`*também funciona com Razor exibições convencionais.*

  Considere o arquivo de exibição *páginas/Create. cshtml* :

  CSHTMLCopiar

  ```cshtml
  @page
  @model RazorPagesContacts.Pages.Customers.CreateModel
  @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  
  <p>Validation: customer name:</p>
  
  <form method="post">
      <div asp-validation-summary="ModelOnly"></div>
      <span asp-validation-for="Customer.Name"></span>
      Name:
      <input asp-for="Customer.Name" />
      <input type="submit" />
  </form>
  
  <script src="~/lib/jquery/dist/jquery.js"></script>
  <script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
  <script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
  ```

  O arquivo de exibição *páginas/Create. cshtml* atualizado com *_ViewImports. cshtml* e o arquivo de layout anterior:

  CSHTMLCopiar

  ```cshtml
  @page
  @model CreateModel
  
  <p>Enter a customer name:</p>
  
  <form method="post">
      Name:
      <input asp-for="Customer.Name" />
      <input type="submit" />
  </form>
  ```

  No código anterior, o *_ViewImports. cshtml* importou os auxiliares de namespace e de marca. O arquivo de layout importou os arquivos JavaScript.

  O [Razor projeto inicial de páginas](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/?view=aspnetcore-6.0&tabs=visual-studio#rpvs17) contém as *páginas/_ValidationScriptsPartial. cshtml*, que conectam a validação do lado do cliente.

  Para obter mais informações sobre exibições parciais, consulte [Exibições parciais no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/partial?view=aspnetcore-6.0).

  

  ## Geração de URL para Páginas

  A página `Create`, exibida anteriormente, usa `RedirectToPage`:

  C#Copiar

  ```csharp
  public class CreateModel : PageModel
  {
      private readonly CustomerDbContext _context;
  
      public CreateModel(CustomerDbContext context)
      {
          _context = context;
      }
  
      public IActionResult OnGet()
      {
          return Page();
      }
  
      [BindProperty]
      public Customer Customer { get; set; }
  
      public async Task<IActionResult> OnPostAsync()
      {
          if (!ModelState.IsValid)
          {
              return Page();
          }
  
          _context.Customers.Add(Customer);
          await _context.SaveChangesAsync();
  
          return RedirectToPage("./Index");
      }
  }
  ```

  O aplicativo tem a estrutura de arquivos/pastas a seguir:

  - */Pages*
    - *Index.cshtml*
    - *Privacy. cshtml*
    - */Customers*
      - *Create.cshtml*
      - *Edit.cshtml*
      - *Index.cshtml*

  As páginas *pages/Customers/Create. cshtml* e *pages/Customers/Edit. cshtml* redirecionam para *pages/Customers/index. cshtml* após o êxito. A cadeia de caracteres `./Index` é um nome de página relativo usado para acessar a página anterior. Ele é usado para gerar URLs para a página *pages/Customers/index. cshtml* . Por exemplo:

  - `Url.Page("./Index", ...)`
  - `<a asp-page="./Index">Customers Index Page</a>`
  - `RedirectToPage("./Index")`

  O nome de página absoluto `/Index` é usado para gerar URLs para a página *pages/index. cshtml* . Por exemplo:

  - `Url.Page("/Index", ...)`
  - `<a asp-page="/Index">Home Index Page</a>`
  - `RedirectToPage("/Index")`

  O nome da página é o caminho para a página da pasta raiz */Pages*, incluindo um `/` à direita (por exemplo, `/Index`). Os exemplos de geração de URL anteriores oferecem opções avançadas e recursos funcionais por meio da codificação de uma URL. A geração de URL usa [roteamento](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/routing?view=aspnetcore-6.0) e pode gerar e codificar parâmetros de acordo com o modo como a rota é definida no caminho de destino.

  A Geração de URL para páginas dá suporte a nomes relativos. A tabela a seguir mostra qual página de índice é selecionada usando `RedirectToPage` parâmetros diferentes em *pages/Customers/Create. cshtml*.

  | RedirectToPage(x)          | ?                       |
  | :------------------------- | :---------------------- |
  | RedirectToPage("/Index")   | *Pages/Index*           |
  | RedirectToPage("./Index"); | *Pages/Customers/Index* |
  | RedirectToPage("../Index") | *Pages/Index*           |
  | RedirectToPage("Index")    | *Pages/Customers/Index* |

  `RedirectToPage("Index")`, `RedirectToPage("./Index")` e `RedirectToPage("../Index")` são *nomes relativos*. O parâmetro `RedirectToPage` é *combinado* com o caminho da página atual para calcular o nome da página de destino.

  Vinculação de nome relativo é útil ao criar sites com uma estrutura complexa. Quando nomes relativos são usados para vincular entre páginas em uma pasta:

  - Renomear uma pasta não interrompe os links relativos.
  - Os links não são desfeitos porque não incluem o nome da pasta.

  Para redirecionar para uma página em uma [área](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/areas?view=aspnetcore-6.0) diferente, especifique essa área:

  C#Copiar

  ```csharp
  RedirectToPage("/Index", new { area = "Services" });
  ```

  Para obter mais informações, consulte [Áreas no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/areas?view=aspnetcore-6.0) e [RazorDirecionamento de páginas e convenções de aplicativo no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/razor-pages-conventions?view=aspnetcore-6.0).

  ## Atributo ViewData

  Os dados podem ser passados para uma página com [ViewDataAttribute](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute) . As propriedades com o `[ViewData]` atributo têm seus valores armazenados e carregados do [ViewDataDictionary](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) .

  No exemplo a seguir, o `AboutModel` aplica o `[ViewData]` atributo à `Title` Propriedade:

  C#Copiar

  ```csharp
  public class AboutModel : PageModel
  {
      [ViewData]
      public string Title { get; } = "About";
  
      public void OnGet()
      {
      }
  }
  ```

  Na página Sobre, acesse a propriedade `Title` como uma propriedade de modelo:

  CSHTMLCopiar

  ```cshtml
  <h1>@Model.Title</h1>
  ```

  No layout, o título é lido a partir do dicionário ViewData:

  CSHTMLCopiar

  ```cshtml
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <title>@ViewData["Title"] - WebApplication</title>
      ...
  ```

  ## TempData

  ASP.NET Core expõe o [TempData](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata#Microsoft_AspNetCore_Mvc_Controller_TempData) . Essa propriedade armazena dados até eles serem lidos. Os métodos [Keep](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.tempdatadictionary.keep) e [Peek](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.tempdatadictionary.peek) podem ser usados para examinar os dados sem exclusão. `TempData` é útil para redirecionamento, quando os dados são necessários para mais do que uma única solicitação.

  Os conjuntos de código a seguir definem o valor de `Message` usando `TempData`:

  C#Copiar

  ```csharp
  public class CreateDotModel : PageModel
  {
      private readonly AppDbContext _db;
  
      public CreateDotModel(AppDbContext db)
      {
          _db = db;
      }
  
      [TempData]
      public string Message { get; set; }
  
      [BindProperty]
      public Customer Customer { get; set; }
  
      public async Task<IActionResult> OnPostAsync()
      {
          if (!ModelState.IsValid)
          {
              return Page();
          }
  
          _db.Customers.Add(Customer);
          await _db.SaveChangesAsync();
          Message = $"Customer {Customer.Name} added";
          return RedirectToPage("./Index");
      }
  }
  ```

  A marcação a seguir no arquivo *Pages/Customers/Index.cshtml* exibe o valor de `Message` usando `TempData`.

  CSHTMLCopiar

  ```cshtml
  <h3>Msg: @Model.Message</h3>
  ```

  O modelo de página *Pages/Customers/Index.cshtml.cs* aplica o atributo `[TempData]` à propriedade `Message`.

  C#Copiar

  ```csharp
  [TempData]
  public string Message { get; set; }
  ```

  Para obter mais informações, consulte [TempData](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/app-state?view=aspnetcore-6.0#tempdata).

  

  ## Vários manipuladores por página

  A página a seguir gera marcação para dois manipuladores usando o auxiliar de marcação `asp-page-handler`:

  CSHTMLCopiar

  ```cshtml
  @page
  @model CreateFATHModel
  
  <html>
  <body>
      <p>
          Enter your name.
      </p>
      <div asp-validation-summary="All"></div>
      <form method="POST">
          <div>Name: <input asp-for="Customer.Name" /></div>
          <input type="submit" asp-page-handler="JoinList" value="Join" />
          <input type="submit" asp-page-handler="JoinListUC" value="JOIN UC" />
      </form>
  </body>
  </html>
  ```

  O formulário no exemplo anterior tem dois botões de envio, cada um usando o `FormActionTagHelper` para enviar para uma URL diferente. O atributo `asp-page-handler` é um complemento para `asp-page`. `asp-page-handler` gera URLs que enviam para cada um dos métodos de manipulador definidos por uma página. `asp-page` não foi especificado porque a amostra está vinculando à página atual.

  O modelo de página:

  C#Copiar

  ```csharp
  using System.Threading.Tasks;
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Mvc.RazorPages;
  using RazorPagesContacts.Data;
  
  namespace RazorPagesContacts.Pages.Customers
  {
      public class CreateFATHModel : PageModel
      {
          private readonly AppDbContext _db;
  
          public CreateFATHModel(AppDbContext db)
          {
              _db = db;
          }
  
          [BindProperty]
          public Customer Customer { get; set; }
  
          public async Task<IActionResult> OnPostJoinListAsync()
          {
              if (!ModelState.IsValid)
              {
                  return Page();
              }
  
              _db.Customers.Add(Customer);
              await _db.SaveChangesAsync();
              return RedirectToPage("/Index");
          }
  
          public async Task<IActionResult> OnPostJoinListUCAsync()
          {
              if (!ModelState.IsValid)
              {
                  return Page();
              }
              Customer.Name = Customer.Name?.ToUpperInvariant();
              return await OnPostJoinListAsync();
          }
      }
  }
  ```

  O código anterior usa *métodos de manipulador nomeados*. Métodos de manipulador nomeados são criados colocando o texto no nome após `On<HTTP Verb>` e antes de `Async` (se houver). No exemplo anterior, os métodos de página são OnPost **JoinList** Async e OnPost **JoinListUC** Async. Com *OnPost* e *Async* removidos, os nomes de manipulador são `JoinList` e `JoinListUC`.

  CSHTMLCopiar

  ```cshtml
  <input type="submit" asp-page-handler="JoinList" value="Join" />
  <input type="submit" asp-page-handler="JoinListUC" value="JOIN UC" />
  ```

  Usando o código anterior, o caminho da URL que envia a `OnPostJoinListAsync` é `https://localhost:5001/Customers/CreateFATH?handler=JoinList`. O caminho da URL que envia a `OnPostJoinListUCAsync` é `https://localhost:5001/Customers/CreateFATH?handler=JoinListUC`.

  ## Rotas personalizadas

  Use a diretiva `@page` para:

  - Especifique uma rota personalizada para uma página. Por exemplo, a rota para a página Sobre pode ser definida como `/Some/Other/Path` com `@page "/Some/Other/Path"`.
  - Acrescente segmentos à rota padrão de uma página. Por exemplo, um segmento de "item" pode ser adicionado à rota padrão da página com `@page "item"`.
  - Acrescente parâmetros à rota padrão de uma página. Por exemplo, um parâmetro de ID, `id`, pode ser necessário para uma página com `@page "{id}"`.

  Há suporte para um caminho relativo à raiz designado por um til (`~`) no início do caminho. Por exemplo, `@page "~/Some/Other/Path"` é o mesmo que `@page "/Some/Other/Path"`.

  Se você não gostar da cadeia de caracteres de consulta `?handler=JoinList` na URL, altere a rota para colocar o nome do manipulador na parte do caminho da URL. A rota pode ser personalizada adicionando um modelo de rota entre aspas duplas após a `@page` diretiva.

  CSHTMLCopiar

  ```cshtml
  @page "{handler?}"
  @model CreateRouteModel
  
  <html>
  <body>
      <p>
          Enter your name.
      </p>
      <div asp-validation-summary="All"></div>
      <form method="POST">
          <div>Name: <input asp-for="Customer.Name" /></div>
          <input type="submit" asp-page-handler="JoinList" value="Join" />
          <input type="submit" asp-page-handler="JoinListUC" value="JOIN UC" />
      </form>
  </body>
  </html>
  ```

  Usando o código anterior, o caminho da URL que envia a `OnPostJoinListAsync` é `https://localhost:5001/Customers/CreateFATH/JoinList`. O caminho da URL que envia a `OnPostJoinListUCAsync` é `https://localhost:5001/Customers/CreateFATH/JoinListUC`.

  O `?` após `handler` significa que o parâmetro de rota é opcional.

  ## Configuração e configurações avançadas

  A configuração e as configurações nas seções a seguir não são exigidas pela maioria dos aplicativos.

  Para configurar opções avançadas, use a [AddRazorPages](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addrazorpages) sobrecarga que configura [RazorPagesOptions](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions) :

  C#Copiar

  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {            
      services.AddRazorPages(options =>
      {
          options.RootDirectory = "/MyPages";
          options.Conventions.AuthorizeFolder("/MyPages/Admin");
      });
  }
  ```

  Use o [RazorPagesOptions](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions) para definir o diretório raiz para páginas ou adicione convenções de modelo de aplicativo para páginas. Para obter mais informações sobre convenções, consulte [Razor páginas convenções de autorização](https://docs.microsoft.com/pt-br/aspnet/core/security/authorization/razor-pages-authorization?view=aspnetcore-6.0).

  Para pré-compilar exibições, consulte [Razor Exibir compilação](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/view-compilation?view=aspnetcore-6.0).

  ### Especificar que Razor as páginas estão na raiz do conteúdo

  Por padrão, Razor as páginas têm raiz no diretório */pages* Adicionar [WithRazorPagesAtContentRoot](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) para especificar que suas Razor páginas estão na [raiz do conteúdo](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/?view=aspnetcore-6.0#content-root) ( [ContentRootPath](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath#Microsoft_AspNetCore_Hosting_IHostingEnvironment_ContentRootPath) ) do aplicativo:

  C#Copiar

  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {            
      services.AddRazorPages(options =>
          {
              options.Conventions.AuthorizeFolder("/MyPages/Admin");
          })
          .WithRazorPagesAtContentRoot();
  }
  ```

  ### Especificar que as Razor páginas estejam em um diretório raiz personalizado

  Adicionar [WithRazorPagesRoot](https://docs.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) para especificar que as Razor páginas estão em um diretório raiz personalizado no aplicativo (forneça um caminho relativo):

  C#Copiar

  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {            
      services.AddRazorPages(options =>
          {
              options.Conventions.AuthorizeFolder("/MyPages/Admin");
          })
          .WithRazorPagesRoot("/path/to/razor/pages");
  }
  ```

  ## Recursos adicionais

  - Consulte Introdução [às Razor páginas](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0), que se baseia nesta introdução.
  - [Autorizar atributo e Razor páginas](https://docs.microsoft.com/pt-br/aspnet/core/security/authorization/simple?view=aspnetcore-6.0#aarp)
  - [Baixar ou exibir código de exemplo](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/razor-pages/index/3.0sample)
  - [Introdução ao ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-6.0)
  - [Razorreferência de sintaxe para ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/razor?view=aspnetcore-6.0)
  - [Áreas no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/areas?view=aspnetcore-6.0)
  - [Tutorial: Introdução às Razor páginas no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0)
  - [RazorPáginas convenções de autorização no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/security/authorization/razor-pages-authorization?view=aspnetcore-6.0)
  - [RazorDirecionamento de páginas e convenções de aplicativo no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/razor-pages-conventions?view=aspnetcore-6.0)
  - [RazorPáginas testes de unidade no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/test/razor-pages-tests?view=aspnetcore-6.0)
  - [Exibições parciais no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/partial?view=aspnetcore-6.0)
  - [Pré-gerar e integrar ASP.NET Core Razor componentes](https://docs.microsoft.com/pt-br/aspnet/core/blazor/components/prerendering-and-integration?view=aspnetcore-6.0)

- [ore](https://docs.microsoft.com/pt-br/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-6.0)

- [Razorreferência de sintaxe para ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/razor?view=aspnetcore-6.0)

- [Áreas no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/controllers/areas?view=aspnetcore-6.0)

- [Tutorial: Introdução às Razor páginas no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-6.0)

- [RazorPáginas convenções de autorização no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/security/authorization/razor-pages-authorization?view=aspnetcore-6.0)

- [RazorDirecionamento de páginas e convenções de aplicativo no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/razor-pages/razor-pages-conventions?view=aspnetcore-6.0)

- [RazorPáginas testes de unidade no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/test/razor-pages-tests?view=aspnetcore-6.0)

- [Exibições parciais no ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/mvc/views/partial?view=aspnetcore-6.0)

- [Pré-gerar e integrar ASP.NET Core Razor componentes](https://docs.microsoft.com/pt-br/aspnet/core/blazor/components/prerendering-and-integration?view=aspnetcore-6.0)