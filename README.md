# lead-magnets

Lead magnet landing pages for Thriving Era Studio.

| Path | Magnet |
|------|--------|
| `aistack/` | The Conscious Founder AI Stack — ten tools, what they cost, what each one is for |
| `5prompts/` | 5 Claude Prompts That Don't Sound Like Everyone Else's |
| `whatsapp/` | Automate Your WhatsApp With Claude — three setup paths, five prompts, and the honest limits of each. **Email-gated.** |

Each is a single self-contained `index.html`. No build step, no dependencies beyond the Google
Fonts link. Drop the folder anywhere static.

## House style

Shared across all three, so a new magnet should match rather than invent:

- **Type** — Anton for headings (uppercase, tight tracking), Courier Prime for body
- **Colour** — cream `#FDF8F4`, ink `#1A1A1A`, magenta `#C2185B`, rose `#B76E79`, highlight `#E91E73`
- **Rhythm** — dark hero, alternating cream and `#F5F0EC` sections, gradient CTA, dark footer
- **CTA** — `founders.thrivingera.com/masterclass` primary, with Conscious Founder OS
  (`founders.thrivingera.com`) and the Calendly exploratory call as secondary links

Keep wide content (tables, code blocks) inside an `overflow-x: auto` wrapper so the page body
never scrolls sideways on a phone.

## Email capture

`whatsapp/` posts to the standard pipeline, same as every form on
founders.thrivingera.com:

```
POST https://cfos-webhooks.vercel.app/api/lead-magnet
{ name, email, magnet, source_keyword }
```

That endpoint writes `site_leads`, adds the subscriber to a MailerLite group and the
master nurture list, sends the delivery email, and notifies Rocha. Extra fields ride
along into `site_leads.raw` — that is how the WhatsApp opt-in is stored without the
endpoint needing to know about it.

**A new magnet needs a registry entry first.** `MAGNETS` in `cfos-webhooks`
(`api/lead-magnet.js`) gates the slug; an unknown one returns 400 "Unknown lead
magnet" and the signup is lost. Add the entry, deploy cfos-webhooks, then ship the
page. The MailerLite group is created on first signup, so there is no other setup.

**No Supabase key goes in a magnet.** These pages are public, so anything embedded is
readable by anyone, and an anon key is only as safe as the RLS on every table in the
project. All writes happen server-side.

The gate is soft by design. Gated sections are in the DOM and hidden, so a determined
reader can view source — true of any static gate. The trade is that the free half
stays linkable and shareable, which is what makes a magnet spread. If the endpoint is
down the guide reveals anyway: losing a subscriber costs less than a reader who gave
you their address and got nothing.

The delivery email links back with `?unlocked=1`, which skips the gate — otherwise
someone opening that email on a second device is asked for an address they have
already given.

