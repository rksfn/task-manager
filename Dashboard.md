 %%```dataviewjs
// Match files whose name looks like YYYY-MM-DD (ignores .md extension)
const pages = dv.pages().where(p => /^\d{4}-\d{2}-\d{2}$/.test(p.file.name));

// Collect all tasks from those pages
let allTasks = [];
for (let page of pages) {
  if (page.file.tasks) {
    for (let t of page.file.tasks) {
      allTasks.push(t);
    }
  }
}

// Count
const total = allTasks.length;
const done = allTasks.filter(t => t.completed).length;
const notdone = total - done;

// Output
dv.paragraph(`📊 Across ${pages.length} daily notes: **${total}** tasks | ✅ Done: **${done}** | ❌ Not done: **${notdone}**`);
``` %%

```dataviewjs
// Match files whose name looks like YYYY-MM-DD (ignores .md extension)
const pages = dv.pages().where(p => /^\d{4}-\d{2}-\d{2}$/.test(p.file.name));

// Collect all tasks
let allTasks = [];
for (let page of pages) {
  if (page.file.tasks) {
    for (let t of page.file.tasks) {
      allTasks.push(t);
    }
  }
}

// Normalize task text (trim, lowercase, collapse spaces)
function normalize(text) {
  return text
    .toLowerCase()
    .replace(/\s+/g, " ") // collapse multiple spaces
    .trim();
}

// Group tasks by normalized text
let taskMap = new Map();
for (let t of allTasks) {
  const key = normalize(t.text);
  if (!taskMap.has(key)) {
    taskMap.set(key, { text: t.text, completed: false, occurrences: [] });
  }
  taskMap.get(key).occurrences.push(t);
  if (t.completed) {
    taskMap.get(key).completed = true;
  }
}

// Count
const total = taskMap.size;
const done = Array.from(taskMap.values()).filter(t => t.completed).length;
const notdone = total - done;

// Output
dv.paragraph(
  `📊 Across ${pages.length} daily notes: **${total}** unique tasks | ✅ Done: **${done}** | ❌ Not done: **${notdone}**`
);
```
