# Introdução ao Páginas da Web do ASP.NET-Criando um layout consistente

- 13/05/2021
- - [![img](https://github.com/Rick-Anderson.png?size=32)](https://github.com/Rick-Anderson)
  - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)

Esta página é útil?

por [Tom FitzMacken](https://github.com/tfitzmac)

> Este tutorial mostra como usar *layouts* para criar uma aparência consistente para as páginas em um site que usa páginas da Web do ASP.net. Ele pressupõe que você concluiu a série por meio da [exclusão de dados de banco de dado no páginas da Web do ASP.net](https://go.microsoft.com/fwlink/?LinkId=251584).
>
> O que você aprenderá:
>
> - O que é uma página de layout.
> - Como combinar páginas de layout com conteúdo dinâmico.
> - Como passar valores para uma página de layout.

## Sobre layouts

As páginas que você criou até agora foram todas concluídas, páginas autônomas. Todos eles pertencem ao mesmo site, mas não têm nenhum elemento comum ou uma aparência padrão.

A maioria dos sites tem uma aparência e um layout consistentes. Por exemplo, se você for para o site do [Microsoft.com/Web](https://www.microsoft.com/web/) e observar, verá que as páginas são todas seguidas em um layout geral e em um tema Visual:

![Página do site do Microsoft.com/web mostrando o layout do cabeçalho, da área de navegação, da área de conteúdo e do rodapé](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image1.png)

Uma maneira *ineficiente* de criar esse layout seria definir um cabeçalho, uma barra de navegação e um rodapé separadamente em cada uma de suas páginas. Você estaria duplicando a mesma marcação a cada vez. Se você quisesse alterar algo (por exemplo, atualizar o rodapé), precisaria alterar cada página separadamente.

É aí que entram as *páginas de layout* . No Páginas da Web do ASP.NET, você pode definir uma página de layout que fornece um contêiner geral para páginas em seu site. Por exemplo, a página de layout pode conter o cabeçalho, a área de navegação e o rodapé. A página de layout inclui um espaço reservado onde o conteúdo principal vai.

Em seguida, você pode definir páginas de conteúdo individuais que contêm a marcação e o código somente para essa página. As páginas de conteúdo não precisam ser páginas HTML completas; Eles nem precisam ter um elemento `<body>`. Eles também têm uma linha de código que diz ao ASP.NET em qual página de layout você deseja exibir o conteúdo. Aqui está uma imagem que mostra aproximadamente como essa relação funciona:

![Diagrama conceitual que mostra duas páginas de conteúdo e uma página de layout na qual elas se ajustam](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image2.png)

Essa interação é fácil de entender quando você a vê em ação. Neste tutorial, você alterará suas páginas de filmes para usar um layout.

## Adicionando uma página de layout

Você começará criando uma página de layout que define um layout de página típico com um cabeçalho, um rodapé e uma área para o conteúdo principal. No site do WebPagesMovies, adicione uma página CSHTML denominada *_layout. cshtml*.

O caractere de sublinhado à esquerda (`_`) é significativo. Se o nome de uma página começar com um sublinhado, ASP.NET não enviará diretamente essa página para o navegador. Essa Convenção permite definir páginas que são necessárias para seu site, mas que os usuários não devem ser capazes de solicitar diretamente.

Substitua o conteúdo da página pelo seguinte:

HTMLCopiar

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Movie Site</title>
    <link href="~/Styles/Movies.css" rel="stylesheet" type="text/css" />
  </head>
  <body>
    <div id="container">
        <div id="header">
          <h1>My Movie Site</h1>
        </div>
        <div id="main">
          @RenderBody()
        </div>
        <div id="footer">
          &copy; @DateTime.Now.Year My Movie Site
        </div>
    </div>
  </body>
</html>
```

Como você pode ver, essa marcação é apenas HTML que usa elementos `<div>` para definir três seções na página mais um elemento mais `<div>` para manter as três seções. O rodapé contém um pouco de código do Razor: `@DateTime.Now.Year`, que renderizará o ano atual nesse local na página.

Observe que há um link para uma folha de estilos chamada *Movies. css*. A folha de estilos é onde os detalhes do layout físico dos elementos serão definidos. Você criará isso daqui a pouco.

O único recurso incomum neste *_página layout. cshtml* é a linha de `@Render.Body()`. Esse é o espaço reservado onde o conteúdo será usado quando esse layout for mesclado com outra página.

## Adicionando um arquivo. css

A maneira preferida de definir a organização real (ou seja, aparência) dos elementos na página é usar as regras de CSS (folha de estilos em cascata). Portanto, você criará um arquivo *. css* que tem as regras para o novo layout.

No WebMatrix, selecione a raiz do seu site. Na guia **arquivos** da faixa de faixas, clique na seta sob o botão **novo** e clique em **nova pasta**.

![A opção ' nova pasta ' em novo na faixa de opções.](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image3.png)

Nomeie os novos *estilos*de pasta.

![Nomeando a nova pasta ' Styles '](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image4.png)

Dentro da nova pasta *estilos* , crie um arquivo chamado *Movies. css*.

![Criando um novo arquivo Movies. css](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image5.png)

Substitua o conteúdo do novo arquivo *. css* pelo seguinte:

cssCopiar

```css
html{ height:100%; margin:0; padding:0; }

body {
  height:60%;
  font-family:'Trebuchet MS',  'Arial', 'Helvetica', 'sans-serif';
  font-size:10pt;
  background-color: LightGray;
  line-height:1.6em;
}

h1{ font-size:1.6em; }
h2{ font-size:1.4em; }

#container{
   min-height:100%;
   position:relative;
   left:10%;
}

#header{
  padding:8px;
  width:80%;
  background-color:#4b6c9e;
  color:White;
}

#main{
  width:80%;
  padding: 8px;
  padding-bottom:4em;
  background-color:White;
}

#footer{
  width:80%;
  height:2em;
  padding:8px;
  margin-top:-2em;
  background-color:LightGray;
}

.head { background-color: #E8E8E8; font-weight: bold; color: #FFF; }
.grid th, .grid td { border: 1px solid #C0C0C0; padding: 5px; }
.alt { background-color: #E8E8E8; color: #000; }
.selected {background-color:Yellow;}
span.caption {width:100px;}
span.dataDisplay {font-weight:bold;}
```

Não vamos dizer muito sobre essas regras de CSS, exceto para observar duas coisas. Uma delas é que, além de definir fontes e tamanhos, as regras usam o posicionamento absoluto para estabelecer o local do cabeçalho, do rodapé e da área de conteúdo principal. Se você for novo no posicionamento em CSS, poderá ler o tutorial de [posicionamento de CSS](http://www.w3schools.com/css/css_positioning.asp) no site do w3schools.

Outra coisa a ser observada é que, na parte inferior, copiamos as regras de estilo que foram originalmente definidas individualmente no arquivo *Movies. cshtml* . Essas regras foram usadas na [introdução à exibição de dados usando páginas da Web do ASP.net](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial para fazer com que o auxiliar de `WebGrid` processe a marcação que adicionou as faixas à tabela. (Se você for usar um arquivo *. css* para definições de estilo, você também poderá colocar as regras de estilo para todo o site nele.)

## Atualizando o arquivo de filmes para usar o layout

Agora você pode atualizar os arquivos existentes no seu site para usar o novo layout. Abra o arquivo *Movies. cshtml* . Na parte superior, como a primeira linha de código, adicione o seguinte:

C#Copiar

```csharp
Layout = "~/_Layout.cshtml";
```

A página agora começa desta forma:

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";

    var db = Database.Open("WebPagesMovies") ;
    var selectCommand = "SELECT * FROM Movies";
    var searchTerm = "";

    // Etc.
```

Essa linha de código informa ao ASP.NET que, quando a página de *filmes* é executada, ela deve ser mesclada com o arquivo *layout. cshtml de_* .

Como o arquivo *Movies. cshtml* agora usa uma página de layout, você pode remover a marcação da página *Movies. cshtml* que é manipulada pelo arquivo *layout. cshtml de_* . Retire as marcas `<!DOCTYPE>`, `<html>`e `<body>` de abertura e fechamento. Retire todo o elemento `<head>` e seu conteúdo, que inclui as regras de estilo para a grade, já que você tem essas regras em um arquivo *. css* . Enquanto estiver, altere o elemento `<h1>` existente para um elemento `<h2>`; Você já tem um elemento `<h1>` na página de layout. Altere o texto do `<h2>` para "listar filmes".

Normalmente, você não precisaria fazer esses tipos de alterações em uma página de conteúdo. Ao iniciar o site com uma página de layout, você cria páginas de conteúdo sem todos esses elementos para começar. Nesse caso, no entanto, você está convertendo uma página autônoma para uma que usa um layout, portanto, há um pouco de limpeza.

Quando tiver terminado, a página *Movies. cshtml* será parecida com a seguinte:

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";

    var db = Database.Open("WebPagesMovies") ;
    var selectCommand = "SELECT * FROM Movies";
    var searchTerm = "";

    if(!Request.QueryString["searchGenre"].IsEmpty() ) {
        selectCommand = "SELECT * FROM Movies WHERE Genre = @0";
        searchTerm = Request.QueryString["searchGenre"];
    }

    if(!Request.QueryString["searchTitle"].IsEmpty() ) {
      selectCommand = "SELECT * FROM Movies WHERE Title LIKE @0";
      searchTerm = "%" + Request.QueryString["searchTitle"] + "%";
    }

    var selectedData = db.Query(selectCommand, searchTerm);
    var grid = new WebGrid(source: selectedData, defaultSort: "Genre", rowsPerPage:3);
}
  <h2>List Movies</h2>
  <form method="get">
    <div>
      <label for="searchGenre">Genre to look for:</label>
      <input type="text" name="searchGenre"
         value="@Request.QueryString["searchGenre"]" />
      <input type="Submit" value="Search Genre" /><br/>
      (Leave blank to list all movies.)<br/>
    </div>
    <div>
       <label for="SearchTitle">Movie title contains the following:</label>
       <input type="text" name="searchTitle" value="@Request.QueryString["searchTitle"]" />
       <input type="Submit" value="Search Title" /><br/>
    </div>
  </form>
  <div>
    @grid.GetHtml(
        tableStyle: "grid",
        headerStyle: "head",
        alternatingRowStyle: "alt",
        columns: grid.Columns(
            grid.Column(format: @<a href="~/EditMovie?id=@item.ID">Edit</a>),
            grid.Column("Title"),
            grid.Column("Genre"),
            grid.Column("Year"),
            grid.Column(format: @<a href="~/DeleteMovie?id=@item.ID">Delete</a>)
       )
    )
  </div>
  <p><a href="~/AddMovie">Add a movie</a></p>
```

### Testando o layout

Agora você pode ver qual é a aparência do layout. No WebMatrix, clique com o botão direito do mouse na página *Movies. cshtml* e selecione **Iniciar no navegador**. Quando o navegador exibe a página, ele é semelhante a esta página:

![Página de filmes renderizada usando um layout](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image6.png)

ASP.NET mesclou o conteúdo da página Movies. cshtml na página *_layout. cshtml* , onde o método `RenderBody` é. E, claro, a página *_layout. cshtml* faz referência a um arquivo *. css* que define a aparência da página.

## Atualizando a página addmovie para usar o layout

O verdadeiro benefício dos layouts é que você pode usá-los para todas as páginas do seu site. Abra a página *addmovie. cshtml* .

Você pode se lembrar de que a página *addmovie. cshtml* tinha originalmente algumas regras de CSS nela para definir a aparência das mensagens de erro de validação. Como você tem um arquivo *. css* para seu site agora, você pode mover essas regras para o arquivo *. css* . Remova-os do arquivo *addmovie. cshtml* e adicione-os à parte inferior do arquivo *Movies. css* . Você está movendo as seguintes regras:

cssCopiar

```css
.field-validation-error {
  font-weight:bold;
  color:red;
  background-color:yellow;
 }
.validation-summary-errors{
  border:2px dashed red;
  color:red;
  background-color:yellow;
  font-weight:bold;
  margin:12px;
}
```

Agora faça os mesmos tipos de alterações em *addmovie. cshtml* que você fez para *Movies. cshtml* — adicione `Layout="~/_Layout.cshtml;` e remova a marcação HTML que agora é estranha. Altere o elemento `<h1>` para `<h2>`. Quando terminar, a página se parecerá com este exemplo:

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";
    Validation.RequireField("title", "You must enter a title");
    Validation.RequireField("genre", "Genre is required");
    Validation.RequireField("year", "You haven't entered a year");

    var title = "";
    var genre = "";
    var year = "";

    if(IsPost){
        if(Validation.IsValid()){
            title = Request.Form["title"];
            genre = Request.Form["genre"];
            year = Request.Form["year"];

            var db = Database.Open("WebPagesMovies");
            var insertCommand =
                "INSERT INTO Movies (Title, Genre, Year) Values(@0, @1, @2)";
            db.Execute(insertCommand, title, genre, year);
            Response.Redirect("~/Movies");
        }
    }
}
  <h2>Add a Movie</h2>
    @Html.ValidationSummary()
 <form method="post">
  <fieldset>
    <legend>Movie Information</legend>
    <p><label for="title">Title:</label>
      <input type="text" name="title" value="@Request.Form["title"]" />
      @Html.ValidationMessage("title")
    </p>

    <p><label for="genre">Genre:</label>
      <input type="text" name="genre" value="@Request.Form["genre"]" />
      @Html.ValidationMessage("genre")
    </p>

    <p><label for="year">Year:</label>
      <input type="text" name="year" value="@Request.Form["year"]" />
      @Html.ValidationMessage("year")
    </p>

    <p><input type="submit" name="buttonSubmit" value="Add Movie" /></p>
  </fieldset>
  </form>
```

Execute a página. Agora, ele é semelhante a esta ilustração:

![Página ' Adicionar filmes ' processada usando um layout](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image7.png)

Você deseja fazer alterações semelhantes às páginas no site — *EditMovie. cshtml* e *DeleteMovie. cshtml*. No entanto, antes de fazer isso, você pode fazer outra alteração no layout que o torna um pouco mais flexível.

## Passando informações de título para a página de layout

A página *_layout. cshtml* que você criou tem um elemento `<title>` definido como "meu site de filmes". A maioria dos navegadores exibe o conteúdo deste elemento como o texto em uma guia:

![O título da <da página> elemento exibido em uma guia do navegador](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image8.png)

Essa informação de título é genérica. Suponha que você deseja que o texto do título seja mais específico para a página atual. (O texto do título também é usado pelos mecanismos de pesquisa para determinar a sua página.) Você pode passar informações de uma página de conteúdo como *Movies. cshtml* ou *addmovie. cshtml* para a página de layout e, em seguida, usar essas informações para personalizar o que a página de layout renderiza.

Abra a página *Movies. cshtml* novamente. No código na parte superior, adicione a seguinte linha:

C#Copiar

```csharp
Page.Title = "List Movies";
```

O objeto `Page` está disponível em todas as páginas *. cshtml* e é para essa finalidade, ou seja, para compartilhar informações entre uma página e seu layout.

Abra a página *_layout. cshtml* . Altere o elemento `<title>` de forma que ele se pareça com esta marcação:

HTMLCopiar

```html
<title>@Page.Title</title>
```

Esse código renderiza o que estiver na propriedade `Page.Title` diretamente nesse local na página.

Execute a página *Movies. cshtml* . Desta vez, a guia Navegador mostra o que você passou como o valor de `Page.Title`:

![Uma guia do navegador mostrando o título criado dinamicamente](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image9.png)

Se desejar, exiba a origem da página no navegador. Você pode ver que o elemento `<title>` é renderizado como `<title>List Movies</title>`.

 Dica

**O objeto Page**

Um recurso útil do `Page` é que ele é um objeto dinâmico — a propriedade `Title` não é um nome fixo ou reservado. Você pode usar *qualquer* nome para um valor do objeto `Page`. Por exemplo, você poderia facilmente passar o título usando uma propriedade chamada `Page.CurrentName` ou `Page.MyPage`. A única restrição é que o nome precisa seguir as regras normais para quais propriedades podem ser nomeadas. (Por exemplo, o nome não pode conter um espaço).

Você pode passar qualquer número de valores usando o objeto `Page`. Se você quisesse passar informações de filme para a página de layout, poderá passar valores usando algo como `Page.MovieTitle` e `Page.Genre` e `Page.MovieYear`. (Ou quaisquer outros nomes que você inventou para armazenar as informações.) O único requisito, que provavelmente é óbvio, é que você precisa usar os mesmos nomes na página de conteúdo e na página de layout.

As informações que você passa usando o objeto `Page` não estão limitadas a apenas texto a ser exibido na página de layout. Você pode passar um valor para a página de layout e, em seguida, o código na página de layout pode usar o valor para decidir se deve exibir uma seção da página, o arquivo *. css* a ser usado e assim por diante. Os valores que você passa no objeto `Page` são como quaisquer outros valores que você usa no código. É apenas que os valores se originam na página de conteúdo e são passados para a página de layout.

Abra a página *addmovie. cshtml* e adicione uma linha à parte superior do código que fornece um título para a página *addmovie. cshtml* :

C#Copiar

```csharp
Page.Title = "Add a Movie";
```

Execute a página *addmovie. cshtml* . Você verá o novo título lá:

![Uma guia do navegador mostrando o título ' Adicionar filmes ' criado dinamicamente](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image10.png)

## Atualizando as páginas restantes para usar o layout

Agora você pode concluir as páginas restantes no seu site para que elas usem o novo layout. Abra *EditMovie. cshtml* e *DeleteMovie. cshtml* por vez e faça as mesmas alterações em cada um.

Adicione a linha de código que vincula à página de layout:

C#Copiar

```csharp
Layout = "~/_Layout.cshtml";
```

Adicione uma linha para definir o título da página:

C#Copiar

```csharp
Page.Title = "Edit a Movie";
```

ou:

C#Copiar

```csharp
Page.Title = "Delete a Movie";
```

Remover toda a marcação HTML incorreta — basicamente, deixe apenas os bits que estão dentro do elemento `<body>` (mais o bloco de código na parte superior).

Altere o elemento `<h1>` para que seja um elemento `<h2>`.

Quando você fez essas alterações, teste cada uma e verifique se ela está sendo exibida corretamente e se o título está correto.

## Ideias de partes sobre páginas de layout

Neste tutorial, você criou uma página *_layout. cshtml* e usou o método `RenderBody` para Mesclar conteúdo de outra página. Esse é o padrão básico para usar layouts em páginas da Web.

As páginas de layout têm recursos adicionais que não abordamos aqui. Por exemplo, você pode aninhar páginas de layout — uma página de layout pode, por sua vez, fazer referência a outra. Layouts aninhados podem ser úteis se você estiver trabalhando com subseções de um site que exigem layouts diferentes. Você também pode usar métodos adicionais (por exemplo, `RenderSection`) para configurar seções nomeadas na página layout.

A combinação de páginas de layout e arquivos *. css* é eficiente. Como você verá na próxima série de tutoriais, no WebMatrix, você pode criar um site com base em um *modelo*, que fornece um site com funcionalidade predefinida. Os modelos fazem uso bom das páginas de layout e do CSS para criar sites que têm uma aparência ótima e que têm recursos como menus. Aqui está uma captura de tela da home page de um site com base em um modelo, mostrando recursos que usam páginas de layout e CSS:

![Layout criado pelo modelo de site do WebMatrix mostrando o cabeçalho, área de navegação, área de conteúdo, seção opcional e links de logon](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts/_static/image11.png)

## Listagem completa da página de filme (atualizada para usar uma página de layout)

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";
    Page.Title = "List Movies";

    var db = Database.Open("WebPagesMovies") ;
    var selectCommand = "SELECT * FROM Movies";
    var searchTerm = "";

    if(!Request.QueryString["searchGenre"].IsEmpty() ) {
        selectCommand = "SELECT * FROM Movies WHERE Genre = @0";
        searchTerm = Request.QueryString["searchGenre"];
    }

    if(!Request.QueryString["searchTitle"].IsEmpty() ) {
        selectCommand = "SELECT * FROM Movies WHERE Title LIKE @0";
        searchTerm = "%" + Request.QueryString["searchTitle"] + "%";
    }

    var selectedData = db.Query(selectCommand, searchTerm);
    var grid = new WebGrid(source: selectedData, defaultSort: "Genre", rowsPerPage:3);
}

<h2>List Movies</h2>
    <form method="get">
      <div>
        <label for="searchGenre">Genre to look for:</label>
        <input type="text" name="searchGenre" value="@Request.QueryString["searchGenre"]" />
        <input type="Submit" value="Search Genre" /><br/>
        (Leave blank to list all movies.)<br/>
      </div>

      <div>
        <label for="SearchTitle">Movie title contains the following:</label>
        <input type="text" name="searchTitle" value="@Request.QueryString["searchTitle"]" />
        <input type="Submit" value="Search Title" /><br/>
      </div>
    </form>

<div>
    @grid.GetHtml(
        tableStyle: "grid",
        headerStyle: "head",
        alternatingRowStyle: "alt",
        columns: grid.Columns(
    grid.Column(format: @<a href="~/EditMovie?id=@item.ID">Edit</a>),
    grid.Column("Title"),
    grid.Column("Genre"),
    grid.Column("Year"),
    grid.Column(format: @<a href="~/DeleteMovie?id=@item.ID">Delete</a>)
        )
    )
</div>
<p><a href="~/AddMovie">Add a movie</a></p>
```

## Lista completa de páginas para adicionar filme (atualizado para layout)

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";
    Page.Title = "Add a Movie";

    Validation.RequireField("title", "You must enter a title");
    Validation.RequireField("genre", "Genre is required");
    Validation.RequireField("year", "You haven't entered a year");

    var title = "";
    var genre = "";
    var year = "";

    if(IsPost){
        if(Validation.IsValid()){
            title = Request.Form["title"];
            genre = Request.Form["genre"];
            year = Request.Form["year"];

            var db = Database.Open("WebPagesMovies");
            var insertCommand = "INSERT INTO Movies (Title, Genre, Year) VALUES(@0, @1, @2)";
            db.Execute(insertCommand, title, genre, year);

            Response.Redirect("~/Movies");
        }
    }
}

<h2>Add a Movie</h2>
@Html.ValidationSummary()
<form method="post">
<fieldset>
    <legend>Movie Information</legend>
    <p><label for="title">Title:</label>
        <input type="text" name="title" value="@Request.Form["title"]" />
        @Html.ValidationMessage("title")

    <p><label for="genre">Genre:</label>
        <input type="text" name="genre" value="@Request.Form["genre"]" />
        @Html.ValidationMessage("genre")

    <p><label for="year">Year:</label>
        <input type="text" name="year" value="@Request.Form["year"]" />
        @Html.ValidationMessage("year")

    <p><input type="submit" name="buttonSubmit" value="Add Movie" /></p>
</fieldset>
</form>
```

## Concluir a listagem de página para excluir página de filme (atualizada para layout)

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";
    Page.Title = "Delete a Movie";

    var title = "";
    var genre = "";
    var year = "";
    var movieId = "";

    if(!IsPost){
        if(!Request.QueryString["ID"].IsEmpty() && Request.QueryString["ID"].AsInt() > 0){
            movieId = Request.QueryString["ID"];
            var db = Database.Open("WebPagesMovies");
            var dbCommand = "SELECT * FROM Movies WHERE ID = @0";
            var row = db.QuerySingle(dbCommand, movieId);
            if(row != null) {
                title = row.Title;
                genre = row.Genre;
                year = row.Year;
            }
            else{
                Validation.AddFormError("No movie was found for that ID.");
                // If you are using a version of ASP.NET Web Pages 2 that's
                // earlier than the RC release, comment out the preceding
                // statement and uncomment the following one.
                //ModelState.AddFormError("No movie was found for that ID.");
            }
        }
        else{
            Validation.AddFormError("No movie was found for that ID.");
            // If you are using a version of ASP.NET Web Pages 2 that's
            // earlier than the RC release, comment out the preceding
            // statement and uncomment the following one.
            //ModelState.AddFormError("No movie was found for that ID.");
        }
    }

    if(IsPost && !Request["buttonDelete"].IsEmpty()){
        movieId = Request.Form["movieId"];
        var db = Database.Open("WebPagesMovies");
        var deleteCommand = "DELETE FROM Movies WHERE ID = @0";
        db.Execute(deleteCommand, movieId);
        Response.Redirect("~/Movies");
    }

}

<h2>Delete a Movie</h2>
@Html.ValidationSummary()
<p><a href="~/Movies">Return to movie listing</a></p>

<form method="post">
<fieldset>
<legend>Movie Information</legend>

<p><span>Title:</span>
    <span>@title</span></p>

<p><span>Genre:</span>
    <span>@genre</span></p>

<p><span>Year:</span>
    <span>@year</span></p>

<input type="hidden" name="movieid" value="@movieId" />
<p><input type="submit" name="buttonDelete" value="Delete Movie" /></p>
</fieldset>
</form>
```

## Lista completa de páginas para editar filme (atualizado para layout)

CSHTMLCopiar

```cshtml
@{
    Layout = "~/_Layout.cshtml";
    Page.Title = "Edit a Movie";

    var title = "";
    var genre = "";
    var year = "";
    var movieId = "";

    if(!IsPost){
        if(!Request.QueryString["ID"].IsEmpty() && Request.QueryString["ID"].IsInt()) {
            movieId = Request.QueryString["ID"];
            var db = Database.Open("WebPagesMovies");
            var dbCommand = "SELECT * FROM Movies WHERE ID = @0";
            var row = db.QuerySingle(dbCommand, movieId);

            if(row != null) {
                title = row.Title;
                genre = row.Genre;
                year = row.Year;
            }
            else{
                Validation.AddFormError("No movie was selected.");
                // If you are using a version of ASP.NET Web Pages 2 that's
                // earlier than the RC release, comment out the preceding
                // statement and uncomment the following one.
                //ModelState.AddFormError("No movie was selected.");
            }
        }
        else{
            Validation.AddFormError("No movie was selected.");
            // If you are using a version of ASP.NET Web Pages 2 that's
            // earlier than the RC release, comment out the preceding
            // statement and uncomment the following one.
            //ModelState.AddFormError("No movie was selected.");
        }
    }

    if(IsPost){
        Validation.RequireField("title", "You must enter a title");
        Validation.RequireField("genre", "Genre is required");
        Validation.RequireField("year", "You haven't entered a year");
        Validation.RequireField("movieid", "No movie ID was submitted!");

        title = Request.Form["title"];
        genre = Request.Form["genre"];
        year = Request.Form["year"];
        movieId = Request.Form["movieId"];

        if(Validation.IsValid()){
            var db = Database.Open("WebPagesMovies");
            var updateCommand = "UPDATE Movies SET Title=@0, Genre=@1, Year=@2 WHERE Id=@3";
            db.Execute(updateCommand, title, genre, year, movieId);
            Response.Redirect("~/Movies");
        }
    }
}

<h2>Edit a Movie</h2>
@Html.ValidationSummary()
<form method="post">
<fieldset>
    <legend>Movie Information</legend>

    <p><label for="title">Title:</label>
        <input type="text" name="title" value="@title" /></p>

    <p><label for="genre">Genre:</label>
        <input type="text" name="genre" value="@genre" /></p>

    <p><label for="year">Year:</label>
        <input type="text" name="year" value="@year" /></p>

    <input type="hidden" name="movieid" value="@movieId" />

    <p><input type="submit" name="buttonSubmit" value="Submit Changes" /></p>
</fieldset>
</form>
<p><a href="~/Movies">Return to movie listing</a></p>
```

## Chegando em seguida

No próximo tutorial, você aprenderá a publicar seu site na Internet para que todos possam vê-lo.

## Recursos adicionais

- [Criando uma aparência consistente](https://go.microsoft.com/fwlink/?LinkID=202891) — um artigo que fornece mais detalhes sobre como trabalhar com layouts. Ele também descreve como passar um valor para uma página de layout que mostra ou oculta parte do conteúdo.
- [Páginas de layout aninhadas com Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind bloga um exemplo de como aninhar páginas de layout. (Inclui um download das páginas.)

[Anterior](https://docs.microsoft.com/pt-br/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data) 