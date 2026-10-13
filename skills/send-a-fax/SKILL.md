---
name: send-a-fax
description: Send a fax to a US fax number with ProntoFax, from photos or a PDF, for $2.99 flat and charged only when delivery is confirmed. Use when the user wants to fax a document, a form, a letter or a signed page to a government office, a court, a doctor, an insurer or any other US fax number.
---

# Send a fax

ProntoFax sends one fax to one US fax number. It costs $2.99 flat for up to 25 pages including the cover page, with no account and no subscription. The card is held when the user pays and charged only when delivery is confirmed. A fax that fails is not charged.

This plugin connects to the ProntoFax server, which has two tools: `lookup_fax_number` and `send_fax`. Your part is to gather what the send needs and hand the user a link. The user adds the pages and pays on prontofax.com. You never fill in the checkout, and you never enter card details.

## Steps

### 1. Ask about the pages

Ask what the user wants to fax. The pages can be photos taken with a phone or a PDF. A fax holds up to 25 pages including the cover page, so a document with a cover can have at most 24 pages of its own.

A file attached to this conversation cannot be passed to `send_fax`. The user adds the pages on the ProntoFax page the link opens. If they already attached the document here, say so plainly and tell them they will add it on that page instead of uploading it again here.

If the document runs past that, tell the user before going further. ProntoFax does not split a long document, so they will need to send it as more than one fax.

### 2. Get the destination fax number

The number must come from one of two places:

- **The user or their document.** If the user typed a number, or attached a letter or form that prints one, use that number. Read it back to them and ask them to confirm it.
- **`lookup_fax_number`.** If the user names an agency or office instead of a number, call `lookup_fax_number` with the agency in their own words, plus a state or city when they gave one. Show the result as it came back: the number, the official source it was read from, and the date it was last verified. Ask the user to confirm it is the office they mean. If several offices come back, ask which one.

Never guess a fax number. Never take one from memory, from your training data or from a web search. If the lookup returns no verified number, tell the user that, and ask them for the number printed on their letter or on the agency's own website. The `find-a-fax-number` skill covers lookups in more detail.

ProntoFax sends only to US fax numbers.

### 3. Ask about a cover page

Ask whether they want a cover page. It is optional and they add it on the same page as the rest of the fax. When the fax goes to a government office, a cover page with the sender's name and a case or claim number helps the office match it to the right file.

### 4. Call send_fax

Call `send_fax` with:

- `fax_number`: the confirmed destination, in any format.
- `agency`: the agency name, when the number came from a lookup or the user named one. Optional.
- `language`: `es` when the user is writing in Spanish, otherwise leave it out.

If the tool says the number is incomplete or outside the US, pass that on and ask the user for the full ten digit US number.

### 5. Hand the user the link

`send_fax` returns a link to prontofax.com with the number already filled in. Give the user that link exactly as returned and tell them:

- They add the pages there, from a photo or a PDF, and the cover page if they want one, up to 25 pages including the cover page.
- They pay $2.99 on that page. Nothing is sent and nothing is charged until they finish there.
- The card is held, not charged, and is charged only when delivery is confirmed.
- An email confirms delivery with the time it was delivered and the page count.
- If the fax cannot be delivered, an email explains why, and they are not charged.

Do not describe a form inside this conversation. On this host the send happens on the ProntoFax page the link opens.

## What ProntoFax does not do

- It sends faxes only. It cannot receive a fax, so a reply from the office has to come back some other way, such as mail, phone or the office's own portal.
- It has no status lookup in the conversation. The delivery or failure email is the record.
- It sends only to US numbers.

## Example

User: I need to fax my signed form to the Texas Workforce Commission.

1. Ask whether the form is a photo or a PDF, and how many pages.
2. Call `lookup_fax_number` with agency "Texas Workforce Commission". Show the number, its source and its verified date, and ask the user to confirm it.
3. Ask whether they want a cover page with their name and claim number.
4. Call `send_fax` with the confirmed number and agency "Texas Workforce Commission".
5. Give them the link and explain that they add the pages and pay $2.99 there, that nothing is sent until they do, and that the confirmation arrives by email.
