# Análisis del codelab y secuencia de implementación

Fuente principal: [codelab oficial en español](https://developer.android.com/codelabs/basic-android-kotlin-compose-adaptive-content-for-large-screens?hl=es-419), consultado el 3 de noviembre de 2026.

## Los siete apartados

| Apartado | Objetivo e instrucciones | Archivos y comprobación |
|---|---|---|
| 1. Introducción | Continuar la navegación adaptable previa. Seleccionar `nav-update` e identificar lista y detalles. | Proyecto, recursos, Gradle, paquete y estado inicial de Git. |
| 2. Vistas previas | Conservar Compact; añadir `ReplyAppMediumPreview` y `ReplyAppExpandedPreview` con `showBackground = true`, `widthDp` 700 y 1000 y clases Medium y Expanded. | `MainActivity.kt`, `ReplyTheme`, `Surface`, `ReplyApp`. Compilar y revisar las presentaciones. |
| 3. Contenido adaptable | Crear y propagar `ReplyContentType`; elegir lista o dos paneles; conservar el panel permanente; adaptar detalles con `isFullScreen`; cerrar con Atrás en Expanded. | `WindowStateUtils.kt`, `ReplyApp.kt`, `ReplyHomeScreen.kt`, `ReplyDetailsScreen.kt`, `ReplyHomeContent.kt`. Commits separados para tipos, propagación, paneles, detalles y retroceso. |
| 4. Verificación manual | Activar rotación, recorrer la lista, seleccionar Ali, pasar a horizontal y regresar manteniendo el correo. | Teléfono y tablet virtual; capturas y registro de rotación y Atrás. |
| 5. Pruebas automatizadas | Tres pruebas de navegación, dos de restauración y tres anotaciones por ancho. Usar actividad vacía, recursos de etiquetas y `annotation`. | `ReplyAppTest.kt`, `ReplyAppStateRestorationTest.kt`, `TestAnnotations.kt`, `.run/`. Grupos de 2, 1 y 2 pruebas. |
| 6. Solución | Consultar `main` y comparar firmas, recursos, modificadores y pruebas. | Se revisó el diff oficial sin sustituir el proyecto con la solución terminada. |
| 7. Conclusión | Comprobar adaptación, vistas previas y pruebas por tamaño. | Documentar resultados observados y límites de las verificaciones. |

## Secuencia de contenido

1. `ReplyContentType` es la única enumeración nueva de producción. Define `LIST_ONLY` y `LIST_AND_DETAIL`.
2. Compact, Medium y el caso alternativo asignan `LIST_ONLY`; Expanded asigna `LIST_AND_DETAIL`. Las asignaciones de navegación permanecen independientes.
3. `ReplyHomeScreen` y `ReplyAppContent` reciben `contentType`; ambas invocaciones del contenido lo transmiten. Se conservan `ReplyUiState`, `Email`, `MailboxType`, `NavigationItemContent` y los eventos del ViewModel.
4. La condición reutiliza `ReplyListOnlyContent` y `ReplyListAndDetailContent`, ya presentes en la base. Se conservan pesos, dimensiones y selección del correo.
5. El panel permanente deja de depender de `isShowingHomepage`; permanece visible al seleccionar un correo.
6. `ReplyDetailsScreen` y `ReplyEmailDetailsCard` reciben `isFullScreen: Boolean = false`. La barra superior solo se muestra en detalles independientes. El asunto se presenta en la tarjeta integrada; el modo completo usa el separador de `detail_content_padding_top`.
7. Se reutilizan `detail_card_outer_padding_horizontal`, `detail_card_inner_padding` y `detail_expanded_subject_body_spacing`. La vista integrada utiliza margen final conforme al codelab.
8. El detalle independiente pasa `isFullScreen = true`. El integrado utiliza `LocalContext.current as Activity` y `onBackPressed = { activity.finish() }`.

## Pruebas y recursos

Las cadenas `navigation_bottom`, `navigation_rail`, `navigation_drawer` y
`details_screen` ya existían en `nav-update`. Se añadieron las etiquetas
inferior y de detalles faltantes. Se reutilizaron las extensiones de
`ComposeTestRuleExtensions.kt`.

La restauración selecciona `LocalEmailsDataProvider.allEmails[2]`, comprueba
su cuerpo y simula la restauración de instancia. En Expanded, `onChildren`,
`assertAny`, `hasAnyDescendant` y `hasText` buscan dentro del panel etiquetado
para no aceptar por error el texto de la lista.

## Comparación oficial

Base: `aab5b01d64cd8fca8689250d7a780be88bd1c394` (`nav-update`).
Referencia: `5bca5ac04caf35ff30c39b07c92fb0f9386fe658` (`main`).

El diff oficial incluye cambios de versiones, iconos, formato y datos ajenos
al recorrido funcional. Se conservaron las versiones de la base, los iconos
AutoMirrored y los datos. Se tomó de `main` el margen seguro de la lista al
observar una superposición con la barra de estado del teléfono. El margen
final del detalle integrado sigue el codelab; `main` distribuye ese margen
desde el padre.

No se añadieron pantallas, persistencia, servicios ni arquitecturas.
La restauración simulada y la rotación no prueban recuperación tras muerte del proceso.

En Android Studio se detectó que el cast inmediato de `LocalContext.current`
a `Activity`, presente en el ejemplo, impide renderizar Expanded en Compose
Preview. Se conserva el contexto durante la composición y se convierte a
`Activity` únicamente al ejecutar Atrás, manteniendo `activity.finish()` y
el mismo comportamiento en ejecución. No se añaden librerías ni componentes.
