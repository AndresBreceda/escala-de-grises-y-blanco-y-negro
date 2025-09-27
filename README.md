# Descripción del Código BMP: Conversión a Gris y Blanco/Negro

Este programa en Python convierte una imagen **BMP de 24 bits sin compresión** en dos versiones nuevas:  

1. **Escala de grises** (`gris.bmp`)  
2. **Blanco y negro** (`blanco_negro.bmp`)  

Todo esto **sin usar librerías externas**, manipulando directamente los bytes del archivo.

---

## Flujo general del código

1. **Carga la imagen BMP** (subida por el usuario en Colab).  
2. **Lee los encabezados** del archivo BMP para obtener información del formato, tamaño y offset de los píxeles.  
3. **Lee los píxeles crudos (RGB)** fila por fila, teniendo en cuenta el padding de cada fila.  
4. **Convierte cada píxel**:  
   - Primero a **escala de grises** usando la fórmula de luminancia:  
     ```python
     Y = 0.299*R + 0.587*G + 0.114*B
     ```  
   - Luego aplica un **umbral** para generar la versión **blanco y negro**:  
     ```python
     if gris > threshold:
         blanco
     else:
         negro
     ```  
5. **Guarda dos archivos BMP nuevos**, copiando los headers originales y reemplazando solo los datos de los píxeles.  
6. **Descarga los archivos** en Colab para el usuario.

---

## Explicación de cada parte

### 1. Subida de archivo en Colab
```python
from google.colab import files
uploaded = files.upload()
entrada = list(uploaded.keys())[0]

