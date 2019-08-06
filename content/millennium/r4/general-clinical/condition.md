---
title: Condition | R4 API
---

# Condition

* TOC
{:toc}

## Overview

The Condition resource is used to record problems, diagnoses, or other health matters that are concerning to a patient. Depending on the site, problems and diagnoses are used in different ways. Diagnoses are recorded on an encounter to document conditions addressed or treated during a specific patient visit. For U.S. clients, diagnoses support financial or reimbursement workflows. Problems are on-going or chronic conditions that are managed over every visit and not associated to a specific encounter. A condition may be both a diagnosis and a problem. Conditions, specifically diagnoses, are often associated to orders to document the medical necessity of a specific medication or procedure order and may be referenced by other resources as a “reason” for an action or order. Health concerns are also returned as part of the Condition resource and represent other concerns a patient may have such as financial or social risks.

The following fields are returned if valued:

* [Id](https://hl7.org/fhir/R4/resource-definitions.html#Resource.id)
* [Clinical status](https://hl7.org/fhir/R4/condition-definitions.html#Condition.clinicalStatus)
* [Verification status](https://hl7.org/fhir/R4/condition-definitions.html#Condition.verificationStatus)
* [Category](https://hl7.org/fhir/R4/condition-definitions.html#Condition.category)
* [Severity](https://hl7.org/fhir/R4/condition-definitions.html#Condition.severity)
* [Condition code](https://hl7.org/fhir/R4/condition-definitions.html#Condition.code)
* [Patient](https://hl7.org/fhir/R4/condition-definitions.html#Condition.subject)
* [Patient encounter when first recorded (only applies to diagnoses)](https://hl7.org/fhir/R4/condition-definitions.html#Condition.encounter)
* [Onset (dateTime)](https://hl7.org/fhir/R4/condition-definitions.html#Condition.onset_x_)
* [Resolved date  (only applies to problems)](https://hl7.org/fhir/R4/condition-definitions.html#Condition.abatement_x_)
* [Date recorded](https://hl7.org/fhir/R4/condition-definitions.html#Condition.recordedDate)
* [Who recorded the condition](https://hl7.org/fhir/R4/condition-definitions.html#Condition.recorder)
* [Comment/Note](https://hl7.org/fhir/R4/condition-definitions.html#Condition.note)

## Terminology Bindings

<%= terminology_table(:condition, :r4) %>

## Search

Search for Conditions that meet supplied query parameters:

    GET /Condition?:parameters

_Implementation Notes_

* Currently `problem-list-item` is supported.

### Authorization Types

<%= authorization_types(practitioner: true, patient: false, system: true) %>

### Parameters

 Name               | Required?          | Type          | Description
--------------------|--------------------|---------------|-----------------------------------------------------------------------
 `patient`          | This or `subject`  | [`reference`] | Who the condition is for. Example: `12345`
 `subject`          | This or `patient`  | [`reference`] | Who the condition is for. Example: `12345`
 `clinical-status`  | No                 | [`token`]     | The clinical status of the condition. Example: `active`, `inactive`, `resolved`
 `category`         | No                 | [`token`]     | The category of the condition. Category problem-list-item is supported as of now. Example: `problem-list-item`

### Headers

 <%= headers fhir_json: true %>

### Example

#### Request

    GET https://fhir-open.sandboxcerner.com/r4/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Condition?patient=1316024

#### Response

<%= headers status: 200 %>
<%= json(:r4_condition_bundle) %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

[`reference`]: https://hl7.org/fhir/r4/search.html#reference
[`token`]: https://hl7.org/fhir/R4/search.html#token
[errors]: ../../#client-errors
[OperationOutcomes]: https://hl7.org/fhir/R4/operationoutcome.html