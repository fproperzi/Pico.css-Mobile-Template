# 📱 Pico.css Mobile Template - Modern tiny Mobile Alternative 

Ultra-lightweight mobile web app with Pico CSS. Features: responsive lists with search, side panels, async dialogs, toast system. Perfect for PHP backends!

![Weight](https://img.shields.io/badge/Weight-~19KB-brightgreen)
![CSS](https://img.shields.io/badge/CSS-Pico_CSS-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)


## 🎬 Live Demo

👉 **Try it now:**  

> 🚀 [https://fproperzi.github.io/Pico.css-Mobile-Template/](https://fproperzi.github.io/Pico.css-Mobile-Template/)

> 🧩 Fully interactive demo — open it on mobile or resize your browser to experience the responsive layout.


## 🎯 Features

### 📋 Lists and Search
- ✅ ListView with 80×80px avatars
- ✅ Real-time search with filter
- ✅ Alphabetical dividers
- ✅ 20 sample contacts with images
- ✅ Touch-optimized layout

### 📱 Navigation
- ✅ **Multi-page** (4 pages: Home, Form, Test, Info)
- ✅ **Responsive header** - Burger menu on mobile, horizontal nav on desktop
- ✅ **Footer with tabs** - Always visible quick navigation
- ✅ **Side panels** - Menu (left) and Settings (right)
- ✅ Sticky headers in panels during scroll

### 💬 Dialogs and Notifications
- ✅ **Custom Alert, Confirm, Prompt** with async/await (synchronous behavior)
- ✅ **Toast system** with 4 types: Success, Error, Warning, Info
- ✅ **Multiple toasts** - Automatic stack with progress bar
- ✅ **Auto-dismiss** configurable
- ✅ Complete test page for dialogs and toasts

### 🎨 Design
- ✅ **Pico CSS** (only ~13KB) - Minimal CSS framework
- ✅ **Material Design colors** (blue #2196F3)
- ✅ **Fully responsive** - Mobile, tablet, desktop
- ✅ **Dark mode ready** - Prepared for dark theme

### ⚙️ Form Features
- ✅ Validated form with all HTML5 controls
- ✅ Input text, email, tel, select, checkbox, Pico style!
- ✅ Integrated error handling


## 📊 Weight and Performance

### Weight breakdown (original/gzipped):
```
				Original       Gzipped 
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Pico CSS (CDN):   ~81 KB		~13 KB	
Custom CSS:       ~14 KB        ~ 3 KB
JavaScript:       ~11 KB        ~ 3 KB
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL:           ~106 KB        ~19 KB
```

## 🚀 Installation and Usage

### Download
```bash
# Clone the repository
git clone https://github.com/fproperzi/Pico.css-Mobile-Template.git

# Or download the HTML file directly
```

### Basic Usage
```html
<!-- Just open index.html in your browser! -->
<!-- Or serve it with PHP -->
php -S localhost:8000
```

### Integration with PHP

#### 1. Dynamic list from database:
```php
<?php
$contacts = $db->query("SELECT * FROM contacts ORDER BY name")->fetchAll();
?>

<ul class="listview" id="contactList">
    <?php 
    $current_letter = '';
    foreach ($contacts as $c): 
        $letter = strtoupper($c['name'][0]);
        if ($letter !== $current_letter):
            $current_letter = $letter;
    ?>
        <li class="list-divider"><?= $letter ?></li>
    <?php endif; ?>
    
    <li data-name="<?= htmlspecialchars($c['name']) ?>">
        <a href="detail.php?id=<?= $c['id'] ?>">
            <img src="<?= $c['avatar'] ?>" alt="<?= $c['name'] ?>" class="list-item-avatar">
            <div class="list-item-content">
                <div class="list-item-title"><?= htmlspecialchars($c['name']) ?></div>
                <div class="list-item-subtitle"><?= htmlspecialchars($c['role']) ?> • <?= htmlspecialchars($c['email']) ?></div>
            </div>
            <div class="list-item-after">›</div>
        </a>
    </li>
    <?php endforeach; ?>
</ul>
```

#### 2. Dialogs and toasts in PHP:
```php
<?php
if ($_POST['action'] === 'save') {
    $result = saveContact($_POST);
    if ($result) {
        echo "<script>toastSuccess('Saved!', 'Contact added successfully');</script>";
    } else {
        echo "<script>toastError('Error', 'Unable to save contact');</script>";
    }
}
?>
```

#### 3. Form with validation:
```php
<form method="post" onsubmit="return validateForm()">
    <label>
        Name
        <input type="text" name="name" required>
    </label>
    <label>
        Email
        <input type="email" name="email" required>
    </label>
    <button type="submit">Save</button>
</form>

<script>
async function validateForm() {
    const name = document.querySelector('[name="name"]').value;
    
    if (name.trim() === '') {
        await alert('Name is required!');
        return false;
    }
    
    const confirm = await confirm('Save contact?');
    return confirm;
}
</script>
```

## 📚 JavaScript API

### Dialogs (Synchronous with async/await)
```javascript
// Alert
await alert('Important message');

// Confirm
const response = await confirm('Are you sure?');
if (response) {
    // User clicked OK
}

// Prompt
const name = await prompt('What is your name?', 'John');
if (name !== null) {
    console.log('Name entered:', name);
}
```

### Toasts
```javascript
// Single toasts
toastSuccess('Title', 'Success message');
toastError('Error', 'Something went wrong');
toastWarning('Warning', 'Check your data');
toastInfo('Info', 'New version available');

// With custom duration (default: 4000ms)
toastSuccess('Saved', 'File saved', 6000);

// Remove all toasts
clearAllToasts();
```

### Navigation
```javascript
// Change page
goToPage('page-form');

// Go back
goBack();

// Open panel
openPanel('left');  // Menu
openPanel('right'); // Settings

// Close panel
closePanel();
```

## 🛠️ Customization

### Change colors:
```css
:root {
    --primary: #2196F3;        /* Blue - change as needed */
    --primary-hover: #1976D2;
}
```

### Add new pages:
```html
<!-- 1. Add the HTML page -->
<div class="page" id="page-new">
    <header class="app-header">
        <div class="header-inner">
            <div class="header-left">
                <button class="header-btn" onclick="goBack()">‹ Back</button>
            </div>
            <h1 class="header-title">New Page</h1>
            <div class="header-right"></div>
        </div>
    </header>
    
    <div class="page-content">
        <div class="content-wrapper">
            <!-- Content -->
        </div>
    </div>
</div>

<!-- 2. Add link in menu/footer -->
<a href="#" onclick="goToPage('page-new'); return false;">New</a>
```

## 🌐 Browser Support

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

## 📝 File Structure
```
Pico.css-Mobile-Template/
├── index.html          # Main file (all-in-one)
└── README.md           # This file

```

## 🎓 Ideal Use Cases

- ✅ Simple **admin panels**
- ✅ **CRUD applications** with PHP
- ✅ Lightweight **contact managers** / CRMs
- ✅ Corporate **dashboards**
- ✅ **Internal apps** for small teams
- ✅ Quick **prototypes**
- ✅ Any project needing a **fast and lightweight** frontend

## ❌ When NOT to Use

- ⚠️ Complex Single Page Applications (better with React/Vue)
- ⚠️ Apps with advanced client-side routing
- ⚠️ Projects requiring Framework7/Ionic (native mobile apps)

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

Feel free to check the [issues page](https://github.com/fproperzi/Pico.css-Mobile-Template/issues).

## 📄 License

MIT License - Feel free to use this project however you like.

## 🙏 Credits

- **Pico CSS** - https://picocss.com/
- **Pravatar** - https://pravatar.cc/ (demo avatars)
- Inspired by **jQuery Mobile** for ease of use

## 📧 Contact

For questions or suggestions, open an issue on GitHub.

---

⭐ If you find this project useful, give it a star on GitHub!

## 🌍 Languages

- [English](README.md) (this file)

