# Auto API

This is an experimental project to make an API standard allowing for a client to determine the contract of any RESTful API resource without need to communicate directly with the API team. Beyond making a standard, I would also like to make a simple JavaScript node package to implement and enforce the standard.

## Purpose

If an API conforms to this standard, it should be possible for a client to traverse and use the entire API without insider knowledge of the API or manually referencing documentation exposing API metadata.

## REST, HATEOAS, HTTP and JSON

Auto API will be fully REST compliant--and that includes HATEOAS. It will also standardized the typical HTTP methods for doing REST with one edition. It will also use JSON exclusively (except when it exposes a resource of another media type via a hypermedia link). This means that Auto API will merely be standardized resource provided by a RESTful API, and not itself a replacement to REST.

## Requirements

### 1) `HELP` Verb for Every Resource

Every resource must support the HTTP `HELP` verb.

#### The URI for accessing `HELP` is identical to the resource URI

| HTTP METHOD | URL | Associated Resource |
|---|---|---|
| `HELP` | `api.example.com` | `/` |
| `HELP` | `api.example.com/users` | `/users` |
| `HELP` | `api.example.com/users/royfielding` | `/users/royfielding` |

#### Help Response

TODO

### 2) Private vs. Hidden

Every resource must register its access level. This is because sometimes private data's very existence needs to be protected. For example, a resource like `api.example.com/users/joe/notes/diary_entry_title_1` should not only hide its _contents_ to unauthorized clients, but also hide its _existence_ to unauthorized clients.<sup>1</sup>

On the server side the access level is either a:

|||
|---|---|
| (a) | Public resource with public data |
| (b) | Public resource with public data<sup>2</sup> and private data |
| (c) | Public resource with public data and hidden private data |
| (d) | Hidden resource with hidden private data |

On the client side the access level is either:

|||
|---|---|
| (a) | Public resource with public data |
| (b) | Public resource with public data and private data |

A mapping the server's account of a resource's access to what the client finds

| Resource's Access Level on Server | Resource's Visibility on Client |
|---|---|
| (a) | (a) |
| (b) | (b) |
| (c) | (a) |
| (d) ||

TODO I'm not sure if this feature is at all necessary for Auto API. I thought it was a cool idea, and maybe it will be useful at this level of abstraction.

### 3) Error Correction

Every resource must provide error correction conforming to the standardization below for all cases of malformed requests. This should be possible once the `HELP` resource is define rigorously enough. This will help developers who attempt to build an API request but make a small mistake. This would be similar to a compilation error when building a project. TODO

### 4) Confident vs. Blind Usage

Every resource must support two modes of request.

| Confident | Blind |
|---|---|
|`Usage-Mode: mode="confident"; sha256="HASH";`||

TODO. It should be possible to hash the response to a `HELP` and pass that hash in a header when doing `GET`s, `POST`s, etc to do ensure there was not a breaking change on the server side before executing.

<sup>1</sup>[GitHub](https://developer.github.com/v3/#authentication) does this very thing in multiple parts of their API to protect the existence of private user resources.

<sup>2</sup>It is possible for public data to be empty. For the purpose of this access level distinction, lacking public data is the same as returning empty public data.
