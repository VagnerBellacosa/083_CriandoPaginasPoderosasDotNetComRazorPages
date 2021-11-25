# Por que a Razor Pages é a abordagem recomendada para criar uma interface de usuário da Web no Asp.net Core 2.0?

Aprender coisas novas requer investimento de tempo, espaço e energia. Atualmente estou aprendendo Asp.Net Core MVC 2.0. Esta [Visão Geral dos Tutoriais do ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/tutorials/) estados:

> Razor Pages é a abordagem recomendada para criar uma interface do usuário da Web com o ASP.NET Core 2.0.

Esta informação me confundiu ao decidir se eu teria que parar de aprender o Asp.net Core MVC e começar a aprender o Asp.net Core Razor Pages.

- Por que a Razor Pages é a abordagem recomendada para criar uma interface de usuário da Web no Asp.net Core 2.0? 

Qualquer direção é bem vinda.

**[asp.net](https://www.ti-enxame.com/pt/asp.net/)****[asp.net-core](https://www.ti-enxame.com/pt/asp.net-core/)****[asp.net-core-mvc](https://www.ti-enxame.com/pt/asp.net-core-mvc/)****[asp.net-core-mvc-2.0](https://www.ti-enxame.com/pt/asp.net-core-mvc-2.0/)****[razor-pages](https://www.ti-enxame.com/pt/razor-pages/)**

 36

16 de out. de 2017[Artificial Stupidity](https://stackoverflow.com/users/5482465/artificial-stupidity)







O Razor Pages é otimizado para fluxos de trabalho baseados em página e pode ser usado nesses cenários com menos partes móveis do que os modelos MVC tradicionais. Isso porque você não precisa lidar com Controladores, Ações, Rotas, ViewModels e Views (como normalmente faria). Em vez disso, seu roteiro é baseado em convenções e seu PageModel serve como seu Controlador, Ação (s) e ViewModel, tudo em um. A página, naturalmente, substitui a vista. Você também não precisa ter tantas pastas quanto faria no MVC, simplificando ainda mais o seu projeto.

De [ASP.NET Core - Aplicativos ASP.NET MVC mais simples com o Razor Pages](https://msdn.microsoft.com/en-us/magazine/mt842512.aspx) , um artigo do MSDN de setembro de 2017 por [Steve Smith](https://msdn.microsoft.com/en-us/magazine/mt149362?author=steve smith) :

> [Razor Pages] fornece 
>
> - uma maneira mais simples de organizar o código dentro dos aplicativos ASP.NET Core, mantendo a lógica de implementação e os modelos de visualização mais próximos do código de implementação da visualização. 
> - Eles também oferecem uma maneira mais simples de começar a desenvolver aplicativos ASP.NET Core, 

Esse artigo tem mais informações sobre por que usar o Razor Pages over MVC para fluxos de trabalho baseados em página. Obviamente, para APIs, você ainda desejará usar os Controllers.

### Edição de terceiros - desvantagens da organização clássica de pastas MVC

[ASP.NET Core - Fatias de recursos para o ASP.NET Core MVC](https://msdn.microsoft.com/en-us/magazine/mt763233) , um artigo do MSDN antigo de setembro de 2016, descreve por que a convenção MVC clássica para organizar exibições e controlador pode ter desvantagens para projetos maiores. O artigo dá um exemplo de quatro conceitos de aplicativos frouxamente relacionados: *Ninjas, Plants, Pirates and Zombies*. O artigo descreve uma maneira de estruturá-los fora da convenção de pastas padrão, organizando arquivos em pastas por recurso ou área de responsabilidade. 

 24

17 de out. de 2017[ssmith](https://stackoverflow.com/users/13729/ssmith)



A Microsoft está voltando à abordagem WebForms para simplificar a estrutura do projeto confiando no mantra "Convenção sobre configuração", enquanto oculta a configuração do desenvolvedor para tornar as coisas mais rápidas. Mas tem a desvantagem de que tudo será misturado novamente. Eu não pareço uma jogada inteligente para organizar. Mas ... Ei! Algo novo deve chamar a atenção do desenvolvedor para a Microsoft. 

**Se sua página usa uma API da Web do MVC para o REStful, é realmente mais fácil usar apenas as páginas do Razor. Se não, eu recomendo que você use o Core MVC.**

Em grandes projetos, onde o modelo e o controlador estão juntos no mesmo arquivo, a manutenção será um pesadelo. Ele funciona bem para clases com apenas 2 propriedades, mas viola o Princípio de Fechamento Aberto da POO. Você deve projetar e usar uma arquitetura que pode crescer com o tempo (Extensible) e ainda ser estável e lógica (sem reestruturar o projeto), apenas estendê-lo usando o mesmo padrão. 

 5

14 de mar. de 2018[Sterling Diaz](https://stackoverflow.com/users/1228807/sterling-diaz)

Os desenvolvedores estavam em fóruns em 2013 perguntando "O que a Microsoft quer dizer, o Silverlight não é o recomendado ... ???" Só que desta vez, é que o MVC será declarado morto e viverá muito tempo no MVVM. .____.] E você pode esperar que o MVC seja jogado no depósito de sucata, lentamente, mas acelerado em cerca de 18 meses a partir de agora, e todo e qualquer tempo gasto em aprender MVC irá para o mesmo depósito. Além disso, o MVVM parece fácil, mas leva um ano para pegar o jeito e realmente fazer certo.