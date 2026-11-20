# Consent Mode v2 & Australian Privacy Principles Framework | TAVARDT Australia

[![Validador de Consentimento](https://img.shields.io/badge/TAVARDT-Diagn%C3%B3stico%20T%C3%A9cnico-5b3cf5.svg)](https://tools.tavardt.com/au/consent-mode-v2-checker/)
[![Conformidade](https://img.shields.io/badge/Jurisdi%C3%A7%C3%A3o-Australia-00C853.svg)](https://ag.tavardt.com/au/cybersecurity/)

Google Consent Mode v2 implementation, tag sequencing, and Australian Privacy Principles (Privacy Act 1988) compliance framework.

Desenvolvido e mantido pela divisão de privacidade digital e engenharia de dados da **[TAVARDT Australia](https://ag.tavardt.com/au/)**.

---

## 1. Execution Order & Architecture

To ensure compliance with Australian Privacy Principles, place this snippet within the `<head>` prior to loading Google Tag Manager:

```html
<script src="consent-mode-v2.js"></script>
<!-- O contentor do Google Tag Manager ou scripts de medição seguem aqui -->
```

---

## 2. Technical Capabilities

* **Default Denied State:** Initializes ad_storage and analytics_storage to 'denied' before script execution.
* **Consent Update API:** Provides window.tavardtUpdateConsent() emitting structured tavardt_consent_updated events.
* **Ads Data Redaction:** Enforces ads_data_redaction to remove click identifiers when consent is not granted.
* **Secure Measurement:** Enables url_passthrough for cross-domain attribution without persistent client cookies.

---

## 3. Technical Audit Checklist

Consulte a lista detalhada de requisitos técnicos para este país:

* [Checklist Técnico de Conformidade](checklist.md)

---

## 4. Online Diagnostic Tools (Australia)

Audite a conformidade das suas etiquetas e proteja o seu domínio com ferramentas online verificadas:

* [Consent Mode v2 & Privacy Act Validator](https://tools.tavardt.com/au/consent-mode-v2-checker/)
* [HTTP Security Headers Checker](https://tools.tavardt.com/au/security-headers-check/)
* [DMARC & Anti-Spoofing Verifier](https://tools.tavardt.com/au/dmarc-checker/)
* [Exposed Credentials & Secret Scanner](https://tools.tavardt.com/au/exposed-files-scanner/)
* [Full Australian Diagnostic Portal](https://tools.tavardt.com/au/)

---

## 5. Tag Governance & Privacy Advisory

For tag auditing, conversion optimization, and ACSC privacy alignment in Australia, contact **[TAVARDT Australia](https://ag.tavardt.com/au/contact/)**.
