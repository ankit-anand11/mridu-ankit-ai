# UI Reviewer — UXR Discovery Session: Sahana S
**Date:** 21 August 2026

## Participants

| Name | Role / Title | Organisation | Side |
|---|---|---|---|
| Mridusmita Nath | UX Researcher / Interviewer | IBM | IBM |
| Ankit Anand | Designer | IBM | IBM |
| Sahana S | Frontend Developer | webMethods / Integration team | Participant |

---

**Mridusmita Nath:** All right, so Sahana, I will just quickly tell you how we have structured the interview for your knowledge. So first section, first few questions will be around implementation, right? What happens? What is your journey like after you receive a design file? And then second part would be something around reviews and corrections. How does that happen in your team or what, how is your experience so far? And in the last section, we will just wrap up with a few feedback and comments we are eager to know from you. Okay, so yeah.

**Sahana S:** Okay. Sure, thanks. Sure. So coming to how a developer or me after we receive a design, right? We do have — can I share my screen of the Figma file?

**Mridusmita Nath:** Yeah. Sure.

**Sahana S:** Is it visible? Yes, there is a topic. Okay, so we do have — first is having a developer access is helpful and this is something that is insightful: it shows which component from Carbon is used in each of the design. Okay, be it — I mean, in high level, we won't be knowing from where it is coming from because Carbon is divided into 3 to 4 files, right? Because IBM products, Carbon reactor products and all that. So this is something that helps us to know what it is, which component is used in the Figma and we go ahead with it and this is how we do it. Okay, this link doesn't help much because it opens in Figma itself, but the name does help.

**Mridusmita Nath:** Mhm. So yeah. What do you do after that?

**Sahana S:** I mean, it doesn't take us to — it doesn't take us to the Carbon though, it takes us to Figma address, but we do have certain bookmarks for Carbon React and all that where we go here and search the component or check what are the — say, for example, data table itself — check what are the attributes. So it is a list of attributes that gets listed here. Okay, we check on that. Yeah, each of them have component APIs which will help us to know what it is. Say if this is title or subtitle it has to be added or this is how we study it.

**Sahana S:** And if the storybook doesn't help, I do reach out to Ankit to share the expected documents which at times we would not have. And these documents give all the alternative uses and rules to be followed by the Carbon component.

**Mridusmita Nath:** Okay, so you go through them in detail — like how a component should be applied. Nice.

**Sahana S:** So that would be yes. Yes, I mean this again was what even Ankit would be referring and he is designing it, right — like the spacing or say the colour, text or size of it, so all this will be part of the documentation of the design system.

**Ankit Anand:** Just an additional question here, right? So even when I am designing, right, there are certain places where I have detached the component — for example, the options style that is used there, right, for client applications — where the suite itself right now that I have broken that component, so I'm sure you wouldn't be able to get —

**Sahana S:** It does show it here, though. Most of the time it does show it here. See, clicking on it would not come up, but the hierarchy here would still show the name of it — option time — Carbon for IBM products. So this is not the one where I have to go to. This is Carbon React. So we have another place for that itself.

**Ankit Anand:** Okay.

**Mridusmita Nath:** Got it.

**Sahana S:** I do have a problem for IBM products. This is the doc I opened. Yeah, yes.

**Mridusmita Nath:** Okay, you inspect the layers to find out, okay.

**Sahana S:** Yeah. One thing that would be good is this link would take us to the storybook rather than Figma itself. But I think it is more beneficial for a designer than a developer. I don't know how this — designed it goes to Figma itself and it gives you this which is not that helpful for us. Yeah, but we do get the name.

**Ankit Anand:** Is there the view document? Can you go to the library? Does the view documentation on the right side take you to the exact documentation of that component?

**Sahana S:** No, it takes you to the code — where there's okay, this is it — it just gives the same Carbon for IBM products. I mean you have to scan, yeah, storybook — then to go to storybook — code again gives you the insight of how it can be added in the code structure, like how it can be written. But here is the storybook link. So it is like 3 times navigated to get there.

**Mridusmita Nath:** Mhm. Okay. Got it.

**Sahana S:** One other thing that I have faced is with respect to the colour icons — as of now, which even till date I have not found the library for it. I think Tala might be knowing that and he had updated it. So let's verify — this thing that I was referring to is for the runtimes or for the apps that we add, right? At present — let me show that — these icons is so anything with respect to the icons — it's a bit difficult to like navigate and find the source of this.

**Mridusmita Nath:** Mhm. Got it. I was just coming to this question — what kind of information is generally missing or unclear, right, while you are inspecting a file or trying to find out — yeah, what stops you from doing accurate implementation?

**Sahana S:** Yeah. And one more thing which we would like is also to let us know what is the behaviour — maybe with an annotation or anything — like what would be the behaviour if you hover over that object. Sometimes we will use the default hover method of Carbon.

**Mridusmita Nath:** Mhm.

**Sahana S:** For a button, if you hover the colour changes — it's all Carbon — but at times it would be customer-specific behaviour integration itself. Say, for example, our client application page — at places it is mentioned by the designers, but also there are one or two places where it could have missed, and they have reached out for in the follow-up review of what has to be done for the hovering. See, if you hover over the string compat, it is a link, right? So such cases would be better to add what it has to be done. And this was the recent comment that I have got, for variables, so the smaller ones. Apart from that, everything is smooth to navigate and develop.

**Sahana S:** And things like this also — where at times this item can be a popover, or — there are 2 things. There is a toggle tip and there is a tooltip. Toggle tip is with respect to clicking on it and displaying; tooltip is just hovering over it. So that information would also be helpful — what has to be added.

**Mridusmita Nath:** Okay. So when you face situations like this, or even the icon example that you gave us, or it could be any other — what is your next step then? How do you navigate through this roadblock?

**Sahana S:** Usually check with the designer — and till date I have worked with Ankit alone, so I have checked with him and then check internally with the other UI developers if they have worked on it and used it. I mean, majorly before that, first I would check in the code base if anywhere else it's been used, and if I don't find any implementation of it, then the next is the designer and then.

**Mridusmita Nath:** Okay. So in case of custom components, what do you do then?

**Sahana S:** Till date, it's been the Carbon components itself, but custom validations — so say — the most validation that a Carbon component has done till date that I have seen is with respect to these dropdowns for any integration runtime, right? It has been bombarded with so many validations that we would have written a custom validation for it, which would not be ideally supported by Carbon, like here itself if you see. It also includes typing and gives an error, then also validates what has been typed and all this — like it has a create virtual button on top of this combo box itself. So that way, apart from that, custom components are lesser that's been used. One custom component which we constantly use is for the tooltip. Sometimes our Carbon tooltip CSS or the alignment would not work with the existing components.

**Mridusmita Nath:** Mhm.

**Sahana S:** I think that's how the tooltip actually works. I guess at that point of time we add our custom tooltip data into it. Say we have to add tooltip inside the dropdown of this component — it's all our custom tooltip that we have added. For the design time and all that, right? We have a tooltip right for that.

**Ankit Anand:** I have one question here. So component is one thing. There are also tokens for colours, typography, and actually spacing as well, which I have honestly not used in Figma designs for sure.

**Sahana S:** No.

**Ankit Anand:** But colour and typography tokens I have been able to do it more or less consistently. So I am curious to understand — are you, in the implementation also, are you able to leverage the Carbon tokens for colours and typography and spacing?

**Sahana S:** Yeah, most of them already converted, and while doing the Carbon transformation that happened, the codes are already defined, so we need to use that internally. We used the Carbon components itself. So good.

**Mridusmita Nath:** Okay.

**Sahana S:** And at places we do use hex codes now and then, so it is rarely, but yeah.

**Mridusmita Nath:** So what is the situation that leads to the usage of hex codes?

**Sahana S:** It would be a bit time saving, but also we wouldn't have found the exact code for the colour and we would have proceeded with the hex code. It would be mainly for the backgrounds — say the error background. I don't have anything in this — yeah, an error background which has to show this colour, right? The background colour — I am just showing an example of the colour — such things. Yeah, we do use the hex code. But it would be an indirect match itself. There would be no mismatch with respect to the hex code.

**Mridusmita Nath:** Okay, it's interesting.

**Ankit Anand:** But I don't think spacing is a token based variable, right? You would be hard coding the spacing.

**Sahana S:** No, yes, we do that with padding and margins, the CSS part.

**Ankit Anand:** Got it, okay.

**Sahana S:** So here also it is the same thing that gets shown.

**Mridusmita Nath:** So you inspect the design file and then apply the same spacing.

**Sahana S:** Yeah, just to be sure, yes, sometimes it would not have applied on its own like the default one, or we would just check it once to be sure that it is not off by 2 pixels.

**Mridusmita Nath:** Okay. And why are you not using Carbon spacing tokens?

**Sahana S:** Of Oddspace — these spacing, right? It's showing the spacing 03. I think that's — currently it's been a habit to use padding. So just.

**Mridusmita Nath:** Yeah. Okay. All right, we can move to the reviewing part. So yeah, what does a typical UI review look like? Suppose the first level of implementation is done and you are almost ready — say this screen is done. Then in what way does UI reviews happen in your team? Who does the UI review? Who initiates it? And how is feedback shared?

**Sahana S:** We do a demo with the stakeholders and the managers. So this is a demo. I think even Ankit would have from UX also — we do ask them for their input as well, and if those stakeholders have any questions it would be directly addressed by the UX designer who would have initiated that design. Say, for example, there was a copy text on clicking of the runtimes, which was the most debated one — and at such places, yeah, they do question why there is a requirement of it and yeah, there is the gap between them.

**Sahana S:** Apart from that, it is mostly the smooth usage of it — say for instance, earlier too, we had missed adding — say when you click on apply — the applying part of it. So it does load as "applying." You see that "creating" and then it loads, right? The button loader. So we had not added the button loader and it was something that even John had mentioned — let's add that, it looks good. So we have added everything.

**Mridusmita Nath:** Yeah, that looked good. Mhm. Understood. And for smaller things like spacing and all, it is always like an eye scan only — that's what we all do. Just wanted to know if there is a different thing you are using here.

**Sahana S:** Yeah. No, it's more of an eye scan itself and either QA might find it or during our UX review we might find anything that is missed, or internally if anything is missed, we will just — QA also points out spacing issues, yes, at times. Those buttons or the spacing is different. Say, for example, from the developer's point of view — I have currently seen one open issue with the text vector delete button and a similar one which is eye-catching. Or else at times the border of this box will be a bit bigger, the bottom will be a bit bigger and aligning straight to the next dev.

**Mridusmita Nath:** So how does QA point out these kind of issues? Do they take a screenshot and add, or how is it communicated?

**Sahana S:** Yeah, with a screenshot — please show the difference.

**Mridusmita Nath:** Putting a circle or something like that, right, and raising a defect. Okay.

**Sahana S:** Yes, I mean it looks out of place or something like that.

**Mridusmita Nath:** Okay. And when defects are raised, are individual items raised as individual tickets or are they all spacing stuff together?

**Sahana S:** It is individual — with respect to say someone is testing in English or B2 BNT which came up in the second phase, right? Or say something else is broken with the English space — they would raise it while testing it, or outside the feature testing also if they come across anything, they will raise it from time to time.

**Mridusmita Nath:** Alright, Sahana, I am sorry, we are at time. Are you okay to extend a few minutes if you don't have a hard stop?

**Sahana S:** I did have to — I had other commitments for 12:30, I had to finish few screens. Yeah, it is also a call with Ankit.

**Ankit Anand:** It's okay if you can spare 5–10 minutes.

**Mridusmita Nath:** Just 5 more, yeah.

**Sahana S:** Sure — because currently the tenants have been unstable for a bit because a few deployments were happening and I might go ahead and move the meeting accordingly, but yeah, we can continue for a few.

**Mridusmita Nath:** Okay, maximum 5 to 7 minutes. Okay, alright, okay. We want to know a little bit around — have you ever shipped something you knew didn't match the standard, like while you're doing it, but circumstances — what kind of circumstances generally lead to non-compliant implementations?

**Sahana S:** I didn't get that — with respect to Figma designs or the UI implementation?

**Mridusmita Nath:** UI implementation — what are, most of the time, the circumstances which lead us to ship something which was not very Carbon compliant?

**Sahana S:** To not point — I mean, there's a point of more about the company now that we are implementing it, but say the newest screens — for example, I think in the demo call also there were a few modals which did not have a few of the Carbon buttons or things used, right? So it looks a bit out of place and that's when it gets raised — okay, this does not look Carbon compared with the buttons that are being used now.

**Mridusmita Nath:** No, the question was — what leads to those kinds of noncompliant things? Is it something that comes in Figma, or there is no time, or there could be multiple situations which lead us to that.

**Sahana S:** I think if the Figma is given — I mean, most of us will just see whether it is up to date with the Figma. So it would be more of when the design is very small and we implemented and produced it. I am not sure. But this not got such correctly, so I don't have any pointers.

**Sahana S:** But one review that I have got is with respect to copy text — okay, it comes with every release of English — the copy text, which is required to have a copy on click on the runtime, right?

**Ankit Anand:** So Sahana, just a follow-up question: Does QA also flag Carbon compliance issues at all? I don't think they would do that, but they would just flag anything.

**Sahana S:** No, they would flag with respect to the design that you have shared, right? What you have refined — given a refinement call, whatever we have done — either we produce the Figma file itself with them and they see that, okay, it is out of place.

**Mridusmita Nath:** Okay, they compare it with the Figma you are saying. Okay, all right.

**Mridusmita Nath:** Okay, all right, Sahana, now — let's say if there was no constraints and we could just automate the whole process, right — what kind of — how would you want — if there was a way to get automated Carbon compliance feedback during implementation, what would you prefer? How would you want it to tell you, while you are working, how you want it to flag the non-compliant parts of the implementation?

**Sahana S:** I think currently Bob has access to the Carbon MCP, right? So maybe we can leverage that to say that the current developed screens or anything — as far as the Carbon design goes — say for a data table if a custom data table is used in UI and it is not Carbon compliant, that can be found with respect to comparing with the help of Carbon.

**Mridusmita Nath:** Mhm. Okay, and you have been using Bob right for your UI implementations. And are you happy with the output? Like, has Bob deviated sometimes from Carbon?

**Sahana S:** No, it's most of the time it uses Carbon components, but there are one or twice — it is very rare — that there is an existing component in the screen that might be of older design before Carbon, so it might use that, and later if we say that it should use Carbon, just.

**Mridusmita Nath:** Sorry, I missed that. I didn't understand.

**Sahana S:** Also — say for example, this already has an integration runtime speed in deployment and most of the things are custom components — like this existing and all these buttons. For example, then sometimes the top same top-down design would have been used — say these — I mean, I am not able to zoom in, but this design is not as per the Carbon design specs. It would have used the same thing — leveraging, if I have to create another step here, if we have used the same thing which is existing in the previous step, if we have not mentioned to use Carbon, so we have to clearly state it. Yeah, but it depends on how well we prompt it. If you say to use Carbon — to test all the strictly.

**Ankit Anand:** But saying that it has to use Carbon ensures that Bob is able to comply and leverage the Carbon components, the typography tokens, the colour tokens — all of those things it is able to leverage and implement correctly.

**Sahana S:** Yes. Yes, with the MCP server which has the Carbon React — it does leverage it — it has access to all the docs and storybooks.

**Ankit Anand:** Wow, amazing. Okay.

**Mridusmita Nath:** Okay, I think we are almost at the end of it. Sahana, tell us — yeah, you are implementing day in and day out. What is the most frustrating pain point for you in this whole implementation journey, like from the point of receiving a design to delivering it completely — like the feature release — what are the most pain points you can point us to?

**Sahana S:** I have it — I mean, like recent times I have not faced any. That one point when I was transitioning to Carbon was with respect to finding the components, which I do have them easily accessible now. As I mentioned, Carbon components are divided with different storybooks, right? So that was one — first I had to go through. Now that I have used most of them, it is just a repeat of the same components. Only if I am using some other new components, I have to go back to those docs and check them out.

**Sahana S:** Apart from that, I believe the job is — I mean apart from that, nothing else.

**Mridusmita Nath:** We've heard very good feedback about your implementation. So have you also — do you also have any point about how other teams or other developers are working — anything that they can learn from your practices, something that you do from your side and you have seen that others don't do?

**Sahana S:** I am not entirely sure — maybe get the designs reviewed after developing. I mean, any UX developer would have developed it — that would tell you with respect to what is missed and what is not, right? With respect to UX developers, that will be UX design. Apart from that, nothing else from it.

**Mridusmita Nath:** Okay, thank you for that. Ankit, to you.

**Mridusmita Nath:** Okay, thank you. Ankit, do you have any questions for Sahana? Alright, Sahana, thank you so much for your time.

**Ankit Anand:** No, I'm good. Yes, thank you, Sahana. It was really helpful. Yeah, hope we can create a good solution here and then share it with you.

**Sahana S:** Happy to help.

**Mridusmita Nath:** Yeah. Thank you.

**Ankit Anand:** Thank you. Bye bye.

**Sahana S:** Bye. Thank you. Yeah.

---

<!-- Corrections & Flags -->
<!-- Corrections: "Zana" → "Sahana" (mishearing of participant's name, used multiple times) -->
<!-- Corrections: "Karib" → "Carbon" (mishearing in context of Carbon component library) -->
<!-- Corrections: "toggle time" → "toggle tip" (mishearing, Carbon component name confirmed by participant) -->
<!-- Corrections: "Oddspace" → context unclear, left as-is — FLAG: Sahana's response "Of Oddspace" at spacing tokens section may be a mishearing; original kept verbatim -->
<!-- Corrections: "Pokerans" → "Carbon components" (mishearing, context: "we used the carbon components itself") -->
<!-- FLAG: Participant's screen share references cannot be fully captured in the transcript — several references to "this" or "here" refer to visual elements not visible in the text -->
<!-- FLAG: "Tala" — name mentioned as knowing icon library source; unclear if IBM colleague or external contact -->
<!-- FLAG: "B2 BNFT" / "B2 BNT" — likely a product or testing acronym; could not verify from transcript alone -->
