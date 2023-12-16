# Descripcion del proyecto

 **¿Cuál es un mejor plan?**

Trabajas como analista para el operador de telecomunicaciones Megaline. La empresa ofrece a sus clientes dos tarifas de prepago, Surf y Ultimate. El departamento comercial quiere saber cuál de los planes genera más ingresos para poder ajustar el presupuesto de publicidad.

Vas a realizar un análisis preliminar de las tarifas basado en una selección de clientes relativamente pequeña. Tendrás los datos de 500 clientes de Megaline: quiénes son los clientes, de dónde son, qué tarifa usan, así como la cantidad de llamadas que hicieron y los mensajes de texto que enviaron en 2018. Tu trabajo es analizar el comportamiento de los clientes y determinar qué tarifa de prepago genera más ingresos.

**Descripción de las tarifas**

Nota: Megaline redondea los segundos a minutos y los megabytes a gigabytes. Para **llamadas**, cada llamada individual se redondea: incluso si la llamada duró solo un segundo, se contará como un minuto. Para **tráfico web**, las sesiones web individuales no se redondean. En vez de esto, el total del mes se redondea hacia arriba. Si alguien usa 1025 megabytes este mes, se le cobrarán 2 gigabytes.

| Detalle         | **Surf** | **Ultimate** |
|-----------------|----------|----------    |
| Pago mensual    | 20 USD   | 70 USD       |
| Paquete         | 500 minutos al mes, 50 SMS y 15 GB de datos   | 3000 minutos al mes, 1000 SMS y 30 GB de datos  |
| Límite excedido | - 1 minuto: 3 centavos | - 1 minuto: 1 centavo |
|                 | - 1 SMS: 3 centavos    | - 1 SMS: 1 centavo|
|                 | - 1 GB de datos: 10 USD| - 1 GB de datos: 7 USD  |

### Tabla `users`
Almacena los datos de los usuarios:
- *user_id* — identificador único del usuario
- *first_name* — nombre del usuario
- *last_name* — apellido del usuario
- *age* — edad del usuario (en años)
- *reg_date* — fecha de suscripción (dd, mm, aa)
- *churn_date* — la fecha en que el usuario dejó de usar el servicio (si el valor es ausente, la tarifa se estaba usando cuando se recuperaron estos datos)
- *city* — ciudad de residencia del usuario
- *plan* — nombre de la tarifa

### Tabla `calls`
Almacena los datos sobre las llamadas:

- *id* — identificador único de la llamada
- *call_date* — fecha de la llamada
- *duration* — duración de la llamada (en minutos) - **Estos se redondean hacia minutos, 1 seg = 1 min**.
- *user_id* — el identificador del usuario que realiza la llamada

### Tabla `messages`
Almacena los datos sobre los SMS:

- *id* — identificador único del SMS
- *message_date* — fecha del SMS
- *user_id* — el identificador del usuario que manda el SMS

### Tabla `internet`
Almacena los datos sobre las sesiones web:

- *id* — identificador único de la sesión
- *mb_used* — el volumen de datos gastados durante la sesión (en megabytes)
- *session_date* — fecha de la sesión web
- *user_id* — identificador del usuario

### Tabla `plans`
Almacena los datos sobre las tarifas:

- *plan_name* — nombre de la tarifa
- *usd_monthly_fee* — pago mensual en dólares estadounidenses
- *minutes_included* — minutos incluidos al mes
- *messages_included* — SMS incluidos al mes
- *mb_per_month_included* — datos incluidos al mes (en megabytes) - **Estos se redondean hacia arriba**.
- *usd_per_minute* — precio por minuto tras exceder los límites del paquete (por ejemplo, si el paquete incluye 100 minutos el operador cobrará el minuto 101)
- *usd_per_message* — precio por SMS tras exceder los límites del paquete
- *usd_per_gb* — precio por gigabyte de los datos extra tras exceder los límites del paquete (1 GB = 1024 megabytes)

# Conclusión 

1. En la preparacion de datos, tuvimos que comprender la informacion que nos ofrecia cada tabla y como estos valores se relacionaban con el objetivo que teniamos de saber cual de los planes genera mas ingresos, para ello corregimos algunos datos de manera que sean faciles de trabajar y analizar.
2. Luego de tener las tablas revisadas y limpias, agrupamos los datos de cada tabla por usuario y mes con el fin de unificarlos en un solo dataframe para tener la informacion relevante y completa en una sola vista. Esto nos ayudo a identificar que habian usuarios que se excedieron con los paquetes de minutos, mensajes e internet que los planes ofrecian mensualmente, lo que alteraria en el ingreso mensual de cada usuario en cada plan.
3. Seguidamente, estudiamos la distribucion estadistica del consumo de los usuarios y los ingresos. A partir de ello, se concluyo que el plan "Ultimate" tiene mayores ingresos que "Surf" unicamente porque su costo del plan es superior ya que, el plan de "Surf" es el que genera mayores ingresos por consumos adicionales a los disponibles contratados. Por lo tanto, se puede sugerir promover a que estos usuarios de "Surf" que exceden en sus consumos migren al plan "Ultimate" y asi crecer los ingresos de este plan.
4. Finalmente, se formularon 2 hipotesis de 2 colas comparando las medias de 2 poblaciones donde se rechazaron las hipotesis nulas aceptando las siguientes tesis: 
    - El ingreso promedio de los usuarios de los planes de llamada Ultimate y Surf son diferentes.
    - El ingreso promedio de los usuarios del área NY-NJ son diferentes de los usuarios de otras regiones.
