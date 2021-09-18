# Margins and Padding

Spacing between heading elements, as well as paragraphs, list (any text element) are controlled by margin-top and margin-bottom.

There are built in defaults set by the browser:
* The left and right have a default of 0
* The top and bottom are equal to the font-size of the text within the element.

This is the final output we are building:

![](https://raw.githubusercontent.com/hoc-labs/images/main/responsive-design-bootcamp-img2.png)

This is the initial output without any styling.

![](https://raw.githubusercontent.com/hoc-labs/images/main/responsive-design-bootcamp-img3.png)



## Centering Content
* Center the content on the screen.

## Add Space Between Last Two Elements
* Use the existing styles to add more space between the last two paragraphs. Remember that the default margin size is equal to the font size of the element. So the font-size of the `<p>` is currently set to 18px. We can use this to estimate what the total margin should be: maybe try around 40px.

## Collapsing Margins

* Load the document in the browser and inspect the elements. 

Notice that the top margin of the `<h1>` element at the top extends beyond the upper border of the parent container element and the bottom margin of the `<p>` element at the bottom extends beyond the border of the parent container element.

Why is that?

We learned earlier that margins collapse. The margin between two elements will collapse to be the margin of the greatest among the two elements. So if the element on top has a margin-bottom of 50px and the element on the bottom has a margin-top of 50px the margin between them will be 50px, not 100px.

* add a margin-bottom:40px to the `p` style and look at the page. The space between the two paragraphs will not have changed because the margins were collapsed for a combined margin of 40px.
* change the margin-bottom to the `p` style to 100px and now look at the page. Now the margin is 100px;

Usually this behavior is helpful because it makes it predictable what the margin will be. You do not have to add together margins from neighboring elements. 

![](https://raw.githubusercontent.com/hoc-labs/images/main/responsive-design-bootcamp-img4.png)

But, there is an unexpected behavior. The marign of the first or last child is collapsed with the margin of the parent container.

Take a look at the `<p>` element at the bottom of the page. It has a margin-bottom of 100px, but it is not expanding the space between its border and the parent container. You would expect the black background-color to expand by 100px.

But this is not the case because the bottom margin of the last `<p>` and the bottom margin of the containing `<div>` are collapsing and the margin of the two share the margin of the containing `<div>`.

That is why the top margin of the `<h1>` element at the top of the parent container extends beyond the top of the parent container instead of pushing the top border of the parent container. The same issue for the `<p>` element at the bottom of the container.

Therefore, you cannot add a margin-top to the first child or the last child to add a margin to the child elements. It is very noticeable here with the black background of the parent container. If you add margin-top:40px to the `<h1>` element, it will add to the collapsed margin that the `<h1>` element shares with the parent `<div>` element (.card margin-top:0, so collapsed total is 40px) and the margin will be on the `<div>` element and that has a white background.

![](https://raw.githubusercontent.com/hoc-labs/images/main/responsive-design-bootcamp-img5.png)

### A Design Pattern to Solve This Issue

Use padding on the parent container instead of setting margin-top on the first child element.

Create a general style rule to turn off margin-top on typography releated elements, such as paragraphs, headings, lists.

This pattern is beneficial because margins do not collapse when using flexbox and grid.

That way we can get consistent spacing within a parent container.

We can create a single selector to match all of these typography elements:

```css
h1, h2, h3, h4, h5, h6, p, ul {
  margin-top:0;
}
```
We cannot use the same technique of creating a general rule to deal with the last child element because we will run into trouble when two of the same elements are next to eachother.

For example, if we set the margin-top and margin-bottom of `<p>` elements to 0, then if one follows another in the parent container, there will be no margin between them.

Therefore, the solution for the last child is to explicitly set the margin-bottom to 0 on that element.

# Inline Text Styling
Span elements are non-semantic elements that are used to target styling of inline elements. They are useful for styling inline text.

* add a span element around the text `ultricies integer`, with a class named accent-color, to change the color to yellow.

# Link Styling

We can style a link just like any other element, such as:

```css
a {
  color:orange;
}
```

But links also have a set of states that we can style as well. 
* Link: Default state.
* Visited: visited the link already (typically only used on external links)
* Focus: navigating a web site by keyboard.
* Hover: mouse or cursor hovering over the link
* Active: style while actively clicking on it.

To style these we use something known as **pseudo-classes**.

Try styling some of these pseudo classes to see how the behave.
* change the color of the focus state to aquamarine.
* change the color of the hover state to red. 

### Important Specificity of Link Pseudo Classes

It is important to make sure that the styles are ordered correctly in your CSS file. For example, the `a` style will override `a:focus, a:hover` styles if it comes after them because the a selector will be the last one that matches.

The same issue applies to the a:hover and a:focus. They are pretty much equivalent to each other, so the last one wins. Usually the focus and hover states are the same.

If you put a:link last, none of the previous settings will apply because the a:link selector will always match and override any of the previous ones. So it should always go first, after any generic `a` styles.

A good pattern is to start with the 

```css
a {
    color: #FFE600;
}
```

This style will cover all of the cases: a:hover, a:link, a:focus. Then you can just add the ones you want to override after it.

### Make Link Styling Obvious

 * change the color on hover, focus
 * leave the text-decoration on, or if remove it, make sure it's obvious that it's a link.
 * remember to include styles for focus











