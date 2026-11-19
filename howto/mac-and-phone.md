# Mac and phone

## Phone web app

Open the orchestrator’s **HTTPS** address on your phone. On a narrow screen you
see the bot list first. Opening a bot keeps an unsent draft if you go back.

![Mobile bot list with install-app notice](images/chat-mobile.png)

*Demo capture: phone-width bot list, marketplace, add-bot and the install-app
notice.*

The search field on this list opens the same palette as **Ctrl+K** on a wide
window: bots, hidden specialists, messages and routines.

**Install app** appears on sign-in and on the list. Supporting browsers offer a
button; on iPhone use Safari **Share → Add to Home Screen**. The installed app
keeps this server. Chatting still needs a connection; the bot keeps working if
you leave.

## Mac app

The Mac app requests microphone permission when you record a voice message.
Its permission prompt explains that the recording is sent to your bots.

Download the universal ZIP from the same preview release (macOS 13+, Intel and
Apple Silicon). This preview is not Apple-notarized; macOS may ask for extra
permission to open it. Once your server offers the download, later server
updates keep it available until a newer Mac build replaces it.

**My workspace → Desktop app** copies the server URL. Sign in with the same
account. Closing the window does not stop the server. Personal settings stay
in the Mac app. **Organization settings** opens this server in the system
browser.

**My workspace → Computers** (Mac app only) can enable passkeys and security
keys for bot browsers. That setting is off by default and is separate from
**My account → Passkeys**. Forwarding those ceremonies is not finished yet;
use **Take over** on the Computer window when a site asks for MFA.

```text
kobozo-bot://connect?server=https%3A%2F%2Fyour-server
```

That link carries only the origin, never a password or session.
