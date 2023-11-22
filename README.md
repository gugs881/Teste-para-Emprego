# Teste-para-Estagio-de-C#.Net


# Intro

# Lacuna Software has launched a fictional branch named Lacuna Space. They have deployed a clock synchronization project called Luma to monitor probes across the Solar System.
# Time synchronization is crucial for cohesive communication and data transfer between computers in a network and probes running experiments.
# Your task is to follow the provided documentation and create a C# .Net program that communicates with Lacuna Space's APIs. The program should sync your local clock with each space probe's clock and assist in syncing and monitoring the systems.
# Remember, this is not a race. Showcase your coding skills, modularization, data serialization, and code reuse. Failing is considered part of the process, so enjoy the challenge!

# Start

# 1. Start API

# Endpoint: [POST] /api/start
# Request:
# {
#   "username": "your_username",
#   "email": "your_email@example.com"
# }
# Response:
# {
#   "accessToken": "your_access_token",
#   "code": "Success",
#   "message": "response_details_message"
# }
# Note: Use the received access token for Authorization in subsequent APIs. The token is valid for 2 minutes.

# List Probes

# 2. List Probes API

# Endpoint: [GET] /api/probe
# Headers:
# - Authorization: Bearer {accessToken}
# Response:
# {
#   "probes": [
#     {
#       "id": "probe_id",
#       "name": "probe_name",
#       "encoding": "probe_encoding"
#     }
#   ],
#   "code": "Success",
#   "message": "response_details_message"
# }

# Timestamp

# 3. Timestamp Encodings

# - Iso8601: "2023-06-03T12:57:27.6003807+00:00"
# - Ticks: "638213938476003807"
# - TicksBinary: "37GQFTJk2wg="
# - TicksBinaryBigEndian: "CNtkMhWQsd8="

# Clock Synchronization

# 4. Sync API

# Endpoint: [POST] /api/probe/{id}/sync
# URL Parameters:
# - id: Probe ID
# Headers:
# - Authorization: Bearer {accessToken}
# Response:
# {
#   "t1": "probe_encoded_timestamp_after_request",
#   "t2": "probe_encoded_timestamp_before_response",
#   "code": "Success",
#   "message": "response_details_message"
# }
# Sync Algorithm: Compute time offset (θ) and round-trip (σ) as specified.

# Jobs

# 5. Jobs APIs

# a. Get a Job API

# Endpoint: [POST] /api/job/take
# Headers:
# - Authorization: Bearer {accessToken}
# Response:
# {
#   "job": {
#     "id": "job_id",
#     "probeName": "probe_name_to_check_clock"
#   },
#   "code": "Success",
#   "message": "response_details_message"
# }

# b. Check Job API

# Endpoint: [POST] /api/job/{id}/check
# URL Parameters:
# - id: Job ID
# Headers:
# - Authorization: Bearer {accessToken}
# Request:
# {
#   "probeNow": "your_current_synced_probe_clock_timestamp_encoded",
#   "roundTrip": 12345
# }
# Response:
# {
#   "code": "Success",
#   "message": "response_details_message"
# }
# Continue taking and checking jobs until 'Done' response is received.

# Putting It All Together

# 6. C# Program

# - Call the start API and get an access token
# - Get a list of probes to sync with
# - Create synchronized clocks for each probe
# - Get and check jobs providing the corresponding probe synced timestamp and the round-trip value
# - If 'Fail' response code is received at any time, start from the beginning.
# - If no more jobs are left and check job call returns 'Done', you passed!

# One Step Further

# 7. Advanced Mode

# - Call the start API with a level 2 route parameter: [POST] /api/start/2
# - Be aware of 'ProbeUnreachable' response code on sync API; wait 5 seconds before retrying.
# - Adjust elapsed time for probes under strong gravitational fields based on timeDilationFactor.

# Have fun!
