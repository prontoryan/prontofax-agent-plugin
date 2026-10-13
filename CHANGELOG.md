# Changelog

## 1.0.0 (10-13-2026)

- First release.
- Connects to the hosted ProntoFax MCP server at https://mcp.prontofax.com/mcp, with the tools `lookup_fax_number` and `send_fax`.
- Skill `send-a-fax`: gather the pages, confirm the destination, ask about a cover page, and hand the user a link to finish and pay on prontofax.com.
- Skill `find-a-fax-number`: look up a verified fax number for a US government office, with its source and verified date.
