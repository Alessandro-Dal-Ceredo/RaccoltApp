# RaccoltApp

RaccoltApp è un'applicazione Android sviluppata per supportare la gestione quotidiana della raccolta differenziata e la comunicazione tra cittadini e servizio di raccolta. Il progetto integra calendario, mappa dei punti di raccolta, guida al conferimento dei rifiuti, segnalazioni e profilo utente.

Il progetto è stato realizzato in Java con Android SDK, Material Components, Google Maps, Firebase Cloud Messaging e Retrofit per la comunicazione con un backend Supabase.

## Funzionalità principali

- Calendario della raccolta con consultazione dei giorni di conferimento.
- Mappa interattiva dei punti di raccolta caricati da file GPX, con marker raggruppati e filtri per tipologia di bidone.
- Guida "Dove lo butto?" con categorie espandibili per carta, plastica, vetro, organico e secco indifferenziato.
- Sistema di segnalazioni con elenco, filtri per comune, priorità e tipo di problema.
- Creazione di nuove segnalazioni con descrizione, posizione e immagini.
- Autenticazione utente tramite Supabase.
- Profilo utente con gestione del comune associato.
- Notifiche push tramite Firebase Cloud Messaging, con iscrizione ai topic legati al comune dell'utente.

## Stack tecnico

- Linguaggio: Java
- Build system: Gradle
- UI: Android Views, ViewBinding, Material Components
- Navigazione: AndroidX Navigation
- Mappe: Google Maps SDK e Google Maps Android Utils
- Posizione: Google Play Services Location
- Backend/API: Supabase REST/Auth
- Networking: Retrofit e Gson
- Notifiche: Firebase Cloud Messaging

## Struttura del progetto

```text
.
├── app/
│   ├── src/main/java/it/unive/raccoltapp/
│   │   ├── model/          # Modelli dati e utility applicative
│   │   ├── network/        # API manager, Retrofit service e FCM
│   │   └── ui/             # Activity, Fragment e adapter UI
│   ├── src/main/res/
│   │   ├── layout/         # Layout XML delle schermate
│   │   ├── drawable/       # Icone e asset grafici
│   │   ├── navigation/     # Grafo di navigazione
│   │   └── raw/            # Dataset GPX dei bidoni
│   └── build.gradle
├── build.gradle
├── gradle.properties
├── settings.gradle
└── check_setup.sh
```

## Schermate principali

- `MainActivity`: contiene la navigazione principale e la bottom navigation.
- `CalendarFragment`: mostra il calendario della raccolta.
- `MapFragment`: visualizza la mappa dei bidoni e applica i filtri per materiale.
- `ReportsFragment`: mostra le segnalazioni e permette l'accesso alla creazione di nuove segnalazioni.
- `AddReportFragment`: gestisce l'invio di una nuova segnalazione.
- `WasteGuideFragment`: mostra la guida al conferimento dei rifiuti.
- `ProfileFragment`, `LoginFragment`, `SignUpFragment`: gestiscono profilo, login e registrazione.

## Requisiti

- Android Studio aggiornato
- JDK compatibile con Android Gradle Plugin 8.x
- Android SDK con `compileSdk 34`
- Dispositivo o emulatore Android con API level 24 o superiore
- Connessione internet per API, mappe e autenticazione

## Configurazione locale

1. Clonare il repository:

   ```bash
   git clone https://github.com/Alessandro-Dal-Ceredo/IngegneriaDelSoftware.git
   cd IngegneriaDelSoftware
   ```

2. Aprire il progetto con Android Studio.

3. Verificare che `local.properties` contenga il percorso corretto dell'Android SDK:

   ```properties
   sdk.dir=/percorso/al/tuo/Android/Sdk
   ```

4. Configurare Google Maps inserendo una chiave API valida in `app/src/main/AndroidManifest.xml`:

   ```xml
   <meta-data
       android:name="com.google.android.geo.API_KEY"
       android:value="LA_TUA_API_KEY" />
   ```

5. Configurare Firebase aggiungendo il file `google-services.json` nel modulo `app/`, se non già presente localmente.

6. Eseguire il sync Gradle e avviare l'app da Android Studio.

## Build da terminale

Per compilare una build debug:

```bash
./gradlew :app:assembleDebug
```

Per controllare rapidamente la presenza dei file principali:

```bash
./check_setup.sh
```

## Note su backend e servizi esterni

L'app usa Supabase per autenticazione, dati utente, segnalazioni e immagini. La classe `API_MANAGER` centralizza configurazione Retrofit, gestione del token, persistenza della sessione e chiamate principali.

Per usare l'app in un nuovo ambiente è necessario verificare che il progetto Supabase contenga le tabelle e le policy coerenti con le chiamate definite in `SupabaseApiService`, in particolare:

- `users_info`
- `reports`
- `images`

Le notifiche push richiedono una configurazione Firebase valida e topic coerenti con il formato `city_<nome_comune>`.

## Stato del progetto

Il repository contiene il codice sorgente dell'app Android, gli asset grafici, i layout, il grafo di navigazione e i dataset GPX usati dalla mappa. Non sono presenti test automatici significativi: la verifica principale avviene tramite build Gradle ed esecuzione su dispositivo o emulatore.
