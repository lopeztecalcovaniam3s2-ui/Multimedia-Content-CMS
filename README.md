# Multimedia-Content-CMS
Busqueda eficiente por texto (text index) infiltrado por etiquetas (multikey index)

👥 # Roles de trabajo

"
|Rol|Nombre técnico|Responsabilidad principal|
|---|--------------|-------------------------|
|1|Scrum Master. Arzabal Flores Adolfo|
|2|The Data Modeler. López Tecalco Vania|Arquitecto JSON. Define la estructura del documento. Decide qué datos se "embeben" (embed) y cuáles se referencian. Escribe el diagrama en Mermaid.js.
|3|The Query Developer. Gil Guzman Guillermo|Constructor MQL. Traduce las preguntas de negocio ("¿Cuántos usuarios...?") a código MongoDB (db.collection.find(...)). Es quien más interactúa con la IA para optimizar filtros.
|4|The Integration Specialist. Olivares Luengas Tadeo de Jesús|Configurador del Entorno. Se encarga de crear el Cluster en Atlas o la conexión en Compass. Gestiona los índices básicos y asegura que la conexión no falle. Administra el repositorio GitHub.
|5|The Data Seeder/ QA. Damian Tepole Casimiro|Generador de Caos. Crea los datos de prueba (archivos JSON ficticios) usando herramientas de IA o Mockaroo. Valida que las consultas del Developer funcionen con datos reales y reporta "bugs".
