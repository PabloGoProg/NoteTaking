Tres variantes de uso:
1. _Chat View:_ Abre al asistente a un lado `"Shift" + "Command | Control" + "I"`
2. _Inline Chat:_ Abre el chat en linea dentro del código `"Command | Control" + "I"` 
3. _Quick Chat:_ Pregunta corta de la que no se guarda memoria.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/copilot-chat-menu-command-center.png)

[**Prompt Exmaples**](https://docs.github.com/en/copilot/copilot-chat-cookbook)

* Copilot ofrece distintos LLM's entre los cuales elegir para maximizar los resultados obtenidos del trabajo realizado con el copiloto. Se puede realizar el cambio desde la configs de Copilot.
* Copilot usa el [[Chat Context]] dado para generar las mejores respuestas posibles.
### Chat Participants
Son expertos en su determinado campo, son invocados a traves de `@` seguido del nombre del participante requerido - SI bien existen muchos por defecto, se pueden agregar mas a traves de extensiones.

| Built-in participant | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `@workspace`         | Knows about the code in your workspace. Use it to navigate your code base, find relevant classes, files, and more.  <br>  <br>**Example prompts:**  <br><br>- `@workspace how are notifications scheduled?`<br>- `@workspace add form validation, similar to the newsletter page`                                                                                                                                                                                           |
| `@vscode`            | Knows about features, settings, and APIs of VS Code.  <br>  <br>**Example prompt:**  <br><br>- `@vscode the name of that thing when vscode fake opens a file? And how to disable it?`                                                                                                                                                                                                                                                                                       |
| `@terminal`          | Knows about the integrated terminal shell and its contents.  <br>  <br>**Example prompts:**  <br><br>- `@terminal how to undo the last commit`<br>- `@terminal help with #terminalLastCommand`                                                                                                                                                                                                                                                                              |
| `@github`            | Knows about and has skills for GitHub repositories issues, PRs, and more. Can also perform web searches using the Bing API. Get more information about [using GitHub skills](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#using-github-skills-for-copilot).  <br>  <br>**Example prompts:**  <br><br>- `@github What are all of the open PRs assigned to me?`<br>- `@github #web what is the latest VS Code version` |
Se pueden instalar participantes adiciones desde [VSCode Workspace](https://marketplace.visualstudio.com/search?term=tag%3Achat-participant&target=VSCode&category=All%20categories&sortBy=Relevance) o [GitHub Workspace](https://github.com/marketplace)
- Los provenientes de VSCode son extensiones client side que tienen acceso a la API de la aplicación.
- Las provenientes de Github no corren localmente en la maquina del anfitrión y solicitan permiso al editor una vez son llamados (`@`) por primera vez.
### Slash Commands
Son un atajo para instrucciones especificas - usados para evitar escribir prompts complejos de forma repetida - se invocan usando `/` seguido de un comando - Algunos Chat Participants tienen sus propios comandos.

Ejemplo: `@workspace /new Express app with pug and typescript`
### Aplicar Bloques de Codigo Sugeridos por el Editor

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/copilot-chat-view-code-block-actions.png)

Con los bloques de código se puede:
1. Insertar el código en la posición del cursor.
2. Copiar.
3. Insertar el código en la terminal integrada.
4. Insertarlo en un nuevo archivo.
Si el trozo de código es un comando, puede ser directamente ejecutado en la terminal integrada.
### Historial de Chats
Se puede usar `"Command | Control" + "L"` - Se puede ver el historial de chats pasados en el boton de `Show Chats` desde Copilot Chat.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/copilot-chat-view-show-chats.png)

Se pueden eliminar prompts y sus respuestas desde el chat - Se puede exportar la conversación a JSON a con el comando `Chat: Export Chat...` en el _Command Palette_.
### Quick Chat
En caso de requerir hacer una pregunta aislada que no requiera un chat completo, se puede usar el chat rapido que proporciona Copilot con 
`"Command | Control" + "Shift" + "Alt | Option" + "L"`
O usando el icono de Copilot en la parte superior de la pantalla.

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/quick-chat-dropdown.png)

Si se necesita continuar con la conversacion, se puede a traves del siguiente boton:

![](https://code.visualstudio.com/assets/docs/copilot/copilot-chat/open-in-chat-view.png)

### Inline Terminal Chat
Similar al `Inline Chat` del Workspace, pero se realiza desde la terminal integrada del editor.

### Capacidades de Cada Chat
|Capability|Copilot Edits|Chat view|Inline Chat|Quick Chat|
|---|---|---|---|---|
|Receive code suggestions|✅|✅|✅|✅|
|Multi-file edits|✅|✅*||✅*|
|Preview code edits in editor|✅||✅||
|Code review flow|✅||||
|Roll back changes|✅||||
|Attach context|✅|✅|✅|✅|
|Use participants & commands||✅||✅|
|Generate shell commands||✅||✅|
|General-purpose chat||✅|✅|✅|