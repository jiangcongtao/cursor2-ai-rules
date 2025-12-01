# Cursor Rules Documentation

## Introduction

This directory contains the cursor rules configuration for this project. Cursor rules are instructions that guide the AI assistant's behavior, personality, and response formatting throughout your interactions. These rules ensure consistent, high-quality assistance tailored to your project's needs.

## Directory Structure

```
.cursor/
├── README.md          # This file - documentation for the rules system
└── rules/             # Rule files directory
    ├── core.mdc       # Teaching assistant identity and behavior
    ├── common.mdc     # Disclaimer footnote requirement
    └── identity.mdc   # Identity introduction instruction
```

## Rule Files

### core.mdc
**Status:** `alwaysApply: true`

**Purpose:** Defines the AI assistant's core identity and teaching methodology.

**Behavior:**
- Establishes the assistant as a patient and knowledgeable teaching guide
- Ensures systematic explanations progressing from fundamentals to practical applications
- Provides clear examples and step-by-step guidance
- Makes complex topics accessible to beginners
- Enables learning through hands-on practice

This rule is always active and shapes the overall interaction style of the AI assistant.

### common.mdc
**Status:** `alwaysApply: true`

**Purpose:** Ensures responsible AI usage by requiring a disclaimer on all responses.

**Behavior:**
- Automatically adds a disclaimer footnote to the bottom of every response
- Disclaimer text: "_Disclaimer: This content is AI-generated. Please verify all facts and details prior to use._"
- Reminds users to verify AI-generated content before relying on it

This rule is always active to promote responsible use of AI-generated content.

### identity.mdc
**Status:** `alwaysApply: false`

**Purpose:** Instructs the assistant to introduce its identity when appropriate.

**Behavior:**
- When active, the assistant briefly introduces its identity before answering queries
- This rule is conditionally applied (not always active)
- Provides context to users about who/what they're interacting with

## Configuration

### alwaysApply Setting

Each rule file contains a YAML frontmatter section with an `alwaysApply` setting:

```yaml
---
alwaysApply: true
---
```

**Values:**
- `alwaysApply: true` - The rule is always active in all conversations
- `alwaysApply: false` - The rule is conditionally applied based on context

### How Rules Work Together

1. **Core Identity (core.mdc)** - Always active, provides the foundational teaching assistant persona
2. **Disclaimer (common.mdc)** - Always active, ensures all responses include appropriate disclaimers
3. **Identity Introduction (identity.mdc)** - Conditionally active, adds context when needed

The combination of these rules creates a consistent, educational, and responsible AI assistant experience.

## Usage Notes

- Rules with `alwaysApply: true` affect every interaction automatically
- Rules with `alwaysApply: false` may be selectively applied by the system
- You can add new rule files to the `rules/` directory as needed
- Each rule file should use the `.mdc` extension (Markdown with metadata)
- Rule files should include the YAML frontmatter with the `alwaysApply` setting

## Best Practices

1. **Keep Rules Focused** - Each rule file should address a specific aspect of AI behavior
2. **Document Changes** - Update this README when adding, modifying, or removing rules
3. **Test Rules** - Verify that new rules work as intended and don't conflict with existing ones
4. **Use Clear Language** - Write rules in clear, unambiguous language
5. **Consider Priority** - Rules that should always apply should have `alwaysApply: true`

## Modifying Rules

To modify the AI assistant's behavior:

1. Edit the appropriate rule file in `.cursor/rules/`
2. Maintain the YAML frontmatter structure
3. Keep rule descriptions clear and concise
4. Update this README to reflect any changes
5. Test the changes in a conversation to ensure they work as expected

---

_Last Updated: December 2025_

