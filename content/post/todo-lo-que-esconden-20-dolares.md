---
title: "Todo lo que esconden 20 dólares"
date: 2026-09-17
draft: false
---

Me agota usar las redes sociales por un rato y darme cuenta de lo predatorio que se volvieron los anuncios últimamente. La industria de los anuncios me da miedo y asco al mismo tiempo: Miedo porque no sé dónde va, y asco porque no puedo creer que hayan llegado hasta este punto. Mientras más límites cruza, más nos acostumbramos al bombardeo, y más cosas horribles dejamos pasar.

Particularmente me dan más asco los anuncios que usan el miedo como herramienta de venta, porque se siente injusto. Hacer asustar a alguien para que compre algo se siente ruin, y bajo, por lo menos para mí. Es un buen ejercicio detenerse ante la publicidad a intentar ver si está buscando asustarte con algo: Quedarse atrás, perderse algo, estar expuesto y vulnerable, ser menos... Lo que se te ocurra. Lo hacen porque necesitan la plata, pero debería haber un límite.

Yo creo que este comportamiento se está usando mucho en la industria de la informática en estas épocas. Imagino que quien me lee ahora mismo sabe a lo que me refiero, pero en esta entrada me gustaría traer a colación como se usa específicamente en el área del *self-hosting* y en los laboratorios hogareños. Todo desde una perspectiva personal, ya que yo conviví con esto.

Cuando empezás a cruzarte con videos de home labbing, el mundo parece ser un arenero para que te diviertas. Los creadores de contenido te prometen independencia, seguridad, comodidad, y una serie de herramientas que se ajustan específicamente a tus necesidades. Las suscripciones, las filtraciones de datos, los cortes de servicio, cosas que serán parte de tu pasado si agarrás tus computadoras viejas, les instalás alguna distribución de Linux, les instalás Docker y *pipeás* un script a tu shell que estás descargando del internet con curl. 

**curl tu-url-aqui.com/install.sh | bash**... se entiende.

Y cuando indefectiblemente se rompe (no es tan poco común como te lo prometen) supuestamente es donde aprendés más. Porque el fracaso enseña. 
¿Pero realmente vale la pena?

Te divertiste una tarde, instalaste Pi-hole, hiciste que el internet se enlentezca un poco, el HTML tarda más, pero adiós anuncios para siempre... Y hola la complejidad de ser un administrador de sistemas. Porque por más insignificante que se sienta un servicio, termina siendo tu responsabilidad, y cuando llegás cansado de la calle y te querés sentar a ver un video pero tu computadora no resuelve https://www.youtube.com, volvés a pagar.
Te molesta tener que pagar por Spotify, entonces recauchutás un disco, lo ponés en una laptop, la dejás todo el día enchufada, le instalás Plex, y después la **suite arr*, y después la app para el teléfono, y lo sincronizás, y te aseguro que el día que te despiertes con muchísimas ganas de escuchar cómo es que tus artistas favoritos cantan esa parte de esa canción de ese álbum y abras la aplicación y veas un HTTP 500, volvés a pagar.

¿Y quién está detrás de todo esto? La gente que *come* gracias a que vos te asustaste. Porque los personajes que ves en YouTube viven de que los veas. Necesitan que los veas, necesitan que te pique el bichito de la curiosidad. No son malos por eso, pero no te olvides de que te necesitan. Necesitan que te resuenen las preguntas que te hacen, cuando te apuntan con el dedo, cuando te dicen que las suscripciones son predatorias. Pero no creo que sea así de fácil, y no creo que deberías tomártelo tan a pecho.

No creo que hay que criminalizar el SaaS cuando en TU vida reduce la fricción en momentos donde VOS lo necesitás. Si la suscripción te hace la vida más fácil, no tiene sentido empezar a pensar en todo lo que piensan los tipos que te cobran los 20 dólares para que no pienses. Porque eso es lo que hay atrás de 20 dólares, la responsabilidad de mantener todo andando.

Capaz te gusta la adrenalina, capaz querés una buena excusa para gastar tu plata, y todo eso es válido, pero si sos algo parecido a mí y solamente querés descansar... No cortes la suscripción. Porque yo me arrepentí, dí toda la vuelta y volví. Probalo, y fijate.

Y respecto a la seguridad... No hay dispositivo que no sea vulnerable, y tener tu infraestructura no te asegura nada. Fijate en los logs de tu fail2ban (espero que lo hayas configurado) cuantas IPs rusas te intentaron abrir el puerto 22 con user ubuntu password admin123. Tus datos ya están donde no querés. Lo peor ya pasó, y hay muy poco que puedas hacer. Y si configuraste mal tu servidor, corrés tanto riesgo como corren tus datos en Google Drive. No es idea mía esto.

Así que antes de comprarte el NAS o la GPU o armarte el clúster, sentate a pensar quién te está queriendo asustar y por qué.