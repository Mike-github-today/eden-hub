# CONTRIBUTING

**Technical Conventions for Eden Hub Portal Development**

---

## File Versioning

**Always backup before editing:**

```
portal_v1.html → portal_v2.html → portal_v3.html
```

Never overwrite working versions. Keep iterations until feature is complete.

---

## Git Workflow

### Branch Naming

```
feature/friction-feed
fix/pipeline-colour-alignment
docs/update-status
```

### Commit Messages

```
feat: Add client pipeline tracker to detail panel
fix: Correct amber colour hex value
docs: Update EDEN_STATUS with session progress
```

---

## Code Style

### CSS Variables

Always use design tokens from EDEN_MASTER.md:

```css
/* ✓ Correct */
background: var(--eden-whisper);
color: var(--eden-deep);

/* ✗ Wrong - hardcoded values */
background: #f4f7f6;
color: #2d5f4d;
```

### Component Structure (React)

```
src/
├── components/
│   ├── ui/              ← shadcn components
│   ├── panels/          ← Detail panels (Associate, Client)
│   ├── cards/           ← Gateway cards, client cards
│   └── shared/          ← Reusable (Pipeline tracker, etc.)
├── context/             ← Auth context, etc.
├── hooks/               ← Custom hooks
└── lib/                 ← Utilities
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `ClientDetailPanel.tsx` |
| Hooks | camelCase with 'use' prefix | `useAuth.ts` |
| Utilities | camelCase | `formatUcid.ts` |
| CSS variables | kebab-case | `--eden-deep` |
| Airtable fields | Title_Case with underscores | `Portal_Access` |

---

## Responsive Breakpoints

```css
/* Mobile first */
@media (min-width: 640px)  { /* sm */ }
@media (min-width: 768px)  { /* md */ }
@media (min-width: 1024px) { /* lg - side panel kicks in */ }
@media (min-width: 1280px) { /* xl */ }
```

### Panel Patterns

| Breakpoint | Pattern |
|------------|---------|
| < 1024px | Bottom Sheet (slides from bottom) |
| ≥ 1024px | Side Panel (slides from right) |

---

## Accessibility Checklist

- [ ] All images have descriptive alt text
- [ ] Interactive elements are keyboard accessible
- [ ] Focus states are visible
- [ ] Colour contrast meets WCAG AA (4.5:1 text, 3:1 UI)
- [ ] Touch targets are 44px minimum
- [ ] No information conveyed by colour alone
- [ ] Semantic HTML elements used

---

## Testing

### Manual Testing Checklist

- [ ] Desktop Chrome
- [ ] Desktop Safari
- [ ] Mobile Safari (iPhone)
- [ ] Mobile Chrome (Android)
- [ ] Keyboard navigation only
- [ ] Screen reader (VoiceOver)

### Before Merging

1. All chunks work independently
2. No console errors
3. Responsive behaviour verified
4. Accessibility checklist passed

---

## Documentation Updates

When completing work:

1. Update `EDEN_STATUS.txt` with session summary
2. Add changelog entry if significant
3. Update EDEN_MASTER.md if specs change
4. Create ADR for architectural decisions

---

## Environment Variables

Use `.env.example` as template. Never commit real credentials.

```
# .env.example
AIRTABLE_API_KEY=your_key_here
MAKE_WEBHOOK_URL=your_webhook_here
```

---

## Performance Guidelines

- Lazy load panels (don't render until opened)
- Optimise images before upload
- Minimise JavaScript bundle size
- Use CSS transitions, not JS animation where possible

---

## Error Handling

### User-Facing Errors

Use Eden Calm styling:
- Soft language ("We couldn't complete that" not "Error 500")
- Clear next action
- Eden green accent on retry button

### Logging

Console errors should include:
- What was attempted
- What failed
- Suggested resolution

---

## Dependencies

### Approved Packages

| Purpose | Package |
|---------|---------|
| UI Components | shadcn/ui |
| Icons | lucide-react |
| Date handling | date-fns |
| Form validation | zod |
| State management | React Context (keep simple) |

### Adding New Dependencies

1. Check if existing package covers need
2. Evaluate bundle size impact
3. Verify maintenance status
4. Document reason in commit message

---

*For design specifications, see EDEN_MASTER.md*  
*For philosophy and context, see PROJECT_CONTEXT.md*
