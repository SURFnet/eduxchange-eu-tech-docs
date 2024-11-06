# This is a FAQ

## About OOAPI

- [How to connect OOAPI endpoints?](./connecting-ooapi.endpoints.md)
- Where can I find an example of protecting my API (`/persons/` `/associations/`) using oauth/MyAcademicID?
  - [Mock implementation of a home institution](https://github.com/SURFnet/student-mobility-home-institution-mock)
- What OOAPI endpoints are needed for enrollment?
  - GET /persons/me
  - POST /associations/external/me
  - GET /associations/{associationId}
  - PATCH /associations/{associationId}
    These endpoints will be protected using oauth tokens.

## About the broker

- What is the edubroker?
  - The edubroker is a component hosted by SURF that initiates the enrollment-process for a student. The broker provides a visual interface with feedback for the student.
- How can I enable the edubroker for my offerings on the frontend?
  - Currently, when a student clicks on a enrollment button in eduxchange.eu, the student is sent to a form or an email. To enable the broker for your offerings, SURF has to change a setting for you. Ask SURF if you want to activate the broker for your offerings.

## About Enrollment

For enrollment to work, an institution has to implement functionality to play two "roles":

1. The Host Institution, where you receive incoming enrollment requests. The Host Institution sends several (OOAPI) requests (via the Enrollment Receiver) to the Home Institution of the student to:
   - Get personal information about the student.
   - Let the Home Instution know the students want to enroll at the Host Institution, giving the Home Institution a chance to allow or deny the enrollment.
   - Check whether a student is still "active" at the Home Institution, for example just before the course starts.
   - Inform the Home Insitution that the students has cancelled the enrollment.
   - Inform the Home Insitution of the result that student achieved when the course has finished.
2. The Home Insitution, who will receive OOAPI requests from the Host Institution and responds to them. In the responses, the Home Institution can inform the Host Institution about decisions regarding the enrollment of the student.

In general, the Host Institution is in charge of the communication and will initiate requests. The Home Institution responds to those request.

- How does the enrollment work in general?
  - [Sequence diagram for EuroTeQ enrollment](./sequence-diagram.md)
- What are the possible initial states of an association?
  - [Flowchart of the association states](./association-states.md)

## About the enrollment receiver

- Can you tell me more about the communication between the generic part of the enrollment
receiver and the custom implementation at the host institution?
  - [Communication dataformat](./dataformat.md)
- Do you have an example configuration of the enrollment receiver?
  - [example application.yaml for enrollment receiver](./application.yaml)
- How do I run the enrollment receiver?
  - It's advised to use the docker image [as described here](./running.md)
- What is the response from the SIS to the enrollment receiver?
  - After processing the enrollment request in the host institution, and
  informing the home institution a response is returned to the enrollment receiver. The HTTP status code should always be 200, and the response should look like this:

    ```json
    {
      "result": "ok",
      "code": 200,
      "message": "Message to show to the student",
      "oo-api-offering-id": "offeringId_value_here",
      "redirect" : "https://optional.redirect/for-extra-information"
    }
    ```

    For the `code` use these values:

        | Value | Label                                      |
        |-------|--------------------------------------------|
        | 200   | 200 - All is good                          |
        | 400   | 400 - Backend error                        |
        | 404   | 404 - Person endpoint not found            |
        | 409   | 409 - Queue-session validation failed      |
        | 412   | 412 - Invalid enrollmentRequest            |
        | 417   | 417 - Token request failed                 |
        | 419   | 419 - eduID not present in the ARP         |
        | 422   | 422 - Administrative error (already enrolled) |
        | 500   | 500 - Not so good                          |

    If a value is present for `redirect`, the user will be asked to provide extra
    information. A butten will be shown sending the user to the form in a new
    window. Leave out this field if no extra form is required.

## About openID and MyAcedemicID

- What are the url's for starting authentication/introspection/tokens at MyAcedemicID?
  - The MyAcademidID endpoints for openID can be found in the
  [well-known](https://proxy.prod.erasmus.eduteams.org/.well-known/openid-configuration)
  location. Please use a widely used library for all openID parts, instead
  of builing it.
- How can we start an enrollment for testing?
  - There is a [demo enrollment broker](https://broker.test.eduxchange.eu/)
  available for testing.
  - To connect to the demo enrollment broker, edit this yaml document
  and send it to Peter or Jelmer:

    ``` yaml
    schacHome: demoinst02.eduxchange.eu
    name: Demo 02 home  # The display name for your institution
    abbreviation: Demo02home  # The short name
    courseEndpoint: "https://demoinst02.eduxchange.eu/basic/offerings"  # The OOAPI endpoint for courses
    courseAuthentication: BASIC  # For authenticating to the offerings endpoint, Not used when useEduHubForOffering=True
    courseAuthenticationUserName: "user"  # For authenticating to the offerings endpoint, Not used when useEduHubForOffering=True
    courseAuthenticationPassword: "secret"  # For authenticating to the offerings endpoint, Not used when useEduHubForOffering=True
    personsEndpoint: "https://demoinst02.eduxchange.eu/persons/me"  # The OOAPI endpoint for persons
    personAuthentication: HEADER  # Should always be HEADER for token based authentication
    associationsEndpoint: "https://demoinst02.eduxchange.eu/associations" # The OOAPI endpoint for courses
    authenticationEndpoint: "https://demoinst01.eduxchange.eu/api/enrollment" # This is on the enrollment-receiver
    registrationEndpoint: "https://demoinst01.eduxchange.eu/api/start"  # This is on the enrollment-receiver
    registrationUser: "user"  # These are configured in the broker section of the enrollment-receiver config file
    registrationPassword: "secret"  # These are configured in the broker section of the enrollment-receiver config file
    logoURI: https://static.surfconext.nl/logos/idp/surf.png # The logo to be displayed for your institution
    scopes: email schac_personal_unique_code demoinst02.eduxchange.eu/persons demoinst02.eduxchange.eu/results # Always "email schac_personal_unique_code" plus the scopes required for accessing the persons and associations endpoints
    privacyEndpoint: https://www.surf.nl/studentmobiliteit  # A link to the privacy declaration
    useEduHubForOffering: True # Should always be True for EuroTeq
    useQueueIt: False # Should always be False for EuroTeq
    ```

- What are scopes? What should I use for scopes?

  Scope is a mechanism in OAuth 2.0 to limit an application's access to a user's account. An application can request one or more scopes, this information is then presented to the user in the consent screen, and the access token issued to the application will be limited to the scopes granted.

  For EuroTeQ, two general scopes are used:
  - `email` : To retrieve the user's home institution email
  - `schac_personal_unique_code` : To retrieve the user's identifier at the home institution

  Also, two institution specific scopes are used:
  - `persons`: Personal Information
  - `results`: Enrollment and results

  To make the scope identifier unique, the institutiond primary domain is added.
  So to request access to the personal data of a student of MyUniversity, the
  scope `institution.tld/persons` is requested.

  Currently, these scopes are known for EutoTeQ institutions:

  - demoinst01.eduxchange.eu/persons
  - demoinst01.eduxchange.eu/results
  - demoinst02.eduxchange.eu/persons
  - demoinst02.eduxchange.eu/results
  - taltech.ee/persons
  - taltech.ee/results
  - du50.vc.cvut.cz/eq/resource/v5/persons
  - du50.vc.cvut.cz/eq/resource/v5/results
  - technion.ac.il/persons
  - technion.ac.il/results

  When receiving a token, the MyUniversity's API endpoint **must** validate if
  the scope is valid for the API being called.

- How do I connect to MyAcademicID?
  - The enrollment receiver needs to be connected as a relying party to
  MyAcademicID. The API server needs to be connected as a Resource Server.
  Both can be registered by [filling in the myacademic id registration form](./registration.md)

- How does this OpenID connect Oauth thing work? What is the flow for token
introspection?
  - [Here is a nice explanation of how OpenID connect works](https://yasasramanayaka.medium.com/openid-connect-authorization-code-flow-8c02081135fc).
  - The OpenID Connect flow is projected on the euroteq usecase [in this diagram](./openidconnect.md)
- How do I do introspection?
  - Example using curl: `curl -k -u RS-Client-ID:RS-CLIENT-Secret -H 'Content-Type: application/x-www-form-urlencoded' -X POST --data 'token=eyJhbGciOiJFUzI1NiIsImtpZCI6Ik1sVm9jb...' https://proxy.prod.erasmus.eduteams.org/OIDC/introspect -q | jq`
  - Example Response:

   ```json
   {
     "active": true,
     "scope": "openid email schac_personal_unique_code institution.tld/persons institution.tld/results",
     "client_id": "APP-02BDEC4A-6B0D-4488-8932-4E92A8A80F71",
     "exp": 1730715844,
     "iat": 1730712244,
     "sub": "ae3881fe8102b250e1d0766c600010a85faa9b19@myacademicid.org",
     "iss": "https://proxy.prod.erasmus.eduteams.org",
     "token_type": "Bearer",
     "aud": [
       "APP-02BDEC4A-6B0D-4488-8932-4E92A8A80F71"
     ],
     "email": "user.edmail@institution.tld"
   }
   ```

  - In the response validate `"active": true` and the scopes for your institution are present. In the example `institution.tld/persons` and `institution.tld/results`
  - Use the email to look up your user

## Testing

- How can I test the registration flow?
  - [See the page on testing](./testing.md)

## Status

- Where can I see what has to be done, and what has already been done by
all institutions?
  - [See the status page here](./progress.md)
