## 1. Structure a site using semantic HTML to aid accessibility

We made sure we used consistent semantic html elements through out our project.<br />

```html
<footer>
    <blockquote>
        "Inflatable men don't care, they love you anyway."
        <cite> -Winston Churchill </cite>
    </blockquote>
</footer>
```

We could've used a ```<div>``` and ```<p>``` tag for this section without much difference in <br />
presentation and performance. But using a "blockquote" tag, used to indicate a quoted passage of text, <br />
and "cite" tag, used to indicate the source of the quote, provides a clear and structured description <br /> 
of the content in the footer, making it easier for both users and assistive technologies to understand the content.

## 2. Ensure a web page is readable for screen readers

We have utilised a number of techniques to ensure the content is readable for screen readers, <br />
making the web page more accessible for users with disabilities.

```html
<div class="bio-box">
  <div class="bio-box__body">
      <img tabindex="0" class="bio-box__image"
          src="https://imgs.search.brave.com/O_IZruYZ8nF-GDm6Qs_6mLdXl4sGICWXgy-tiTrksmk/rs:fit:1200:720:1/g:ce/aHR0cHM6Ly9pLnl0/aW1nLmNvbS92aS9y/aWlLd1JUNUZ0SS9t/YXhyZXNkZWZhdWx0/LmpwZw"
          alt="artistic representation of Zakarie as an inflatable man" />
  </div>
  <div class="bio-box__info flex row justify-around">
      <p class="bio-box__title">Zakarie</p>
      <p id="bio2-description" class="bio-box__description justified">
          Zakarie left home at 16 with only a backpack and a small loan of
          300 million from his parents to start his own inflatable men
          emporium.
          In 1789, his twice-removed great-cousin sharpened the blade of the
          first guillotine.
      </p>
      <button class="bio-box__button" type="button"
          aria-label="read more about Zakarie" aria-expanded="false"
          aria-activedescendant="bio2-description">
          Read more
      </button>
  </div>
</div>
```

- We used appropriate <b>"alt"</b> attributes for images to provide a brief and clear descriptions, <br />
allowing screen readers to communicate the content to users who are unable to see the image.<br /> <br />
- Additionally, we used *ARIA (Accessible Rich Internet Applications)* attributes to provide additional <br />
information about the content and its behavior. For example, the "aria-label" attribute on the "button" element <br />
provides a text description of the button's purpose, making it easier for screen readers to understand the button's function. <br /><br />
- Finally, we used descriptive class names and id values, which can also help screen readers understand the structure <br />
and content of the page. This makes it easier for users to navigate the page using their screen reader and find the <br />
information they need more quickly and efficiently.

## 3. Ensure our UI has sufficient colour contrast so that everyone can perceive it comfortably

## 4. Use various tools to check that our website meets accessibility criteria

## 5. Use CSS media queries to ensure our content is always presented effectively on screens of different sizes

## 6. Demonstrate a mobile-first approach to building a website

## 7. Use CSS variables to apply repeated colours to HTML elements

## 8. Use CSS Flexbox to style children in a single-direction layout (ie a row or a column)

## 9. Use CSS Grid to style children in two-direction layout

## 10. Ensure our Git commit history tells a coherent story

## 11. Use the appropriate input types in HTML forms for gathering different types of information
