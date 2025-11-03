
# OpenID Federation Test Cases

This document defines test cases for OpenID Federation in eduGAIN. This includes interoprability tests for Trust Anchors, Relying Party's, and OpenID Providers. 

---

## Test Preconditions and Dependencies

| Ref | Area | Preconditions / Dependencies |
|------|------|-------------------------------| 
| **P-01** | Federation Entities | Valid OP and RP federation entity configurations are available, each with correct metadata and signing keys. |
| **P-02** | Trust Anchor Endpoints | The TA exposes `/fetch`, `/list`, and `/resolve` endpoints per OpenID Federation specification. |
| **P-03** | Network & Authentication | All components (TA, OP, RP) can communicate over HTTPS. |
| **P-04** | Trust Marks | Trust mark issuers and validation endpoints are available and reachable. |
| **P-05** | Logging & Monitoring | Logging enabled on TA, OP, and RP components to record enrolment, key, and trust evaluation events. |


## Test Architectures

| Ref | Type | Topology | Description |
|------|-----------|-----------|-------------------------------|
| **TA-01** | Basic | Single TA with OP and RP | A single Trust Anchor managing enrolment and trust for one OP and one RP. |
| **TA-02** | Hierarchical Single-Root | Single root TA with a Single intermediate authority and one OP and one RP | A root Trust Anchor delegates trust to a subordinate intermediate, which in turn manages its own OP and RP. |
| **TA-03** | Hierarchical Multi-Root | Two root TAs each with a single intermediate authority, each intermediate with one OP and one RP | More than one root Trust Anchor delegates trust to a subordinate intermediate, which in turn manage their own OPs and RPs. |



## Federation Enrolment Test Cases

| Ref | Arch | Type | Test Name | Objective / Test Description | Validation / Expected Result |
|------|------|-----------|-----------|-------------------------------|------------------------------|
| **FE-01** | TA-01 | Enrolment | Enrolment of an RP into a Trust Anchor | Verify that a Relying Party (RP) can be successfully enrolled into a federation Trust Anchor. | The enrolled entity is correctly listed at the `/list` endpoint and Entity Statements are issued about them from the `/fetch` endpoint. |
| **FE-02** | TA-01 | Enrolment | Enrolment of an OP into a Trust Anchor | Verify that an OpenID Provider (OP) can be successfully enrolled into a federation Trust Anchor. | The enrolled entity is correctly listed at the `/list` endpoint and Entity Statements are issued about them from the `/fetch` endpoint. |
| **FE-03** | TA-01 | Enrolment | Enrolment of a Trust Anchor into another Trust Anchor | Verify that a Trust Anchor can be successfully enrolled as an intermediate into another federation Trust Anchor. | The enrolled entity is correctly listed at the `/list` endpoint and Entity Statements are issued about them from the `/fetch` endpoint. |
| **FE-04** | TA-01 | Enrolment | Conditional Enrolment Based on Entity Identifier Policy | Test enrolment of an OP when subject to federation policies that only permits the OP by Entity Identifier. | The OP is correctly listed at the `/list` endpoint and an Entity Statement is issued about it from the `/fetch` endpoint. |
| **FE-05** | TA-01 | Enrolment | Conditional Enrolment Based on Entity Identifier Policy | Test enrolment of an OP when subject to federation policies that do *not* permit the OP by Entity Identifier. | The OP is not listed at the `/list` endpoint and an Entity Statement is *not* issued about them from the `/fetch` endpoint. |
| **FE-06** | TA-01 | Enrolment | Conditional Enrolment Based on Trust Marks | Test enrolment of an OP that has an eduGAIN Trust Mark when subject to federation policies that require an eduGAIN Trust Mark. | The OP is listed at the `/list` endpoint and an Entity Statement is issued about them from the `/fetch` endpoint. |
| **FE-07** | TA-01 | Enrolment | Conditional Enrolment Based on Trust Marks | Test enrolment of an OP that does **not** have an eduGAIN Trust Mark when subject to federation policies that require an eduGAIN Trust Mark. | The OP is not listed at the `/list` endpoint and an Entity Statement is *not* issued about them from the `/fetch` endpoint. |
| **FE-08** | TA-01 | Enrolment | Conditional Enrolment Based on Entity Identifier Policy | Test enrolment of an RP when subject to federation policies that only permits the RP by Entity Identifier. | The RP is correctly listed at the `/list` endpoint and an Entity Statement is issued about it from the `/fetch` endpoint. |
| **FE-09** | TA-01 | Enrolment | Conditional Enrolment Based on Entity Identifier Policy | Test enrolment of an RP when subject to federation policies that do *not* permit the RP by Entity Identifier. |  The RP is not listed at the `/list` endpoint and an Entity Statements is *not* issued about it from the `/fetch` endpoint. |
| **FE-10** | TA-01 | Enrolment | Updating an Enrolled Entity | Allow an existing entity registration to be updated by its owner. | The entity registration is updated; only the owner can update; non-owners are rejected. |
| **FE-11** | TA-01 | Enrolment | Enrolment with Specific Display Name Attribute | Verify that entities can be enrolled with TA-authorised attributes (like `display_name`) overriding self-asserted values. | Entity Statements published via `/fetch` contain the required attributes encoded in the `metadata` claim |
| **FE-12** | TA-01 | Unenrolment | Unenroll an RP from the Trust Anchor | Ensure the RP can be removed from the federation Trust Anchor. | Unenrolled entities are not listed or trusted by the TA; they do not appear in `/list`, and `/fetch` will not issue Entity Statements about it. |
| **FE-13** | TA-01 | Unenrolment | Unenroll an OP from the Trust Anchor | Ensure the OP can be removed from the federation Trust Anchor. | Unenrolled entities are not listed or trusted by the TA; they do not appear in `/list`, and `/fetch` will not issue Entity Statements about it. |


---

## Key Management Test Cases

| Ref | Arch | Type | Test Name | Objective / Test Description | Validation / Expected Result |
|------|-----|-----------|-----------|-------------------------------|------------------------------|
| **KM-01**| TA-01 | Key Rollover | Adding New Federation Signing Keys | Validate that new signing keys can be added to the TA’s JWK set, signed with the existing key, and leaf entities can replace their existing, trusted, TA key with the new key | Entities recognize the new key as a trusted key |
| **KM-02**| TA-01 | Key Rollover | Adding New Federation Signing Keys | Validate that the new signing keys established in KM-01 are trusted | Entities recognize the new key as a trusted key, and correctly verify documents signed with the new key |
| **KM-03** | TA-01 | Key Rollover | Removing Old Federation Signing Keys | Ensure old signing keys can be safely removed from the TA’s JWK set. | Only current keys are trusted; deprecated keys appear only in historical listings `federation_historical_keys`. |
| **KM-04** | TA-01 | Key Revocation | Revocation of TA Signing Keys | Test the impact of revoking a TA’s signing key. | Documents signed with revoked keys are rejected; trust is not established. |
| **KM-05** | TA-01 | Key Revocation | Revocation of OP Federation Signing Keys | Ensure that revoking an OP’s federation signing key prevents trust establishment. | OP federation documents are no longer trusted. |
| **KM-06** | TA-01 | Key Revocation | Revocation of RP Federation Signing Keys | Ensure that revoking an RP’s federation signing key prevents trust establishment. | RP federation documents are no longer trusted. |

---

## Trust Mark Test Cases

| Ref | Arch | Category | Test Name | Objective / Test Description | Validation / Expected Result |
|------|------|-----------|-----------|-------------------------------|------------------------------|
| **TM-01** | TA-01 | Trust Mark Issuance | Issuing Federation Membership Trust Marks | Validate a federation membership trust mark, e.g., eduGAIN, can be correctly issued to an OP | The trust mark is correctly formatted and signed. |
| **TM-02** | TA-01 | Trust Mark Issuance | Issuing Federation Membership Trust Marks | Validate a federation membership trust mark, e.g., eduGAIN, can be correctly issued to an RP | The trust mark is correctly formatted and signed. |
| **TM-03** | TA-01 | Trust Mark Usage | Enforcing Federation Membership via Trust Marks | Ensure that trust marks are used by an RP to influence interoperability and trust decisions. | Ensure the OP requires an RP to contain the eduGAIN trust mark. |
| **TM-04** | TA-01 | Trust Mark Usage | Enforcing Federation Membership via Trust Marks | Ensure that trust marks are used by an RP to influence interoperability and trust decisions. | Ensure the RP requires an OP to contain the eduGAIN trust mark. |
| **TM-05** | TA-01 | Trust Mark Revocation | Handling Invalid / Revoked / Expired Trust Marks | Verify that a revoked or expired eduGAIN trust mark on the RP prevents trust establishment at the OP. | Trust is not established; trust mark status endpoint at the TA reflects the correct trust mark status (`/federation_trust_mark_status_endpoint`). |
| **TM-06** | TA-01 | Trust Mark Revocation | Handling Invalid / Revoked / Expired Trust Marks | Verify that a revoked or expired eduGAIN trust mark on the OP prevents trust establishment at the RP. | Trust is not established; trust mark status endpoint at the TA reflects the correct trust mark status (`/federation_trust_mark_status_endpoint`). |
| **TM-06** | TA-01 | Trust Mark Delegation | Trust Mark Delegation | *TBD* | *TBD* |

---

## Federation Entity Discovery & Metadata Handling Test Cases

| Ref | Arch | Type | Test Name | Objective / Test Description | Validation / Expected Result |
|------|-----|-----------|-----------|-------------------------------|------------------------------|
| **FD-01** | TA-01 | Trust Path Resolution | Handling embedded Trust Chains in RP’s Authentication Request | Confirm that an OP can parse and validate embedded trust chains inside a Request Object. | OP successfully establishes trust if the embedded chain is valid. |
| **FD-02** | TA-01 | Trust Path Resolution | Expired Entity Statement in Embedded Trust Chain | Ensure an OP rejects trust paths containing expired Entity Statements in the Trust Chain of a Request Object. | OP rejects the embedded Trust Chain but succeeds via Federation Entity Discovery. |
| **FD-03** | TA-01 | Trust Path Resolution | Expired Entity Statement in RP’s Trust Chain | Ensure OP rejects trust paths containing expired Entity Statements during Federation Entity Discovery. | OP fails to establish trust due to an expired Entity Statement. |
| **FD-04** | TA-03 | Trust Path Resolution | Multiple Trust Paths | Validate that the OP selects the shortest, valid trust path among multiple available. | OP selects the shortest, common, valid trust path and successfully establishes trust with the RP. |
| **FD-05**| TA-01 | Metadata Constraints  | Allowed Entity Types | TA policy allows only `openid_relying_party` and `openid_provider` entities | An entity registers as a `relying_party` but later changes to a `federation_entity` |Trust chain resolution fails |
| **FD-06** | TA-01 | Metadata Constraints | Maximum Trust Path Length | TA policy defines `max_path_length = 1`. A trust chain of 2 entities is presented. | Trust chain resolution fails as max path length is exceeded.|
| **FD-07**| TA-01 | Metadata Policy | Add Metadata Field | TA policy adds TA contact information into the OP/RPs metadata | Resolved metadata contains the added contact information.|
| **FD-08** | TA-01 | Metadata Policy | Algorithm Constraints | TA policy allows only `RS256` for `id_token` signing. OP/RP publishes unsupported signing algorithm, `ES256`, in its Entity Configuration metadata. | Trust chain validation fails; entity is not supported. | 
| **FD-09** | TA-01 | Metadata Augmentation | TA Asserted Values | Ensure TA-defined metadata overrides (e.g., `display_name`, `organization_name`) take precedence over self-asserted ones. | Clients use TA-defined values. |
| **FD-10** | TA-01 | Metadata Augmentation | Metadata Provided by the Trust Anchor | Verify that TA-provided metadata for an OP is correctly applied during trust resolution. | TA-provided metadata is visible in resolved configurations. |



---

## Client Registration Test Cases

| Ref | Arch | Category | Test Name | Objective / Test Description | Validation / Expected Result |
|------|-----|-----------|-----------|-------------------------------|------------------------------|
| **CR-01** | TA-01 | Explicit Registration | Successful Registration | Validate that an RP using `client_secret_basic` client authentication an explicitly register with an OP. | RP receives valid credentials (`client_id`, `client_secret`) and can authenticate in subsequent OpenID Connect interactions. |
| **CR-02** | TA-01 | Explicit Registration | Unsuccessful Registration | Ensure proper error handling when trust cannot be established. | OP returns compliant error response when registration fails. |
| **CR-03** | TA-01 | Automatic Registration | Successful Registration | Verify that an RP can automatically register with an OP using a signed Request Object JWT. | RP receives valid authentication response; trust established. |
| **CR-04** | TA-01 | Automatic Registration | Successful Registration | Verify that an RP can automatically register with an OP using a signed and encrypted Request Object JWT. | RP receives valid authentication response; trust established. |
| **CR-05** | TA-01 | Automatic Registration | Unsuccessful Registration | Ensure automatic registration fails gracefully when trust cannot be established. | Confirm that the OP terminates the flow with an appropriate error response and does not perform a redirect to the `redirect_uri`. |

---

## Client Authentication Test Cases

| Ref | Arch |  Type | Test Name | Objective / Test Description | Validation / Expected Result |
|------|-----|-----------|-----------|-------------------------------|------------------------------|
| **CA-01** | TA-01 | Endpoint Authentication | `/resolve` Endpoint Authentication | Ensure that clients must authenticate to access the resolution functionality. | Only authenticated clients can retrieve resolved Entity Statements. |
| **CA-02** | TA-01 | Endpoint Authentication | `/fetch` Endpoint Authentication | Validate that client authentication is required to fetch Entity Statements. | Only authenticated clients can access signed Entity Statements. |
| **CA-03** | TA-01 | Endpoint Authentication | `/list` Endpoint Authentication | Check that client authentication is required to list entities. | Only authenticated clients can retrieve entity lists. |

---



