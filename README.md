# AI Comic Translator

820, 5, 1050, 340
830, 10, 1050, 220

problemas de la mascara de texto


Notebook para Google Colab que traduce páginas de cómics del inglés al español usando OCR, limpieza del texto original, traducción automática y reescritura dentro de la imagen.

## Qué hace

- Permite subir varias imágenes JPG/PNG.
- Permite subir un archivo ZIP con todas las páginas del cómic.
- También admite descargar imágenes desde una URL básica, si activas esa opción en la configuración.
- Detecta texto con preprocesamiento robusto (escala de grises, CLAHE, denoise y binarización adaptativa).
- Usa EasyOCR como motor principal, con opción de Tesseract o PaddleOCR.
- Reintenta OCR en regiones de baja confianza.
- Corrige texto OCR en inglés con diccionario + fuzzy matching (rapidfuzz).
- Añade corrección contextual (`correct_context`) con IA opcional (Gemini) y fallback local.
- Traduce con deep-translator usando GoogleTranslator.
- Borra el texto original con inpainting y escribe la traducción encima.
- Guarda todas las páginas traducidas y las comprime en un ZIP.

## Cómo usarlo en Colab

1. Abre el notebook [ai_comic_translator_colab.ipynb](ai_comic_translator_colab.ipynb) en Google Colab.
2. Ejecuta las celdas 1 a 5 en orden para cargar funciones y pipeline.
3. Ajusta opciones en la celda 6 (motor OCR, corrección, idioma, etc.).
4. Ejecuta la celda 6 para iniciar la carga y procesamiento.
5. Cuando aparezca el selector de archivos, sube una de estas opciones:
	- varias imágenes JPG/PNG, o
	- un archivo ZIP con las páginas del cómic.
6. Espera a que termine el OCR, corrección, traducción y renderizado.
7. Al finalizar, el notebook genera un ZIP con las imágenes traducidas y descarga el archivo automáticamente en Colab.

## Importante

- En Colab no basta con compilar o abrir el notebook: debes ejecutar las celdas.
- La subida de archivos ocurre durante la ejecución de la pipeline, no antes.
- Si no detecta texto en una página, esa página se copia igual al resultado final.

## Opciones útiles

Dentro del notebook puedes cambiar:

- `CONFIG['target_lang']`: idioma de salida, por ejemplo `es`, `fr`, `pt`, `it`.
- `CONFIG['source_lang']`: idioma de origen. Por defecto está en `en` para cómics en inglés.
- `CONFIG['ocr_engine']`: `easyocr`, `tesseract` o `paddle`.
- `CONFIG['ocr_min_confidence']`: por defecto `0.50` para filtrar OCR inestable.
- `CONFIG['enable_ocr_correction']`: activa/desactiva corrección de OCR.
- `CONFIG['use_ai_context_correction']`: activa corrección contextual con IA.
- `CONFIG['gemini_api_key']`: API key para corrección IA (opcional).
- `CONFIG['retry_low_confidence']`: reintento de OCR en cajas con baja confianza.
- `CONFIG['manual_box_mode']`: `ask`, `always` o `never` para seleccionar regiones manualmente por pagina.
- `CONFIG['keep_original_subtitle']`: activa o desactiva el subtítulo con el texto original.
- `CONFIG['use_gpu']`: si quieres intentar usar GPU cuando esté disponible.
- `CONFIG['use_url_input']`: para descargar imágenes desde una URL.

## Salida

El resultado se guarda en una carpeta temporal del entorno y también se empaqueta como ZIP para descarga directa.

## Recomendación práctica

Si quieres el flujo más estable, sube un ZIP con todas las páginas ordenadas. Si prefieres revisión manual, sube las imágenes una por una o selecciona varias al mismo tiempo.

## Solución de problemas

- Si ves un bloque largo de JavaScript al subir archivos en Colab, es normal: forma parte del mecanismo interno de `files.upload()`.
- En la primera ejecución, EasyOCR descarga modelos y puede tardar varios minutos.
- Si aparece un error similar a "not enough values to unpack (expected 3, got 2)", usa la versión actual del notebook y vuelve a ejecutar desde la primera celda.
- Si una ejecución falla a mitad, usa "Runtime > Restart runtime" y ejecuta todas las celdas en orden.
- Si quieres corrección contextual con IA, activa `use_ai_context_correction` y coloca `gemini_api_key`.
- Si una pagina no detecta todo el texto, usa `manual_box_mode='ask'` y marca manualmente regiones con 2 clics por globo.
- Si quieres máxima precisión en OCR, prueba:
	- `CONFIG['ocr_engine'] = 'easyocr'`
	- `CONFIG['enable_ocr_correction'] = True`
	- `CONFIG['retry_low_confidence'] = True`
