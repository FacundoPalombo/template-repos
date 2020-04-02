<article align="center"><h1 align="center">MS - $este-repo</h1></article>

![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/alert_status)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/coverage)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/bugs)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/code_smells)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/sqale_rating)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/reliability_rating)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/security_rating)
![Build Status](http://sonar-badges.prisma.redbee.io/sonar/$este-repo/vulnerabilities)

## Secciones 📜

 - [Instalación](#instalación-)
 - [Desarrollando la API](#desarrollando-la-api-)
 - [Quick reference](#quick-reference-)
 - [Otras tareas](#otras-tareas-)
 - [Despliegue](#despliegue-)
 - [Versionado de API](#versionado-)

## Stack tecnológico 🛠️

Los frameworks y librerías que utilizaremos son:

 - [Rails 3.2](http://rubyonrails.org/) - Web Framework
 - [Grape](http://rdoc.info/github/intridea/grape) - API endpoints
 - [Devise](https://github.com/plataformatec/devise) - Authentication
 - [RailsAdmin](https://github.com/sferik/rails_admin) - Database dashboard
 - [MiniTest](https://github.com/seattlerb/minitest) - Unit testing

## Instalación 🔧

### Dependencias 📦

Asegurate de tener instalado JDK 11, Java 8 y Git.

Para verificar las versiones puedes ejecutar:
**Java**
```bash
$ java --version
```
**Git**
```bash
$ git --version
```
### GitHub :octocat:

El primer paso es registrarte en [github](https://github.com/) y solicitar asociarte a la organización TodoPago. Podrás encontrar más info de como contribuir en [éste link](/CONTRIBUTING.md). También podrás ver nuestra lista de [contribuyentes](./graphs/contributors)


### Clonando el repositorio  🧙

Luego clonar el repositorio por HTTPS.

```bash
$ git clone https://github.com/TodoPago/$este-repo
```

```bash
$ cd portal-web-app
```

**Note:** Recuerda reemplazar las configuraciones de git en tu repositorio con el usuario y email que estás utilizando en github. Para ello ejecutar:
```bash
$ git config user.name '$tu-nombre' && git config user.email '$tu-email'
```
Puedes verificar las variables con el comando: `$git config -l`

### Instalación 🔧

Ejecuta éste comando para instalar las dependencias:

```bash
$ gradle build
```

Ahora vamos a instalar la base de datos de desarrollo en nuestra computadora:

```bash
$ rake db:migrate db:test:prepare
```

### Running :runner:

Para correr el proyecto:

```bash
$ gradlew bootRun
```
O ejecuta el comando `gradlew.bat` `bootrun.sh`

El entorno de desarrollo corre sobre <http://localhost:8087>. Ejecuta una llamada GET de prueba en <http://localhost:8087/actuator>

## Desarrollando la API 🐱‍💻

### Trabaja sobre las User Stories ✅

Comienza tus actividades a partir de una User Story de jira.
Puedes encontrar el backlog aquí: <http://jira.prismamp.com.ar:8080/browse/TPWEB>

### Definiendo el Schema 🧮

Next, define a schema based on resources.

 - Identify resources in your application (i.e user, tweets, favorites)
 - Identify attributes of each resource (i.e a tweet has a body, timestamp)
 - Identify the "associations" for each resource (i.e a tweet has a user_id)

For example with twitter, you have a `user` resource and a `tweets` resource
and a tweet "belongs to" a user. A user has an email and a password and a tweet
has a body and a timestamp.

### Crear modelos 📃

Models are the way that a Rails application stores data for your application resources.
On a high level:

  - Use `rails g model <NAME>` to generate models for each resource
    - `rails g model Tweet`
  - Fill out the "db/migrate/xxxxx" file for each model
  - Fill out associations for each model (i.e `belongs_to :user`)
  - Fill out any validations for each model (i.e `validates :body, :presence => true`)

For example, imagine we want to create a "Tweet" resource that has a status and is created by a user. First,
we would generate the tweet resource:

```bash
$ rails g model tweet body:string user_id:integer
```

This will generate a file in `db/migrate/xxxxxx_create_tweets.rb` that defines the fields
for the tweet (right now just a body and a number representing the user).

Now we can run the migrations with `rake db:migrate` and then check out our
model file at `app/models/tweet.rb`. Models are blank by default and often don't need any
additional code. The fields (body and user_id) will work automatically.

We can now create, update or destroy tweets from within our APIs:

```ruby
# create
tweet = Tweet.create(:body => "foo", :user_id => 1)
# update
tweet.update_attribute(:body, "bar")
# find
my_tweet = Tweet.where(:body => "bar").first
# delete
my_tweet.delete
```

Once we have our models, we can build the related API endpoints so our client mobile applications
can modify the resources.


## Otras tareas 📜

Estos son links importantes y guias de configuración para algunas utilidades:

  - Poner aquí tarea de configuración de variables de entorno.
  - Poner aquí detalles de autenticación.
  - Listar o mostrar como referencia las variables de CloudConfig que este proyecto utiliza
  - Mas info acerca del repo con tutoriales

## Quick Reference 🏃💨

### Key files

Key files to edit:

  - "./config" - Aqui podrás setear las variables de configuración de tu entorno

### Endpoints 

Acá vamos a encontrar una lista de los endpoints que se pueden consumir y el swagger

  - [/api/users](./docs/api/users) - Manejo de usuarios

## Despliegue 🚀 

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
## Versionado 📌
Para el versionado de apis tenemos los siguientes releases con sus respectivas referencias en cada link:
- ~~v0: [ms/api/v0/users](/version/0)~~ _deprecated_
- v1: [ms/api/v1/users](/version/1)
- **v2: [ms/api/v2/users](/version/2)** *LTS*
- v3: [ms/api/v3/users](/version/3)
- v4: [ms/api/v4/users](/version/4) *Current*
