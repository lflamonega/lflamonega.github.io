---
title: "De qué hablamos cuando hablamos de arnés"
slug: "de-que-hablamos-cuando-hablamos-de-arnes"
date: "2026-11-10"
draft: true
---

Para todos los que no mantenemos un clúster de GPUs, el LLM que usamos en el día a día termina siendo una API. Detrás hay mucha infraestructura, servicios que convierten los pesos de los modelos en algo compatible con HTTP. Pero delante de esa API también hay servicios que la convierten en lo que conocemos hoy: chats, agentes. Últimamente estuve pensando mucho en cómo llamarlos, en qué tipos hay, y en cómo ese conocimiento puede ayudarnos a entender todo lo que se puede hacer con un modelo.

Lo más cercano que hay en la bibliografía es el término arnés (*harness*). La palabra ya se usaba para hablar de agentes, pero se volvió popular en febrero de 2026 con el *harness engineering*: Mitchell Hashimoto lo [puso por escrito](https://mitchellh.com/writing/my-ai-adoption-journey) el 5 de febrero y OpenAI publicó [su caso con Codex](https://openai.com/index/harness-engineering/) seis días después. La idea era simple: cada vez que el agente se equivoca, ajustás el entorno con documentación y tests para que no vuelva a pasar. Philipp Schmid ya sostenía [en enero](https://www.philschmid.de/agent-harness-2026) que, a medida que los modelos se parecen entre sí, el arnés pasa a ser lo que diferencia un resultado de otro. Se podría debatir si el *harness engineering* sigue de moda, pero ¿quién está contando?

La práctica de modificar la aplicación misma, en cambio, ya venía de antes. [Claude Code sumó plugins](https://claude.com/blog/claude-code-plugins) en octubre de 2025, OpenCode tiene los suyos, y [Pi](https://mariozechner.at/posts/2025-11-30-pi-coding-agent), un agente de código minimalista pensado para ser extendido, salió a fines de noviembre. Codex los sumó [en marzo de 2026](https://thenewstack.io/openais-codex-gets-plugins/). Con todo eso, cada uno puede hacer que su modelo siga el flujo que quiera.

El problema es que casi siempre la discusión se queda en la definición general, "todo lo que no es el modelo", y de ahí no pasa. Pero un arnés de chat tiene otras prioridades que el de un agente que trabaja sobre un repositorio, y ese se parece poco al que coordina varios subagentes en paralelo. Si los arneses se pueden modificar, hace falta una forma de distinguirlos. Así que acá propongo una clasificación en dos niveles: la clase dice cómo se define el arnés, y el tipo dice qué función cumple. Con eso se puede responder qué arnés estoy construyendo o eligiendo.

No soy el primero en intentar ordenar esto. Hay un [estudio de 70 proyectos de agentes](https://arxiv.org/abs/2604.18071) que encontró cinco dimensiones de diseño (subagentes, contexto, herramientas, seguridad y orquestación) y cinco arquetipos, entre ellos los orquestadores multi-agente y los proyectos verticales. Y Microsoft, en [Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/harnesses-overview), separa tres arneses: uno estándar para agentes basados en reglas, uno de GitHub Copilot para trabajo de razonamiento intensivo (aclaran que no es el servicio GitHub Copilot) y uno de Customer Conversation para atender clientes por voz y chat. Lo que propongo yo toma los dos niveles por separado, y empiezo por el más básico.

La clase depende de cómo se construye el arnés, y hay dos. Un arnés declarativo se define con configuración. Uno describe qué debe hacer el agente (prompt, skills, plugins, servidores MCP) y el arnés pone el motor que lo ejecuta. [kagent](https://kagent.dev/docs/kagent/latest/agents/agent-harness/) funciona así: una plantilla define el modelo, el prompt y las herramientas, y un recurso aparte, el Harness, decide qué ejecuta al agente: su motor propio, Codex, Claude o una imagen tuya. Con el motor propio el bucle ya viene hecho y solo se configura. Como no se escribe, tampoco se puede cambiar sin salir de la configuración.

Un arnés imperativo, en cambio, se define con código. Uno escribe el bucle y las condiciones de parada. Hay control total, y también responsabilidad total sobre cada falla.

En la práctica la frontera no es tan limpia. Un arnés imperativo puede exponer una capa declarativa para que otros lo configuren, y eso es justamente lo que hacen los plugins de los agentes de código. kagent hace lo contrario: mete a Codex o a Claude Code, que son imperativos, dentro de un recurso declarativo. La clase describe cómo está construido el núcleo y deja afuera lo que se le agrega encima o alrededor. Al final la diferencia sigue siendo dónde vive el trabajo, si en la configuración o en el código, y se elige según cuánto control necesitás y cuánta complejidad estás dispuesto a asumir.

Después está el tipo, que describe qué hace el arnés. Los hay de cuatro tipos, y los dos primeros son imperativos en su núcleo, porque en ambos alguien escribió el bucle en código: el ciclo de turnos entre usuario y modelo en el chat, el ciclo de llamadas a herramientas hasta terminar la tarea en el agente de código. Sobre ese núcleo pueden montarse capas declarativas (plugins, skills, servidores MCP), pero no lo reemplazan. Los otros dos se pueden construir de cualquiera de las dos formas, con código que arma los agentes o con configuración sobre un motor existente.

El conversacional es el más simple y el más común. Gestiona el ida y vuelta entre el usuario y el modelo, y es el usuario quien conduce el bucle: manda un mensaje, el modelo responde, y se repite. En su forma básica no hay ejecución autónoma ni estado entre sesiones, y la memoria se reduce a la ventana de contexto de la conversación. Los chats actuales suelen sumar algunas herramientas, pero el usuario sigue llevando el bucle. Son los chats como claude.ai o chatgpt.com, o cualquier app que envuelva una API en un bucle de turnos. Alcanza cuando la tarea es exploratoria o cuando querés pensar en voz alta con un modelo.

El de ejecución es el que popularizó el término. Deja que el modelo actúe sobre un entorno: leer y escribir archivos, correr comandos y tests. Acá el modelo conduce el bucle. Decide qué herramienta usar y cuándo terminó. Vos le das una tarea de alto nivel y el arnés la descompone y la ejecuta. Claude Code, OpenAI Codex, Gemini CLI, OpenCode y Pi son ejemplos, y es también el tipo donde más se nota la práctica de la que hablaba al principio: casi todos permiten modificar el flujo con plugins (Gemini CLI los llama extensiones), y Pi está pensado justamente para eso.

El arnés mueve bastante el resultado. [LangChain subió su agente de código](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) de 52,8 % a 66,5 % en Terminal Bench 2.0 cambiando solo el arnés (prompt, herramientas y middleware), con el mismo modelo. Pasó de quedar apenas afuera del top 30 a estar en el top 5. El propio post aclara que el arnés se adapta a cada modelo, así que el modelo sigue importando.

El de orquestación coordina varios agentes especializados que trabajan en paralelo o en secuencia. Un orquestador parte la tarea, la reparte y junta los resultados, y cada subagente puede tener su propio contexto, sus herramientas y hasta su propio modelo. LangGraph y CrewAI son ejemplos. Acá la evidencia no ayuda mucho. Un [estudio de más de 1.600 trazas de siete frameworks multi-agente](https://arxiv.org/abs/2503.13657) catalogó 14 modos de falla, agrupados en problemas de diseño del sistema, desalineación entre agentes y verificación de tareas. Su punto de partida es que las ganancias de estos sistemas suelen ser mínimas frente a un solo agente: coordinar agrega fallas propias.

El de dominio vertical está optimizado para un tipo de tarea o de industria, por ejemplo análisis financiero o atención al cliente. Trae herramientas y contexto del área ya preconfigurados. El arnés de Customer Conversation de Copilot Studio es un caso: atiende clientes por voz y chat y deriva a una persona cuando no puede resolver. Gana en eficiencia, porque ya sabe qué herramientas exponer y qué contexto cargar, y pierde en flexibilidad: si la tarea se sale del dominio, no sabe qué hacer.

Combinar clase y tipo le pone límites al agente antes de que escribas una línea de prompt. A un arnés conversacional le podés pedir que ejecute comandos, pero no puede. Uno vertical no razona bien fuera de su dominio porque no tiene ni el contexto ni las herramientas. Por eso esta elección viene antes que el ajuste del prompt.

Dejo un cuadro con los tipos y la clase a la que pertenece cada uno:

| Tipo | Clase | Función principal | Quién conduce el bucle | Estado persistente | Ejemplos |
|---|---|---|---|---|---|
| Conversacional | Imperativo | Gestionar turnos | Usuario | Solo la sesión | claude.ai, chatgpt.com |
| De ejecución | Imperativo en el núcleo, extensible de forma declarativa | Actuar sobre un entorno | Modelo | Archivos del sistema | Claude Code, Codex, OpenCode, Pi |
| De orquestación | Declarativo o imperativo | Coordinar agentes | Orquestador | Estado compartido | LangGraph, CrewAI |
| De dominio vertical | Declarativo o imperativo | Optimizar para un campo | El sistema | Propio del dominio | Customer Conversation de Copilot Studio, un asistente de análisis financiero |

La clasificación tiene sus límites. Las fronteras entre clases no son limpias, como muestran los plugins sobre agentes de código, y los tipos se combinan: un agente de ejecución puede lanzar subagentes, y un arnés vertical puede apoyarse en uno de orquestación.

Si tuviera que quedarme con una sola pregunta práctica, sería esta: antes de preguntarte qué modelo usar, preguntate qué arnés necesita ese modelo.
