# my-ai-workforce
My AI Workforce showcases a portfolio of AI agents, designed to automate business processes, enhance decision-making, and drive operational efficiency.  Each agent demonstrates practical applications of AI through real-world use cases, architecture, and implementation approaches.


## System Overview: Research and Content Production Agent

The Research and Content Production Agent is the two-stage pipeline that turns a row logged in Kryste's Research List.xlsx into a finished, client-ready deliverable. It is made up of two separate skills that hand off to each other: the **Research Agent**, which finds and verifies facts, and the **Writer of Research Agent**, which turns those verified facts into polished documents, decks, and other output. Neither skill does the other's job — the Research Agent never produces a client deliverable, and the Writer of Research Agent never originates new facts of its own.

### Where it lives

Everything for this pipeline lives in one folder on Kryste's own computer, reached through the desktop device bridge:

`C:\Users\klwie\OneDrive\Desktop\Claude Research and Content Production Agent`

That folder holds `Research List.xlsx` (the single source of truth for what's due and what's done), an `Archive` folder, a `Branding` folder, a `Deliverable Templates` folder, and one subfolder per completed research topic, named from each row's Folder Name.

### Stage 1 — Research Agent

Reads `Research List.xlsx`, finds rows where Date / Time Entered has passed and Research Completed Date is blank, researches each one using tiered, verifiable sources, and writes the findings to a structured Markdown file in a new folder named after the row's Folder Name. It produces only the verified source material, never the final deliverable. When a row's research is complete, it stamps that row's Research Completed Date.

### Stage 2 — Writer of Research Agent

Picks up where the Research Agent leaves off. It finds rows where Published Date is blank, reads the `.md` research file from that row's folder, and generates whichever deliverables are marked in the row's output-type columns — Word document, deck, training material, process document, and so on — following the KrysteCo Brand Style Guide. Every generated file is validated (structure, citations, placeholder text, visual render) before it counts as done. Once every marked deliverable for a row passes validation, it stamps that row's Published Date.

### How a row moves through the pipeline

Step 1: A row is logged in `Research List.xlsx` with a topic, audience, and one or more deliverable types marked.

Step 2: Research Agent picks it up once its entry time has passed, researches it, and writes a `.md` file into a new folder — Research Completed Date gets stamped.

Step 3: Writer of Research Agent picks up the same row once its `.md` file exists, generates the marked deliverables into that same folder, and validates each one.

Step 4: Once every marked deliverable passes validation, Writer of Research Agent stamps Published Date and the row is complete.

### Shared rules across both stages

No guessing: facts that can't be verified, blank Folder Names, naming collisions, and structural changes to the spreadsheet all stop the run and ask Kryste rather than proceeding on an assumption.

Local access required: both skills only run with the desktop app open and the working folder connected — neither proceeds against a cloud-only guess at the file location.

Central Time, computed live: dates are written in the sheet's existing Central Time text format, computed from the real current time, not the model's training cutoff or the container's UTC clock.

No partial credit: Research Completed Date and Published Date are only stamped once every relevant piece of work for that row has actually succeeded.

### Where to find the detail

The full step-by-step instructions for each stage live in agents/Research Agent.txt and agents/Writer of Research Agent.txt. This overview is also available as agents/Research and Content Production Agent.txt.
