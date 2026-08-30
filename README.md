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
- **CTA** — always `https://founders.thrivingera.com`

Keep wide content (tables, code blocks) inside an `overflow-x: auto` wrapper so the page body
never scrolls sideways on a phone.
