# UI Reviewer — UXR Discovery Session: Senthil Kumaran Pattabiraman
**Date:** 21 August 2026

## Participants

| Name | Role / Title | Organisation | Side |
|---|---|---|---|
| Mridusmita Nath | UX Researcher / Interviewer | IBM | IBM |
| Ankit Anand | Designer | IBM | IBM |
| Senthil Kumaran Pattabiraman | Senior Frontend Developer / Tech Lead | webMethods / API team | Participant |

---

**Senthil Kumaran Pattabiraman:** Yes, so — okay, so currently the UI review is happening purely — at least for the product I am working on — it is done by the designers. So we will be sharing a screen recording video, which is attached to the pull request and then they play it. And then since it is a video, they can pause and then find the gaps where all misalignments are there, all components used. So this actually solves the visual issue first, at least. But at the back end, if they are really using the Carbon component, are they really using the tokens? No one has any idea. So that gap is still there. I would still say you can fill in that gap, but I also have an idea which is easily possible with the AI PDLC. Now this AI PDLC is going to have all these pre-created tests. For example, there will be a MD file which will do the pull request review — PR review. The moment if I type slash PR review, it pulls that skill or the MD file, and then goes through all the guardrails the engineer or the architect already defined. So, for example, there are certain things engineers cannot do when they are writing the code — all those are already documented, well documented in the architect's MD file, and this gets in there, tries to map those, and then checks it out based on what the developer has used against the document created by the architect. What I would suggest is I would suggest you to create something similar for UX review — like rather than just PR review, there could also be a UI review or UX review. So the moment you type that MD file, which is already part of the new AI PDLC structure — I'm not sure if your product is already having that, but Studio is already integrated that. So we already have the AI PDLC and we are already having the PR review. And so there, if it is possible, you can define all your expectations. For example, when you're giving a component, you expect them to use the exact same component. And if there are spacing, you don't want the developer to use their own px values or even a third-party library like Tailwind, but they will be recommended to use the spacing tokens provided by Carbon itself. So these are just some examples, right? This list goes really long. So you can also make sure they're using the colour values directly from Carbon, not any random hex value or any random colours from Tailwind CSS. So there are third-party libraries like today — Tailwind, Bootstrap — all these frameworks are also providing colours which can be directly used and most of the developers are already using it. And Bob also — currently, what it does is — when you just share a design even in a Figma frame, if it is not able to figure out the component, if the component is not connected well in Figma, then what Bob thinks is: maybe this is not a component available in Carbon, so let me create it on my own. So it writes its own CSS, own component. Uses whatever value it can — if the user is already using Bootstrap, it will use Bootstrap colours directly and then change everything. But look and feel, it will look perfectly fine, but it will not scale in the future, right? If there is some change, it will definitely break — the developer will have to rework or the tech debt will keep on increasing. So this is just for colour, right? In the same way, typography is already an issue, spacing is already an issue, and components itself. So there are cases — even yesterday I had one. So there was a design provided by a designer which had a dropdown.

**Mridusmita Nath:** Designer used what?

**Senthil Kumaran Pattabiraman:** Select. There are 2 components in Carbon library: one is Select, the other one is Dropdown. So by mistake, they have used Select and we blindly trusted, because when I am giving the Figma MCP link, it will be pulling up the Figma, takes a screenshot, and looks at all the connected components and uses that component by itself. So when I looked at it, when I tested it, it looks perfectly fine, but the only change is when you click on it, you will see dropdown values in the native browser dropdown rather than the customised Carbon one. Luckily, one of the other developers who was reviewing my PR got it and then I was able to change it to Dropdown. So these gaps are still there. So I would say — but I am afraid that you may not show it as a tool — but you could write that MD file which does all these checks. You can take help of Bob — Bob can actually write it for you — and you just recommend your product team to integrate this into their flow. So it will be part of the skills.md or rules.md — somewhere it will be keeping these rules — and then make sure whenever it is writing it will not do that. I actually created — so that all the use cases which I just mentioned to you — I already created a MD file and it is already integrated into our AI PDLC structure. So now when they are using the Figma — I'm —

**Mridusmita Nath:** Oh. Can you show us something, Senthil?

**Senthil Kumaran Pattabiraman:** I don't think how much you will make it out from that.

**Mridusmita Nath:** So, what does the AI PDLC structure look like and what does this file look like?

**Senthil Kumaran Pattabiraman:** So that is actually the Bob thing only. So inside Bob you will have — this is Bob, right? So all these things — plan, rules, code — and these are the skills. So in all these you can see right here — merge, PR review, plan and epic, Jira manager — all this. So my step goes into implement issue. In this skill I'm trying to add — so these are rules. So for example, for Jira issues use the Jira MCP server to fetch the issue body. So this is kind of a rule, right? For a Jira issue, you should follow these steps. So what I have done is similar — when you are implementing a UI, make sure you're using only the things provided by Carbon, don't use Tailwind classes, don't use Bootstrap classes — like that. I have to define. You don't have to write all this — you just type to Bob, Bob will create the MD file and you just have to integrate it.

**Mridusmita Nath:** Okay. So if you say so. Got it, but how to review? Because the MD file — it is going to write like on its own, right?

**Senthil Kumaran Pattabiraman:** You don't have to review. But when they ask Bob to review this, it will go through the rules you defined and it will throw errors when it is not met.

**Mridusmita Nath:** Got it. Okay. And just one example — suppose you have said that don't use anything other than Carbon, okay. And then there is some custom or there is some implementation — then does this sentence ensure that Bob will not ever create anything on its own?

**Senthil Kumaran Pattabiraman:** Yeah. That is the first step. So what — that is what I have done. So this is, as I told you, when it is implementing an issue, I am making sure it is not deviating from what it is supposed to do — it has to follow Carbon. That should be the primary step. Now at your stage, what I would say is there will be a review, right? Part of this peer review, I will add UI review. UI review will again cross-check all these things are met. If there is anything, it will create a detailed report and it will also give you the next action items where Bob can get in and fix these. So that would also be part of it — that is why I am saying either you do it here. I am actually doing it here. You can do it here.

**Mridusmita Nath:** Yeah.

**Senthil Kumaran Pattabiraman:** Yeah, so PR UI review could be part of PR review, or if you want, you can have a UI review separately also created and then the developer can run it.

**Mridusmita Nath:** Got it. Peer review. Implementation. Got it.

**Senthil Kumaran Pattabiraman:** And the report is quite detailed, so the developer will immediately know — these are wrong. And again, Bob is going to offer them the solution as well. So they will just say yes, go ahead and fix it, and Bob will fix it happily.

**Mridusmita Nath:** Okay, that's been happening in your —

**Senthil Kumaran Pattabiraman:** So this is one thing, but for your task, I think this is more than enough. But if they're really looking for something tangible, then you have to do something beyond this — maybe using the same in an application — that doesn't make sense, right?

**Mridusmita Nath:** Yeah, I mean, it has to definitely scan the implementation and then show some kind of —

**Senthil Kumaran Pattabiraman:** So that code repository is the right place. If you are having an application, that will be superficial, right? You cannot get in. You can still provide — I think those tools can still get into the git repository. For example, if you are trying to review it at some point, whatever the developer has developed, you can pass in the branch information. This could be one idea — actually this could be a potential one. So you create a UI where it takes the branch from so-and-so repository. For example, if it is integration, you get access to the integration repository and you should also populate the branches available, and if the user — as a user, you can review, right? So you choose whichever repository, whichever branch you want to check. Recently, if a developer implemented a feature, there must be some branch. You get the branch from the developer itself and choose that branch, ask Bob to run — characters. So that's the issue with the older way. I always do the review — I do 100% review — but if the developer is not willing to fix it, again, you are going to fail. So that's why.

**Mridusmita Nath:** But are you also — do you also have some form of automation to create Jira issues out of the issues found?

**Senthil Kumaran Pattabiraman:** I think we do have in the skills somewhere. I think that is part of some step. If it is vulnerable and then if it has to be broken down in your task, that is also something this is doing. It creates an issue.

**Mridusmita Nath:** Okay, nice. I think this level of maturity — no, I mean this level of maturity for teams, it is not there for all the teams, so we have to.

**Senthil Kumaran Pattabiraman:** It is also doing that — you can actually do that. Actually, in your case — and that is true. I spoke with the integration team, one of the developers, he mentioned exactly the same. So they still have that scary side — where they might replace us. Developers are still taking it seriously. They didn't know the fact that whether you do it or not, you're still going to be replaced, so they have not started accepting it. At least we accepted it. See, now with the rule I have written, right? Actually, there won't be a need for a person like me to govern the developers to write the code in the first place. So now, whatever I check, it's already been written as a MD file and shared it with Bob. So what I do majorly — most of the part — Bob is going to take care. So that part is there, that is why they are avoiding. But yes, again, coming back to the second idea, you can still have an application, share the branch, let Bob run the test and run the scan. Once it is done, ask it to create a report itself and attach that report as a description in a Jira ticket.

**Mridusmita Nath:** Yeah.

**Senthil Kumaran Pattabiraman:** And what the developer can do is when they share the Jira ticket in Bob again here, the moment I type my ticket number something, it will be able to read the description and it will be able to go through the code and fix them all — because your description, whatever you're going to write, there will also be an acceptable solution, right? What is that called? — we have something, some term —

**Mridusmita Nath:** Mhm.

**Senthil Kumaran Pattabiraman:** So this is the issue, and for acceptance criteria — so there will be acceptance criteria — that also you can ask Bob to coin it according to your rules and expectations. If the ticket has that information, that is more than enough for Bob to run this and then get the information and then fix the code as well, and it will also create a PR based on that particular ticket with the branch created by itself. That could be one. So if they are not matured enough to have something like this AI PDLC, then the second idea helps — and also that serves the purpose of having something tangible for your use case also.

**Mridusmita Nath:** Okay. Mhm.

**Senthil Kumaran Pattabiraman:** You could do that actually.

**Mridusmita Nath:** Okay, let's try that.

**Senthil Kumaran Pattabiraman:** Yeah, you ask Bob to do all that and for the rules.md you type whatever you don't want the developer to use — Bob should be able to write the MD file for itself — and then it will use it when running the scan on the code based on the branch, and you can choose main branch to go through the whole application. So that is still possible.

**Mridusmita Nath:** I mean, branch is just a link, right? I mean, I am also thinking it could be — there is an interface where we enter it, or Bob only asks, right — the branch thing.

**Senthil Kumaran Pattabiraman:** You can do that, yeah. So what would be the starting point? "Review integration" — something like that. There will be a button and then you click on it, it'll ask for repository information, and then you paste the repository information, then it'll ask you to choose the branch, then you go ahead. You can do that.

**Mridusmita Nath:** I think feature name or something. But what you are proposing is within Bob's interface only, right?

**Senthil Kumaran Pattabiraman:** Yes. Out of the box interface, there is going to be a new interface you are going to develop — could be potentially an HTML file or some technology Bob is going to choose. But end of the day, you'll be looking at a page in a browser with all these actions — other standard application, yeah.

**Mridusmita Nath:** Yeah. Okay. All right, okay. Let's move on — we also want to document how the UX review process now goes — like who initiates, how does the designer, how does the collaboration between designer and developer happen, and the correction.

**Senthil Kumaran Pattabiraman:** I don't know about the other teams, but yeah — API teams, I think, right? So we always have that part of the PR review.

**Mridusmita Nath:** No, you tell about your process. We need it for the recording — Senthil, please explain it.

**Senthil Kumaran Pattabiraman:** So whenever there is a UI-related change — yeah, I can explain. So whenever we have a PR which has UI-related changes, or if there is a new UI feature implemented — in all those PRs, we add the designers. Either it is a respective designer or the design lead. So both of them will be there. And it is also mandated to the team that they have to attach the screen recording video, not just screenshots. So they need to attach the video, and then they link it — unless until they get one approved from the UX team, they can't merge the PR. So that's the rule we follow. So even during development also — we are — see, we already mandated our design team to always use the connected components, so that when we are sharing that link — you know that, right? — when we have something in Figma called, when in developer mode, whoever has the developer mode, they can see this. For example, I click this frame and it will have a frame ID as a link. So now if I click this, I have this — I copy this and paste it — Bob is able to develop exactly the similar one like this without any deviation, because this design is well connected. If it is properly connected then it works just fine.

**Mridusmita Nath:** Okay. Mhm. When you say connected, these are the —

**Senthil Kumaran Pattabiraman:** Connected components — no detached components, no custom components — because that is the first rule we established already in the team. There is no deviation from Carbon, so we can't, you know, right? So we don't have anything apart from Carbon accepted. If at all needed, that would be a custom component. So like the metadata component, for example, we developed. So I think so far that is the only exception we have. The metadata component is the only component the API team has developed on its own. So otherwise, you know, right? So you use exactly the same. Tear sheet, left panel, and then tear sheet header — everything is Carbon component. So in that way, when it is connected, when I'm using this, mostly — that works — so the developer does not have to think which component it is using or all those things. And once it is done, also we are making sure we did it right with the designer — and that comes in the PR review — and unless until they don't approve, we will not merge it. And we will get into the discussion, we will again demo it, we will again go through the code and then fix it. And then once the designer is happy with the design, we request an approval from themselves and once they approve, we merge it. So that is the process we follow. So I think in our case, in every step we reach out to designers. Maybe that is one reason why our designers are always excited. So whenever there is a doubt, we immediately reach out to them — because not all the use cases are covered sometimes, right? So there could be corner cases — and we always take it back to them and then they will again provide some ad hoc designs and then accordingly we take it forward and get it to completion. So they are not away from us. They are very close with us. So it is like closely knit — hand in hand only — and still we would want a PR approval from them. See, that is again a selfish way, right? One day I don't want a designer to randomly come back to me and say: "this is not what I have given — how did you develop this? How did you get it merged?" For that reason also, developers wanted a clear contract: "See, this is what I have done as per your knowledge. You approved this, so you are aware that this is what is going in — you can't come back later someday and blame me." Yes, exactly. That is again one reason why we want to always include them in the PR review and get it signed by them.

**Mridusmita Nath:** Yeah, transparency is there. Yeah.

**Senthil Kumaran Pattabiraman:** So this is how the API team is following, and mostly it says it is successful — there are no gaps.

**Mridusmita Nath:** Yeah.

**Ankit Anand:** Certain design-development utopia is definitely there in the API team. I will say that.

**Senthil Kumaran Pattabiraman:** Yes.

**Mridusmita Nath:** No, we were also very lucky to start it from scratch, right? After we moved to IBM, we redid the whole thing, yeah.

**Senthil Kumaran Pattabiraman:** That is one thing. So that — and when they did also — the one good thing they have done is they started with React, luckily. So just a year before, even though we don't know we are going to be merged with IBM, they just wanted to learn React — it is a new technology, that time it was a new bubble. And luckily, since they have chosen React, it was easy for them to migrate to Carbon React. And that is the reason we were able to be 100% Carbon compliant. And because of that, accessibility was naturally cleared. So we did run an accessibility check — it was cleared — so that was again another positive thing. Accessibility, and then even this localisation and translations are all handled because of Carbon.

**Senthil Kumaran Pattabiraman:** Yeah, I know this is very, very difficult for a product like integration to look at. So I was also looking at the UI and this Wednesday only it is still the same crappy UI. And then I heard clearly that John told: "as long as it is working, don't touch it." So even the control toolbar icons they have, right? They are so big — there is no padding around — till they are working, it is, because it is working, right? "Don't touch it." So that's how they follow. So very difficult.

**Mridusmita Nath:** That's decided, okay.

**Senthil Kumaran Pattabiraman:** Yeah. But the UX review tool could help even for integration, right? So you can tell them: "we don't give clearance because you're not meeting these." So once they finish it, you can run it again and then try to generate a report again. And if the report still has mistakes, again circulate back to them. At least you can say, right? "This is not what we have done — you're going ahead with release without our consent. Then when the pain is yours, you handle it — don't come back to us saying you didn't do well." Currently, they are not even taking that responsibility or ownership. One day — I am damn sure — one day even if they are discussing internally with the management, they will simply say: "this is what we got from you." You never know, because you are not going to hear that word.

**Mridusmita Nath:** Yeah, and it's not part of the process also, right? The documentation.

**Senthil Kumaran Pattabiraman:** Yeah, exactly.

**Mridusmita Nath:** Okay, looks like you have already created your ideal world scenario, but I would still like to ask you — if there is a tool that does this for you, how would you want it to behave? Who would do UI reviews?

**Senthil Kumaran Pattabiraman:** Ideally, a tool — a new tool — which I would recommend.

**Mridusmita Nath:** How do you want it to work? Which stage?

**Senthil Kumaran Pattabiraman:** I would say what I just suggested you — that would actually help me a lot — because even though I am there, I can't make sure all my junior developers are doing exactly the way I do. So for that reason I have created a rules file. But still, what if they hand-code by themselves? Because when they make a change and push it, the skills won't run. But before development, if you are asking Bob to develop, Bob will make sure whatever is suggested is what I have said to follow. If they do it on their own without asking Bob, Bob will still not be able to intervene there — so they can still write wrong code, which is not at all acceptable — where I may not be able to go and check line by line. In those cases, that tool which I was just suggesting you will help. The moment I know this developer has worked on this feature, I can get the branch information from them. I can just put it on the tool and run it. I don't have to ask them — I can run it by myself and generate the report, create the ticket, assign it back to them: "you finish this, then take this PR forward." I can still do that. Actually, the tool I suggested — I will also create one day, but yeah, you do it first.

**Mridusmita Nath:** Got it. Let's see what we can do in one week.

**Senthil Kumaran Pattabiraman:** You can still do it in 2 to 3 days. I think Bob will be able to do that.

**Ankit Anand:** Yeah.

**Mridusmita Nath:** Yeah. Okay, Ankit, do you have any more questions?

**Ankit Anand:** I am good. This is very out-of-the-world. For integration, yeah.

**Mridusmita Nath:** Okay. Yeah, Senthil is a special case.

**Senthil Kumaran Pattabiraman:** No, I think API is a special case — I can't take much credit. No, for UI I would still take that, but for the AI PDLC, this team is like — oh my God, I don't know what word to call them. But yeah, the moment they discussed it, that certification happened, right? Where all these AI-related things were part of a mandatory course. So the moment they finished the course, they started creating this AI PDC environment.

**Mridusmita Nath:** Nice. Assam.

**Senthil Kumaran Pattabiraman:** Yeah, good luck with the product.

**Mridusmita Nath:** Okay, yeah, thank you.

**Ankit Anand:** Thank you. Senthil, I definitely —

**Senthil Kumaran Pattabiraman:** Yeah, and see the thing you are going to develop — I can also test it — because you're going to create it in a way that it is going to be neutral. You are letting — you're not hard-tying that with just the integration repository. You're going to keep the repository also open. So now I can use the same tool for my Studio repository, I can use the same tool for API Connector repository, any repository I wish. So you make sure you are creating something generalised, not tied to one single product. Yeah, okay. And your rules are mostly going to be the same rules. Yeah.

**Mridusmita Nath:** Yeah. So during the next week we might — yeah, during the next week we might meet you again. Yeah, once we start the process, okay.

**Senthil Kumaran Pattabiraman:** Sorry. Yes. Okay, yeah.

**Mridusmita Nath:** Alright, thank you. Yeah, bye bye.

**Senthil Kumaran Pattabiraman:** Thank you so much. Bye.

**Ankit Anand:** Thank you so much. Bye bye.

---

<!-- Corrections & Flags -->
<!-- Corrections: "UAA review" → "UI review" (mishearing, context clear throughout) -->
<!-- Corrections: "AIPDLC" / "AAPDLC" / "VIPDLC" → "AI PDLC" (normalised capitalisation/spacing throughout) -->
<!-- Corrections: "Bart" → "Bob" (mishearing of IBM Bob AI assistant name, context clear) -->
<!-- Corrections: "VR" → "PR" (mishearing of pull request, context clear) -->
<!-- Corrections: "empty file" → "MD file" (mishearing of Markdown file, context clear throughout) -->
<!-- FLAG: "yesterday's review could review tool" — garbled phrase around 20:35; left as close to source as possible -->
<!-- FLAG: "Assam" at end — likely a filler/reaction word, not a place name; left verbatim -->
<!-- FLAG: Speaker references "Studio" and "API Connector" as distinct products — both appear to be webMethods product lines -->
