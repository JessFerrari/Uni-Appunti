---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Dipendenze funzionali]]"
tags:
  - BD
  - todo
Creation: 2024-02-24
---
 ![[Pasted image 20240224231336.png]]

Titolo, Anno -> Semestre
Dipartimento -> Indirizzo
Codcorso -> Titolo, CFU, Anno, semestre, CodiceDocente, dipartimento, Indirizzo 
	è chiave
Titolo -> CFU


![[Pasted image 20240224231630.png]]

---
![[Pasted image 20240224231839.png]]

# [[Dipendenze funzionali#Dipendenze funzionali atomiche|Dipendenze funzionali atomiche]]
![[Pasted image 20240224231949.png]]

## ridondanza
![[Pasted image 20240224232038.png]]


---

![[Pasted image 20240224232108.png]]
`PrezzoTot` è ripetuto in ogni tupla che si riferisce allo stesso kit
`PrezzoComp` è ripetuto in ogni tupla che ha lo stesso valore di `Tipo` e `Fornitore`
`Componente` è ripetuto in ogni tupla che ha lo stesso `Tipo`
**Dipendenze funzionali :**
- `Tipo`->`Componente`
- `Kit`->`PrezzoTot`
- `Kit, Tipo`->`PrezzoComponente`, `Quantcomp`, `Fornitore`

## Decomposizione
![[Pasted image 20240224232925.png]]


--- 
# sintassi
![[Pasted image 20240224233054.png]]![[Pasted image 20240224233110.png]]

---
![[Pasted image 20240224233208.png]]![[Pasted image 20240224233218.png]]

![[Pasted image 20240224233233.png]]![[Pasted image 20240224233254.png]]
![[Pasted image 20240224233307.png]]
![[Pasted image 20240224233323.png]]

---

![[Pasted image 20240225015726.png]]