| Feature Category | Specification Feature | Shibboleth | SimpleSAMLphp | OFFA | DjangoRP | Shibboleth | SimpleSAMLphp | Inmor | Lighthouse |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| | **(ROLE)**| **OP** | **OP** | **RP** | **RP** | **RP** | **RP** | **TA** | **TA** |
| **Basic** | Publish Entity Configuration, self-signed | ✔ | ✔ | ✔|✔ | NA| ✔| ✔| ✔|
| **Basic** | Issues Entity Statements |✘ |? |? |? |NA |? | ✔| ✔|
| **Basic** | Publish JSON Web Key Sets (JWKS) |✔|? |? |? |NA |? | ✔| ✔|
| **HTTP Federation APIs** | `/list` endpoint |✘ |✘ | ?| ?|NA |? | ✔|✔ |
| **HTTP Federation APIs**| `/fetch` endpoint |✔ |✔ |✔ |✔ |NA |✔ |✔ | ✔|
| **HTTP Federation APIs**| `/resolve` endpoint | ✔| ✔| ✔| ?| NA| ?| ✘| ✔|
| **HTTP Federation APIs**| Support client_authentication |✔ | ?|? |? |NA | ? |? |? |
| **Client Registration** | Explicit Registration | ✔ | ? | ? |? |? |? |? |? |
| **Client Registration** | Dynamic Registration | ✔ | ✔ | ✔ |? |? |? |? |? |
| **Metadata Resolution** | Can Resolve Metadata, Internally |✔| ✔|✔|✔ |✔ | ✔ |✔ |✔  |
| **Metadata Resolution** | Can Resolve Metadata From External Resolver |✔| ?|✔|? |? | ? |? |? |
| **Metadata Resolution** | Internal Resolver Supports Metadata Overrides |✔| ?|✔|? |? | ? |? |? |
| **Metadata Resolution** | Internal Resolver Supports Metadata Policies |✔| ?|✔|? |? | ? |? |✔ |
| **Metadata Resolution** | Embedded trust chain validation | ? | ? | ? |? |? |? |? |? |
| **Trust Marks** | Scope Checking From Trust Marks | ? | ? | ? |? |? |? |? |? |
| **Trust Marks** | Attribute Release Policies From Trust Marks | ? | ? | ? |? |? |? |? |? |
| **Key Managment** | Automatic Trust Anchor Key Rotation | ? | ? | ? |? |? |? |? |? |
| **Key Managment** | JWKS Key Rotation | ? | ? | ? |? |? |? |? |? |
| **Admin UI** | Admin UI User Managment |✘ | ✘|✘ |✘ |✘ | ✘ |✔ |✔  |
| **Admin UI** | List Trust Marks |✘ | ✘|✘ |✘ |✘ | ✘ |✔ |? |
| **Admin UI** | Get Trust Mark |✘ | ✘|✘|✘ |✘ | ✘ |✔ |? |
| **Admin UI** | Update Trust Mark |✘ | ✘|✘|✘ |✘ | ✘ |✔ |? |
| **Admin UI** | Create Trust Mark For Subject |✘ | ✘|✘|✘ |✘ | ✘ |✔ |✔ |
| **Admin UI** | Configure Trust Mark Delegation |✘ | ✘|✘|✘ |✘ | ✘ |? |✔ |
| **Admin UI** | Register Subordinate |✘ | ✘|✘|✘ |✘ | ✘ |✔ |✔  |
| **Admin UI** | Suspend Subordinate |✘ | ✘|✘|✘ |✘ | ✘ |? |✔  |
| **Admin UI** | Approve Subordinate |✘ | ✘|✘|✘ |✘ | ✘ |? |✔  |
| **Admin UI** | Remove Subordinate |✘ | ✘|✘|✘ |✘ | ✘ |? |✔  |
| **Admin UI** | Update Subordinate |✘ | ✘|✘|✘ |✘ | ✘ |✔ |✔  |
| **Admin UI** | Configure Subordinate Metadata (overrides) |✘ | ✘|✘|✘ |✘ | ✘ |? |✔  |
| **Admin UI** | Configure Subordinate Metadata Policies |✘ | ✘|✘|✘ |✘ | ✘ |? |✔  |
| **Admin UI** | Preview Subordinate Statements |✘ | ✘|✘|✘ |✘ | ✘ |? |✔  |
| **Admin UI** | Signing Key CRUD operations |✘ | ✘|✘|✘ |✘ | ✘ |✔ |?  |
| **Admin UI** | Signing Key signing algorithm and key rotation operations |✘ | ✘|✘|✘ |✘ | ✘ |✔ |?  |
| **Admin UI** | Get OIDFederation Subordinate Events (1.0) |✘ | ✘|✘|✘ |✘ | ✘ |✔ |?  |


