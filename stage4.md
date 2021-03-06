

# Paso a producción: servidor

Transferir tu API local a producción supone desplegar los archivos que la componen a un servidor externo, permitiendo así que las respuestas que ahora se emiten desde `http://localhost:6000/api` pasen a realizarse desde `https://myserver.herokuapp.com/api`.

## Variables de entorno remoto

Debido a que el archivo `.env` no será desplegado, es necesario habilitar las variables de entorno en tu aplicación de Heroku.
 
1. Accede mediante la terminal al directorio raíz de tu servidor, donde se encuentra el `package.json`. Puedes comprobar en cualquier momento la aplicación de Heroku asociada a un Git mediante el comando

       heroku apps:info

2. Declara cada una de las variables de entorno de tu archivo `.env` con el comando `heroku config:set NOMBREVARIABLE=”VALORVARIABLE”`. Ejemplo:

       heroku config:set CLOUDINARY_NAME="german-cloud" --app myServer
  
   No olvides sustituir `myServer` por el nombre de tu aplicación servidor. Puedes consultar el valor de cualquier variable de entorno con el comando `heroku config:get NOMBREVARIABLE` 

3. Una vez has realizado este proceso para cada una, incluye dos variables adicionales en vistas a garantizar frente a CORS el acceso de tu cliente a la API, tanto si se realiza desde el entorno local como desde el remoto:

       DOMAIN_REMOTE=https://myclient.herokuapp.com  
       DOMAIN_LOCAL=http://localhost:3000

4. No olvides incluir igualmente estas dos variables en el archivo `.env` de tu entorno local.

## Configuración multi dominio en CORS

En este punto tu API acepta peticiones desde `http://localhost:3000` gracias a la configuración de CORS. En adelante debe también aceptarlas desde `https://myclient.herokuapp.com` ya que tu cliente necesitará comunicarse con la API tanto desde el entorno de desarrollo como de producción.

Para ello, incluye la nueva variable de entorno `DOMAIN_REMOTE` a la *whitelist*, que contiene los dominios aceptados por CORS:

    const whitelist = [process.env.DOMAIN_REMOTE, process.env.DOMAIN_LOCAL]

Comprueba cómo tu servidor sigue funcionando en local con normalidad.

## Paso a producción

Transferir los archivos a la aplicación de Heroku hará accesible tu API desde los dominios aceptados por CORS, a la vez que mantendrá todas sus funcionalidades en el entorno local, donde puedes seguir desarrollando.

1. Accede mediante la terminal a la raíz de tu servidor, donde se encuentra el archivo `package.json`
2. Agrega los cambios y realiza un primer commit:
       
       git add .
       git commit -m "first server deploy on heroku app"  

3. Procede a la subida
       
       git push heroku master

4. Una vez finalizado, comprueba la ausencia de errores en los logs mediante el comando `heroku logs --tail`
5. Abre tu aplicación en el navegador mediante `heroku open`, o tecleando la URL de la misma. Podrás comprobar si los endpoints de tu API mantienen su funcionalidad, ahora en remoto.

## Interfaz de usuario de Heroku

Puedes acceder a [tu cuenta de Heroku](https://dashboard.heroku.com/apps) mediante el navegador para comprobar detalles de tus aplicaciones: commits (pestaña *Activity*), variables de entorno (pestaña *Settings*), o incluso trabajar con la consola de Heroku en la esquina superior derecha *More => Console*.
