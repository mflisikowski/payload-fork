Your task is to generate comprehensive and high-quality technical documentation in MDX format for $ARGUMENTS.

**Step 1: Deep Package Analysis**

Conduct a detailed package analysis, focusing on:

1. **Existing documentation** (`README.md`):
- Find the documentation link in format: `[Documentation source](https://github.com/payloadcms/payload/tree/main/docs/...)`
- Transform the link from `https://github.com/payloadcms/payload/tree/main/` to local path
- Read the existing documentation content from this path
- Preserve the structure and content of the original documentation
- After executing all instructions, overwrite the file

2. **Package metadata** (`package.json`):
- Name, version, description
- Peer dependencies and their required versions
- Scripts and entry points
- Keywords

3. **Additional documentation** (`CHANGELOG.md`, other `.md` files):
- Current usage examples
- Known issues or limitations
- Change history and breaking changes

4. **Source code** (all files in `src/`):
- **Main function/class**: Identify entry point and main logic
- **TypeScript types**: All interfaces, types, enums
- **React components**: Props, state, lifecycle
- **Hooks**: Parameters, return types, side effects
- **Utility functions**: Input/output, error handling
- **API endpoints**: Routes, middleware, validation
- **Database schema**: Models, relations, migrations
- **Event handlers**: Hooks, callbacks, listeners

5. **Tests** (`*.test.ts`, `*.spec.ts`):
- Use cases from tests
- Edge cases and error scenarios
- Configuration examples

6. **Dependencies and integrations**:
- How it works with other Payload packages
- External dependencies and their roles
- Required environment (Node.js, browser, etc.)

**Step 2: Documentation Generation**

Create documentation according to the following template:

---

```mdx
---
title: {{package_display_name}}
label: {{package_short_name}}
order: {{calculated_order}}
desc: {{concise_description_max_160_chars}}
keywords: [{{comma_separated_keywords_from_analysis}}]
---

{{#if_original_documentation_exists}}
<Banner type="warning">
**Original Documentation**: The content below comes from [official PayloadCMS documentation]({{local_docs_path}}).
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

{{original_documentation_content}}

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

{{/if_original_documentation_exists}}

![NPM Version](https://img.shields.io/npm/v/@payloadcms/{{package_name}})
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/{{package_name}})

## {{#if_original_documentation_exists}}Detailed {{/if_original_documentation_exists}}Overview

{{2-3_paragraph_introduction_explaining}}:
- What this package is and its main purpose
- What problems it solves
- Who it's intended for (developers, administrators, etc.)
- Key benefits and use cases

<Banner type="info">
The package is open-source. [View source code]({{github_link}}). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: {{required_payload_version}}
- **Node.js**: {{required_node_version}}
- **TypeScript**: {{if_typescript_required}}
{{#if_additional_requirements}}
- **Additional requirements**: {{list_additional_requirements}}
{{/if_additional_requirements}}

## Installation

```bash
# npm
npm install @payloadcms/{{package_name}}

# yarn
yarn add @payloadcms/{{package_name}}

# pnpm
pnpm add @payloadcms/{{package_name}}
```

{{#if_peer_dependencies}}
### Peer Dependencies
This package requires the following peer dependencies:
```bash
{{list_peer_dependencies_with_versions}}
```
{{/if_peer_dependencies}}

## Quick Start

Basic configuration and usage:

```typescript
{{minimal_but_complete_example_with_comments}}
```

{{#if_env_variables}}
### Environment Variables
```bash
{{list_required_env_variables}}
```
{{/if_env_variables}}

## Detailed Configuration

### Main Options

{{#for_each_config_option}}
#### `{{option_name}}`

- **Type**: `{{typescript_type}}`
- **Default value**: `{{default_value}}`
- **Required**: {{true/false}}

{{detailed_description_of_what_it_does}}

```typescript
{{example_usage_of_this_option}}
```

{{#if_has_nested_options}}
##### Sub-options:
{{nested_options_table_or_list}}
{{/if_has_nested_options}}

{{/for_each_config_option}}

### Configuration Schema

```typescript
{{complete_typescript_interface_with_comments}}
```

## Usage Guides

### {{use_case_1_name}}
{{practical_step_by_step_guide_with_code}}

### {{use_case_2_name}}
{{another_practical_example}}

{{#if_advanced_patterns}}
### Advanced Patterns

#### {{advanced_pattern_name}}
{{complex_implementation_example}}
{{/if_advanced_patterns}}

## API Reference

{{#if_exported_functions}}
### Functions

{{#for_each_function}}
#### `{{function_name}}({{parameters}})`

{{function_description}}

**Parameters:**
{{parameters_table}}

**Returns:** `{{return_type}}`

**Example:**
```typescript
{{function_usage_example}}
```
{{/for_each_function}}
{{/if_exported_functions}}

{{#if_exported_components}}
### React Components

{{#for_each_component}}
#### `{{component_name}}`

{{component_description}}

**Props:**
{{props_table_with_types_and_descriptions}}

**Example:**
```tsx
{{component_usage_example}}
```
{{/for_each_component}}
{{/if_exported_components}}

{{#if_exported_hooks}}
### Hooks

{{#for_each_hook}}
#### `{{hook_name}}({{parameters}})`

{{hook_description}}

**Parameters:**
{{parameters_description}}

**Returns:**
{{return_value_description}}

**Example:**
```typescript
{{hook_usage_example}}
```
{{/for_each_hook}}
{{/if_exported_hooks}}

{{#if_exported_types}}
### TypeScript Types

```typescript
{{all_exported_types_with_comments}}
```
{{/if_exported_types}}

## Integrations

{{#if_payload_hooks}}
### PayloadCMS Hooks
{{list_which_payload_hooks_are_used_and_how}}
{{/if_payload_hooks}}

{{#if_database_integration}}
### Database
{{explain_database_schema_changes_or_requirements}}
{{/if_database_integration}}

{{#if_external_services}}
### External Services
{{list_external_services_integrations}}
{{/if_external_services}}

## Troubleshooting

### Common Issues

{{#for_each_common_issue}}
#### {{issue_title}}

**Problem:** {{problem_description}}

**Solution:**
{{solution_steps}}

**Example:**
```typescript
{{solution_code_example}}
```
{{/for_each_common_issue}}

### Debugging

{{debugging_tips_and_techniques}}

## Migration

{{#if_migration_needed}}
### From version {{previous_version}} to {{current_version}}

{{migration_steps_and_breaking_changes}}
{{/if_migration_needed}}

## Performance

{{#if_performance_considerations}}
### Performance Optimization

{{performance_tips_and_best_practices}}
{{/if_performance_considerations}}

## Security

{{#if_security_considerations}}
{{security_best_practices_and_warnings}}
{{/if_security_considerations}}

## Example Projects

{{#if_example_projects}}
- [{{example_1_name}}]({{link}}) - {{description}}
- [{{example_2_name}}]({{link}}) - {{description}}
{{/if_example_projects}}

## Contributing

Found a bug or have a suggestion? [Open an issue]({{github_issues_link}}) or submit a Pull Request.

## License

{{license_info}}

**Step 3: Integration with Original Documentation**

When generating documentation:

1. **Check for existing original documentation**:
- Look in `README.md` for a link in format: `[Documentation source](https://github.com/payloadcms/payload/tree/main/docs/...)`
- If found, transform `https://github.com/payloadcms/payload/tree/main/` to local path
- Load file content from this local path

2. **Documentation structure**:
- If original documentation exists: place it first with an informational banner
- Add separator `---`
- Then place our extended documentation with appropriate banner
- If original documentation doesn't exist: use only our version

3. **Preserve original formatting**:
- Don't modify original documentation content
- Preserve all links, examples and structure from the original

**Step 4: Validation and Optimization**
Check completeness: Are all exported elements documented?

**Step 5: Save**
Create a new documentation file alongside the original documentation:
- If original documentation exists at path `docs/original-file.mdx`, create new file at `docs/original-file-extended.mdx`
- If original documentation is `README.md`, create `README-extended.md`
- This prevents Git conflicts while keeping documentation close to the original
- Use the same directory structure as the original file
