# Order-to-Cash Revenue Leakage Monitor (SAP)

The app of the **Order-to-Cash Revenue Leakage Monitor (SAP)** template in the Kaman marketplace, built the way
every app on Kaman is (the reference is the Smart Site Planning desk;
Kai's *Building an app on Kaman* skill teaches it).

Finds revenue that leaks between order and cash in SAP S/4HANA: matches every delivery to its order and invoice in code (not by guesswork), flags unbilled deliveries, under-billing and unexplained credits, explains the root causes, and once finance agrees raises debit memo requests on billing block for the billing team to release. Set your materiality threshold and your SAP codes at install.

It is installed as a code project of yours when you install the template.

## What it does

| screen | what it is |
|---|---|
| `/login`, `/signup` | the app's **own** sign-in — its users never see Kaman |
| `/` — the desk | a Kaman **scenario**: the live records from your connected system, read as you, with **Ask** on each |
| `/chat` | Kaman's chat component with the template's agent, as you |
| the header's **Run** | an **action** the desk declares: starts the template's workflow, approvals included |

## How it is wired

- The app **acts as its signed-in user**: every call carries their token
  (`auth.session`), so Kaman applies their permissions and organisation.
  The API key is used only to sign a new person up.
- Kaman's browser components reach Kaman through `app/api/kaman/[...path]`
  (`auth.proxy`), narrowed to the scenario routes. The browser never holds
  a token.
- `kaman.app.json` names the agents, workflow and desk scenario by the ids
  the template seeds them under. **Install rewrites them** to your copies
  and shares exactly those with your organisation.

## Publishing a new version

Push here, then republish the template pinned to the new commit. Installs
always take the pinned commit, never the tip of `main`.
