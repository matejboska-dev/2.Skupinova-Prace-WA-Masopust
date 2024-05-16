
# 2. Skupinová práce - popis řešení

  

  

  

## Počeštění

  

  

### Jazykové stringy

  

V souboru jquery.dataTables. js jsem našel všechny stringy, které odpovídají nějaké zprávě nebo popisu, a přeložil jsem je do češtiny.

  

  

  

Příklad:

  

  

  

z:

  

```php

"sInfoFiltered": "(filtered from _MAX_ total entries)"

```

  

  

jsem přeložil na:

  

  

```php

"sInfoFiltered": "(filtrováno z _MAX_ celkem záznamů)"

```

  

  

  

Poté, jsem změnil odkazy na script ve dvou souborech:

  

  

```html

<script type="text/javascript" charset="utf8" src="[https://cdn.datatables.net/1.12.1/js/jquery.dataTables.js](https://cdn.datatables.net/1.12.1/js/jquery.dataTables.js)"></script>

```

  

  

v table.php na:

  

  

```html

<script type="text/javascript" charset="utf8" src="vendor/jquery.dataTables.js"></script>

```

  

  

  

a v tableEvents.php na:

  

```html

<script type="text/javascript" charset="utf8" src="../vendor/jquery.dataTables.js"></script>

```

  

### Odstranění null hodnot v tabulce

  

Dále jsem odstranil null hodnoty z načítání do tabulky v table.php:

  

  

  

Dřive, při načítání dat při tvorbě záznamu v tabulce se čistě načetla hodnota.

  

  

```php

<td class="<?php echo $column_name; ?> click"><?php echo $row[$column_name]; ?></td>

```

  

  

Přidal jsem kontrolu, která si nejdřívě ověří že se nenačítá stringový ekvivalent hodnoty null, pokud ano, nahradí ho prázdným stringem, a pokud ne tak načte hodnotu.

  

  

```php

<td class="<?php echo $column_name; ?> click"><?php echo ($row[$column_name]=="null") ? "" : $row[$column_name]; ?></td>

```

  

## Tlačítko zavřít plovoucí

  

Cílem tohoto úkolu bylo nastavit tlačítko, které zavírá postraní okno tak, že se stále nachází na obrazovce.

  

![](https://lh7-us.googleusercontent.com/UNyjAzNrnDIG_04oGt3jCmpjc08RRWfVzKsCBUVAU5AN0XP3GhmlWXQTc1GyKATPsAsek1eziFS-Ad2KTNQxt0xSTkmhECzUTd1v1d89nQZFMQuDpPZb9lVAxZyo7GAKQenLFst6IPC8iRjEXNZES1k)

  
  

Zjistili jsme, že toto tlačítko má id `#closeIFrame`. Následně jsme ve souboru `css/style.css`nastavili následující.

  

```css

#closeIframe {

z-index: 100;

position: sticky;

float: right;

right: 0;

}

```

  

## Vyhledávátka, nejde klikání na řádek![](https://lh7-us.googleusercontent.com/JD2FfoIPYT6rbI-tS44YDiQAzho-kyPqsPqV7uy_tKjQNYHttU_m_SEkYkeDcQAFvAmFuufYLOwoppNPEjEnwWNs1H_mSHDjVH5x7LIHZjyGPsJTMt5R_HuCfrpKFHkWD-JaHhgYEBIqsIBivDNuz3g)

- Úprava javascriptového souboru select.js, kvůli kterému občas nebylo možné si zobrazit bližší informace o dané firmě.

  

Soubor select.js:

```javascript
$(document).ready(function(event){
	var main = $("#main-select");
	main.click(function(event){
		var state = main.prop("checked");
		console.log(state);
		var chechboxs = $(".check");
		for(const box of chechboxs){
			$(box).prop("checked", state);
			if(state != false){
				$(box).parent().parent().addClass("selected");
			}else {
				$(box).parent().parent().removeClass("selected");
			}
		}
	})
	var click = $(".check");
	click.click(function(event){
		var state2 = $(event.target).prop("checked");
		if(state2 != false){
			$(event.target).parent().parent().addClass("selected");
		}else {
			$(event.target).parent().parent().removeClass("selected");
		}
	})
});
```

## Reverzní tlačítko

Dalším úkolem je vytvoření tlačítka při exportu, které převrátí výběr položek v daném exportu.

  

V souboru `js/table.js` jsme našli funkci tlačítka `export-btn`, která vypisuje výběr. Tam jsme vytvořili tlačítko s funkcí, která pomocí foreach cyklu všech výběrů převrátí hodnoty.

```javascript

var inverseBtn = document.createElement('button');

inverseBtn.innerHTML = "převrátit";

inverseBtn.type = 'button';

inverseBtn.addEventListener('click', function(){

  

var checks = $('form[name="expF"]').children("input");

for (var ii=0;ii<checks.length;ii++) {

var check = checks[ii];

check.checked = !check.checked;

}

});

form.appendChild(inverseBtn);

```
