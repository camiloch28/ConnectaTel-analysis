# ConnectaTel-analysis

onnectaTel: Análisis de Uso de Servicios Móviles (México y Colombia)
🎯 Objetivo del proyecto

ConnectaTel es una empresa de telecomunicaciones con operaciones en México y Colombia que necesita entender cómo sus clientes usan realmente los servicios móviles de llamadas y mensajes. Este proyecto analiza el comportamiento real de uso para responder cuatro preguntas clave del negocio:

¿Qué segmentos de clientes muestran mayor o menor uso de llamadas y mensajes?
¿Qué usuarios presentan valores atípicos que puedan indicar comportamientos inusuales, fraude o errores de registro?
¿Cómo varía el uso según la edad y el tipo de plan contratado?
¿Qué patrones pueden ayudar a diseñar mejores planes, optimizar la oferta y mejorar la satisfacción del cliente?

El resultado es un perfil de cliente limpio y segmentado, junto con recomendaciones comerciales accionables para el diseño de nuevos planes.

📂 Datasets utilizados

El análisis integra tres fuentes de datos:

plans.csv → Catálogo de los planes actuales de ConnectaTel: precio, minutos incluidos, GB incluidos y costo por unidad extra.
users_latam.csv → Información de cada cliente: edad, ciudad, fecha de registro, plan contratado y fecha de baja (churn), si aplica.
usage.csv → Detalle de la actividad real de cada usuario: llamadas (con su duración) y mensajes (con su longitud).

Estas tres fuentes se combinan para construir un perfil consolidado de cada cliente, cruzando quién es (users), qué contrató (plans) y cómo usa realmente el servicio (usage).

🔄 Etapas del análisis realizadas
Carga y exploración inicial de los tres datasets: revisión de estructura (.shape, .info()) y primeras filas de cada uno.
Identificación de problemas de calidad de datos:
Conteo y proporción de valores nulos por columna.
Detección de sentinels (valores inválidos disfrazados de datos reales), como -999 en la edad y "?" en la ciudad.
Revisión de fechas fuera de rango (por ejemplo, registros con año 2026, imposibles dado que los datos llegan hasta 2024).
Limpieza básica de datos:
Reemplazo del sentinel -999 en age por la mediana.
Reemplazo del sentinel "?" en city por valores nulos explícitos.
Conversión de columnas de fecha a formato datetime, marcando como nulas las fechas imposibles.
Verificación de que los nulos en duration y length son estructurales (MAR — Missing At Random), ya que dependen directamente del tipo de evento (llamada o mensaje), y no un error de captura.
Estadística descriptiva (summary statistics) de las variables clave, tanto numéricas (edad, mensajes, llamadas, minutos) como categóricas (tipo de plan).
Visualización y detección de outliers: histogramas por variable (segmentados por tipo de plan) y boxplots con cálculo de límites mediante el método IQR, para decidir con criterio si los valores extremos debían mantenerse o tratarse.
Segmentación de clientes:
Por nivel de uso: Bajo uso, Uso medio, Alto uso, según cantidad de llamadas y mensajes.
Por edad: Joven, Adulto, Adulto Mayor.
Visualización de la distribución de clientes en cada segmento.
Insight ejecutivo: conclusiones y recomendaciones comerciales basadas en los hallazgos de calidad de datos, segmentación y patrones de uso extremo.
▶️ Cómo ejecutar el notebook

Puedes abrir y correr este análisis directamente en Google Colab, sin instalar nada en tu computador:

Entra a Google Colab.
Ve a Archivo > Abrir notebook > GitHub.
Pega la URL de este repositorio.
Selecciona el notebook principal del proyecto en la lista que aparece.
El notebook se abrirá listo para ejecutar.

💡 Alternativa rápida: si el repositorio es público, puedes pegar directamente esta estructura de URL en tu navegador: https://colab.research.google.com/github/<usuario>/<repositorio>/blob/main/<nombre_del_notebook>.ipynb

🔁 Guía de reproducción
Ejecuta todas las celdas en orden, usando Entorno de ejecución > Reiniciar y ejecutar todo. El análisis depende de que cada paso se construya sobre el anterior (limpieza → estadística descriptiva → visualización → segmentación).
La carga de los tres datasets ya está incluida en las primeras celdas del notebook (plans.csv, users_latam.csv, usage.csv) — no necesitas descargar ni subir archivos manualmente antes de empezar.
Sigue el flujo documentado en las secciones del notebook, en este orden:
Carga y exploración de estructura.
Identificación de problemas de calidad (nulos, sentinels, fechas).
Limpieza básica de datos.
Estadística descriptiva por usuario.
Visualización de distribuciones y detección de outliers.
Segmentación de clientes por uso y por edad.
Insight ejecutivo final.
No se requieren pasos manuales adicionales entre celdas — todas las transformaciones (limpieza, agregación, merge) quedan guardadas en las variables del notebook y se usan automáticamente en los pasos siguientes.

⚠️ Si al ejecutar alguna celda aparece un error de tipo KeyError o NameError, generalmente significa que se corrió una celda fuera de orden o que el entorno se reinició a mitad de camino. La solución es reiniciar el entorno y ejecutar todas las celdas nuevamente desde el inicio.

🔗 Repositorio

Link al repositorio público del proyecto: https://github.com/camiloch28/ConnectaTel-analysis
https://colab.research.google.com/drive/1CsichDkbkjpjfWb1hDDPBmRTpUZadRc2?usp=sharing
