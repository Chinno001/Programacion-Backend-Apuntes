# Unidad 1 · Tecnologías del lado del servidor

> Resumen de apuntes
> Basado en la Guía de Contenido de la Unidad 1.

---

## 1. Modelo Cliente-Servidor

- **Cliente** (navegador): presenta la información al usuario → **Front End**
- **Servidor**: gestiona lógica de negocio, acceso a datos y seguridad → **Back End**
- Ambos se comunican mediante un **protocolo común**

---

## 2. Protocolo HTTP / HTTPS

HTTP define el intercambio de información mediante un ciclo **solicitud → respuesta**.
HTTPS = HTTP + cifrado criptográfico.

### Métodos HTTP

| Método | Acción |
|--------|--------|
| `GET`    | Solicita información, no modifica datos |
| `POST`   | Envía datos para crear un nuevo recurso |
| `PUT`    | Actualiza un recurso existente |
| `DELETE` | Elimina un recurso |

### Códigos de estado comunes

- `200` → Éxito
- `404` → Recurso no encontrado
- `500` → Error interno del servidor

---

## 3. DNS y Hosting

- **DNS** (Domain Name System): traduce dominios legibles (`agroconecta.cl`) en direcciones IP
- **Hosting**: infraestructura que almacena y ejecuta los archivos/datos de la app, manteniéndola accesible

---

## 4. Patrón MVC → adaptación MVT en Django

El patrón **MVC** separa responsabilidades: Modelo (datos), Vista (presentación), Controlador (coordina).

Django lo adapta como **MVT**:

| MVC tradicional | MVT Django | Rol |
|---|---|---|
| Modelo | **Model** | Gestiona los datos (el *qué*) |
| Controlador | **View** | Lógica de negocio (el *cómo*) |
| Vista | **Template** | Estructura HTML (el *dónde*) |

> ⚠️ **Ojo con la confusión de nombres:** en Django, la `View` cumple el rol del Controlador (procesa lógica), y el `Template` cumple el rol de la Vista tradicional (presentación).

### Flujo de una petición

1. El navegador envía un `GET`
2. `urls.py` enruta la petición a la View correspondiente
3. La View consulta al Model
4. El Model consulta la base de datos y devuelve los datos
5. La View pasa los datos como contexto al Template
6. El Template genera el HTML dinámico
7. Se devuelve la respuesta al navegador

---

## 5. Entorno virtual e instalación de Django

```bash
# Crear entorno virtual
python -m venv nombre_entorno

# Activar (Mac/Linux)
source nombre_entorno/bin/activate

# Activar (Windows)
nombre_entorno\Scripts\activate

# Instalar Django
pip install django

# Crear proyecto
django-admin startproject nombre_proyecto
```

`settings.py` centraliza toda la configuración del proyecto.

### Buena práctica: `requirements.txt`

```bash
# Registrar dependencias actuales
pip freeze > requirements.txt

# Replicar el entorno en otra máquina
pip install -r requirements.txt
```

Garantiza que el proyecto funcione igual en cualquier máquina (evita el clásico "en mi computador sí funcionaba").

---

## 6. Paquetes externos relevantes

| Paquete | Función | Caso de uso |
|---|---|---|
| `Pillow` | Procesamiento de imágenes | Redimensionar/validar fotos subidas |
| `python-decouple` | Gestión de variables de entorno | Ocultar contraseñas de BD |
| `django-cors-headers` | Políticas de acceso entre dominios | Permitir peticiones desde un Frontend separado |
| `requests` | Peticiones HTTP hacia otros servidores | Conectarse a APIs de terceros |

---

## 7. Django: Models, Views y Templates

### Models

Clase Python que hereda de `models.Model`. Cada atributo = una columna en la tabla.

```bash
python manage.py makemigrations
python manage.py migrate
```

### Views

Recibe la petición, interactúa con el Model, elige el Template:

```python
def lista_productos(request):
    productos = Producto.objects.all()
    return render(request, 'lista.html', {'productos': productos})
```

### Templates

HTML con lenguaje de marcado Django: `{% %}` para lógica, `{{ }}` para variables.

```html
{% for producto in productos %}
    <li>{{ producto.nombre }}</li>
{% endfor %}
```

---

## 8. IA como copiloto del desarrollo

La IA ayuda a generar código, sugerencias y datos de prueba — **pero el criterio técnico del desarrollador siempre manda**.

### ❌ Prompt mal formulado
> "Hazme datos para productos."
Ambiguo: no define formato, cantidad, atributos ni dominio.

### ✅ Prompt bien formulado
> "Genera un archivo JSON con 5 registros de productos para una tienda de insumos agrícolas. Cada producto debe incluir: id (entero), nombre (string), precio (float en CLP), unidad_medida (string) y disponibilidad (boolean). Devuelve solo el JSON válido sin comentarios."

### ✅ Checklist de validación para código generado por IA

- [ ] ¿Cumple exactamente el requerimiento pedido?
- [ ] ¿Introduce alguna vulnerabilidad (datos sin validar, contraseñas expuestas)?
- [ ] ¿Lo entiendes completamente antes de implementarlo?
- [ ] ¿Funciona correctamente con los datos reales del proyecto?

---

## 9. Conclusión (Cierre de la unidad)

- HTTP regula cómo se comunican los sistemas
- MVT organiza el código de forma mantenible
- Django provee herramientas para no partir desde cero
- La IA acelera el desarrollo, pero la **responsabilidad de validar el código siempre recae en el desarrollador**

---

## 📚 Recursos complementarios

- [Django Docs — Getting started](https://docs.djangoproject.com/es/stable/intro/)
- [MDN Web Docs — Protocolo HTTP](https://developer.mozilla.org/es/docs/Web/HTTP)
- [Real Python — Desarrollo web con Python](https://realpython.com/tutorials/web-dev/)
- [GeeksforGeeks — MVC vs MVT](https://www.geeksforgeeks.org/software-engineering/difference-between-mvc-and-mvt-design-patterns/)
- [Python venv docs](https://docs.python.org/3/library/venv.html)
