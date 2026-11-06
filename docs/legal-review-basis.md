# Legal review basis

The checklist the Claude PR reviewer (`.github/workflows/claude-review.yml`) holds every
change in this repo against, with the source for each rule. **Last researched: 6 Nov 2026.**
Rules change. Re-check the sources when a date below has passed or a reviewer cites
something that looks out of date. This is a working checklist, not legal advice. Anything
marked *(confirm)* had conflicting or secondary-only sources.

## Who this applies to

- Controller: Jonathan Wilson, sole developer, United Kingdom. Users are worldwide, mostly
  UK/EU/US. Laws in scope: **UK GDPR + DPA 2018 (as amended by the Data (Use and Access) Act
  2025)**, **EU GDPR** (EU users), **Apple App Review Guidelines**, and later the **EU AI Act**
  and **UK DMCC Act** subscription rules.
- Apps covered today: AI Decorator. Each new app's page must meet the same bar.

## 1. Apple App Review (rejection / removal risk)

Source: [App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
(last updated 16 Oct 2026 *(confirm)*), [App privacy details](https://developer.apple.com/app-store/app-privacy-details/).

| Rule | What the page must do |
|---|---|
| 5.1.1(i) Privacy policies | Be linked from ASC metadata **and** inside the app. Say what data is collected, how, and **all** uses. Confirm that third parties receiving data (analytics, SDKs, AI services) give equal protection. Explain retention/deletion and how to revoke consent or request deletion. |
| 5.1.2(i) Data use & sharing (Nov 2025 change) | Sharing personal data with third parties, **explicitly including third-party AI**, needs clear disclosure **and explicit permission in the app**. Putting it only in the privacy policy is not enough ([TechCrunch](https://techcrunch.com/2025/11/13/apples-new-app-review-guidelines-clamp-down-on-apps-sharing-personal-data-with-third-party-ai), [dev forum 816140](https://developer.apple.com/forums/thread/816140)). The policy must name the AI provider and the data sent, and match the in-app consent wording. |
| 5.1.1(v) Account deletion | If an app adds account creation, it must offer in-app deletion, and the policy must say how. |
| App privacy label | The label must cover data collected by **third-party SDKs/partners** too. "Collect" = sent off-device and kept longer than needed to serve the request. The policy and label must not contradict each other. |
| 1.2 AI content creation apps | Need content filtering, reporting, and **published contact information**. The support page must carry a working contact. |
| 3.1.2(c) Subscriptions | Describe clearly what the user gets for the price (Schedule 2 of the DPLA). The support page should point to Apple for cancelling and refunds. |
| URLs | Privacy URL is required on the product page. A 404 here gets apps rejected, so shipped URLs must never break. |

## 2. UK / EU GDPR: what a privacy notice must contain

Source: UK GDPR Art. 13 ([text](https://gdpr-text.com/read/article-13/)), ICO
[Right to be informed](https://ico.org.uk/media/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/the-right-to-be-informed-1-0.pdf).

Required items (blocker if missing):
1. Controller identity and contact details.
2. Purposes of processing **and the lawful basis for each**: contract (providing the
   redesign), legitimate interests (analytics, crash reports), and consent where relied on
   (e.g. third-party AI sharing). If legitimate interests are relied on, say what they are.
3. Recipients or categories of recipients (processors: Replicate, Google/Firebase,
   RevenueCat, Apple).
4. **International transfers**: most processors are in the US. Say so, and name the
   safeguard (UK-US Data Bridge / EU-US DPF for certified recipients, otherwise IDTA / SCCs +
   UK Addendum) ([gov.uk explainer](https://www.gov.uk/government/publications/uk-us-data-bridge-supporting-documents/uk-us-data-bridge-explainer), [ICO](https://ico.org.uk/media/about-the-ico/dppc/4031439/going-stateside-transferring-data-to-the-us.pdf)).
5. **Retention period** for each data type, or the criteria used to set it.
6. Rights: access, rectification, erasure, restriction, objection, portability, and the
   right to withdraw consent where consent is relied on.
7. **Right to complain to the ICO** (and an EU supervisory authority for EU users).
8. Whether providing the data is required, and what happens if the user refuses.
9. Automated decision-making with legal effects, if any (not today).
10. Language that is plain, concise and accessible. The ICO says this is not a tick-box exercise.

## 3. Data (Use and Access) Act 2025: complaints to the controller

Source: [Squire Patton Boggs](https://www.squirepattonboggs.com/insights/publications/the-data-use-and-access-act-2025-and-the-new-right-for-individuals-to-complain-to-controllers/),
[Mayer Brown](https://www.mayerbrown.com/zh-hans/insights/publications/2026/02/preparing-for-the-data-use-and-access-act-2025-upcoming-complaints-procedure-requirement),
[Privacy World](https://www.privacyworld.blog/2026/06/the-data-use-and-access-act-2025-and-the-new-right-for-individuals-to-complain-to-controllers-what-organisations-need-to-do-before-19-june-2026/).

- **In force from 19 June 2026** *(confirm; one source said Nov 2025)*. New DPA 2018 s.164A
  gives people the right to complain **to the controller first**. Controllers need an
  accessible channel, must **acknowledge within 30 days**, investigate, and keep the
  complainant informed. There is no small-business exemption.
- The privacy notice should explain how to complain to the developer, as well as to the ICO.

## 4. Processor facts (check the policy against these)

| Processor | Fact | Source |
|---|---|---|
| Replicate (AI) | API prediction inputs, outputs, files and logs are deleted automatically **about 1 hour** after a prediction finishes. Replicate does not train on API data *(confirm in its terms)*. US-based. | [Replicate data retention](https://replicate.com/docs/topics/predictions/data-retention), [changelog](https://replicate.com/changelog/2023-01-04-api-prediction-data-no-longer-stored) |
| Google Firebase Analytics / GA4 | Retention is a property setting (2 or 14 months). The policy must match the setting. Free-text prompts sent as event params are user content and may contain personal data. Disclose them, or stop sending them. | Firebase / GA4 settings |
| RevenueCat | Receives an anonymous app user ID and App Store receipts. US-based. | RevenueCat privacy docs |
| Amazon Associates | AI Decorator can show affiliate links (`AmazonV1` flag). Clicking one sends the user to Amazon, which sets its own cookies. Disclose the affiliate relationship. | App code |

## 5. Upcoming rules to watch

- **EU AI Act Art. 50**: transparency duties from **2 Aug 2026**. Machine-readable marking
  of AI-generated images (50(2), providers) runs to **2 Dec 2026** for systems already on the
  market. The deepfake disclosure under 50(4) is for deployers. Room redesigns are not deepfakes
  of people, but stating that results are AI-generated is cheap insurance
  ([Goodwin](https://www.goodwinlaw.com/en/insights/publications/2026/08/alerts-technology-dpc-eu-ai-act-transparency-obligations-now-in-force), [Ropes & Gray](https://www.ropesgray.com/en/insights/viewpoints/2026/08/102nfqm/you-talkin-to-me-operationalising-the-eu-ai-acts-transparency-obligations)).
- **UK DMCC Act subscription contracts regime**: expected **January 2027** *(confirm;
  earlier sources said spring 2027)*. It brings key pre-contract information, renewal
  reminders, a 14-day cooling-off period after a trial converts or a renewal, and easy
  cancellation. Apple's billing covers part of this, but the support/terms pages should
  explain cancellation and refunds ([Stephenson Harwood](https://www.stephensonharwood.com/insights/subscription-reforms-brought-forward-to-january-2027-is-your-business-ready/), [Bird & Bird](https://cm.twobirds.com/en/insights/2026/uk/new-uk-legislation-to-mean-stricter-rules-for-subscription-services)).
- **Children**: if an app could appeal to under-18s in the UK, the ICO Age Appropriate
  Design Code applies. "Not directed at under-13s" alone may not be enough.
