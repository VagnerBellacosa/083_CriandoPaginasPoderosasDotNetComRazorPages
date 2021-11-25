# Apresentando Razor Pages - III

------

|      |      |
| ---- | ---- |
|      |      |

Continuando a **[segunda do artigo](http://www.macoratti.net/18/02/aspcore_rzpg2.htm)** vamos implementar a edição das informações do cliente no projeto Razor Pages.

A view **Index** representando pelo arquivo **Index.cshtml** usa a tag-helper **asp-page** para definir um link para a view **Edit** passando como parâmetro o **Id** do cliente:

```
 ``   <a asp-page="./Edit" asp-route-id="@contact.Id">Editar</a>
```


Vamos implementar essa funcionalidade.

**Recursos usados:**

- [Visual Studio 2017 Community](https://www.visualstudio.com/pt-br/downloads/)

Editando informações de Clientes : incluind a razor Page Edit.cshtml

Abra o projeto **AspnRazorPage1** criado na primeira parte do artigo e inclua uma pasta **Models** no projeto. **(Project-> New Folder)**

Vamos agora incluir uma página chamada **Edit.chstml** na pasta **Pages**.

Clique com o botão direito do mouse sobre a pasta **Pages** a seguir clique em **Add -> Razor Page**

![img](http://www.macoratti.net/18/02/aspcore_rzpg14.png)

A seguir na janela **Add Scaffold** clique em **Razor Page** e a seguir no botão **Add**;

![img](http://www.macoratti.net/18/02/aspcore_rzpg15.png)

Na janela **Add Razor Page** informe o nome **Edit** e marque as opções conforme a figura a seguir:

![img](http://www.macoratti.net/18/02/aspcore_rzpg31.png)

Clicando no botão **Add** teremos a view **Edit.cshtml** e seu arquivo code-behind criados na pasta **Pages**.

Vamos iniciar definindo o código do arquivo code-behind **Edit.cshtml.cs** :

```
using AspnRazorPage1.Models; using Microsoft.AspNetCore.Mvc; using Microsoft.AspNetCore.Mvc.RazorPages; using Microsoft.EntityFrameworkCore; using System; using System.Threading.Tasks;``namespace AspnRazorPage1.Pages {    public class **EditModel** : PageModel    {        private readonly AppDbContext _db;``        public EditModel(AppDbContext db)        {            _db = db;        }``        [BindProperty]        public Cliente **Cliente** { get; set; }``        public async Task<IActionResult> **OnGetAsync**(int id)        {            Cliente = await _db.Clientes.FindAsync(id);``            if (Cliente == null)            {                return RedirectToPage("/Index");            }``            return Page();        }``        public async Task<IActionResult> **OnPostAsync**()        {            if (!ModelState.IsValid)            {                return Page();            }``            _db.Attach(Cliente).State = EntityState.Modified;``            try            {                await _db.SaveChangesAsync();            }            catch (DbUpdateConcurrencyException)            {                throw new Exception($"Cliente {Cliente.Id} não encontrado !");            }``            return RedirectToPage("/Index");        }    } }
```

O código é muito parecido com o da página **Create**.

No método **OnPostAsync**: temos a verificação para validação de erros com as seguintes ações:

1 - Se não houver erros, salva os dados e faz o redirecionamento
2 - Se houver erros, exibe a página novamente com as mensagens de validação. *(A validação do lado do cliente é idêntica às feitas nas aplicações ASP.NET Core MVC. Em muitos casos, erros de validação seriam detectados no cliente.)*

Quando os dados são inseridos com sucesso, o método do manipulador **OnPostAsync** chama o método helper **redirectToPage** para retornar uma instância de **RedirectToPageResult**.

Agora abra o arquivo **Edit.cshtml** e inclua o código abaixo:

```
**@page "{id:int}" @model AspnRazorPage1.Pages.EditModel** @{    ViewData["Title"] = "Editar Cliente"; } <h1>Editar Cliente - @Model.Cliente.Id</h1> <form method="post">    <div asp-validation-summary="All"></div>    <input asp-for="Cliente.Id" type="hidden" />    <div>        <label asp-for="Cliente.Nome"></label>        <div>            <input asp-for="Cliente.Nome" />            <span asp-validation-for="Cliente.Nome"></span>        </div>    </div>    <div>        <button type="submit">Salvar</button>    </div> </form>
```

A primeira linha de código da página contém a diretiva : **@page "{id:int}"**

Esta restrição de roteamento informa para a página aceitar requisições que contém os dados **id** do tipo int. Se uma requisição para a página não contiver dos dados que podem ser convertidos para um int , será retornado o erro **HTTP 404 (not found).**

Lembrando que a página **Index.cshtml** possui o código abaixo que define um **Button** e uma tag-helper **asp-page-handler** que define o método delete passando o id do cliente.

 <button type="submit" asp-page-handler="delete" asp-route-id="@contato.Id">Deletar</button>

Como o handler é do tipo delete o método **OnPostDeleteAsync** foi definido no arquivo code-behind **Index.cshtml** para realizar a exclusão do cliente:
 

```
       public async Task<IActionResult> **OnPostDeleteAsync**(int id)        {            var contact = await _**db.Clientes.FindAsync(id);**``            if (contact != null)            {                _db.Clientes.Remove(contact);                await _db.SaveChangesAsync();            }            return RedirectToPage();        }
```



Agora nossa aplicação Razor Pages possui implementa a inclusão , alteração e exclusão dos dados do cliente conforme planejamos.

Executando o nosso projeto neste momento teremos o seguinte resultado:

**1- Exibição da view Index.cshtml**

![img](http://www.macoratti.net/18/02/aspcore_rzpg17.png)

**2- Exibição da view Create.cshtml após clicar no link - Criar Contato**

![img](http://www.macoratti.net/18/02/aspcore_rzpg18.png)

**3- Exibição da view Index.cshtm após incluir um novo contato**

![img](http://www.macoratti.net/18/02/aspcore_rzpg19.png)

**4- Realizando a alteração dos dados do cliente após clicar no link Editar**

![img](http://www.macoratti.net/18/02/aspcore_rzpg32.png)

Para excluir um cliente basta cliar no link **Deletar**.

Concluimos assim nossa aplicação usando os recursos das Razor Pages. Lembrando que os dados são tratados apenas em memória. Para persistir altere o provedor in-memory do EF Core no arquivo Startup.

Pegue o projeto completo aqui : ![img](http://www.macoratti.net/downl.gif) **[AspnRazorPage1.zip](http://www.macoratti.net/18/02/AspnRazorPage1)**