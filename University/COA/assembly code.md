Tags : #COA 
Date : 2026-07-22

---
; Take 3 numeric user inputs and Add them
.model small
.stack 100h

.data
msg1 db 0AH,0DH,"Give number 1: $"
msg2 db 0AH,0DH,"Give number 2: $"
msg3 db 0AH,0DH,"Give number 3: $"
msg4 db 0AH,0DH,"Result : $"

.code
main proc
    mov ax, @DATA
    mov ds, ax

    ; --- Get first number ---
    mov ah, 9
    lea dx, msg1
    int 21h

    mov ah, 1
    int 21h
    sub al, 30h
    mov bl, al

    ; --- Get second number ---
    mov ah, 9
    lea dx, msg2
    int 21h

    mov ah, 1
    int 21h
    sub al, 30h
    mov cl, al

    ; --- Get third number ---
    mov ah, 9
    lea dx, msg3
    int 21h

    mov ah, 1
    int 21h
    sub al, 30h
    mov dl, al

    ; --- Add them together ---
    add bl, bh
    add bl, cl
    add bl, 30h

    ; --- Display result ---
    mov ah, 9
    lea dx, msg4
    int 21h

    mov ah, 2
    mov dl, bl
    int 21h

    mov ah, 4ch
    int 21h
main endp
end main