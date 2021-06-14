# Cloud Computing
- https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-145.pdf
- Essential Characteristics:
  - On-demand self-service. 
    - Can provision capabilities as needed without requiring human interaction.
    - A consumer can unilaterally provision computing capabilities, such as
server time and network storage, as needed automatically without requiring human
interaction with each service provider.

  - Broad network access. 
    - Capabilities are available over the network and accessed through standard
mechanisms that promote use by heterogeneous thin or thick client platforms (e.g.,
mobile phones, tablets, laptops, and workstations).
  - Resource pooling. 
    - The provider’s computing resources are pooled to serve multiple consumers
using a multi-tenant model, with different physical and virtual resources dynamically
assigned and reassigned according to consumer demand. There is a sense of location
independence in that the customer generally has no control or knowledge over the exact
location of the provided resources but may be able to specify location at a higher level of
abstraction (e.g., country, state, or datacenter). Examples of resources include storage,
processing, memory, and network bandwidth.
  - Rapid elasticity. 
    - Capabilities can be elastically provisioned and released, in some cases
automatically, to scale rapidly outward and inward commensurate with demand. To the
consumer, the capabilities available for provisioning often appear to be unlimited and can
be appropriated in any quantity at any time.
  - Measured service. 
    - Cloud systems automatically control and optimize resource use by leveraging
a metering capability1 at some level of abstraction appropriate to the type of service (e.g.,
storage, processing, bandwidth, and active user accounts). Resource usage can be
monitored, controlled, and reported, providing transparency for both the provider and
consumer of the utilized service.

  - Service Models:
    - Software as a Service (SaaS). 
      - The capability provided to the consumer is to use the provider’s
applications running on a cloud infrastructure. The applications are accessible from
various client devices through either a thin client interface, such as a web browser (e.g.,
web-based email), or a program interface. The consumer does not manage or control the
underlying cloud infrastructure including network, servers, operating systems, storage, or
even individual application capabilities, with the possible exception of limited userspecific application configuration settings.
    - Platform as a Service (PaaS). 
      - The capability provided to the consumer is to deploy onto the cloud
infrastructure consumer-created or acquired applications created using programming
