# Whopper King - Proyecto de Sistema de Información (ERP/POS)

Este repositorio contiene la documentación y planificación estratégica para la implementación de un sistema de información (ERP y POS) diseñado específicamente para **Whopper King**, un restaurante ubicado en Pasto, Colombia. El objetivo principal es digitalizar y optimizar sus procesos operativos, financieros y de inventario, sentando las bases para futuros modelos de análisis de datos e inteligencia artificial.

Links:
(Estructura entregables )https://unaledu-my.sharepoint.com/:w:/g/personal/juamador_unal_edu_co/IQBo9fJk-2CVRZhiN08DpgCdAfrLIwVQZRCTy2jkFn9TX7k?rtime=iqCGIQUd30g
(Hito numero 1) https://unaledu-my.sharepoint.com/:w:/g/personal/juamador_unal_edu_co/IQAfCkqXU9nBR4EYZaIEN_bLAUN_Crxkbu8_wi-Or0behM4?e=I8ljkm&or=WORD-WEB.BODY.NT&ct=1790561360548
(Matrix del hito numero 1) https://unaledu-my.sharepoint.com/:x:/g/personal/juamador_unal_edu_co/IQClhJNqJNXwTZuEifLOQLZOAb0R7l4E2wlS953NadApDZY?e=wIMf7Q&or=WORD-WEB.BODY.NT&ct=1790561357901
(Mapa de sentimientos de usuario) https://docs.google.com/spreadsheets/d/19mdH4KjPX7gglhLxKqk-S8mid6bJlW58XvoNvXnOoJ8/edit?gid=0#gid=0

---

## 1.1. ¿Quién es Whopper King? (Historia y Propuesta de Valor)

Ubicado en el sector de las cuadras en Pasto, Whopper King fusiona el concepto de comida rápida al estilo estadounidense con la oferta de un restaurante tradicional.

*   **Historia y Esencia en Pasto:** El negocio nació con un enfoque empírico. Actualmente opera bajo el liderazgo de una jefa de cocina, apoyada por personal auxiliar. Su esencia radica en la hiper-diversificación: ofrecen hamburguesas gigantes estilo americano (como la "Todo Terreno" o la "Texana"), pero también operan como restaurante tradicional vendiendo almuerzos completos y cortes especiales (ej. churrasco).
*   **Misión y Visión (no oficial):** Proveer una experiencia gastronómica local versátil que cubra desde la necesidad de volumen rápido diario hasta el consumo de especialidades de alto valor para compartir el fin de semana.
*   **El Cliente Ideal:** Familias tradicionales que buscan compartir (alta afluencia los fines de semana), así como oficinistas y trabajadores que consumen menús diarios. Existe una fuerte familiaridad del cliente con el servicio.
*   **Modelo de Negocio Actual:** Modelo 100% manual y no sistematizado. El control de inventario se lleva en papel (libro fiscal) para evitar la facturación directa ante la DIAN. Los ingresos se dividen en tickets de volumen (almuerzos/fast food), tickets medios (combos) y tickets altos (proteínas a la carta).

---

## 1.2. Planteamiento del Problema (Dolores del Negocio)

*   **Descontrol de Inventario (Warehouse Management):** Las compras de materias primas se realizan de forma diaria/semanal basándose en revisiones visuales y anotaciones en papel, sin un sistema formal que optimice los pedidos o genere pronósticos (*Forecast*). Fugas de capital por falta de control.
*   **Cuellos de Botella Operativos (Bottlenecks):** Falta de personal en días específicos para procesar materias primas (carnes, papas) y alto volumen de lavado de platos. No existen indicadores de tiempos en líneas de cocción, no se aplica teoría de colas, ni se aprovechan las "horas muertas" para reasignar tareas.
*   **Opacidad Financiera y Operativa:** Al no contar con un ERP o POS estructurado, se desconoce el gasto real y el rendimiento de los trabajadores. El negocio carece de datos limpios para implementar modelos de IA o Machine Learning a futuro.

---

## Fase 2: Requerimientos del Sistema (El 'To-Be')

### 2.1. Objetivos del ERP
1.  **Digitalización Interna:** Implementar un sistema centralizado de uso interno ("sombra") que digitalice el libro fiscal y elimine las fugas de capital.
2.  **Eficiencia Operativa:** Establecer parámetros cuantitativos para medir la eficiencia (tiempos de cocción/preparación), balancear la carga laboral y definir horarios fijos de preparación masiva (*batching*).
3.  **Data Driven:** Generar un repositorio de data histórica estructurada y limpia como base para futuros algoritmos de predicción de demanda.

### 2.2. Módulos Propuestos (Product Backlog)
*    **Módulo 1: POS y Ventas (Front-end)** - Interfaz ágil para comandos que separe transacciones por tipo de ticket y capture el momento exacto del pedido (para análisis de colas).
*   **Módulo 2: Control de Inventario Dinámico (Back-end)** - Descuento automático de insumos mediante recetas estandarizadas (*Bill of Materials*). Incluye alertas de reorden.
*   **Módulo 3: Dashboard Operativo y de RRHH** - Panel para monitorear horas pico vs. horas valle, identificando momentos óptimos para reasignar tareas de preparación al personal de servicio.
*   **Módulo 4: Dashboard Financiero** - Visualización de ingresos, COGS (Costo de Bienes Vendidos) y rentabilidad por principio de Pareto (80/20).

---

## Fase 3: Arquitectura Técnica y Bases de Datos

*   **Modelo de Datos:** Arquitectura relacional estructurada en **PostgreSQL** (desplegada vía **Supabase**) para asegurar transacciones ACID y facilitar la futura ingesta de datos hacia Python.
*   **Entidades Clave:** 
    *   `Inventario_Insumos`: Gestión de stock, mermas y umbrales de reorden.
    *   `Menu_Productos`: Categorización por tipo de ticket (Volumen, Medio, Alto).
    *   `Recetas_Estandar`: Tabla intermedia para el descuento exacto de porciones por platillo.
    *   `Registro_Tiempos`: Captura de inicio y fin de comandas para calcular *Cycle Time*.
    *   `Turnos_Actividad`: Mapeo de actividades de empleados para optimizar horas muertas.

---

## Fase 4: Plan de Implementación y Capacitación

*   **Estrategia de Adopción:** Capacitación sin fricción enfocada en personal empírico, utilizando interfaces visuales de alto contraste y flujos de trabajo con mínimos clics.
*   **Indicadores de Éxito (KPIs):** 
    *   Precisión en la conciliación de inventario teórico vs. real.
    *   Reducción del porcentaje de mermas.
    *   Medición del tiempo de ciclo en horas pico.
    *   Tasa de aprovechamiento de horas valle.

---

## Plan de Ejecución del Proyecto de Sistemas de Información

Para conectar la ingeniería de procesos con la analítica de datos, la hoja de ruta estratégica es la siguiente:

1.  **Diagnóstico Cuantitativo (Gemba Walk):** Levantar los tiempos estándar de la línea de cocción y el procesamiento de materias primas antes de programar. Usar estos datos para aplicar modelos de teoría de colas y evaluar la necesidad real de operarios en horas pico vs. días de semana.
2.  **Diseño de la Base de Datos:** Configurar instancias en Supabase asegurando un registro histórico granular (guardando "qué se vendió", "a qué hora ingresó" y "a qué hora salió").
3.  **Desarrollo Iterativo (ETL y Backend):** Construir scripts (ej. en Python) que gestionen la lógica de inventario y la limpieza de datos (*Data Cleaning*). Esto garantizará la calidad del dataset para el futuro Machine Learning.
4.  **Optimización de Recursos (Lean Manufacturing):** Diseñar un modelo de planificación de la demanda con la nueva data. Agendar "días fijos de producción" para carnes/papas, eliminando cuellos de botella diarios y distribuyendo tareas urgentes estratégicamente durante las horas valle.
