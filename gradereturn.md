# Grade Return (DRAFT)

## The Result Lifecycle: Finality and Overwrites

The API supports sending a result multiple times. This is common in scenarios where a preliminary grade is issued, followed by a final grade after a review period or an appeal.

* **Last-One-Wins:** The receiving system (Home Institution) must treat the most recent successful `PATCH` as the authoritative state of the result.
* **Overwriting:** Each `PATCH` to `/associations/{associationId}` overwrites the previous values within the `result` object. Receiving institution should store all results, to provide a history of changes.
* **`remoteState`:** While you can send multiple updates, setting the `remoteState` to `"completed"` signals to the Home Institution that the grading process is officially finished.

### Scope: Course Results Only

This implementation strictly uses the **Course Result** level. We do not utilize `componentResult` (for partial assignments) or `programResult` (for degree-level outcomes). By updating the `association` directly, you are reporting the final outcome for the specific course offering.

### Technical Mapping: `resultValueType` & `score`

The `score` field is a string, but its content must align with the `resultValueType` defined in the **Offering** object. This ensures the Home Institution can correctly parse the value into their local Student Information System (SIS).

| `resultValueType` | Description | Example `score` |
| :--- | :--- | :--- |
| `pass-or-fail` | Binary outcome (Pass/Fail). | `"pass"` |
| `US letter` | American letter grading scale. | `"A-"` |
| `UK letter` | British letter grading scale. | `"2:1"` |
| `0-100` | Percentage or point-based scale. | `"88"` |
| `1-10` | Standard decimal scale (e.g., Dutch/European). | `"7.5"` |
| **EuroTeQ Specifics** | | |
| | | |
| | | |

### The `ext` Object and Teaching Person

For administrative transparency, use the `ext` (extension) object to include the name of the examiner or teacher responsible for the grade as `responsibleTeachers`.

See [the eduxchange profile](https://openonderwijsapi.nl/#/technical/consumers-and-profiles/eduxchange)

**Example Payload:**

```json
PATCH /associations/{associationId}
Content-Type: application/json

{
  "result": {
    ...
    "ext": {
        "responsibleTeachers": [
            {
                "givenName": "Harry",
                "surname": "Potter"
            }
        ]
    }
  }
}
```
