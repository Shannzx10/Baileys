### ✨ Features
- 🧠 Intelligent `@lid` and `@jid` mapping
- 📱 Multi-device support
- 🔐 End-to-End Encryption support
- 💬 Handles all WhatsApp message types
- ⚡ Fast and modern TypeScript codebase

### 🚀 Quick Example

```ts
import makeWASocket from '@yupra/baileys'
import { getSenderLid, toJid } from '@yupra/baileys'

const sock = makeWASocket({ printQRInTerminal: true })

sock.ev.on('messages.upsert', ({ messages }) => {
    const msg = messages[0]
    const info = getSenderLid(msg) // logs the sender LID
    const jid = toJid(info.lid)
    console.log('normalized jid:', jid)
})
```

### 🧪 Advanced Usage (Multi-file Auth)

```ts
import makeWASocket, { useMultiFileAuthState } from "@yupra/baileys"

async function start() {
    const { state, saveCreds } = await useMultiFileAuthState("auth_info")
    const sock = makeWASocket({ auth: state, printQRInTerminal: true })

    sock.ev.on("creds.update", saveCreds)
    sock.ev.on("messages.upsert", ({ messages }) => {
        for (const m of messages) {
            console.log(m.key.remoteJid, m.message?.conversation)
        }
    })
}

start()
```
