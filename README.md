# Postman Pagination Handler — PokéAPI

[![Run in Postman](https://run.pstmn.io/button.svg)](https://god.gw.postman.com/run-collection/your-collection-id-here)

A Postman collection that automatically pages through a paginated API, using `pm.execution.setNextRequest()` to chain requests until the data runs out.

📄 [View live documentation](your-published-url-here)

## What it does

- Sends an initial request and pulls the pagination cursor (`next`) straight out of the JSON response body
- Chains into a second request that re-runs itself, advancing to the next page each time
- Logs each page's results to the Postman Console as it runs
- Includes a hard iteration cap so it can't loop forever against a live API

## Requests

| Request | Purpose |
|---|---|
| `Start Pagination (Pokemon)` | Kicks off the run, grabs page 1, extracts the `next` URL |
| `Fetch Page (Pokemon)` | Re-runs itself against each subsequent page until `next` is null or the safety limit is hit |

## How to use it

1. Click **Run in Postman** above, or import `pokemon-pagination.postman_collection.json` manually
2. No environment setup or auth needed — PokéAPI is open
3. Open the Postman Console (`View → Show Postman Console`) to watch it run
4. Right-click the collection → **Run collection** → run `Start Pagination (Pokemon)`

## Key logic

```javascript
if (data.next && count < 5) {
  pm.environment.set("next_url", data.next);
  pm.execution.setNextRequest("Fetch Page (Pokemon)");
} else {
  pm.execution.setNextRequest(null);
}
```

Adjust the iteration cap or the `limit` query param on the first request to page through more or less data per run.

---

**Built with:** [Postman](https://www.postman.com/) · [PokéAPI](https://pokeapi.co/)
