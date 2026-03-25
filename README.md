# Centralina di Accesso Dormiente

Sistema embedded per il controllo accessi basato su sensore di prossimità e inserimento codice Morse, progettato per ottimizzare consumi energetici e sicurezza.

---

## Descrizione

Questo progetto implementa una **centralina di accesso intelligente** che rimane in modalità *low-power* (sleep) e si attiva solo quando rileva una presenza entro 30 cm.

L’utente può inserire un codice segreto tramite pulsante utilizzando il **codice Morse**. Il sistema gestisce:

- Accesso autorizzato
- Tentativi errati
- Attivazione allarme
- Risparmio energetico avanzato tramite interrupt

---

## Funzionalità principali

- Rilevamento presenza con sensore ultrasuoni (HC-SR04)
- Visualizzazione messaggi su display 7 segmenti (4 digit)
- Inserimento codice Morse tramite pulsante
- Sblocco serratura tramite relè
- Sistema di allarme con buzzer
- Modalità sleep per ottimizzazione energetica
- Gestione completa tramite interrupt (NO delay)

---

## Logica di funzionamento

1. **Sleep Mode**
   - Sistema inattivo per risparmio energetico

2. **Rilevamento presenza**
   - Attivazione periodica tramite Watchdog Timer
   - Se distanza < 30 cm → sistema attivo

3. **Interazione utente**
   - Display mostra `"CIAO"`
   - Inserimento codice Morse:
     - Pressione breve → `.`
     - Pressione lunga → `_`

4. **Verifica codice**
   - Corretto → `"Ent"` + apertura serratura
   - Errato → `"Er n"` (tentativi rimanenti)

5. **Allarme**
   - Dopo troppi errori → `"8888"` lampeggiante + buzzer

6. **Ritorno a sleep**

---

## Architettura modulare

Il sistema è suddiviso in moduli indipendenti:

- Sensore HC-SR04
- Display 7 segmenti
- Gestione pulsante + Morse
- Controllo accesso
- Sistema di allarme
- Gestione sleep mode

---

## Gestione Interrupt

Il sistema è completamente **event-driven**, senza uso di `delay()`.

### Interrupt utilizzati:

- WDT (Watchdog Timer) → attivazione sensore
- INT0 (ECHO) → calcolo distanza
- INT1 (Pulsante) → input Morse
- Timer0 → gestione TRIG
- Timer1 → gestione display
- Timer2 → timing e timeout

---

## Parametri principali

| Parametro | Valore |
|----------|--------|
| Distanza attivazione | 30 cm |
| Debounce pulsante | 10–50 ms |
| Punto Morse | 100–300 ms |
| Linea Morse | 300–900 ms |
| Timeout input | ~6 sec |
| Frequenza display | ≥ 40 Hz |
| Frequenza buzzer | ~750 Hz |

---

## Componenti hardware

- Sensore ultrasuoni HC-SR04
- Display 7 segmenti (4 digit)
- Pulsante
- Relè
- Buzzer
- Microcontrollore (es. AVR)

---

## Soluzioni alternative

- LED / LED RGB → più semplice ma meno informativo
- Display LCD → più flessibile ma più complesso
- Sensore PIR → meno preciso ma più efficiente

---

## Simulazione

- Modalità normale: https://wokwi.com/projects/408737880547079169
- Modalità debug: https://wokwi.com/projects/421052364059217921

---

## Manuale utilizzo

| Messaggio | Significato |
|----------|------------|
| CIAO | Sistema pronto |
| Ent | Accesso consentito |
| Er n | Codice errato |
| 8888 | Allarme attivo |

---

## Competenze sviluppate

- Programmazione embedded
- Gestione interrupt
- Ottimizzazione energetica
- Progettazione modulare
- Interfacciamento hardware/software

---

## Conclusione

Sistema progettato per essere:

- efficiente   
- sicuro   
- reattivo 

