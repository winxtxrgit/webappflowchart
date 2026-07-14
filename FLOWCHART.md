# FLOWCHART.md

**Every flow in the project, in one place.** Planning, building, running, failing, recovering.

> **Source of truth:** `Work/1.png` (architecture), `Work/2.png` (roles), `Work/3.png` (machines).
> **Marker legend:** 📌 = from the images · 🧩 = derived from the images · 🤖 = `AI Recommendation` · ⚠️ = `Needs further verification`

---

## Contents

| # | Flowchart | Answers the question |
|---|---|---|
| 1 | [The whole project, end to end](#1-the-whole-project-end-to-end) | *What happens, in what order, from nothing to deployed?* |
| 2 | [The planning flow](#2-the-planning-flow) | *How does an idea become an assigned task?* |
| 3 | [The working system — runtime](#3-the-working-system--runtime) | *What actually happens when a user clicks "Generate"?* |
| 4 | [The working system — sequence](#4-the-working-system--sequence-diagram) | *Same thing, showing the timing and the waiting* |
| 5 | [Parallel vs sequential work](#5-parallel-vs-sequential-work) | *Who can work at the same time as whom?* |
| 6 | [The agent working loop](#6-the-agent-working-loop) | *How does one agent take a task from start to handover?* |
| 7 | [The Master Agent coordination loop](#7-the-master-agent-coordination-loop) | *How does work get assigned and reviewed?* |
| 8 | [Task routing decision tree](#8-task-routing--which-agent-gets-this) | *Given a task, whose is it?* |
| 9 | [The integration flow](#9-the-integration-flow) | *In what order do the pieces get connected?* |
| 10 | [Testing flow](#10-testing-flow) | *What gets tested, by whom, when?* |
| 11 | [Deployment flow](#11-deployment-flow) | *How does code get onto the four machines?* |
| 12 | [Failure and rollback](#12-failure-and-rollback) | *What do we do when it breaks?* |
| 13 | [Git branch flow](#13-git-branch-flow) | *How does code move from a branch to production?* |
| 14 | [The state of a single task](#14-the-life-of-a-single-task) | *What states does a task pass through?* |

---

## 1. The whole project, end to end

**The master flowchart.** Red = the two places the project can die. Orange = the gate that unlocks parallel work.

```mermaid
flowchart TD
    START([Project starts]) --> S1

    S1["<b>STAGE 1 · Requirement Analysis</b><br/>🔁 all 5 roles<br/><i>What are we building?</i>"]
    S1 --> CP1{{"✅ CP-1<br/>Requirements agreed<br/>3-PC or 4-PC chosen"}}

    CP1 --> S2["<b>STAGE 2 · System Planning</b><br/>API contract · DB schema · network plan"]
    S2 --> CP2{{"🔶 CP-2 · THE CRITICAL GATE<br/><b>API CONTRACT FROZEN</b><br/>everything below can now run in parallel"}}

    CP2 --> S3["<b>STAGE 3 · Network + Nginx</b><br/>👤 P5 / P4<br/>static IPs · firewall · proxy"]
    CP2 --> S4["<b>STAGE 4 · UX/UI Design</b><br/>👤 P1<br/>wireframes · design system"]
    CP2 --> S5B["<b>STAGE 5B · Flask Backend</b><br/>👤 P2<br/>auth · API · DB · logging"]
    CP2 --> S5C["<b>STAGE 5C · AI Server</b><br/>👤 P3<br/>Forge AI · LoRA · Queue"]
    CP2 --> S5D["<b>STAGE 5D · Test plan</b><br/>👤 P4<br/>written BEFORE the code exists"]

    S3 --> CP3{{"✅ CP-3 · Network alive<br/>every machine reaches every machine"}}
    S4 --> CP4{{"✅ CP-4 · Mockups approved"}}
    CP4 --> S5A["<b>STAGE 5A · Frontend</b><br/>👤 P1<br/>Bootstrap · JS · <i>on mocks</i>"]

    S5A --> CP5{{"✅ CP-5 · Each part works ALONE"}}
    S5B --> CP5
    S5C --> CP5
    CP3 --> CP5

    CP5 --> S6["<b>STAGE 6 · INTEGRATION</b><br/>⛓️ strictly ordered<br/>DB → AI → Frontend → Nginx"]
    S6 --> CP6{{"✅ CP-6 · M4<br/><b>END-TO-END PATH WORKS</b><br/>every arrow in 1.png is real"}}

    CP6 --> S7["<b>STAGE 7 · Testing</b><br/>👤 P4<br/>unit · integration · E2E · load · failure"]
    S5D --> S7
    S7 --> CP7{{"✅ CP-7 · No critical defects"}}

    CP7 --> S8["<b>STAGE 8 · Deployment</b><br/>👤 P4<br/>deploy · dashboard · backup · manuals"]
    S8 --> CP8{{"✅ CP-8 · Survives a full reboot"}}

    CP8 --> S9["<b>STAGE 9 · Final Evaluation</b><br/>🔁 all 5"]
    S9 --> DONE([✅ PROJECT COMPLETE])

    style CP2 fill:#ffe0b2,stroke:#e65100,stroke-width:4px,color:#000
    style S6 fill:#ffcdd2,stroke:#b71c1c,stroke-width:4px,color:#000
    style CP6 fill:#ffcdd2,stroke:#b71c1c,stroke-width:3px,color:#000
    style START fill:#c8e6c9,color:#000
    style DONE fill:#c8e6c9,color:#000
```

**Read this chart for one thing: the shape.** Everything is a single narrow line until **CP-2**, then it explodes into five parallel tracks, then it funnels back into **Stage 6**. Those two pinch points are where the project is won or lost — the contract gate at the top, and integration at the bottom.

---

## 2. The planning flow

**How an idea becomes an assigned task.** This is the loop the Master Agent runs continuously.

```mermaid
flowchart TD
    A["📥 A requirement, feature<br/>or defect arrives"] --> B{"Is it in<br/>REQUIREMENTS.md<br/>or the images?"}
    B -->|No| B1["⚠️ Mark it<br/><b>Needs further verification</b><br/>Ask the human team.<br/><i>Do not invent it.</i>"]
    B1 --> STOP1([Hold])
    B -->|Yes| C["Read PROJECT_WORKFLOW.md<br/>Which stage are we in?"]

    C --> D{"Are its<br/>dependencies<br/>satisfied?"}
    D -->|No| D1["🔴 Do not dispatch.<br/>Queue it behind<br/>the blocking task."]
    D1 --> STOP2([Queued])
    D -->|Yes| E["Decompose into tasks"]

    E --> F{"Does one task touch<br/>files owned by<br/><b>two</b> agents?"}
    F -->|Yes| F1["✂️ SPLIT IT.<br/>It is not one task —<br/>it is two tasks<br/>and a contract."]
    F1 --> E
    F -->|No| G["Identify the single<br/>owning agent<br/><i>(see chart 8)</i>"]

    G --> H{"Is a shared file<br/>locked by<br/>someone else?"}
    H -->|Yes| H1["⏸️ Wait for the lock.<br/>Serialise the tasks."]
    H1 --> STOP3([Waiting])
    H -->|No| I{"Can this run<br/>in PARALLEL with<br/>anything already<br/>in flight?"}

    I -->|Yes| I1["🔀 Dispatch both.<br/><i>This is where the<br/>schedule is won.</i>"]
    I -->|No| I2["⛓️ Dispatch alone."]

    I1 --> J["📋 Issue the task<br/>in the standard format"]
    I2 --> J
    J --> K["👀 Monitor · unblock · chase"]
    K --> L{"Completion report<br/>received?"}
    L -->|No| K
    L -->|Yes| M{"Quality checklist<br/><b>fully</b> complete?"}
    M -->|No| M1["❌ Reject.<br/>Name the exact<br/>unticked item."]
    M1 --> K
    M -->|Yes| N["✅ DONE<br/>Release the lock<br/>Trigger the handover"]
    N --> O{"Checkpoint<br/>reached?"}
    O -->|No| C
    O -->|Yes| P["📊 Publish the status report<br/>Advance the milestone"]
    P --> C

    style B1 fill:#fff3e0,stroke:#e65100,color:#000
    style F1 fill:#e1f5fe,stroke:#01579b,color:#000
    style I1 fill:#c8e6c9,stroke:#2e7d32,color:#000
    style M1 fill:#ffcdd2,stroke:#b71c1c,color:#000
```

---

## 3. The working system — runtime

**What physically happens when a user asks for an image.** Every arrow here is drawn in `1.png` 📌.

```mermaid
flowchart TD
    U(["👤 User's Browser"])

    subgraph MAC1["🖥️ MAC-01 — 192.168.1.10 📌"]
        NG["<b>Nginx</b><br/>Reverse Proxy 📌<br/>🤖 :80"]
        FE["<b>Frontend</b><br/>HTML / CSS / JS 📌<br/>Bootstrap · JavaScript"]
    end

    subgraph MAC2["🖥️ MAC-02 — 192.168.1.20 📌"]
        BE["<b>Backend (Flask)</b> 📌<br/>Auth · API · Logging<br/>🤖 :5000"]
        DB[("<b>Database</b><br/>SQLite 📌")]
    end

    subgraph WIN1["🎮 WINDOWS-PC-01 — 192.168.1.30 📌"]
        Q["<b>Queue</b> 📌<br/>one job at a time"]
        AI["<b>Forge AI</b> 📌<br/>Generation · Editing<br/>Model / LoRA<br/>🤖 :7860"]
    end

    U -->|"1 · HTTP request"| NG
    NG -->|"2 · static files"| FE
    FE -->|"3 · user clicks Generate"| NG
    NG -->|"4 · /api/* → .20"| BE
    BE -->|"5 · authenticate"| BE
    BE -->|"6 · record the job"| DB
    BE -->|"7 · HTTP → .30"| Q
    Q -->|"8 · when the GPU is free"| AI
    AI -->|"9 · the image ⏱️ SLOW"| BE
    BE -->|"10 · store it"| DB
    BE -->|"11 · respond"| NG
    NG -->|"12 · the image"| U

    NOPE1["🚫 The Browser NEVER<br/>talks to .30 or the DB<br/><i>1.png draws no such arrow</i>"] -.- WIN1

    style WIN1 fill:#fff3e0,stroke:#e65100,color:#000
    style NOPE1 fill:#ffcdd2,stroke:#b71c1c,color:#000
    style AI fill:#ffe0b2,color:#000
```

**The single most important structural fact in this diagram:** there is **no arrow from the browser to the AI Server.** Every AI request is brokered by the Backend — that is what makes authentication, logging and the queue possible at all. An agent who "optimises" by calling `.30` directly from JavaScript has destroyed all three.

---

## 4. The working system — sequence diagram

**The same flow, but showing the thing the boxes hide: the waiting.**

```mermaid
sequenceDiagram
    autonumber
    actor U as 👤 Browser
    participant N as Nginx<br/>192.168.1.10
    participant F as Flask<br/>192.168.1.20
    participant D as SQLite<br/>192.168.1.20
    participant A as Forge AI<br/>192.168.1.30

    U->>N: GET / (load the app)
    N-->>U: HTML · CSS · JS (Bootstrap)

    U->>N: POST (generate an image)
    N->>F: proxy → :5000
    F->>F: authenticate the user
    F->>D: record the job
    D-->>F: ok

    F->>A: HTTP → :7860
    A-->>F: accepted (job queued)
    F-->>N: "queued" — returns IMMEDIATELY
    N-->>U: job accepted 🤖

    Note over A: ⏱️ THE GPU WORKS<br/>seconds to minutes<br/>ONE job at a time 📌

    loop 🤖 the browser polls while it waits
        U->>N: is it ready?
        N->>F: proxy
        F->>D: check the status
        D-->>F: still working
        F-->>U: not yet
    end

    A-->>F: ✅ the image is done
    F->>D: store the image + result
    F-->>N: completed + image URL
    N-->>U: 🖼️ display the image

    Note over U,A: 🔴 The whole asynchronous design exists<br/>for ONE reason: the AI is slow and everything<br/>else is fast. Get the real number from 03.
```

> ⚠️ The *accept-then-poll* pattern is an **`AI Recommendation`** — it is **not** drawn in the images. But it is forced by physics: a browser cannot hold an HTTP connection open for a minute-long GPU job. **The alternative — a blocking request — will fail with a 504 the first time a generation runs long.**

---

## 5. Parallel vs sequential work

**Who can work at the same time as whom.** The green band is where four people build simultaneously.

```mermaid
gantt
    title Development timeline — parallel work begins at CP-2
    dateFormat YYYY-MM-DD
    axisFormat %d %b

    section 🔁 Shared
    Requirement analysis (all 5)      :done, s1, 2026-07-14, 3d
    System planning · API contract    :crit, s2, after s1, 4d
    CP-2 · CONTRACT FROZEN            :milestone, crit, cp2, after s2, 0d

    section 👤 P1 UX/UI Frontend
    Wireframes + design system        :active, p1a, after s1, 5d
    CP-4 Mockups approved             :milestone, after p1a, 0d
    Build pages (Bootstrap · JS)      :p1b, after cp2, 10d
    Integrate with the real API       :p1c, after p2b, 4d

    section 👤 P2 Flask Backend
    Auth · API · DB · Logging         :p2b, after cp2, 12d
    Integrate with the AI Server      :crit, p2c, after p3b, 4d

    section 👤 P3 AI Engineer
    🔴 VERIFY THE GPU (day 1!)        :crit, p3a, 2026-07-14, 1d
    Forge AI · LoRA · Queue           :p3b, after cp2, 11d
    Test its own API (ทดสอบ API)      :p3c, after p3b, 2d

    section 👤 P4 QA / DevOps
    Write the test plan               :p4a, after cp2, 5d
    System · load · failure testing   :p4b, after p2c, 6d
    Deploy · dashboard · backup       :p4c, after p4b, 5d
    Manuals                           :p4d, after p4b, 4d

    section 👤 P5 Reverse Proxy
    Network · static IPs · ping test  :crit, p5a, after s2, 3d
    Nginx routing                     :p5b, after p5a, 3d
    📌 Then HELP OTHERS (light load)  :p5c, after p5b, 12d

    section 🎯 Milestones
    M4 · End-to-end path works        :milestone, crit, after p1c, 0d
    M6 · Deployed                     :milestone, after p4c, 0d
```

**Three things this chart tells you that a task list cannot:**
1. **P3 verifies the GPU on day 1** — before anything else, because everything depends on it.
2. **Nothing parallel happens before CP-2.** The contract is not paperwork; it is the starting gun.
3. **P5 finishes early and then helps** — exactly as `2.png` instructs (*"ช่วยงานส่วนอื่น เพราะภาระงานต่ำ"*) 📌.

---

## 6. The agent working loop

**How any one of the five agents takes a task from inbox to handover.** Identical for all five.

```mermaid
flowchart TD
    A["📥 1 · Receive the task"] --> B{"Does it touch files<br/>I <b>own</b>?"}
    B -->|No| B1["🚫 <b>REJECT</b><br/>Tell the Master who owns it.<br/><i>Following an out-of-scope order<br/>is how the ownership map dies.</i>"]
    B1 --> END1([Returned])

    B -->|Yes| C["🔍 2 · Analyze<br/>Re-read the contract.<br/><b>Never guess a field name.</b>"]
    C --> D{"Can I answer<br/>every question<br/>from the contract?"}
    D -->|No| D1["❓ ASK NOW.<br/><i>A question before coding costs<br/>5 minutes. After coding, a day.</i>"]
    D1 --> C

    D -->|Yes| E["📝 3 · Plan<br/>State: files, approach,<br/>and how I'll mock<br/>what doesn't exist yet"]
    E --> F["🔨 4 · Build"]
    F --> G["🧪 5 · Test"]
    G --> H{"Do my own tests<br/>pass?"}
    H -->|No| F

    H -->|Yes| I["📄 6 · Document<br/>Contract · schema · design system"]
    I --> J["✅ 7 · Run MY Quality Checklist"]
    J --> K{"<b>Every</b> box ticked?<br/><i>not most — every</i>"}
    K -->|No| F

    K -->|Yes| L["📊 8 · Completion report<br/>in my own format"]
    L --> M["🤝 9 · HAND OVER"]
    M --> N{"Does the next agent have:<br/>branch · files · how to run it ·<br/>a <b>working example</b> ·<br/>what is NOT finished?"}
    N -->|No| N1["⛔ Not a handover.<br/><i>'I pushed it' is not a handover.</i>"]
    N1 --> M
    N -->|Yes| END2([✅ DONE])

    style B1 fill:#ffcdd2,stroke:#b71c1c,color:#000
    style D1 fill:#fff3e0,stroke:#e65100,color:#000
    style N1 fill:#ffcdd2,stroke:#b71c1c,color:#000
    style END2 fill:#c8e6c9,color:#000
```

---

## 7. The Master Agent coordination loop

```mermaid
flowchart LR
    A["📚 Read all 8 files<br/>workflow · 5 agents ·<br/>machines · rules"] --> B["📍 Where are we?<br/>Stage · checkpoint · milestone"]
    B --> C["📋 What is outstanding?"]
    C --> D["✂️ Decompose<br/><i>one task = one agent</i>"]
    D --> E["🔗 Dependencies OK?"]
    E --> F["🔒 Locks clear?"]
    F --> G["🔀 What can go<br/>in PARALLEL?"]
    G --> H["📤 DISPATCH"]
    H --> I["👀 Monitor<br/>unblock · chase"]
    I --> J["🔍 Review against<br/>the agent's checklist"]
    J --> K{"Pass?"}
    K -->|No| L["❌ Reject —<br/>name the exact item"]
    L --> I
    K -->|Yes| M["✅ Done · release lock"]
    M --> N{"Checkpoint?"}
    N -->|No| C
    N -->|Yes| O["📊 Status report<br/>Advance the milestone"]
    O --> B

    P["🚫 <b>THE PRIME DIRECTIVE</b><br/>The Master NEVER writes code.<br/>Its output is only:<br/>an assignment · a decision ·<br/>an approval · a report."]

    style P fill:#ffcdd2,stroke:#b71c1c,stroke-width:3px,color:#000
    style H fill:#c8e6c9,color:#000
```

---

## 8. Task routing — which agent gets this?

```mermaid
flowchart TD
    T["📋 A task arrives"] --> Q1{"Does it touch<br/><b>two</b> agents' files?"}
    Q1 -->|Yes| SPLIT["✂️ SPLIT IT<br/>= two tasks + a contract"]
    SPLIT --> T

    Q1 -->|No| Q2{"What does it<br/>involve?"}

    Q2 -->|"a screen · CSS · Bootstrap ·<br/>a mockup · browser JS"| A1["👤 <b>01</b><br/>UX/UI Frontend"]
    Q2 -->|"a Flask route · auth · the API ·<br/>the database · logging"| A2["👤 <b>02</b><br/>Flask Backend"]
    Q2 -->|"calling the AI Server"| A2
    Q2 -->|"image generation · editing ·<br/>a model · LoRA · the GPU · the queue"| A3["👤 <b>03</b><br/>AI Engineer"]
    Q2 -->|"testing the AI's OWN API 📌<br/>(ทดสอบ API)"| A3
    Q2 -->|"system testing · a defect ·<br/>deployment · dashboard · backup ·<br/>the manuals"| A4["👤 <b>04</b><br/>QA / DevOps"]
    Q2 -->|"Nginx · routing · IPs ·<br/>ports · firewall"| A5["👤 <b>05</b><br/>Reverse Proxy"]
    Q2 -->|"changing the API contract"| M["🔶 <b>02 proposes</b><br/>→ Master approves<br/>→ 01 and 03 notified"]

    A5 --> Q3{"Does Person 5<br/>exist? ⚠️"}
    Q3 -->|"No (ถ้ามี)"| A4

    style SPLIT fill:#e1f5fe,stroke:#01579b,color:#000
    style M fill:#ffe0b2,stroke:#e65100,color:#000
```

> **Two routing rules people get wrong:**
> • **Calling the AI Server is a *Backend* task**, not an AI task. The AI Engineer builds the service; the Backend calls it. 📌
> • **Testing the AI's own API is an *AI Engineer* task**, not a QA task — `2.png` assigns *ทดสอบ API* to คนที่ 3. 📌

---

## 9. The integration flow

**Strictly ordered. This is where projects die.**

```mermaid
flowchart TD
    START(["CP-5 · each part works alone"]) --> I1

    I1["<b>6A · Backend ↔ Database</b><br/>👤 P2<br/><i>data survives a restart</i>"]
    I1 --> C1{"Persists?"}
    C1 -->|No| I1
    C1 -->|Yes| I2

    I2["<b>6B · Backend ↔ AI Server</b><br/>👤 P2 + P3<br/>🔴 <b>THE HIGHEST-RISK STEP</b><br/>the first cross-machine call<br/>.20 → .30"]
    I2 --> C2{"Does .20 reach .30<br/>and get an image?"}
    C2 -->|No| I2
    C2 -->|Yes| M3{{"🎯 M3 · CP-6a<br/>first cross-machine call"}}

    M3 --> I3["<b>6C · Frontend ↔ Backend</b><br/>👤 P1 + P2<br/><i>delete the mocks</i>"]
    I3 --> C3{"Real data<br/>renders?"}
    C3 -->|No| I3
    C3 -->|Yes| I4

    I4["<b>6D · Nginx front door</b><br/>👤 P5<br/><i>one address for the whole app</i>"]
    I4 --> C4{"Reachable through<br/>one address?<br/>No 504 on a slow<br/>generation?"}
    C4 -->|No| I4
    C4 -->|Yes| I5

    I5["<b>6E · Full-path smoke test</b><br/>👤 P4<br/>every arrow in 1.png"]
    I5 --> M4{{"🎯 M4 · CP-6<br/><b>END-TO-END PATH WORKS</b>"}}

    style I2 fill:#ffcdd2,stroke:#b71c1c,stroke-width:3px,color:#000
    style M4 fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px,color:#000
```

> 🔴 **Schedule 6B early — on stubs if you must.** It is the first moment two separately-built machines must agree, and it crosses a network boundary *and* a slow-job boundary at the same time. Teams that leave it until the end discover both problems in the same week, with no time left.

---

## 10. Testing flow

```mermaid
flowchart TD
    A["📌 API_CONTRACT.md<br/>frozen at CP-2"] --> B["👤 P4 writes the test cases<br/><b>BEFORE the code exists</b>"]

    B --> C["<b>1 · Unit</b><br/>each agent, own code"]
    C --> D["<b>2 · Contract</b><br/>👤 P4<br/><i>does every endpoint match<br/>the contract EXACTLY?</i>"]
    D --> E["<b>3 · Integration</b><br/>👤 P4 + the two owners<br/>Frontend ↔ Backend ↔ AI"]
    E --> F["<b>4 · End-to-end</b><br/>👤 P4<br/>every arrow in 1.png"]
    F --> G["<b>5 · Load</b><br/>👤 P4<br/>🔴 <b>concurrent generations</b><br/><i>does the Queue hold?</i> 📌"]
    G --> H["<b>6 · Failure drill</b><br/>👤 P4<br/>switch each machine OFF<br/>and watch"]
    H --> I["<b>7 · Restore test</b><br/>👤 P4<br/>🔴 <i>an untested backup<br/>is not a backup</i>"]

    I --> J{"Any critical<br/>or high defects?"}
    J -->|Yes| K["🐛 Route each defect<br/>to its <b>OWNER</b><br/>🚫 P4 never patches<br/>other agents' code"]
    K --> C
    J -->|No| L{{"✅ CP-7 · TESTED<br/>deployment is authorised"}}

    style G fill:#fff3e0,stroke:#e65100,color:#000
    style I fill:#fff3e0,stroke:#e65100,color:#000
    style K fill:#ffcdd2,stroke:#b71c1c,color:#000
    style L fill:#c8e6c9,color:#000
```

---

## 11. Deployment flow

**Start what others depend on, first.**

```mermaid
flowchart TD
    A(["✅ CP-7 · green test report"]) --> B["🔖 Tag the release<br/>freeze the branch"]

    B --> C["1️⃣ <b>Database</b><br/>MAC-02 · 192.168.1.20 📌"]
    C --> D["2️⃣ <b>AI Server</b><br/>WINDOWS-PC-01 · 192.168.1.30 📌<br/><i>Forge AI + models</i>"]
    D --> E["3️⃣ <b>Flask Backend</b><br/>MAC-02 · 192.168.1.20 📌"]
    E --> F["4️⃣ <b>Frontend + Nginx</b><br/>MAC-01 · 192.168.1.10 📌<br/><i>the front door goes LAST</i>"]

    F --> G["🔥 Smoke test<br/>from a real browser"]
    G --> H{"Full path<br/>works?"}
    H -->|No| ROLL["⏮️ ROLLBACK<br/><i>see chart 12</i>"]
    H -->|Yes| I["📊 Bring up the Dashboard 📌<br/>every machine reports healthy"]

    I --> J["💾 Run the first Backup 📌<br/>DB + generated images<br/>MAC-02 → WINDOWS-PC-02"]
    J --> K["🔄 <b>TEST THE RESTORE</b><br/>🔴 <i>a backup that has never been<br/>restored is a hope, not a backup</i>"]
    K --> L{"Restore<br/>works?"}
    L -->|No| J
    L -->|Yes| M["📖 Publish the manuals 📌<br/>User + Admin"]

    M --> N["🔌 Reboot ALL machines"]
    N --> O{"Does everything<br/>come back<br/>unaided?"}
    O -->|No| P["Fix the startup order<br/>and the services"]
    P --> N
    O -->|Yes| Q{{"🎯 M6 · DEPLOYED"}}

    style ROLL fill:#ffcdd2,stroke:#b71c1c,color:#000
    style K fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#000
    style Q fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px,color:#000
```

**The deployment order is not arbitrary:** the database has no dependencies, so it starts first. The front door starts last — because there is no point opening it onto a system that is not yet awake.

---

## 12. Failure and rollback

### 12.1 Which machine died?

```mermaid
flowchart TD
    A["🚨 Something is broken"] --> B{"Which machine<br/>is down?"}

    B -->|"MAC-01<br/>Nginx + Frontend"| C["🔴 <b>THE WHOLE SITE<br/>IS UNREACHABLE</b><br/><br/>✅ but nothing irreplaceable<br/>lives here<br/><br/><b>Fix:</b> nginx.conf is in Git.<br/>Stand it up elsewhere.<br/><b>Recovery: fast</b>"]

    B -->|"MAC-02<br/>Flask + DB"| D["🔴 <b>THE WORST FAILURE</b><br/>No login · no data · no generation<br/><br/>💀 the live data lives HERE<br/><br/><b>Fix:</b> restore the DB from the<br/>WINDOWS-PC-02 backup.<br/><b>Recovery is only as good as<br/>the last backup.</b>"]

    B -->|"WINDOWS-PC-01<br/>Forge AI"| E["🟠 <b>Generation fails</b><br/><br/>✅ login · gallery · history all work<br/><br/><b>Fix:</b> redeploy from Git,<br/>re-download the models.<br/>The Backend must show a clear<br/>error — <b>NOT hang</b>."]

    B -->|"WINDOWS-PC-02<br/>QA + Backup"| F["🟡 <b>Production is unaffected</b><br/><br/>⚠️ but the backup destination<br/>is gone<br/><br/><b>Fix:</b> back up elsewhere<br/>until it returns."]

    style C fill:#ffcdd2,color:#000
    style D fill:#ff8a80,stroke:#b71c1c,stroke-width:3px,color:#000
    style E fill:#fff3e0,color:#000
    style F fill:#f1f8e9,color:#000
```

> **This layering is deliberate:** the machine holding the irreplaceable data (`MAC-02`) is **not** the one exposed to the public (`MAC-01`), and the machine that watches everything (`WINDOWS-PC-02`) **cannot take production down**. Preserve that property.

### 12.2 The rollback procedure

```mermaid
flowchart LR
    A["🚨 P0<br/>production down<br/>or data at risk"] --> B["🛑 <b>STOP ALL WORK</b>"]
    B --> C["👤 <b>P4 executes</b><br/><i>not the agent who broke it —<br/>they are the last person who<br/>should touch production now</i>"]
    C --> D["⏮️ Check out the<br/>last known-good tag"]
    D --> E["🚀 Redeploy the<br/>affected machine"]
    E --> F["✅ Verify healthy"]
    F --> G["🔬 <b>THEN</b> diagnose —<br/>on a branch,<br/>never on the live system"]

    style B fill:#ffcdd2,stroke:#b71c1c,stroke-width:3px,color:#000
    style F fill:#c8e6c9,color:#000
```

**Restore service first. Understand it second.**

### 12.3 🔴 The one true emergency

```mermaid
flowchart TD
    A["👤 P3 · Day 1<br/>run <b>nvidia-smi</b><br/>on both Windows machines"] --> B{"Is there a discrete<br/>NVIDIA GPU?"}
    B -->|"✅ Yes"| C["Record the model + VRAM<br/>in NETWORK_PLAN.md<br/><br/>→ proceed with the plan"]
    B -->|"❌ No"| D["🔴 <b>STOP THE PROJECT PLAN</b><br/><br/>Forge AI needs CUDA.<br/>CUDA needs NVIDIA.<br/>macOS cannot provide it.<br/><br/><b>The AI Server as designed<br/>is not buildable.</b>"]
    D --> E["📢 <b>Escalate to the human team<br/>IMMEDIATELY</b><br/><br/>🚫 Do NOT let the other agents<br/>keep building against an AI Server<br/>that will never exist."]
    E --> F["Re-scope:<br/>• external GPU service?<br/>• image editing only (CPU)?<br/>• a different engine?"]

    style D fill:#ff8a80,stroke:#b71c1c,stroke-width:4px,color:#000
    style E fill:#ffcdd2,stroke:#b71c1c,stroke-width:3px,color:#000
    style C fill:#c8e6c9,color:#000
```

> ⚠️ **No image states any hardware specification.** This is **assumption A1** in `COMPUTER_ROLE_ALLOCATION.md`, and it is the only failure in the project that **cannot be fixed by writing more code** — and the only one that gets dramatically cheaper the earlier it is found. **It costs ten minutes to check.**

---

## 13. Git branch flow

```mermaid
gitGraph
    commit id: "init"
    branch develop
    checkout develop
    commit id: "scaffold"

    branch feature/reverse-proxy
    checkout feature/reverse-proxy
    commit id: "network + IPs"
    commit id: "nginx routing"
    checkout develop
    merge feature/reverse-proxy

    branch feature/backend
    checkout feature/backend
    commit id: "API contract"
    commit id: "auth"
    commit id: "database"

    checkout develop
    branch feature/ai-engineer
    checkout feature/ai-engineer
    commit id: "forge + queue"
    commit id: "AI API tested"

    checkout develop
    branch feature/ux-ui-frontend
    checkout feature/ux-ui-frontend
    commit id: "design system"
    commit id: "pages on mocks"

    checkout develop
    merge feature/backend
    merge feature/ai-engineer
    merge feature/ux-ui-frontend

    branch feature/qa-devops
    checkout feature/qa-devops
    commit id: "tests + deploy"
    checkout develop
    merge feature/qa-devops

    checkout main
    merge develop tag: "v1.0"
```

**Branch names come from the exact role names in `2.png`** 📌. Note the shape: three feature branches run **side by side** off `develop` — that is CP-2 doing its job.

---

## 14. The life of a single task

```mermaid
stateDiagram-v2
    [*] --> BACKLOG: identified

    BACKLOG --> ASSIGNED: Master dispatches<br/>(deps satisfied · locks clear)
    ASSIGNED --> REJECTED: not my files
    REJECTED --> BACKLOG: re-routed to the owner

    ASSIGNED --> IN_PROGRESS: agent accepts
    IN_PROGRESS --> BLOCKED: missing input<br/>or an unanswered question
    BLOCKED --> IN_PROGRESS: Master unblocks
    BLOCKED --> ESCALATED: blocked > 1 session
    ESCALATED --> IN_PROGRESS: resolved

    IN_PROGRESS --> IN_REVIEW: checklist complete<br/>+ PR opened
    IN_REVIEW --> IN_PROGRESS: ❌ rejected<br/>(a named checklist item failed)
    IN_REVIEW --> MERGED: ✅ approved

    MERGED --> HANDED_OVER: next agent has branch,<br/>files, a WORKING example,<br/>and what is NOT finished
    HANDED_OVER --> DONE: lock released

    DONE --> [*]

    note right of BLOCKED
        A blocked agent is the
        MASTER's problem, not theirs.
        Report it immediately.
    end note

    note right of IN_REVIEW
        "Every box ticked" — not most.
        "It works on my machine"
        is NOT done. There are four
        machines.
    end note
```

---

## Quick index — which chart do I need?

| I want to… | Chart |
|---|---|
| See the whole project at a glance | **1** |
| Understand how tasks get created and assigned | **2**, **7** |
| Understand how the app actually works at runtime | **3**, **4** |
| Know who can work at the same time | **5** |
| Know what to do with the task I was just given | **6** |
| Work out whose job something is | **8** |
| Connect the pieces together | **9** |
| Know what to test and when | **10** |
| Ship it | **11** |
| Deal with something breaking | **12** |
| Use Git correctly | **13** |
| Know what state my task is in | **14** |

---

*Architecture from `Work/1.png`. Roles from `Work/2.png`. Machines from `Work/3.png`. Anything marked 🤖 is an AI recommendation. Anything marked ⚠️ is not stated in any image and must be confirmed by the team.*
