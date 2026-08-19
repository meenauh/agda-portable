> AGDA file-first override: write or update `preproduction/design.md` immediately when the player's answer gives enough information. Do not wait for per-section CONTINUE, do not present REFINE/CONTINUE menus inside this stage, and do not post full drafts into chat unless requested. CONTINUE is only for the stage boundary after the complete `preproduction/design.md` is ready.

---
name: 'step-06-references'
description: 'Define inspiration games and design differentiators'

# Path Definitions
workflow_path: '{installed_path}'

# File References
thisStepFile: './step-06-references.md'
nextStepFile: './step-07-content.md'
workflowFile: '{workflow_path}/workflow.md'
outputFile: 'preproduction/design.md'

# Task References
---

# Step 6: Reference Framework

**Progress: Step 6 of 12** - Next: Content and Production

## STEP GOAL:

Identify inspiration games (what you're drawing from and NOT taking) and define concrete design differentiators that make this game worth making.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with CONTINUE, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- NEVER mention time estimates
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a veteran game designer facilitator collaborating with a creative peer
- Challenge "just better" thinking
- Push for genuine, specific differentiation

### Step-Specific Rules:

- Focus on what makes this game unique
- FORBIDDEN to generate references without real user input
- Validate that differentiators are concrete and achievable
- Understand both what you're taking AND what you're avoiding

## EXECUTION PROTOCOLS:

- Show your analysis before taking any action
- Do not present per-section REFINE/CONTINUE menus; update preproduction/design.md and continue the guided stage.
- Save/update preproduction/design.md immediately after the answer provides enough information.
- Update frontmatter `stepsCompleted: [1, 2, 3, 4, 5, 6]` before loading next step

## File Update
- **REFINE**: Challenge differentiation claims
- **CONTINUE**: Save the content and proceed

## Sequence of Instructions (Do not deviate, skip, or optimize)

### 1. Inspiration Games

**Guide user through references:**

"Let's identify the games that inspire {{game_name}}.

**For each inspiration game, I want to know:**

1. **What game?**
2. **What are you taking?** (mechanics, feel, art style, structure)
3. **What are you NOT taking?** (equally important!)

**Example:**

- 'From Hades: the combat feel and build variety'
- 'NOT from Hades: the roguelike structure or the dialogue system'

What 3-5 games inspire {{game_name}}, and what specifically are you drawing from each?"

### 2. Design Neighbor Analysis

**Explore nearby designs:**

"Now let's analyze nearby games as design references.

**Competition Questions:**

- **Same player itch:** Games that create a similar experience
- **What they do well:** Why do those design choices work?
- **What they do poorly:** Where does the experience fall short?
- **Design contrast:** What should feel meaningfully different in your game?

Which nearby games should inform the design of {{game_name}}?"

### 3. Differentiators

**Define unique value:**

"Now for the critical question: What makes {{game_name}} genuinely different?

**Differentiation Test:**

A strong differentiator passes ALL of these:

1. Is it concrete and achievable?
2. Does it matter to the intended player experience?
3. Is it visible in actual play?
4. Would you still make the game without it?

**Challenge 'just better' thinking:**
'Better graphics' or 'more content' aren't differentiators - they're expectations.

What 2-4 things make {{game_name}} genuinely different and worth players' attention?"

### 4. Generate References Content

Based on the conversation, prepare the content:

```markdown
## Reference Framework

### Inspiration Games

{{for_each_inspiration}}
**{{game_name}}**

- Taking: {{what_taking}}
- Not Taking: {{what_avoiding}}
  {{/for_each}}

### Design Neighbors

{{design_neighbors}}

**Reference Strengths:**
{{what_references_do_well}}

**Reference Weaknesses:**
{{where_references_fall_short}}

### Key Differentiators

{{differentiators_with_descriptions}}

**Design Promise:**
{{one_sentence_design_promise}}
```

### 5. Present Content and Menu

Show the generated content to the user and present:

"I've drafted the Reference Framework section based on our conversation.

**Here's what I'll add to the document:**

[Show the complete markdown content from step 4]

**Validation Check:**

- Are differentiators genuine, not just features?
- Do the design neighbors clarify what to take and avoid?
- Are inspirations specific about what you're taking vs avoiding?

**Do not present per-section options. Update `preproduction/design.md` and continue the stage.**
Edit/refinement: apply corrections directly to `preproduction/design.md`.
Stage boundary: use CONTINUE only after the complete game-conception stage is ready.

### 6. Handle Menu Selection

#### If the player refines:

- Ask targeted follow-up questions about weak, vague, risky, or incomplete parts of the current draft.
- Revise the current content in place using the user's answers.
- Apply the refinement directly to preproduction/design.md and continue the stage.

#### Do not use CONTINUE inside the stage:

- Append the final content to `{outputFile}`
- Replace the existing Reference Framework section in `{outputFile}` if it already exists.
- Update frontmatter: `stepsCompleted: [1, 2, 3, 4, 5, 6]`
- Load `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [CONTINUE option] is selected and [references content saved with frontmatter updated], will you then load and read fully `{nextStepFile}`.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- 3-5 inspiration games with specific takeaways
- Design neighbors analyzed with strengths and weaknesses
- Differentiators are concrete and achievable
- Unique value proposition is clear
- REFINE/CONTINUE menu presented and handled correctly
- Frontmatter updated with stepsCompleted: [1, 2, 3, 4, 5, 6]

### SYSTEM FAILURE:

- Generating references without user input
- Generic differentiators like "better gameplay"
- Missing the "not taking" aspect of inspirations
- Waiting for per-section approval instead of updating preproduction/design.md
- Waiting for per-section CONTINUE before writing or proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.




