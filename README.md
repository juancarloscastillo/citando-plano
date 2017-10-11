# citando-plano
**Vínculos entre Bibtex, Markdown, Latex, Pandoc y Zotero para generar documentos académicos con referencias bibliográficas**

**Juan Carlos Castillo - Instituto de Sociología, Pontificia Universidad Católica de Chile,  [www.jc-castillo.com](www.jc-castillo.com)**

**Objetivo**: poder facilitar la inclusión de citas y referencias bibliográficas en documentos escritos en texto plano (Markdown / Latex).

## Bibtex, Zotero y Beter BibTex (BBT)

La forma general como funciona la inclusión de referencias en texto plano (Latex/Markdown) es tenerlas almacenadas en formato Bibtex (archivos en extensión .bib). Este formato almacena las referencias en base a ciertos campos donde se incluye la información correspondiente. Por ejemplo:

```
@article{sabbagh_dimension_2003,
  title = {The Dimension of Social Solidarity in Distributive Justice},
  volume = {42},
  timestamp = {2014-09-26T12:30:41Z},
  number = {2},
  urldate = {2014-09-26},
  journal = {Social science information},
  author = {Sabbagh, Clara},
  year = {2003},
  pages = {255--276},
  file = {Snapshot:/storage/V5R7I29W/255.html:text/html},
  groups = {social justice theory,social justice theory}
}
```

Luego, en la primera línea aparece la "clave" (key) de la referencia (en este caso sabbagh_dimension_2003), que permite llamarla en el texto como veremos más adelante.

Por supuesto, almacenar manualmente referencias en este formato bib no es muy amigable. Si bien una serie de softwares de administración de referencias tienen la opción de convertir fácilmente la colección o parte de ella a formato .bib, el problema es que si se añade una referencia en el software, cada vez habría que convertir/sincronizar nuevamente a .bib para mantener esta base también actualizada. Por lo tanto, lo ideal sería que una colección .bib se actualizara automáticamente desde un software de gestión de referencias. La solución que por ahora se recomienda es usar la aplicación Better(bib)tex (BBT), que funciona dentro de Zotero (www.zotero.org). Ambos gratuitos y de código abierto, así que ok.

**Zotero / BBT**: El funcionamiento de Zotero queda fuera del alcance de este tutorial, solo nos enfocaremos en el vínculo con BBT.

  - instalar siguiendo las instrucciones: https://github.com/retorquere/zotero-better-bibtex/wiki  (NOTA: se han reportado problemas exportando con la nueva versión de Zotero (5); la adaptación de BBT se encuentra en desarrollo, ver https://github.com/retorquere/zotero-better-bibtex/issues/555); por lo tanto, si hay problemas con la instalación tradicional con el Zotero 5, se recomienda instalar la versión 4 de Zotero Standalone, y bajar la versión previa correspondiente de la extensión https://github.com/retorquere/zotero-better-bibtex/releases/tag/1.6.100)
  - recordar reiniciar Zotero para que la instalación se complete.
  - Ahora, si se quiere exportar a bib, basta solamente posicionarse sobre una carpeta (que también puede ser la colección completa), botón derecho, export collection, y en el formato escoger "Better BibTex". Luego escoger directorio donde se graba (que puede ser el mismo de Zotero).
  - Para revisar las opciones de la sincronización, ir a edit>preferences aparece una pestaña nueva al final a la derecha de BBT. En esa pestaña hay una serie de opciones que luego se pueden explorar, por lo pronto ir a la pestaña "Automatic export" donde debería aparecer en el listado la carpeta seleccionada para exportar. En "automatic export" seleccionar "on change", que hace que cada vez que se cambia algo en Zotero de esa carpeta, se cambia también en el archivo .bib exportado y sincronizado.

### Sobre exportar referencias en trabajo colaborativo

- Aquí, una opción es dar el link desde Markdown/Latex al archivo completo de Zotero (del autor a cargo), pero en general es muy pesado y contiene todas las referencias, no el subgrupo que se utiliza en el paper. Por lo tanto, se recomienda hacer lo siguiente:
    -  crear una colección/carpeta compartida de Zotero (asumiendo escenario de trabajo colaborativo) donde se copian las referencias que se utilizan en el paper. Esto es fácil en Zotero, solo se arrastran, y no hace que toda la información se duplique, es solo un link. Como es compartida, cualquier miembro del equipo puede modificar. Precaución: el nombre de esta carpeta sin espacios y sin acentos
    - El coordinador/primer autor exporta esta colección a la carpeta del proyecto colaborativo (eventualmente un dropbox) donde está el tex/md. Para ello, botón derecho sobre la carpeta, "export library", seleccionar *format Better Bibtex*, y muy importante: check box "keep updated", así cualquier cambio que se haga en la colección desde Zotero se reflejará en el .bib. Guardar en la carpeta donde se encuentra el archivo tex
    - Luego, revisar en la pestaña de BBT de preferencias, en automatic export, que la carpeta efectivamente está en el listado. Además, marcar la opción "on change", así apenas se actualice la librería de Zotero se va a actualizar el bib

## Referenciando en TEX

  - En el preambulo (hay diferentes opciones de formato, pero para estilo clásico APA):

    - \usepackage{natbib} % for Bibtex
    - \bibliographystyle{apalike}   % ver por ej otros estilos en https://es.sharelatex.com/learn/Natbib_bibliography_styles
    - Y luego, donde se quiera la bibliografía, (usualmente, antes de \end(document)
        - \bibliography{micolección} % aquí va el nombre de la colección, cuidado con no darle nombre con espacios, y tampoco terminarla con .bib
        - También se puede indicar con path relativos, ej: \bibliography{../../bib/merit_pref_int} , donde "../" es para subir un nivel en la estructura de directorios
    - Con esto, ya se puede comenzar a citar con las distintas opciones (ver https://gking.harvard.edu/files/natnotes2.pdf)


  - Para mayores detalles referentes a natbib y en general bibliographic management en Latex ver https://es.sharelatex.com/learn/Bibliography_management_with_natbib

  - Algunos issues con Latex: si se añade alguna cita a la carpeta Zotero, si bien esto es actualizado automáticamente en el bib, no necesariamente es reconocido al momento de citar. Por eso, se recomienda tener abierto el archivo .bib en el editor de tex en otra pestaña, y si la referencia no aparece al intentar citar compilar el bib, esto hace que queden disponibles para citar (lo que se ve en el .bbl, donde se encuentran las referencias citadas en el texto)
    - Por lo visto, las referencias en el .bbl se van sumando, y no se borran. Por lo tanto, puede pasar que se cite algo en alguna ocasión, pero si esa cita se decide borrar va a seguir de todas maneras apareciendo en la bibliografía final. Para ajustar esto, cuando se genere una versión más definitiva del documento, borrar el bbl y compilar el tex nuevamente.
    - Atención: si se quiere cambiar el estilo (\bibliographystyle{}), a veces no lo reconoce y se queda con el anterior o arroja error; la opción que me resulta es borrar los archivos aux y bbl, y luego compilar nuevamente.
    - También hay problemas cuando alguna entrada del archivo .bib no tiene el año, en este archivo aparecen como ???? y esto crea dificultades de compilación. Importante: arreglar esto en Zotero (no en bib ni bbl), sincronizar nuevamente y compilar.

## Referenciando en Markdown

- se establece la ruta al archivo bib en el YAML header, al comienzo del documento, por ejemplo:

```
---
bibliography:
- 'MyLibrary.bib'
---
```
- para citar, se debe escribir el "citation key" de la referencia correspondiente.
- la lista de referencias aparece automáticamente al final del documento
- el estilo de bibliografía se debe indicar adicionalmente, basado en un archivo .csl correspondiente.Un listado de estilos disponibles se encuentra en: https://www.zotero.org/styles
- Luego el csl se agrega al YAML. Ej:

```
---
bibliography:
- MyLibrary.bib
- csl: apa.csl
---
```

- Alternativas para automatizar la inserción de referencias:  ya que insertar referencias manualmente es muy engorroso, hay algunas alternativas de automatización que generan un flujo de trabajo similar al de insertar citas y bibliografía en Word/Open Office vía Zotero. El mejor entorno que conozco para hacer esto es Atom, porque sirve tanto para Latex como para Markdown. También hay una forma en Rstudio vía la librería/add-in "citr". Comenzamos con esta:

- Usando Rstudio - citr https://github.com/crsh/citr:
  - Al instalar Rmarkdown, se instala automaticamente pandoc al interior de la carpeta de Rstudio (/usr/lib/rstudio/bin/pandoc), donde están los ejecutables pandoc y pandoc-citeproc. Por lo tanto, en archivos Rmd basta dar el nombre del archivo/path al bib  en el YAML header para que encuentre la bibliografía y la compile correctamente.
  - Instalar citr
  - reiniciar
  - Luego en el add-in (desplegable, o tools/add-ins) aparece "insert citations", si está bien especificado el bib en el YAML debería aparecer aquí la lista de referencias.

## Usando Atom para flujo de trabajo académico en texto plano con citas

Aquí hay tres cosas que ver: insertar, preview y convert

  - Insertar:
      - para insertar citaciones lo más fácil es instalar el zotero-picker, que automáticamente detecta la librería bib que se encuentra en la misma carpeta de Zotero (vía Better Bibtex). Funciona igual que el plugin clásico para procesadores de texto, shortcut alt-z
      - otra alternativa que se puede instalar en paralelo es el autocomplete-bibtex, que busca la cita una vez escrito @ y las tres primeras letras, asumiendo que la bib está en el mismo directorio (o probar también si funciona dando el path con YAML)

  - Preview
      - markdown se puede visualizar simultáneamente en atom con el paquete markdown-preview-plus (MPP) (ctrl+shift+m). Para que aparezcan las citas y la bibliografía se deben hacer un par de ajustes (* si se instala Rmarkdown, pandoc ya está instalado, pero en el directorio de R y Atom no lo reconoce, por eso recomiendo instalarlo nuevamente):
        - instalar pandoc, en ubuntu
          - sudo apt-get update
          - sudo apt-get install pandoc
          - chequear instalado: dpkg -L pandoc
        - instalar pandoc citeproc
          - sudo apt-get update
          - sudo apt-get install pandoc-citeproc
        - en las opciones del paquete
          - enable pandoc parser
          - pandoc options: citations
        - en el documento .md crear al principio un YAML header con el path hacia el bib:

```
 ---
bibliography:
- '/media/ntfs/Dropbox/zoterojcydocs/MyLibrary.bib'
---
```
    - con esto, luego el MPP muestra las citas (en el preview)


  - Convertir: el paquete pandoc-convert (hasta ahora) no convierte las citas, solo el texto. Lo que funciona es vía linea de comando, abriendo terminal desde atom y:
    - pandoc -s -S --bibliography MyLibrary.bib --filter pandoc-citeproc --csl apa-cv.csl inequality_perception_issp.md -o inequality_perception_issp.html
