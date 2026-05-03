[Copilot chat context](https://code.visualstudio.com/docs/copilot/copilot-chat-context#_chat-context-types)
### Chat Context
* VSCode agrega de forma directa el editor activo como contexto para construir la respuesta, en caso de solo requerir el contexto de una porción de código, se pude seleccionar el mismo unicamente.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/copilot-chat-view-selection-context.png)

Se pueden seleccionar distintos tipos de contexto, algunos predefinidos del `workspace` como la base de código en general, una sección de la terminal, o archivos y carpetas.
* Se puede usar el caracter `#`  en el prompt para hacer referencia a variables que involucran contexto por medio de `intelliSense`.
* Se pueden arrastrar los archivos o carpetas para mayor fluidez.

![[Pasted image 20250318145606.png]]

En caso de no conocer los archivos relevantes como recursos para la respuesta, se puede usar `#codebase` para que Copilot por si mismo busque los archivos que pueden ser relevantes para el contexto de la pregunta. -> Verificar que `github.copilot.chat.codesearch.enabled` este activo.

**Contexto para hacer Bug Fixing**
* Arrastrar y soltar el problema desde el `Problem Panel` 
* Seleccionar el problema desde los tipos de contexto (`#`).
* Seleccionar el contexto de `#terminalLastCommand` para entregar la respuesta al ultimo comando ejecutado en la terminal.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/copilot-chat-attach-problem.png)

**Tipos de Contexto de Chat**
- Files - include specific files from your workspace in the prompt
- Folders - add a folder to include the files in that folder in the prompt
- Symbols - add a symbol from your workspace to the prompt
- Codebase - let Copilot find the right files automatically
- Editor or terminal selection - include a selection of text from the editor or terminal in the prompt
- Terminal command output - include the output of the last command run in the terminal
- Problems - include a specific code issue from the Problems panel to the prompt
- Test failures - include details from test failures in the prompt