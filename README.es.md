<div align="center">

[Português](README.md) · [English](README.en.md) · **Español**

# Poker MTT BI

**La app donde sigo mis torneos de póker: paneles, las finanzas del equipo y un asistente con IA local que responde y registra cosas por mí.**

<img src="docs/img/resumo-escuro.png" alt="Pantalla Resumen, tema oscuro" width="900">

<sub>Código cerrado · imágenes con datos ficticios · la interfaz de la app está en portugués</sub>

</div>

## Por qué existe

Juego torneos online (MTT) todos los días, en varias cuentas, dentro de un equipo. El equipo tiene reglas propias de reparto: el makeup (pérdida acumulada que hay que recuperar antes de repartir ganancias), el deal (la parte de la ganancia que me queda), el rakeback (parte de las comisiones pagadas que vuelve) y una meta semanal. Antes lo llevaba todo en una hoja de cálculo, y revisar que cada pago coincidiera me llevaba horas.

Hoy marco los registros del día y la app hace el resto. Muestra cómo voy, calcula lo que el equipo me debe y me avisa cuando algo no cuadra.

## Resumen

El mes de un vistazo: ganancia, ROI, la curva de la carrera, el mejor torneo, el resultado por categoría y por cuenta, y cuánto falta para la meta de rake de la semana.

<img src="docs/img/resumo-claro.png" alt="Pantalla Resumen, tema claro" width="900">

## Diario y Torneos

El calendario muestra cada día jugado y su resultado. Al hacer clic en un día aparecen sus destacados. En Torneos está la lista completa, con búsqueda, filtros y exportación a hoja de cálculo.

<img src="docs/img/diario.png" alt="Pantalla Diario" width="900">

<img src="docs/img/torneios.png" alt="Pantalla Torneos" width="900">

## Finanzas

La app rehace el makeup día a día desde el primer torneo, con las reglas del equipo de cada época. Muestra la semana actual, las semanas cerradas, los retiros recibidos y cuánto falta para liberar el rakeback.

<img src="docs/img/financeiro.png" alt="Pantalla Finanzas" width="900">

## Pool

Pego el informe diario que manda el equipo. La app revisa los totales, reparte la cuota de cada jugador y suma el mes.

<img src="docs/img/pool.png" alt="Pantalla Pool" width="900">

## Asistente con IA local

Un chat dentro de la app, con un modelo de lenguaje (Qwen, `qwen3.5:4b`) que corre en mi propia tarjeta gráfica. No tiene costo de API, y ningún dato sale de la computadora.

- **Pregunto en vez de buscar:** "¿cuánto gané en noviembre?", "¿qué cuenta perdió más en octubre?", "¿cuánto me pagó el equipo en septiembre?".
- **Registra por mí:** escribo "cayeron 136,20 del cierre diario del 05/11 en el banco" y arma el retiro. No se guarda nada hasta que hago clic en **Gravar** (Guardar).
- **Me avisa:** un pago calculado que no llegó, un día de la pool sin informe, un registro que necesita revisión.

El modelo solo entiende el pedido. Las cuentas las hace la propia app, así que el asistente muestra los mismos números que las demás pantallas.

Elegí el modelo midiendo. Probé 7 modelos locales con 22 pedidos reales. `qwen3.5:4b` acertó 19, sin inventar filtros y sin intentar guardar por su cuenta, en 5,4 s por respuesta. `qwen3:8b`, del doble de tamaño, también acertó 19, pero inventó 12 filtros que nadie pidió y tardó 50 s. Tres de los seis modelos que corrieron intentaron escribir en la base sin confirmación, y por eso solo el clic guarda. La prueba también mostró que buena parte del error estaba en el formato del pedido, no en el modelo: cuando pasó a enviar solo "mes pasado" y la app a calcular las fechas, los aciertos subieron de 13 a 18.

<img src="docs/img/assistente.png" alt="Asistente respondiendo una pregunta y proponiendo un retiro" width="900">

## Grilla

La grilla semanal de torneos del equipo, tomada de su hoja de cálculo.

<img src="docs/img/grade.png" alt="Pantalla Grilla" width="900">

## Hecho con

Lo construí orquestando agentes de IA (Claude Code y Gemini), al estilo *vibe coding*. Escribo las reglas y el criterio de aceptación de cada funcionalidad y divido el trabajo en tareas pequeñas. Los agentes escriben el código, otro agente revisa cada entrega sin haber visto cómo se hizo, y nada entra sin pasar más de 1.800 pruebas automatizadas. Después lo compruebo en el uso diario.

Por debajo: C# y .NET 10 en el servidor, React y TypeScript en la interfaz, SQLite como base de datos y Ollama para el modelo local. Corre entero en mi computadora, con tema claro y oscuro.

---

<sub>Hecho por **Yan Camargo** · [LinkedIn](https://www.linkedin.com/in/yancaecamargo) · © 2026, todos los derechos reservados ([LICENSE](LICENSE))</sub>
