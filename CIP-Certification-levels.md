---
CIP: xxx
Title: Cardano Certification levels
Category: Meta
Status: Draft
Authors:
    - Romain Soulat <romain.soulat@iohk.io>
Implementors: []
Discussions:
    - 
Created: 2024-05-17
License: CC-BY-4.0
---

## Abstract
<!-- A short (\~200 word) description of the proposed solution and the technical issue being addressed. -->
This CIP describes three different levels of certification for the Cardano ecosystem. The goal is to provide a clear and transparent way to communicate the level of quality of a given project or product in the Cardano ecosystem to all stakeholders. Contrary to [CIP-0052](https://developers.cardano.org/docs/governance/cardano-improvement-proposals/cip-0052/), they are requirements to be achieved. This standard does not aim to impose tools and techniques to be used, but rather objectives to be reached.

## Motivation: why is this CIP necessary?
<!-- A clear explanation that introduces the reason for a proposal, its use cases and stakeholders. If the CIP changes an established design then it must outline design issues that motivate a rework. For complex proposals, authors must write a Cardano Problem Statement (CPS) as defined in CIP-9999 and link to it as the `Motivation`. -->
This CIP aims at defining a common understanding of what a certified project or product in the Cardano ecosystem is. It will help stakeholders to understand the level of quality of a given project or product. It will also help developers to understand what is expected from them to achieve a given level of certification. 

Certificates compliant with this CIP are expected to be broadcasted on-chain using [CIP-0096](). This will allow the certificate to be easily discoverable by any one. 

## Specification
<!-- The technical specification should describe the proposed improvement in sufficient technical detail. In particular, it should provide enough information that an implementation can be performed solely on the basis of the design in the CIP. This is necessary to facilitate multiple, interoperable implementations. This must include how the CIP should be versioned, if not covered under an optional Versioning main heading. If a proposal defines structure of on-chain data it must include a CDDL schema in its specification.-->
### Level 0 - Security Audit

#### Level 0: Overview

Level 0 provides the capability to an auditor, a DApp operator, or a DApp developer to provide the result of any security audit. 

#### Level 0: Requirements

Level 0 imposes no requirements on the security audit itself, auditors are encouraged to follow best practices and guidelines such as [CIP-0052](https://developers.cardano.org/docs/governance/cardano-improvement-proposals/cip-0052/).

#### Level 0: Certificate broadcast on chain

The broadcasted certificate must follow CIP-0096 schema as an `AUDIT` certificate.

### Level 1 - Automated testing

#### Level 1: Overview

Level 1 provides a *basic level of assurance in functional and security verification*. The goal of this level is for the developer to provide, at very low cost, a basic level of assurance to the end user that the DApp has been tested, is functional, and has some basic levels of security.

The major part of the work is to be done by the developer. At this level, the automated tool can be seen as assuming the role of the "evaluator" in the evaluation process. 

#### Level 1 - Requirements

##### Documentation

###### From developer: Dapp description, requirements, test plan and traceability

The developer information does not have to be released with the certificate. It is expected to be used by the automated tool to perform the evaluation.

[TODO: Build objectives for each of the following]

- Architecture & Design
- Unique versioning of the DApp
- Identification of the part of the DApp that is certified
- Interfaces (how to interact with the DApp) <- Could be how the automated tool interacts with the DApp

- Security
  - Assets
  - Threats
  - Assumptions
  - Mitigations

- Specifications
  - Functional
  - Security

- Traceability
  - Specifications
  - Test plan

###### From evaluator: Evaluation report

The evaluation document needs to be released with the certificate. 

- Security Target (simply a recompilation of the developer information)
  - Unique identification for the DApp evaluated
  - Threats
  - Assumptions
  - Mitigations

- Developer Test results & coverage (an overview?)

- List of vulnerabilities tested
  - Results of the tests

##### Delivery

The developer shall provide to the automated tool all the necessary information to build the DApp as intended to be used in production.
The developer shall provide to the automated tool all the necessary information to test the DApp as intended to be used in production.
The developer needs to provide the necessary means to the automated tool to interact with the DApp.

The evaluator shall check that the DApp can be built from the source code and the instructions provided by the developer.
The evaluator shall check that the DApp can be tested from the source code and the instructions provided by the developer.

The evaluator shall check that the delivered version of the DApp is the one intended to be certified.

##### Functional & Security testing

The developer shall provide a testing suite for the DApp.
The developer shall provide all the necessary information for the tests to be run automatically in a reproducible way.
The developer shall provide the expected results of the tests.
The evaluator shall run the tests and compare the results with the expected results.
The actual results of the tests shall match the expected results.

##### Independent testing

At level 1, the independant testing can only be performed by automated checks from the testing tools. No advanced attack scenarios are expected to be performed, only application of well-known vulnerabilities.

The evaluator shall provide a testing suite that covers well-known security vulnerabilities as described in maintained and openly accessible lists.
The evaluator shall run attacks based on well-known security vulnerabilities and check that the DApp is not vulnerable to them.

##### Coverage

The developer shall provide a test suite that covers all the behaviors of the DApp. 

- Positive tests: The DApp shall behave as expected when the input is correct.
- Negative tests: The DApp shall handle correctly the incorrect inputs and attacks.

The evaluator shall check that the test suite provided by the developer covers all the behaviors of the DApp and provide. (TODO: What is the expected coverage? What is the coverage criteria?)

#### Level 1: Certificate broadcast on chain

The broadcasted certificate must follow CIP-0096 schema as a `CERTIFY` certificate with a level of 1.
The off-chain information shall contain the full evaluation report.
The certificate shall be issued to the scripts as computed by the automated tool.

### Level 2 - Manual Audit

#### Level 2: Overview

Level 2 provides a *higher level of assurance in functional and security verification*. The goal of this objective is to have an independant entity to challenge the developer's work. At this level, the documentation provided by the developer is challenged by the evaluator, and further penetration testing is expected to be performed.

###### From developer: Dapp description, requirements, test plan and traceability

[TODO: Build objectives for each of the following]

- Architecture & Design
- Unique versioning of the DApp
- Identification of the part of the DApp that is certified
- Interfaces (how to interact with the DApp) <- Could be how the automated tool interacts with the DApp

- Security
  - Assets
  - Threats
  - Assumptions
  - Mitigations

- Specifications
  - Functional
  - Security

- Traceability
  - Specifications
  - Test plan

###### From evaluator: Evaluation report

The evaluation document needs to be released with the certificate. 
- **Developer documentation review**

- Security Target (As reviewed by the evaluator and agreed with the developer)
  - Unique identification for the DApp evaluated
  - Threats
  - Assumptions
  - Mitigations

- Developer Test results & coverage (an overview?)

- List of vulnerabilities tested & Results of the tests

- List of attacks scenarios performed & Results of the attacks

##### Delivery

The developer shall provide the evaluator the source code of the DAapp in its entirety as it is used by the developers.
The developer shall provide the evaluator the source code of the testing framework used to test the DApp.
The developer shall provide all the necessary information to build the DApp as it is used by the developers, and intended to be used in production.

The evaluator shall check that the DApp can be built from the source code and the instructions provided by the developer.
The evaluator shall check that the DApp can be tested from the source code and the instructions provided by the developer.

The evaluator shall check that the delivered version of the DApp is the one intended to be certified.

##### Functional & Security testing

The developer shall provide a testing suite for the DApp.
The developer shall provide all the necessary information for the tests to be run automatically in a reproducible way.
The developer shall provide the expected results of the tests.
The evaluator shall run the tests and compare the results with the expected results.
The actual results of the tests shall match the expected results.

##### Independent testing

At level 1, the independant testing can only be performed by automated checks from the testing tools. No advanced attack scenarios are expected to be performed, only application of well-known vulnerabilities.

The evaluator shall provide a testing suite that covers well-known security vulnerabilities as described in maintained and openly accessible lists.
The evaluator shall run attacks based on well-known security vulnerabilities and check that the DApp is not vulnerable to them.

##### Coverage

The developer shall provide a test suite that covers all the behaviors of the DApp.
  
- Positive tests: The DApp shall behave as expected when the input is correct.
- Negative tests: The DApp shall handle correctly the incorrect inputs and attacks.

The evaluator shall check that the test suite provided by the developer covers all the behaviors of the DApp and provide. (TODO: What is the expected coverage? What is the coverage criteria?)
The evaluator shall check that no edge cases are left untested even if the coverage criteria is met.

#### Level 2: Certificate broadcast on chain

The broadcasted certificate must follow CIP-0096 schema as a `CERTIFY` certificate with a level of 2.
The off-chain information shall contain the full evaluation report.
The certificate shall be issued to the scripts as computed by the automated tool.


#### Level 3 - Formal Verification

#### Level 3: Overview

Level 3 provides strong guarantees on the correctness of the DApp. The goal of this level is to provide a formal proof that the DApp behaves as expected.

#### Level 3: Requirements

##### Documentation

###### From developer: Dapp description, requirements, test plan and traceability

Same as before + formal model of the DApp

###### From evaluator: Evaluation report

Same as before + evaluation of the formal model + the formalization of the requirements + the proof itself?
Identify any gaps between the formal model and the DApp.

##### Delivery

Same as before + proof should be replayable

##### Functional & Security testing

Same as before + the proof itself

##### Independent testing

Same as before? 

##### Coverage

??

#### Level 3: Certificate broadcast on chain

The broadcasted certificate must follow CIP-0096 schema as a `CERTIFY` certificate with a level of 3.
The off-chain information shall contain the full evaluation report.
The certificate shall be issued to the scripts as computed by the automated tool.

## Rationale: how does this CIP achieve its goals?
<!-- The rationale fleshes out the specification by describing what motivated the design and what led to particular design decisions. It should describe alternate designs considered and related work. The rationale should provide evidence of consensus within the community and discuss significant objections or concerns raised during the discussion.

It must also explain how the proposal affects the backward compatibility of existing solutions when applicable. If the proposal responds to a CPS, the 'Rationale' section should explain how it addresses the CPS, and answer any questions that the CPS poses for potential solutions.
-->

This CIP is based on well established standard in other industries. It provides a clear 

## Path to Active

### Acceptance Criteria
<!-- Describes what are the acceptance criteria whereby a proposal becomes 'Active' -->

### Implementation Plan
<!-- A plan to meet those criteria or `N/A` if an implementation plan is not applicable. -->

<!-- OPTIONAL SECTIONS: see CIP-0001 > Document > Structure table -->

## Copyright
<!-- The CIP must be explicitly licensed under acceptable copyright terms.  Uncomment the one you wish to use (delete the other one) and ensure it matches the License field in the header: -->

<!-- This CIP is licensed under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/legalcode). -->
<!-- This CIP is licensed under [Apache-2.0](http://www.apache.org/licenses/LICENSE-2.0). -->
