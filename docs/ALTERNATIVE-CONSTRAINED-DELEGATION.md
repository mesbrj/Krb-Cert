## kerby realm alternative constrained delegation:

The kerby-instruments HTTPS (Kerberos authenticated) endpoints for delegation services, needs to be used for service principals (servers) needing to authenticate on-behalf of users.

The kerby-instruments will generate and validate the user-principal JWT via Client Credentials flow and will use a changed JWT with the correct claims. After all policy validations, the delegation can be processed (if the case) and the JWT will be sended as a cryptographic text material to the service principal. The service principal will use the KrbClient (Apache Kerby lib) and request (on-behalf a user via decrypted JWT) a service-ticket for the other service-principal.
![](/docs/alternative-constrained-delegation.png)
Here we achieved a constrained delegation in a *"FORWARDABLE + OK-AS-DELEGATE level"* without using the kerberos protocol or data structures from Kerberos tickets.
The kerby-instruments (a KDC extension service) can act on-behalf of the user without user interaction and can apply policies on delegation requests, but in a *"FORWARDABLE + OK-AS-DELEGATE level"*. When the service principal get the user principal JWT, it can be used to request a TGT and service-tickets (for any another service-principal) on-behalf of the user.