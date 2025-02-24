# Associations example

 An example for the body of the `POST /associations/external/me` call:

```json
{
   "person":{
      "personId":"7f5b2771-c6a0-461b-8ed6-216255b981ed",
      "givenName":"test Name",
      "surname":"test Name",
      "displayName":"Test Name Test NAme",
      "gender":"M",
      "dateOfBirth":"1990-11-26",
      "nationality":null,
      "mail":"veiko.samma@taltech.ee",
      "affiliations":[
         "employee"
      ],
      "activeEnrollment":true
   },
   "offering":{
      "offeringType":"program",
      "offeringId":"76daa0f3-dcae-4e28-a048-f1201ea3965d",
      "primaryCode":{
         "codeType":"programCode",
         "code":"4000MMODDN"
      },
      "academicSession":{
         "academicSessionId":"d82ee7b5-b16c-4148-817f-6e325dcbb064",
         "academicSessionType":"academic year",
         "primaryCode":{
            "codeType":"identifier",
            "code":"2022-2023"
         },
         "name":[
            {
               "language":"nl-NL",
               "value":"2022-2023-nl"
            },
            {
               "language":"en-GB",
               "value":"2022-2023-en"
            }
         ],
         "startDate":"2022-09-01",
         "endDate":"2023-08-27",
         "otherCodes":[
            {
               "codeType":"x-ascme",
               "code":"2022"
            }
         ]
      },
      "name":[
         {
            "language":"nl-NL",
            "value":"Modern Drug Discovery"
         },
         {
            "language":"en-GB",
            "value":"Modern Drug Discovery"
         }
      ],
      "abbreviation":"Test-INFOMQNM-20FS",
      "description":[
         {
            "language":"en-GB",
            "value":"*The program*\nHow are new drugs developed? This question is central to the Minor Modern Drug Discovery (MDD), which covers the entire trajectory from disease to drug molecule and vice versa. The various research groups involved offer a complementary and interdisciplinary perspective by connecting the diverse subjects in drug development into a coherent Minor. The main goal is to provide insight into novel drugs and their targets within the body. Students learn how to design, synthesize, formulate, administer and test a drug molecule before it may serve as ‘lead’ molecule for a future drug. These may be small molecules but also therapeutic proteins or vaccines may be considered. Moreover, (novel) targets are studied intensely via ‘omics’ approaches and bio-analysis of drugs. The drug development trajectory requires cooperation of various disciplines, which is shown by the fact that three different Bachelor studies from the Faculty of Science are involved in this Minor: MST, LST and BFW.\n\nThe following subjects are addressed in the Minor Modern Drug Discovery:\n\n* bio- and cheminformatics\n\n* ‘omics’ approaches\n\n* bio-analysis of drugs and their targets\n\n* formulation of drug molecules\n\n* administration of drugs\n\n* receptor- and enzyme systems\n\n* synthetic approaches\n\n* biological testing\n\nThese important parts are studied both in theory as well as in practice during the Minor programme. Based on interdisciplinary examples students learn various ways to identify and/or produce new ‘lead’ molecules that may serve as a basis for the development of new drug therapies.\n\n**When foreign students follow the Minor, all lectures and exams will be in English**; students may however answer in Dutch."
         }
      ],
      "teachingLanguage":"eng",
      "modeOfDelivery":[
         "on campus"
      ],
      "resultExpected":false,
      "link":"https://studiegids.universiteitleiden.nl/studies/9036",
      "otherCodes":[
         {
            "codeType":"x-ascme",
            "code":"4000MMODDN"
         }
      ],
      "consumers":[
         {
            "alliances":[
               {
                  "name":"lde",
                  "selection":false,
                  "type":"deepening",
                  "visibleForOwnStudents":true,
                  "enrollmentForOwnStudents":"broker",
                  "source":{

                  }
               }
            ],
            "consumerKey":"eduxchange"
         }
      ],
      "startDate":"2022-09-01",
      "endDate":"2023-08-27",
      "priceInformation":[

      ],
      "program":{
         "name":[
            {
               "language":"nl-NL",
               "value":"Kleine moderne drugsontdekking"
            },
            {
               "language":"en-GB",
               "value":"Minor Modern Drug Discovery"
            }
         ],
         "abbreviation":"MEBE-BEADVKK-04",
         "studyLoad":{
            "studyLoadUnit":"ects",
            "value":3
         },
         "modeOfDelivery":[

         ],
         "duration":"",
         "firstStartDate":"",
         "description":[
            {
               "language":"nl-NL",
               "value":"1 Inhoud \n In deze module leert de student het toerekenen van kosten via de kostenplaatsenmethode en het maken van analyses van afdelingsresultaten. \n \n Onder andere komen de volgende onderwerpen aan bod: \n \n - het toerekenen van kosten aan orders \n - de kostenplaatsenmethode \n - boekingen bij toepassing van de kostenplaatsenmethode \n - de budgettering van de indirecte kosten \n - het budget en de boekhouding \n - de fabrieksboekhouding bij Make to stock \n - de berekening en de analyse van het periode resultaat \n - de administratie van dienstverlenende bedrijven \n - de boekhouding bij direct costing \n \n Voor een inhoudelijke beschrijving van deze cursus kan je het beste kijken in de cursuswijzer, \n te vinden op sharepoint: https://www.sharepoint.hu.nl/sites/CursuswijzersFEM. Daar vind je \n ook een beschrijving van de competenties en vaardigheden, behorende bij de cursus."
            },
            {
               "language":"en-GB",
               "value":"1 Inhoud \n In deze module leert de student het toerekenen van kosten via de kostenplaatsenmethode en het maken van analyses van afdelingsresultaten. \n \n Onder andere komen de volgende onderwerpen aan bod: \n \n - het toerekenen van kosten aan orders \n - de kostenplaatsenmethode \n - boekingen bij toepassing van de kostenplaatsenmethode \n - de budgettering van de indirecte kosten \n - het budget en de boekhouding \n - de fabrieksboekhouding bij Make to stock \n - de berekening en de analyse van het periode resultaat \n - de administratie van dienstverlenende bedrijven \n - de boekhouding bij direct costing \n \n Voor een inhoudelijke beschrijving van deze cursus kan je het beste kijken in de cursuswijzer, \n te vinden op sharepoint: https://www.sharepoint.hu.nl/sites/CursuswijzersFEM. Daar vind je \n ook een beschrijving van de competenties en vaardigheden, behorende bij de cursus."
            }
         ],
         "teachingLanguage":"nld",
         "fieldsOfStudy":"",
         "learningOutcomes":[
            [

            ]
         ]
      }
   }
   "issuer": {
    "primaryCode": {
      "codeType": "identifier",
      "code": "1234qwe12"
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
    "otherCodes": [
      {
        "codeType": "brin",
        "code": "00AA"
      },
      {
        "codeType": "kvk",
        "code": "12345678"
      }
    ],
    "parent": "42e2bc1b-6741-4e2e-b138-97b4a342c999",
    "children": [
      "497f6eca-6276-4993-bfeb-53cbbbba6f08"
    ],
    "consumers": [
      {
        "consumerKey": "x-test-consumer",
        "additional": "custom",
        "attributes": "here"
      }
    ],
    "ext": {}
  }
}
```
