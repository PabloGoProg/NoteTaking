Solucion de problemas de ingenieria de software:
* Localization: localizar las funciones y lineas importantes para la solucion del problema
* Repair: Generar los parches necesarios para el codigo - similar a map explorer - reemplazar trozos de codigo por codigo nuevo.

Cada respuesta del modelo contiene:
- Rasonamiento de lo que estuvo haciendo (lo que el modelo entendio)
- Respuesta estructurada que contenga la informacion seleccionada (lo que el modelo decicdio hacer)

![[Screenshot 2025-03-11 at 2.32.19 PM.png]]

0. Read problems statement and golden patch-  any of the next is a bad issue:
	- Missing important information.
	- GP contains solutions that have no common changes with the PR.
	- More than 5 files to fix the issue.
	- Issue not closed on Github
	- Cannot create new files - Just edit Python files.
	- The GP do not edit Python files or just edit documentation.
	- GP removes/adds imports.
	- Cannot edit `__init__.py`
	- Python version must be version 3 or above
	- Functionality stays the same after GP solutions (Var or func names changes).
1. Localization
	1. **Obtain Relevant Agent Files** File finding - File that needs to be edited and its justifications.
	2. **File Skeleton** Functions, variables or classes that needs to be edited for each file and its justifications.
	3. **Line Level Localization** We gave the model the problem statement and files & resources that needs to be edited. (1 & 2). The the model should return the lines that need to be edited to solve the issue.

**NOTAS:**
1. Las respuestas dadas por el modelo deben ser escritas de forma "impersonal". - No usar sujeto o categorizaciones a si mismo.
2. Estructura para redaccion de una critica
	The model was wrong cuz ... (bas justification, lack of info, hallucinated info, not following instructions, format errors)
3. El modelo no tiene contexto de los pasos previos, no preocuparse en caso de que las respuestas se sientas repetitivas.
