# Spese Viola & Alice

Web app per dividere le spese di Viola e Alice tra Filippo e Simona.
Si apre da un link, senza installare niente. Su iPhone e Android si può aggiungere alla schermata Home.

- Spese con categoria, "per chi" (Viola, Alice, entrambe), chi ha pagato e divisione (50/50 predefinita, regolabile)
- Foto dello scontrino
- Saldo sempre aggiornato ("Simona deve X a Filippo" o viceversa)
- Registrazione dei pagamenti tra genitori per azzerare il conto
- Riepilogo PDF del mese
- Sincronizzazione in tempo reale tra i due telefoni (Firebase), accesso con Google

Senza configurazione Firebase l'app gira in **modalità prova**: i dati restano solo sul dispositivo.

## Attivare la sincronizzazione (una volta sola, ~10 minuti)

1. Vai su <https://console.firebase.google.com> → **Aggiungi progetto** → nome `spese-viola-alice` (Google Analytics non serve).
2. **Authentication** → Inizia → Metodo di accesso → **Google** → Attiva → Salva.
3. **Authentication → Impostazioni → Domini autorizzati** → Aggiungi `phil4fun.github.io`.
4. **Firestore Database** → Crea database → posizione `eur3 (europe-west)` → modalità produzione.
5. **Firestore → Regole**: incolla il contenuto di `firestore.rules` sostituendo `EMAIL_FILIPPO` ed `EMAIL_SIMONA` con i vostri indirizzi Gmail (in minuscolo) → **Pubblica**.
6. **Impostazioni progetto** (rotellina) → Le tue app → icona **</>** (Web) → nome "Spese V&A" → Registra.
   Copia l'oggetto `firebaseConfig` e incollalo in `firebase-config.js` al posto di `null`.

Fatto. Il piano gratuito di Firebase (Spark) basta e avanza: le foto vengono compresse e salvate in Firestore, quindi non serve Firebase Storage.

## Primo accesso

Ognuno apre il link, tocca **Accedi con Google** e sceglie "Sono Filippo" o "Sono Simona" (una volta sola).
Un account non presente nelle regole non può leggere né scrivere niente.
