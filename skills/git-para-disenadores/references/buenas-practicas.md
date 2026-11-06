# Buenas prácticas para repos colaborativos

Texto literal de Sho (Interface School) para el taller «Git y GitHub para Diseñadores», 5 de noviembre de 2026. Cítalo tal cual cuando expliques una regla a la persona o redactes su `CONTRIBUTING.md`.

## Para quienes colaboran

1. **Acordar el objetivo antes de editar.** Dejar escrito qué problema se resuelve, qué queda fuera y cómo comprobar el resultado. Puede ser en una tarea de GitHub (*issue*) enlazada al cambio.
2. **Crear una rama por cambio coherente.** Por ejemplo, `ajustar-contraste-alertas`. No una por archivo, ni una sola para mezclar trabajos independientes.
3. **Proponer cambios pequeños y enfocados.** Un pull request (PR, propuesta de cambio) debería tener un propósito claro. No mezclar corregir un color con reorganizar todo el proyecto.
4. **Escribir commits que expliquen el cambio.** Un commit es un cambio guardado en el historial. Mejor «Mejora el contraste del texto de error» que «cambios finales». Un PR puede contener varios commits.
5. **Preparar el PR para quien lo revisa.** Explicar el problema, qué cambió, por qué y qué se comprobó. En diseño, añadir capturas antes/después y el enlace de Figma cuando ayuden. Revisar primero los propios cambios; si están incompletos, marcar el PR como borrador.
6. **Revisar con comentarios concretos.** Explicar el problema y su efecto, distinguir lo que impide aprobar de una sugerencia opcional y pedir contexto si algo no se entiende. «Se ve bien» no sustituye una revisión.
7. **Integrar después de la revisión acordada.** Que el botón de *merge* (integrar el cambio) esté disponible no significa que ya esté aprobado. El autor puede integrarlo después de la aprobación si las reglas del equipo lo permiten.
8. **Resolver conflictos conversando.** Si dos cambios se cruzan, coordinar qué resultado conservar; no elegir automáticamente «mi versión». Si no se entiende el archivo, pedir apoyo técnico y comprobar de nuevo el resultado.
9. **No subir información sensible.** Tampoco en capturas o comentarios. Borrar una contraseña del archivo no la elimina del historial: si se expone, hay que avisar y revocarla o reemplazarla.

## Para quien es dueño del repositorio

1. **Documentar cómo empezar.** Mantener un `README` que explique para qué sirve el proyecto, cómo usarlo y a quién pedir ayuda. Otra persona debería poder orientarse sin depender de una llamada contigo.
2. **Dejar claras las reglas para contribuir.** En `CONTRIBUTING.md`, explicar cómo proponer cambios, nombrar ramas, comprobar el resultado y pedir revisión. Una plantilla de pull request (PR, propuesta de cambio) ayuda a recoger objetivo, capturas y comprobaciones sin repetir instrucciones.
3. **Dar únicamente los permisos necesarios.** No todas las personas necesitan administrar el repositorio. Revisar los accesos y retirarlos cuando alguien deja el equipo o termina su colaboración.
4. **Proteger la rama principal.** Configurar protección de ramas o conjuntos de reglas para exigir propuestas de cambio, revisiones y comprobaciones antes de integrar. Evitar que alguien pueda borrar o sobrescribir el historial compartido accidentalmente. Las opciones disponibles dependen del plan y del tipo de repositorio.
5. **Aplicarse las mismas reglas.** Que seas el dueño no significa que debas saltarte la revisión. Las excepciones urgentes deben tener una razón y quedar documentadas.
6. **Definir quién revisa y quién integra.** Cada propuesta necesita una persona responsable de revisarla. En equipos más grandes, `CODEOWNERS` permite señalar responsables por archivos o carpetas; las aprobaciones obligatorias deben configurarse además en las reglas del repositorio.
7. **Atender las contribuciones.** Dar contexto cuando pides cambios o rechazas una propuesta. Si no puedes revisarla todavía, decirlo y acordar cuándo retomarla. Evitar que las propuestas queden abiertas indefinidamente sin respuesta.
8. **Configurar controles proporcionales al proyecto.** Por ejemplo, comprobar enlaces, validar archivos de estilos o ejecutar pruebas antes de integrar. La automatización debe detectar problemas reales; no añadir requisitos que nadie entiende ni mantiene.
9. **Cuidar la seguridad y la confidencialidad.** Definir qué puede publicarse, activar las protecciones disponibles contra credenciales expuestas y establecer cómo reportar un incidente. Un repositorio privado también necesita controles de acceso.
10. **Mantener el repositorio ordenado.** Actualizar instrucciones, cerrar tareas resueltas y eliminar ramas terminadas cuando ya no se necesiten. Si el proyecto deja de mantenerse, indicarlo y considerar archivarlo.
