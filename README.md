[![CircleCI](https://circleci.com/gh/adobe/commerce-cif-graphql-client.svg?style=svg)](https://circleci.com/gh/adobe/commerce-cif-graphql-client)
[![codecov](https://codecov.io/gh/adobe/commerce-cif-graphql-client/branch/master/graph/badge.svg)](https://codecov.io/gh/adobe/commerce-cif-graphql-client)
[![Maven Central](https://img.shields.io/maven-central/v/com.adobe.commerce.cif/graphql-client.svg)](https://search.maven.org/search?q=g:com.adobe.commerce.cif%20AND%20a:graphql-client)

# GraphQL client

This project is a GraphQL client for AEM. It is an OSGi bundle that can be instantiated with an OSGi configuration in the AEM OSGi configuration console. It can also be instantiated directly with java code.

## Installation

To build and install the latest version in a running AEM instance, simply do

```
mvn clean install sling:install
```
This installs everything by default to `localhost:4502` without any context path. You can also configure the install location with the following maven properties:
* `aem.host`: the name of the AEM instance
* `aem.port`: the port number of the AEM instance
* `aem.contextPath`: the context path (if any) of your AEM instance, starting with `/`

## Using the GraphQL client

To use this library in your project, just add the following maven dependency to your project and install the bundle in your AEM instance:

```xml
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>...</version>
    <scope>provided</scope>
</dependency>
```

You'll then have to setup and configure the client in your AEM instance.

## OSGi configuration

To instantiate instances of this GraphQL client, simply go the AEM OSGi configuration console and look for "GraphQL Client Configuration Factory". Add a configuration and set the following mandatory parameters:
* `identifier`: must be unique among all GraphQL clients.
* `url`: the URL of the GraphQL server endpoint used by this client.
* `httpMethod`: the default HTTP method used to send requests, can be either GET or POST. This can be overriden on a request basis.

The `identifier` is used by the adapter factory to resolve clients via the `cq:graphqlClient` property set on any JCR node. When this is set on a resource or the resource ancestors, one can write `GraphqlClient client = resource.adaptTo(GraphqlClient.class);`.

## Releases to Maven Central

Releases are triggered by manually running `mvn release:prepare release:clean` on the `master` branch. This automatically pushes a commit with a release git tag like `graphql-client-x.y.z.` which triggers a dedicated `CircleCI` build that performs the deployment of the artifact to Maven Central.

## Code Formatting
You can find the code formatting rules in the `eclipse-formatter.xml` file. The code formatting is automatically checked for each build. To automatically format your code, please run:
```bash
mvn clean install -Pformat-code
```

### Contributing
 
Contributions are welcomed! Read the [Contributing Guide](.github/CONTRIBUTING.md) for more information.
 
### Licensing
 
This project is licensed under the Apache V2 License. See [LICENSE](LICENSE) for more information.
