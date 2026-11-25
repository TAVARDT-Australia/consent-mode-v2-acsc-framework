# Consent Mode v2 & Australian Privacy Principles Framework

[![Technical Audit](https://img.shields.io/badge/TAVARDT-Technical%20Audit-5b3cf5.svg)](https://tools.tavardt.com/au/consent-mode-v2-checker/)
[![JavaScript](https://img.shields.io/badge/JavaScript-Node.js-yellow.svg)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Technical implementation of Google Consent Mode v2, prior consent controls, and privacy governance aligned with the Australian Privacy Act 1988 and ACSC guidelines.

Engineered and maintained by the cyber defence and privacy engineering practice at **TAVARDT** for Australian digital infrastructure.

***

## 1. Execution Order and Architecture

Deploy this module at the top of the `<head>` section before the Google Tag Manager container loads. Proper tag sequencing guarantees that all measurement scripts respect default consent configurations before executing network requests:

```html
<script src="consent-mode-v2.js"></script>
```

Load Google Tag Manager or measurement scripts immediately after this inclusion to ensure privacy signals are active.

***

## 2. Technical Capabilities

* **Default Denied Architecture:** Enforces `denied` state for advertising and analytics cookies prior to explicit affirmative choice.
* **Event-Driven Synchronization:** Exposes `window.tavardtUpdateConsent()` to synchronize user choices with downstream analytics tags.
* **Advertising Parameter Redaction:** Activates `ads_data_redaction` to strip click identifiers when advertising storage is declined.
* **URL Parameter Passthrough:** Utilizes `url_passthrough` to retain campaign attribution without persistent client-side tracking cookies.
* **Granular Preference Mapping:** Maps individual marketing, analytics, and preference categories to official Google consent signals.
* **Zero External Dependencies:** Built with vanilla JavaScript to ensure rapid execution and zero external network overhead.

***

## 3. Consent Signals & Telemetry Matrix

<table>
  <thead>
    <tr>
      <th>Consent Parameter</th>
      <th>Telemetry & Storage Scope</th>
      <th>Default Baseline</th>
      <th>Post-Consent State</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>ad_storage</strong></td>
      <td>Controls cookie storage related to advertising</td>
      <td><code>denied</code></td>
      <td><code>granted</code> upon marketing opt-in</td>
    </tr>
    <tr>
      <td><strong>ad_user_data</strong></td>
      <td>Governs transmission of user data to advertising platforms</td>
      <td><code>denied</code></td>
      <td><code>granted</code> upon marketing opt-in</td>
    </tr>
    <tr>
      <td><strong>ad_personalization</strong></td>
      <td>Enables remarketing and personalized ad audiences</td>
      <td><code>denied</code></td>
      <td><code>granted</code> upon marketing opt-in</td>
    </tr>
    <tr>
      <td><strong>analytics_storage</strong></td>
      <td>Permits cookie storage for visitor behavior analytics</td>
      <td><code>denied</code></td>
      <td><code>granted</code> upon analytics opt-in</td>
    </tr>
    <tr>
      <td><strong>functionality_storage</strong></td>
      <td>Enables essential website features such as language settings</td>
      <td><code>granted</code></td>
      <td><code>granted</code> (strictly necessary)</td>
    </tr>
    <tr>
      <td><strong>security_storage</strong></td>
      <td>Supports authentication, fraud prevention, and session security</td>
      <td><code>granted</code></td>
      <td><code>granted</code> (strictly necessary)</td>
    </tr>
  </tbody>
</table>

***

## 4. Event-Driven Consent Update Integration

When a user updates their preferences through a consent banner or preference modal, invoke `window.tavardtUpdateConsent()` with boolean parameters:

```javascript
// Triggered by your Consent Management Platform (CMP) or banner interaction
window.tavardtUpdateConsent({
    marketing: true,
    analytics: true,
    preferences: false
});
```

This updates internal gtag consent signals and immediately dispatches a `tavardt_consent_updated` custom event to `dataLayer` to unblock authorized marketing and analytics tags.

***

## 5. Frequently Asked Questions (Technical FAQ)

### 1. Why is prior consent enforcement required before Google Tag Manager container initialization?
Under Australian Privacy Principles (APPs 1 and 5) and Google Consent Mode v2 standards, tracking tags must not write or read identifiers before consent is registered. Loading the consent configuration script before Google Tag Manager ensures default denied signals govern all subsequently dispatched measurement tags.

### 2. What is the specific function of the ad_user_data and ad_personalization signals in Consent Mode v2?
These two signals control whether user-provided data and behavioural cookies can be utilized for audience building and remarketing campaigns. When set to denied, ad platforms receive aggregate pings lacking personal identifiers, preserving measurement without cross-site tracking.

### 3. How does ads_data_redaction safeguard Australian user privacy?
When ads_data_redaction is activated, ad click identifiers such as GCLID or DCLID are stripped from network request URLs whenever ad_storage is denied. This mechanism prevents ad networks from correlating user sessions with previous ad exposures while consent is withheld.

### 4. What technical advantage does url_passthrough provide for campaign attribution?
The url_passthrough setting allows campaign landing parameters to pass between internal site pages via query strings rather than persistent cookies. This maintains aggregated conversion path tracking across a single session without writing third-party storage to the visitor device.

### 5. How does the event-driven synchronization model notify downstream tags in GTM?
Calling `window.tavardtUpdateConsent(preferences)` pushes a `tavardt_consent_updated` custom event to `dataLayer` alongside the updated signal dictionary. Tag management triggers listening to this event fire analytics or advertising scripts instantaneously once affirmative consent is received.

***

## 6. Online Diagnostic Tools (Australia)

Audit your public infrastructure using the TAVARDT diagnostic suite:

* [HTTP Security Headers Checker](https://tools.tavardt.com/au/security-headers-check/)
* [DMARC & Anti-Spoofing Verifier](https://tools.tavardt.com/au/dmarc-checker/)
* [Exposed Credentials & Secret Scanner](https://tools.tavardt.com/au/exposed-files-scanner/)
* [Full Australian Tools Portal](https://tools.tavardt.com/au/)

***

## 7. Technical Advisory & Privacy Governance in Australia

For Australian Privacy Principle reviews, web telemetry governance, and cyber resilience consulting in Sydney, Melbourne, Brisbane, or Perth, contact **TAVARDT**.

***

## Useful Links

* **Corporate Portal:** https://ag.tavardt.com/au/
* **Diagnostic Suite:** https://tools.tavardt.com/au/
* **Technical Contact:** https://ag.tavardt.com/au/contact/

***

### License
Released under the MIT License.

***

© 2026 TAVARDT. All rights reserved.
