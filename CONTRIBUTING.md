# Contribuciones 🤜🤛

Para contribuir en este repositorio, antes de realizar cualquier cambio, por favor discutirlo por los portales de gestion de proyectos (JIRA o Github Issues) y si tienes alguna duda, por favor haz el review con tus compañeros de equipo. 

Para las comunicaciónes entre individuos nos regimos por el codigo de conducta que detallamos más abajo.

## Pull Request Process ⛓

### Pull requests para desarrollo 🛠

1. Deberán crear una rama que corresponda al ticket que le fue asignado desde la rama develop, para ello hacer `git checkout develop` --> `git checkout -b [newbranch]`
2. Se utilizará la siguiente convención de branching: `[feature|bugfix]/[story_number_code]-[detail-of-branch]`. Donde:
 *`[feature|bugfix]` es el tipo de ticket que estás trabajando, si es una nueva funcionalidad va feature, si es un arreglo de una funcionalidad va bugfix.
 *`story_number_code` es el código numerico del ticket de JIRA o Github Pages asignado. Ej: Story: '_[ALPHA-365] - agregar año bisiesto al calendario para que funcione mejor_' el story_number_code será 365
 *`detail-of-branch` es el nombre de la branch breve, los espacios deben ser delimitados por guiones medios: (-)
 * Evitar utilizar ñ o carácteres especiales en los nombres de las branches, cambienlo por lo que quieran, (n ni, gn),
 *en el ejemplo anterior la branch que crearíamos sería: _feature/365-agregar-anio-bisiesto_*
3. La estructura de los commits ideal sería:
```
1>> Titulo corto explicativo. 
2>> Algo mas detallado de lo que se realizó en la branch.
n>> Mas info, por ej si quieres puedes agregar un sumario detallado de las modificaciones, eso es a gusto.
```
4. Cuando esté listo el ticket recuerda de antes de subirlo al repositorio remoto hacer pull de los cambios y chequear que no se haya roto nada con `git checkout develop` -> `git pull` -> `git checkout [branch_with_my_work]` -> `git merge develop` -> resolver conflictos (si los hubiere) -> `git merge --continue` || `git commit -am 'Merge commit with branch develop, resolving deltas'` 
5. Crea un Pull Request a la branch develop con el código completo del ticket con el que estuviste trabajando, y una descripción muy breve de todo lo hecho, puedes detallar abajo lo que se realizó en el pull request con el mismo template que utilizabamos en los commits, pero más generalizado. En el ejemplo anterior el título de nuestro pr tendría que ser algo como esto: _[ALPHA-365] - se agregó la funcionalidad de año bisiesto_.

6. Recuerda que para que un Pull Request sea aceptado, debe haber code review de al menos 2 desarrolladores más. Píde ayuda a tus compañeros de equipo!

## Despliegue. 🚀

Para desplegar a desa, qa o prod debemos ejecutar el job de jenkins TP_ENCOLADOR-SPRINT, este lo encontraremos en [jenkins.prisma.redbee.io](jenkins.prisma.redbee.io), solicitar las credenciales en el equipo de desarrolladores o en el canal de dev-ops.
*Como encolar un tag*
1. Tomar el tag que tiene la imagen que queremos encolar, cada vez que se realiza un pr a la rama `develop` se generará un paquete con un tag, ver en la sección [releases](./releases). Copiar ese tag.
2. Ir al Jenkins [jenkins.prisma.redbee.io](jenkins.prisma.redbee.io) y abrir el job TP_ENCOLADOR-SPRINT.
3. Ejecutar un build with parameters con los siguientes campos llenados:
- Acción: `Encolar`
- Id: `/todopago/#este-repo`
- Tag: `El tag que obtuviste`
- TagContent_QC_Jira: `TUPROYECTO 123`  <- Este es el id de la historia de jira relacionada, no debe usarse guiones ni corchetes.
- UseJSON: `true|false` *Opcional* 

## Código de conducta. 📖

Por favor leer nuestro código de conducta [aquí](./CODE_OF_CONDUCT.md).
