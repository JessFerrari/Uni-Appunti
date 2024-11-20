---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
Ogni componente dello schema (risorsa) può essere protetta (tabelle, attributi, viste, domini, ecc.).

Il possessore della risorsa (colui che la crea) assegna dei privilegi agli altri utenti.

Un utente predefinito ($\_system$) rappresenta l’amministratore della base di dati ed ha completo accesso alle risorse.

Ogni privilegio è caratterizzato da:  
- la risorsa a cui si riferisce  
- l’utente che concede il privilegio 
- l’utente che riceve il privilegio 
- l’azione che viene permessa sulla risorsa 
- se il privilegio può esser trasmesso o meno ad altri utenti

*Tipi di privilegi*: 
- SELECT: lettura di dati 
- INSERT `[(Attributi)]`: inserire record (con valori non nulli per gli attributi) 
- DELETE: cancellazione di record 
- UPDATE `[(Attributi)]`: modificare record (o solo gli attributi) 
- REFERENCES `[(Attributi)]`: definire chiavi esterne in altre tabelle che riferiscono gli attributi. 
- WITH GRANT OPTION: si possono trasferire i privilegi ad altri utenti


Chi crea lo schema della BD è l'unico che può fare CREATE, ALTER e DROP  

Chi crea una tabella stabilisce i modi in cui altri possono farne uso: 
```MYSQL
GRANT Privilegi 
ON Oggetto 
TO Utenti [ WITH GRANT OPTION ]
```

Per concedere un privilegio ad un utente: 
```MYSQL
grant < Privileges | all privileges > on Resource to Users [ with grant option ] 
```

`grant option` specifica se ha il privilegio di propagare il privilegio ad altri utenti 
	Es.: 
```MYSQL
grant select on Department to Stefano 
```

Per revocare il privilegio: 
```MYSQL
revoke Privileges on Resource from Users [ restrict | cascade ]
```

La revoca deve essere fatta dall’utente che aveva concesso I privilegi.

`restrict` (di default) specifica che il comando non deve essere eseguito qualora la revoca dei privilegi all’utente comporti qualche altra revoca (dovuta ad un precedente grant option) 
`cascade` invece forza l’esecuzione del comando.

Bisogna fare attenzione alle reazioni a catena

Chi definisce una tabella o una VIEW ottiene automaticamente tutti i privilegi su di esse, ed è l’unico che può fare un DROP e può autorizzare altri ad usarla con GRANT. 
Nel caso di viste, il "creatore" ha i privilegi che ha sulle tabelle usate nella definizione. 
Le autorizzazioni si annullano con il comando:  
```MYSQL
REVOKE [ GRANT OPTION FOR ] Privilegi ON Oggetto FROM Utenti [ CASCADE ] 
```

Quando si toglie un privilegio a U, lo si toglie anche a tutti coloro che lo hanno avuto solo da U.

![[Pasted image 20240224030631.png]]

## Grafo delle autorizzazioni

![[Pasted image 20240224030720.png]]
Se un nodo N ha un arco uscente con un privilegio, allora esiste un cammino da SYSTEM a N con ogni arco etichettato dallo stesso privilegio + WGO. 

Effetto del REVOKE, ad es.
	I: REVOKE SELECT ON R FROM A CASCADE 
e poi 
	I: REVOKE SELECT ON R FROM C CASCADE

![[Pasted image 20240224030738.png]]