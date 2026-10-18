---
name: biver-page-workflow
description: Use when you build, edit, or publish a Biver landing page with the Biver connector. Covers the order of the tools, the cost of each step against the workspace quota, and how to read a refusal.
---

# Build a Biver landing page

Biver is a landing page builder for Indonesian businesses. One connection works on one workspace. No tool has a workspace parameter. Do not ask the user which workspace to use.

## Start with the overview

Call `get_workspace_overview` first. It shows the plan, what already exists, and how much quota is left.

Biver AI actions use a weekly quota. These actions are `create_page` in `ai` mode, `add_section` in `ai` mode, and `update_section` with an `instruction`. Check the quota before a large job. If the user asks for ten AI sections and the quota covers three, say so first.

When you write the content yourself, use `add_section` in `content` mode. It does not use quota.

## The order that works

A page is not live until you publish it. Edits change the draft only.

1. Call `list_pages` to find existing pages. Reuse a page if one fits.
2. Call `create_page`. Use `template` mode when a template fits. The page starts as a draft.
3. Call `get_page` to read the outline and the `contentHash`. Section IDs are not guessable.
4. Call `add_section`, `update_section`, and `reorder_sections`. Send the `baseContentHash` from `get_page`.
5. Add images with `add_image`. Use `search_stock_photos` for free stock photos. Put the image link into the section.
6. Create products with `create_product` if the page sells something.
7. Check the payment mode with `get_checkout_settings`. Change it with `update_checkout_settings`.
8. Call `publish_page` with `dryRun: true`. Show the result to the user.
9. Call `publish_page` after the user agrees.

A page with a checkout but no payment mode takes orders that nobody can pay. Do not skip step 7.

## Sections

Call `list_section_types` instead of guessing a type. The canonical types are `hero`, `content`, `media`, `image_slider`, `product_showcase`, `action_form`, `action_button`, `shipping_calculator`, `faq`, `custom_code`, `divider`, and `embed`.

Older pages can carry legacy type names. They still render. The catalog maps them.

Call `get_sections` for the full content of a section. `get_page` returns only a short outline.

## Publish and unpublish

`publish_page` makes the draft live. Use `list_domains` with `checkSubdomain` to check that a subdomain is free.

A draft status does not take a live page offline. Use `unpublish_page`. The draft stays after you unpublish.

A custom domain needs three steps in this order: `connect_domain`, then `update_domain` with `verify`, then `update_domain` with `assign`. Another order leaves a domain that looks connected and serves nothing.

## Conflicts and versions

If a tool returns `PAGE_CONFLICT`, the page changed after you read it. Call `get_page` again. Repeat the change with the new `contentHash`.

Biver saves a version before it changes a page. Use `list_page_versions` and `restore_page` to go back.

## Read a refusal

When Biver blocks an action, the answer names the quota, the numbers, the time of the reset, and what lifts the limit. Give those numbers to the user. Do not round them. Do not change the time zone. Biver already uses WIB.

There are two cases:

- **A quota that resets.** Waiting works. Tell the user when.
- **A feature that the plan does not include.** Waiting does not work. Tell the user which plan adds it.

A refused call changes nothing and costs nothing. Say this, so the user does not think they lost quota.

## Do not

- Do not ask for payment keys, bank account numbers, or ad platform tokens in the chat. The account owner enters them in the dashboard.
- Do not try to move money. The connector cannot withdraw, refund, or pay.
- Do not create AI images. The connector has no tool for it.
- Do not delete anything before you show the user what will be lost. Call `delete_item` with `dryRun: true` first.
- Do not publish without the user's agreement.
