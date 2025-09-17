# Alpine.js Standalone HTML Application Template

🚀 **Create powerful, reactive web applications in a single HTML file** - perfect for tools, utilities, and applications that need to be easily distributed without servers or build processes.

## ✨ What is this?

This template helps you build modern, reactive web applications using [Alpine.js](https://alpinejs.dev/) and [Tailwind CSS](https://tailwindcss.com/) that work completely offline and can be shared as a single HTML file.

### Perfect for:
- ✅ Internal tools and utilities
- ✅ Data analyzers and converters
- ✅ Offline calculators and forms
- ✅ Prototypes and demos
- ✅ Educational tools
- ✅ Apps you share via email or USB drive

### Not ideal for:
- ❌ Large-scale applications
- ❌ SEO-critical websites
- ❌ Apps needing backend APIs
- ❌ Real-time collaboration apps

## 🚀 Quick Start

### 1. Basic Template
Copy this starter template and save as an `.html` file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Alpine App</title>
    
    <!-- Alpine.js for reactivity -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    
    <style>
        [x-cloak] { display: none !important; }
    </style>
</head>
<body>
    <div x-data="app()" x-cloak class="min-h-screen bg-gray-50 p-6">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-3xl font-bold text-gray-900 mb-8">My Alpine App</h1>
            
            <!-- Your app content here -->
            <div class="bg-white rounded-lg shadow p-6">
                <p x-text="message" class="text-lg"></p>
                <button @click="updateMessage()" 
                        class="mt-4 bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
                    Click me!
                </button>
            </div>
        </div>
    </div>
    
    <script>
        function app() {
            return {
                message: 'Hello, Alpine.js!',
                
                updateMessage() {
                    this.message = 'You clicked the button! 🎉';
                }
            }
        }
    </script>
</body>
</html>
```

### 2. Save and Test
1. Save the code above as `my-app.html`
2. Double-click the file to open in your browser
3. Click the button to see Alpine.js reactivity in action!

## 📚 Documentation

- **[Complete Alpine.js Guide](docs/alpine-guide.md)** - Comprehensive guide with patterns and examples
- **[Copilot Instructions](.github/copilot-instructions.md)** - How GitHub Copilot can help you build Alpine.js apps

## 🎯 Common Use Cases

### Data Analyzer
Perfect for CSV/JSON analysis tools:
```javascript
function dataAnalyzer() {
    return {
        data: [],
        
        async handleFileUpload(event) {
            const file = event.target.files[0];
            const text = await file.text();
            this.data = this.parseCSV(text);
        },
        
        get statistics() {
            return {
                total: this.data.length,
                average: this.data.reduce((sum, item) => sum + item.value, 0) / this.data.length
            };
        }
    }
}
```

### Form Builder
Create interactive forms with validation:
```javascript
function formApp() {
    return {
        form: { name: '', email: '' },
        errors: {},
        
        validate() {
            this.errors = {};
            if (!this.form.name) this.errors.name = 'Name required';
            if (!this.form.email.includes('@')) this.errors.email = 'Valid email required';
            return Object.keys(this.errors).length === 0;
        },
        
        submit() {
            if (this.validate()) {
                alert('Form submitted!');
            }
        }
    }
}
```

### Calculator/Converter
Build calculation tools:
```javascript
function calculator() {
    return {
        input: '',
        result: 0,
        history: [],
        
        calculate() {
            try {
                this.result = eval(this.input);
                this.history.push(`${this.input} = ${this.result}`);
            } catch (error) {
                alert('Invalid calculation');
            }
        }
    }
}
```

## 🎨 Key Features

### Reactive Data Binding
```html
<input x-model="searchTerm" placeholder="Search...">
<p x-text="'You searched for: ' + searchTerm"></p>
```

### Conditional Display
```html
<div x-show="isVisible">This appears conditionally</div>
<template x-if="user.isAdmin">
    <button>Admin Panel</button>
</template>
```

### Lists and Loops
```html
<template x-for="item in filteredItems" :key="item.id">
    <div x-text="item.name" class="p-2 border-b"></div>
</template>
```

### Event Handling
```html
<button @click="handleClick()">Click me</button>
<input @keyup.enter="search()">
<form @submit.prevent="save()">
```

## 💾 Data Persistence

### Local Storage
```javascript
function persistentApp() {
    return {
        data: [],
        
        init() {
            const saved = localStorage.getItem('appData');
            if (saved) this.data = JSON.parse(saved);
        },
        
        save() {
            localStorage.setItem('appData', JSON.stringify(this.data));
        }
    }
}
```

### File Export
```javascript
exportData() {
    const blob = new Blob([JSON.stringify(this.data, null, 2)], 
                         { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'data.json';
    a.click();
}
```

## 🎯 Best Practices

### ✅ Do This
- Use computed properties for derived data: `get filteredItems() { }`
- Include `x-cloak` to prevent flash of unstyled content
- Use `x-show` for frequently toggled elements
- Always provide `:key` for `x-for` loops
- Organize code into clear sections (state, computed, methods)

### ❌ Avoid This
- Don't filter/sort data in templates - use computed properties
- Don't use `x-if` for frequently shown/hidden content
- Don't forget error handling for file operations
- Don't use Tailwind classes for modal heights - use inline styles

## 📏 File Size Guidelines

- **Target**: Keep HTML + JS under 2000 lines
- **Performance**: Test with 1000+ data items
- **Distribution**: Single file should be under 100KB
- **Compatibility**: Test with `file://` protocol

## 🚀 Distribution

### Share Your App
1. **Email**: Attach the HTML file
2. **USB Drive**: Copy and share
3. **GitHub**: Upload to repository
4. **Company Drive**: Share via internal systems

### Users Just Need To:
1. Save the HTML file
2. Double-click to open in browser
3. Start using immediately!

## 🔧 Advanced Features

### File Upload Handling
```html
<input type="file" @change="handleFileUpload($event)" accept=".csv,.json">
```

### Modal with Proper Scrolling
```html
<div x-show="showModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-8">
    <div class="bg-white rounded-lg w-full max-w-4xl" style="height: 80vh">
        <div class="p-6 border-b">Header</div>
        <div class="p-6 overflow-y-scroll" style="height: calc(80vh - 120px)">
            Content
        </div>
    </div>
</div>
```

### Copy to Clipboard
```javascript
async copyToClipboard(text) {
    try {
        await navigator.clipboard.writeText(text);
        alert('Copied!');
    } catch (err) {
        // Fallback for older browsers
        const textarea = document.createElement('textarea');
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        alert('Copied!');
    }
}
```

## 🎓 Learning Resources

- **[Alpine.js Documentation](https://alpinejs.dev/)** - Official Alpine.js docs
- **[Tailwind CSS](https://tailwindcss.com/)** - Utility-first CSS framework
- **[Bootstrap Icons](https://icons.getbootstrap.com/)** - Icon library
- **[MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)** - Browser APIs reference

## 🤝 Contributing

Have examples or improvements? Contributions welcome!

1. Fork the repository
2. Create your feature branch
3. Add your example or improvement
4. Submit a pull request

## 📄 License

This template is free to use for any purpose. No attribution required.

---

**Happy coding!** 🎉 Start building amazing standalone applications with Alpine.js today.
````

This README provides a comprehensive introduction to using the Alpine.js template, including:

1. **Clear purpose** - What this template is for and when to use it
2. **Quick start** - A working example users can copy and run immediately
3. **Common patterns** - Practical examples for typical use cases
4. **Best practices** - Do's and don'ts based on real experience
5. **Distribution guidance** - How to share the finished apps
6. **Learning resources** - Links to further documentation
