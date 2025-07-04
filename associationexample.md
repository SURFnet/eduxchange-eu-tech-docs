# Associations example

 An example for the body of the `POST /associations/external/me` call.

 Note: this is a me call, so the person should be identified in the authorisation proces. No persons info is required in this call.

```json
{
   "role": "student",
   "state": "associated", // The desired state the Host would like the Home institution to reach.
   "remoteState": "associated", // The initial state the Host has reached so far. Could also be pending or queued.
   "offering": { // The offering the student is trying to enroll on
      "primaryCode": {
         "codeType": "offeringCode",
         "code": "123e4567-e89b-12d3-a456-426614174000"
      },
      "offeringType": "course",
      "name": [
         {
            "language": "en-GB",
            "value": "Introduction to Bio-Informatics - fall 2024"
         }
      ],
      "abbreviation": "INTROBIOINF2024",
      "description": [
         {
            "language": "en-GB",
            "value": "Intro text"
         }
      ],
      "teachingLanguage": "eng",
      "resultExpected": true,
      "resultValueType": "1-10",
      "link": "https://institution.tld/courses/bioinf/2024",
      "startDate": "2024-10-15",
      "endDate": "2024-11-16",
      "enrollStartDate": "2024-01-24",
      "enrollEndDate": "2024-08-29",
      "course": { // more information about the course this offering is for
         "primaryCode": {
            "codeType": "courseCode",
            "code": "123e4567-e89b-12d3-a456-426614174000"
         },
         "name": [
            {
               "language": "en-GB",
               "value": "Introduction to Bio-Informatics"
            }
         ],
         "abbreviation": "INTROBIOINF",
         "studyLoad": {
            "studyLoadUnit": "ects",
            "value": 3
         },
         "description": [
            {
               "language": "en-GB",
               "value": "Description text"
            }
         ],
         "teachingLanguage": "eng",
         "level": "master",
         "link": "https://institution.tld/courses/bioinf"
      }
   },
   "issuer": { // The issuer should be an Organization of type root. It represents the institution that is offering the course (offering).
      "primaryCode": {
         "codeType": "schacHome",
         "code": "surf.nl"
      },
      "organizationType": "root",
      "name": [
         {
            "language": "nl-NL",
            "value": "Coöperatie SURF U.A."
         }
      ],
      "shortName": "SURF",
      "description": [
         {
            "language": "nl-NL",
            "value": "SURF is een coöperatieve vereniging van Nederlandse onderwijs- en onderzoeksinstellingen waarin de leden hun krachten bundelen. De leden zijn eigenaar van SURF."
         }
      ],
      "addresses": [
         {
         "addressType": "postal",
         "street": "Moreelsepark",
         "streetNumber": "48",
         "additional": [
            {
               "language": "en-GB",
               "value": "On the other side of the road"
            }
         ],
         "postalCode": "3511 EP",
         "city": "Utrecht",
         "countryCode": "NL",
         "geolocation": {
            "latitude": 52.089123,
            "longitude": 5.113337
         },
         "ext": {}
         }
      ],
      "link": "https://surf.nl",
      "logo": "https://www.surf.nl/themes/surf/logo.svg",
   }
}
```
