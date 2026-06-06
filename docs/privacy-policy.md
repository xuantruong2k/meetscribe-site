# MeetScribe Privacy Policy

**Last updated: June 6, 2026**

MeetScribe ("the app") is a proprietary desktop application for Windows and
macOS that records meetings, transcribes them, and generates summaries. This
policy explains what the app does with your data. The official website is
<https://meetscribe.goldenpaw.org>.

> **The short version:** MeetScribe is **local-first**. Your recordings,
> transcripts, summaries, and settings live on your own computer — we do not
> run any server that receives or stores them. The app has no user accounts
> and collects no analytics or telemetry. The only data that leaves your
> machine is audio (sent to the transcription service you choose) and
> transcript text (sent to the AI service you choose) so the app can do its
> job. You supply your own API keys for those services and connect to them
> directly.

---

## 1. Who is responsible for your data

MeetScribe is published by **Golden Paw**. Because the app stores your content
locally and connects directly to the third-party services *you* configure with
*your own* API keys, you and those service providers are the parties that hold
your meeting data — Golden Paw never receives it.

For privacy questions, contact us at **meetscribe.support@goldenpaw.org** or
visit <https://meetscribe.goldenpaw.org>.

## 2. What the app accesses on your device

| Data | Why | Where it goes |
|---|---|---|
| **Microphone audio** | To capture your voice during a recording | Streamed to your chosen transcription service; mixed audio is processed in memory |
| **System audio (loopback)** | To capture other participants' voices | Same as above |
| **Transcript text** | To produce live and post-meeting summaries | Sent to your chosen AI summary service |
| **API keys** you enter | To authenticate to the transcription and AI services | Stored in the operating system's secure credential store (Windows Credential Manager / macOS Keychain) — never in plain files |
| **Your preferences** | To remember settings between launches | Stored locally on your device |

## 3. Where your data is stored (locally)

All meeting content stays on your computer. Nothing is uploaded to a Golden Paw
server, because there isn't one.

**Windows**
- Recordings metadata, transcripts, summaries, logs: `%LOCALAPPDATA%\MeetScribe\`
- Settings: `%APPDATA%\MeetScribe\settings.json`
- API keys: Windows Credential Manager

**macOS**
- Recordings metadata, transcripts, summaries, logs: `~/Library/Application Support/MeetScribe/`
- Settings: app preferences (UserDefaults)
- API keys: macOS Keychain

## 4. Third-party services your data passes through

To transcribe and summarize a meeting, the app must send data to external
services **over an encrypted (TLS) connection**. You choose which providers to
use and supply your own API keys, so your use of each service is also governed
by **that provider's** privacy policy and terms.

**Transcription (audio is sent to the one you select):**
- Gladia — <https://www.gladia.io>
- AssemblyAI — <https://www.assemblyai.com>

**AI summaries (transcript text is sent to the one you select):**
- Google Gemini — <https://policies.google.com/privacy>
- OpenAI — <https://openai.com/policies/privacy-policy>
- DeepSeek — <https://www.deepseek.com>

The app only contacts the providers you have configured. If you do not enter a
key for a provider, no data is sent to it. We are not responsible for how these
independent providers handle the data you send them — please review their
policies, including any data-retention or model-training terms.

## 5. What we do NOT do

- We do **not** collect analytics, usage statistics, or telemetry.
- We do **not** require an account or sign-in.
- We do **not** sell, rent, or share your data with advertisers.
- We do **not** transmit your recordings, transcripts, or summaries to any
  Golden Paw–operated server (we operate none).

## 6. Updates

The Windows app distributed through the Microsoft Store receives updates through
the Store. Outside the Store, the app checks for updates **only when you ask it
to** in Settings — there is no background update tracking.

## 7. Data retention and deletion

Because all content is stored locally, **you** control retention:
- Delete an individual meeting from within the app.
- Delete the data folders listed in Section 3 to remove everything.
- Uninstalling the app and clearing those folders, plus removing the saved API
  keys from your credential store, removes all locally held data.

Data already sent to a third-party provider is retained according to that
provider's own policy; manage or delete it through your account with them.

## 8. Security

API keys are held only in your operating system's secure credential store, not
in configuration files. All network connections to transcription and AI
services use TLS encryption. Local files are protected by your operating
system's normal user-account permissions.

## 9. Children's privacy

MeetScribe is a productivity tool intended for general business and personal
use and is not directed at children under 13. We do not knowingly collect data
from children.

## 10. Your rights

Since your data resides on your own device and in your own provider accounts,
you can access, export, or delete it directly at any time. If you have
questions about this policy, contact us at the address in Section 1.

## 11. Changes to this policy

We may update this policy as the app evolves. Material changes will be reflected
by updating the "Last updated" date at the top. Continued use of the app after a
change constitutes acceptance of the revised policy.
