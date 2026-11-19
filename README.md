# ProntoFax agent plugin

Send a fax from your agent. Pay $2.99 on delivery, no account.

This plugin connects Claude, Cursor and Grok Bot to [ProntoFax](https://www.prontofax.com), a pay per fax service for US fax numbers. It adds the hosted ProntoFax MCP server and two skills that teach the agent the fax workflow.

- **Find a fax number.** The agent looks up the verified fax number for a US government office, such as a Social Security field office, a state unemployment or Medicaid agency, MassHealth, California EDD or FEMA. Each result shows the official source and the date it was last verified. When there is no verified number, the agent says so instead of guessing.
- **Send a fax.** The agent confirms the destination, asks about a cover page and gives you a link to prontofax.com with the number filled in. You add the pages there, from a photo or a PDF, up to 25 pages including the cover page, and pay $2.99. Your card is held and charged only when delivery is confirmed. Nothing is sent or charged until you finish on that page.

ProntoFax sends faxes only. It does not receive them.

## What is in this repository

```
plugin.json                        Agent Plugins 1.0.0 manifest
.claude-plugin/plugin.json         Claude plugin manifest
mcp.json                           The hosted MCP server
skills/send-a-fax/SKILL.md         The send workflow
skills/find-a-fax-number/SKILL.md  Fax number lookups
assets/                            Listing icons
```

The MCP server is hosted at `https://mcp.prontofax.com/mcp`. It needs no sign in and no API key. It has two tools, `lookup_fax_number` and `send_fax`. The plugin sends one fixed header, `X-PF-Client: agent-plugin` from Cursor and Grok Bot or `X-PF-Client: claude-plugin` from Claude, so ProntoFax can count sends that start from this plugin. It carries nothing about you.

## Install

### Claude

Install ProntoFax from the Claude plugin directory. The plugin connects Claude to the ProntoFax server at `mcp.prontofax.com` and adds the two skills. Claude can look up a verified agency fax number and start a send. You upload the document and pay on prontofax.com, and nothing is sent or charged until you pay there.

### Cursor

Add the server by hand: put this in `~/.cursor/mcp.json` (create the file if it does not exist), then restart Cursor. The site also has a one-click Add to Cursor button at https://www.prontofax.com/fax-from-cursor/.

```json
{
  "mcpServers": {
    "prontofax": {
      "url": "https://mcp.prontofax.com/mcp"
    }
  }
}
```

This adds the MCP server only. The two skills come with the plugin install below.

From the marketplace, once listed: open the Cursor Marketplace, search for ProntoFax and install it.

From this repository, as a local plugin:

1. Clone this repository.
2. Copy the folder to `~/.cursor/plugins/local/prontofax`.
3. Restart Cursor, or run **Developer: Reload Window** from the command palette.
4. Ask the agent something like "What is the fax number for the Social Security office in Denver?"

If a marketplace copy of ProntoFax is installed, it takes precedence over the local one.

### Grok Bot

From the marketplace, once listed: the Cursor Marketplace listing also serves Grok Bot.

Until then, add the server by hand. Open grok.com/connectors, or Settings, then Plugins, then **Add Custom MCP**, and enter this URL:

```
https://mcp.prontofax.com/mcp
```

No sign in is needed.

## Privacy and terms

- Privacy: https://www.prontofax.com/privacy/
- Terms: https://www.prontofax.com/terms/
- More about the MCP server: https://www.prontofax.com/mcp/

## Support

Email support@prontofax.com.

## License

The plugin files in this repository are MIT licensed. See [LICENSE](LICENSE). The ProntoFax service is paid per fax.
