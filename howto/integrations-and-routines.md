# Integrations and routines

## MCP integrations

On a configured server, bots can connect reviewed HTTP MCP services (Gmail,
GitHub, HubSpot, X, PagerDuty, ClickUp and others from the catalog). In
**My workspace → Integrations**, choose **OAuth** and **Autoriseren**. That
opens the provider’s consent flow. The server does not connect to the MCP
until you finish that consent. **API token** connects with the token you enter.
Chat shows an **Authorize** card for OAuth. Other bots can reuse that account.
**My workspace → Integrations** controls which sandboxes may use it, and
**Bot access** can narrow that to selected bots, so for example only your
finance bot uses the finance mailbox. A second
named account on the same service uses **Account toevoegen** or
`mcp_add_account`; sandbox grants stay per account.

If one account stays on **Connection error**, open that account and choose
**Reset**. Reset throws away that account’s stored tokens and everything this
server remembers about the connection. The account disappears, and **Add account**
can create it again. Other accounts of the same integration stay. Your data at
the provider stays too. **Unlink** only removes the tokens and keeps the account
so you can connect it again.

The catalog is not a claim that every provider completed live acceptance on your
host. Local stdio packages and arbitrary API-key headers are not supported.
**Also search the MCP Registry** only shows servers that publish a remote HTTP
endpoint you can connect here; local-only packages stay out of the list.

Demo mode has no live MCP.

## Standard mailboxes

**My workspace → Mailboxes** connects a normal mailbox with IMAP and, when you
want to send, SMTP. The password stays on this server and is not shown in chat.
Bots you allow can read, search, move messages, save drafts, send, and use
signatures you saved there, including small inline images. This is separate from
the Gmail entry in the MCP catalog.

Presets fill Gmail (an app password), Outlook / Microsoft 365, iCloud and
Fastmail. A custom server uses the host and port you enter. The connection is
TLS or STARTTLS. A checkbox allows a self-signed certificate only for an
internal server whose certificate you trust.

**Sandbox access** and **Bot access** work like integrations: every sandbox or
selected ones, every bot or selected bots.

Sending, moving a message and deleting a signature ask first unless you add an
**Allow** rule for that action. The service name is **IMAP**. Reading and
searching continue unless a rule names that action.

The Mailboxes screen is available in the demo. A saved mailbox contacts the
host you type, so the published demo does not include a live mailbox.

![Mailboxes in My workspace](images/mailboxes-desktop.png)

*Demo capture: the empty Mailboxes screen. Demo has no live mailbox.*

![A Gmail preset on the mailbox form](images/mailboxes-form-desktop.png)

*Demo capture: choosing Gmail fills the IMAP host. Nothing was saved, and no
password was entered.*

![Mailboxes on a phone](images/mailboxes-mobile.png)

*Demo capture on a phone-sized screen. Demo has no live mailbox.*

## Action rules and approvals

**My workspace → Action rules** decides what bots may do in your connected
services and on their computer. Each rule names a service (or any service), an
optional account, an action by its tool name (or every writing action) and a
decision: **Allow**, **Ask first** or **Block**. Leave the account on **All
accounts** and the rule covers every account of that service, which is how
rules you already saved behave. Pick one label and the rule applies only to
that account. A rule that names an account wins over the same service and
action with no account. The labels are the accounts you connected. Renaming an account keeps its rules
on the new name. If that name already has a rule for the same action, the
rename is refused and the old name stays. A name that differs only by case is
the same account. A label you later remove stays listed as account removed and
no longer matches. Rules apply to all your bots, routines included.

When one bot may use several accounts of the same service, **Edit agent** and
that service under **Integrations** show which account it uses by default.
Until you choose, that is the first account the bot is allowed to use.

Use the service name **Computer** for desktop actions such as
`computer_terminal`, `computer_click` or `computer_type`. Use **IMAP** for a
standard mailbox. Without a rule of your
own, a bot asks first for MCP actions the service itself marks as destructive,
such as deleting, and for sending, moving or deleting a signature on a mailbox.
Other actions, including computer tools, keep working as
before. Looking things up and screenshots are only interrupted by a rule that
names that action.

![Action rules in My workspace](images/action-rules-desktop.png)

*Demo capture: example rules for Gmail, HubSpot and Computer. Demo has no live
MCP or desktop, so no rule is applied to a real service here. The account
field and the default-account control were added after this capture; a
replacement screenshot is still open.*

When a rule asks first, chat shows the action with the service, account and
exactly what will be sent. **Approve and run** sends exactly that; the bot
cannot change it afterwards. **Don't run** stops it, and the bot may not try
the same thing another way. A blocked action is never sent.

A routine that wants to change a bot's memory, name or task shows the same
kind of card, with the old text and the new text. Nothing is saved until you
approve. A helper task from another bot cannot change those. Appearance, such
as the icon, still updates immediately. Who may ask a bot for help, and which
colleagues that bot may ask, stay in **Edit agent**. A bot cannot change them.

With a workspace decision model set, the card also shows its advice: whether
the action seems to match what you asked, whether it shares something with
others and whether it is hard to undo. The advice never decides for you.

![Action rules on a phone](images/action-rules-mobile.png)

*Demo capture on a phone-sized screen. The presets, the new-workspace switch and the account field were added after this capture; a replacement screenshot is still open.*

Two presets sit above the rule list. **Ask before terminal commands** asks in every run. **Ask for every computer action in routines and handed-off tasks** asks only in routines and tasks one bot hands to another. Each preset is an ordinary rule. It shows **On** while that rule exists, and choosing it again offers **Remove**. You can change or delete it like any other rule. A removed preset does not come back.

A rule can apply **everywhere**, or only to **routines and handed-off tasks**. In those runs, that narrower rule outweighs a general Allow or Ask. An everywhere Block still wins over that narrower Allow or Ask. A chat with you stays a normal attended chat.

Printing always asks unless you add an **Allow** rule for Print. Other computer actions stay allowed until a rule says otherwise. Screenshots are only interrupted by a rule that names that action.

On a computer card, **Approve** runs that one action. **Approve for the rest of this task** lets the same computer action run again in this task without another card. It is not offered for printing or for filling a saved sign-in. It does not cover a different action, a later task, or a rule that blocks the action. **Don't run** stops it.

A new installation starts with the routines-and-handed-off preset on for workspaces that have not been used yet. An installation that already had bots keeps its current rules. An administrator can change what **new** workspaces start with under the same page. That switch does not edit workspaces that already have rules.

## Sensitive numbers

Kobozo holds an outgoing action when the text contains a card number, an IBAN or a national ID number (Belgium or the Netherlands, unless an administrator chooses otherwise). The approval card shows a badge, the number masked, and a reminder to check the recipient. **Approve and run** sends the original text. **Show the numbers** reveals it while the card is still waiting, with the same sign-in check as approval. After you approve, decline, or the card closes, the stored copy is masked and Show is gone.

This is on for every workspace, including one that was upgraded. A personal Allow rule cannot turn it off. An IBAN in a mail action can skip the hold when an Allow rule names that exact IMAP tool and you already approved an IBAN to that same recipient from this card. An MCP call or a computer action that contains an IBAN is still held. A card number or a national ID is still held. **Approve for the rest of this task** does not skip a later action that contains one of these numbers.

An administrator changes categories, countries and the Allow exception under **Organization settings → Security → Sensitive numbers**. On **Action rules** you can see whether the check is on. You cannot switch it off there. If the installation country is not Belgium or the Netherlands, no national-ID country is selected until an administrator chooses one.

The check does not see a number that is only inside an image or a PDF, a number written as words, or a number split across fields. Digits joined by a single space count as one number, so a card or ID is not picked out of a longer run of digits. A Belgian national number is also recognised when it is grouped, for example `85 07 30 033 28` or `850730 033 28`. A leading `+` hides a short phone number, and it does not hide a card number or that Belgian number. A flight or order code in the same sentence does not hide the number that follows. A desktop file is not opened just because the action names its path.

*A screenshot of the masked approval card and the Sensitive numbers setting is still open. The captures above predate this check.*

## Routines

A routine starts **on a schedule** or **on a webhook event**. Webhook routines stay hidden until an administrator turns on **Inbound webhooks** under **Organization settings → Project environment**. The switch is off on a new installation. The public base URL is shown there. When `KOBOZO_HOOKS_ORIGIN` is set, that address is shown and cannot be edited. Only `/api/hooks/i/` has to be reachable; a sender on your network does not need the server exposed to the internet.

![New routine with webhook start disabled](images/webhook-routine-off.png)

*Demo capture: On a webhook event stays disabled until an administrator enables inbound webhooks.*

Ask a bot to repeat work, or open the discreet **Routines** control beside
**Computer**. The server runs due work even when every client is closed. Results
appear in the same chat. You can pause, resume, edit, remove or run once. On a
new bot that still has no task, that routine instruction becomes the task shown
in **Edit agent**. A task you already saved is left unchanged.

If an administrator disables your account, routines that were switched on are
paused and stay paused after the account is turned back on. The card says they
were paused when the account was disabled, with the date. **Resume** starts
that routine from the next time from now. It does not run the occurrences that
were missed. A delivery that was still waiting is dropped and is not sent when
the routine resumes. Resuming a writable webhook still requires a signing secret.
**All routines** can resume every paused item for your account.

A webhook routine is read-only until you clear **Read only**. A routine that is not read-only must require a signature; the server refuses the delivery until you turn that on. A read-only routine can stay token-only. The editor and the routine card then say: “Without a signature, anyone with this address can start the routine.”

After you save it, the address is shown once, with **Copy**. Later it is masked. **Rotate address** issues a new one and the old address stops working. **Require signature** shows a signing secret once. Send `X-Kobozo-Signature: sha256=<hex>` or `X-Hub-Signature-256` over the raw body bytes. If you also send `X-Kobozo-Timestamp`, it must be within five minutes and the signed bytes are `timestamp`, a dot, then the body. **Require a timestamp** rejects a signature that omits that header. The event is data for the routine, not a new instruction. **Send test event** queues one delivery without those HTTP checks. Recent deliveries list time, status, dedup key and size. The card shows how many webhook runs this routine has used today, out of the daily limit. An administrator sets that limit under **Inbound webhooks**; a new installation starts at 50 per routine per UTC day. Past the limit the address answers 429 until the next UTC day. A manual **Run now** does not count toward it. Three failed runs pause the routine and say so on the card. **Resume** turns it back on. A refused delivery is not a failed run.

A model account that has reached its limit is not one of those three failures. The card says **Waiting for model limit**, with **Resume** and a link to **My workspace → Model keys**. Resume does not run the occurrences that were missed, and it does not start a run by itself. A short Retry-After, up to one minute, is waited once. The chat then names the account. That wait is skipped once a tool in the same reply has already run, so a send or a write is not repeated. When the provider sends a reset time in a standard header, and that time is still ahead, the message includes the time it should be available again.

Set `KOBOZO_TRUST_PROXY` to a hop count, such as `1`, or to a comma-separated list of trusted proxy addresses such as `10.0.0.0/8,127.0.0.1`. The value `true` is not accepted, because it would trust every address in `X-Forwarded-For`. Use a hop count only when this process can be reached through that proxy alone. Left unset, every sender behind one proxy shares that proxy’s per-minute bucket, and the server stops tracking new addresses once it already remembers 2000. Those per-minute limits stay in memory on this version. The daily count is kept even after older deliveries scroll off the list, so a limit above 100 still stops the routine for the rest of the UTC day.

![Inbound webhooks with the daily limit](images/webhook-daily-cap.png)

*Installation capture: Inbound webhooks is on, the public base URL is set, and Daily limit per routine is 50.*

![Webhook routine editor with the token-only warning](images/webhook-routine-editor.png)

*Demo capture: On a webhook event is selected, Read only is checked, and the editor says that anyone with this address can start the routine.*

![Webhook tools with Require a timestamp checked](images/webhook-routine-delivery.png)

*Demo capture: Require a timestamp is on, and a test delivery is listed as dispatched. The address itself is masked after the first view.*

![Webhook routine tools on a phone](images/webhook-routine-mobile.png)

*Demo capture, phone width: Require a timestamp stays checked beside the dispatched test delivery.*

**All routines** on the bot list, or **My workspace → Routines**, shows every
routine you own: the bot, the same wording as that bot’s panel, the timezone,
the next run and whether it is active or paused. Pause, resume, run once and
remove from that list use the same checks as the bot’s own panel. Create or
edit a schedule from the per-bot panel. The overview also shows how close the
server is to its 50 pending or active runs.

![All routines in My workspace](images/routines-overview.png)

*Demo capture: routines from Chief and Schrijver, with queue depth and the
same pause / run-now / remove actions as each bot’s own panel. Demo has no
live models.*

You can also ask one bot to set up a repeating job on another bot you own.
The schedule then belongs to that specialist: it uses that bot’s model,
memory, project and connected accounts. Chat and **Routines** show which
teammate created it.

A scheduled run can pause itself when the work is done — for example once a
reply has arrived. Changing its own instructions shows a before/after card
first. **Approve change** saves the new text for the next run. **Don't apply**
leaves the old text. This run keeps going either way. An instruction that is
already stored does not ask. It cannot create another routine, including on a
colleague, or change a different one. An approved text or a pause appears in
the Routines panel, and the change is recorded in **Details**.

Routines use the bot’s current model and permissions. They do not invent extra
account access.

### Fewer notifications for routine results

With a workspace decision model (**My workspace → Models → Default model**), a
routine result that clearly holds nothing new, such as "no new invoices" or
"everything is as expected", does not send a notification. The result still
appears in the chat, and **Details** shows **Routine notification skipped:
nothing that needs your attention**. Anything that reports a change, a problem,
a deadline or a question still notifies you, and so does a failed run. When in
doubt, you get the notification. See [decision models](decision-models.md).

![Routine result in the chat with the skipped notification in Details](images/routine-quiet.png)

*Lab capture: a local test install with a stand-in chat model and a stand-in
LAYA decision model. The routine reported no new invoices, so **Activity** shows
that the notification was skipped.*

### Read-only routines

Tick **Read only** when a routine should only follow something up: check a
mailbox, watch a project or look for changes. The bot can look things up, but
cannot send, change, delete or use its computer. It ends each run with what it
found and concrete proposals, which you can then ask it to carry out in chat.
The routine card and **All routines** show **Read only**.

![Routine editor with the Read only option](images/routine-read-only.png)

*Demo capture: a new routine with **Read only** ticked. Demo has no live
models, so the run itself is not shown.*

## Telegram

Link one Telegram bot to one Kobozo bot. Open the bot, choose **Edit agent**, and use **Telegram**. Paste the token from BotFather and choose **Link**. The token is stored encrypted and is not shown again.

![Edit agent with Telegram linked and receiving](images/telegram-bot-editor.png)

*Demo capture: Chief linked to a stand-in Telegram bot. The token is not shown. Demo has no live Telegram.*

![The same Telegram section on a phone](images/telegram-bot-editor-mobile.png)

Nobody can message the bot until you create a pairing code. The code lasts 10 minutes and works once. Open it in Telegram and send `/start` with that code.

![A one-time pairing code in the bot editor](images/telegram-bot-pairing.png)

*Demo capture: the code is shown once. It is not the bot token.*

You can pair more than one of your own Telegram accounts. Anyone else gets a single “This bot is private.” and no task is stored. Group chats are ignored. Photos and other files get “Text only for now.”

A message you send there starts a normal task on this bot’s saved model. The answer comes back in Telegram. The same message appears in the Kobozo chat with **via Telegram**. **Activity** lists the task as **Telegram**. A task you start in the app or from a routine is not copied to Telegram.

`/stop` cancels the task that this Telegram chat started. `/help` lists what the channel can do. A single-choice question shows one button per answer. Anything that needs approval, sign-in, or a settings change says the bot needs you. **Open in Kobozo** opens that bot in the app. There is no approve button in Telegram. Account changes from a Telegram task are refused.

**Remove Telegram** stops new messages. The conversation in Kobozo stays.

Disabling the account also pauses a Telegram link that was receiving. It does
not come back when the account is turned on. An administrator resumes it from
**Users**, or you turn **Telegram-berichten ontvangen** back on. The panel
shows the date the account was disabled.

Under **Organization settings → Project environment → Channels**, an administrator sets the Telegram API address, the app address used in those links, and the daily limit for new Telegram tasks (200 per UTC day unless you change it). A local-network app address is allowed. **Local-only bots may use Telegram** is off. Turning it on tells you that messages pass through Telegram’s servers even when the model stays local.

**Telegram tasks may change the bot's memory, mission or routines directly** has two choices. **Ask for approval on the approval card** is the recommended default: memory, mission, a new bot, a Teach guide, a new routine, and a change to a routine's instructions, write access, schedule, start or time zone wait for you on the same approval card a routine uses. The new-bot card names the scope, the model that will be saved, and who that bot may ask for help. It does not accept a hidden bot, a chosen icon or colour, or an image, speech or decision model; Telegram refuses those. The routine card names the schedule or webhook trigger, says when the routine can write, names a time-zone change, and says when the prompt will also become the bot's task. Renaming a routine still happens immediately. Moving a bot to another project, hiding it, changing its icon or colour, or changing its image, speech or decision model is refused in Telegram until you allow changes in the chat. Changing appearance or visibility is not offered there; the bot is told to do that in the Kobozo app. A Telegram task does not save a distilled memory note on its own. Pausing a routine still happens immediately. **Allow the change in the chat** applies them immediately, including that memory note, a new bot's hidden flag, icon, colour and image, speech or decision model, and a routine time-zone change. Appearance and visibility are offered again in that mode. Account changes from Telegram stay in the Kobozo app either way. Switching Telegram off, or removing it, stops tasks that chat already started.

![Channels under Project environment](images/telegram-channels-settings.png)

*Lab capture: an administrator’s Project environment. The daily limit is 200. Approval on the card is selected.*

![The same approval choice on a phone](images/telegram-channels-mobile.png)

When a public HTTPS address is set for inbound webhooks, Telegram delivers to that same `/api/hooks/i/` path. Otherwise the server fetches updates itself. Telegram keeps working when inbound webhooks are switched off. The channel does not look at that switch. Behind a reverse proxy, set `KOBOZO_TRUST_PROXY` so Telegram does not share one per-minute bucket with every other sender. In BotFather, turn groups off. Run one server process: a second process would fight the same Telegram connection.

The bot token, webhook secret and hook address are not shown in the app after linking, and they are not written to the channel’s error line.
