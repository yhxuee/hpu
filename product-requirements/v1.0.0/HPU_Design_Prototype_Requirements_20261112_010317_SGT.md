# HPU Design Prototype Requirements

## Document control

| Field | Value |
| --- | --- |
| Product | HPU |
| Document version | v1.0.0 |
| Created | 2026-11-12 01:03:17 SGT (UTC+08:00) |
| Status | Discussion baseline for design review; not an approved implementation specification |
| Deliverable | Product and interaction requirements for a design prototype |
| Working platform assumption | iPhone-first; optional Apple Health integration |
| Document language | English |
| Scope boundary | Documentation only. No application, executable prototype, model integration, or release is requested by this document. |

The version identifies this requirements package, not a shipped application. Requirements below distinguish user-established direction from proposed design decisions and unresolved research questions.

## 1. Product intent

HPU helps people with demanding workloads and strong personal ambitions understand where their mental effort goes, recognize persistent demands on their attention, and review whether their commitments reflect their priorities.

The central user behavior is already established outside HPU: people discuss difficult experiences with friends through messaging apps, or with an AI assistant. Retelling everything in another app adds friction before the user knows whether that app is useful.

HPU should turn voluntarily imported conversations into an evolving personal event record. Its distinctive value is continuity across conversations, recurrence tracking, and periodic review. A standalone conversational assistant is secondary to this workflow.

**Working product promise:** Turn conversations you have already had into a clearer picture of what is occupying your attention.

The product should help answer:

1. Where has my effort been going: personal priorities, work responsibilities, other people, or shared goals?
2. Which commitments feel worthwhile, and which repeatedly demand more than I want to give?
3. Which events keep returning, and how has their impact changed?
4. What appears alongside changes in my rest and recovery?
5. What small adjustment do I want to try next?

## 2. Decision status

### 2.1 User-established direction

- Serve high-load, ambitious users who value reflection and analytical review.
- Track effort allocation, perceived return, periodic audits, and trends.
- Make screenshot OCR and reuse of existing conversations central to capture.
- Support local AI summarization where actually available.
- Keep AI-dependent functionality separate so unsupported users retain a useful product.
- Treat repeated discussion of an event as a potentially important signal.
- Explore Apple Watch and Apple Health data, especially sleep and heart rate.
- Keep the core experience useful without an Apple Watch.
- Remain in product and prototype planning at this stage.

### 2.2 Proposed baseline for this prototype

- Use an import-first experience organized around persistent events.
- Keep subjective impact, observed recurrence, and recovery context distinct.
- Use interpretable descriptions and evidence instead of an unvalidated mental-energy percentage.
- Make OCR independent of generative AI.
- Add health observations only when usable data exists; do not automatically assign bodily changes to an event.
- Prefer calm, precise, restrained visual design and short interactions.
- Position the experience around personal effectiveness and reflection; final brand and marketplace positioning remain open.

### 2.3 Open decisions

- Initial audience segment: employed professionals, founders/independent workers, students/researchers, or a narrower group.
- Final brand language and the meaning of the HPU name.
- Whether a separate third-party on-device model is viable for unsupported AFM devices.
- Whether optional cloud processing belongs in the first release.
- Original screenshot retention, backup, and synchronization defaults.
- Validated scoring rules, personal baseline windows, and minimum evidence requirements.
- Release platform versions, localization coverage, pricing, and subscription boundaries.

## 3. Experience principles

1. **Reuse before requesting input.** An imported conversation should replace substantial retyping.
2. **Deliver value before asking for commitment.** Show a usable event preview before account creation, a long questionnaire, or optional health setup.
3. **Preserve user authority.** Summaries, event matches, and interpretations must be correctable.
4. **Make evidence inspectable.** Distinguish source text, user confirmation, model suggestions, and device observations.
5. **Keep missing information unknown.** Missing entries, absent sensor samples, or unavailable AI must not become zero burden or assumed improvement.
6. **Support closure.** Users can save and leave without completing an analysis session.
7. **Avoid creating another performance obligation.** No streak penalties, mandatory reflection, or forced task cancellation.
8. **Separate cost from value.** A demanding commitment may be worthwhile; an activity serving others is not automatically wasteful.

## 4. Prototype scope

### 4.1 Required journeys

- Import one or multiple conversation screenshots.
- Paste an existing text conversation.
- Review extracted content and correct speaker attribution where necessary.
- Create an event or append a new episode to an existing event.
- Provide optional one-tap feedback about current attention demand.
- Review an event timeline and its latest state.
- View a weekly audit and a longer-term trend concept.
- Explore an optional sleep association with user confirmation.
- Complete the core journey with neither generative AI nor health data.
- Experience loading, partial extraction, uncertain matching, and unavailable-capability states.

### 4.2 Secondary concepts to show lightly

- A short responsibility/scope clarification tool.
- A communication draft the user can copy after review.
- One optional adjustment experiment linked to an audit finding.
- User-chosen follow-up reminders.

### 4.3 Outside this prototype's implementation scope

- Automatic access to private messaging histories or background monitoring of conversations.
- Automatic sending of messages to friends, colleagues, or AI services.
- A full task manager, social network, relaxation game, or general-purpose chatbot.
- Clinical diagnosis, treatment claims, or legal responsibility judgments.
- Scientifically calibrated mental-energy units or exact responsibility percentages.
- A standalone Watch application or continuous physiological monitoring implementation.
- Production OCR/model benchmarks, HealthKit integration, payments, or deployment.

## 5. Information architecture

Proposed bottom navigation:

| Destination | Primary purpose | Main content |
| --- | --- | --- |
| Today | Capture and orient | Import action, active events, recent updates, optional recovery context |
| Events | Maintain continuity | Search, filters, event list, event detail and timeline |
| Audit | Review patterns | Weekly review, trends, evidence, optional adjustment experiment |
| Settings | Control processing and data | Processing capabilities, health connection, privacy, export/delete, reminders |

Import is the most prominent action on Today and remains available from Events. Event-specific reflection tools live inside event detail rather than taking over the primary navigation.

Avoid a large score dashboard before enough information exists to make it useful.

## 6. Core information model for design

| Object | Meaning | Important distinctions |
| --- | --- | --- |
| Source item | A voluntarily imported screenshot or text passage | Import time is not necessarily conversation or event time |
| Conversation episode | A distinct discussion or update about an event | Several overlapping screenshots can represent one episode |
| Event | A persistent real-world situation | Can contain multiple episodes, changes, and outcomes |
| User assessment | A user's own report of current impact or value | Timestamped; newer assessments do not erase history |
| Suggested interpretation | An AI or rule-generated candidate | Must not silently become a confirmed fact |
| Health observation | A sample or aggregate from an available source | Carries time, source, coverage, and metric definition |
| Association | A possible link between an event and an observation | Temporal proximity alone does not establish causation |
| Audit finding | A description supported by selected records | Links back to evidence and can be disputed |
| Adjustment experiment | One user-selected change | Optional; can be helpful, neutral, unhelpful, or untried |

Keep event time, conversation time, screenshot/import time, and assessment time separate. If an original time is unknown, display that uncertainty instead of substituting import time.

## 7. Capture and import requirements

### 7.1 Entry points

- System share sheet accepting supported images or text.
- In-app selection of one or multiple screenshots.
- Explicit paste of copied text.
- Optional short manual entry for experiences with no conversation source.

Messaging-app sharing behavior must be verified individually. The prototype must not imply that HPU can silently read WeChat, iMessage, WhatsApp, or other apps.

### 7.2 Import sequence

1. Receive the selected material and preserve the draft.
2. Extract text locally when the input is an image.
3. Identify ordering and likely overlaps; allow review when uncertain.
4. Produce an event preview using available capabilities.
5. Offer a new event or a candidate existing event.
6. Offer one optional current-impact question.
7. Save without requiring deeper reflection.

If analysis cannot complete inside the share interaction, allow the material to be saved for later review. Do not promise unlimited processing in a share extension.

### 7.3 Preview content

- Suggested title or a selected source excerpt.
- Concise summary where generation is available.
- Original text accessible through an evidence control.
- Suggested event match with an explicit alternative to create a new event.
- Optional impact chips: “Not much,” “Occasionally on my mind,” “Hard to put down,” and “Skip.”
- Primary action: “Save.”

In the no-generative-AI state, show extracted text and a short editable excerpt instead of implying that a semantic summary was generated. Offer recent events and conservative keyword-based candidates for manual selection.

### 7.4 Extraction safeguards and edge cases

- Handle overlapping screenshots without increasing recurrence counts.
- Provide reorder, remove, and retry controls for multi-image imports.
- Let users identify their own messages if bubble position or identity is ambiguous.
- Distinguish the user's statements, another person's opinions, and an AI assistant's suggestions.
- Preserve uncertainty around missing dates, quotes, truncated messages, and unreadable regions.
- Support saving partial results; do not force a complete re-entry after one image fails.
- Keep OCR confidence separate from confidence in an interpretation.
- Allow irrelevant or private passages to be excluded before further processing.
- Long conversations may produce a partial result, but the interface must disclose omitted or unprocessed material.

## 8. Event continuity and recurrence

An event should remain recognizable across different friends, apps, and later AI conversations. Semantic similarity is a suggestion mechanism, not permission to merge unrelated situations automatically.

### 8.1 Event detail

Show:

- Title and short account of the situation.
- Latest user-reported state.
- First known occurrence and most recent update, with time uncertainty where relevant.
- Distinct discussion episodes and the days on which they occurred.
- Timeline of new information, renewed concern, actions, and outcomes.
- Optional allocation, willingness, and perceived-value labels.
- Linked recovery observations, if any.
- Actions: add update, correct summary, separate an episode, merge with confirmation, pause reminders, and mark resolved or reopen.

“Resolved” is a user-controlled state. Silence alone does not resolve an event.

### 8.2 Recurrence interpretation

| Situation | Required treatment |
| --- | --- |
| Three overlapping screenshots of one exchange | One episode after deduplication |
| The same screenshot imported twice | Detect a likely duplicate; avoid silent double counting |
| The same story told to several friends close together | Preserve separate sources; do not scale burden linearly by audience size |
| A later conversation with new decisions | Label as progress or new information where confirmed |
| A later conversation about renewed distress | Eligible evidence of continued attention demand |
| Opening an event from an HPU reminder | Not automatically counted as spontaneous recurrence |
| Repeated visits without an explicit update | Interaction metadata, not proof of rumination |

When clarification is useful, ask only: “Is there new progress, or is this bothering you again?” Include “Both” and “Not sure.”

## 9. Mental-effort assessment

### 9.1 Separate the dimensions

| Dimension | Example evidence | Display approach |
| --- | --- | --- |
| Current attention demand | User's current report | A small labeled scale, with skip |
| Recurrence | Distinct confirmed episodes | Counts and dates, with provenance |
| Persistence | Known ongoing influence over time | Timeline and latest status |
| Functional impact | User reports effects on focus, work, rest, or interaction | Optional impact labels |
| Willingness | Chosen, necessary, difficult to decline, mixed | Optional labels |
| Perceived value | Progress, growth, connection, recovery, not yet apparent | Optional labels; allow delayed returns |
| Effort allocation | Personal goals, work role, others, shared goals, mixed/unknown | User-correctable categorization |

These are product design dimensions, not a validated clinical instrument.

### 9.2 Initial presentation

Prefer an explanation such as:

> Still occupying attention. Mentioned in three distinct conversations across five days. You twice selected “Hard to put down.” Your latest update says the discussion helped.

Do not display absolute mental-energy consumption, clinical severity, or precise responsibility percentages.

If a review-priority ranking is explored, label it as a product heuristic. Its main evidence should come from the user's assessments, persistence, and qualified recurrence. Keep evidence coverage separate from the priority label.

### 9.3 Allocation and return reporting

- Keep cost, beneficiary, willingness, and value independent.
- Support mixed motives and unknown beneficiaries.
- Do not equate service to others with low value.
- Do not equate exhaustion with a poor choice.
- Distinguish “No perceived return” from “Return has not appeared yet.”
- A count-based chart must say it counts recorded events. It must not be labeled a percentage of total mental effort.
- If estimated time or effort allocation is later introduced, disclose how it was obtained and what remains unrecorded.
- Imported conversations are a selected sample, likely emphasizing difficult events. Audit language must not present them as a complete account of the user's life.

## 10. Apple Health and optional Watch-related observations

### 10.1 Role in the product

Health data supplies recovery context and possible associations. It does not independently determine the psychological burden of an event.

Use available, authorized, sufficiently covered data rather than a simple “owns an Apple Watch” flag. A supported data source may exist without an Apple Watch; a Watch owner may have no usable samples for a particular interval.

### 10.2 Candidate metrics

| Metric | Proposed priority | Intended use | Limitation to show or account for |
| --- | --- | --- | --- |
| Sleep duration and timing | First health prototype | Compare with the user's recent pattern | A shorter night has many possible explanations |
| Recorded awake periods | Secondary | Describe sleep continuity when supported | Coverage and source definitions vary; absence is not proof of uninterrupted sleep |
| Heart rate near a known event or discussion | Exploratory | Show available samples in the relevant window | Background sampling is intermittent; activity matters |
| Overnight heart rate | Secondary | Recovery context across comparable nights | Not the same metric as daily resting heart rate |
| Resting heart rate trend | Secondary | Personal longitudinal context | Not an event-specific stress measure |
| HRV | Later or exploratory | Compare like-for-like observations over time | Metric, sample duration, source, and context must remain comparable |
| Steps and workouts | Supporting context | Help interpret movement-related heart-rate changes | Not a direct measure of mental burden |
| Respiratory rate and wrist temperature | Deferred | Broader context when useful | Nonspecific changes; not direct mental-load inputs |

Do not prioritize blood oxygen, ECG, or sleep-stage percentages as a simple mental-load score in this prototype.

### 10.3 Sleep association flow

1. Identify a known event or conversation time; do not use import time as a substitute.
2. Identify the relevant sleep episode, accounting for the user's schedule rather than assuming midnight boundaries.
3. Compare with an available personal baseline from comparable data. The baseline window and evidence threshold remain research decisions.
4. Present an observation: “Sleep was shorter than your recent pattern after this discussion.”
5. Optionally ask: “Do you think this affected your rest?” with “Yes,” “A little,” “No,” and “Not sure.”
6. Store the answer as a self-reported association, separate from the sensor observation.

A single poor night may make an event worth reviewing. It must not automatically establish that the event caused poor sleep or increase a supposedly objective psychological severity score.

### 10.4 Interpretation constraints

- Distinguish the night before an event from the night after it.
- Consider available context such as activity, travel, illness, alcohol, or an unusual schedule without making a mandatory questionnaire.
- If several events precede one poor night, do not allocate the entire sleep difference to every event.
- Compare individuals with their own relevant history, not a universal stress threshold.
- Do not blend different HRV definitions or different sources as if interchangeable.
- Handle overlapping sleep sources without double-counting duration.
- Show insufficient baseline, incomplete coverage, delayed sync, and absent samples explicitly.
- Do not imply a real-time reading exists at the moment the user types.
- If the event time is unknown, omit event-window heart-rate claims.

## 11. Capability separation and fallback states

AI and health capabilities are independent. The prototype must demonstrate all four combinations:

| Generative AI | Usable health data | Required experience |
| --- | --- | --- |
| Available | Available | Assisted summarization and matching, plus optional recovery observations |
| Available | Unavailable | Assisted event workflow and audit without health panels |
| Unavailable | Available | OCR/text capture, user-selected event organization, deterministic audit, optional recovery observations |
| Unavailable | Unavailable | Complete capture, event timeline, user assessments, and deterministic audit |

### 11.1 AI rules

- Detect actual runtime capability; do not infer availability solely from country, language, or hardware name.
- Distinguish model unavailable, not ready, processing failed, and unsupported input where possible.
- Preserve the user's draft when inference fails.
- Never silently fall back from local processing to a remote service.
- A separately shipped on-device model is an optional research path, not an assumed fallback.
- If cloud processing is later offered, require explicit opt-in and communicate which selected content will leave the device.
- AI may suggest summaries, matches, and questions. It must not silently create confirmed impact or causal labels.
- Local model availability does not guarantee that every mental-health-related request will be supported; refusals and unsupported tasks need graceful handling.

### 11.2 Health rules

- Request only relevant data types when the user enables the corresponding feature.
- Avoid claiming to know that read access was denied when the platform only returns no readable data.
- Use neutral empty-state copy such as “No usable sleep data is available.”
- Missing health data must not reduce event importance or prevent audits.
- Deleting or disconnecting optional health context should leave the user's event record usable.

### 11.3 Apple availability note

The discussion referenced mainland-China limitations and iOS 27.3. Apple has announced a staged mainland rollout of some system features, but that announcement does not itself establish third-party access to the local AFM on each device/build. The exact regional/model behavior remains an implementation verification item. This prototype must work regardless of that outcome.

## 12. Screen requirements

| ID | Screen | Essential content | Essential variants |
| --- | --- | --- | --- |
| P01 | First use / Today | Product promise, import screenshot, paste text, recent events | Empty; returning user; optional health context absent |
| P02 | Import review | Selected sources, extraction progress, readable text, remove/reorder controls | Single image; overlapping batch; partial OCR; failure |
| P03 | Event preview | Title/excerpt, summary when supported, source evidence, match candidate, impact chips | AI available; no AI; ambiguous speaker; uncertain match |
| P04 | Events | Search, latest state, meaningful timestamps, filters | Mixed ongoing/resolved events; empty search |
| P05 | Event detail | Timeline, current assessment, recurrence evidence, corrections, optional tools | Progress; renewed concern; reopened event; unknown time |
| P06 | Weekly audit / Trends | Key observation, allocation, recurring events, worthwhile commitments, evidence coverage | Sparse data; adequate data; recording frequency changed |
| P07 | Recovery association | Observed sleep change, baseline context, source, optional association question | Insufficient baseline; several candidate events; no data |
| P08 | Settings and data controls | Processing mode, health integration, reminders, source retention concept, export/delete | Local model unavailable; health data unavailable; optional remote processing disabled |

### 12.1 Today wireframe direction

```text
HPU                                      Import +

What is still on your mind?

[ Import screenshots ]     [ Paste a conversation ]

ONGOING
Project scope change
3 conversations across 5 days
Latest update: Feeling somewhat clearer

Family commitment
High effort · Still worthwhile

THIS WEEK
Temporary requests appear in several ongoing events.
Review the evidence ->

Today          Events          Audit          Settings
```

### 12.2 Event detail direction

```text
Project scope change
First known discussion: Monday · Updated today

CURRENT STATE
Still on my mind, but less than earlier this week

TIMELINE
Monday       First discussion with a friend
Tuesday      Considered options with an AI assistant
Thursday     Concern returned; focus affected
Friday       Clarified the delivery scope

RECOVERY CONTEXT                           Optional
A related night was shorter than your recent pattern.
Relationship to this event: Not confirmed

[ Add update ]   [ Set aside ]   [ Review options ]
```

## 13. Audit and trend requirements

### 13.1 Weekly audit structure

1. One concise observation supported by the available records.
2. Allocation across personal priorities, work roles, others, and shared goals, with an honest denominator.
3. Events that continued to occupy attention.
4. Demanding commitments the user still found worthwhile.
5. Changes in willingness or perceived return where actually recorded.
6. Optional recovery observations presented separately.
7. One optional next-week adjustment.

Each interpretation should link to evidence and offer “This does not fit my experience.” A disagreement should allow correction rather than forcing the user to accept the model's framing.

### 13.2 Trend concepts

- Active and user-resolved events over time.
- Distinct episodes and days with reported impact.
- Changes in the same event's user-reported attention demand.
- Perceived value and willingness across recorded commitments.
- Optional sleep patterns alongside event activity, without causal wording.
- Outcomes of previously selected adjustments.

Show recording coverage and significant changes in capture frequency. A quiet recording period must not automatically appear as improved wellbeing. Sparse data should produce a modest summary rather than a confident pattern claim.

## 14. Visual design, language, and accessibility

- Use a restrained neutral palette, strong typography, clear hierarchy, and generous spacing.
- Use color to indicate categories or attention cues, not moral worth.
- Support dark-mode exploration without making a terminal-like aesthetic mandatory.
- Favor simple timelines, bars, and lines over dense gauges or decorative dashboards.
- Support readable text sizing, accessible contrast, reduced motion, and non-color indicators.
- Keep optional haptics subtle; never make them necessary for understanding.
- Use engineering metaphors sparingly. Everyday actions should remain easy to understand.
- Avoid scolding, forced positivity, hostile descriptions of other people, and personality diagnoses.

Preferred copy includes “Review the evidence,” “Still on your mind?”, “Related event?”, and “Save for later.”

Avoid copy such as “Your responsibility is only 15%,” “External garbage processes are draining you,” or “This event caused your sleep loss.”

## 15. Privacy and user control

Conversation imports may contain sensitive information about both the user and third parties. The design should make processing and retention understandable without interrupting every ordinary action.

- Use user-selected imports; do not imply unrestricted access to chat apps or the photo library.
- Show a clear local-processing explanation where accurate.
- Provide controls to remove individual images, text passages, and an entire event.
- Allow user correction of summaries and associations.
- Include an original-source retention concept in Settings; choose the final default after review.
- If originals are removed, retain an honest indication of which evidence remains available.
- Keep remote processing off unless explicitly enabled.
- Define deletion and export behavior for derived summaries and associations as well as source material.
- Keep optional health setup out of the first successful import journey.
- Show discreet reminder previews that do not expose sensitive event details by default.

## 16. Prototype fixtures and review scenarios

Use synthetic conversations and synthetic health observations. Clearly label all fixture data and simulated processing; do not use real private chats for the prototype.

| Scenario | What the prototype must demonstrate |
| --- | --- |
| A. First import after talking to a friend | Useful preview without rewriting the story or enabling Health |
| B. Three screenshots with overlap | One coherent episode without inflated recurrence |
| C. Another conversation about the same project | Suggested match, explicit confirmation, updated timeline |
| D. A similar conversation about a different project | User can reject the match and create a separate event |
| E. No local model available | OCR and event organization still work without pretending to summarize |
| F. No Watch and no usable health samples | Core event and audit flows remain complete |
| G. Short sleep after a discussion | Observation shown; event attribution remains unconfirmed |
| H. Several events before the same short night | No duplicated full attribution to every event |
| I. Late import of an old screenshot | Import time is not used as the event's physiological window |
| J. Repeated discussion brings relief | Recurrence increases while latest subjective impact can decrease |
| K. A quote from a friend or AI | Opinion is not converted into an established fact |
| L. Fewer imports this week | Audit marks limited coverage rather than claiming recovery |
| M. User follows an HPU reminder | Opening the event does not itself count as renewed distress |
| N. Local generation fails mid-import | Draft survives; user can save or retry without cloud fallback |

## 17. Prototype acceptance criteria

- **AC01:** A first-time user can reach a saved event through screenshot import without retyping the account.
- **AC02:** The preview exposes the source and allows a meaningful correction.
- **AC03:** A multi-screenshot conversation does not automatically become multiple recurrences.
- **AC04:** Appending to an existing event is reversible through episode separation or correction.
- **AC05:** The no-AI/no-health route reaches a usable event timeline and audit concept.
- **AC06:** No screen equates missing sensor data with low psychological impact.
- **AC07:** The sleep association flow distinguishes observation from user-reported attribution.
- **AC08:** Unknown event time prevents a false event-time heart-rate claim.
- **AC09:** Charts disclose whether they show event counts, user reports, or device observations.
- **AC10:** Audit findings are supported by inspectable evidence and can be disputed.
- **AC11:** Repeated discussion can coexist with improvement in the latest assessment.
- **AC12:** A user can save and exit without answering optional questions.
- **AC13:** Model unavailability or failure never silently enables cloud processing.
- **AC14:** Privacy, deletion, and correction controls are discoverable in the proposed navigation.
- **AC15:** All four AI/health capability combinations are represented in design review.
- **AC16:** Prototype fixture data and simulated capabilities are clearly identified.

## 18. Validation priorities and delivery sequence

### 18.1 Questions to test with users

- Does importing existing material feel sufficiently easier than retelling the event?
- Is the first event card useful before any weekly history exists?
- Can users correct a poor summary or match without starting over?
- Do users understand the difference between repeated discussion and continued distress?
- Does a weekly audit reveal something useful beyond the original friend/AI conversation?
- Does health context add useful understanding without encouraging unsupported attribution?
- Does the fallback experience remain valuable without automatic summarization?

Measure time to first useful saved event, completion, correction burden, match acceptance and reversal, perceived usefulness, and voluntary return. Initial speed targets are hypotheses to establish through testing, not promised OCR or model latency.

### 18.2 Proposed sequencing

1. Import, source review, event preview, and timeline; cover both AI and no-AI states.
2. Recurrence interpretation, allocation/value dimensions, and a transparent weekly audit.
3. Optional sleep-context flow and no-data variants.
4. Broader physiological observations only after baseline, sampling, and interpretation questions are resolved.
5. Additional intervention tools and model backends after the core value is demonstrated.

## 19. Technical reference notes

These references informed the discussion. They are not proof that every capability works on every target device or regional build. Recheck owning documentation and test real devices before implementation commitments.

- [Apple Vision: Recognizing text in images](https://developer.apple.com/documentation/vision/recognizing-text-in-images) — device-side OCR independent of the proposed generative summary workflow.
- [Apple: Share extensions](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Share.html) — user-initiated receipt of shared text and attachments.
- [Apple Foundation Models: Generating content and performing tasks](https://developer.apple.com/documentation/FoundationModels/generating-content-and-performing-tasks-with-foundation-models) — availability checks and fallback experience.
- [Apple Foundation Models: Model availability](https://developer.apple.com/documentation/foundationmodels/systemlanguagemodel/availability-swift.property) — runtime availability interface.
- [Apple mainland-China rollout announcement](https://www.apple.com.cn/newsroom/2026/10/apple-intelligence-features-are-coming-to-users-in-china/) — system-feature rollout context; does not establish the exact third-party local-model capability required here.
- [Apple HealthKit: Authorizing access to health data](https://developer.apple.com/documentation/HealthKit/authorizing-access-to-health-data) — granular access and limits on inferring read-permission status.
- [Apple HealthKit: Sleep analysis values](https://developer.apple.com/documentation/healthkit/hkcategoryvaluesleepanalysis) — sleep sample meanings and coverage considerations.
- [Apple HealthKit: HRV SDNN](https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/heartratevariabilitysdnn) — metric definition; different HRV measures must not be blended.
- [Apple Watch heart-rate technical overview](https://images.apple.com/my/health/pdf/Heart_Rate_Calorimetry_Activity_on_Apple_Watch_November_2024.pdf) — sampling context and limitations.
- [Apple: Overnight vitals](https://support.apple.com/en-ie/120142) — personal context and factors that can affect physiological observations.

## 20. Requirement traceability

| User need | Relevant sections |
| --- | --- |
| Avoid rewriting a conversation already shared with a friend or AI | 1, 7, 12, 16 |
| Screenshot OCR and local summarization | 7, 11, 19 |
| Mainland/model capability separation | 2, 11 |
| Evaluate mental-effort demand | 8, 9 |
| Recognize repeated discussion of one event | 6, 8, 16 |
| Explore sleep and heart-rate associations | 10 |
| Preserve a complete experience without Watch hardware | 10, 11, 17 |
| Show self/other allocation and low perceived return | 1, 9, 13 |
| Provide recurring audits and trends | 13 |
| Keep the current phase at design and requirements | Document control, 4, 18 |
