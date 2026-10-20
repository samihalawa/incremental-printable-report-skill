---
name: incremental-printable-report-skill
description: Create, refresh, save and optionally print a useful, visual project report from current primary records. Reuse one canonical report and Drive identity, report only the delta since the last cutoff plus still-open obligations, compare executors by time (so every platform, including ones without token telemetry, is measured), render inline in memory and prove the print at the printer.
---

# Incremental Printable Report

## 1. Scope and authority
- Report on the project named by the request or the workspace. Use the user's language, audience and formats.
- **Authority.** A report request authorises reading sources and producing the report. It does not authorise filing, sending, CRM state changes, scheduling or reorganising files.
  - "Print" authorises one physical job.
  - "Printable" means a ready PDF only.

## 2. Bind the report once
- **Read the destination policy first.** That is the destination's `AGENTS.md` reporting section and the topic row in `INDEX.md`.
- **One subject, one canonical path and Drive ID.**
  - Search aliases and filenames before creating anything.
  - Never create `v2`, `final`, `copy` or dated replacements.
  - Different formats are exports of the same report family (for example `… — informe diario.pdf` and `… — panel visual.pdf`).
- **Recover the last cutoff** from the canonical report and its INDEX row. A second writer on the same report waits; re-read the target just before writing.

## 3. Collect facts incrementally, in one snapshot
- **On a re-run, read only the delta since the cutoff from primary records:** the CRM (complete cursor pagination, backoff on 429), the receipts folder, and owner messages after the cutoff.
  - Full history recovery (all transcripts, Chronicle, Screenpipe, Computer History) runs only for a first report, an explicit request or a named gap.
  - Never rebuild the analysis from thousands of logs on every run.
- **Take one data snapshot per report.** Every page must come from it, so the numbers agree. State the cutoff time on the page.
- **Counting rule for outcome time** (use it everywhere):
  - the explicit `submittedAt` field when present;
  - otherwise the first date-time on the receipt line;
  - otherwise date only, counted per day but not per hour.
- **Keep states separate:** prepared, submitted, admitted, awarded, paid. Deduplicate lots, replacements, copies and concurrent executors before totals.
- **Attribution** comes from the receipt line or claim at filing time. When it is lossy, say how many outcomes are unattributed.

## 4. Measure efficiency by time first
- **Compare every executor or platform on time, which all of them expose.** Grok and others without token telemetry are never left out.
  - Outcomes per active hour: the span from first to last outcome per day, summed over days.
  - Median minutes between consecutive outcomes.
  - Outcomes per day.
- **Tokens (non-cached input plus output) per outcome are a secondary cost line.** Show them only for platforms that expose them, and label that the others are not counted. A platform-native usage gauge (for example a weekly pool percentage) is compared only within that platform.
- **Mark method changes and mistakes on the timeline** with a number, the measured effect (before vs after on the same metric) and worked / failed / partial. Pending decisions are not losses. Never claim savings without measured inputs.

## 5. Choose the report kind and write it
Pick what the request implies; combine kinds only when asked.
- **Status briefing:** for each active matter, its position, what is missing, the next action, who owes it and the real deadline.
- **Visual efficiency panel:**
  - 4 headline tiles;
  - outcomes per hour and per day;
  - executor comparison by time (tokens as a side note);
  - the numbered change/mistake timeline;
  - at most 5 "what to do now" points.
- **Owner action sheet:** only physical, payment or personal-decision steps, as a dated checklist. Agent-doable electronic work never goes here.

**Writing rules:**
- Apply the usefulness test to every item: would it help the owner understand, decide or act on paper? Keep a consequential older obligation; drop unchanged old news.
- Keep metrics few. Each chart has one job and one value axis.
- Labels follow the user's language and number format. Status is shown by icon plus word, never colour alone.
- The body holds facts, implications, useful uncertainty and actions. It holds no prompts, tool or agent jargon, methods, source inventories, credentials or process chatter. Source pointers go in metadata or the CRM, not the print body.
- **Compare semantically with the last verified report.** With no meaningful change and all outputs verified, reuse them; with an explicit reprint request, re-render without inventing progress.

## 6. Save in Drive
- Persist the requested source and PDF in the established report root (for example `AI_REPORTS_MASTER`), resolved from current instructions, not hard-coded.
- Update existing files in place. Update the INDEX row only when the subject, files, cutoff or status changes.
- Verify the exact remote identity (Drive file ID) after saving. A local synced path alone does not prove cloud persistence.

## 7. Render inline and check once
- **Build data and charts in memory.** For example, one interactive Python session with matplotlib and PdfPages, kept alive between steps.
  - Write only the requested PDF/source.
  - No helper scripts, scratch images, intermediate HTML or exports, trackers or logs.
  - A print-only request may stream the PDF to the printer without writing a file.
- **Page defaults:** A4 portrait, readable type, page numbers. Colour is allowed if meaning survives grayscale. No links, widgets or raw URLs in a print PDF.
- **Do one self-check of every page** from a low-resolution in-memory preview. Check page count and size, labels, clipping, dates, amounts and number format. No reviewer or auditor agents.

## 8. Print and prove
- Use the printer's IPP queue, not a raw socket queue, so the printer reports its own job state. Bind the job ID to this PDF.
- Claim "printed" only on the terminal native state (`completed` plus impressions, or `job-completed-successfully`). CUPS acceptance proves only queuing.
- After an uncertain response, inspect existing jobs before resubmitting.

## Closure
Return the outcome, the material changes, the canonical source and PDF links, the cutoff, and the exact save and print state. State coverage gaps only where material. On the next run, resume the bound report family and its missing outputs.
