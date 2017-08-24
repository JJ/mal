# Lo estamos haciendo mal: una llamada al debate sobre el cambio en la enseñanza universitaria de la informática

_Version 0.3_

[![Build Status](https://travis-ci.org/oslugr/polleitor.svg?branch=master)](https://travis-ci.org/oslugr/polleitor)
[![Coverage Status](https://coveralls.io/repos/github/oslugr/polleitor/badge.svg?branch=master)](https://coveralls.io/github/oslugr/polleitor?branch=master)

## Charla: Lo estamos haciendo mal

La charla es una 
*appresentación* que usa Polleitor, un Sistema cliente-servidor para crear widgets de encuestas. Durante un tiempo, estará desplegada en [Heroku en jenui06.herokuapp.com](http://jenui06.herokuapp.com). Las [referencias para esta presentación están en este documento](REFERENCIAS.md).

Los fuentes de la charla, con licencia CC, y los del software, con licencia MIT, están en [este repo de GitHub](http://github.com/JJ/mal). 

## Aplicación: polleitor

La parte servidor usa LokiDB para almacenar las encuestas y
resultados y funciona con REST, la parte cliente JavaScript para
configurar las encuestas y enviar los resultados.

La configuración se hace en el servidor y en él se almacenan los
resultados.

## Instalación

Tras clonar de este repo:
```bash
npm install
```

Ejecutar Tests (opcional):
```bash
npm test
```

Iniciar servidor:
```bash
npm start
```

De ahí, se accede http://localhost:3000 y listo. 

### Desplegar en heroku

Si usas [Heroku](http://heroku.com), cambia `repository` en el fichero
de configuración `app.json` y

    heroku login
	heroku git:remote -a mi-proyecto-en-heroku
	git push heroku master

El problema con heroku es que no mantiene la aplicación en memoria de
forma continua ni tampoco mantiene los ficheros, con lo que si quieres
tener una encuesta que se ejecute durante un tiempo determinado no es
la opción más adeduada.

Una alternativa es guardar los resultados en los logs, para lo cual se
puede usar un *addon* gratuito tal como
[Papertrail](https://elements.heroku.com/addons/papertrail) o (Sumo Logic(https://elements.heroku.com/addons/sumologic)


## API

Se accede al servicio mediante una API REST

| **Método** | **Ruta**           | **Descripción**                        | **Resultado**                  |
|:----------:|:------------------:|:--------------------------------------:|:------------------------------:|
| GET        |`:poll`             | Devuelve las preguntas de una encuesta |`[{question,options,id}]`       |
| GET        |`:poll/resultados`  | Resultados del poll                    |`[{question,options,id,answers}]`|
| PUT        |`:poll`             | Responde al poll [{id,answer}]         |`{poll,updates,failedUpdates}`  |
