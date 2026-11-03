# Historial cronológico de Reply App

Se conservan las fechas reales y los commits incrementales. Cada entrada incluye la etapa y los cambios descritos en el mensaje original.

## 4d49b8326afcf31e4d9491ff1b5cc183b85e2bea

chore: preparar proyecto Reply App desde la rama nav-update

Se incorpora la base oficial nav-update aab5b01d64cd8fca8689250d7a780be88bd1c394 en la carpeta requerida. Se conservan los avisos Apache 2.0, el código Compose y los recursos originales. La plantilla vacía anterior queda respaldada localmente en .codex-local y excluida de Git.

## a0b2bc63e3b9fb005627e643db5434c07eaaa1c9

feat: incorporar vistas previas Compose para pantallas medianas y expandidas

Se añaden ReplyAppMediumPreview y ReplyAppExpandedPreview con widthDp de 700 y 1000 y las clases Medium y Expanded. Ambas reutilizan ReplyTheme, Surface y ReplyApp. Se conserva la vista compacta y el diseño original en este checkpoint.

## 14e4169e6a95a9377046621a500efe943d51f2df

feat: definir tipos de contenido adaptable según el ancho de pantalla

ReplyContentType diferencia LIST_ONLY y LIST_AND_DETAIL. Compact, Medium y el caso alternativo mantienen solo lista; Expanded utiliza lista y detalles. La clasificación de contenido conserva las asignaciones originales de ReplyNavigationType.

## 60d9a43b99c40ac40886935bf304dfa1043048d3

refactor: propagar ReplyContentType entre los componentes principales de Compose

Se transmite contentType desde ReplyApp a ReplyHomeScreen y a las dos invocaciones de ReplyAppContent. Se conservan ReplyUiState, los eventos de selección y los callbacks del ViewModel.

## f2654c43df5cec2c2c9d0a3085ceadf87db7f360

feat: implementar diseño adaptable de lista y detalles para pantallas expandidas

ReplyAppContent selecciona ReplyListAndDetailContent para LIST_AND_DETAIL y ReplyListOnlyContent para LIST_ONLY, reutilizando los componentes y dimensiones existentes. El panel permanente deja de depender de isShowingHomepage para permanecer visible al seleccionar un correo.

## 0ea3a047ed728fa368a0c79692366ecd1914bd72

refactor: adaptar pantalla de detalles para vistas independientes y de dos paneles

isFullScreen distingue el detalle independiente del panel integrado. La barra superior solo aparece a pantalla completa; el asunto se presenta dentro de la tarjeta integrada y se sustituyen los encabezados duplicados por el espaciado definido en recursos. Se conserva el padding horizontal o final según el modo.

## 60a4daa56c729e655a6c7a411aaf715180566b7a

fix: ajustar comportamiento del botón Atrás en diseño expandido

El detalle integrado llama activity.finish() mediante LocalContext, como establece el codelab. Los detalles independientes conservan el callback que regresa a la lista.

## d48723a071b54969141224731240a6e2e33f3060

test: implementar pruebas Compose para navegación compacta mediana y expandida

Se utiliza createAndroidComposeRule<ComponentActivity>() para comprobar la barra inferior, el riel y el panel permanente mediante onNodeWithTagForStringId y assertExists. Se agrega testTag a la barra inferior y se reutilizan las etiquetas y cadenas ya presentes en nav-update para el riel y el panel.

## 277062c241e49a23413f518574cf97161c16188d

test: verificar conservación del correo en pantallas compactas

StateRestorationTester abre el tercer correo de LocalEmailsDataProvider, comprueba el botón Atrás y el cuerpo del mensaje y simula la restauración de instancia. Las mismas comprobaciones se repiten después del cambio de configuración.

## c8fe1370ca79a0e18167a07ebfdebb2da17361ee

test: verificar conservación del correo en pantallas expandidas

Se agrega la prueba Expanded y la etiqueta details_screen al panel de detalles. onChildren, assertAny y hasAnyDescendant restringen la comprobación al panel para no confundir el contenido del mensaje con su vista previa en la lista.

## f972219195ea8110fa4d6cb081071f047831b102

test: organizar pruebas instrumentadas mediante anotaciones por tamaño de pantalla

Se crean TestCompactWidth, TestMediumWidth y TestExpandedWidth y se aplican a las cinco pruebas. Se guardan tres configuraciones compartidas de Android Studio con el argumento annotation y el paquete real com.example.reply.test para ejecutar cada grupo por separado.

## 0b3be05a5c38ad8b4bf7fc862c663d51561e543e

test: aplicar anotaciones y guardar configuraciones de ejecución por tamaño

Se completa la clasificación de las cinco pruebas y se agregan las tres configuraciones compartidas de Android Studio. El commit anterior incorporó las definiciones de las anotaciones; esta etapa incorpora su aplicación y las opciones de ejecución.

## 98819a24e4f9869d4582c45940a089cd661a92d2

chore: normalizar finales de línea para revisar cambios entre plataformas

Se configura .gitattributes y se normalizan los archivos de texto importados desde nav-update. Esta modificación facilita revisar los diffs de Kotlin y XML en Windows sin cambiar el comportamiento de la aplicación.

## a4c26a37bb492497495a953d6825a29d5516dbbf

chore: identificar la aplicación y el proyecto como Reply App

Se establece Reply App como nombre visible y Reply_App como nombre del proyecto. Se conserva el namespace y applicationId com.example.reply de la base oficial sin modificar el diseño ni los recursos funcionales.

## 966082e451b00806a90acb722af74146a021d354

fix: respetar los márgenes seguros en la lista de correos

La comparación visual en el teléfono mostró el perfil superpuesto con la barra de estado. Se incorpora contentPadding con WindowInsets.safeDrawing en ReplyListOnlyContent, tal como contempla la rama main oficial, para conservar legibles el encabezado y la lista en dispositivos con barras de sistema.

## 9e1af84f8160072e52266590ff670c76c2680e18

fix: permitir la vista previa expandida conservando el cierre con Atrás

Android Studio confirmó que el contexto de Compose Preview no puede convertirse en Activity durante la composición. Se obtiene LocalContext al componer y se realiza la conversión únicamente dentro del callback de Atrás. La ejecución conserva activity.finish(), sin cambiar navegación ni agregar componentes.
