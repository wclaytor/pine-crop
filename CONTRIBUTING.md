# Contributing to Pine Crop

## 🎯 Project Purpose

**Pine Crop** is primarily a **testing ground for using GitHub Copilot** to implement a proof-of-concept based on a template and incrementally improve it. This project serves as a practical experiment in AI-assisted development workflows and iterative enhancement.

## 🤝 How to Contribute

We welcome contributions from the community! However, please follow these guidelines to ensure your effort is well-directed and valuable.

### Before You Start

1. **Check Existing Issues**: Review open issues to understand what's already being worked on
2. **Avoid Duplicate Work**: **DO NOT** submit pull requests for issues that have already been assigned to someone
   - If someone is already working on an issue, your PR will be ignored
   - This prevents wasted effort and duplicate work
3. **Discuss First**: For major changes, open an issue to discuss your approach before implementing

### Contribution Process

1. **Fork** the repository
2. **Create a feature branch** from `main`
3. **Make your changes** following the coding standards
4. **Test thoroughly** in multiple browsers
5. **Submit a pull request** with a clear description

### Areas for Enhancement

We're particularly interested in contributions in these areas:

#### Core Features
- Support for additional image formats (JPEG, WebP, GIF, etc.)
- Preset crop dimensions and templates
- Undo/redo functionality
- Crop history and session management
- Multiple crop areas per image

#### User Experience
- Keyboard shortcuts for common actions
- Touch device support and mobile optimization
- Drag-and-drop file handling improvements
- Better error handling and user feedback

#### Technical Improvements
- Image rotation capabilities
- Performance optimizations for large files
- Progressive web app (PWA) features
- Accessibility enhancements
- Code organization and documentation

### Code Standards

Since this project uses **Alpine.js** and **Tailwind CSS** for a standalone HTML application:

- Follow the existing Alpine.js patterns and conventions
- Use Tailwind CSS utility classes consistently
- Maintain the single-file architecture where possible
- Ensure browser compatibility (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- Test with various image sizes and formats
- Keep the tool lightweight and fast

### Pull Request Guidelines

#### Required Information
- **Clear description** of what the PR accomplishes
- **Testing details** - browsers and scenarios tested
- **Screenshots** for UI changes
- **Breaking changes** clearly documented

#### Code Quality
- Code should be clean and well-commented
- Follow existing naming conventions
- Ensure no console errors or warnings
- Test with multiple file sizes and edge cases

### Testing Your Changes

Before submitting, please test:

1. **File Loading**: Various PNG files, different sizes
2. **Crop Functionality**: Different crop areas, edge cases
3. **Batch Processing**: Multiple files at once
4. **Browser Compatibility**: At least 2 different browsers
5. **Error Handling**: Invalid files, network issues, etc.

### Issue Reporting

When reporting bugs or requesting features:

1. **Use clear, descriptive titles**
2. **Provide reproduction steps** for bugs
3. **Include browser and OS information**
4. **Attach sample files** when relevant
5. **Check for existing similar issues** first

### Communication

- Be respectful and constructive in all interactions
- Provide context when asking questions
- Be patient - this is a side project with limited maintenance time
- Focus on the learning and experimentation aspects of the project

## 🚀 Getting Started

1. **Clone your fork**
   ```bash
   git clone https://github.com/yourusername/pine-crop.git
   cd pine-crop
   ```

2. **Open the project**
   - Simply open `index.html` in your browser
   - No build process or dependencies needed

3. **Make changes**
   - Edit the HTML/CSS/JavaScript directly
   - Test in your browser

4. **Submit your contribution**
   - Push to your fork
   - Create a pull request

## ❓ Questions?

If you have questions about contributing:

1. Check existing issues and discussions first
2. Open a new issue with the `question` label
3. Be specific about what you're trying to accomplish

## 🙏 Recognition

All contributors will be acknowledged in the project. This includes:

- Code contributions
- Bug reports and testing
- Documentation improvements
- Feature suggestions and feedback

Thank you for helping make Pine Crop better while contributing to our exploration of AI-assisted development!

---

**Remember**: This project is an experiment in GitHub Copilot-assisted development. Your contributions help us learn and improve both the tool and our development processes.