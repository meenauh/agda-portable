---
name: 'step-02-context'
description: 'Load game-specific brainstorming context and techniques'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-02-context.md'
nextStepFile: './step-03-ideation.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: '{output_folder}/brainstorming-session-{date}.md'

# Context Files
gameContext: '{workflow_path}/game-context.md'
gameBrainMethods: '{workflow_path}/game-brain-methods.csv'
coreBrainstorming: 'skill:bmad-brainstorming'
---

# Step 2: Load Context

**Progress: Step 2 of 4** - Next: Ideation Session

## STEP GOAL:

Load game-specific brainstorming context and techniques to guide the ideation session. Merge game techniques with core brainstorming methods.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with CONTINUE, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- NEVER mention time estimates
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a creative game design facilitator
- Game-specific techniques enhance standard brainstorming
- Understand various ideation methods deeply

### Step-Specific Rules:

- Load all context files completely
- Present technique options to user
- Let user select preferred approach

## EXECUTION PROTOCOLS:

- Show your analysis before taking any action
- Present REFINE/CONTINUE menu after context loaded
- ONLY proceed when user chooses CONTINUE
- Update frontmatter `stepsCompleted: [1, 2]` before loading next step

## COLLABORATION MENU (REFINE/CONTINUE):

- **REFINE**: Explore technique combinations
- **CONTINUE**: Confirm context and proceed

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Load Game Context

**Load the game context document:**

Read `{gameContext}` to understand:

- Focus areas for game ideation
- Key considerations for game design
- Recommended techniques
- Output structure guidance

### 2. Load Game Brain Methods

**Load game-specific techniques:**

Read `{gameBrainMethods}` CSV to load:

- MDA Framework exploration
- Core loop brainstorming
- Player fantasy mining
- Genre mashup
- And other game-specific methods

### 3. Present Available Techniques

"**Game Brainstorming Techniques Loaded!**

I've loaded game-specific brainstorming methods:

**Conceptual Techniques:**

- **MDA Framework** - Mechanics, Dynamics, Aesthetics exploration
- **Player Fantasy Mining** - What fantasy does the player fulfill?
- **Core Loop Design** - Define the central gameplay loop
- **Genre Mashup** - Combine unexpected genres

**Experience Techniques:**

- **Emotion Mapping** - Target emotions throughout gameplay
- **Moment Design** - Plan memorable peak moments
- **Flow Analysis** - Balance challenge and skill

**Practical Techniques:**

- **Constraint Box** - Creative limits spark innovation
- **Reference Blending** - Combine inspiration sources
- **What If Scenarios** - Explore radical possibilities

**How would you like to brainstorm?**

1. **Guided** - I'll walk you through techniques one by one
2. **Selective** - Choose specific techniques to use
3. **Freeform** - Open exploration with techniques as needed
4. **YOLO** - Let me drive the session with all techniques

Your preference:"

### 4. Capture User Preference

**Based on selection:**

- **Guided**: Prepare structured technique sequence
- **Selective**: Present technique menu for selection
- **Freeform**: Prepare all techniques for on-demand use
- **YOLO**: Plan comprehensive technique coverage

### 5. Generate Context Section

Based on the conversation, prepare the content:

```markdown
## Brainstorming Approach

**Selected Mode:** {{selected_mode}}

**Techniques Available:**
{{technique_list}}

**Focus Areas:**
{{focus_areas_from_context}}
```

### 6. Present Content and Menu

Show the loaded context and present:

"I've prepared the brainstorming context.

**Here's what I'll add to the document:**

[Show the complete markdown content from step 5]

**Ready to start ideation?**

**Select an Option:**
REFINE - Explore technique combinations
CONTINUE - Save this and move to Ideation Session (Step 3 of 4)"

### 7. Handle Menu Selection

#### IF REFINE:

- Ask targeted follow-up questions about weak, vague, risky, or incomplete parts of the current draft.
- Revise the current content in place using the user's answers.
- Return to the REFINE/CONTINUE menu.

#### IF CONTINUE:

- Append the context section to `{outputFile}`
- Update frontmatter: `stepsCompleted: [1, 2]`
- Load `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [context saved with frontmatter updated], will you then load and read fully `{nextStepFile}`.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Game context loaded completely
- Game brain methods loaded from CSV
- Techniques presented clearly
- User selected brainstorming approach
- REFINE/CONTINUE menu presented and handled correctly
- Frontmatter updated with stepsCompleted: [1, 2]

### SYSTEM FAILURE:

- Not loading context files
- Proceeding without user technique selection
- Not presenting REFINE/CONTINUE menu after context
- Proceeding without user selecting CONTINUE

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.



