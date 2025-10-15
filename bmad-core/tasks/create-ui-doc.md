<!-- Powered by BMAD™ Core -->

# Create UI Documentation from References (YAML Driven)

## ⚠️ CRITICAL EXECUTION NOTICE ⚠️

**THIS IS AN EXECUTABLE WORKFLOW - NOT REFERENCE MATERIAL**

When this task is invoked:

1. **DISABLE ALL EFFICIENCY OPTIMIZATIONS** - This workflow requires full user interaction
2. **MANDATORY STEP-BY-STEP EXECUTION** - Each section must be processed sequentially with user feedback
3. **ELICITATION IS REQUIRED** - When `elicit: true`, you MUST use the 1-9 format and wait for user response
4. **NO SHORTCUTS ALLOWED** - Complete documents cannot be created without following this workflow

**VIOLATION INDICATOR:** If you create a complete document without user interaction, you have violated this workflow.

## Critical: Reference Material Discovery

**BEFORE starting document generation, you MUST collect reference materials:**

### Ask the user to provide ONE of the following:

1. **Web URL(s)** - Link(s) to design systems, style guides, or UI documentation
2. **Local file path(s)** - Path(s) to existing design documents (markdown, PDF, images)
3. **Folder path** - Directory containing multiple reference documents
4. **Mixed references** - Combination of URLs, files, and folders

### Reference Collection Process:

1. **Request references from user:**
   ```
   Please provide reference materials for creating the UI documentation:
   - Web URLs (design systems, style guides, inspiration sites)
   - Local file paths (design documents, mockups, screenshots)
   - Folder paths (directories with multiple reference files)

   You can provide multiple references separated by commas or newlines.
   ```

2. **Process each reference:**
   - **For URLs**: Use WebFetch to extract content and design patterns
   - **For files**: Use Read to analyze content (supports markdown, images, PDFs)
   - **For folders**: Use Glob to find all relevant files, then read each

3. **Synthesize reference insights:**
   - Extract color schemes, typography choices, spacing patterns
   - Identify design principles and philosophies
   - Note component patterns and usage guidelines
   - Capture brand personality and tone

4. **Store insights for document generation:**
   - Create a reference summary to inform template population
   - Use insights to suggest defaults during elicitation
   - Reference source materials when presenting rationale

## Critical: Template Discovery

If a YAML Template has not been provided, list all templates from `.bmad-core/templates` or ask the user to provide another.

**Available UI Documentation Templates:**
- `design-principles-tmpl.yaml` - Comprehensive design checklist
- `style-guide-tmpl.yaml` - Visual design language specification

## CRITICAL: Mandatory Elicitation Format

**When `elicit: true`, this is a HARD STOP requiring user interaction:**

**YOU MUST:**

1. Present section content with insights from reference materials
2. Provide detailed rationale (explain trade-offs, assumptions, decisions made)
3. **Reference source materials** when suggesting defaults or patterns
4. **STOP and present numbered options 1-9:**
   - **Option 1:** Always "Proceed to next section"
   - **Options 2-9:** Select 8 methods from data/elicitation-methods
   - End with: "Select 1-9 or just type your question/feedback:"
5. **WAIT FOR USER RESPONSE** - Do not proceed until user selects option or provides feedback

**WORKFLOW VIOLATION:** Creating content for elicit=true sections without user interaction violates this task.

**NEVER ask yes/no questions or use any other format.**

## Processing Flow

1. **Collect reference materials** - URLs, files, or folders (MANDATORY FIRST STEP)
2. **Process references** - Extract design insights and patterns
3. **Parse YAML template** - Load template metadata and sections
4. **Set preferences** - Show current mode (Interactive), confirm output file
5. **Process each section:**
   - Skip if condition unmet
   - Check agent permissions (owner/editors) - note if section is restricted to specific agents
   - Draft content using section instruction + reference insights
   - Present content + detailed rationale + reference citations
   - **IF elicit: true** → MANDATORY 1-9 options format
   - Save to file if possible
6. **Continue until complete**

## Reference-Enhanced Rationale Requirements

When presenting section content, ALWAYS include rationale that explains:

- Trade-offs and choices made (what was chosen over alternatives and why)
- **How reference materials informed the choices**
- Key assumptions made during drafting
- Interesting or questionable decisions that need user attention
- Areas that might need validation
- **Citations to specific reference sources** (e.g., "Based on color palette from [reference URL]")

## Elicitation Results Flow

After user selects elicitation method (2-9):

1. Execute method from data/elicitation-methods
2. Present results with insights from references
3. Offer options:
   - **1. Apply changes and update section**
   - **2. Return to elicitation menu**
   - **3. Ask any questions or engage further with this elicitation**

## Agent Permissions

When processing sections with agent permission fields:

- **owner**: Note which agent role initially creates/populates the section
- **editors**: List agent roles allowed to modify the section
- **readonly**: Mark sections that cannot be modified after creation

**For sections with restricted access:**

- Include a note in the generated document indicating the responsible agent
- Example: "_(This section is owned by ux-expert and can only be modified by ux-expert)_"

## Reference Processing Examples

### Example 1: Web URL Reference
```
User: https://stripe.com/docs/design
Assistant: Fetching design system from Stripe...
- Primary color: #635BFF (vibrant purple)
- Typography: Inter font family
- Design principle: "Simple, clear, and purposeful"
I'll use these insights when creating your design principles and style guide.
```

### Example 2: Local File Reference
```
User: /path/to/mockup.png
Assistant: Reading design mockup...
- Color scheme: Blues and grays with orange accents
- Typography: Modern sans-serif, generous spacing
- Layout: Card-based, mobile-first approach
I'll incorporate these patterns into the style guide.
```

### Example 3: Folder Reference
```
User: /path/to/design-docs/
Assistant: Scanning folder for reference materials...
Found 5 files:
- brand-guidelines.md (brand identity, colors)
- typography-spec.pdf (font choices, scales)
- component-library.png (UI patterns)
- spacing-grid.png (layout system)
- style-examples.md (usage examples)
Processing all references...
```

## YOLO Mode

User can type `#yolo` to toggle to YOLO mode (process all sections at once).

## CRITICAL REMINDERS

**❌ NEVER:**

- Skip the reference collection step
- Ask yes/no questions for elicitation
- Use any format other than 1-9 numbered options
- Create new elicitation methods
- Proceed without processing provided references

**✅ ALWAYS:**

- Collect and process reference materials FIRST
- Use exact 1-9 format when elicit: true
- Select options 2-9 from data/elicitation-methods only
- Provide detailed rationale with reference citations
- End with "Select 1-9 or just type your question/feedback:"
- Reference source materials when suggesting defaults

## Output Files

This task typically generates:

- `docs/ui/design-principles.md` - Design checklist and principles
- `docs/ui/style-guide.md` - Visual design language specification

Both documents should reference the source materials used in their creation.
