# CONTRIBUTING

**Technical Conventions for Eden Hub Portal Development**

---

## Current Development Approach

Eden Hub is currently a **single-file HTML prototype** (`index.html`, ~900KB). This approach ensures:

- Complete understanding of every line of code
- No "black box" components
- Rapid iteration without build tooling
- Clear migration path to React when ready

---

## File Versioning

**Always backup before major edits:**

```
index.html → index_v10_pre_feature.html → index_v11_post_feature.html
```

Use descriptive backup names that indicate what change follows.

---

## Git Workflow

### Branch Naming

```
claude/feature-name-sessionId
feature/friction-feed
fix/pipeline-colour-alignment
docs/update-status
```

### Commit Messages

```
feat: Add client pipeline tracker to detail panel
fix: Correct amber colour hex value
docs: Update EDEN_STATUS with session progress
feat: Chunk X - [brief description]
```

---

## Code Style

### CSS Variables

Always use design tokens from the Eden Calm system:

```css
/* ✓ Correct */
background: var(--eden-mint);
color: var(--eden-green);
border: 1px solid var(--eden-border);

/* ✗ Wrong - hardcoded values */
background: #f4f7f6;
color: #2d5f4d;
border: 1px solid #ccc;  /* NEVER use grey! */
```

### JavaScript Organisation

Functions are organised by section with comment headers:

```javascript
// ============================================
// SECTION NAME
// ============================================

function functionName() {
    // Implementation
}
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Functions | camelCase | `renderAssociateCard()` |
| Variables | camelCase | `currentUserRole` |
| Constants | UPPER_SNAKE | `SPECIALISATIONS` |
| CSS variables | kebab-case | `--eden-green` |
| CSS classes | kebab-case | `.id-card-header` |
| Mock data IDs | UPPER-YYSEQ | `ASSOC-2401`, `CLIENT-2501` |

---

## Component Patterns

### ID Cards

```html
<div class="id-card" onclick="openPanel(id)">
    <div class="id-card-header">
        <div class="avatar">XX</div>
        <div class="id-card-info">
            <div class="id-card-name">Name</div>
            <div class="id-card-ucid">UCID-XXXX</div>
        </div>
        <span class="support-badge independent">✓ Independent</span>
    </div>
    <div class="id-card-stats">
        <!-- Stats content -->
    </div>
</div>
```

### Detail Panels

Panels use the unified detail view pattern:

```javascript
function open(entityType, entity, fromContext) {
    // Render header with avatar, name, UCID
    // Render tabs based on entity type
    // Render menu (role-aware)
    // Render tab content
}
```

### Empty States

```html
<div class="eden-empty-state">
    <div class="eden-empty-illustration">
        <!-- Garden in Bloom SVG -->
    </div>
    <p class="eden-empty-message">Role-aware message</p>
    <button class="eden-empty-action">Action Button</button>
</div>
```

---

## Responsive Design

### Breakpoints

```css
/* Mobile first */
@media (max-width: 768px) {
    .sidebar { transform: translateX(-100%); }
    .side-panel { display: none; }
    .bottom-sheet { display: flex; }
}
```

### Panel Patterns

| Breakpoint | Pattern |
|------------|---------|
| ≤ 768px | Bottom Sheet (slides from bottom, 85vh) |
| > 768px | Side Panel (slides from right, 450px) |

---

## Accessibility Checklist

- [ ] All images have descriptive alt text
- [ ] Interactive elements are keyboard accessible
- [ ] Focus states are visible
- [ ] Colour contrast meets WCAG AA (4.5:1 text, 3:1 UI)
- [ ] Touch targets are 44px minimum
- [ ] No information conveyed by colour alone
- [ ] Semantic HTML elements used
- [ ] ARIA labels where needed

---

## Testing

### Manual Testing Checklist

- [ ] Desktop Chrome
- [ ] Desktop Safari
- [ ] Mobile Safari (iPhone)
- [ ] Mobile Chrome (Android)
- [ ] Keyboard navigation only
- [ ] Role switching (Admin ↔ Associate)

### Before Committing

1. Test in both Admin and Associate roles
2. Verify responsive behaviour at 768px
3. Check for console errors
4. Verify all panels open/close correctly

---

## Documentation Updates

When completing work:

1. Update `EDEN_STATUS.txt` with session summary
2. Add changelog entry if significant
3. Update `agents.md` with completed features
4. Create ADR for architectural decisions

---

## Environment Variables

Use `.env.example` as template. Never commit real credentials.

```
# .env.example
AIRTABLE_API_KEY=your_api_key_here
AIRTABLE_BASE_ID=your_base_id_here
MAKE_GENERATE_TOKEN_URL=https://hook.eu1.make.com/your_token_scenario
MAKE_VERIFY_ACCESS_URL=https://hook.eu1.make.com/your_verify_scenario
```

---

## Performance Guidelines

- Lazy load panels (don't render until opened)
- Use CSS transitions, not JS animation where possible
- Minimise DOM manipulation in loops
- Use event delegation where appropriate

---

## Error Handling

### User-Facing Errors

Use Eden Calm styling:
- Soft language ("We couldn't complete that" not "Error 500")
- Clear next action
- Eden green accent on retry button

### Console Logging

Use sparingly, primarily for debugging:

```javascript
console.log('currentView:', currentView);
console.log('isInSubView:', isInSubView);
```

---

## Dependencies

### Current (Prototype)

- None (vanilla HTML/CSS/JS)
- Lucide icons embedded as inline SVG

### Future (React Migration)

| Purpose | Package |
|---------|---------|
| UI Components | shadcn/ui |
| Icons | lucide-react |
| Date handling | date-fns |
| Form validation | zod |
| State management | React Context |

---

*For design specifications, see EDEN_MASTER.md*
*For philosophy and context, see PROJECT_CONTEXT.md*
