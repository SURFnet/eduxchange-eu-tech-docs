# [Step 1. Implementing an OOAPI endpoint](https://wiki.surfnet.nl/display/EDX/Step+1.+Implementing+an+OOAPI+endpoint)

Eduxchange relies on the [Open Onderwijs API (OOAPI)](https://openonderwijsapi.nl/#/) standard to function. To enable Eduxchange to operate correctly, your educational institution must have an OOAPI endpoint that adheres to this standard.

![conceptual-model](images/conceptual-model.png)

Your institution's OOAPI endpoint will function as a standardized interface that enables Eduxchange to communicate with your systems without needing to comprehend your specific systems.

Eduxchange utilizes OOAPI for the following processes:

1. **Retrieving information about educational offerings** to display on [eduxchange.nl](http://eduxchange.nl/) or eduxchange.eu.
2. **Enrolling students** in educational offerings.
3. **Transmitting students' grades** from the host institution back to the home institution.

## Implementation Guidelines

- **Gradual Implementation:** Not all required parts of the API need to be implemented simultaneously.
- **Initial Step:** Begin by implementing the necessary parts of the OOAPI to showcase educational offerings on Eduxchange.
- **Subsequent Enhancements:** Later, you can extend your endpoint to include additional features such as enrollment and grade transmission support.

Eduxchange utilizes a subset of the OOAPI specification. The specific parts that need to be implemented are detailed in the Eduxchange profile \[LINK\].

## Steps to Implement an OOAPI Endpoint

- Some institutions may already have an OOAPI endpoint for other use cases. If so, a significant portion of the work might already be completed.

  - For example, most Dutch institutions already have an OOAPI endpoint that is used to provide data to RIO (DUO).
- Identify the systems where Eduxchange data is stored.

  - Sometimes those systems already have API's or interfaces that can be used to build you endpoint upon.

  - In other cases such interfaces might not be available, which makes implementing your OOAPI endpoint more challenging.

    - In all cases it is useful to identify the persons who manage your educational systems and contact them.

- Map your data to the OOAPI data model.

  - This step requires that you study the OOAPI standard and Eduxchange profile and compare them to the datamodels of your institutions' systems.
- Create a REST API that adheres to the [OOAPI standard](https://openonderwijsapi.nl/specification/v5/docs.html) and the Eduxchange profile \[LINK\] on your system(s).

  - This step will usually involve development work requiring some time of a programmer.
- You can [validate your endpoint using our validator](https://wiki.surfnet.nl/display/EDX/Step+4.+Validating+your+OOAPI+endpoint).
