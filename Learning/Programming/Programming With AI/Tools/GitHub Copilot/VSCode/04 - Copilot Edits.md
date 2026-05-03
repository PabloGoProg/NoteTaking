Útil para la edición de multiples archivos con lenguaje natural - Copilot realiza los cambios sobre el editor activo, donde se tiene el contexto de la base de código del proyecto utilizado.

Existen dos modos:
* _Modo de Edición:_ Needs to select the files to be edited, provide the context and prompt - Copilot sugiere las ediciones.
* _Modo de Agente:_ Copilot se encarga de planear las tareas y archivos relevantes a usar para completar una petición - _No funciona de forma adecuada con Python Notebooks_.

### Edit Mode

**Cómo utilizarlo?**
1. Abrir Copilot Edits con: `Ctrl+Shift+Alt+I`
2. Seleccionar la opción de edit:
		![](https://code.visualstudio.com/assets/docs/copilot/copilot-edits/copilot-edits-edit-mode.png)
3. Añadir los archivos, carpetas o ventanas del editor como contexto para Copilot.
	1. Copilot automáticamente añade el editor actual como contexto usando `chat.implicitContext.enabled`
	2. Copilot sugiere la adición de archivos adicionales basado en el historial de GitHub, usando la configuración `github.copilot.chat.edits.suggestRelatedFilesFromGitHistory`
4. Realizar el prompt.
5. Revisar y aceptar o rechazar los cambios.
6. Iterar.

### Modo Agente
Este modo aun se encuentra en [VS Code Insiders](https://code.visualstudio.com/insiders), lo que implica que sigue en la búsqueda de una versión estable para su uso.

**Cómo utilizarlo?**
1. Abrir Copilot Edits con: `Ctrl+Shift+Alt+I`
2. Seleccionar la opción de agente:
		![](https://code.visualstudio.com/assets/docs/copilot/copilot-edits/copilot-edits-agent-mode.png)
3. Hacer un prompt para solicitar los cambios en el código.
4. Revisar el código generado por el agente y aceptar o rechazar los cambios - Revisar y aceptar o rechazar los comandos de terminal (editarlos si es requerido).
	1. En caso de que el proyecto cuente con Tasks, el agente tratará de correr las tareas apropiadas asociadas al contexto. - Cambiar esta opción con: `github.copilot.chat.agent.runTasks`
5. Iterar

### Aceptar o Rechazar Cambios
Copilot da una lista e indica los archivos editados - Es necesario aceptar o rechazar la edición para hacer un nuevo prompt.
![](https://code.visualstudio.com/assets/docs/copilot/copilot-edits/copilot-edits-changed-files.png)

Para aceptar o rechazar los cambios y navegar entre los distintos archivos, se puede usar el menu dado por Copilot.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-edits/copilot-edits-file-review-controls.png)

### Interrumpir y Deshacer
* Se puede pausar o cancelar el proceso de un agente - cuando se pausa, se puede reanudar o escribir un nuevo prompt (lo cual cancela el prompt actual) - Si se cancela, aun así se pueden revisar los cambios generados hasta ese momento.
* Se puede revertir el último conjunto de cambios (último prompt) desde la parte superior de la ventana de cambios:

	![](https://code.visualstudio.com/assets/docs/copilot/copilot-edits/copilot-edits-undo-redo.png)
### Copilot Chat a Copilot Edits
En lugar de pasar uno a uno los bloques de código obtenidos en una conversación de Copilot chat, podemos seleccionar los bloques que deseemos pasar a nuestro proyecto, e integrarlos usando Copilot Edits.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-edits/copilot-chat-edit-with-copilot.png)

### Posibles Configuraciones

- `chat.editing.confirmEditRequestRemoval` - ask for confirmation before undoing an edit (default: `true`)
- `chat.editing.confirmEditRequestRetry` - ask for confirmation before performing a redo of the last edit (default: `true`)
- `chat.implicitContext.enabled` _(preview)_ - configure if the active editor should be automatically added as context to the chat prompt.
- `chat.editing.autoAcceptDelay` - configure a delay after which suggested edits are automatically accepted, use zero to disable auto-accept (default: 0)
- `github.copilot.chat.codesearch.enabled` _(preview)_ - let Copilot find the right files when you add `#codebase` to your prompt, similar to how agent mode works (default: `false`)
- `chat.agent.maxRequests` - maximum number of requests that Copilot Edits can make in agent mode (default: 5 for Copilot Free users, 15 for other users)
- `github.copilot.chat.edits.suggestRelatedFilesFromGitHistory` _(Experimental)_ - suggest related files from git history in Copilot Edits (default: `false`)
- `github.copilot.chat.agent.runTasks` - run workspace tasks when using agent mode in Copilot Edits (default: `true`)