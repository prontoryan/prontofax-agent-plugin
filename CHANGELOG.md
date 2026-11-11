# Changelog

## Unreleased (11-11-2026)

- README: Cursor install by hand in `~/.cursor/mcp.json`, verified against cursor.com/docs/mcp, with a pointer to the one-click button on prontofax.com. Cursor documents no https install link, so the README carries the config block rather than a button. Docs only, no change to the plugin itself.

## 1.0.0 (10-13-2026)

- First release.
- Connects to the hosted ProntoFax MCP server at https://mcp.prontofax.com/mcp, with the tools `lookup_fax_number` and `send_fax`.
- Skill `send-a-fax`: gather the pages, confirm the destination, ask about a cover page, and hand the user a link to finish and pay on prontofax.com.
- Skill `find-a-fax-number`: look up a verified fax number for a US government office, with its source and verified date.
