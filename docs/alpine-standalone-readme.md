# 🚀 Alpine.js Standalone HTML Applications

> Build powerful, reactive web applications in a single HTML file - no servers, no build process, just double-click and run!

[![Alpine.js Version](https://img.shields.io/badge/Alpine.js-3.x-8BC0D0?logo=alpine.js)](https://alpinejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## ✨ What is This?

This project provides a complete framework and guide for building modern web applications that:
- 📦 **Run from a single HTML file**
- 🔌 **Work completely offline** (after initial load)
- 📧 **Can be shared via email** or USB drive
- 🎯 **Require zero installation** - just save and open
- ⚡ **Provide reactive, modern UIs** like React/Vue but simpler

Perfect for internal tools, data analyzers, converters, calculators, and any utility that needs easy distribution without IT deployment hassles.

## 🎬 Quick Start (2 Minutes!)

### Your First App

1. **Copy this code into a new file called `my-app.html`:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Alpine App</title>
    
    <!-- Alpine.js for reactivity -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    
    <style>
        [x-cloak] { display: none !important; }
    </style>
</head>
<body>
    <div x-data="todoApp()" x-cloak class="min-h-screen bg-gray-50 p-6">
        <div class="max-w-2xl mx-auto">
            <!-- Header -->
            <div class="bg-white rounded-lg shadow-md p-6 mb-6">
                <h1 class="text-2xl font-bold text-gray-800 mb-4">
                    <i class="bi bi-check2-square text-blue-500"></i>
                    My Todo List
                </h1>
                
                <!-- Add Todo -->
                <div class="flex gap-2">
                    <input x-model="newTodo" 
                           @keyup.enter="addTodo"
                           type="text" 
                           placeholder="Add a new task..."
                           class="flex-1 px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    <button @click="addTodo" 
                            class="px-6 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600">
                        Add
                    </button>
                </div>
            </div>
            
            <!-- Todo List -->
            <div class="bg-white rounded-lg shadow-md p-6">
                <div class="mb-4 text-sm text-gray-600">
                    You have <span class="font-bold" x-text="todos.filter(t => !t.done).length"></span> 
                    active tasks
                </div>
                
                <template x-for="todo in todos" :key="todo.id">
                    <div class="flex items-center gap-3 p-3 border-b hover:bg-gray-50">
                        <input type="checkbox" 
                               x-model="todo.done" 
                               class="w-5 h-5 text-blue-500">
                        <span :class="{'line-through text-gray-400': todo.done}" 
                              x-text="todo.text"
                              class="flex-1"></span>
                        <button @click="removeTodo(todo.id)" 
                                class="text-red-500 hover:text-red-700">
                            <i class="bi bi-trash"></i>
                        </button>
                    </div>
                </template>
                
                <div x-show="todos.length === 0" class="text-center py-8 text-gray-400">
                    No tasks yet. Add one above!
                </div>
            </div>
        </div>
    </div>
    
    <script>
        function todoApp() {
            return {
                todos: [],
                newTodo: '',
                
                addTodo() {
                    if (this.newTodo.trim()) {
                        this.todos.push({
                            id: Date.now(),
                            text: this.newTodo,
                            done: false
                        });
                        this.newTodo = '';
                        this.saveTodos();
                    }
                },
                
                removeTodo(id) {
                    this.todos = this.todos.filter(t => t.id !== id);
                    this.saveTodos();
                },
                
                saveTodos() {
                    localStorage.setItem('todos', JSON.stringify(this.todos));
                },
                
                init() {
                    // Load saved todos
                    const saved = localStorage.getItem('todos');
                    if (saved) {
                        this.todos = JSON.parse(saved);
                    }
                }
            }
        }
    </script>
</body>
</html>
```

2. **Save the file and double-click to open it in your browser**

3. **That's it!** You now have a working todo app that:
   - Saves data locally
   - Works offline
   - Can be shared with anyone

## 📚 Documentation

### Guides
- **[📖 Complete Development Guide](alpine-standalone-guide.md)** - Everything you need to know
- **[🤖 AI/Copilot Instructions](copilot-alpine-instructions.md)** - For AI-assisted development

### Quick Links
- [Basic Templates](#templates)
- [Common Patterns](#common-patterns)
- [Example Apps](#example-apps)
- [Troubleshooting](#troubleshooting)

## 🎯 Common Patterns

### File Upload & Processing
```javascript
async handleFileUpload(event) {
    const file = event.target.files[0];
    const text = await file.text();
    
    if (file.name.endsWith('.json')) {
        this.data = JSON.parse(text);
    } else if (file.name.endsWith('.csv')) {
        this.processCSV(text);
    }
}
```

### Export Data
```javascript
exportData() {
    const blob = new Blob([JSON.stringify(this.data, null, 2)], 
                          { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'export.json';
    a.click();
}
```

### Search & Filter
```javascript
get filteredItems() {
    return this.items.filter(item => 
        item.name.toLowerCase().includes(this.searchTerm.toLowerCase())
    );
}
```

## 🛠️ Templates

### Basic App Template
```bash
# Download the basic template
curl -O https://raw.githubusercontent.com/[your-repo]/templates/basic-app.html
```

### Data Analyzer Template
```bash
# Download the data analyzer template
curl -O https://raw.githubusercontent.com/[your-repo]/templates/data-analyzer.html
```

### Report Generator Template
```bash
# Download the report generator template
curl -O https://raw.githubusercontent.com/[your-repo]/templates/report-generator.html
```

## 💡 Example Apps

### 1. CSV Analyzer
A complete data analysis tool that:
- Uploads and parses CSV files
- Displays data in sortable tables
- Generates statistics
- Exports processed data

[View Code](examples/csv-analyzer.html) | [Live Demo](#)

### 2. JSON Formatter
A developer utility that:
- Formats and validates JSON
- Converts between formats
- Provides tree view navigation
- Highlights syntax

[View Code](examples/json-formatter.html) | [Live Demo](#)

### 3. Markdown Editor
A writing tool that:
- Live preview
- Export to HTML/PDF
- Keyboard shortcuts
- Local storage sync

[View Code](examples/markdown-editor.html) | [Live Demo](#)

## 🏗️ Project Structure

```
alpine-standalone-apps/
├── README.md                      # This file
├── alpine-standalone-guide.md     # Complete development guide
├── copilot-alpine-instructions.md # AI assistant instructions
├── templates/                     # Ready-to-use templates
│   ├── basic-app.html
│   ├── data-analyzer.html
│   └── report-generator.html
├── examples/                      # Complete example applications
│   ├── csv-analyzer.html
│   ├── json-formatter.html
│   └── markdown-editor.html
└── snippets/                      # Reusable code snippets
    ├── file-upload.js
    ├── modal.html
    └── table.html
```

## ⚡ Key Features

### Why Alpine.js?
- **15KB** - Tiny footprint
- **No build step** - Just include via CDN
- **Reactive** - Automatic UI updates
- **Simple** - Learn in an afternoon
- **Powerful** - Handle complex interactions

### Why Standalone HTML?
- **Zero deployment** - No servers needed
- **Instant sharing** - Email or USB drive
- **Always works** - No dependencies to break
- **Version control** - Just one file to manage
- **Offline capable** - Works without internet

## 🚀 Advanced Features

### Local Storage Persistence
```javascript
init() {
    const saved = localStorage.getItem('appData');
    if (saved) this.data = JSON.parse(saved);
}

save() {
    localStorage.setItem('appData', JSON.stringify(this.data));
}
```

### Keyboard Shortcuts
```javascript
document.addEventListener('keydown', (e) => {
    if (e.ctrlKey && e.key === 's') {
        e.preventDefault();
        this.save();
    }
});
```

### Drag & Drop
```html
<div @drop.prevent="handleDrop($event)"
     @dragover.prevent
     class="border-2 border-dashed p-8">
    Drop files here
</div>
```

## 🐛 Troubleshooting

### Modal Scrolling Issues
Always use inline styles for modal heights:
```html
<!-- ✅ CORRECT -->
<div style="height: 80vh">

<!-- ❌ WRONG - Won't scroll properly -->
<div class="h-[80vh]">
```

### Flash of Unstyled Content
Always include `x-cloak`:
```html
<style>[x-cloak] { display: none !important; }</style>
<div x-data="app()" x-cloak>
```

### Performance with Large Data
Use computed properties:
```javascript
// ✅ Efficient - computed once
get filtered() { return this.data.filter(...) }

// ❌ Inefficient - computed every render
<template x-for="item in data.filter(...)">
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Ways to Contribute
- 🐛 Report bugs
- 💡 Suggest new features
- 📝 Improve documentation
- 🎨 Submit app examples
- ⭐ Star this repo!

## 📄 License

This project is MIT licensed. See [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Alpine.js](https://alpinejs.dev/) - The lightweight reactive framework
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- [Bootstrap Icons](https://icons.getbootstrap.com/) - Beautiful open source icons

## 💬 Support

- 📧 Email: support@example.com
- 💬 Discord: [Join our community](#)
- 🐦 Twitter: [@AlpineStandalone](#)
- 📖 Docs: [Full documentation](alpine-standalone-guide.md)

---

<div align="center">

**Ready to build something awesome?** 🚀

Start with the [Quick Start](#-quick-start-2-minutes) or dive into the [Complete Guide](alpine-standalone-guide.md)

Made with ❤️ by developers who were tired of deployment complexity

</div>