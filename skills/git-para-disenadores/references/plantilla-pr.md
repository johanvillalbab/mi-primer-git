# Plantilla de pull request

Título con «qué cambió», corto y en el idioma de la persona. Por ejemplo «Cambia el botón principal a verde».

Cuerpo, para `gh pr create --base main --title "<título>" --body-file <archivo>`:

```markdown
## Problema
<Qué no funcionaba o qué se quería lograr, en una o dos frases.>

## Qué cambió
- <Cambio concreto 1>
- <Cambio concreto 2>

## Por qué
<La razón de diseño o de producto detrás del cambio.>

## Cómo se comprobó
- <Qué se abrió o probó y qué se vio. Por ejemplo, «abrí index.html y el botón se ve verde en móvil y escritorio».>

## Capturas o Figma
| Antes | Después |
|---|---|
| <captura> | <captura> |

Figma: <enlace, si aplica>

## Enlace de prueba
<Enlace de Vercel u otro, si existe. Si no, borra esta sección.>

## Qué revisar
<Dónde mirar con más cuidado, o qué decisión necesita la persona que revisa.>
```

Reglas:

- Borra las secciones que no aplican en lugar de dejarlas vacías.
- Si falta algo para que esté lista, abre con `--draft` y anota qué falta en «Qué revisar».
- Si el equipo nombra a quien revisa, agrega `--reviewer <usuario>`.
- Escribe el cuerpo en un archivo temporal fuera del repo y pásalo con `--body-file`, así no se rompen las comillas ni entra al commit.
