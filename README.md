# Optimizacion-Del-Almacenamiento

import os
import shutil

def analizar_espacio(directorio):
    # Obtener el espacio en disco del directorio
    total, usado, libre = shutil.disk_usage(directorio)
    return total, usado, libre

def sugerir_eliminacion(directorio, tam_limite=500):  # Tamaño límite en MB
    archivos_innecesarios = []
    for carpeta_actual, _, archivos in os.walk(directorio):
        for archivo in archivos:
            ruta_archivo = os.path.join(carpeta_actual, archivo)
            tam_archivo_mb = os.path.getsize(ruta_archivo) / (1024 * 1024)  # Convertir a MB
            if tam_archivo_mb > tam_limite:
                archivos_innecesarios.append(ruta_archivo)
    return archivos_innecesarios

def mover_archivos(origen, destino):
    # Mover archivos del almacenamiento principal a otro directorio
    try:
        shutil.move(origen, destino)
        print("Archivos movidos exitosamente.")
    except Exception as e:
        print(f"Error al mover archivos: {e}")

if _name_ == "_main_":
    directorio_a_analizar = "C:\Program Files"  # Reemplaza con la ruta que deseas analizar

    total_espacio, espacio_usado, espacio_libre = analizar_espacio(directorio_a_analizar)
    print(f"Espacio total: {total_espacio / (1024 * 1024 * 1024):.2f} GB")
    print(f"Espacio usado: {espacio_usado / (1024 * 1024 * 1024):.2f} GB")
    print(f"Espacio libre: {espacio_libre / (1024 * 1024 * 1024):.2f} GB")

    archivos_innecesarios = sugerir_eliminacion(directorio_a_analizar)
    if archivos_innecesarios:
        print("\nArchivos sugeridos para eliminación:")
        for archivo in archivos_innecesarios:
            print(archivo)

    # Dirección de destino para mover archivos (cambia esto a la ruta que desees)
    destino_mover = "ruta/del/directorio/de/destino"
    mover_archivos(directorio_a_analizar, destino_mover)
