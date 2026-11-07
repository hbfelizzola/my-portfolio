# Legal pages and privacy measures for hbfelizzola.de

Research for the ticket "What legal pages and privacy measures does a German freelancer's site need?" on the map "Spec the next version of hbfelizzola.de".

> **This is research, not legal advice.** It summarises primary sources as read on 2026-11-07 for a static, single-person freelancer site. Have a lawyer or a reputable generator check the final Impressum and privacy policy text before launch.

## Situation assumed

- Humberto is a self-employed software developer in Munich: a natural person, not in the commercial register, not in a regulated profession, no official licence needed for the work.
- hbfelizzola.de is a static site on GitHub Pages that advertises his services to prospective Clients, in English, German and Portuguese.
- Today `index.html` loads three families (Bricolage Grotesque, Atkinson Hyperlegible, JetBrains Mono) from `fonts.googleapis.com`, with `preconnect` hints to `fonts.googleapis.com` and `fonts.gstatic.com`. It links to email (`mailto:`), GitHub and LinkedIn. It has no analytics, no forms and no cookies.

## Answer in brief

| Question | Answer |
|---|---|
| Impressum needed? | Yes. § 5 DDG applies to any business site. Fines go up to EUR 50,000, and competitors can send warning letters (Abmahnungen). |
| What it contains | Full name (and trading name if used), a street address where legal papers can be served, email, a second fast contact channel (in practice a phone number), and a VAT ID or business ID number if he has one. Nothing about registers, chambers or regulators applies. |
| Where | A separate page, linked from every page with a standard label ("Impressum"), reachable in at most two clicks. |
| Privacy policy needed? | Yes, even with no analytics. GitHub logs every visitor's IP address, and email enquiries are personal data. It must cover the GDPR Art. 13 items. |
| Google Fonts | Self-host them and remove the `preconnect` hints. LG München I held that loading Google Fonts from Google without consent is unlawful because self-hosting is possible. |
| Analytics | Any JavaScript analytics on GitHub Pages needs prior opt-in consent under § 25 TDDDG, through a banner with a "reject" button as easy as "accept". Regulators will not exempt even basic visitor counting in general. The cheapest compliant option is no analytics. |
| Language | The law sets no language for the Impressum. Its content is mostly names and numbers, so one page labelled "Impressum" in every language works. The privacy policy should be translated into each language the site targets (EN, DE, PT). |

## 1. Impressum (provider identification)

### Legal basis and who must comply

- **§ 5 Abs. 1 DDG** (Digitale-Dienste-Gesetz) applies to providers of *geschäftsmäßige, in der Regel gegen Entgelt angebotene digitale Dienste*. It requires the information to be *leicht erkennbar, unmittelbar erreichbar und ständig verfügbar* (easy to recognise, directly reachable, always available). [DDG § 5]
- The DDG replaced the Telemediengesetz on **14 May 2024**. § 5 DDG takes over the duty from § 5 TMG with essentially the same content. [BGBl. 2024 I Nr. 149; IHK München leaflet p. 1]
- A site that advertises one's own services counts. The IHK München lists "owner of an advertising site (e.g. company website)" as a provider and concludes that "as a rule every homepage that is not purely private" needs the § 5 DDG information. [IHK München leaflet p. 2]
- **§ 18 Abs. 1 MStV** (Medienstaatsvertrag) separately requires name and address for any telemedia that are not purely personal or family. **§ 18 Abs. 2 MStV** adds a named responsible person for *journalistic-editorial* content. A portfolio of one's own services is commercial communication rather than journalistic-editorial content, so Abs. 2 does not apply now. It would become relevant if a blog were added later, and a blog is out of scope on the map. [MStV § 18]

### Required content for Humberto

Mapped to § 5 Abs. 1 DDG:

| § 5 Abs. 1 | Item | Applies? | What to show |
|---|---|---|---|
| Nr. 1 | Name and address | **Yes** | First and last name; a trading name may be added (the IHK example is "Software Consulting Mustermann / Hans Mustermann"). Give a **full street address where documents, including court papers, can be served**; a PO box is not enough. Do not use titles such as "Geschäftsführer", which are reserved for legal entities. [IHK leaflet p. 3] |
| Nr. 1 | Legal form, representative, capital | No | Only for companies. |
| Nr. 2 | Fast electronic contact plus direct communication, **including email** | **Yes** | Email address plus a second fast, direct, effective channel. The CJEU held that this channel "does not necessarily have to be a telephone number": an electronic enquiry form answered promptly can do. Because the map rules out a server-backed contact form, the **phone number** is the practical second channel, and the IHK names "email address and phone number". Use a normal-rate number, not a premium-rate one. [CJEU C-298/07; IHK leaflet pp. 3–4] |
| Nr. 3 | Supervisory authority | No | Only for activities that need an official licence (e.g. § 34c GewO brokers). Software development needs none. |
| Nr. 4 | Register and number | No, unless registered | Only if he is in the Handelsregister or a similar register (e.g. as e.K.). |
| Nr. 5 | Regulated profession details | No | Only for regulated professions (lawyers, doctors, architects, engineers holding a protected title, etc.). [IHK leaflet p. 5] |
| Nr. 6 | USt-IdNr. or Wirtschafts-Identifikationsnummer | **If he has one** | Show the VAT ID if one has been issued (likely if he invoices EU business Clients); there is no duty to apply for one just for the Impressum. The W-IdNr. (§ 139c AO) only needs to be shown once one has been assigned. [IHK leaflet pp. 5–6] |
| Nr. 7–8 | Liquidation; audiovisual media | No | — |

The IHK München's sample Impressum for a natural person matches this case: name, street address in Munich, phone, email, VAT ID "(sofern vorhanden)" ("if available"). [IHK leaflet p. 7]

Not needed:
- **Link to the EU online dispute resolution (ODR) platform.** Regulation (EU) 2024/3228 repealed the ODR Regulation with effect from 20 July 2025, which removed that duty. [Reg. (EU) 2024/3228]
- **Citing the statute.** "Angaben gemäß § 5 DDG" is optional. If kept, it must no longer say "§ 5 TMG". [IHK leaflet p. 6]

### Where and how it must be reachable

- **Two clicks are enough.** The BGH held that provider information reachable via two links ("Kontakt", then "Impressum") meets the "easy to recognise and directly reachable" standard. It also held that "Kontakt" and "Impressum" are established labels. [BGH I ZR 228/03; IHK leaflet p. 6]
- IHK guidance:
  - Put the information on a separate page.
  - Use a clear label ("Impressum" is established).
  - Put the link in the same place on every page, ideally visible without scrolling.
  - Don't show several links ("Über uns", "Kontakt", "Impressum") that each look as if they might hold the information. [IHK leaflet p. 6]
- In practice: one Impressum page, linked from a persistent header or footer element on every page and in every language.

### Consequences of getting it wrong

- Administrative fine of **up to EUR 50,000** for failing to provide § 5 Abs. 1 information, or giving it incorrectly or incompletely (§ 33 Abs. 2 Nr. 1, Abs. 6 Nr. 3 DDG). [DDG § 33] (The May 2024 IHK leaflet cites this as "§ 25 DDG", which is outdated numbering; the current consolidated text has it in § 33.)
- More common in practice: a competitor's or association's warning letter (Abmahnung), with a cease-and-desist declaration and legal fees. [IHK leaflet p. 7]

## 2. Privacy policy (Datenschutzerklärung)

### Is one required?

Yes.
- The GDPR applies: Humberto is established in the EU (Art. 3(1)), and a business site falls outside the "purely personal or household activity" exemption (Art. 2(2)(c)). [GDPR]
- **Personal data is processed even on a static site without analytics:**
  - **Hosting:** GitHub documents that when someone visits a GitHub Pages site, "the visitor's IP address is logged and stored for security purposes", whether or not they are signed in to GitHub. [GitHub Docs, What is GitHub Pages?] A dynamic IP address is personal data. [LG München I, Rn. 4–5, following BGH case law; GDPR Art. 4(1)]
  - **Email contact:** the `mailto:` link invites enquiries, which carry names, addresses and message content.
  - **Today's Google Fonts call** sends every visitor's IP address to Google (see §3). It goes away once the fonts are self-hosted.
- Art. 13 requires the information "at the time when personal data are obtained", and Art. 12(1) requires it to be "concise, transparent, intelligible and easily accessible". The transparency guidelines (WP260 rev.01, endorsed by the EDPB) add: "Every organisation that maintains a website should publish a privacy statement/notice", linked "on each page of this website" under a common term such as "Privacy" or "Privacy Policy". [GDPR Art. 12–13; WP260 rev.01 para. 11]

### What it must cover (GDPR Art. 13), applied to this site

| Art. 13 | Item | For hbfelizzola.de |
|---|---|---|
| 1(a) | Controller identity and contact details | Humberto, same address and email as the Impressum. |
| 1(b) | Data protection officer | None required. Under § 38 BDSG a DPO is needed only from 20 people regularly processing personal data. Say there is none, or omit the item. [BDSG § 38] |
| 1(c), 1(d) | Purposes, legal basis, legitimate interests | (1) Delivering the site and keeping it secure (server logs at GitHub): Art. 6(1)(f), interest in a secure, working site. (2) Answering email enquiries: Art. 6(1)(b) (steps before a contract) or 6(1)(f). (3) Only if analytics are added: Art. 6(1)(a) consent. |
| 1(e) | Recipients | GitHub (hosting); the email provider behind `hello@hbfelizzola.de` (to confirm which). |
| 1(f) | Third-country transfer | GitHub, Inc. is in the US. GitHub says it is certified under the **EU-U.S. Data Privacy Framework**, which has an EU adequacy decision (Commission Implementing Decision (EU) 2023/1795 of 10 July 2023). Name the DPF as the transfer mechanism and link GitHub's privacy statement. [GitHub General Privacy Statement] |
| 2(a) | Retention period or criteria | Server logs: per GitHub's policy (link to it). Emails: for as long as needed to handle the enquiry or engagement, then as tax/commercial retention rules require. |
| 2(b) | Rights | Access, rectification, erasure, restriction, objection (Art. 21) and portability (Art. 15–20). |
| 2(c) | Withdrawing consent | Only if a consent-based feature (e.g. analytics) is added. |
| 2(d) | Right to complain to a supervisory authority | For private controllers in Bavaria this is the Bayerisches Landesamt für Datenschutzaufsicht (BayLDA), Ansbach. |
| 2(e) | Whether providing data is required | Visiting needs no data beyond what the browser sends; emailing is voluntary. |
| 2(f) | Automated decision-making | None. |

Also worth stating, for transparency:
- Fonts and all other assets are served from the site itself.
- Links to GitHub and LinkedIn are plain links: nothing is sent to those services until the visitor clicks.
- No cookies are set (true today; keep it true or update the policy).

### Format and placement

- A separate page, linked from every page next to the Impressum link, using a common label ("Datenschutz" / "Privacy" / "Privacidade"). [WP260 rev.01 para. 11]
- It may share a page with the Impressum, but the two duties come from different laws; separate pages with separate links are the usual pattern and keep each easy to find.
- Plain language: no "may", "might" or "possibly" where the processing is known, and short structured sections. [WP260 rev.01 para. 13]

## 3. Google Fonts: self-host them

**Primary source: LG München I, judgment of 20 January 2022, 3 O 17493/20.**
- **Ruling:**
  - The website operator was ordered to stop disclosing the plaintiff's IP address to Google through Google Fonts, under penalty of up to EUR 250,000 per violation.
  - It also had to give information about the data processed.
  - It had to pay **EUR 100 in non-material damages** (Art. 82(1) GDPR).
- **Reasoning:**
  - A dynamic IP address is personal data (Rn. 4–5).
  - Sending it to Google without consent infringed the visitor's rights (Rn. 6–7).
  - **Legitimate interest under Art. 6(1)(f) failed because Google Fonts "can be used without a connection to a Google server"**, so the transfer was not necessary (Rn. 8).
  - Visitors are not expected to hide their own IP addresses (Rn. 9).
  - Switching to local fonts afterwards does not remove the risk of repetition. Only a cease-and-desist declaration backed by a penalty does (Rn. 10).
  - The damages rested partly on the transfer to the US (pre-DPF, citing Schrems II) and on the deterrent purpose of liability (Rn. 12).

**What this means here:**
- The current `index.html` does exactly what the court condemned: it loads CSS from `fonts.googleapis.com`, which then loads font files from `fonts.gstatic.com`, on every page view.
- The two `<link rel="preconnect">` tags open connections to Google before any CSS loads, so they send the IP address to Google too. Remove them as well.
- Since 2023 Google is DPF-certified, which weakens the US-transfer part of the court's damages reasoning. The core holding does not change: self-hosting is a ready alternative, so the transfer is unnecessary. Self-hosting needs neither consent nor a legitimate-interest argument, and costs one-time setup work.
- **Measure:** Download the WOFF2 files, serve them from the repo, and declare them with `@font-face` in the site's own CSS. Then check in the browser's network panel that no request goes to any Google domain.
- The three families are distributed through Google Fonts under open font licences (generally SIL OFL 1.1), which allow self-hosting. Check each family's licence file when copying them into the repo.

The same reasoning applies to any other resource loaded from a third-party server, for example JS/CSS CDNs, embedded booking widgets, YouTube or maps embeds: self-host it or link out to it.

## 4. Analytics: consent rules if any are added

### The rule

- **§ 25 Abs. 1 TDDDG** (Telekommunikation-Digitale-Dienste-Datenschutz-Gesetz, the former TTDSG, renamed on 14 May 2024): *storing* information on, or *accessing* information already on, a user's device is allowed only with consent, based on clear and comprehensive information and given to GDPR standards. [TDDDG § 25]
- **§ 25 Abs. 2 TDDDG** gives only two exceptions:
  - transmitting a message over a public network;
  - access that is **strictly necessary** to provide a digital service the user has **expressly requested**. [TDDDG § 25]
- **§ 25 is not limited to cookies or personal data.** It covers localStorage and sessionStorage (DSK OH Digitale Dienste Rn. 21) and fingerprinting built from screen size, OS version or installed fonts (Rn. 23). Reading device properties with JavaScript and sending them to a server counts as access (Rn. 24).
- The EDPB agrees: JavaScript that "instructs the browser of the user to send asynchronous requests with the targeted information" falls within Art. 5(3) ePrivacy, the EU rule behind § 25 TDDDG. So do tracking pixels and tracking links, and IP-only tracking can too. [EDPB Guidelines 2/2023 v2.0, paras. 33, 47–51, 54–55]

### Does basic visitor counting escape consent?

Not reliably.
- The German regulators (DSK) **explicitly refuse to say that "reach measurement" is generally exempt** under § 25 Abs. 2 Nr. 2. The term is too vague, the purposes differ, and third-party tools collect far more than a count (OH Digitale Dienste Rn. 87–92).
- "Even the simple measurement of visitor numbers is therefore not per se part of the basic service"; it depends on the purpose (Rn. 90).
- They do describe what pure counting looks like: a page counter, server log files without personal data, or a simple counting pixel served by the site itself that collects nothing more (Rn. 88).
- **GitHub Pages gives the site owner no server logs and no server-side code**, so on this host any analytics means client-side JavaScript or a third-party pixel. Both fall under § 25.

### What a valid consent setup requires

If analytics are added despite the above:
- **Prior opt-in.** Nothing may load or run before consent. Silence, pre-ticked boxes or inactivity are not consent (GDPR Art. 4(11), Recital 32).
- **Reject as easy as accept, on the first layer.** If rejecting takes more clicks or a second banner layer, consent is not freely given; regulators treat this as bad faith (DSK Rn. 58–60).
- **Withdrawal as easy as giving consent,** through the same channel on the site, e.g. a persistent "privacy settings" link (GDPR Art. 7(3); DSK Rn. 61–62).
- **Granular, documented consent.** Keep records of the banner texts that were shown (DSK Rn. 85).
- **Privacy policy update:** the tool, its provider, the data, the legal basis (consent), retention, any third-country transfer, and how to withdraw.
- The GDPR still applies alongside § 25 to whatever personal data the tool processes (DSK Rn. 25–26).

**Practical conclusion for the spec:**
- No analytics: no banner, a shorter privacy policy, no legal risk from this source.
- Any analytics on GitHub Pages: plan for a compliant consent banner, and accept that many visitors will reject (or never answer) it, which thins the data.
- A tool marketed as "cookieless, no consent needed" is a vendor claim. German regulators do not endorse it in general, and it would need a configuration-specific assessment.

## 5. Language of the legal pages

- **Impressum.** Neither § 5 DDG nor Art. 5 of the E-Commerce Directive sets a language; the test is that the information is easy to recognise and reachable. The content is almost all language-neutral (name, address, phone, email, VAT ID).
  - *Inference, not settled law:* one Impressum page shared by all three language versions is defensible. It can carry German field labels plus English/Portuguese equivalents ("Impressum / Legal notice / Aviso legal"). Keep the link label "Impressum" in every language, because that is the term German case law and the IHK treat as established. [BGH I ZR 228/03; IHK leaflet p. 6]
- **Privacy policy.** GDPR Art. 12(1) requires "clear and plain language", and the transparency guidelines say a translation "should be provided where the controller targets data subjects speaking those languages" (WP260 rev.01 para. 13). The site deliberately targets English, German and Portuguese speakers, so **publish the privacy policy in all three languages**. Make every translation accurate enough that it "does not have to be deciphered or re-interpreted" (ibid.).
  - *Inference:* German is a sensible reference version, since the controller and the competent authority (BayLDA) are German. If the versions might drift apart, state which one prevails.

## 6. Checklist for the spec

1. Impressum page with: name (plus optional trading name), serviceable street address, email, phone, VAT ID / W-IdNr. if issued. Link it from every page in every language, labelled "Impressum".
2. Privacy policy page in EN, DE and PT covering the Art. 13 items above: GitHub hosting and IP logs, the DPF transfer, email enquiries, rights, the BayLDA complaint right. Link it from every page.
3. Self-host the three font families. Delete the Google Fonts `<link>` and both `preconnect` tags, and confirm in DevTools that no request goes to a third-party host.
4. Load no other third-party resources (CDNs, embeds); link out to booking tools and social profiles instead.
5. Analytics: either none (recommended for v1), or a consent banner with an equal reject button, no loading before consent, easy withdrawal, and a policy update.
6. Open items for Humberto:
   - Which street address to publish: a home address is public in the Impressum.
   - Which phone number to show.
   - Whether he has a VAT ID.
   - Which provider hosts `hello@hbfelizzola.de` (it is a recipient in the privacy policy).

## Sources

Statutes and regulations
- [DDG § 5, Allgemeine Informationspflichten](https://www.gesetze-im-internet.de/ddg/__5.html), gesetze-im-internet.de (Federal Ministry of Justice)
- [DDG § 33, Bußgeldvorschriften](https://www.gesetze-im-internet.de/ddg/__33.html)
- [TDDDG § 25, Schutz der Privatsphäre bei Endeinrichtungen](https://www.gesetze-im-internet.de/ttdsg/__25.html)
- [BDSG § 38, Datenschutzbeauftragte nichtöffentlicher Stellen](https://www.gesetze-im-internet.de/bdsg_2018/__38.html)
- [MStV § 18, Informationspflichten](https://www.gesetze-bayern.de/Content/Document/MStV-18), gesetze-bayern.de
- [Regulation (EU) 2016/679 (GDPR)](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679), Arts. 2(2)(c), 3(1), 4(1), 4(11), 6(1), 7(3), 12(1), 13, 82, Recital 32
- [Regulation (EU) 2024/3228, repealing the ODR Regulation](https://eur-lex.europa.eu/eli/reg/2024/3228/oj/eng)
- DDG promulgated as Art. 1 of the law of 6 May 2024, BGBl. 2024 I Nr. 149, in force 14 May 2024 (see the [IHK Bayreuth notice](https://www.ihk.de/bayreuth/hauptnavigation/service/recht/allgemeine-rechtsthemen/telemediengesetz-tmg-ist-jetzt-digitale-dienste-gesetz-ddg--6204406) and [buzer.de consolidated history](https://www.buzer.de/gesetz/16427/a310758.htm))

Case law
- LG München I, Endurteil v. 20.01.2022, 3 O 17493/20 (Google Fonts), [full text on gesetze-bayern.de](https://www.gesetze-bayern.de/Content/Document/Y-300-Z-GRURRS-B-2022-N-612) (GRUR-RS 2022, 612)
- CJEU, C-298/07, judgment of 16.10.2008, *Bundesverband der Verbraucherzentralen v deutsche internet versicherung*, ECLI:EU:C:2008:572, [EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:62007CJ0298)
- BGH, Urteil v. 20.07.2006, I ZR 228/03 (*Anbieterkennzeichnung im Internet*), [text on lexetius.com](https://lexetius.com/2006,2487)

Regulator and chamber guidance
- DSK, [Orientierungshilfe der Aufsichtsbehörden für Anbieter:innen von digitalen Diensten (OH Digitale Dienste), Version 1.2, November 2024](https://datenschutzkonferenz-online.de/media/oh/OH_Digitale_Dienste.pdf), Rn. 21–26, 58–62, 77, 85–95
- EDPB, [Guidelines 2/2023 on Technical Scope of Art. 5(3) of ePrivacy Directive, Version 2.0, adopted 7 October 2024](https://edpb.europa.eu/system/files/2024-10/edpb_guidelines_202302_technical_scope_art_53_eprivacydirective_v2_en_0.pdf), paras. 33–34, 47–55
- Article 29 Working Party, [Guidelines on transparency under Regulation 2016/679, WP260 rev.01 (11 April 2018), endorsed by the EDPB](https://ec.europa.eu/newsroom/article29/items/622227), paras. 11 and 13
- IHK für München und Oberbayern, [Merkblatt "Pflichtangaben im Internet-Impressum", Stand Mai 2024](https://ihk-muenchen.de/ihk/Merkblätter-WettbewerbsR/Pflichtangaben-Internetimpressum_Stand05_2024.pdf)

Platform documentation
- GitHub Docs, [What is GitHub Pages?](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages) (visitor IP logging)
- GitHub, [General Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) (effective 27 April 2026; EU-U.S. DPF certification)
