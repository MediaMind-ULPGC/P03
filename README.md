# Práctica 3: Procesamiento de imágenes.

Integrantes:
- Gerardo León Quintana
- Susana Suárez Mendoza

## Ejercicio 1.
El negativo de una imagen es el resultado de aplicar la siguiente operación: 255-imagen(i,j). Aplica esta operación sobre la imagen2.png y, posteriormente, crea un video que vaya mezclando las dos imágenes por columnas, de forma que aparezca primero el negativo de la imagen y vaya apareciendo poco a poco la imagen original. El número de iteraciones debe ser igual al ancho de la imagen y en cada una se debe ir desplazando una columna a la derecha la imagen original sobre el negativo. Guarda el vídeo con el nombre vídeo2.mp4. 
**Flujo del programa**
1. **Calcular el negativo** de la imagen segun la fórmula especificada.
$$ negativo(i,j) = 255 - imagen(i,j) $$
```python
img = cv.imread('images/imagen2.png')
negative_image = 255 - img
```
2. **Generación del vídeo**. El número de iteraciones será igual al ancho de la imagen, y en cada iteración, la imagen original se desplazará una columna a la derecha sobre el negativo. En cada iteración se guarda el frame del video.

```python
for i in range(width):
    img_act = img.copy()
    img_act[:, i:] = negative_image[:, i:]
    video_writer.write(img_act)
```
3. **Mostrar el resultado final** en bucle.
```python
while True:
    ret, frame = video.read()
    if not ret:
        video.set(cv.CAP_PROP_POS_FRAMES, 0)
        continue
    cv.imshow('Original Image', img)
    cv.imshow('Video', frame)
    if cv.waitKey(1) & 0xFF == ord('q'):
        break
```
<div align="center">
  <img src="gif/video2.gif" alt="Gif Ejercicio 1" />
</div>

## Ejercicio 2. 
Ecualiza el histograma de la imagen imagen3.png y luego elimina el ruido utilizando un filtro bilateral con un diámetro d=10 y valores de sigma de 11 y 11. Guarda el resultado como imagen3_salida.png.
