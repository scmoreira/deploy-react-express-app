# Deploy a Heroku

## Objeto de la documentación

Esta documentación tiene como objeto describir el proceso de paso a producción en [Heroku](https://www.heroku.com/) + [Mongo Atlas](https://www.mongodb.com/cloud/atlas) para una SPA con cliente [`create-react-app`](https://create-react-app.dev/docs/getting-started/) y servidor [ExpressJS](https://expressjs.com/).

## Especificaciones

El deploy se realizará en base a los siguientes objetivos:

- Disponer de los entornos de desarrollo y producción **activos de forma paralela**.
- Consumir la base de datos desde Mongo Atlas.
- Disponer del cliente y servidor alojados en dos aplicaciones independientes de Heroku.


## Fases de paso a producción

1. Registro y configuración base en Mongo Atlas y Heroku
2. Paso a producción: base de datos
3. Paso a producción: servidor
4. Paso a producción: cliente