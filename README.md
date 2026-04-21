# Google Login & Splash Screen Component (MIRV Tec)

Un componente web premium, altamente personalizable y seguro para pantallas de inicio (splash screens) diseñado para experiencias del Tec de Monterrey. Este componente no solo gestiona la autenticación de Google, sino que también proporciona una interfaz completa de ayuda, créditos, valoración de la experiencia y herramientas de autoría.

## ✨ Características Principales

-   **Autenticación Segura**: Integración con Google Identity Services (GSI) con verificación automática de dominios institucionales (`@tec.mx`, `@itesm.mx`, etc.).
-   **Sistema de Ayuda Dinámico**: Modal de instrucciones con soporte multi-idioma (ES/EN), diferentes layouts (horizontal, vertical, tipo personaje) y soporte para Markdown.
-   **Barra de Usuario Inteligente**: Barra superior desplegable (hover) que incluye:
    -   Información del usuario.
    -   Acceso rápido a Ayuda y Créditos.
    -   **Impresión a PDF**: Genera un documento de la pantalla actual con una marca de agua del usuario autenticado (ideal para evidencias).
    -   Cierre de sesión.
-   **Sistema de Valoración**: Recopilación de feedback mediante estrellas e integración opcional con Qualtrics.
-   **Modo Debug**: Atributo para saltar el login durante el desarrollo.
-   **Herramientas de Autoría**: Incluye dos herramientas visuales para generar el contenido sin escribir JSON a mano:
    -   **Instruction Maker**: Generador de archivos de ayuda con vista previa en tiempo real.
    -   **Credits Maker**: Generador de archivos de créditos.

## 🚀 Instalación

Incluya el script del componente en el `<head>` de su HTML:

```html
<script src="https://mirv.tec.mx/common/google-login-component.js"></script>
```

## 🛠️ Uso Básico

```html
<google-login 
  experience-name="Simulador de Logística VR"
  experience-instructions="./json/experience.json">
</google-login>
```

## 📋 Atributos

| Atributo | Descripción | Por Defecto |
| :--- | :--- | :--- |
| `experience-name` | Título principal de la experiencia. | Vacío |
| `experience-type` | Tipo de navegación (`static`, `orbit`, `firstperson`). Carga instrucciones base. | `static` |
| `experience-instructions`| Ruta al archivo JSON de instrucciones de la experiencia. | Vacío |
| `experience-answers` | Ruta al archivo JSON de respuestas/ayuda adicional. | Vacío |
| `assets-base-url` | URL base para buscar recursos predeterminados. | `https://mirv.tec.mx/common/` |
| `credits-url` | Ruta al archivo `credits.json`. | `{assets-base-url}/json/credits.json` |
| `background-image`| Imagen de fondo de la pantalla de inicio. | `{assets-base-url}/media/background.png` |
| `ga-id` | ID de Google Analytics 4. | `G-M7B2GZZ8BX` |
| `qualtrics-url` | URL de encuesta para el sistema de feedback. | Vacío |
| `debug-mode` | Si está presente, salta el login con un usuario de prueba. | False |
| `on-success` | Función global a llamar tras el login. | Vacío |

## 📖 Sistema de Ayuda e Instrucciones

El componente gestiona tres tipos de contenido de ayuda en el modal:
1.  **General**: Instrucciones comunes (cómo navegar, qué es la plataforma). Se cargan automáticamente desde el servidor central.
2.  **Esta Experiencia**: Contenido específico definido en `experience-instructions`.
3.  **Respuestas**: Sección opcional para FAQs o guías de resolución definida en `experience-answers`.

### Formato de JSON de Instrucciones
Se recomienda usar el **Instruction Maker** incluido en el repositorio para generar este archivo. El formato admite layouts como `vertical`, `horizontal`, `character` (estilo burbuja de diálogo) y `text-only`.

## 🛠️ Herramientas de Autoría

Para facilitar la creación de contenido, el repositorio incluye:

1.  **Instruction Maker** (`/instruction-maker`): 
    -   Arrastra y suelta imágenes.
    -   Vista previa idéntica a cómo se verá en el componente.
    -   Exporta un ZIP listo para usar en tu proyecto.
2.  **Credits Maker** (`/credits-maker`): 
    -   Gestiona roles y nombres para los créditos finales de forma visual.

## 🧪 Desarrollo y Pruebas

Para probar localmente sin tener que autenticarse cada vez, use el atributo `debug-mode`:

```html
<google-login debug-mode experience-name="Test Mode"></google-login>
```

## 📊 Manejo de Eventos

Escuche el evento `login-success` para obtener los datos del usuario:

```javascript
document.querySelector('google-login').addEventListener('login-success', (e) => {
    const { user } = e.detail;
    console.log(`Bienvenido, ${user.name} (${user.email})`);
});
```

---
*D.R. Instituto Tecnológico y de Estudios Superiores de Monterrey, México.*

