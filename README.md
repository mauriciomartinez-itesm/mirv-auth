# Componente Web de Inicio de Sesión de Google (Google Login)

Un componente web premium, personalizable y seguro para pantallas de inicio (splash screens) diseñado para experiencias del Tec de Monterrey. Este componente gestiona la autenticación, verificación de dominios, créditos dinámicos e integración con Google Analytics.

## Características

-   **Valores Predeterminados Sin Configuración**: Obtiene automáticamente recursos de alta calidad (logotipos, fondo) desde un servidor central si no se proporcionan.
-   **Seguridad**: Verificación integrada para dominios `@tec.mx`, `@itesm.mx`, `@tecmilenio.mx` y `@tecsalud.mx`.
-   **Estética**: Diseño elegante con glassmorphism, transiciones suaves y animaciones premium.
-   **Créditos Interactivos**: Modal animado para créditos del proyecto cargados desde un archivo JSON sencillo.
-   **Barra de Perfil de Usuario**: Una barra superior oculta y desplegable (hover) que muestra la información del usuario y permite cerrar sesión.
-   **Auto-Login**: Recuerda sesiones y omite la pantalla de inicio automáticamente al regresar.
-   **Integración GA4**: Seguimiento de eventos integrado para inicios de sesión, errores y vistas de página.

## Instalación

Simplemente incluya el script del componente en el `<head>` de su HTML:

```html
<script src="https://mirv.tec.mx/common/google-login-component.js"></script>
```

## Uso Básico

```html
<google-login experience-name="Mi Experiencia VR"></google-login>
```

## Atributos

| Atributo | Descripción | Por Defecto |
| :--- | :--- | :--- |
| `experience-name` | Título de la experiencia que se muestra en la pantalla de inicio. | Vacío |
| `assets-base-url` | URL base para buscar imágenes/JSON predeterminados. | `https://mirv.tec.mx/common/` |
| `background-image`| Ruta absoluta o relativa a la imagen de fondo. | `{assets-base-url}/bgImg.png` |
| `top-logo` | Ruta al logotipo principal en la parte superior. | `{assets-base-url}/logo_largo_blanco.png` |
| `bottom-logo` | Ruta al logotipo de soporte/secundario en la parte inferior. | `{assets-base-url}/MIRV_2020b.png` |
| `credits-url` | Ruta al archivo `credits.json`. Use `""` para desactivar. | `{assets-base-url}/credits.json` |
| `allowed-domains` | Lista separada por comas de dominios de correo válidos. | `@tec.mx, @itesm.mx, @tecmilenio.mx, @tecsalud.mx` |
| `footer-text` | Texto de pie de página personalizado. Use `{currentyear}` para el año automático. | Pie de página estándar ITESM |
| `ga-id` | ID de medición de Google Analytics 4. | `G-M7B2GZZ8BX` |
| `on-success` | Nombre de una función global a llamar tras el login exitoso. | Vacío |
| `debug` | Atributo booleano para habilitar el tráfico de depuración de GA4. | False |

## Manejo de Eventos

Puede escuchar el evento `login-success` o especificar un callback global:

### Método 1: Callback por Atributo
```javascript
function alTerminarLogin(detail) {
    console.log("Usuario ingresó:", detail.user.name);
}
```
```html
<google-login on-success="alTerminarLogin"></google-login>
```

### Método 2: Event Listener
```javascript
document.querySelector('google-login').addEventListener('login-success', (e) => {
    const { user, credential } = e.detail;
    // user contiene: name, email, picture, etc.
});
```

## Formato de JSON para Créditos
El `credits-url` debe apuntar a un archivo JSON con la siguiente estructura:

```json
[
  {
    "role": "Dirección",
    "names": ["Nombre Apellido"]
  },
  {
    "role": "Desarrollo",
    "names": ["Dev 1", "Dev 2"]
  }
]
```

## Personalización de Recursos por Defecto
Si desea usar su propio servidor para todos los recursos predeterminados (manteniendo los nombres de archivo como `bgImg.png`), simplemente configure la URL base:

```html
<google-login assets-base-url="./mis-assets/"></google-login>
```
