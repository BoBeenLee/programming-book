# How To Limit Lines Of Text With CSS Only(JS없이 더보기 버튼 만들기)

- JS없이 더보기 버튼 만들기
- https://codesandbox.io/s/elegant-cloud-v0c730?file=/index.html:0-1697

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Static Template</title>
    <link href="./index.css" rel="stylesheet" />
  </head>
  <body>
    <article>
      <h2 class="cutoff-text">
        This is a static template, there is no bundler or bundling involved!
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia
        corporis consequuntur debitis repellat quos, nemo autem doloremque
        provident commodi optio quod libero ipsum in officiis amet asperiores
        est itaque deleniti.
      </h2>
      <input class="expand-btn" type="checkbox" />
    </article>
    <article>
      <h2 class="cutoff-text">
        This is a static template, there is no bundler or bundling involved!
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia
        corporis consequuntur debitis repellat quos, nemo autem doloremque
        provident commodi optio quod libero ipsum in officiis amet asperiores
        est itaque deleniti.
      </h2>
      <input class="expand-btn" type="checkbox" />
    </article>
    <article>
      <h2 class="cutoff-text">
        This is a static template, there is no bundler or bundling involved!
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia
        corporis consequuntur debitis repellat quos, nemo autem doloremque
        provident commodi optio quod libero ipsum in officiis amet asperiores
        est itaque deleniti.
      </h2>
      <input class="expand-btn" type="checkbox" />
    </article>
  </body>
</html>

```

```css
body {
  display: flex;
  flex-direction: row;
}

h2 {
  margin-bottom: 1rem;
}

.cutoff-text {
  --max-lines: 3;
  --line-height: 1.4;

  max-height: calc(var(--max-lines) * 1rem * var(--line-height));
  line-height: var(--line-height);

  overflow: hidden;
  position: relative;
}

.cutoff-text:has(+ .expand-btn:not(:checked))::before {
  content: "";
  position: absolute;
  height: calc(1em * var(--line-height));
  width: 100%;
  bottom: 0;
  pointer-events: none;
  background: linear-gradient(to bottom, transparent, white);
}

.expand-btn {
  appearance: none;
  border: 1px solid black;
  padding: 0.5em;
  border-radius: 0.25em;
  cursor: pointer;
  margin-top: 1rem;
}

.expand-btn:hover {
  background-color: #ccc;
}

.expand-btn::before {
  content: "Expand";
}

.expand-btn:checked::before {
  content: "Collapse";
}

.cutoff-text:has(+ .expand-btn:checked) {
  max-height: none;
}
```