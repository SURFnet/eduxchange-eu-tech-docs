# Association State Flowchart

The flowchart below describes the outcome of association states after the initial application of a student. The student should receive an initial result.

The HOST and HOME institutions each have their own business logic rules they can use to determine the state.

btw: states can change later.

[![Association States](./images/inschrijven-gastinstelling-EN.drawio.png)](./images/inschrijven-gastinstelling-EN.drawio.png)

## Explanation of rules governing the association state (Home Institution)

- pending (proces is waiting on the status of the students home institution)
- associated (the student is enrolled in the learning activity)
- canceled (by student)
- denied (either learning activity is stopped or student is not allowed)
- queued (student is put on a waiting list)

## Explanation of rules governing the association remoteState (Host Institution)

- pending (proces is waiting on the status of the students home institution)
- associated (the student is enrolled in the learning activity)
- canceled (by student)
- denied (student is not allowed)
- queued (student is put on a waiting list)

[(source)](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange?id=explanation-of-rules-governing-the-association-state)
