# ❄️ Clima Automatico – Risparmio Energetico | Energy-saving Climate Automation

---

## 🇮🇹 Descrizione

Questo blueprint automatizza la gestione del climatizzatore in base a:

- temperatura media di uno o più sensori di temperatura (puoi selezionarne più di uno, verrà usata la media)  
- presenza in casa (l’automazione funziona solo se almeno una persona è “home”)  
- stato delle finestre (tutte devono essere chiuse per far partire l’automazione)  
- fascia oraria configurabile (per esempio attivo solo dalle 08:00 alle 22:30)  

Permette di risparmiare energia alternando due modalità:

- **Climatizzazione** (quando la temperatura supera una soglia alta configurabile)  
- **Deumidificazione** (quando la temperatura scende sotto una soglia bassa configurabile)  

Se il climatizzatore è in modalità deumidificazione e la temperatura supera la soglia alta, l’automazione attiverà uno script per riportare il climatizzatore alla modalità climatizzazione.

Sono supportate notifiche opzionali sul dispositivo mobile e una gestione robusta degli stati tramite `input_boolean` per evitare accensioni e spegnimenti continui.

---

## 🇬🇧 Description

This blueprint automates AC control based on:

- average temperature from one or more temperature sensors (you can select multiple, average is used)  
- presence at home (automation runs only if at least one person is “home”)  
- window status (all must be closed to activate automation)  
- configurable time range (for example active only from 08:00 to 22:30)  

It saves energy by alternating two modes:

- **Climate mode** (when temperature rises above a configurable high threshold)  
- **Dehumidify mode** (when temperature drops below a configurable low threshold)  

If the AC is in dehumidify mode and temperature rises above the high threshold, the automation runs a script to return the AC to climate mode.

Optional mobile notifications are supported and robust state management via `input_boolean` avoids unnecessary toggling.

---

## ⚙️ Parametri del Blueprint | Blueprint Inputs

| Nome / Name                  | Descrizione / Description                                                    | Tipo / Type         | Esempio / Example                |
|-----------------------------|-----------------------------------------------------------------------------|---------------------|---------------------------------|
| **Sensori di temperatura**   | Uno o più sensori di temperatura (media calcolata)                          | Entity list (sensor) | `sensor.soggiorno_temp`          |
| **Persone presenti**          | Entità `person` da monitorare per presenza casa                             | Entity list (person) | `person.davide`, `person.chiara` |
| **Finestre da monitorare**    | Finestre (binary_sensor) che devono essere chiuse per attivare automazione  | Entity list (binary_sensor) | `binary_sensor.finestra_ingresso` |
| **Ora inizio**                | Ora di inizio automazione (formato 24h)                                   | Time                | `08:00:00`                      |
| **Ora fine**                  | Ora di fine automazione (formato 24h)                                     | Time                | `22:30:00`                     |
| **Temperatura alta**          | Soglia alta per attivare climatizzazione                                  | Number (°C)         | `27`                            |
| **Temperatura bassa**         | Soglia bassa per attivare deumidificazione                               | Number (°C)         | `25.5`                          |
| **Script climatizzazione**    | Script da eseguire per attivare la modalità climatizzazione                | Entity (script)     | `script.accendi_clima_pt`        |
| **Script deumidificatore**    | Script da eseguire per attivare la modalità deumidificazione               | Entity (script)     | `script.modalita_deumidificatore`|
| **Script ritorno climatizzazione** | Script per tornare da deumidificazione a climatizzazione              | Entity (script)     | `script.ritorno_climatizzazione`|
| **Boolean clima attivo**      | Input boolean che indica se il clima è attivo                             | Entity (input_boolean) | `input_boolean.clima_on`          |
| **Boolean deumidificatore attivo** | Input boolean che indica se la modalità deumidificazione è attiva      | Entity (input_boolean) | `input_boolean.deumidificatore_on`|
| **Dispositivo notifiche (opzionale)** | Dispositivo mobile per notifiche push                                 | Device (mobile_app) | `iphone_di_davide`               |

---

## 📋 Istruzioni per l’installazione

1. Crea gli `input_boolean` necessari (esempio da inserire in `configuration.yaml`):

```yaml
input_boolean:
  clima_on:
    name: Clima On
    initial: false
  deumidificatore_on:
    name: Deumidificatore On
    initial: false

## Import diretto in Home Assistant
### Importa il Blueprint direttamente in Home Assistant
[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Angelofsin666/ClimatePro/main/ClimatePro.yaml)
