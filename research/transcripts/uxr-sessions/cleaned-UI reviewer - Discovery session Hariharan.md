# UI Reviewer — UXR Discovery Session: Hariharan SV
**Date:** 21 August 2026

## Participants

| Name | Role / Title | Organisation | Side |
|---|---|---|---|
| Ankit Anand | Designer / Interviewer | IBM | IBM |
| Mridusmita Nath | UX Researcher | IBM | IBM |
| Hariharan SV | Frontend Developer | webMethods / Integration team | Participant |

---

**Ankit Anand:** Alright, okay. Could you just quickly tell me about how long you have been working in webMethods integration and what does your role exactly look like?

**Hariharan SV:** Okay, so I have been around 2 and a half years. And mostly I will be working on the front end tasks — I could say like 70/30, so 70% it is front end and 30% it is back end.

**Ankit Anand:** Okay, so you joined right after the acquisition or right before the acquisition?

**Hariharan SV:** It's like before the acquisition.

**Ankit Anand:** Okay. Okay, alright, so the first bit that we will try to cover is the implementation process. So can you walk me through what you do when you receive a Figma design to implement? You can start from when you first open the file — like what happens next and how do you understand what is in the Figma file and what are the gaps, anything like that.

**Hariharan SV:** Okay, so when I first receive the Figma file, I will be comparing it with the current existing UI. So I will identify the delta and based on it, I will be starting implementing from top to bottom kind of approach.

**Ankit Anand:** Yeah. And how do you see which component has been used, or which kind of tokens, typography, icons — all of those things — have been used in Figma? How do you sort of bring that into actual implementation?

**Hariharan SV:** Okay, so for me — I mean, I faced issues with identifying the numbers only — like to identify the space that has been left relative to the parent component. So I could identify the colours, the size — these things — just the spacing part, it's like difficult to identify.

**Ankit Anand:** The spacing part you are saying.

**Hariharan SV:** Yeah, with respect to the parent component. So it's like, let's say we have a card and within this card we are having — let's say — an SVG, and to identify — I mean, if it is displaced from this parent div — I mean, how many pixels it's been to the left and to the top.

**Ankit Anand:** Okay. And what about the components that have been used?

**Hariharan SV:** Okay, by looking at it, I won't be able to — in some cases I can, but in some cases I can't. So for example, if it is with respect to icon names, right? So we in general have an in-person discussion. That's when I navigate to the IBM Carbon icon site and I will identify the icons. So sometimes the in-person discussion helps me to particularly identify the icons.

**Ankit Anand:** Okay. Okay, so let's say that there is an accordion or let's say there is a side panel or a button to be used. How do you understand which component it should be? Or do you use Carbon components in your implementation, or you are coding that component from scratch almost?

**Hariharan SV:** Okay. At the time of side panel development, I had coded it from scratch — this accordion part, the folder structure — everything from scratch. So I did not use the Carbon component at that time.

**Ankit Anand:** Has that changed over time? So I think that was sometime back, but I'm also trying to —

**Hariharan SV:** Okay, I haven't like followed up on this part.

**Ankit Anand:** Okay, so you're not using Carbon components in the current workflow at all.

**Hariharan SV:** As far as I know — in some places I am able to find the Carbon components, in some places I didn't. It's like a mix.

**Ankit Anand:** Okay, do you mind sharing your screen probably and open up a Figma file and tell me how you read the Figma file itself?

**Hariharan SV:** Okay.

**Ankit Anand:** Yeah.

**Hariharan SV:** Yeah, Ankit, so in this case, what I had is — we have a side panel and I will be comparing the delta. So currently how the side panel looks like and what do we have in this mockup, and I will compare the delta — what should we add now and what should be removed — and like that, I will be implementing the changes.

**Ankit Anand:** Okay, so and you are doing this in this mode only — do you leverage dev mode?

**Hariharan SV:** Last time when I requested for dev mode, they told in this bucket we couldn't accommodate me, and after that I haven't checked on it.

**Ankit Anand:** Okay, can you try to move to the dev mode in the bottom panel? Like there is a code icon right in the bottom panel, center bottom panel.

**Hariharan SV:** Yeah.

**Ankit Anand:** Okay, you have to request. Okay, ideally — yeah, that is one of the fundamentals of dev mode. I think without dev mode it is absolutely impossible to get the right components and get all of these kind of information. Okay, so — okay, alright, sorry, just give me a second, I lost my —

**Mridusmita Nath:** I would — I have a question. So Hariharan, how do you search for a component when you get a Figma file?

**Hariharan SV:** So basically I identify the components with the in-person discussion — in general meeting with the UX people only.

**Mridusmita Nath:** So suppose this is a Figma screen you have received. So next step would be to meet them in person and they will individually tell you — each of the links — say this is the list, this is the data table. Is it like that, or how is it done?

**Hariharan SV:** In general, I had the idea based on these meetings only.

**Mridusmita Nath:** Yeah, but do you receive the correct link — that this is the list component you have to pick from storybook? Okay.

**Hariharan SV:** Yeah, I had received the links, yeah.

**Mridusmita Nath:** Okay. And the next step would be you will receive the link and you will use that to implement your design.

**Hariharan SV:** Okay, so in our Angular codebase, currently we are not using the Carbon web components, so we are trying to provide the same kind of experience with the existing modules — I mean the PrimeNG modules we had. So for this inline reference data editor, we didn't use the Carbon component. We provided the similar kind of experience. I mean, yeah.

**Mridusmita Nath:** Okay, you tried to match it visually, but in the code they are not Carbon web components — they are like some third party. Is it?

**Hariharan SV:** Yeah. Yeah.

**Mridusmita Nath:** Okay. But why are Carbon web components not — we may not know, but I just know that these web components are framework agnostic — whether React or Angular, you can use web components. What is the challenge in our case?

**Hariharan SV:** Okay, I think the developer effort only. So we need to spend a significant amount of time to utilise these — I mean, rewrite all these components.

**Mridusmita Nath:** Okay. Okay, even when the web component is available, still you have to rewrite.

**Hariharan SV:** Yeah, we need to rewrite.

**Mridusmita Nath:** Okay. Alright, yeah, Ankit, I think we can move to the next section of reviews.

**Ankit Anand:** So I was — there is another question here: which information, if any, is typically missing or unclear in a design file that makes implementation harder for you?

**Mridusmita Nath:** Yeah.

**Hariharan SV:** Okay, so in this case, I could — I mean, take an example. So here — so the side panel part — right, maybe a few more details. Like if it is a private runtime owned by current user, private runtime owned by other user — I mean, a little more context will be helpful. Yeah, if we look in depth, I could understand — okay, so this content refers to this use case, it refers to a different use case.

**Ankit Anand:** Okay, so alright, so there is a component list on the left side of the Figma file — no, in this Figma page itself, if you scroll to the left side — can you scroll on the main canvas?

**Hariharan SV:** Yeah. Okay, on the main canvas, okay, yeah, I had seen this part as well, yeah.

**Ankit Anand:** Yeah. So the component states and when a certain thing is happening — something that is highlighted — are you talking about something different? That is what I am trying to understand.

**Hariharan SV:** Hey, this part — it is like mentioning about the particular scenario. So let's say if it is a section of a side panel — yeah — and here it is the whole mockup.

**Ankit Anand:** Correct.

**Hariharan SV:** So instead if it's like a — just a second. So I believe what I am slightly able to make sense is the file organisation is probably not as right as it would make life easier for you, or easier to reach.

**Hariharan SV:** Like a hierarchy could have been better, yeah — private runtime owned by current user and then owned by different user. So this is an example only — I couldn't correlate with this mockup, yeah.

**Ankit Anand:** All right, thank you. I will move to the next section which is around the review and the release side of things. So what does a review look like within your team or for you specifically? Like, who initiates it? Who is responsible for it? What do they look at? How is feedback received? All of those things.

**Hariharan SV:** Okay, so we mainly focus on the code quality part. So what happens is — we check if the functions are being duplicated or if it is not properly reused and we could reduce the complexity — and all these main requirements that have been mentioned in the refinement, are they captured?

**Ankit Anand:** Okay.

**Hariharan SV:** So that's — I mean, that's what in general happens in the code review, yeah.

**Ankit Anand:** Okay, so there is no UI review as such that is happening.

**Hariharan SV:** UI. Just a second, Ankit. Yeah, let me recollect. Yeah, I mean, I am not getting you — can you please elaborate? No, I mean, what kind of checks are you expecting in a UI review?

**Ankit Anand:** No, I am just meaning — so for example, we got to know from another developer that even QA, they sort of assess the implementation from a Figma file as well. Is that — so that would be one kind of review, right? Another would be probably something within your team also, before the code gets moved or I think merged is the way, right? It is evaluated. But there it is only code health, you said, right? Like — what did you say? — I forgot — code quality. Yeah. So that is the only evaluation that is happening within your team.

**Hariharan SV:** Yeah, code quality here.

**Ankit Anand:** No UI review.

**Hariharan SV:** So you were expecting — I mean — the mockups and the current code, are they matching — that kind of UI review?

**Ankit Anand:** Yeah. Is that happening at all?

**Hariharan SV:** No, currently it's not.

**Ankit Anand:** Okay, all right. And does the QA team do anything along those lines?

**Hariharan SV:** Yeah, so once the code changes are merged, QA compares the designs and they will be telling — so in this use case, this component is not coming up.

**Ankit Anand:** Okay, and then you will be addressing that — resolving that.

**Hariharan SV:** Yeah.

**Ankit Anand:** Okay, all right. Mridusmita, do you have any questions here?

**Mridusmita Nath:** No, I'm good.

**Ankit Anand:** Okay, all right. So if there was a magical way that existed in the world, right, to help you understand or get the Figma file, right, and then to help you facilitate the implementation — what would it be?

**Hariharan SV:** Okay, so I haven't explored the Figma dev mode, so maybe — once I receive access, I will check on that part. Currently, what I heard is we have this Figma MCP which we could connect to Bob and we could implement the UI changes, so that part I meant to explore.

**Ankit Anand:** Okay. All right, and so if there was a way to get automated compliance feedback — come Carbon or UI both — during the implementation, what would you want it to tell you, and when? What would you want it to tell you?

**Hariharan SV:** So I am not getting you.

**Ankit Anand:** Okay, so if there was a way to get sort of an automated Carbon compliance, or like a UI review sort of automation, or like a skill or like a tool right during the implementation — what would you want it to tell you that would be great, or if it could evaluate this particular thing.

**Hariharan SV:** I think I have heard of this part. So there is a skill that actually evaluates — I mean, to get the styling part from the Figma. So maybe we could utilise it by connecting with the UHS which we had already done, and comparing with Figma and identifying the delta.

**Ankit Anand:** Mhm. And when would you be using that? Is there a particular time in your workflow of implementation when you would like this to be leveraged?

**Hariharan SV:** The compliance checker.

**Ankit Anand:** Yeah.

**Hariharan SV:** Okay, let's say I had received like 23 screens for a feature. So what I will in general do is I will take a snap and I will paste it in Bob and ask it to generate the output. So in general, what happens is it doesn't generate the component like — pixel to pixel — the pasted screenshot and the actual dropdown won't match. So these kinds of differences arise. So it will take 2–3 iterations. So I will be manually checking if it is matching the Figma mockup and maybe after my check, I want this compliance check to run.

**Ankit Anand:** Got it, okay. Okay, I'm on to the last question, which is: what is the most frustrating part of the design to implementation workflow for you?

**Hariharan SV:** Okay, I mean — I don't think I have — I mean, I have been frustrated by implementing the design. So yeah — sorry, I had personally faced it once. So what happened is while implementing the side panel, the data table component — while implementing from scratch. So if I am going to implement it from scratch, this experience — at that time I felt — yeah.

**Ankit Anand:** Sorry, I did not catch that clearly. So when you were implementing the side panel or the data table component from scratch, it was frustrating because you couldn't get the details?

**Hariharan SV:** Like — I couldn't make it fix up perfect. So I wanted the line to be in a different style. I wanted the whole accordion to be having data table in a different format. So while implementing it from scratch, right — I mean, it took a lot of time, yeah.

**Mridusmita Nath:** So at that time you didn't use a third-party data table.

**Hariharan SV:** No, at that time I was using a custom implementation, not the Carbon implementation.

**Mridusmita Nath:** Okay, no — for customer said no, you get the third party and you make it look like Carbon colours. So.

**Hariharan SV:** So at that time, I mean, we couldn't find the similar third-party thing, so I had to implement it from scratch.

**Mridusmita Nath:** Okay. Understood. Okay.

**Ankit Anand:** Okay, if you do not have any other question, I think we can close. Do you have anything you want to tell us — anything that we couldn't cover? Have you heard it?

**Mridusmita Nath:** No, yeah, we can close it. Yeah.

**Hariharan SV:** Yeah, Ankit, so I want to know about this Figma dev mode only. Is it like approved? I mean —

---

<!-- Corrections & Flags -->
<!-- Corrections: "web method integration" → "webMethods integration" (MISHEARINGS table: webMethods) -->
<!-- Corrections: "in person discussion" → "in-person discussion" (hyphenated compound adjective, clarity) -->
<!-- Corrections: "death mode" → "dev mode" (mishearing of Figma Developer Mode, context clear) -->
<!-- Corrections: "Ritu" → "Mridusmita Nath" (nickname used by Ankit at 15:02; mapped to full name for consistency) -->
<!-- Corrections: "PrimeNG" — kept as-is; likely correct reference to Angular UI component library -->
<!-- Corrections: "UHS" — FLAG: unclear abbreviation at 17:34; possibly "UX", a tool name, or a mishearing; left as-is -->
<!-- FLAG: Participant did not have Figma dev mode access at time of interview — key context for implementation gaps -->
<!-- FLAG: "Ankit stopped transcription" appears mid-interview at line 11 of source — likely a transcription system artefact; no content appears to be lost -->
<!-- FLAG: Session ended abruptly — participant asked about Figma dev mode approval but transcript cut off before resolution -->
