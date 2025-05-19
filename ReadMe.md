# Custom API Call Policy on Mule 4

This guide provides instructions for creating, configuring, and deploying a custom Mule 4 policy that sends incoming request payloads and headers to an external API endpoint (e.g., a webhook) when a request is received.

## Prerequisites

- Refer to the top-level `README.md` for prerequisites (Java 17, Anypoint Studio 7.21.0, MuleSoft account) and `settings.xml` setup.

## Creating a Custom API Call Policy

Reference: MuleSoft Custom Policy Documentation

A sample custom policy is available in this directory (`custom-api-call-policy`).

### Steps

1. **Obtain Organization ID**:

   - Go to https://anypoint.mulesoft.com/accounts/businessGroups.
   - Select your business group and note the **Business Group ID**.

2. **Update the groupId of the policy**:

- Open treblle-policy/pom.xml
- Change <groupId>{Use Business Group ID here}</groupId>

3. **Update Credentials**

In order to add the custom policy to the organization, we have to build and push the policy to the MuleSoft. Hence we need to update the credentials.

- Navigate to samples/.m2/settings.xml
- Update the credentials

  ```
  <username>{MuleSoft Username}</username>
  <password>{MuleSoft Password}</password>
  ```

4. **Push the API Policy to the Mule Exchange**

- Build and push the API policy (Execute this inside the treblle-policy/ folder)

  ```
  mvn -s ../samples/.m2/settings.xml clean package
  mvn -s ../samples/.m2/settings.xml clean deploy
  ```

5. **Verify Policy**:

- Visit https://anypoint.mulesoft.com/exchange.
- Search for **treblle policy** to confirm the policy is available.

## Applying the Policy

1. **Apply Policy in API Manager**:

- In Anypoint Platform, navigate to **API Manager**.
- Select your API (e.g., `hello-world`).
- Go to **Policies** and click **Apply New Policy**.
- Choose **treblle-policy** from the list.
- Configure the policy with the following values:
  - **API Key**: `API Key`
  - **SDK Token**: `SDK token`
  - **Mask Keywords**: `Comma-separated list of masking keywords`


2. **Save and Apply**:

- Save the policy configuration and apply it to the API.

3. **Invoke the API**:

- Invoke the API and check Treblle Dashboard.

