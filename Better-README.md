# Auto API

This is an experimental project to make an API standard allowing for a client to determine the contract of any RESTful API resource without need to communicate directly with the API team. Beyond making a standard, I would also like to make a simple JavaScript node package to implement and enforce the standard.

## Purpose

If an API conforms to this standard, it should be possible for a client to traverse and use the entire API without insider knowledge of the API or manually referencing documentation exposing API metadata.

## REST, HATEOAS, HTTP and JSON

Auto API will be fully REST compliant--and that includes HATEOAS. It will also standardized the typical HTTP methods for doing REST with one edition. It will also use JSON exclusively (except when it exposes a resource of another media type via a hypermedia link). This means that Auto API will merely be standardized resource provided by a RESTful API, and not itself a replacement to REST.

## Requirements

### 1) GET /api-root/resource?halpmepls=true

Done!

