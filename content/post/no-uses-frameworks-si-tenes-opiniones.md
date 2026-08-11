---
title: "No uses frameworks si tenés opiniones"
date: 2026-05-17
slug: "no-uses-frameworks-si-tenes-opiniones"
draft: false
---

Vos tenés un camino como desarrollador independiente del camino que tiene cualquier otra persona. Aprendiste lo que aprendiste en el orden en el que decidiste aprenderlo, si es que tomaste una decisión. En todo caso, tomaste la decisión de formar parte de la institución que te formó en desarrollo. Si ese camino que elegiste te llevó a desarrollar software de una manera en particular, entonces hacete un favor, y no uses frameworks.

O por lo menos, si vas a usar un framework, es importante que entiendas por qué existe, y qué problema vendría a resolver.

El patrón de diseño de aplicaciones web [Modelo-Vista-Controlador](https://es.wikipedia.org/wiki/Modelo%E2%80%93vista%E2%80%93controlador) es muy útil para diseñar aplicaciones web con una cantidad de lógica considerable. Si tenés que acomodar un poco de texto realmente [no deberías usar nada más que HTML.](https://justfuckingusehtml.com/es-AR) Pero si tus formularios generan datos que pueden llegar a ser utilizados, la verdad es que esta metodología es muy intuitiva. Y hay excelentes soluciones para esto: Spring MVC, Ruby on Rails, Laravel, Django si nos ponemos laxos con la definición... Imposible quedarse con uno solo.

Pero MVC espera que vos hagas las cosas de una manera: El modelo trabaja con la información y encapsula las reglas del dominio, el controlador responde a solicitudes HTTP y prepara la información llamando clases de servicio o haciendo operaciones básicas, y las vistas muestran lo que el controlador les dijo que muestren. Y no hay mucho más.

Y si no te gusta esto, entonces no uses frameworks.

Todos los frameworks tienen opiniones, todos los frameworks esperan que hagas las cosas de una determinada manera. Y si vas a estar rebelándote contra el framework porque te parece innecesario declarar una clase de servicio o una acción, o porque no te gusta que hayan tantos directorios en tu repositorio, entonces creo que la pregunta no es "¿Por qué no puedo hacer lo que quiero con el framework?" (El framework te deja, pero la comunidad no), sino:
"¿Por qué estás usando un framework y no una librería?"

Si lo que necesitás es flexibilidad para estructurar tu código como te parezca, Express, Flask o Fiber te van a hacer más felices que Rails o Laravel. Son herramientas sin opiniones fuertes: te dan un router, middleware, y el resto lo decidís vos. El precio es que todas las preguntas que el framework respondía por vos en base a poner de acuerdo a un montón de desarrolladores ahora las tenés que responder vos, y hacerte cargo de lo que eso signifique en el futuro.

Defender pelearte con el framework y llenar de lógica tu controlador me suena a usar una motosierra para hacer collage y quejarte de que te rompe las revistas.
"¡Mi imagen Docker pesa 850MB después de todas las dependencias de Laravel!"
No uses un framework.

> "In general, don't fight your frameworks. Seek ways to keep the fundamentals of domain-driven design and let go of the specifics when the framework is antagonistic."
>
> — Eric Evans, *Domain-Driven Design: Tackling Complexity in the Heart of Software*

ERRATA: "Aprendiste lo que aprendiste en el orden en el orden en el que decidiste _aprendirlo_" -- Aprenderlo.

Gracias MAD!

27-05-26