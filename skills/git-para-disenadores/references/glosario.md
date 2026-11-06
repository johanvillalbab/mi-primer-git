# Glosario en lenguaje llano

Usa la frase de la segunda columna la primera vez que aparezca el término. La tercera columna corrige la confusión más común en diseñadores (Isomöttönen y Cochez 2014, Pro Git §3.1, GitHub Docs). Si la persona muestra esa confusión, corrígela con la frase de esa columna.

| Término | Explicación en una frase | Confusión típica y cómo corregirla |
|---|---|---|
| Git | La herramienta que guarda el historial de cambios de tu proyecto en tu computadora. | «Git y GitHub son lo mismo». Git es la herramienta, GitHub es el sitio web donde se comparte. |
| GitHub | El sitio web donde vive una copia de tu proyecto para compartirlo, revisarlo y publicarlo. | «Es un Google Drive para código». No sincroniza solo. Tú decides cuándo subir y cuándo traer cambios. |
| Repositorio (repo) | La carpeta de tu proyecto más todo su historial de cambios. | «Es solo la carpeta». El historial vive en la carpeta oculta `.git`. Si se borra, se pierde el historial. |
| Commit | Un punto guardado del historial, con un mensaje que dice qué cambió y para qué. | «Es Ctrl+S». Guardar el archivo no crea un commit. Tú eliges cuándo y qué entra. Se parece más a una versión con nombre en Figma. |
| Staging (`git add`) | Elegir qué cambios entran en el próximo commit. | «Con agregarlo una vez basta». Cada cambio nuevo se vuelve a agregar antes del commit. |
| Rama | Una línea de trabajo aparte para probar un cambio sin tocar main. | «Es una carpeta o una copia del proyecto». Es un marcador que apunta a un commit. Al cambiar de rama los archivos cambian en pantalla, y eso es normal. |
| main | La rama principal, la versión que vale. | «Puedo trabajar directo ahí». Los cambios llegan a main solo por PR. |
| Remoto (`origin`) | La copia del repositorio que vive en GitHub. | «Lo local y lo remoto son lo mismo». Son dos copias. Se igualan con push y pull. |
| Push | Subir tus commits a GitHub. | «Ya quedó integrado». Subir no integra. Solo deja la rama en GitHub. |
| Pull | Traer a tu computadora los cambios que hay en GitHub. | Ver la fila de pull request. |
| Pull request (PR) | Una propuesta para llevar los cambios de una rama a main, que otra persona revisa y comenta. | «Pull request es descargar». Es pedir que alguien revise e integre tu cambio. |
| Merge | Integrar una rama en otra, normalmente tu rama en main. | «Si el botón está verde, ya está aprobado». El botón disponible no es una aprobación. |
| Conflicto | Cuando dos ramas cambiaron las mismas líneas y Git necesita que una persona elija. | «Rompí el proyecto, hay que volver a clonar». No se pierde nada. Se eligen las líneas y se sigue. |
| Clone | Copiar a tu computadora un repositorio que está en GitHub, con todo su historial. | Volver a clonar para «arreglar» un conflicto. Eso no resuelve nada y puede dejar trabajo atrás. |
| `.gitignore` | La lista de archivos que Git no debe guardar, como secretos o exportaciones pesadas. | «Si está en .gitignore, ya no está en el historial». Solo evita que entre desde ahora. Lo que ya entró sigue ahí. |
| Revert | Un commit nuevo que deshace otro sin borrar el historial. | Confundirlo con reset. Revert es la forma segura de deshacer algo ya subido. |
| Enlace de prueba (preview) | Una URL temporal donde ves la PR funcionando antes de integrarla, por ejemplo en Vercel. | «Es la página publicada». Producción cambia solo cuando main cambia. |

## Analogías que sí y que no

- Usa «una versión con nombre en Figma» para commit, aclarando que Git no guarda solo.
- Usa «un universo paralelo» para rama, aclarando que no es una copia de archivos.
- Evita «una carpeta» para rama y «Google Drive» para GitHub. Generan los errores de la tabla.
