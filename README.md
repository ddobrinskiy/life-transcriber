# life-transcriber
Project to transcribe, embed and search my life

## Project Structure

```mermaid
graph TD
    subgraph audio transcriber
        CA[Computer Audio] --> W[OpenAI Whisper]
        MS[Microphone Stream] --> W
        OD[Other Devices] --> W
        W --> RT[Raw Transcripts]
        RT --> E1[OpenAI Embeddings]
    end

    subgraph searcher
        UI[Search Query] --> E2[OpenAI Embeddings]
        SR[Search Results]
    end

    E1 --STORE--> EDB[Embeddings DataBase]
    E2 --SEARCH----> EDB
    EDB --RETRIEVE--> SR

    subgraph metadata_engine
        MT[Metadata]
        GC[Google Calendar] --> MT
        CHP[Call History Phone] --> MT
        CHT[Call History Telegram] --> MT
        OMD[Other Metadata, tbd] --> MT
    end

    MT -...-> RT
    MT -.-> EDB
```

## Components

* audio transcriber
  * script runs in background and saves all audio as time-stamped small files
  * audio is transcribed and converted into raw text, stored in a database
  * raw text converted to embeddings, stored in a vector DB
* metadata engine
  * parse life metadata
  * calendar
  * geolocation
  * call history
  * other?
  * upload metadata to both transcript and vector DB for context/filtering
* searcher
  * convert search queries into embeddings to search the vector DB for closest matches
  * also add metadata filters/sorting


## ToDo

* choose storage format for raw text, timestamps and metadata
* choose a vector DB for the project
