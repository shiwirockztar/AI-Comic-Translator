# AI Comic Translator

Notebook para Google Colab que traduce páginas de cómics del inglés al español usando OCR, limpieza del texto original, traducción automática y reescritura dentro de la imagen.

## Qué hace

- Permite subir varias imágenes JPG/PNG.
- Permite subir un archivo ZIP con todas las páginas del cómic.
- También admite descargar imágenes desde una URL básica, si activas esa opción en la configuración.
- Detecta texto con EasyOCR y usa Tesseract como respaldo.
- Borra el texto original con inpainting y escribe la traducción encima.
- Guarda todas las páginas traducidas y las comprime en un ZIP.

## Cómo usarlo en Colab

1. Abre el notebook [ai_comic_translator_colab.ipynb](ai_comic_translator_colab.ipynb) en Google Colab.
2. Ejecuta la celda de instalación de dependencias.
3. Ejecuta la celda de configuración y procesamiento.
4. Cuando aparezca el selector de archivos, sube una de estas opciones:
	- varias imágenes JPG/PNG, o
	- un archivo ZIP con las páginas del cómic.
5. Espera a que termine el OCR, la traducción y el renderizado.
6. Al finalizar, el notebook genera un ZIP con las imágenes traducidas y descarga el archivo automáticamente en Colab.

## Importante

- En Colab no basta con compilar o abrir el notebook: debes ejecutar las celdas.
- La subida de archivos ocurre durante la ejecución de la pipeline, no antes.
- Si no detecta texto en una página, esa página se copia igual al resultado final.

## Opciones útiles

Dentro del notebook puedes cambiar:

- `CONFIG['target_lang']`: idioma de salida, por ejemplo `es`, `fr`, `pt`, `it`.
- `CONFIG['keep_original_subtitle']`: activa o desactiva el subtítulo con el texto original.
- `CONFIG['use_gpu']`: si quieres intentar usar GPU cuando esté disponible.
- `CONFIG['use_url_input']`: para descargar imágenes desde una URL.

## Salida

El resultado se guarda en una carpeta temporal del entorno y también se empaqueta como ZIP para descarga directa.

## Recomendación práctica

Si quieres el flujo más estable, sube un ZIP con todas las páginas ordenadas. Si prefieres revisión manual, sube las imágenes una por una o selecciona varias al mismo tiempo.