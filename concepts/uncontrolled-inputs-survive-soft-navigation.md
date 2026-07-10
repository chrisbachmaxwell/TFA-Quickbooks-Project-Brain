# defaultValue changes don't apply across server-action soft navigations

A server component re-rendered after a server action (soft navigation) updates attributes on hydrated DOM, but an **uncontrolled** form element keeps its live value — a new `defaultValue`/`selected` lands in the HTML and does nothing. Symptom here: the category dropdown's payee suggestion rendered `selected` in fresh page loads but stayed on the placeholder after categorizing a row (which re-renders via action + redirect to the same route).

**Fix:** give the element a `key` derived from the value that should reset it (`key={suggestedId ?? "none"}`) so React remounts it — or make it controlled in a client component. Found via a failing Playwright gate in goal 008, 2026-07-10.
