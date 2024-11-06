# Dataformat Enrollment Receiver

This descibes the communication between the generic part of the enrollment
receiver, and the custom implementation at the host institution (backend).

## Naming

The `backend` is the custom implementation in the host institution,
communicating with the SIS
The `subscription receiver` is a instance of
[this software](https://github.com/SURFnet/student-mobility-inteken-ontvanger-generiek/),
running at the host institution

## First request (enrollment start)

After authentication and retrieving the person-data from the home institution,
a combination of an enrollment and a person is sent to the `/api/start`
endpoint of the backend.
[An example of this message can be found here](https://github.com/SURFnet/student-mobility-inteken-ontvanger-email/blob/main/src/test/resources/data/requestV5.json).
The `personId` in the data should be used for getting updated
person information later.

## Informing home-institution of an enrollment

### Creating

To inform the home institution about a new enrollment request
[an OOAPI associations object can be POST'ed](https://openonderwijsapi.nl/specification/v5/docs.html#tag/associations/paths/~1associations~1external~1me/post) to the subscription receivers
`/associations/external/{personId}` endpoint. It will add the necessary
authentication, and forward the request to the home institution. It will
use the `personId` in the url to find the correct oauth token for the user. The
response will be an OOAPI association object containing an associationId for
future updates, and a status in  `state` and `remoteState`.
`state` [is the enrollment status at the home institution](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange?id=explanation-of-rules-governing-the-association-state)
`remoteState` [is the enrollment status at the host institution](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange?id=explanation-of-rules-governing-the-association-remotestate)

### Updating

To inform the home institution about an updatet enrollment [an OOAPI associations object can be PATCH'ed](https://openonderwijsapi.nl/specification/v5/docs.html#tag/associations/paths/~1associations~1external~1me/post) to the subscription receivers  `/associations/{associationId}` endpoint. It will add the necessary authentication, and forward the request to the home institution. It will use the `associationId` in the url to find the correct oauth token for the user. The response will be an OOAPI association object containing an status  in  `state` and `remoteState`.
`state` [is the enrollment status at the home institution](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange?id=explanation-of-rules-governing-the-association-state)
`remoteState` [is the enrollment status at the host institution](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange?id=explanation-of-rules-governing-the-association-remotestate)

## Get updated person information

To validate a student is still active at the home institution, the backend can send a GET request to `/person/{personId}` of the  subscription receiver. It will add the necessary authentication, and forward the request to the home institution. It will use the `personId` in the url to find the correct oauth token for the user. The response will be an OOAPI persons object containing a current status of the student in  `activeEnrollment`.

## Sending Results

The backend can send the users' results to the home institution by POST'ing an OOAPI association object to the `/api/results` endpoint of the subscription receiver. It will add the necessary authentication, and forward the request to the home institution. It will use the `personId` in the association object to find the correct oauth token for the user.

Also read the informaion about [Consumers and Profiles](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange)

## Response

The backend responds to the /api/start request with a (HTTP 200) json response:

``` json
{
  "result": "ok",
  "code": 200,
  "message": "A message to show to the enrolling user",
  "oo-api-offering-id": "<The offeringid from the request>"
}
```

The defined values for `code` are:

| Value | Label                                            |
|-------|--------------------------------------------------|
| 200   | 200 - All is good                                |
| 400   | 400 - Backend error                              |
| 404   | 404 - Person endpoint not found                  |
| 409   | 409 - Queue-session validation failed            |
| 412   | 412 - Invalid enrollmentRequest                  |
| 417   | 417 - Token request failed                       |
| 419   | 419 - eduID not present in the ARP               |
| 422   | 422 - Administrative error (already enrolled)    |
| 500   | 500 - Not so good                                |
