# CourtSync — every channel, one board

Standalone channel manager for sports venues: court bookings from Playo,
Hudle, District, the venue's own website and the front desk all live on
ONE availability board. A slot blocked on any channel is blocked on all
of them — the hotel-industry channel-manager model, for courts.

Sold independently of the Academy Manager SaaS: a venue that never buys
the full academy app can run just this board.

- **Ledger**: the multi-tenant platform database (schema in the Leo repo,
  `supabase/schema.sql`). All writes go through server-side RPCs —
  prices computed in Postgres, courts claimed atomically, staff-only
  guards enforced by row-level security.
- **Multi-venue**: `?venue=<tenant_id>` — the board reads the venue's
  courts/rates from its tenant config; sign-in must belong to that venue.
- **Marketplace sync**: manual entry today; Playo/Hudle/District partner
  APIs plug into the same ledger when granted.
- **Stack**: vanilla HTML/CSS/JS, no build step. Deploy = push to main.
