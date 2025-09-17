# GitHub Copilot Instructions - Alpine.js Standalone HTML Applications

## 🎯 Context and Purpose

When users ask for standalone HTML applications, tools, utilities, or "single file" solutions, use Alpine.js with Tailwind CSS to create modern, reactive applications that work without servers or build processes. This approach is ideal for internal tools, data analyzers, converters, and utilities that need easy distribution.

## 🚀 When to Recommend This Approach

### ✅ USE Alpine.js Standalone When User Wants:
- Single HTML file that works offline
- Tool to share via email or file transfer
- No server or hosting required
- Internal company tool without IT deployment
- Data analyzer or converter
- Quick prototype or demo
- Educational tool for students
- "Just double-click to open" simplicity

### ❌ DON'T Use When User Needs:
- SEO optimization
- Large-scale application
- Backend API integration
- User authentication
- Database persistence
- Real-time collaboration
- Mobile app

## 📋 Core Template to Start With

Always begin with this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[App Name]</title>
    
    <!-- Alpine.js for reactivity -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Bootstrap Icons (recommended) -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    
    <style>
        [x-cloak] { display: none !important; }
    </style>
</head>
<body>
    <div x-data="app()" x-cloak class="min-h-screen bg-gray-50 p-6">
        <!-- App content here -->
    </div>
    
    <script>
        function app() {
            return {
                // State and methods
            }
        }
    </script>
</body>
</html>
```

## 🎨 Key Implementation Patterns

### 1. State Management Pattern

```javascript
function app() {
    return {
        // === STATE ===
        data: [],
        searchTerm: '',
        filter: 'all',
        loading: false,
        
        // === COMPUTED PROPERTIES ===
        get filteredData() {
            return this.data.filter(item => {
                const matchesSearch = item.name.toLowerCase()
                    .includes(this.searchTerm.toLowerCase());
                const matchesFilter = this.filter === 'all' || 
                    item.status === this.filter;
                return matchesSearch && matchesFilter;
            });
        },
        
        get statistics() {
            return {
                total: this.data.length,
                active: this.data.filter(d => d.active).length
            };
        },
        
        // === METHODS ===
        async loadData() {
            this.loading = true;
            // Process data
            this.loading = false;
        }
    }
}
```

### 2. File Upload Pattern

```html
<!-- HTML -->
<label class="flex flex-col items-center justify-center w-full h-32 border-2 border-dashed border-gray-300 rounded-lg cursor-pointer bg-gray-50 hover:bg-gray-100">
    <div class="flex flex-col items-center justify-center pt-5 pb-6">
        <i class="bi bi-cloud-upload text-4xl text-gray-400 mb-3"></i>
        <p class="mb-2 text-sm text-gray-700">
            <span class="font-semibold">Click to upload</span> or drag and drop
        </p>
    </div>
    <input type="file" class="hidden" multiple accept=".csv,.json,.xml"
           @change="handleFileUpload($event)" />
</label>

<!-- JavaScript -->
async handleFileUpload(event) {
    const files = Array.from(event.target.files);
    for (const file of files) {
        const text = await file.text();
        // Process file based on type
        if (file.name.endsWith('.json')) {
            this.data = JSON.parse(text);
        } else if (file.name.endsWith('.csv')) {
            this.processCSV(text);
        }
    }
}
```

### 3. Modal Pattern (CRITICAL - Use Inline Styles)

```html
<!-- ALWAYS use this exact pattern for scrollable modals -->
<div x-show="showModal" 
     @click="showModal = false"
     class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-8 z-50">
    <div @click.stop 
         class="bg-white rounded-lg shadow-xl w-full max-w-4xl" 
         style="height: 80vh"> <!-- INLINE STYLE REQUIRED -->
        
        <!-- Fixed Header -->
        <div class="bg-white p-6 border-b rounded-t-lg">
            <h3 class="text-lg font-semibold">Title</h3>
        </div>
        
        <!-- Scrollable Content -->
        <div class="bg-gray-50 p-6 overflow-y-scroll" 
             style="height: calc(80vh - 120px)"> <!-- INLINE STYLE REQUIRED -->
            <!-- Content -->
        </div>
    </div>
</div>
```

### 4. Search and Filter UI

```html
<!-- Search bar -->
<div class="relative">
    <i class="bi bi-search absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400"></i>
    <input x-model="searchTerm" 
           type="text" 
           placeholder="Search..."
           class="w-full pl-10 pr-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
</div>

<!-- Filter buttons -->
<div class="flex space-x-2">
    <button @click="filter = 'all'"
            :class="filter === 'all' ? 'bg-blue-500 text-white' : 'bg-gray-200'"
            class="px-4 py-2 rounded-lg">
        All
    </button>
    <button @click="filter = 'active'"
            :class="filter === 'active' ? 'bg-blue-500 text-white' : 'bg-gray-200'"
            class="px-4 py-2 rounded-lg">
        Active
    </button>
</div>
```

### 5. Table with Alpine.js

```html
<table class="min-w-full divide-y divide-gray-200">
    <thead class="bg-gray-50">
        <tr>
            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Name</th>
            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Status</th>
        </tr>
    </thead>
    <tbody class="bg-white divide-y divide-gray-200">
        <template x-for="item in filteredData" :key="item.id">
            <tr class="hover:bg-gray-50">
                <td class="px-6 py-4" x-text="item.name"></td>
                <td class="px-6 py-4">
                    <span :class="{
                        'text-green-600': item.status === 'active',
                        'text-red-600': item.status === 'inactive'
                    }" x-text="item.status"></span>
                </td>
            </tr>
        </template>
    </tbody>
</table>
```

## 💡 Common Feature Implementations

### Copy to Clipboard
```javascript
async copyToClipboard(text) {
    try {
        await navigator.clipboard.writeText(text);
        alert('Copied to clipboard!');
    } catch (err) {
        // Fallback for older browsers
        const textarea = document.createElement('textarea');
        textarea.value = text;
        textarea.style.position = 'fixed';
        textarea.style.opacity = '0';
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        alert('Copied to clipboard!');
    }
}
```

### Export Data as JSON
```javascript
exportData() {
    const dataStr = JSON.stringify(this.data, null, 2);
    const blob = new Blob([dataStr], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'export.json';
    a.click();
    URL.revokeObjectURL(url);
}
```

### Generate Markdown Report
```javascript
generateMarkdown() {
    let md = `# Report\n\n`;
    md += `Generated: ${new Date().toLocaleString()}\n\n`;
    md += `## Summary\n\n`;
    md += `Total items: ${this.data.length}\n\n`;
    md += `## Details\n\n`;
    this.data.forEach(item => {
        md += `- **${item.name}**: ${item.value}\n`;
    });
    return md;
}
```

### Local Storage Persistence
```javascript
// In the app function
init() {
    // Load saved data on startup
    const saved = localStorage.getItem('appData');
    if (saved) {
        this.data = JSON.parse(saved);
    }
},

saveData() {
    localStorage.setItem('appData', JSON.stringify(this.data));
}
```

## ⚠️ Critical Rules and Pitfalls

### ALWAYS Follow These Rules:

1. **Modal Heights**: ALWAYS use inline styles for modal dimensions
   ```html
   <!-- ✅ CORRECT -->
   <div style="height: 80vh">
   
   <!-- ❌ WRONG - Won't scroll properly -->
   <div class="h-[80vh]">
   ```

2. **Scrollable Content**: Use `overflow-y-scroll` not `overflow-y-auto`
   ```html
   <!-- ✅ CORRECT - Forces scrollbar -->
   <div class="overflow-y-scroll">
   
   <!-- ❌ WRONG - Scrollbar may not appear -->
   <div class="overflow-y-auto">
   ```

3. **Use x-cloak**: Prevent flash of unstyled content
   ```html
   <!-- ✅ ALWAYS include -->
   <style>[x-cloak] { display: none !important; }</style>
   <div x-data="app()" x-cloak>
   ```

4. **Computed Properties**: Use getters for derived data
   ```javascript
   // ✅ CORRECT - Reactive
   get filtered() { return this.data.filter(...) }
   
   // ❌ WRONG - Not reactive
   filtered: this.data.filter(...)
   ```

5. **Event Handlers**: Use Alpine syntax
   ```html
   <!-- ✅ CORRECT -->
   <button @click="handleClick">
   
   <!-- ❌ WRONG -->
   <button onclick="handleClick()">
   ```

## 📏 Code Quality Guidelines

### File Size Targets
- **HTML + JS**: Keep under 2000 lines
- **Inline Styles**: Minimal, only for critical dimensions
- **Components**: If over 500 lines, suggest splitting logic

### Performance Considerations
- Use `x-show` for frequently toggled elements
- Use `x-if` only for rarely shown elements
- Always use `:key` in `x-for` loops
- Debounce search inputs (300ms recommended)

### Naming Conventions
```javascript
// State: noun
data: [],
searchTerm: '',
isLoading: false,

// Computed: get + noun
get filteredData() {},
get statistics() {},

// Methods: verb + noun
handleFileUpload() {},
processData() {},
generateReport() {}
```

## 🎯 Response Strategy

When user asks for a standalone tool:

1. **Confirm Requirements**
   - "Would you like this as a single HTML file that works offline?"
   - "Will users need to save/export data?"

2. **Start with Core Template**
   - Use the basic Alpine.js template
   - Add only needed features

3. **Implement Features Incrementally**
   - File upload first (if needed)
   - Then data processing
   - Then UI features
   - Finally, export/reporting

4. **Test Scenarios to Mention**
   - "Save as .html and double-click to open"
   - "Works offline after first load"
   - "Share via email or USB drive"

## 📚 Reference Patterns

Point users to common patterns:
- **Data Analyzer**: File upload → Process → Display table → Export
- **Converter Tool**: Input → Transform → Preview → Download
- **Report Generator**: Load data → Filter → Generate markdown → Copy
- **Calculator**: Input form → Compute → Show results → Save history

## 💬 Example Responses

### When user asks: "I need a CSV analyzer tool"
```
I'll create a standalone HTML file that can analyze CSV files offline. 
This will use Alpine.js for reactivity and work by just opening the 
HTML file in your browser - no server needed.

[Provide full HTML with CSV parsing, table display, and statistics]
```

### When user asks: "Can this work without internet?"
```
Yes! After the initial load of CDN resources (Alpine.js and Tailwind), 
the app works completely offline. For true offline use, you can also 
download and inline the CDN resources.
```

### When user asks: "How do I share this with my team?"
```
Simply save the HTML file and share it via:
- Email attachment
- Shared drive
- USB drive
- Slack/Teams file upload

Recipients just save and double-click to open - no installation needed!
```

## 🚫 Anti-Patterns to Avoid

Never suggest:
- jQuery for new projects (Alpine.js is better)
- Complex build processes for simple tools
- Server-side code for standalone requirements
- React/Vue via CDN (too complex for standalone)
- Vanilla JS for reactive UIs (Alpine.js is simpler)

## ✅ Success Metrics

A good standalone HTML app has:
- Single file under 100KB
- Works with file:// protocol
- No external dependencies after load
- Responsive design
- Professional appearance
- Fast performance with 1000+ items
- Clear error messages
- Export capabilities

---

*Use these instructions to help users create powerful, modern standalone HTML applications that are easy to distribute and use.*