---
title: "De qué hablamos cuando hablamos de arnés"
slug: "de-que-hablamos-cuando-hablamos-de-arnes"
date: "2026-11-01"
draft: true
---

Para todos nosotros que no estamos manteniendo un clúster de GPUs, el LLM que usamos en el día a día termina siendo una API. Es evidente que detrás de todo eso hay mucha infraestructura, servicios que convierten los pesos de los modelos en una aplicación compatible con HTTP. Pero delante de esa API también hay servicios que la convierten en lo que conocemos hoy: Chats, agentes, bots de conversación. Estuve pensando mucho en esto últimamente, en cómo llamarlos, en qué tipos de interfaces hay, y cómo ese conocimiento puede ayudar a entender todo lo que podemos hacer con nuestros modelos.

Lo más cercano que hay en la bibliografía es el término **arnés**. 

Surgió en tándem con la práctica del _harness engineering_. La idea era simple, que el sistema guíe y fuerce al agente a cumplir ciertos estándares, y en teoría con un sistema lo suficientemente fuerte, cualquier modelo daría los mismos resultados. Se logra con tests, con walktroughs, con PRDs, depende de lo que esté de moda. Aunque podría debatirse que esto del HE ya no está de moda, pero ¿Quién está contando?
Llegó un punto en que la práctica evolucionó a hacerle modificaciones a la misma aplicación para forzar el flujo. Plugins de Claude Code o Codex o Opencode que hacían que el modelo se comporte de una manera. Cuando llega Pi esto se amplía ya que uno podía hacer que su modelo siga el flujo que quiera.