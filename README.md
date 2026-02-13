# Git y GitHub: Pull Requests

Este documento responde a preguntas clave sobre el uso de Pull Requests en GitHub.

## a. ¿Qué es un pull request en GitHub?

Un **Pull Request (PR)**, o solicitud de extracción, es una funcionalidad central de GitHub que permite informar a otros desarrolladores sobre los cambios que se han realizado en una rama (branch) de un repositorio. Es el mecanismo mediante el cual se proponen cambios para ser revisados y posteriormente fusionados (merged) en una rama base (comúnmente `main` o `master`).

El Pull Request facilita la colaboración:
*   Muestra las diferencias (diffs) del código.
*   Permite la discusión y revisión del código línea por línea.
*   Sirve como punto de control de calidad antes de integrar nuevo código al proyecto.

## b. ¿Cómo se crea un pull request en GitHub?

1.  **Subir cambios**: Realiza `commit` y `push` de tus cambios a una rama en tu repositorio de GitHub.
2.  **Navegar al repositorio**: Ve a la página principal del repositorio en GitHub.
3.  **Iniciar PR**:
    *   Frecuentemente verás un aviso de "Compare & pull request" si acabas de hacer push.
    *   Si no, ve a la pestaña **"Pull requests"** y haz clic en el botón verde **"New pull request"**.
4.  **Seleccionar ramas**: En la lista desplegable "base", selecciona la rama donde quieres fusionar los cambios. En "compare", selecciona la rama con tus cambios.
5.  **Detallar**: Escribe un título claro y una descripción de los cambios.
6.  **Crear**: Haz clic en **"Create pull request"**.

## c. ¿Cómo se aprueba un pull request en GitHub?

1.  **Acceder al PR**: En la pestaña **"Pull requests"**, selecciona el PR que deseas revisar.
2.  **Revisar archivos**: Ve a la pestaña **"Files changed"** para ver las diferencias en el código.
3.  **Evaluar**: Puedes dejar comentarios en líneas específicas si es necesario.
4.  **Emitir revisión**:
    *   Haz clic en el botón **"Review changes"** en la esquina superior derecha.
    *   Escribe un resumen de tu revisión.
    *   Selecciona **"Approve"** (Aprobar) para dar el visto bueno a la fusión.
    *   Haz clic en **"Submit review"**.

## d. Bibliografía

GitHub. (s.f.). *About pull requests*. GitHub Docs. Recuperado el 13 de febrero de 2026, de https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests

GitHub. (s.f.). *Creating a pull request*. GitHub Docs. Recuperado el 13 de febrero de 2026, de https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

GitHub. (s.f.). *Approving a pull request with required reviews*. GitHub Docs. Recuperado el 13 de febrero de 2026, de https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/approving-a-pull-request-with-required-reviews
