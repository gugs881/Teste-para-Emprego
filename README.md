## Teste para Estágio de C#.Net

Intro

Lacuna Software has launched a fictional branch named Lacuna Space. They have deployed a clock synchronization project called Luma to monitor probes across the Solar System.
Time synchronization is crucial for cohesive communication and data transfer between computers in a network and probes running experiments.
Your task is to follow the provided documentation and create a C# .Net program that communicates with Lacuna Space's APIs.
The program should sync your local clock with each space probe's clock and assist in syncing and monitoring the systems.

> Lembre-se: isso não é uma corrida. Mostre suas habilidades de programação, modularização, serialização de dados e reutilização de código. Falhar faz parte do processo, então aproveite o desafio!




---

1. Start API

Endpoint: [POST] /api/start
Request:

{
  "username": "your_username",
  "email": "your_email@example.com"
}

Response:

{
  "accessToken": "your_access_token",
  "code": "Success",
  "message": "response_details_message"
}

> Nota: Use o token de acesso recebido para autorização nas chamadas seguintes. Ele é válido por 2 minutos.




---

2. List Probes API

Endpoint: [GET] /api/probe
Headers:

Authorization: Bearer {accessToken}

Response:

{
  "probes": [
    {
      "id": "probe_id",
      "name": "probe_name",
      "encoding": "probe_encoding"
    }
  ],
  "code": "Success",
  "message": "response_details_message"
}


---

3. Timestamp Encodings

Iso8601: "2023-06-03T12:57:27.6003807+00:00"

Ticks: "638213938476003807"

TicksBinary: "37GQFTJk2wg="

TicksBinaryBigEndian: "CNtkMhWQsd8="



---

4. Sync API (Clock Synchronization)

Endpoint: [POST] /api/probe/{id}/sync
URL Parameters:

id: Probe ID


Headers:

Authorization: Bearer {accessToken}

Response:

{
  "t1": "probe_encoded_timestamp_after_request",
  "t2": "probe_encoded_timestamp_before_response",
  "code": "Success",
  "message": "response_details_message"
}

> Sync Algorithm: compute time offset (θ) and round-trip (σ) as especificado.




---

5. Jobs APIs

a. Get a Job API

Endpoint: [POST] /api/job/take
Headers:

Authorization: Bearer {accessToken}

Response:

{
  "job": {
    "id": "job_id",
    "probeName": "probe_name_to_check_clock"
  },
  "code": "Success",
  "message": "response_details_message"
}

b. Check Job API

Endpoint: [POST] /api/job/{id}/check
URL Parameters:

id: Job ID


Headers:

Authorization: Bearer {accessToken}

Request:

{
  "probeNow": "your_current_synced_probe_clock_timestamp_encoded",
  "roundTrip": 12345
}

Response:

{
  "code": "Success",
  "message": "response_details_message"
}

> Continue realizando as tarefas e checando os jobs até receber um código "Done".




---

6. Putting It All Together

Chame o Start API e obtenha um access token

Liste as sondas para sincronizar

Crie relógios sincronizados para cada sonda

Obtenha e envie as respostas dos jobs com o timestamp sincronizado e round-trip

Se receber um código "Fail" em qualquer ponto, recomece

Se o check retornar "Done", você concluiu!



---

7. One Step Further (Modo Avançado)

Chame o Start API com um parâmetro de nível 2: [POST] /api/start/2

Esteja atento ao código "ProbeUnreachable" na API de sincronização; aguarde 5 segundos antes de tentar novamente

Ajuste o tempo decorrido para sondas sob forte campo gravitacional com base no timeDilationFactor.
