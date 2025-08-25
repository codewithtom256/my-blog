---
layout: ../../layouts/MarkdownLayout.astro
title: "My First Blog Post"
pubDate: 2022-07-01
description: "This is the first post of my new Astro blog."
author: "Astro Learner"
image:
  url: "https://docs.astro.build/assets/rose.webp"
  alt: "The Astro logo on a dark background with a pink glow."
tags: ["astro", "blogging", "learning in public"]
---

# Building a Complete Photo Gallery: Step-by-Step Guide

Welcome! In this tutorial, we'll build a photo gallery from scratch, covering everything from HTML structure to backend integration. We'll use real images, code snippets, and explanations for each step.

---

## Step 1: Gather Your Images

Start by selecting a few images for your gallery. You can use your own photos or royalty-free images from Unsplash.

**Example Images:**

- ![Sunset](https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=400&q=80)
- ![Mountains](https://images.unsplash.com/photo-1465101046530-73398c7f28ca?auto=format&fit=crop&w=400&q=80)
- ![Forest](https://images.unsplash.com/photo-1444065381814-865dc9da92c0?auto=format&fit=crop&w=400&q=80)
- ![Beach](https://plus.unsplash.com/premium_photo-1683910767532-3a25b821f7ae?q=80&w=1408&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

---

## Step 2: Create the HTML Structure

Let's lay out the gallery using HTML. Each image will be inside a container for easy styling.

```html
<div class="gallery">
  <img src="sunset.jpg" alt="Sunset">
  <img src="mountains.jpg" alt="Mountains">
  <img src="forest.jpg" alt="Forest">
  <img src="beach.jpg" alt="Beach">
</div>
```

If you're using external images, update the `src` attributes accordingly.

---

## Step 3: Style the Gallery with CSS

Make your gallery visually appealing. We'll use Flexbox for layout and add some effects.

```css
.gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
  margin: 2rem 0;
}
.gallery img {
  width: 220px;
  height: 150px;
  object-fit: cover;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.18);
  transition: transform 0.2s, box-shadow 0.2s;
  cursor: pointer;
}
.gallery img:hover {
  transform: scale(1.08);
  box-shadow: 0 8px 32px rgba(0,0,0,0.22);
}
```

---

## Step 4: Add Interactivity with JavaScript

Let’s allow users to click an image to view it larger in a modal.

**HTML for Modal:**

```html
<div id="modal" class="modal">
  <span id="close">&times;</span>
  <img id="modal-img" src="" alt="">
</div>
```

**CSS for Modal:**

```css
.modal {
  display: none;
  position: fixed;
  z-index: 100;
  left: 0; top: 0;
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.7);
  justify-content: center;
  align-items: center;
}
.modal img {
  max-width: 80vw;
  max-height: 80vh;
  border-radius: 16px;
}
#close {
  position: absolute;
  top: 2rem;
  right: 3rem;
  color: #fff;
  font-size: 2.5rem;
  cursor: pointer;
}
```

**JavaScript for Modal Functionality:**

```javascript
const images = document.querySelectorAll('.gallery img');
const modal = document.getElementById('modal');
const modalImg = document.getElementById('modal-img');
const closeBtn = document.getElementById('close');

images.forEach(img => {
  img.addEventListener('click', () => {
    modal.style.display = 'flex';
    modalImg.src = img.src;
    modalImg.alt = img.alt;
  });
});

closeBtn.addEventListener('click', () => {
  modal.style.display = 'none';
});
```

---

## Step 5: Responsive Design

Make sure your gallery looks good on all devices.

```css
@media (max-width: 600px) {
  .gallery img {
    width: 100px;
    height: 70px;
  }
  .modal img {
    max-width: 95vw;
    max-height: 60vh;
  }
}
```

---

## Step 6: Backend Integration with Python Flask

Suppose you want to serve images dynamically from a backend. Here’s a simple Flask example:

**Directory Structure:**
```
/static/images/
  sunset.jpg
  mountains.jpg
  forest.jpg
  beach.jpg
/templates/
  gallery.html
app.py
```

**app.py:**

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def gallery():
    photos = [
        {'url': '/static/images/sunset.jpg', 'alt': 'Sunset'},
        {'url': '/static/images/mountains.jpg', 'alt': 'Mountains'},
        {'url': '/static/images/forest.jpg', 'alt': 'Forest'},
        {'url': '/static/images/beach.jpg', 'alt': 'Beach'},
    ]
    return render_template('gallery.html', photos=photos)
```

**gallery.html:**

```html
<div class="gallery">
  {% for photo in photos %}
    <img src="{{ photo.url }}" alt="{{ photo.alt }}">
  {% endfor %}
</div>
```

---

## Step 7: Building the Gallery in React

Here’s how you can render the gallery in React, with modal functionality:

```jsx
import { useState } from 'react';

function Gallery({ photos }) {
  const [modalPhoto, setModalPhoto] = useState(null);

  return (
    <>
      <div className="gallery">
        {photos.map(photo => (
          <img
            key={photo.url}
            src={photo.url}
            alt={photo.alt}
            onClick={() => setModalPhoto(photo)}
          />
        ))}
      </div>
      {modalPhoto && (
        <div className="modal" onClick={() => setModalPhoto(null)}>
          <img src={modalPhoto.url} alt={modalPhoto.alt} />
        </div>
      )}
    </>
  );
}
```

---

## Step 8: Accessibility Tips

- Always use descriptive `alt` text for images.
- Ensure modal dialogs are keyboard accessible.
- Use sufficient color contrast for overlays and controls.

---

## Step 9: Final Touches

- Add captions or titles below images.
- Allow users to upload their own images (advanced).
- Optimize images for faster loading.

---

## Conclusion

You’ve built a fully functional, interactive, and responsive photo gallery using HTML, CSS, JavaScript, Python Flask, and React. Try customizing it with your own images, styles, and features!

---

**Demo Gallery:**

![Sunset](https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=400&q=80)
![Mountains](https://images.unsplash.com/photo-1465101046530-73398c7f28ca?auto=format&fit=crop&w=400&q=80)
![Forest](https://images.unsplash.com/photo-1444065381814-865dc9da92c0?auto=format&fit=crop&w=400&q=80)
![Beach](https://plus.unsplash.com/premium_photo-1683910767532-3a25b821f7ae?q=80&w=1408&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

Happy coding!