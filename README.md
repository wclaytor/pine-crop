# Pine Crop

A standalone, browser-based tool for batch cropping PNG images with the same dimensions. Perfect for cropping screenshots, removing unwanted borders, or extracting specific regions from multiple images at once.

![Alpine.js](https://img.shields.io/badge/Alpine.js-3.x-8BC0D0?logo=javascript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?logo=tailwindcss)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## 🎯 Features

- **Visual Crop Selection** - Interactive drag-and-drop interface with resize handles
- **Batch Processing** - Apply the same crop to multiple images at once
- **No Installation Required** - Runs entirely in your browser
- **Offline Capable** - Works without internet after initial load
- **Precise Control** - Manual input fields for exact pixel-perfect positioning
- **Real-time Preview** - See exactly what will be cropped before processing
- **Progress Tracking** - Visual progress bar during batch operations
- **Automatic Downloads** - Cropped images are automatically saved with `-crop` suffix

## 🚀 Quick Start

1. **Download** the `index.html` file and rename it to your liking
2. **Open** it in any modern web browser (Chrome, Firefox, Edge, Safari)
3. **Select** your PNG images using the file picker
4. **Adjust** the crop area on the preview image
5. **Click** "Crop All Images" to process the entire batch

## 📖 Usage Guide

### Selecting Images

Click the "Choose Files" button or drag and drop PNG files onto the file input area. The tool accepts multiple PNG files at once.

### Setting Crop Boundaries

The first image in your selection will be displayed as a preview with an adjustable crop overlay:

- **Move the crop area**: Click and drag the blue box
- **Resize from corners**: Drag the corner handles for proportional resizing
- **Resize from edges**: Drag the edge handles to adjust width or height
- **Fine-tune with inputs**: Use the number fields for pixel-perfect positioning
  - **X Position**: Horizontal offset from the left edge
  - **Y Position**: Vertical offset from the top edge
  - **Width**: Width of the crop area in pixels
  - **Height**: Height of the crop area in pixels

### Processing Images

Once you're satisfied with the crop boundaries:

1. Click the **"Crop All Images"** button
2. Watch the progress bar as each image is processed
3. Cropped images will be automatically downloaded to your browser's default download folder
4. Each file will have `-crop` appended to its original filename
   - Example: `screenshot.png` → `screenshot-crop.png`

### Resetting

Click the **"Reset"** button to:
- Clear all loaded images
- Reset crop parameters to defaults
- Start fresh with a new batch

## 🛠️ Technical Details

### Requirements

- **Browser**: Any modern web browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- **JavaScript**: Must be enabled
- **File System Access**: Browser must allow file downloads

### Technologies Used

- **Alpine.js 3.x** - Reactive UI framework
- **Tailwind CSS 3.x** - Utility-first CSS framework
- **Bootstrap Icons** - Icon library
- **HTML5 Canvas API** - Image manipulation
- **File API** - Local file handling

### How It Works

1. **File Reading**: Uses FileReader API to load PNG images into memory
2. **Preview Display**: First image is displayed with an overlay showing crop boundaries
3. **Interactive Controls**: Mouse events handle dragging and resizing of the crop area
4. **Canvas Processing**: HTML5 Canvas API performs the actual image cropping
5. **Blob Generation**: Cropped images are converted to PNG blobs
6. **Auto Download**: Object URLs trigger automatic downloads for each processed image

## 💡 Use Cases

- **Screenshot Processing**: Remove desktop/taskbar from multiple screenshots
- **Web Design**: Extract specific UI components from mockups
- **Documentation**: Crop multiple images to consistent dimensions
- **Photo Editing**: Batch extract regions from similar photos
- **Social Media**: Prepare multiple images with identical dimensions
- **Quality Assurance**: Crop test screenshots to focus on specific areas

## ⚙️ Customization

The tool can be customized by editing the HTML file:

### Default Crop Dimensions

Find and modify these values in the `imageCropper()` function:

```javascript
cropX: 100,        // Default X position
cropY: 100,        // Default Y position
cropWidth: 800,    // Default width
cropHeight: 600,   // Default height
```

### Default Crop Area (Percentage)

The initial crop area is set to 80% of the image. Modify this in `loadPreviewImage()`:

```javascript
this.cropWidth = Math.round(this.originalWidth * 0.8);   // Change 0.8 to desired percentage
this.cropHeight = Math.round(this.originalHeight * 0.8);
```

### Styling

Customize colors, sizes, and styles using Tailwind CSS classes or add custom CSS in the `<style>` section.

## 🐛 Troubleshooting

### Images Not Loading
- Ensure files are valid PNG format
- Check that JavaScript is enabled in your browser
- Try refreshing the page and reloading the images

### Crop Area Not Visible
- Make sure the image has loaded completely
- Try clicking Reset and reloading your images
- Check browser console for any error messages

### Downloads Not Working
- Check your browser's download settings
- Ensure popups are not blocked for local files
- Try a different browser if issues persist

### Performance Issues with Large Files
- The tool works best with images under 10MB each
- For very large images, process in smaller batches
- Close other browser tabs to free up memory

## 📝 Notes

- **File Format**: Currently supports PNG files only
- **Browser Storage**: No data is uploaded or stored remotely
- **Privacy**: All processing happens locally in your browser
- **Batch Size**: Limited only by browser memory
- **Output Format**: Cropped images are saved as PNG

## 🤝 Contributing

Feel free to fork this project and submit improvements. Some areas for potential enhancement:

- Support for additional image formats (JPEG, WebP, etc.)
- Preset crop dimensions
- Undo/redo functionality
- Crop history
- Keyboard shortcuts
- Touch device support
- Multiple crop areas
- Image rotation

## 📄 License

This project is released under the MIT License. You are free to use, modify, and distribute this tool for personal or commercial purposes.

## 🙏 Acknowledgments

Built with:
- [Alpine.js](https://alpinejs.dev/) - Lightweight reactive framework
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- [Bootstrap Icons](https://icons.getbootstrap.com/) - Beautiful open source icons

## 📧 Support

For issues, questions, or suggestions, please create an issue in the project repository or contact the maintainer.

---

**Version**: 1.0.0  
**Last Updated**: September 2025  
**Compatibility**: Modern web browsers with HTML5 support