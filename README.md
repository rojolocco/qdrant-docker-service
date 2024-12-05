# Qdrant en Producción

Este directorio contiene la configuración para desplegar **Qdrant** en un entorno de producción utilizando Docker Compose. **Qdrant** es un motor de búsqueda vectorial que permite almacenar y buscar embeddings de manera eficiente.

---

## **Estructura de Archivos**

```plaintext
qdrant/
├── .env.prod                  # Variables de entorno para producción (opcional)
├── docker-compose.yml         # Docker Compose para despliegue en producción
```

---

## **Requisitos Previos**

1. **Docker y Docker Compose** deben estar instalados.
2. **Red compartida** (`caddy_network`) creada previamente:

   ```bash
   docker network create caddy_network
   ```

---

## **Configuración de Variables de Entorno**

Las variables de entorno para este despliegue se definen directamente en el archivo `docker-compose.yml`. Sin embargo, puedes optar por moverlas a un archivo `.env.prod` si prefieres.

### **Variables Importantes**

- `QDRANT__SERVICE__GRPC_PORT`: Define el puerto gRPC para Qdrant.
- `QDRANT__STORAGE__PATH`: Ruta para el almacenamiento persistente de Qdrant.

---

## **Uso**

### **Levantar el servicio en producción**

Para levantar **Qdrant** en producción, utiliza el siguiente comando:

```bash
docker-compose -f docker-compose.yml up -d
```

### **Detener el servicio**

Para detener el servicio:

```bash
docker-compose -f docker-compose.yml down
```

### **Verificar el estado del contenedor**

Para verificar que el contenedor de **Qdrant** está corriendo:

```bash
docker ps
```

---

## **Acceso a Qdrant**

Puedes acceder a **Qdrant** a través de su API REST en `http://<tu_ip>:6333`. Esta API te permite interactuar con las colecciones, agregar datos, y realizar búsquedas vectoriales.

---

## **Persistencia de Datos**

Los datos de **Qdrant** se almacenan en el volumen `qdrant_storage`. Este volumen asegura que los datos no se pierdan al detener o reiniciar el contenedor.

### **Ubicación del Volumen**

El volumen se define en el archivo `docker-compose.yml` y es gestionado por Docker.

Para eliminar los datos almacenados:

```bash
docker volume rm qdrant_storage
```

> **Advertencia**: Esto eliminará todos los datos almacenados en Qdrant.

---

## **Solución de Problemas**

### **Error: `Cannot connect to Qdrant`**

- Verifica que el contenedor de **Qdrant** esté en ejecución y accesible en el puerto `6333`.
- Asegúrate de que el servicio esté conectado a la red correcta (`caddy_network`).

### **Advertencia: `Storage path not found`**

- Asegúrate de que el volumen `qdrant_storage` está correctamente montado y que la ruta `/qdrant/storage` sea accesible.

---

## **Contribución**

Si deseas mejorar esta configuración o agregar nuevas funcionalidades, sigue estos pasos:

1. Haz un fork de este repositorio.
2. Realiza tus cambios en una nueva rama.
3. Envía un pull request con tus mejoras.

---

## **Licencia**

Este proyecto está bajo la licencia MIT. Consulta el archivo `LICENSE` para más detalles.
