# BootWrapper

Este projeto tem como objetivo facilitar o udo do Bootstrap.<br/>
Ele possui classes que estendem metódos para a classe HtmlHelper. Todos os métodos iniciam pelas letras BW.<br/>

Todos os componentes podem ser utilizados nas views através da nomenclatura.
<code>@Html.BW*Nome_do_Metodo*</code>

## Install

1 Faça o download do arquivo BootWrapper.BW.dll que se encontra na pasta releases.

2 Adicione a dll no seu projeto.

3 Instale através do Nuget os componentes necessários para utilizaçao do BootWrapper. *Se preferir, substitua o arquivo package.config do seu projeto pelo arquivo que se encontra na pasta 'nuget'.*
  * Install-Package bootstrap -version 3.34
  * Install-Package Bootstrap.Datepicker -version 1.4.0
  * Install-Package BootstrapBootstrap-3-Typeahead -version 3.1.1
  * Install-Package FontAwesome -version 3.1.1
  * Install-Package FontAwesome.MVC -version 1.0.0
  * Install-Package jQuery -version 2.1.4
  * Install-Package jquery.datatables -version 1.10.7
  * Install-Package jQuery.Validation -version 1.13.1
  * Install-Package Messenger -version 1.4.1

4 Adicione no seu arquivo de lauyout os arquivos de javascript que se encontram na pasta 'js'. Ou crie um bundle:
```C#
    var scriptBundle = new ScriptBundle("~/bundles/bootwrapper");
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.Init.js");
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.Helpers.js");
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.Base.js");
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.Validation.js");
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.Typeahead.js");
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.DataTable.js");            
    scriptBundle.Include("~/Scripts/bootwrapper/BootWrapper.Mask.js");
    bundles.Add(scriptBundle);
```

5 Inicie o BootWrapper
```javascript
      jQuery(document).ready(function () {
          $.bwStartBootWrapper();
      });
```
6 Adicione o Namespace para utilziação das tags
Dentro do arquivo Views\Shared\web.config, adicione o namespace dos controles.
```xml
<add namespace="BootWrapper.BW.Controls"/>
``` 
## Classes de/para  Bootstrap 
- Algumas Enumerations dentro da biblioteca tem a função de fazer a tradução para as classes do bootstrap.
  * BootWrapper.BW.Controls.PanelColor
  * BootWrapper.BW.Controls.ButtonColor
  * BootWrapper.BW.Controls.ButtonAction
  * BootWrapper.BW.Controls.ButtonSize

- Classes para geração das tags se encontram em *BootWrapper.BW.Controls.UI*
- Os métodos estendidos do HtmlHelper são declarados na classe *BootWrapper.BW.Controls.WebControls*

## Exemplos
- Painel

```ASP
@using (Html.BWBeginPanel("Título do Painel", PanelColor.Default, new { @class = "col-lg-12" }))
{
// body
}
-- Variação
@using (Html.BWBeginPanel("pnl-id", "Título","fa fa-bars" ,PanelColor.Default, new { @class = "col-lg-12" }))
{
// body
}
```

- Form
```ASP
@using (Html.BWBeginFormEdit("frmEdit", "actionName", "controllerName"))
{
    @Html.AntiForgeryToken()
    @Html.BWHiddenFor(model => model.Id)
    
    using (Html.BWBeginControl())
    {
        @Html.BWLabelFor(model => model.Login)
        @Html.BWTextBoxFor(model => model.Login)
    }

    using (Html.FWBeginControl())
    {
        @Html.BWLabelFor(model => model.Nome)
        @Html.BWTextBoxFor(model => model.Nome)
    }

    using (Html.FWBeginControl())
    {
        @Html.BWLabelFor(model => model.Ativo)
        @Html.BWCheckBoxFor(model => model.Ativo)
    }
    
    using (Html.FWBeginControl())
    {
        @Html.BWLabelFor(model => model.Entity.Senha)
        @Html.BWPasswordFor(model => model.Entity.Senha)
    }
    
    using (Html.BWBeginControl("actions", new { @class = "form-actions" }))
    {
        @Html.BWButtonSubmit("btn-save").Set(ButtonSize.Large).Set(ButtonAction.Save).Set(ButtonColor.Green).Attrib(new { style = "margin-top:20px;" }).Button("Salvar", "submit");
    }
}
```
