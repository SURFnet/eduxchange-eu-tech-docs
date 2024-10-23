# This is a FAQ

## About OOAPI

- [How to connect OOAPI endpoints?](./connecting-ooapi.endpoints.md)
- Where can I find an example of protecting my API (`/persons/` `/associations/`) using oauth/MyAcademicID?
  - [Mock implementation of a home institution](https://github.com/SURFnet/student-mobility-home-institution-mock)
- What OOAPI endpoints are needed for enrollment?
  - GET /persons/me
  - POST /associations/external/me
  - GET /associations/{associationId}  
  - POST /associations/{associationId}  
  - PATCH /associations/{associationId}  
    These endpoints will be protected using oauth tokens.

## About the broker

- What is the edubroker?
  - The edubroker is a component hosted by SURF that initiates the enrollment-process for a student. The broker provides a visual interface with feedback for the student.
- How can I enable the edubroker for my offerings on the frontend?
  - Currently, when a student clicks on a enrollment button in eduxchange.eu, the student is sent to a form or an email. To enable the broker for your offerings, SURF has to change a setting for you. Ask SURF if you want to activate the broker for your offerings.

## About Enrolment

- How does the enrolment work in general?
  - [Sequence diagram for EuroTeQ enrolment](./sequence-diagram.md)
- What are the possible initial states of an association?
  - [Flowchart of the association states](./association-states.md)

## About the enrolment receiver

- Can you tell me more about the communication between the generic part of the enrollment
receiver and the custom implementation at the host institution?
  - [Communication dataformat](./dataformat.md)
- Do you have an example configuration of the enrolment receiver?
  - [example application.yaml for enrollment receiver](./application.yaml)
- How do I run the enrollment receiver?
  - It's advised to use the docker image [as described here](./running.md)

## About openID and MyAcedemicID

- What are the url's for starting authentication/introspection/tokens at MyAcedemicID?
  - The MyAcademidID endpoints for openID can be found in the
  [well-known](https://proxy.prod.erasmus.eduteams.org/.well-known/openid-configuration)
  location. Please use a widely used library for all openID parts, instead
  of builing it.
- How can we start an enrollment for testing?
  - There is a [demo enrollment broker](https://demobroker.eduxchange.eu/)
  available for testing.
  - To connect to the demo enrollment broker, edit this yaml document
  and send it to Peter or Jelmer:

    ``` yaml
    schacHome: demoinst02.eduxchange.eu
    name: Demo 02 home  # The display name for your institution
    abbreviation: Demo02home  # The short name
    courseEndpoint: "https://demoinst02.eduxchange.eu/basic/offerings"  # The OOAPI endpoint for courses
    personsEndpoint: "https://demoinst02.eduxchange.eu/persons/me"  # The OOAPI endpoint for persons
    personAuthentication: HEADER  # Should always be HEADER for token based authentication
    associationsEndpoint: "https://demoinst02.eduxchange.eu/associations" # The OOAPI endpoint for courses
    authenticationEndpoint: "https://demoinst01.eduxchange.eu/api/enrollment" # This is on the enrollment-receiver
    registrationEndpoint: "https://demoinst01.eduxchange.eu/api/start"  # This is on the enrollment-receiver
    registrationUser: "user"  # These are configured in the broker section of the enrollment-receiver config file
    registrationPassword: "secret"  # These are configured in the broker section of the enrollment-receiver config file
    logoURI: https://static.surfconext.nl/logos/idp/surf.png # The logo to be displayed for your institution
    scopes: demoinst02.eduxchange.eu/persons demoinst02.eduxchange.eu/results   # The scopes required for accessing the persons and associations endpoints
    privacyEndpoint: https://www.surf.nl/studentmobiliteit  # A link to the privacy declaration
    useEduHubForOffering: True # Should always be True for EuroTeq
    useQueueIt: False # Should always be False for EuroTeq
    ```

- What are scopes? What should I use for scopes?

  Scope is a mechanism in OAuth 2.0 to limit an application's access to a user's account. An application can request one or more scopes, this information is then presented to the user in the consent screen, and the access token issued to the application will be limited to the scopes granted.

  For EuroTeQ, two scopes are used:
  - `persons`: Personal Information
  - `results`: Enrollment and results

  To make the scope identifier unique, the institutiond primary domain is added.
  So to request access to the personal data of a student of MyUniversity, the
  scope `myuniversity.org/person` is requested.

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

## Status

- Where can I see what has to be done, and what has already been done by
all institutions?
  - [See the status page here](./progress.md)
