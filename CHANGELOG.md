## 0.6.4 (Unreleased)

MISC:

  * Basically the change logs for  VaultSharp till 0.6.4 and follows the changelog 
    for Vault here. (https://github.com/hashicorp/vault/blob/master/CHANGELOG.md)
  * Some of the changes are called out below. But all of Vault 0.6.4 cumulative changes are supported by VaultSharp 0.6.4

DEPRECATIONS/CHANGES:

  * The `InitializeAsync` method now takes a single container object for all parameters, instead of primitive parameters.
    This single container object now has support for the additional recovery fields supported by Vault 0.6.2's initialization.
  * The File Audit backend path json key internally changed from `path` to `file_path`.
  * The `MongoDbGenerateDynamicCredentialsAsync` method now returns `MongoDbUsernamePasswordCredentials` instead of `UsernamePasswordCredentials`.
    This ensures you get the `database` field back as well.
  * The `MicrosoftSqlReadCredentialLeaseSettingsAsync` method now returns the `CredentialTimeToLiveSettings` instead of the deprecated `CredentialTtlSettings` type.
    This is in alignment with Vault deprecating `ttl_max` in favor of `max_ttl`.

FEATURES:

  * New `/sys/wrapping` Apis: Wrap, Rewrap, Lookup and Unwrap.
  * The `UnwrapWrappedResponseDataAsync` method also supports a generic return type to give you strongly typed data back.
    So if you wrapped `AWSCredentials`, then you can unwrap `Secret<AWSCredentials>` instead of `Secret<Dictionary<string, object>>`.
    And at any time if you need the non-generic method, you can always fallback to the non-generic version returning a dictionary.
  * Add support for stored shares, recovery parameters etc. during the initialization of Vault.
  * Supports the new fields (`hmac_accessor`, `jsonx` format etc.) for File and SysLog Audit Backends.
  * The `AWSGenerateDynamicCredentialsWithSecurityTokenAsync` method now supports the `timeToLive` parameter.
  * All the secret backends now support wrapping of the secret into a cubbyhole token.
    * AWS Secret Backend
    * Cassandra Secret Backend
    * Consul Secret Backend
    * Cubbyhole Secret Backend
    * Generic Secret Backend
    * MongoDB Secret Backend
    * Microsoft SQL Secret Backend
    * MySql Secret Backend
    * TBD for PKI Secret Backend
    * PostgreSQL Secret Backend

IMPROVEMENTS:

  * Overall intellisense comments are updated to match the Vault documentation site.
  * The `CassandraRoleDefinition` now supports a consistency level parameter. (defaults to `Quorum`)
  * The `MongoDbGenerateDynamicCredentialsAsync` now returns the database name as well, related to the credentials. 
  * The `MySqlRoleDefinition` now supports the `RevocationSql` parameter to revoke an user.
  * Added `RevocationSql` parameter on the `PostgreSqlRoleDefinition` type to enable customization of user revocation SQL statements.
  * The WriteSecretAsync method now returns data if the underlying data allows for it. [GH-16]

BUG FIXES:

  * Fixed a race condition in the API calls to add the Vault Client Token Header. A single call involves removal and addition of the client token header. 
    Between the removal and addition, some other thread could make the API call, resulting in 401 errors. This is because the HttpClient is shared by all threads.
    The fallacy happens due to messing with Headers at the HttpClient level. 
    The fix was to compose a per thread HttpRequestMessage and set its headers. [GH-13](https://github.com/rajanadar/VaultSharp/issues/13)

## 0.6.1 (October 03, 2016)

MISC:

  * Basically the change log for  VaultSharp 0.6.1 follows the changelog 
    for Vault 0.6.1 here. (https://github.com/hashicorp/vault/blob/master/CHANGELOG.md#061-august-22-2016)
  * Some of the changes are called out below. But all of Vault 0.6.1 changes is supported by VaultSharp 0.6.1

DEPRECATIONS/CHANGES:

  * AppId backend is now deprecated, but still supported. Use AppRole instead.

FEATURES:

  * All the new Authentication backends are now supported: AppRole and AWS-EC2 based login.
  * All the new Secret backends are now supported: MongoDB, MSSQL and RabbitMQ based secret backends
  * All the List Apis are now supported.
  * New Token Apis pertaining to token-roles are now supported.
  * Advanced Health check Api changes
  * Rekey Api changes for Nonce
  * Add convergent encryption support
  * Add support for step-down Api
  * Add support for the capabilities Apis.
  * Add support for the token accessor Apis.

IMPROVEMENTS:

  * You can now provide a delegate for HttpClient to be executed. Use this to set proxy settings, message handlers etc.
  * Upgraded the Json Package dependency to 9.
  * Quick rekey Api is available now.
  * Quick Mount Api is available now.

BUG FIXES:

  * Fixed deadlock issue with Auth login. #5

## 0.4.1 (January 21, 2016)

IMPROVEMENTS:

  * Added extensive XML documentation to the Apis.
  
This is a documentation-addition-only release; other than the version number 
there are no changes from 0.4.0.
  
## 0.4.0 (January 21, 2016)

  * Initial release
  * Parity with Hashicorp's Vault 0.4.1 Api features
