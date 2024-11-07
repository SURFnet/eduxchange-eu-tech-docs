# Associations example

 An example for the body of the `POST /associations/external/me` call:

```json
{
  "role": "student",
  "state": "associated", // The desired state the Host would like the Home institution to reach.
  "remoteState": "associated", // The initial state the Host has reached so far. Could also be pending or queued.
  "offering": {
    "primaryCode": {
      "codeType": "identifier",
      "code": "1234qwe12"
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
    "course": {
      "courseId": "123e4567-e89b-12d3-a456-426614174000",
      "primaryCode": {
        "codeType": "identifier",
        "code": "1234qwe12"
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
      "codeType": "identifier",
      "code": "1234qwe12"
    },
    "organizationType": "root",
    "name": [
      {
        "language": "en-GB",
        "value": "The University"
      }
    ],
    "shortName": "UNI",
    "link": "https://institution.tld",
    "logo": "https://institution.tld/logo.svg"
  }
}
```
