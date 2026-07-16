# Postman Pagination — PokéAPI

A Postman collection that automatically pages through a paginated API, using `pm.execution.setNextRequest()` to chain requests until the data runs out.

📄 [View live documentation](https://documenter.getpostman.com/view/54488922/2sBY4Mv254)

## What it does

- Sends an initial request and pulls the pagination URL (`next`) straight out of the JSON response body
- Chains into a second request that re-runs itself, advancing to the next page automatically
- Logs each page's results to Console as it runs
- Includes a hard stop so it can't loop forever against a live API

## Requests

| Request | Purpose |
|---|---|
| `Start Request` | Kicks off the run, grabs page 1, extracts the `next` URL |
| `Fetch Next URL Request` | Re-runs itself against each subsequent page until `next` is null or the safety limit is hit |

## How to use it

1. Click **View live documentation** above, or import `Pagination Exercise PokéAPI` manually
2. No environment setup or auth needed, PokéAPI is an open API, which is why I chose it 
3. Open the Postman Console (`View → Show Postman Console`) to watch it run
4. Right-click the collection → **Run collection**

---

**Built with:** [Postman](https://www.postman.com/) · [PokéAPI](https://pokeapi.co/) · [Claude](https://claude.ai/)
