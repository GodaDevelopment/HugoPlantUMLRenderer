# HugoPlantUMLRenderer



**Create a New Hugo Site:** Create a new Hugo site by running:

```bash
hugo new site my-hugo-site
cd my-hugo-site
```

**Start the Hugo Server:** Run the Hugo server to see your site:

```bash
hugo server
```
Visit `http://localhost:1313` to view your site.


**Create a Shortcode File:** In your Hugo project directory, navigate to `layouts/shortcode`s and create a file named `plantuml.html`.

```bash
mkdir -p layouts/shortcodes
touch layouts/shortcodes/plantuml.html
```

Add this code to `plantuml.html`

```html
<div class="plantuml-diagram">
    <textarea class="plantuml-code" style="display:none;">
    {{ .Inner }}
    </textarea>
    <img class="plantuml-image" src="" alt="PlantUML Diagram"/>
</div>

```
Create plantuml.js file then index it to your project 

```html
<script src="/js/plantuml.js" charset="utf-8"></script>
```


This Code will loop for all the rendered `.plantuml-diagram` then he will get the content of each then load it's diagram inside it.

```javascript

// Place under /js/plantuml.js

document.addEventListener("DOMContentLoaded", function () {
    function encodeHex(data) {
        return data.split('').map(function (c) {
            return c.charCodeAt(0).toString(16).padStart(2, '0');
        }).join('');
    }

    function compressToPlantUML(hex) {
        return "http://www.plantuml.com/plantuml/img/" + "~h" + hex;
    }

    document.querySelectorAll('.plantuml-diagram').forEach(function (container, index) {
        const textarea = container.querySelector('.plantuml-code');
        const img = container.querySelector('.plantuml-image');

        if (textarea && img) {
            const code = textarea.value;
            console.log("PlantUML Code:", code); 
            const hex = encodeHex(code);
            console.log("Encoded Hex:", hex); 
            img.src = compressToPlantUML(hex);
        }
    });
});


```


**Create a New Markdown Document:** Generate a new Markdown file for your content:
```bash
hugo new posts/my-first-post.md
```

```markdown
---
title: "My First Post"
date: 2024-09-07T00:00:00Z
draft: false
---

Here is a PlantUML diagram:

{{< plantuml >}}
@startuml
Alice -> Bob: test
@enduml
{{< /plantuml >}}


```

**Final Result:**

![image](https://github.com/user-attachments/assets/23f2cfa7-8b72-4711-8547-c0b116bc7038)







