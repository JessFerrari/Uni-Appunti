---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks]]"
tags:
  - ML
  - DL
Creation: 2025-03-08
---
Gli __autoencoders__ sono sono delle [[Neural Networks|reti neurali]] allenate in [[Unsupervised Learning|non supervisionato]]  per riprodurre il proprio input come output. Si utilizzano per apprendere codifiche efficienti di dati senza etichette.

Un autoencoder è composto da :
- ***Encoder***: che trasforma un input in una rappresentazione più compatta
- ***Decoder***: che riconverte la rappresentazione compatta nel dato originale

Prendendo $f$ come funzione di decoding e $g$ come funzione di encoding, l'autoencoder può sere visto come una [[Funzioni|funzione composta]] $$r=f(g(x))$$
L'obiettivo è quello di minimizzare l'errore tra $r$ ed $x$.

Esistono due tipi di autoencoders:
- gli ***Under-complete***, in cui il layer nascosto ha meno unità rispetto all'input e costringe la rete a catturare solo le caratteristiche principali dei dati
- gli ***Over-complete***, in cui il layer nascosto è più grande rispetto all'input. Si applica la regolarizzazione per far si che l'output abbia proprietà aggiuntive rispetto all'input, come ad esempio il *denoising*.

Il **denoising** è un applicazione tipica degli autoencoder, con la quale la rete impara a ricostruire un'immagine partendo da una versione rumorosa.
![[Pasted image 20250308193418.png]]
