Version: NAFATH-V2
Track: Software 

## Overview
A 5G service for emergency responders must stay reliable during congestion, outages, and cyberattacks. A responder's mobile app stores reports offline and synchronizes them when connectivity returns, using HTTP requests that server software must handle safely when retried. These requests travel over 5G network slicing, which can give responders a dedicated slice. Cybersecurity teams protect that service and follow an incident response process when it is attacked. Usage data, organized into reports by region and day, shows where demand is growing, and an AI model trained on this data can predict congestion before it affects responders. Each field supports the others, so a weakness in one can reduce the reliability of the whole service.

## Software
Safe HTTP methods are read-only. GET, HEAD, OPTIONS and TRACE are safe. Idempotent methods have the same intended effect on the server whether a request is sent once or many times. PUT, DELETE and all safe methods are idempotent, but not every idempotent method is safe: DELETE changes data. If a response is lost, retrying an idempotent request is generally safe. Retrying POST may create duplicate incident reports, so applications can use idempotency keys to prevent duplicate processing.

Resource: RFC 9110 - HTTP Semantics - https://www.rfc-editor.org/rfc/rfc9110.html#section-9.2 

## AI
Overfitting happens when a model learns noise and training-specific patterns, performing well on training data but poorly on new data. Cross-validation divides data into several parts, using each part for validation while training on the rest. This provides multiple performance estimates and helps identify overfitting. For example, a network congestion model might learn normal weekly patterns but fail during a disaster or large event. Cross-validation helps assess whether the model generalizes beyond its training data.

Resource: scikit-learn - Cross-validation: evaluating estimator performance - https://scikit-learn.org/stable/modules/cross_validation.html 

## Mobile
An offline-first mobile app stores essential data locally, so users can view information and record updates without internet access. When connectivity returns, the app sends queued changes to the server and fetches new data. It should detect conflicting edits and resolve them with clear rules. For emergency teams, the app must show whether a report is saved locally, pending synchronization, or confirmed by the server, so users never assume an unsent report was delivered.

Resource: Android Developers - Build an offline-first app - https://developer.android.com/topic/architecture/data-layer/offline-first

## Networking
5G network slicing lets an operator run several core networks at the same time, each specialized for a given set of services or subscribers. An emergency-response slice could be dedicated to responders, so their traffic is handled separately from ordinary subscribers, with the operator configuring its resources and policies to prioritize reliable, low-latency communication. However, slicing alone cannot guarantee service during every outage or disaster.

Resource: 3GPP - 5G System Overview - https://www.3gpp.org/technologies/5g-system-overview

## Cybersecurity
NIST SP 800-61 Rev. 3 shows incident response through Detect, Respond and Recover activities. Govern, Identify and Protect help organizations prepare for incidents, but they are not part of the response itself. In a DDoS attack on an emergency service, Detect identifies abnormal traffic, Respond contains the attack (for example, by filtering malicious traffic and prioritizing emergency users), and Recover restores affected services. Lessons learned support continuous improvement across all six CSF 2.0 functions.

Resource: Incident Response | CSRC - https://csrc.nist.gov/projects/incident-response

## Data
A star schema has a central fact table that stores measurements and dimension keys, linked directly to dimension tables for filtering and grouping. A snowflake schema normalizes dimensions into several related tables, such as product, subcategory and category. For daily usage reports by region, I would choose a star schema because its simpler structure makes reporting easier to understand and query. Snowflake designs reduce redundancy but can require more joins and a more complex query structure.

Resource: Understand star schema and the importance for Power BI - https://learn.microsoft.com/en-us/power-bi/guidance/star-schema 

## Misconception in My Track

## Open Question
