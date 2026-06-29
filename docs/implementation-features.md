This document provides a best-effort overview of the features offered by various software products that support OpenID Federation. While some of these features are defined directly by the specification, others extend beyond it to address practical considerations and requirements that often arise production federations.

* `?` : not sure
* `NA` : Not Applicable
* ✔ : Supported
* ✘: Not currently supported; however, this does not rule out the possibility of support being added in the future.

Information is taken from public documentation or from testing; it could be wrong. 

| Feature Category | Specification Feature | Shibboleth | SimpleSAMLphp | OFFA | DjangoRP | Shibboleth | SimpleSAMLphp | Inmor | Lighthouse |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| | **(ROLE)**| **OP** | **OP** | **RP** | **RP** | **RP** | **RP** | **TA** | **TA** |
| **Basic** | Publish Entity Configuration, self-signed | ✔ | ✔ | ✔|✔ | ?| ✔| ✔| ✔|
| **Basic** | Issues Entity Statements |✘ |? |? |? |? |? | ✔| ✔|
| **Basic** | Publish JSON Web Key Sets (JWKS) |✔|✔ |✔ |? |? |? | ✔| ✔|
| **HTTP Federation APIs** | `/list` endpoint |✘ |? | ?| ?|? |? | ✔|✔ |
| **HTTP Federation APIs**| `/fetch` endpoint |✔ |✔ |✔ |✔ |? |✔ |✔ | ✔|
| **HTTP Federation APIs**| `/resolve` endpoint | ✔| ✔| ✔| ?| ?| ?| ?| ✔|
| **HTTP Federation APIs**| Support client_authentication |✔ | ?|? |? |? | ? |? |? |
| **Client Registration** | Support Explicit Registration | ✔ | ? | ? |? |? |? |? |? |
| **Client Registration** | Support Dynamic Registration | ✔ | ✔ | ✔ |? |? |? |? |? |
| **Metadata Resolution** | Can Resolve Metadata Internally |✔| ✔|✔|✔ |✔ | ✔ |✔ |✔  |
| **Metadata Resolution** | Can Resolve Metadata From External Resolver |✔| ?|✔|? |? | ? |? |? |
| **Metadata Resolution** | Internal Resolver Supports Metadata Overrides |✔| ?|✔|? |? | ? |? |? |
| **Metadata Resolution** | Internal Resolver Supports Metadata Policies |✔| ?|✔|? |? | ? |? |✔ |
| **Metadata Resolution** | Internal Resolver Supports Metadata Constraints |✔| ?|✔|? |? | ? |? |✔ |
| **Metadata Resolution** | Embedded trust chain validation | ✔ | ? | ? |? |? |? |? |? |
| **Metadata Resolution** | Trust Mark Verification | ✔ | ? | ? |? |? |? |? |? |
| **Trust Marks** | Scope Checking From Trust Marks | ? | ? | ? |? |? |? |? |? |
| **Trust Marks** | Attribute Release Policies From Trust Marks | ✔ | ? | ? |? |? |? |? |? |
| **Key Managment** | Automatic Trust Anchor Key Rotation | ? | ? | ? |? |? |? |? |? |
| **Key Managment** | JWKS Key Rotation | ? | ? | ? |? |? |? |? |? |
| **Key Managment** | Publish Signed JSON Web Key Sets (JWKS) | ? | ? | ? |? |? |? |? |? |
| **Admin UI** | Admin UI User Managment |NA | NA|NA |NA |NA | NA |✔ |✔  |
| **Admin UI** | List Trust Marks |NA | NA|NA |NA |NA | NA |✔ |? |
| **Admin UI** | Get Trust Mark |NA | NA|NA |NA |NA | NA |✔ |? |
| **Admin UI** | Update Trust Mark |NA | NA|NA |NA |NA | NA |✔ |? |
| **Admin UI** | Create Trust Mark For Subject |NA | NA|NA |NA |NA | NA |✔ |✔ |
| **Admin UI** | Support Trust Mark Registration Policies |NA | NA|NA |NA |NA | NA |? |? |
| **Admin UI** | Configure Trust Mark Delegation |NA | NA|NA |NA |NA | NA |? |✔ |
| **Admin UI** | Register Subordinate |NA | NA|NA |NA |NA | NA |✔ |✔  |
| **Admin UI** | Support Subordinate Registration Policies |NA | NA|NA |NA |NA | NA |? |?  |
| **Admin UI** | Suspend Subordinate |NA | NA|NA |NA |NA | NA |? |✔  |
| **Admin UI** | Approve Subordinate |NA | NA|NA |NA |NA | NA |? |✔  |
| **Admin UI** | Remove Subordinate |NA | NA|NA |NA |NA | NA |? |✔  |
| **Admin UI** | Update Subordinate |NA | NA|NA |NA |NA | NA |✔ |✔  |
| **Admin UI** | Configure Subordinate Metadata (overrides) |NA | NA|NA |NA |NA | NA |? |✔  |
| **Admin UI** | Configure Subordinate Metadata Policies |NA | NA|NA |NA |NA | NA |? |✔  |
| **Admin UI** | Preview Subordinate Statements |NA | NA|NA |NA |NA | NA |? |✔  |
| **Admin UI** | Signing Key CRUD operations |NA | NA|NA |NA |NA | NA |✔ |?  |
| **Admin UI** | Signing Key signing algorithm and key rotation operations |NA | NA|NA |NA |NA | NA |✔ |?  |
| **Admin UI** | Get OIDFederation Subordinate Events (1.0) |NA | NA|NA |NA |NA | NA |✔ |?  |


