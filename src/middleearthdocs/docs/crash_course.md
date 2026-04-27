# Compute Liaisons GitHub Project Management Guide

# Liaisons responsibility

As a sort of statement of problem we can focus on the question:

> what do Liaisons really have to do?

Liaisons are sort of stewards of the computing resources. Their job is to facilitate
communication between:
- Users
- Faculty (decision makers)
- PACS (engineering and maintenance)

Liaisons also educate the users about the system, coordinate between users and PACS
and PACS and faculty, and surface risk factors in terms of long-term maintenance
and state of the resources.

Primarily, however, the kinds of failures we most often see are:
- user spans `n >>> 1` processes and makes the system slow
- user takes up too much RAM and spills over to SWAP and makes the system slow
- user fills up `tmp` and makes the system slow
- user saturates the network making the system feel slow

When we can catch some of these issues on time (Compute Liaisons have root
access and are allowed to kill the processes causing an issue) we can restore the
system performance, get rid of lag and get to a more-fair-to-everyone usage
division again.

When we can not figure it out, we **need to notify PACS.**

## Communicating with PACS

We have a Slack channel in which most of these incidents are addressed:
* `#computing` - for public and user facing communication and response
* `#computing-liaisons` - for internal private communication, and
* `#computing-admins` - for semi-internal faculty, liaisons and PACS communication

So most often these things are handled through there. PACS also has an email
for their help-desk which is often used for less-urgent issues.

Liaisons have a weekly Liaisons Meeting where updates and process is discussed
and there is a biweekly meeting with PACS and Liaisons where system state is
discussed.

There are no official faculty meetings yet, we are trying to develop a process
for engaging with the decision makers.

## Purpose of GH Project

Since we already have a lot of communication channels it can be less obvious why
we need yet another management tool layer. Put simply it's because GitHub issues
should track durable work, not ephemeral chatter and immediate our compute is on
fire circumstances.

Slack handles:

- immediate slowdowns
- “who is using all RAM?”
- “can someone check Gondor?”
- kill-process interventions
- quick PACS pings
- active incidents
- free form discussion

GitHub handles:

- documentation
- onboarding tasks
- policy decisions
- maintenance requests
- planning
- follow-up actions
- summary of free-form discussions (hallways/slack DMs/not in meeting conversation ideas)
- improvements needing ownership

Despite immediate interventions being majority of Liaisons workload, there are
certain questions that require input from other stakeholders (users, faculty,
liaisons or PACS). Many of such issues can span very different time windows.
Because Liaisons rotate on and off their volunteer service positions some of
these activities can be accidentally dropped in the process. That's what GH
Projects are for: shared memory, coordination system, planing tool, backlogs etc.

### Core Principle

> **If forgetting it would hurt later, make an issue. If it is solved in chat**
> **within minutes, leave it in Slack.**

---

# Project management

To summarize the above section:

**What NOT to create issues for:**

* one-off slowdowns fixed in 5 minutes
* normal Slack conversations
* quick user clarifications already resolved
* temporary system load with no follow-up need

**What SHOULD become an issue:**

* problem repeats
* docs are missing
* ownership is unclear
* action item came from meeting
* action item requires more stakeholder engagement
* future planning is needed
* preventative work

To keep friction low, opening an issue only has 1 requirement:
* **Set the correct `type` tag on your issue.**

It would be very nice if you also applied the correct:

* `status` tag
* `system` tag
* `priority` tag

Listed in the order of *importance*, but even these three tags are not required.
The `status` tag helps because the kanban board can auto-update the column of an
issue based on its tag. That means less clicking for you.       
And `system` helps us apply filters on issues.

The weekly meetings should be formed around the following idea:

> Dearly beloved,
> we have gathered here today to move items:
> From    |   To
> --------|----------------------------
> Inbox   | Ready
> Ready   | In Progress
> Waiting | Ready if response received
> Done    | close/archive

and then move an item.

---

# Labels

The rest of this document reviews and explains the existing labels you can use
and showcases practical examples in what circumstances they would be good to use.

There are only 4 types of labels:

* `type` - what kind of work is this: task, docs, education, followup, discussion, approval, or project
* `status` - what stage is this work in (working on it, waiting on something...)
* `system` - which machine, resource, or stakeholder group is involved
* `priority` - how urgently do we need to worry about it (affecting users or not?)

### TYPE Labels (Required)

Type labels describe what kind of work this is. Use one per issue — if two feel
right, pick the one that best describes what the *next action* is.

| Label             | Description                                                                        |
|-------------------|------------------------------------------------------------------------------------|
| `type:task`       | A concrete to-do with a clear owner and done-state. One person can close it.       |
| `type:docs`       | Write, fix, or clarify documentation.                                              |
| `type:education`  | Help users understand or change how they use the system.                           |
| `type:followup`   | Something broke or keeps breaking; track the investigation or preventive response. |
| `type:discussion` | The team needs to agree before anyone can act. No single assignee.                 |
| `type:approval`   | Needs faculty or PACS sign-off before work can begin: budget, hardware, or policy. |
| `type:project`    | Large multi-step effort spanning multiple tasks and people.                        |

> **`type:task` vs `type:discussion`:** If you could write "Assign to: Y,
> Done when: X" on the issue — it's a `type:task`. If the issue would sit in
> limbo until the team agrees on an approach — it's a `type:discussion`.
> For example:
> "Add new liaison to sudo group."  `type:task`
> "How we should communicate status during outages?"  `type:discussion`
>
> **`type:discussion` vs `type:approval`:** Both involve group buy-in, but the
> blocker differs. `type:discussion` is waiting on the *liaison team* to agree.
> `type:approval` is waiting on *faculty or PACS* to sign off. For example:
> "How do we escalate when PACS is unresponsive and its my week" `type:discussion`
> "PACS wants to delete inactive user home directories."  `type:approval` + `system:faculty`
>
> **`type:docs` vs `type:education`:** Both are meant for users, but docs specifically
> means the *content* of the documentation is missing, wrong, or unclear. `type:education`
> means *user behavior* is the problem, we need to do a talk at Dirac AllHands, send out
> a channel notification, talk to a user etc. For example:
> "The SSH setup guide has a broken step"  `type:docs`
> "Users keep filling /tmp because they don't know not to" `type:education`


### SYSTEM Labels (Optional)

System labels identify which machine, resource, or stakeholder group is involved.
Use as many as apply — they are the main way to filter issues.

| Label              | Meaning                                                                          |
|--------------------|----------------------------------------------------------------------------------|
| `system:compute`   | General compute infrastructure, CPU/RAM/tmp issues not tied to one machine only. |
| `system:gondor`    | Issues or work specific to Gondor.                                               |
| `system:arnor`     | Issues or work specific to Arnor.                                                |
| `system:epyc`      | Issues or work specific to Epyc.                                                 |
| `system:rivendell` | Issues or work specific to Rivendell.                                            |
| `system:baldur`    | Issues or work specific to Baldur.                                               |
| `system:bendis`    | Issues or work specific to Bendis.                                               |
| `system:storage`   | Shared filesystems, Helios/Shire/Shiren, backups, and capacity.                  |
| `system:network`   | Connectivity, latency, throughput, or transfer issues.                           |
| `system:accounts`  | Accounts, SSH keys, permissions, groups, or access.                              |
| `system:docs`      | Documentation platform, structure, or published docs.                            |
| `system:liaisons`  | Internal liaison work: onboarding, meetings, procedures, handoffs.               |
| `system:pacs`      | Requires PACS action, response, ownership, or coordination.                      |
| `system:users`     | Involves or impacts users.                                                       |
| `system:faculty`   | Requires a faculty decision, budget approval, or policy authority.               |

### PRIORITY Labels (Optional)

There are no hard-core rules about priorities at the moment as the real immediate
priorities are dealt with through Slack channels. Use your best judgment. Issues
degrading user-experience are p1, everything else is pretty normal.


| Label          | Meaning                                                  |
|----------------|----------------------------------------------------------|
| `priority:p1`  | High priority. Impacts users or needs prompt attention.  |
| `priority:p2`  | Normal priority. Useful work in regular queue.           |
| `priority:p3`  | Low priority. Can wait without immediate impact.         |


### STATUS Labels

This just tracks the status of the ticket in the Kanban project board.
It would be really nice if you added it to your issues.

| Label                | Meaning                                                    |
|----------------------|------------------------------------------------------------|
| `status:ready`       | Triaged and ready to be picked up at the next meeting.     |
| `status:blocked`     | Cannot proceed until dependency or blocker is resolved.    |
| `status:waiting`     | Waiting on PACS, user reply, decision, or external input.  |
| `status:needs-input` | Needs discussion, clarification, or more information.      |
| `status:scheduled`   | Planned for a future meeting, window, or milestone.        |
| `status:in-progress` | Someone is actively working on this item now.              |


# Examples

## Quick classification

Let's summarize one more time. Not sure which `type` to use?
Work through this list and stop at the first match:

1. Did something break, slow down, or fail?  `type:followup`
2. Is there a concrete action with a clear owner and done-state?  `type:task`
3. Does the team need to discuss and agree before anyone can act?  `type:discussion`
4. Does this need faculty or PACS sign-off before anything can start?  `type:approval`
5. Is it too large to fit in a single issue?  `type:project`
3. Does documentation need to be written or corrected?  `type:docs`
4. Does a user need to learn or change their behavior?  `type:education`

For `system`, ask: which machine, resource, or stakeholder group is involved?
Label everything that applies.

## Practical Examples

> Several users report slow jobs on Gondor this week, but no obvious cause
* `type:followup`
* `system:gondor`
* `priority:p1`

Type reason: Someone needs to investigate and possibly escalate to PACS. It's not
a one-off slowdown resolved in Slack. It needs tracking.

System reason: Start with `system:gondor` since that's what's observed. Add
`system:compute`, `system:storage`, or `system:network` once the cause becomes clearer.

---

> Repeated filesystem hangs need PACS review
* `type:followup`
* `system:storage`
* `system:pacs`
* `priority:p1`

`system:pacs` signals that PACS action is required, not just liaison investigation.

---

> User keeps running 200 parallel jobs and slowing Gondor for everyone
* `type:education`
* `system:users`
* `system:gondor`
* `priority:p1`

Type reason: The fix is changing user behavior, not fixing infrastructure. If the
behavior persists because guidance is missing, add `type:docs` as well.

---

> Explain where backed-up shared data should live
* `type:education`
* `system:storage`
* `priority:p2`

---

> Need storage growth plan for the next 3 years
* `type:approval`
* `system:storage`
* `system:faculty`
* `priority:p2`

`system:faculty` signals this will stall until faculty weighs in on the budget.
Multiple system tags are fine — add `system:epyc` too if the discussion is
specifically about Epyc's aging JBOD drives. In this particular case, this issue
would need to be under a bigger `type:project` umbrella because it hits literally
everyone. The particular issue here is the situation where we just went to the
faculty with the bad news and are still hopeful they'll just say ok. But as
pushing and pulling starts and different priorities float up, it's definitely
a project.

---

> After Arnor outage, define a better status communication path
* `type:discussion`
* `system:liaisons`

`type:discussion` because the output is a team agreement, not one person's task.
Followup and the slowdown has been fixed, but there were some rough edges left to
discuss in the process.

---

> Need sudo access for new liaison
* `type:task`
* `system:pacs`
* `system:accounts`
* `priority:p2`

One concrete action, clear owner, clear done-state. Generally, if the title of
your issue can end with a period, it's probably a task.

---

> SSH key docs are outdated or missing steps
* `type:docs`
* `system:docs`
* `priority:p2`

---

> Repeated RAM exhaustion on Gondor
* `type:followup`
* `system:gondor`
* `system:compute`
* `priority:p1`

Something keeps going wrong and causing outages, can't figure out what. Leave
and issue so that everyone can put down their observations on more-permanent
record than annals of Slack chat rooms. Recent example with Mario running 100s
of docker Jupyter hubs for a summer school is a good one.

---

> How should we handle rotating liaisons and handing off open issues?
* `type:discussion`
* `system:liaisons`
* `priority:p2`

No one person can decide this — it needs a team discussion and a shared agreement.
Once the team decides, open a `type:task` or `type:docs` issue to write it up.

---

> Plan storage expansion in next 2 years
* `type:approval`
* `system:storage`
* `system:faculty`
* `priority:p2`

---

> After repeated outages, define how we notify users and faculty
* `type:discussion`
* `system:liaisons`
* `system:users`
* `system:faculty`
* `priority:p2`

`type:discussion` not `type:approval` — the team is agreeing on a communication
protocol, not procuring anything. `system:faculty` because they are a recipient
of the notification and may need to weigh in on the process. Could result in an
issue that needs faculty or pacs approval.
