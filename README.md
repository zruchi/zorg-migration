# Zorg Migration

[Link](https://zendesk.atlassian.net/wiki/spaces/PGM/pages/5413177080/Process+for+migrating+ZORG+upstreams+to+Istio+routing#Step-2%3A-verify-that-the-service-does-not-depend-on-the-Host-header) to wiki page.

## Procedure
1. Apply envoy filter `envoy-filter-host-header.yaml` to change `Host` header value to random string. 
2. Apply envoy filter `access-log.yaml` to log the request. 
3. Perform testing with service owner, if errors occured then the application is using the `Host` header to extract the customer `subdomain`. This means service owner will need to make a change in their application code to extract host instead from either `X-Zendesk-Original-Host` or `x_forwarded_for` header which `zorg` will once the call passes through.

## Traffic flow before and after

### Before 

![Before migration traffic flow](./images/before.svg)

### After

![After migration traffic flow](./images/after.svg)