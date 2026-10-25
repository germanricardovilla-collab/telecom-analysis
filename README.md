# telecom-analysis
# 📱 Análisis de comportamiento de clientes — ConnectaTel

Análisis exploratorio de datos de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en **México y Colombia**, para entender cómo los clientes usan realmente los servicios móviles (llamadas y mensajes), detectar comportamientos atípicos y segmentar a los usuarios para optimizar la oferta comercial.

---

## 🎯 Objetivo

Responder las siguientes preguntas de negocio:

- ¿Qué segmentos de clientes muestran mayor o menor uso de llamadas y mensajes?
- ¿Qué usuarios presentan valores atípicos que puedan indicar comportamientos inusuales, fraude o errores de registro?
- ¿Cómo varía el uso según la edad y el tipo de plan contratado?
- ¿Qué patrones pueden ayudar a diseñar mejores planes y mejorar la satisfacción del cliente?

---

## 🗂️ Datasets

| Archivo | Registros | Descripción |
|---|---|---|
| `plans.csv` | 2 | Catálogo de planes (Básico y Premium): precio mensual, minutos, mensajes y GB incluidos, costo por excedente. |
| `users_latam.csv` | 4.000 | Información de clientes: edad, ciudad, fecha de registro, plan contratado y fecha de cancelación (churn). |
| `usage.csv` | 40.000 | Detalle de uso durante 2024: tipo de evento (llamada o mensaje), fecha, duración y longitud. |

---

## 🔄 Etapas del análisis

1. **Carga y exploración**: estructura, tipos de datos y dimensiones de cada dataset.
2. **Calidad de datos**: nulos, sentinels (`-999` en edad, `"?"` en ciudad) y fechas fuera de rango (año 2026).
3. **Limpieza**: imputación de edad con la mediana, conversión de sentinels a nulos, corrección de fechas imposibles y verificación de nulos MAR en `duration` y `length`.
4. **Estadísticas descriptivas**: agregación del uso por usuario (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`) y unión con la tabla de clientes.
5. **Visualización y outliers**: histogramas por plan, boxplots y detección de valores atípicos con el método IQR.
6. **Segmentación**: grupos por nivel de uso (Bajo / Medio / Alto) y por edad (Joven / Adulto / Adulto Mayor).
7. **Insight ejecutivo**: conclusiones y recomendaciones comerciales.

---

## 💡 Principales hallazgos

- **Uso medio** concentra el 73,6 % de los clientes, **Bajo uso** el 19,5 % y **Alto uso** el 7,0 %.
- **El perfil de uso es prácticamente igual en ambos planes**: los clientes Premium no consumen más que los Básico, aunque pagan más del doble.
- El consumo típico (5 mensajes, 4 llamadas y 20 minutos) está muy por debajo de lo que incluyen los planes, lo que indica una **oferta sobredimensionada**.
- Se identificó un **grupo aislado de usuarios con 130–155 minutos** de llamadas, que se recomienda auditar.
- La edad se distribuye de forma uniforme (18–79 años) y no determina el plan contratado.

**Recomendaciones:** crear un plan de entrada más económico, redefinir el valor del plan Premium con beneficios diferenciales, ofrecer planes a la medida para clientes de alto uso y fortalecer la validación de datos al momento del registro.

---

## 🛠️ Tecnologías

- Python 3
- pandas
- matplotlib
- seaborn
- Jupyter Notebook

---

## ▶️ Cómo ejecutar el notebook

### Opción 1: Google Colab (recomendado)

1. Abre el notebook `.ipynb` de este repositorio y haz clic en **Open in Colab**, o súbelo desde [colab.research.google.com](https://colab.research.google.com) en **File → Upload notebook**.
2. Sube los tres archivos CSV al panel de archivos de Colab (ícono de carpeta 📁).
3. En la celda de carga, cambia las rutas `/datasets/...` por el nombre de cada archivo:

   ```python
   plans = pd.read_csv('plans.csv')
   users = pd.read_csv('users_latam.csv')
   usage = pd.read_csv('usage.csv')
   ```

4. Ejecuta todas las celdas en orden: **Runtime → Run all**.

### Opción 2: Entorno local

```bash
git clone <URL-de-este-repositorio>
cd <nombre-del-repositorio>
pip install pandas matplotlib seaborn notebook
jupyter notebook
```

Coloca los CSV en la misma carpeta del notebook, ajusta las rutas como en la opción 1 y ejecuta todas las celdas.

---

## 🔁 Guía de reproducción

- Las celdas deben ejecutarse **en orden**, de arriba hacia abajo: cada paso depende de las variables creadas en el anterior.
- Si aparece un `NameError`, reinicia el kernel y ejecuta todo de nuevo (**Kernel → Restart & Run All**).
- Los resultados son deterministas: no hay muestreo aleatorio, así que cualquier persona obtendrá las mismas cifras.

---

## 👤 Autor

**Germán Ricardo Villamizar Villamizar**
Analista de datos  · Profesional en operaciones y gestión empresarial
