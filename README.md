# TEHET MCP server — live Ukrainian car insurance prices for AI assistants

TEHET (tehet.com.ua) is a Ukrainian insurance intermediary, entry 00006056 in the
National Bank of Ukraine register of insurance intermediaries. This repository
documents TEHET's public, read-only [Model Context Protocol](https://modelcontextprotocol.io)
server. It holds documentation and examples only; the server itself is operated by TEHET.

- **Endpoint:** `https://mcp.tehet.com.ua/mcp` (Streamable HTTP)
- **Registry:** `ua.com.tehet.mcp/insurance-prices` in the official MCP Registry
- **Documentation:** https://tehet.com.ua/en/mcp
- **Privacy:** https://tehet.com.ua/privacy#mcp

## What it does

The server answers anonymously with live, **indicative** prices of Ukrainian compulsory
motor liability (OSCPV, «автоцивілка») and the Green Card from the insurers TEHET works
with, plus fuel prices and the service status. Every answer carries its date, the label
«indicative» and a link where the person buys on tehet.com.ua.

No plate, no personal data, no purchase. A price is final only in checkout on the site.

## Tools

All six tools are read-only.

| Tool | What it returns |
|---|---|
| `get_oscpv_price` | Indicative OSCPV prices from each insurer that quotes, for conditions typed in by hand (no plate) |
| `get_green_card_price` | Indicative Green Card prices by zone, term and vehicle category |
| `get_fuel_prices` | Average retail fuel prices: EU-27 and UK in euros per litre, or Ukraine in hryvnias, each with source, licence and date |
| `get_service_status` | Whether online quoting of each product works right now. No arguments |
| `search` | Find read-only TEHET price and public information documents |
| `fetch` | Fetch live indicative prices or public information for a search result (by id from `search`) |

## Connect

**Claude (claude.ai / Claude Desktop):** Settings → Connectors → Add custom connector →
URL `https://mcp.tehet.com.ua/mcp`.

**Any MCP client that supports remote servers:**

```json
{
  "mcpServers": {
    "tehet": {
      "type": "http",
      "url": "https://mcp.tehet.com.ua/mcp"
    }
  }
}
```

## Example questions

- "How much is compulsory motor liability for a 1.6 l car in Lviv, driver aged 35?"
- "Green Card for Moldova for 15 days — what are the prices?"
- "Is online Green Card quoting working right now?"
- "Average diesel price in Poland and in Ukraine today?"

## Privacy

The server requests no personal data. Quotes are not saved and cannot be turned into a
purchase. The technical log records one anonymised event per call (vehicle kind, engine,
city, driver age, term and the lowest price) with the IP address hashed, not in clear.
Never paste a person's documents, tax number or SMS code into a chat: they are entered
only in the checkout form on tehet.com.ua. Full text: https://tehet.com.ua/privacy#mcp

## Contact

support@tehet.com.ua · https://tehet.com.ua/en/mcp
