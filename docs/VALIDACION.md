# Validación de Reply App

Fecha de ejecución: 3 de noviembre de 2026, zona America/Guayaquil.

## Compilación y análisis

Se completaron `:app:assembleDebug`, `:app:assembleDebugAndroidTest` y
`:app:lintDebug` con JDK 17 y las versiones originales de `nav-update`.
La última ejecución terminó con **BUILD SUCCESSFUL**. El registro íntegro se
conserva en `evidencias/resultados/compilacion-y-lint.txt`.

Lint no informó errores. Conserva advertencias del proyecto base, entre ellas
SDK objetivo antiguo, etiqueta redundante y recursos no utilizados. No se
actualizaron dependencias arbitrariamente para ocultar esas advertencias.

Android Studio completó la sincronización Gradle. Las tres vistas previas
Compose se renderizaron y el panel indicó **Up-to-date**, sin problemas de
renderización. Se corrigió la conversión del contexto de Preview a Activity
posponiéndola hasta ejecutar el callback de Atrás.

## Pruebas instrumentadas de la versión final

| Grupo | Ancho efectivo | Casos | Fallos | Registro |
|---|---|---|---|---|
| Compacto | 360 dp | 2 | 0 | `pruebas-compactas.txt` |
| Mediano | 700 dp | 1 | 0 | `pruebas-medianas.txt` |
| Expandido | 1280 dp | 2 | 0 | `pruebas-expandidas.txt` |

Los grupos finales se ejecutaron sobre el emulador Android 15 / API 35 con
densidad 320 dpi y superficies de 720×1600, 1400×2000 y 2560×1600 píxeles.
Se filtraron mediante `annotation` con el paquete `com.example.reply.test`.
Cada archivo termina con **OK**, el número correcto de casos y código de
instrumentación -1. `resumen.json` conserva las fechas de inicio y dimensiones.

Se repitieron además los dos casos expandidos desde Android Studio mediante
la configuración compartida `Pruebas expandidas`: **2 aprobados, 0 fallos**.
La captura `09-pruebas-android-studio.jpg` y el XML de resultados conservan
esa ejecución. Las configuraciones utilizan la opción `EXTRA_OPTIONS` del
formato generado por el propio IDE, verificada con esta ejecución real.

También se ejecutaron satisfactoriamente los dos casos compactos sobre el
teléfono Xiaomi 23100RN82L, Android 15, 720×1600 píxeles y 320 dpi. Su sistema
bloqueó el inicio de ComponentActivity en segundo plano; se abrió la actividad
de prueba mediante ADB y se completaron las comprobaciones sin modificar los
casos ni la configuración de seguridad del teléfono. Ese primer registro se
conserva como `pruebas-telefono-xiaomi.txt`.

## Pruebas manuales

- Teléfono: lista con barra inferior, apertura del tercer correo y regreso.
- Tablet vertical: 800 dp, riel lateral y detalle independiente.
- Tablet horizontal: 1280 dp, panel permanente, lista y detalle simultáneos.
- Ali: selección en vertical, rotación a horizontal y regreso conservando
  `Brunch this weekend?` y su contenido.
- Atrás: regresa a la lista en mediano y cierra la actividad en expandido.

El registro `rotacion-y-retroceso.txt` contiene las cinco comprobaciones de
la secuencia completa. Las rotaciones se controlaron desde el equipo para
obtener evidencias reproducibles y se dejó habilitada la rotación libre al
terminar. Las capturas PNG originales se conservan sin alterar.

## Alcance y diferencias justificadas

Se compararon los diez archivos centrales y los recursos con `main`.
La implementación conserva las dependencias y los iconos de `nav-update`;
no adopta los retrocesos de versión ni los cambios de datos del diff oficial.
El margen final integrado sigue el fragmento del codelab; `main` lo aplica
desde el padre. El callback de Atrás se evalúa al pulsarlo para permitir
Compose Preview y mantiene `activity.finish()` en ejecución.

No se probó un plegable físico ni un emulador plegable. La matriz cubre los
tres anchos mediante teléfono y tablet con superficies controladas. La
restauración simulada y la rotación no demuestran persistencia tras muerte
del proceso. Reply conserva los datos locales de ejemplo y no envía correo.

El informe utiliza una copia de `p.docx`; el original permanece intacto.
Las credenciales, archivos locales de configuración, respaldos, instaladores
y documentos con datos académicos se excluyen de la publicación.
