<a href="https://ninjacoding.it/">
     <img src="https://raw.githubusercontent.com/carminemilieni/ninjacoding-commons/main/ninjacoding-primary-logo.svg" alt="NinjaCoding logo" title="NinjaCoding" height="60" />
</a>

# Abstract Design Guide CRUD API

⭐️ Star this project on GitHub: it motivates me a lot!

> Questo repo descrive come dovrebbe comportarsi un servizio CRUD

## Indice

- [Abstract Design Guide CRUD API](#abstract-design-guide-crud-api)
  - [Indice](#indice)
  - [Endpoint e richieste base](#endpoint-e-richieste-base)
    - [Endpoint](#endpoint)
      - [ID API plurare / singolare](#id-api-plurare--singolare)
      - [Endpoint per le raccolte](#endpoint-per-le-raccolte)
      - [Endpoint per i tipi singoli](#endpoint-per-i-tipi-singoli)
      - [Esempio di endpoint per collezioni](#esempio-di-endpoint-per-collezioni)
      - [Esempio di endpoint per tipi singoli](#esempio-di-endpoint-per-tipi-singoli)
    - [Risposte](#risposte)

## Endpoint e richieste base

### Endpoint

#### ID API plurare / singolare

- **:pluralApiID** - Usare l'id api al plurale quando si fa riferimento ad un endpoit che rispecchia una collezione di elementi.
- **:singularApiID** - Usare l'id api al singolare quando si fa riferimento ad un singolo elemento dove :singularApiID è già esso stesso L'id dell'elemento.

Esempio:

||endpoint |descrizione |
|---|---|---|
|`:pluralApiID`|/api/v1/persone|Rispecchia una collezzione di elementi|
|`:singularApiID`|/api/v1/homepage|Fa riferimento ad una pagina di contenuto e non ad una collezione di pagine|

#### Endpoint per le raccolte

|Metodo|Endpoint|Alias|Descrizione|
|---|---|---|---|
|`GET`|/api/v1/:pluralApiID|`findMany`|Ottieni una lista di elementi|
|`POST`|/api/v1/:pluralApiID|`createOne`|Crea un nuovo elemento|
|`GET`|/api/v1/:pluralApiID/:elementID|`findOne`|Ottieni un singolo elemento|
|`PUT`|/api/v1/:pluralApiID/:elementID|`updateOne`|Aggiorna un singolo elemento|
|`DELETE`|/api/v1/:pluralApiID/:elementID|`deleteOne`|Elimina un singolo elemento|

#### Endpoint per i tipi singoli

|Metodo|Endpoint|Alias|Descrizione|
|---|---|---|---|
|`GET`|/api/v1/:singularApiID|`findOne`|Ottieni un singolo elemento|
|`PUT`|/api/v1/:singularApiID|`updateOne`|Aggiorna un singolo elemento|
|`DELETE`|/api/v1/:singularApiID|`deleteOne`|Elimina un singolo elemento|

#### Esempio di endpoint per collezioni

|Metodo|Endpoint|Descrizione|
|---|---|---|
|`GET`|/api/v1/persone|Ottieni una lista di persone|
|`POST`|/api/v1/persone|Crea una nuova persona|
|`GET`|/api/v1/persone/1|Ottieni una singola persona|
|`PUT`|/api/v1/persone/1|Aggiorna una singola persona|
|`DELETE`|/api/v1/persone/1|Elimina una singola persona|

#### Esempio di endpoint per tipi singoli

|Metodo|Endpoint|Descrizione|
|---|---|---|
|`GET`|/api/v1/homepage|Ottieni il contenuto della homepage|
|`PUT`|/api/v1/homepage|Aggiorna il contenuto della homepage|
|`DELETE`|/api/v1/homepage|Elimina il contenuto della homepage|

### Risposte

Una richiesta HTTP dovrebbe restituire una risposta con un codice di stato HTTP appropriato e un corpo di risposta JSON.
L'oggetto dovrebbe essere composto da queste chiavi:

- `data` - I dati della risposta stessa, in genere cosi composti
  - un documento singolo, un oggetto che contiene le chiavi
    - `id` - (int/uuid/obbligatori/) L'id dell'elemento - un numero intero o un uuid 
    - gli attributi dell'elemento
    - `meta` eventuali metadati es.: **created_at**, **updated_at**
  - `meta` - (object): informazioni come la paginazione, il numero di elementi, ecc...
  - `errors` - (object/opzionale): informazioni su eventuali errori generati dalla richiesta
