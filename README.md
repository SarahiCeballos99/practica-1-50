# practica-1-10
# Comparacion de dos numeros
// ============================================================================
// Autor: Verónica Sarahi Ceballos Reséndiz
// Fecha: 8 de abril de 2025
// Archivo: comparar.s
// Descripción: Compara dos números y escribe cuál es mayor usando syscalls
// Plataforma: Raspberry Pi OS 64-bits o Ubuntu ARM64
// ============================================================================

.section .data
msg_a:  .asciz "A es mayor\n"
msg_b:  .asciz "B es mayor\n"

.section .text
.global _start

_start:
    mov     x1, #10         // a = 10
    mov     x2, #7          // b = 7

    cmp     x1, x2          // comparar a y b
    bgt     imprimir_a      // si a > b salta a imprimir A
    b       imprimir_b      // si no, imprime B

imprimir_a:
    mov     x0, #1
    ldr     x1, =msg_a
    mov     x2, #11
    mov     x8, #64         // syscall write
    svc     #0
    b       salir

imprimir_b:
    mov     x0, #1
    ldr     x1, =msg_b
    mov     x2, #11
    mov     x8, #64
    svc     #0

salir:
    mov     x0, #0
    mov     x8, #93         // syscall exit
    svc     #0
