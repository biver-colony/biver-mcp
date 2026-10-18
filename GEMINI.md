# Biver

Biver is an online builder for landing pages and small online stores. It serves Indonesian businesses.

The Biver tools work in one workspace. The user chooses the workspace when they sign in.

## Order of work

1. Call `get_workspace_overview`. Read the plan, the usage, and the next step.
2. Call `list_pages` and `get_page`. Find the page to change.
3. Call `get_sections`. Read the sections before you edit them.
4. Call `update_section` or `add_section`. Changes stay in the draft.
5. Ask the user to approve the draft.
6. Call `publish_page` only after the user agrees. Use `dryRun` first.

## Rules

- Do not publish or delete without the approval of the user.
- Use `dryRun` with `publish_page`, `unpublish_page`, and `delete_item`.
- Biver AI actions use the weekly AI quota. Tell the user before you use them.
- The tools cannot move money. They cannot read payment keys.
- Write page text in Indonesian. Use another language only when the user asks.
