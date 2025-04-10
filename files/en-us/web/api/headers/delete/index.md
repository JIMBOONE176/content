---
title: "Headers: delete() method"
short-title: delete()
slug: Web/API/Headers/delete
page-type: web-api-instance-method
browser-compat: api.Headers.delete
---

{{APIRef("Fetch API")}} {{AvailableInWorkers}}

The **`delete()`** method of the {{domxref("Headers")}}
interface deletes a header from the current `Headers` object.

For security reasons, some headers can only be controlled by the user agent. These
headers include the {{Glossary("Forbidden_request_header", "forbidden request headers")}}
and {{Glossary("Forbidden_response_header_name", "forbidden response header names")}}.

## Syntax

```js-nolint
delete(name)
```

### Parameters

- `name`
  - : The name of the HTTP header you want to delete from the `Headers` object.

### Return value

None ({{jsxref("undefined")}}).

## Examples

Creating an empty `Headers` object is simple:

```js
const myHeaders = new Headers(); // Currently empty
```

You could add a header to this using {{domxref("Headers.append")}}:

```js
myHeaders.append("Content-Type", "image/jpeg");
myHeaders.get("Content-Type"); // Returns 'image/jpeg'
```

You can then delete it again:

```js
myHeaders.delete("Content-Type");
myHeaders.get("Content-Type"); // Returns null, as it has been deleted
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [ServiceWorker API](/en-US/docs/Web/API/Service_Worker_API)
- [HTTP access control (CORS)](/en-US/docs/Web/HTTP/Guides/CORS)
- [HTTP](/en-US/docs/Web/HTTP)
