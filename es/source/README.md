# Ejemplos de la Guía de Beej para  C

`exercises/` : soluciones para ejercicios `examples/` : código de los capítulos principales `examples/atomics/` : código del capítulo principal de atómicos`examples/threads/` : código del capítulo principal de hilos `man/` : código de las páginas de referencia

Ejecuta`make` en un directorio de código fuente en particular para compilar esas fuentes.

## Notas de compilación

Los archivos `Makefile` invocan `gcc` para compilar y se espera que se ejecuten en un sistema similar a Unix (por ejemplo, Linux, BSD, Mac OSX, Windows WSL).

enlace:

- Los programas matemáticos están enlazados con `-lm` .
- Los programas multhihilo están enlazados con `-lpthread` .
- Los programas atómicos están enlazados con `-latomic` .

No todas las funciones están necesariamente disponibles en todas las plataformas.
