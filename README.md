# EntertainmentHub - Último Sprint
Proyecto hecho por Lizeth Consuelo Bañuelos Ruelas.

# Descripción
Hub de entretenimiento donde se pueden ver películas, programas de televisión, las próximas películas, las películas más valoradas y populares, así como detalles de cada una, imágenes y el tráiler, elaborado utilizando Angular v17.3.11 y ASP.NET v8.0

# Objetivos
- Implementar backend con .Net
- Desarrollar la base de datos y normalización
- Implementación de kubernetes
- Implementación de docker

# Capturas de pantalla del proyecto ejecutándose
- ![Captura de pantalla (1590)](https://github.com/user-attachments/assets/f09fd0dd-60b2-4a76-adbc-b53b7fe31c5d)
- ![Captura de pantalla (1591)](https://github.com/user-attachments/assets/fb0ee1e8-986f-4789-9330-1c74ab1b442f)
- ![Captura de pantalla (1592)](https://github.com/user-attachments/assets/0d50ba11-146c-456a-9bc3-abcd1093c77c)
- ![Captura de pantalla (1593)](https://github.com/user-attachments/assets/309daff6-4219-4970-af4b-7951dbcd2a01)
- ![Captura de pantalla (1594)](https://github.com/user-attachments/assets/194a5937-4ac6-4d5f-80ca-43b4e5a438d1)

- `Lista de películas `
- ![Captura de pantalla (1595)](https://github.com/user-attachments/assets/3fd69d2c-a287-4f03-b42c-1403a11c2030)
- `Lista de series`
- ![Captura de pantalla (1596)](https://github.com/user-attachments/assets/4071b1f9-11b7-42a6-b8c9-c711bae6b43a)
- `Filtrar por géneros dando click en la etiqueta correspondiente`
- ![Captura de pantalla (1597)](https://github.com/user-attachments/assets/75c37989-fe47-4ada-812e-764745ba7f07)
- Detalles de las películas
- - ![Captura de pantalla (1605)](https://github.com/user-attachments/assets/dd180026-b181-4823-a861-2f8bf606f1dd)
  - ![Captura de pantalla (1606)](https://github.com/user-attachments/assets/3e944213-1ef7-42aa-b871-eb0f7f1308ae)
  - ![Captura de pantalla (1607)](https://github.com/user-attachments/assets/23f82d97-1827-4306-a026-7e1ecf8f8b3e)
  - ![Captura de pantalla (1608)](https://github.com/user-attachments/assets/79ca1c39-6dc9-4889-a60b-e0a3d722be42)



# Instrucciones
1. Obtener la url del repositorio: Hacer clic en el botón code y copiar la URL del repositorio.
2. Clonar repositorio: abrir la terminal y ejecutar el comando git clone <urldelrepositorio>.
3.
- Crea una base de datos en SQL Server en la cual añadas las tablas necesarias para la funcionalidad de la API (ver diagrama de la base de datos).
- Una vez creada, ahora en tu archivo `appsettings.json` crea tu ConnectionStrings  de la siguiente manera y cambia los datos necesarios para poder conectarte a tu base de datos creada anteriormente:
- ` "ConnectionStrings": {
    "DefaultConnection": "Data Source=your_server_name;Initial Catalog=your_database_name;Encrypt=False;Persist Security Info=True;User ID=your_server_user_name;Password=your_sqlserver_password;"
  } `
4. Instalar las dependencias necesarias, restaurarlas con `dotnet restore`, luego compilar el proyecto con dotnet build y posteriormente ejecutarlo con dotnet run
5. Si es necesario puedes ejecutar migraciones para actualizar tu base de datos.
6. Como puedes observar se implementó `kubernetes`, el repositorio ya cuenta con lo necesario para realizarlo, sin embargo es necesario configurar la conexión a base de datos utilizando un archivo `secret.yaml` donde incluirás datos sobre tu base de datos.
 - Lo puedes hacer de la siguiente manera :
 ```sh
 kubectl create secret generic my-secret\
 --from-literal=username='tu-usuario'\
 --from-literal=password='tu-contraseña'\
 ```

 - Tambien puede crear directamente un archivo `secrets.yaml` dentro de la carpeta `k8s`, el cual puede tener la siguiente estructura
 ```sh
apiVersion: v1
kind: Secret
metadata:
    name: <nombre de tu secret>
type: Opaque
data:
    ConnectionStrings__DefaultConnection: < tu conexión a base de datos en base 64>
```

- Para codificar tu datos sensible de base de datos, puede realizar lo siguiente 
 ```sh
echo -n 'mi-usuario' | base64
echo -n 'mi-contraseña' | base64
```
7. Una vez configurados los archivos necesarios, aplica los archivos de la siguiente manera asegurandote de que sea dentro de la carpeta donde se encuentren los archivos
 ```sh
kubectl apply -f k8s/
```
8. Una vez aplicado lo anterior puedes ejecutar el proyecto `dotnet run` y accede a la url especificada.
9. También puedes ejecutar los siguientes comandos para checar diferentes aspectos de la API  `kubectl get deployments`, así como  para obtener los servicios se puede ejecutar el siguiente  `kubectl get services` y `minikube service <el nombre del service>`
6. Al compilar el proyecto podras interactuar con la api mediante Swagger UI.

# Documentación de la API
- Para el proyecto se utilizó Swagger mediante el paquete Swashbuckle.AspNetCore en el cual al compilarla y navegar a la URL `https://localhost:<puerto>/swagger` (en este caso el puerto es 7249) en el que se documenta todos los enpoints de la API y se puede interactuar con ella.

# Dependencias y bibliotecas
-- .NET version 8.0
- Entity Framework Core -> versión: 8.0.7
- Entity Framework Core.SqlServer -> versión: 8.0.7
- Microsoft.EntityFrameworkCore.Tools -> versión: 8.0.7
- Swashbuckle.AspNetCore -> version: 6.4.0
Estos pueden ser añadidos  mediante los comandos `dotnet add package [package name]` o si estas utilizando Visual Studio puedde añadirlos usando `Nuget package manager`.
- SQL Server como base de datos, y opcional SQL Server Management Studio 20 (SSMS) para la gestión de la base de datos.
- [Docker] (https://www.docker.com/get-started)
- [Kubernetes] (https://kubernetes.io/docs/tasks/tools/) (kubectl)
- primeng -> version: 17.18.3
- rxjs -> version: 7.8.0

# Descripción de como se hizo
- Se comenzó con investigar, después al darnos el cambio a .Net me di a la tarea de averiguar cómo se podría realizar y al darme cuenta de su parecido con SpringBoot comprendí un poco más desde mi punto de vista, después me dispuse a ver videos de manejor de CRUD en .Net para comprender y tratar de implementarlo y darme un ejemplo, sin embargo me di cuenta que se necesitaba algo más profundo para poder desarrollar mi proyecto. 
- Una vez entendido un poco me dispuse a definir modelos, controllers, etc.
- Además, se investigó sobre como realizar la conexión con Angular para poder consumir la API en nuestro Frontend.
- Para impementar docker se investigó como se podría realizar y se encontró que existe una herrramienta de Docker Support para Visual Studio 2022, en al cual se puede generar directamente el Dockerfile, a partir de ello se verificó que funcionara configurando correctamente las credenciales de bases de datos y la creación correcta de la imagen necesaria, una vez hecho eso, se procedió a implementar kubernetes
# Reporte de Code Coverage y de testing
##Code coverage
- ![imagen](https://github.com/user-attachments/assets/561c0bb8-0640-4125-a5a8-9f34ba7ff953)
- ![imagen](https://github.com/user-attachments/assets/926ce2f0-6add-4ccb-a1e6-85ff38d67f3b)

# Diagrama de base de datos
![imagen](https://github.com/user-attachments/assets/ef0a819d-50a2-4be5-a7d5-b96978671155)


# Problemas conocidos
 - En el apartado donde se puede filtrar por géneros al seleccionar uno y otro tarda un poco y solo se puede realizar para películas.
 - En los elementos de la navbar "películas" y "series", al pasar entre uno y otro de manera seguida no funciona, se tiene que dar click a "inicio" o "géneros" para que funcione.
-  Al filtrar por géneros se pueden vser series y pelícuals, sin embargo sólo lo hice para películas, lo cual es un problema creo con mi routing, no está mal que lo haga, pero no debería.
-  
# Posibles mejoras
- Seguir mejores prácticas sobre APIs debido a que al pedir ayuda se me comentaron mejores prácticas al realizarlas y quisiera aplicarlo en el este mismo proyecto.
- Incluir actores y recomendación en base a la pelicula que se selecciona al ver detalles, ya que ya tengo la base de datos para implementarlo, pero por falta de tiempo no logré desarrollar el frontend correctamente.

# Retrospectiva

## ¿Qué hice bien?
- Se logró realizar la API para obtener películas y series de tv, con base de datos configurada de manera correcta (con contraseña y usuario), después de solucionar el error con SSMS en mi laptop.
- Conectar la API con Angular y consumirla para mostrar lo que se requería.
- Saber el momento en el cual pedir ayuda a otras personas conocidas con mayor conocimiento al bloquearme en algún problema.
- Implementar Docker y Kubernetes en mi backend, me fue más fácil hacerlo ahí que en el frontend, ahí sí logré hacerlo.
## ¿Qué no salió bien?
- Me faltó implementar el login con base de datos.
- La filtración de tvshows por género junto a películas, ya que solo lo hice para películas, se pueden ver series también filtradas sobre todo en Sci-fi pero creo que ocurre por un bug en mi código.
- Implementar docker en mi frontend en Angular, no logré encontrar el error y me bloqueé, necesito entender mejor docker y kubernetes sobre todo configuraciones, ya que es algo totalmente nuevo para mi, solo lo habia investigado mas nunca aplicado.
- Los tests, es la segunda vez que los realizo y aun siento que necesito aprender mucho para entender a elaborarlos correctamente.
## ¿Qué puedo hacer diferente?
- Administrar mejor mi tiempo ya que  al bloquearme al no entender algo no podía seguir, como me ocurrión con el login.
- Aprender más a fondo sobre .Net para implementar login, y mejores funcionalidades.
- Comprender de manera más granular docker y kubernetes ya que siento que solo entendí lo básico y solo pude aplicar kubernetes y docker a mi backend.
- 
