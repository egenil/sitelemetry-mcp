# Sitelemetry MCP server

<img src="https://sitelemetry.com/favicon.svg" alt="Sitelemetry" width="48" height="48">

Sitelemetry is a hosted, remote MCP server for authorized website audits. Connect it to your AI assistant and ask for a security, technical SEO, AI visibility, analytics and tracking integrations, accessibility or performance audit in plain language. Each tool returns prioritized findings with severity, evidence, impact and a recommended fix.

> This repository contains documentation only. Sitelemetry runs as a hosted service at `https://sitelemetry.com/mcp`; the server source code is not published here.

| | |
|---|---|
| Endpoint | `https://sitelemetry.com/mcp` |
| Transport | Streamable HTTP (remote only) |
| Authorization | OAuth 2.1 with PKCE (browser sign-in, no API key in the client configuration) |
| Tools | 7 audit tools (your client lists the ones the connected account's plan includes) |
| Report languages | English, Turkish, Spanish, German, French, Portuguese, Italian, Japanese, Chinese |
| Registry name | `com.sitelemetry/sitelemetry` |
| Full setup guide | https://sitelemetry.com/mcp-guide |

## Requirements

- A Sitelemetry account. New users can create one from the sign-in step of the connection flow.
- The audits and usage limits available to a connection follow the plan of the connected account. The Free plan covers security audits only, with a limited set of security checks and a monthly allowance. SEO, AI visibility, integrations, accessibility and performance audits, and a six-area full audit, need a paid plan.
- Use Sitelemetry only for websites and infrastructure you own or are explicitly authorized to assess.

## Configuration

### VS Code (GitHub Copilot)

Add the server to `.vscode/mcp.json` in your workspace, or to your user MCP configuration:

```json
{
  "servers": {
    "sitelemetry": {
      "type": "http",
      "url": "https://sitelemetry.com/mcp"
    }
  }
}
```

Start the server from the CodeLens above the entry, from the MCP SERVERS section of the Extensions view, or with the **MCP: List Servers** command. When VS Code asks you to authenticate, complete the Sitelemetry sign-in in your browser (sign in or create an account), then approve access.

### Codex

```bash
codex mcp add sitelemetry --url https://sitelemetry.com/mcp
codex mcp login sitelemetry
```

### Claude Code

```bash
claude mcp add --transport http sitelemetry https://sitelemetry.com/mcp
```

Then open `/mcp` in Claude Code and choose **Authenticate** for Sitelemetry.

### Cursor

Add this entry to `.cursor/mcp.json` in your project, or to `~/.cursor/mcp.json` for all projects:

```json
{
  "mcpServers": {
    "sitelemetry": {
      "url": "https://sitelemetry.com/mcp"
    }
  }
}
```

### Other MCP clients

Add a remote MCP server named `sitelemetry` with the URL `https://sitelemetry.com/mcp`. Select Streamable HTTP and OAuth if your client asks. The client needs to support remote HTTP MCP servers and browser-based OAuth.

ChatGPT and Claude.ai users can connect through the Sitelemetry listing in those apps. See the [setup guide](https://sitelemetry.com/mcp-guide) for details.

### Long audits

Long hosted audits return a job instead of a final result. The client checks that same job until the result is ready, without starting a second scan. If your client has a per-call timeout setting, allowing up to 15 minutes avoids cutting off long audits.

## Tools

| Tool | What it does |
|---|---|
| `audit_security` | Security posture of a website: public checks such as DNS, e-mail authentication records, TLS and HTTP security headers on any target; on a verified host, the protected and active checks your plan includes. |
| `audit_seo` | Technical SEO crawl: crawlability, indexation, titles and meta tags, headings, canonical tags, structured data, broken internal links, redirect chains and AI-crawler policy. |
| `audit_ai_visibility` | How ready a site's content is to be found and cited by AI search and LLM assistants: entity clarity, answerability, source signals, llms.txt and AI-crawler policy. |
| `audit_integrations` | Analytics, tag manager, marketing pixel, site verification and consent setup detected from the site's HTML and headers. |
| `audit_accessibility` | WCAG 2.2-oriented checks of the static HTML: image alternatives, form labels, heading structure, landmarks, contrast signals, language attribute and more. |
| `audit_performance` | Performance and Core Web Vitals through Google PageSpeed Insights: LCP, INP, CLS, FCP, TTFB and the top improvement opportunities. |
| `audit_full` | Every audit area the connected account includes, in one call, with a combined score across the measured areas. |

Every tool takes an explicit target URL and a report language. The dotted names (`audit.security`, `audit.full`, …) are accepted as aliases.

## Usage

Once connected, ask your assistant in plain language, for example:

- "Audit the security of https://your-site.example and rank the most urgent fixes."
- "Check my site's HTTPS, TLS certificate and security headers."
- "Run a technical SEO audit of https://your-site.example and list the top fixes."
- "Run a full audit of https://your-site.example and report in German."

## Safety and scope

- Sitelemetry is not a penetration test. On an unverified target, hosted security audits run public, non-intrusive checks only. On a host you have verified, the default can also run the active checks your plan includes, such as port and injection probes.
- Checks send read-style requests and benign probes that are not meant to change the audited website, but active checks can appear in the site's logs or alerts. Private-network and cloud-metadata targets are blocked.
- Protected security modules and a full six-area audit need the site to be verified in your Sitelemetry workspace (DNS TXT record, HTTP file or Google Search Console). Through the Claude.ai listing, every audit except the public security checks needs current ownership verification for the exact HTTPS target.
- SEO, AI visibility, accessibility and integrations audits read static HTML. Pages are not rendered in a browser, so content added only by JavaScript is not checked.
- Audit results are point-in-time evidence. They do not establish that a site is free of vulnerabilities.
- OAuth clients receive a short-lived, audience-bound access token, not your Sitelemetry password.
- You can revoke a client's access at any time in **My account > Connected MCP applications**.

## Links

- Setup guide: https://sitelemetry.com/mcp-guide
- Website: https://sitelemetry.com
- Privacy policy: https://sitelemetry.com/privacy
- Terms of service: https://sitelemetry.com/terms
- Support: support@sitelemetry.com

Sitelemetry is operated by Egenil Teleferik Mühendislik Teknik İşletme Danışmanlık Limited Şirketi.
