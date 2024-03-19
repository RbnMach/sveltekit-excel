<script lang="ts">
	import { onMount } from 'svelte';

	let divHtml: HTMLDivElement;
	let jexcel: any;

	onMount(async () => {
		const jspreadsheet = (await import('jspreadsheet-ce')).default; //paquete de cliente

		jexcel = jspreadsheet(divHtml, {
			data: [
				['Jazz', 'Honda', '2019-02-12', '', true, '$ 2.000,00', '#777700'],
				['Civic', 'Honda', '2018-07-11', '', true, '$ 4.000,01', '#007777']
			],
			columns: [
				{ type: 'text', title: 'Car', width: 120, name: 'car' },
				{ type: 'dropdown', title: 'Make', width: 200, source: ['Alfa Romeo', 'Audi', 'Bmw'] },
				{ type: 'calendar', title: 'Available', width: 200 },
				{ type: 'image', title: 'Photo', width: 120 },
				{ type: 'checkbox', title: 'Stock', width: 80 },
				{ type: 'numeric', title: 'Price', width: 100, mask: '$ #.##,00', decimal: ',' },
				{ type: 'color', title: 'Color', width: 100, render: 'square' }
			],
			// csv: '/jspreadsheet/arts.csv',
			csvHeaders: true,
			tableOverflow: true,
			search: true,
			footers: [['Total', '', '', '', '', '=SUM(F1:F8)']],
			text: {
				search: 'Buscar',
				noRecordsFound: 'No se encontraron registros',
				showingPage: 'Mostrando página {0} de {1} entradas',
				show: 'Mostrar',
				entries: 'entradas',
				insertANewColumnBefore: 'Insertar una nueva columna antes de',
				insertANewColumnAfter: 'Insertar una nueva columna después de',
				deleteSelectedColumns: 'Eliminar columnas seleccionadas',
				renameThisColumn: 'Renombrar esta columna',
				orderAscending: 'Orden ascendente',
				orderDescending: 'Orden descendente',
				insertANewRowBefore: 'Insertar una nueva fila antes de',
				insertANewRowAfter: 'Insertar una nueva fila después de',
				deleteSelectedRows: 'Eliminar filas seleccionadas',
				editComments: 'Editar comentarios',
				addComments: 'Agregar comentarios',
				comments: 'Comentarios',
				clearComments: 'Limpiar comentarios',
				copy: 'Copiar ...',
				paste: 'Pegar ...',
				saveAs: 'Guardar como ...',
				about: 'Acerca de',
				areYouSureToDeleteTheSelectedRows: '¿Está seguro de eliminar las filas seleccionadas?',
				areYouSureToDeleteTheSelectedColumns:
					'¿Está seguro de eliminar las columnas seleccionadas?',
				thisActionWillDestroyAnyExistingMergedCellsAreYouSure:
					'Esta acción eliminará todas las celdas combinadas existentes. ¿Está seguro?',
				thisActionWillClearYourSearchResultsAreYouSure:
					'Esta acción limpiará sus resultados de búsqueda. ¿Está seguro?',
				thereIsAConflictWithAnotherMergedCell: 'Hay un conflicto con otra celda combinada',
				invalidMergeProperties: 'Propiedades de combinación inválidas',
				cellAlreadyMerged: 'Celda ya combinada',
				noCellsSelected: 'No se seleccionó ninguna celda'
			}
		});
	});
</script>

<svelte:head>
	<script src="https://bossanova.uk/jspreadsheet/v4/jexcel.js"></script>
	<script src="https://jsuites.net/v4/jsuites.js"></script>
	<link rel="stylesheet" href="https://bossanova.uk/jspreadsheet/v4/jexcel.css" type="text/css" />
	<link rel="stylesheet" href="https://jsuites.net/v4/jsuites.css" type="text/css" />

	<link
		rel="stylesheet"
		href="https://bossanova.uk/jspreadsheet/v4/jexcel.themes.css"
		type="text/css"
	/>
</svelte:head>

<div bind:this={divHtml}></div>
<br />
<button type="button" on:click={() => jexcel.destroy(divHtml, true)}>Destruir</button>
<button type="button" on:click={() => console.log(jexcel.getData())}>Obtener datos DATA</button>
<button type="button" on:click={() => console.log(jexcel.getJson())}>Obtener datos JSON</button>
<button type="button" on:click={() => console.log(jexcel.download())}>Descargar</button>

<style>
	:root {
		--jexcel_header_color: #888;
		--jexcel_header_color_highlighted: #444;
		--jexcel_header_background: #313131;
		--jexcel_header_background_highlighted: #777;
		--jexcel_content_color: #777;
		--jexcel_content_color_highlighted: #333;
		--jexcel_content_background: #3e3e3e;
		--jexcel_content_background_highlighted: #333;
		--jexcel_menu_background: #7e7e7e;
		--jexcel_menu_background_highlighted: #ebebeb;
		--jexcel_menu_color: #ddd;
		--jexcel_menu_color_highlighted: #222;
		--jexcel_menu_box_shadow: unset;
		--jexcel_border_color: #5f5f5f;
		--jexcel_border_color_highlighted: #999;
		--active_color: #eee;
	}
</style>
