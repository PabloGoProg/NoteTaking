[Code completions with GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/ai-powered-suggestions)

Copilot provee dos tipos de sugerencias de codigo:
* **Code Completions:** Empezar a Escribir -> Copilot provee sugerencias que se ajustan al estilo del códificacion del individuo.
* **Next Edit Suggestions (NES):** Predice futuros cambios en base a los cambios que se esten realizando, prediciendo el lugar y el contenido de la próxima edición.

### Code Completions
A medida que se escribe nuevo codigo, Copilot provee sugerencias de la linea o un nuevo bloque de codigo. Pueden ser aceptadas en su totalidad, parcialmente o ser ignoradas.

![Code Completions](https://code.visualstudio.com/assets/docs/copilot/inline-suggestions/js-suggest.png)

En caso de querer aceptar solo parte de la sugerencia, se puede usar `"Command | Control" + "Felcha"` para aceptar de palabra en palabra.
#### Sugerencias desde Comentarios
Se pueden realizar sugerencias desde comentarios de en el codigo. -> Usar _inline prompts_ con `"Command | Control" + "i"`  es mucho mas fluido.

![comment_suggestion](https://code.visualstudio.com/assets/docs/copilot/inline-suggestions/ts-suggest-code-comment.png)

### Next Edit Suggestions
Ya que las ediciones no se realizan de forma aislada, y tienden a seguir un flujo lógico, NES predice la ubicación del siguiente cambio a realizar. - Se puede usar `"Tab"` para acepetar el cambio y `"Esc"` para rechazarlo. - Al momento de pasar a la siguiente, Copilot se encarga de navegar al siguiente archivo si es necesario.

![](https://code.visualstudio.com/assets/docs/copilot/inline-suggestions/nes-arrow-directions.gif)

Feature en preview - debe activarse dentro de las configuraciones de Copilot `github.copilot.nextEditSuggestions.enabled`


