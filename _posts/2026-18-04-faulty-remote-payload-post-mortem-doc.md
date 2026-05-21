---
layout: post
title: "Post-Mortem Analysis: Invalid remote payload causing drop in app revenue"
date: 2026-05-20 08:00:00
description: "Deprecated paywall displayed due to faulty remote config"
---

### ISSUE SUMMARY

Between 2026-05-13 07:17 UTC and 2026-05-15 14:59 UTC, the app displayed a deprecated paywall screen with a lower conversion rate. This resulted in a severe drop in daily sales. During this period of 55 hours and 42 minutes, a minimum of 4500 users were affected.

User traffic metrics remained normal throughout this period.

---

### EVENT TIMELINE

<table style="border-collapse: separate; border-spacing: 0 10px; width: 100%; font-family: Arial, sans-serif;">
  <tr>
    <th align="left" style="background:#f2f2f2; padding:10px; color:black;">Date & Time</th>
    <th align="left" style="background:#f2f2f2; padding:10px; color:black;">Event</th>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-13 07:17 UTC</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">A remote config payload is pushed targeting behaviour of a CTA button (unrelated to the paywall screen) in the app.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-14</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">Drop in sales - slow yet steady but not significant enough to trigger a reaction.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-15 UTC Early Hours</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">Second day of steady drop in sales - significant enough to be considered an anomaly.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-15 14:00 UTC</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">A support email is received from a user asking how they can make the purchase in the app.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-15 14:15 UTC to 14:30 UTC</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">Email is acknowledged, triggering an investigation. Purchase flow tested leading to the discovery of a deprecated paywall screen being displayed instead of the new one with better conversion rate.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-15 14:30 UTC to 14:45 UTC</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">A quick investigation finds a broken JSON configuration payload being fetched from the remote server.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-15 14:59 UTC</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">A new remote payload with a proper JSON body is made available for distribution, effectively fixing the issue for new & existing users.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-15 15:07 UTC</td>
    <td style="background:#f7f9fc; border-radius:6px; padding:10px; color:black;">A support email replying to the user is sent.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">2026-05-19 16:03 UTC</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">The deprecated paywall screen is permanently removed from the codebase. Changes sent for production release under build 32.</td>
  </tr>
</table>

---

### RCA (ROOT CAUSE ANALYSIS)

Using the 5 Whys methodology.

<table style="border-collapse: separate; border-spacing: 0 10px; width: 100%; font-family: Arial, sans-serif;">

  <tr>
    <th style="background:#f2f2f2; padding:10px; text-align:left; color:black;">Step</th>
    <th style="background:#f2f2f2; padding:10px; text-align:left; color:black;">Details</th>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; width: 20%; color:black;">Issue</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">Sales dropped significantly.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">Why #1</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">Users were displayed a deprecated paywall screen with a lower conversion rate instead of the newer paywall screen with significantly better conversion performance.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">Why #2</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">The default paywall screen (old & deprecated) was intended to be overridden using a configuration payload fetched from a remote server. The payload was successfully fetched but not applied.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">Why #3</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">The fetched remote payload contained an invalid JSON structure.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">Why #4</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">The JSON structure was not validated on the server side before being made available for distribution.</td>
  </tr>

  <tr>
    <td style="background:#fff4e6; padding:10px; border-radius:6px; color:black;">Why #5</td>
    <td style="background:#f7f9fc; padding:10px; border-radius:6px; color:black;">The configuration payload relied on manual verification, which was skipped (human error), and there was no automated system in place to validate payload integrity prior to release.</td>
  </tr>

</table>
---

### IMPACT

Between the time the faulty payload became available for distribution and the fix was applied, around 4500 users were affected.

Daily revenue dropped by more than 90%, including at least one refund likely triggered by the deprecated purchase flow experience.

User acquisition and traffic metrics remained normal throughout the incident period, indicating that the primary impact was conversion-related rather than traffic-related.

It is also possible that the app experienced a temporary ranking decrease due to the sudden drop in sales velocity, though this remains speculative.

---

### CONTRIBUTING FACTORS

##### Human Error

- The configuration payload structure was not manually validated before deployment. Additionally, no post-deployment verification was performed.

##### Technical Limitation

- The dashboard/system responsible for payload distribution did not automatically validate JSON integrity before release.

##### Tightly Coupled Configuration File

- A single JSON payload was used to configure multiple unrelated application behaviors. As a result, a failure in one part of the payload caused unrelated configurations to fail and revert to defaults.

- Had the configuration been decoupled into isolated payloads with a 1:1 mapping to features, the incident impact would likely have been limited to the intended target only.

---

### RESOLUTION

##### Immediate Fix

- The configuration payload was updated with valid JSON data, restoring proper paywall behavior.

##### Permanent Fix

- The deprecated paywall screen and all related code were removed from the codebase (PR #147).
- A ticket was created to decouple the configuration system into isolated payloads (Issue #138 - TBD).
- A ticket was created to document release checklist for remote configuration changes (Issue #139 - TBD).

---

### ACTION ITEMS
- Remove deprecated paywall from the codebase ✅
- Create an incident report & post mortem analysis ✅
- Decouple configuration payloads ⬜️
- Establish release checklist for remote configuration changes ⬜️

---

### SUPPORTING EVIDENCE
> All time variables below are in UTC+5:45 timezone

<img src="/assets/img/posts/rca/revenue-chart.png" height="400px">
> Revenue data trend between May 10 & 17 (somewhat skewed due to timezone difference).  The decreasing trend is visible towards the end.

---

<img src="/assets/img/posts/rca/customer-email.png" width="700px">
> User support email that loosely translates to "How can I buy your program?"

---

<img src="/assets/img/posts/rca/fetch-velocity.png" height="300px">
> Remote payload fetch velocity (2K unique app instances in average fetching in the past 24 hours)

---

<img src="/assets/img/posts/rca/config-versions.png" height="100px">

> Remote payload versions (shows the time between the faulty payload and a corrected one)

---
---