# Criando-páginas-poderosas-no-.Net-com-Razor-Pages

Para criar páginas poderosas no .NET com Razor Pages, vamos detalhar o passo a passo e fornecer exemplos de código.

Passo a Passo para Criar Páginas com Razor Pages
1. Criando um novo projeto
Primeiramente, vamos criar um novo projeto no Visual Studio utilizando o template de Razor Pages.

Abra o Visual Studio.
Crie um novo projeto (File -> New -> Project).
Selecione ASP.NET Core Web Application.
Escolha um nome para o projeto e clique em Create.
Selecione o template Razor Pages e clique em Create.
2. Estrutura de diretórios
No projeto de Razor Pages, as páginas são organizadas por diretórios dentro da pasta Pages. Cada diretório representa um agrupamento lógico de páginas relacionadas.

Por exemplo:

/Pages
    /Index.cshtml
    /About.cshtml
    /Contact.cshtml
3. Adicionando novas páginas
Para adicionar uma nova página, basta adicionar um arquivo .cshtml dentro do diretório Pages ou em um subdiretório correspondente.

Exemplo: criando uma página de detalhes para um produto.

Crie um novo arquivo Details.cshtml em /Pages:
@page
@model ProdutoDetalheModel

<h1>Detalhes do Produto</h1>

<div>
    <p>Nome: @Model.Nome</p>
    <p>Descrição: @Model.Descricao</p>
    <p>Preço: @Model.Preco.ToString("C")</p>
</div>
4. Adicionando um modelo (Model)
Os modelos são classes C# que definem a estrutura de dados utilizada nas páginas Razor. Eles podem ser simples classes de dados ou incluir lógica para acesso a dados.

Crie uma classe ProdutoDetalheModel.cs para representar o modelo de dados do produto:
public class ProdutoDetalheModel
{
    public string Nome { get; set; }
    public string Descricao { get; set; }
    public decimal Preco { get; set; }
}
5. Lógica da Página (Page Model)
A lógica da página é encapsulada em uma classe Page Model (cshtml.cs), que interage com o modelo de dados e fornece dados à página Razor.

Crie um arquivo Details.cshtml.cs para a lógica da página:
using Microsoft.AspNetCore.Mvc.RazorPages;

public class DetailsModel : PageModel
{
    public ProdutoDetalheModel Produto { get; set; }

    public void OnGet()
    {
        // Simulação de dados
        Produto = new ProdutoDetalheModel
        {
            Nome = "Produto A",
            Descricao = "Descrição do Produto A",
            Preco = 99.99m
        };
    }
}
6. Navegação entre Páginas
Para navegar entre páginas Razor, utilize diretivas HTML ou métodos de URL helper.

Exemplo: navegação para a página de detalhes de produto.

<a asp-page="Details">Detalhes do Produto</a>
Conclusão
Razor Pages oferece uma maneira poderosa e simplificada de criar aplicativos web no .NET, unificando a camada de visão e controle. Com esta abordagem, podemos criar rapidamente páginas web com código limpo e estruturado.

Vamos explorar alguns exemplos básicos de código usando Razor Pages no contexto de um projeto ASP.NET Core. Vou dividir em alguns módulos para facilitar o entendimento:

### Módulo 1: Configuração Básica

1. **Criando uma página Razor**: Para criar uma página Razor, você cria um arquivo `.cshtml` dentro da pasta `Pages` do seu projeto. Por exemplo, `Pages/Index.cshtml` é a página inicial do seu site.

   ```html
   <!-- Pages/Index.cshtml -->
   @page
   <h1>Bem-vindo à minha página Razor!</h1>
   <p>Esta é a página inicial.</p>
   ```

2. **Definindo um modelo**: Cada página Razor pode ter um modelo associado que fornece dados à página. O modelo é uma classe C# que pode ser injetada com dependências.

   ```csharp
   // Pages/Index.cshtml.cs
   public class IndexModel : PageModel
   {
       public void OnGet()
       {
           // Este método é chamado quando a página "GET" é requisitada.
       }
   }
   ```

### Módulo 2: Trabalhando com Dados

1. **Passando dados para a página**: Você pode passar dados do modelo para a página Razor usando propriedades.

   ```csharp
   // Pages/Contact.cshtml.cs
   public class ContactModel : PageModel
   {
       public string Message { get; set; }

       public void OnGet()
       {
           Message = "Entre em contato conosco!";
       }
   }
   ```

   ```html
   <!-- Pages/Contact.cshtml -->
   @page
   @model ContactModel
   <h1>@Model.Message</h1>
   ```

### Módulo 3: Manipulando Formulários

1. **Criando um formulário**: Você pode criar e manipular formulários HTML em páginas Razor para receber dados do usuário.

   ```html
   <!-- Pages/Contact.cshtml -->
   @page
   @model ContactModel
   <form method="post">
       <input asp-for="Message" />
       <button type="submit">Enviar</button>
   </form>
   ```

   ```csharp
   // Pages/Contact.cshtml.cs
   public class ContactModel : PageModel
   {
       [BindProperty]
       public string Message { get; set; }

       public void OnGet()
       {
           Message = "Entre em contato conosco!";
       }

       public IActionResult OnPost()
       {
           // Lógica para processar o formulário aqui
           // Exemplo: salvar em um banco de dados, enviar um e-mail, etc.
           return RedirectToPage("/Index");
       }
   }
   ```

### Módulo 4: Utilizando Layouts

1. **Criando um layout**: Layouts são arquivos `.cshtml` compartilhados entre várias páginas para fornecer um visual consistente.

   ```html
   <!-- Pages/Shared/_Layout.cshtml -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>@ViewData["Title"] - Meu Site</title>
   </head>
   <body>
       <div>
           @RenderBody()
       </div>
   </body>
   </html>
   ```

2. **Usando o layout em uma página**: Especifique o layout em cada página Razor para aplicar o estilo e a estrutura compartilhada.

   ```html
   <!-- Pages/Index.cshtml -->
   @page
   @{
       ViewData["Title"] = "Página Inicial";
       Layout = "/Pages/Shared/_Layout.cshtml";
   }

   <h1>Bem-vindo à minha página inicial!</h1>
   <p>Esta é a página inicial do meu site.</p>
   ```

### Módulo 5: Trabalhando com Componentes

1. **Criando um componente parcial**: Componentes parciais permitem reutilizar blocos de código em várias páginas.

   ```html
   <!-- Pages/Shared/_Status.cshtml -->
   <div>
       <p>Status: @ViewData["StatusMessage"]</p>
   </div>
   ```

   ```html
   <!-- Pages/Index.cshtml -->
   @page
   @{
       ViewData["Title"] = "Página Inicial";
       Layout = "/Pages/Shared/_Layout.cshtml";
   }

   <h1>Bem-vindo à minha página inicial!</h1>
   <partial name="_Status" />
   ```

Esses exemplos devem ajudar a entender como poderemos começar a trabalhar com Razor Pages em um projeto ASP.NET Core, criando páginas dinâmicas, trabalhando com dados, formulários, layouts e componentes parciais.
