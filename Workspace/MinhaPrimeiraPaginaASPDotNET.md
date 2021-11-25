**Minha primeira página ASP.NET.**

------

Lembra da **ASP - Active Server Pages** ?? Que tal recordar ?

**O que é ASP ?**

ASP é uma tecnologia de scripts que roda no servidor e permite que os scripts embutidos em uma página HTML sejam executados por um servidor WEB.

- ASP é uma tecnologia da Microsoft
- ASP significa - **A**ctive **S**erver **P**ages
- ASP roda sobre o contexto do - **IIS** - **I**nternet **I**nformation **S**erver
- IIS é um componente que vem com o Windows 2000 , Windows XP e é parte do Windows NT 4.0 Option Pack
- ASP também pode ser executado sob o servidor - **PWS** - **P**erson **W**eb **S**erver ( uma versão reduzida do **IIS**)
- **PWS** pode ser encontrado nos CD´s do Windows **95/98 ,** no site da Microsoft ou no [Super CD ASP Total](http://www.macoratti.net/asptotal.htm)

**O que é um arquivo ASP ?**

- Um arquivo ASP é apenas um arquivo do tipo HTML.
- Um arquivo ASP pode conter texto , HTML, XML, e scripts
- Os scripts de um arquivo ASP são executados no servidor
- Um arquivo ASP tem a extensão ".asp"

**Como ASP Funciona ?**

- Quando um Navegador (Internet Explorer , Netscape, Opera...) requisita um arquivo ***HTML*** o servidor apenas retorna o arquivo HTML.
- Quando um Navegador (Internet Explorer , Netscape, Opera...) requisita um arquivo ***ASP*** o servidor (IIS, PWS,.. ) passa a requisição para **ASP.DLL** (que esta no servidor)
- O **ASP.DLL** lê o arquivo linha por linha e executa o(s) script(s) presente(s) no arquivo ASP.
- Ao final o servidor (IIS,PWS,...) retorna o arquivo ASP para o Navegador no formato HTML.

**O que é ASP.NET ?**

- ASP.NET ou ASP+ ou ASP 3.0 é a última versão da ASP.
- ASP.NET é a próxima geração ASP
- ASP.NET não é uma atualização da última versão ASP
- ASP.NET é novo paradigma para utilização de scripts no lado do servidor.
- ASP.NET é parte da plataforma **.NET Framework**

**O que é o .NET Framework ?**

- O **.NET Framework** é a infraestrutura para a nova plataforma .NET
- O .NET Framework é um ambiente comum para construir, desenvolver e executar aplicações WEB e WEB Services
- O .NET Framework contém uma linguagem comum de runtime - **CLR** - **C**ommon **L**anguage **R**untime - , e livrarias de classes comuns - **NET, ASP.NET e Windows Forms** - que fornece serviços avançados que podem ser integrados em uma varidade de sistemas operacionais
- O .NET Framework fornece também um poderoso ambiente para desenvolvimento de aplicações , simplificando o desenvolvimento e de fácil integração com um diferentes linguagens.
- O .NET Framework atualmente suporta : C++, C#, Visual Basic, and JScript (A versão da Microsoft para o JavaScript).
- O Microsoft Visual Studio.NET é o ambiente de desenvolvimento comun para o **.NET Framework**

**ASP.NET é melhor ?**

- ASP.NET possui uma melhor linguagem de suporte e um grande número de novos controles e componentes baseados em XML além de possui um melhor uso da autenticação.
- ASP.NET aumenta o desempenho pois roda o código compilado.
- ASP.NET usa a nova tecnologia ADO.NET
- ASP.NET suporta a linguagem Visual Basic completa.(não suporta VBScript)
- ASP.NET suporta C# (C Sharp) e C++.
- ASP.NET suporta JScript
- ASP.NET apresenta maior escalabilidade.
- ASP.NET é fácil de configurar e de usar.
- ASP.NET contém um grande conjunto de controles HTML
- ASP.NET contém um novo conjunto de objetos orientados para controles de entrada de dados , como controles para validações e controles de listas.
- ASP.NET apresenta o novo controle data grid que suporta ordenação , paginação e muitos mais recursos.

**Como criar páginas ASP.NET ?**

Uma página ASP.NET é similar a uma página HTML. Veja abaixo o código para a página - **Ola.htm** - e o resultado da exibição da página no Navegador internet Explorer:

| `<html> <body bgcolor="blue"> <center> <h4>Olá Pessoal - isto é uma página HTML.</h4> </center> </body> </html>` | ![img](http://www.macoratti.net/aspnet1.gif) |
| ------------------------------------------------------------ | -------------------------------------------- |
|                                                              |                                              |

Para converter a página HTML em uma página ASP.NET basta copiar o arquivo com a extensão **.aspx**. Então renomeando o arquivo - Ola.htm - para Ola.aspx acabamos de criar uma página ASP.NET. O código continha igual e o resultado do processamento também. Verifique e compare : [Ola.htm](http://www15.brinkster.com/macoratti/asp/ola.htm) x [Ola.aspx.](http://www.macoratti.net/aspnet/ola.aspx)

## **Como funciona ?**

Fundamentalmente uma página **ASP.NET** é idêntica a uma página HTML.

Uma página HTML possui a extensão **.htm** ; se um Navegador requisita uma página HTML do servidor o servidor envia a página para o Navegador sem nenhuma alteração.

Uma página ASP.NET possui a extensão **.aspx** ; se um Navegador requisita uma página ASP.NET , o sevidor processa qualquer código script contido na página e devolve o resultado ao Navegador.

A página ASP.NET - ***Ola.aspx*** - não contém nenhum script a ser executado , então nada é executado.

A página - ***Ola.htm*** - é uma página HTML estática e a página ASP.NET - ***Ola.aspx*** - também será uma página estática. A seguir vamos mostrar como criar páginas ASP.NET dinâmicas.

## **ASP.NET - criando páginas dinâmicas**

Vamos começar mostrando o código de uma página dinâmica em ASP. Abaixo temos o código da página - **Ola.asp** - (*as páginas ASP possuem a extensão .asp*). Destacamos em azul o código que representa script que será executado pelo servidor . O código script vem entre as tags - **<% %>** e é o código que será executado pelo servidor.

| <html> <body bgcolor="blue"> <center> <h4>Olá pessoal!</h4> <p><%Response.Write(now())%></p> </center> </body> </html> | - **response.write** é um código ASP que devolve uma saida em HTML- **Now()** é uma função que retorna a data e hora do servidor. |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

O resultado do processamento do arquivo **Ola.asp** é o seguinte:

| ![img](http://www.macoratti.net/aspnet2.gif) | O arquivo **ola.asp** foi executando no PWS.- A direita temos o código da pagína **ola.asp** após o processamento. (*Perceba que o código é puro HTML.*) | <html> <body bgcolor="blue"> <center> <h4>Olá pessoal!</h4> <p>08/08/02 13:36:41</p> </center> </body> </html> |
| -------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                              |                                                              |                                                              |

Para converter a página dinâmica gerada por **ola.asp** em uma página ASP.NET dinâmica basta renomear o arquivo para **Ola.aspx**. O código continua idêntico e não sofre nenhuma alteração. Verifique você mesmo executando as duas páginas e comparando o resultado: [Ola.asp](http://www15.brinkster.com/macoratti/asp/ola.asp) x [Ola.aspx](http://www.macoratti.net/aspnet/ola.aspx)

Ora, então não há nenhuma diferença entre uma página ASP e uma página ASP.NET ?

Bem , vamos responder a esta pergunta.

Como já repetimos acima o arquivo **Ola.asp** possui tags especiais que contém código script que o servidor irá executar. No caso do arquivo Ola.asp existe uma limitação que talvez você não tenha percebido : as tags (marcadores) precisam ser colocadas onde você quer que o resultado apareça !

Para fazer isto as tags e os scripts ASP devem ficar misturados com o código HTML, ou seja , é impossível separar o código script que será executado do código HTML. Isto leva a um código de difícil leitura e manutenção ; o que convencionou-se chamar de *código espeguetti.*

A ASP.NET resolveu este problema com os **Server controls**. **Server controls** são **tags** que podem ser interpretadas pelo servidor. Existem três tipos de **Server Controls**

- **HTML Server Controls** - Tags HTML tradicionais
- **Web Server Controls** - Novas tagas ASP.NET .
- **Validation Server Controls** - Premitem a validação da entrada de dados.

**1- ASP.NET - HTML Server Controls**

Os controles de servidor - **server Controls** - HTML são tags HTML padrão , com exceção de possuirem o atributo : ***runat="server"*** . Vejamos um código que ilustra isto:

| `<% TimeStamp.InnerText=now() %> <html> <body bgcolor="aqua"> <center> <h4>Olá, Pessoal isto é uma página ASP.NET !</h2> <p id="TimeStamp" runat="server"></p> </center> </body> </html>	` |
| ------------------------------------------------------------ |
| **HTML Server Controls** - clique no link para visualizar a página : [aspnet1.aspx](http://www.macoratti.net/aspnet/aspnet1.aspx) |

O atributo **runat="server"** no exemplo acima , tornou a **tag <p>** em um controle do servidor - **server control.** O **atributo id** dá nome ao controle e torna possível fazer uma referência a ele no código executável. Agora perceba que o código foi movido para fora do código HTML.

**2- ASP.NET - Web Server Controls**

**Web Server controls** são iguais ao HTML server controls , mas são mais complexos. Eles não agem como parte de uma tag HTML existente mas tem existência independente. São frequentemente usados em aplicações interativas como formulários para entrada de dados. **Web server controls** são **tags** que começam com **<asp: .** Vejamos um exemplo a seguir:

| `<% TimeStamp.Text=now() %> <html> <body bgcolor="aqua"> <center> <h4>Olá Pessoal , isto é uma página ASP.NET !</h4> <p><asp:label id="TimeStamp" runat="server" /></p> </center> </body> </html>` |
| ------------------------------------------------------------ |
| **Web server controls** - clique no link para visualizar a página : [aspnet2.aspx](http://www.macoratti.net/aspnet/aspnet2.aspx) |

No código acima o Web server control usou o código **asp:label** . Este é um dos muitos controles do servidor(**server controls**) predefinidos que podem ser interpretados pela ASP.NET.

## **3- ASP.NET - Validation Server Controls**

Os controles de servidor para validação - **Validation server controls** - permitem a você validar uma entrada em controle de entrada de dados do servidor(*TextBox*) e exibir uma mensagem quando a validação falha.

Cada controle de validação realiza uma tarefa específica de validação. Por padrão uma página de validação é executada quando um controle *Button, ImageButton, or LinkButton* é clicado. Você pode prevenir a validação configurando a propriedade ***CausesValidation*** como igual a **False.**

**ASP.NET - Eventos.**

A ASP.NET possui manipuladores de eventos que certificam que o código seja executado no tempo apropriado. Vamos a um exemplo. Observe o código da página **aspnet3.aspx** abaixo e responda a seguinte pergunta :

Como você pode saber quando o código : <%TimeStamp.Text=now()%> será executado ?

```
<% TimeStamp.Text=now() %> <html> <body bgcolor="aqua"> <center> <h2>Olá ! Esta é uma página ASP.NET.</h2> <asp:label id="TimeStamp" runat="server" /> </center> </body> </html>
```

A resposta é : Não dá para saber !!! Sabe porque ?

Para ter certeza de que o código seja executado no tempo apropriado você deve incluir um manipulador de evento.Vamos fazer isto no código acima para você entender melhor. Veja código do arquivo **aspnet3.aspx** abaixo já com o evento incluido:

| `<script runat="server">  Sub Page_Load(Sender As Object,E As EventArgs)    TimeStamp.Text=now()  End Sub </script> <html> <body bgcolor="aqua"> <center> <h2>Esta é uma página ASP.NET com Evento.</h2> <asp:label id="TimeStamp" runat="server" /> </center> </body> </html>		` |
| ------------------------------------------------------------ |
| Gerenciando eventos -clique no link a seguir para ver o resultado - [aspnet3.aspx](http://www.macoratti.net/aspnet/aspnet3.aspx) |

Um manipulador de eventos é uma subrotina que executa um código quando um determinado evento ocorrer. No código acima foi incluido o evento **Page_Load** que ocorre quando a página é carregada.

O evento **Page_Load** é um dos muitos eventos que a ASP.NET pode interpretar. Então , quando a página for carregada , ASP.NET chama a rotina **Page_Load** e executa o código associado ao evento. Simples não é mesmo ???

Por enquanto é só !

Na continuação deste artigo vamos criar uma página Asp.NET usando controles de servidor...Aguarde...![img](http://www.macoratti.net/3_gargalha.gif)

[Veja os ](http://www.macoratti.net/destaque.htm)[Destaques e novidades do SUPER DVD Visual Basic (sempre atualizado) : clique e confira !](http://www.macoratti.net/destaques.htm)**Quer migrar para o VB .NET ?**Veja mais sistemas completos para a plataforma .NET no **[Super DVD .NET](http://www.macoratti.net/superdvd.htm)** , confira...[**Curso Básico VB .NET - Vídeo Aulas**](http://www.macoratti.net/curso_vbnet_basico.htm)**Quer aprender C# ??**Chegou o **[Super DVD C#](http://www.macoratti.net/superdvdc.htm)** com exclusivo material de suporte e vídeo aulas com curso básico sobre C#.[**Curso C# Basico - Video Aulas**](http://www.macoratti.net/curso_cshp_basico.htm)**Quer aprender os conceitos da Programação Orientada a objetos ?****[Curso Fundamentos da Programação Orientada a Objetos com VB .NET](http://www.macoratti.net/16/05/15/10/curso_fundamentos_oop.htm)** ![img](http://www.macoratti.net/new.gif)**Quer aprender o gerar relatórios com o ReportViewer no VS 2013 ?****[ Curso - Gerando Relatórios com o ReportViewer no VS 2013 - Vídeo Aulas](http://www.macoratti.net/curso_reportviewer.htm)****Quer aprender a criar aplicações Web Dinâmicas usando a ASP .NET MVC 5 ?****[ Curso ASP .NET MVC 5 - Vídeo Aulas](http://www.macoratti.net/16/05/curso_aspnet_mvc5_basico.htm)**