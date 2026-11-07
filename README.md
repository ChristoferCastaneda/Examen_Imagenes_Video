# Panoramas con ORB desde cero 📷

Pipeline completo para unir varias fotos en un **panorama**, implementado **desde cero con NumPy**, sin usar las funciones de OpenCV: detección de puntos, descriptores, emparejamiento, homografía y fusión.

## Overview

Cada etapa del pipeline está en su propio archivo:

| Paso | Archivo | Qué hace |
|---|---|---|
| 1. Detección | `FAST.py` | Pirámide de imágenes con suavizado gaussiano y detector de esquinas FAST |
| 2. Selección | `Harris.py` | Califica cada esquina con el score de Harris y se queda con las mejores, separadas entre sí |
| 3. Descripción | `BRIEF.py` | Descriptor binario BRIEF de 256 bits sobre parches de 31×31, con orientación |
| 4. ORB | `ORB.py` | Une FAST + Harris + BRIEF en un detector ORB |
| 5. Emparejamiento | `Hamming.py` | Empareja descriptores por distancia de Hamming, con la prueba de razón (el mejor contra el segundo mejor) |
| 6. Homografía | `Homografia.py` | Estima la homografía con normalización de Hartley, eliminación gaussiana y **RANSAC** |
| 7. Panorama | `Panorama.py` | Encadena homografías, calcula el lienzo, transforma con interpolación bilineal y mezcla las imágenes |
| 8. Recorte | `Rectificar.py` | Encuentra el mayor rectángulo válido, recorta los bordes vacíos y endereza el resultado |

Por ejemplo, entre las imágenes 1 y 2 se encontraron 124 parejas, 40 inliers y un error de 1.14 px (`resultados/matrices.txt`).

## Tecnologías

Python · NumPy · Pillow · Matplotlib

## Cómo correrlo

```bash
pip install numpy pillow matplotlib
python Panorama.py IMG/1.jpg IMG/2.jpg IMG/3.jpg
python Rectificar.py resultados/panorama.jpg
```

Sin argumentos, los scripts usan las imágenes de ejemplo. Los resultados (parejas, inliers, matrices y panorama) se guardan en `resultados/`.

## Equipo

Proyecto en equipo para la materia de Procesamiento de Imágenes y Video. Repositorio original: [ivanfmm/Examen_Imagenes_Video](https://github.com/ivanfmm/Examen_Imagenes_Video).

- Christofer Castañeda
- [ivanfmm](https://github.com/ivanfmm)
- [ivanGCetys](https://github.com/ivanGCetys)
