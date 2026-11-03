# Reply App

Práctica de Kotlin y Jetpack Compose basada en el codelab oficial de Google
[Compila una app con un diseño adaptable](https://developer.android.com/codelabs/basic-android-kotlin-compose-adaptive-content-for-large-screens?hl=es-419).

## Procedencia

Base: `nav-update`, commit `aab5b01d64cd8fca8689250d7a780be88bd1c394`, del
[repositorio oficial](https://github.com/google-developer-training/basic-android-kotlin-compose-training-reply-app).
La rama `main`, commit `5bca5ac04caf35ff30c39b07c92fb0f9386fe658`, se consultó como referencia.
Se conservan la licencia Apache 2.0, los avisos de autoría y los recursos originales.

## Contenido adaptable

| Ancho | Navegación | Contenido |
|---|---|---|
| Compacto | Barra inferior | Lista o detalle independiente |
| Mediano | Riel | Lista o detalle independiente |
| Expandido | Panel permanente | Lista y detalle simultáneos |

`ReplyContentType` clasifica el contenido independientemente de `ReplyNavigationType`.
`isFullScreen` controla el encabezado, el asunto y los espaciados del detalle.
Atrás regresa a la lista en detalles independientes y cierra la actividad en Expanded.
Las vistas previas compacta, mediana de 700 dp y expandida de 1000 dp están en
`MainActivity.kt`. Se conserva el paquete y applicationId `com.example.reply`.

## Abrir y compilar

Abrir la carpeta raíz en Android Studio y seleccionar **JDK 17** para Gradle.
Se mantienen las versiones de `nav-update`: Gradle 8.4, AGP 8.3.1, Kotlin 1.9.22,
compilador Compose 1.5.10, BOM Compose 2024.03.00, SDK de compilación y objetivo 34
y SDK mínimo 24. Instalar Android SDK 34 y Build Tools 34.0.0.

```powershell
.\gradlew.bat :app:assembleDebug :app:assembleDebugAndroidTest :app:lintDebug
```

`local.properties`, los SDK, ajustes personales, cachés e instaladores se excluyen de Git.
La plantilla Android vacía anterior se conserva en un respaldo local excluido.

## Pruebas

Cinco pruebas instrumentadas usan `createAndroidComposeRule<ComponentActivity>()`:
tres verifican navegación y dos verifican el correo seleccionado antes y después
de `StateRestorationTester.emulateSavedInstanceStateRestore()`.

Las tres configuraciones compartidas de `.run/` filtran el paquete
`com.example.reply.test` mediante `annotation` y las anotaciones
`TestCompactWidth`, `TestMediumWidth` o `TestExpandedWidth`. Seleccionar el
dispositivo del tamaño correspondiente para cada configuración.

Los registros originales están en [`evidencias/resultados`](evidencias/resultados).
Las capturas PNG proceden del teléfono, emulador e IDE, sin imágenes del tutorial.
Consultar la matriz de resultados y limitaciones en [`docs/VALIDACION.md`](docs/VALIDACION.md).

## Documentación

- [Análisis del codelab y archivos](docs/ANALISIS_CODELAB.md).
- [Validaciones y comparación con la solución](docs/VALIDACION.md).
- [Historial cronológico con hashes y descripciones](docs/HISTORIAL.md).

El informe se entrega localmente en
`entregables/Informe_Reply_App_Diseno_Adaptable.docx`, elaborado sobre una copia de
`p.docx`. La plantilla y el informe con datos académicos se mantienen fuera de Git.
El repositorio se publica con visibilidad **privada**.
