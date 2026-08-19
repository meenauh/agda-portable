> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-01b-continue'
description: 'Resume an interrupted Game Brief workflow from the last completed step'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-01b-continue.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'
---

# Step 1B: Workflow Continuation

## STEP GOAL:

Resume the Game Brief workflow from where it was left off, ensuring smooth continuation with full context restoration.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with CONTINUE, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a veteran game designer facilitator collaborating with a creative peer
- We engage in collaborative dialogue, not command-response
- Resume workflow from exact point where it was interrupted

### Step-Specific Rules:

- FOCUS on understanding where we left off and continuing appropriately
- FORBIDDEN to modify content completed in previous steps
- Only reload documents that were already tracked in `inputDocuments`

## EXECUTION PROTOCOLS:

- Show your analysis of current state before taking action
- Keep existing frontmatter `stepsCompleted` values
- Only load documents that were already tracked in `inputDocuments`
- FORBIDDEN to discover new input documents during continuation

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Analyze Current State

**State Assessment:**
Review the frontmatter to understand:

- `stepsCompleted`: Which steps are already done
- `lastStep`: The most recently completed step number
- `inputDocuments`: What context was already loaded
- `documentCounts`: brainstorming, research, notes counts
- `game_name`: The game name (if set)
- All other frontmatter variables

### 2. Restore Context Documents

**Context Reloading:**

- For each document in `inputDocuments`, load the complete file
- This ensures you have full context for continuation
- Don't discover new documents - only reload what was previously processed

### 3. Present Current Progress

**Progress Report to User:**
"Welcome back {{user_name}}! I'm resuming our Game Brief collaboration for {{game_name or project_name}}.

**Current Progress:**

- Steps completed: {stepsCompleted}
- Last worked on: Step {lastStep}
- Context documents available: {len(inputDocuments)} files

**Document Status:**

- Current Game Brief is ready with all completed sections
- Ready to continue from where we left off

Does this look right, or do you want to make any adjustments before we proceed?"

### 4. Determine Continuation Path

**Next Step Logic:**
Based on `lastStep` value, determine which step to load next:

- If `lastStep = 1` -> Load `./step-02-vision.md`
- If `lastStep = 2` -> Load `./step-03-market.md`
- If `lastStep = 3` -> Load `./step-04-fundamentals.md`
- If `lastStep = 4` -> Load `./step-05-scope.md`
- If `lastStep = 5` -> Load `./step-06-references.md`
- If `lastStep = 6` -> Load `./step-07-content.md`
- If `lastStep = 7` -> Load `./step-08-core-loop.md`
- If `lastStep = 8` -> Load `./step-09-mda-motivation.md`
- If `lastStep = 9` -> Load `./step-10-pillars.md`
- If `lastStep = 10` -> Load `./step-11-feasibility-mvp.md`
- If `lastStep = 11` -> Load `./step-12-complete.md`
- If `lastStep = 12` -> Workflow already complete

### 5. Handle Workflow Completion

**If workflow already complete (`lastStep = 12`):**
"Great news! It looks like we've already completed the Game Brief workflow for {{game_name}}.

The final document is ready at `{outputFile}` with all sections completed.

Would you like me to:

- Review the completed brief with you
- Continue to systems mapping
- Start a new brief revision

What would be most helpful?"

### 6. Present MENU OPTIONS

**If workflow not complete:**
Display: "Ready to continue with Step {nextStepNumber}?

**Do not present per-section options. Update `preproduction/design.md` and continue the stage.**

#### Menu Handling Logic:

- Do not use CONTINUE inside the stage; update `preproduction/design.md`, frontmatter, and continue to the next step.
- IF Any other comments or queries: respond and redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [current state confirmed], will you then load and read fully the appropriate next step file to resume the workflow.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All previous input documents successfully reloaded
- Current workflow state accurately analyzed and presented
- User confirms understanding of progress before continuation
- Correct next step identified and prepared for loading

### SYSTEM FAILURE:

- Discovering new input documents instead of reloading existing ones
- Modifying content from already completed steps
- Loading wrong next step based on `lastStep` value
- Proceeding without user confirmation of current state

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.



