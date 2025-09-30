### Setup

- Use the daily note template in **`temp/daily-tasks.md`**. You can set this as the default template for your Daily Notes.
    
- For the **Dashboard**, install the **Dataview** plugin from _Community Plugins_. Then paste the contents of **`Dashboard.md`** into your dashboard file — and you’re ready to go.
    

### Dashboard Scripts (DataviewJS)

These scripts provide an overview of task completion across your daily notes:

1. **Task Totals**
    
    - Scans all daily notes (files named `YYYY-MM-DD`).
        
    - Collects every task and reports:
        
        - 📌 **Total tasks** written
            
        - ✅ **Completed** tasks
            
        - ❌ **Incomplete** tasks
            
2. **Unique Tasks**
    
    - Normalizes task text (ignores case and extra spaces).
        
    - Groups duplicate tasks across notes.
        
    - Reports:
        
        - 📌 **Unique tasks** created
            
        - ✅ **Completed unique tasks**
            
        - ❌ **Remaining unique tasks**
            
