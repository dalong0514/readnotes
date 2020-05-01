# 04 Getting Started with CSS

Cascading Style Sheets (CSS) are the means by which you specify the presentation (the appearance and the formatting) of an HTML document. In this chapter, I’ll show you how to create and apply CSS styles, explain why they are called cascading style sheets, and provide an overall foundation for future chapters. Table 4-1 provides the summary for this chapter.

Define a style. Use a property/value declaration.

Apply a style directly to an element. Use the style attribute to create an inline style.

Create a style that can be applied to multiple elements. Use the style element, and specify a selector and a number of style declarations.

Create styles that can be applied to multiple HTML documents. Create an external stylesheet, and reference it using the link element.

Determine which style properties will be used for a given element. Apply the cascade order to your source of styles, and calculate style specificity for tie-breaks.

Override the normal style cascade. Create an important style.

Use a style property defined by a parent. Use property inheritance.

Specify a property value in terms of another property. Use a relative unit of measure.

Calculate a property value dynamically. Use the calc function.

1『上面的，前半句是问题，后半句是解决方案。』

## 4.1 Defining and Applying a Style

A CSS style is made up of one or more declarations separated by a semi-colon. Each declaration consists of a CSS property and a value for that property separated by a colon. Listing 4-1 shows a simple style.

In this example, the style has two declarations. The first sets the value grey for the background-color property, and the second sets the value white for the color property.

There is a wide range of CSS properties available, and each controls some aspect of the appearance of the elements to which it is applied. In Chapters 19 through 24, I describe the available CSS properties and demonstrate their effect.

### 4.1.1 Understanding the CSS Properties Used in This Chapter

To demonstrate how CSS operates, I need to use some CSS properties that I don’t describe fully until later chapters. Table 4-2 lists these properties, gives a very brief description of them, and shows you which chapter contains full details.

padding. Specifies the amount of space between an element’s content and its border.

### 4.1.2 Applying a Style Inline

It isn’t enough to just define a style— you also need to apply it, effectively telling the browser which elements the style should affect. The most direct way to apply a style to an element is by using the style global attribute (described in Chapter 3), as shown in Listing 4-2.

Listing 4-2. Applying a Style Using the Style Global Attribute

```html
<!DOCTYPE HTML> 
<html>
<head> 
    <title>Example</title>
</head> 
<body>
    <a href="http://apress.com" style="background-color:grey; color:white">
        Visit the Apress website 
    </a> 
    <p>I like <span>apples</span> and oranges.</p> 
    <a href="http://w3c.org">Visit the W3C website</a> 
</body> 
</html>
```

There are four content elements in this HTML document—two hyperlinks (created with the a element) and a p element that contains a span element. I used the style global attribute to apply the style to the first a element—the one that links to the Apress web site. (You can learn more about the a, p, and span elements in Chapters 8 and 9. For the moment, you are interested only in applying styles.) The style attribute acts upon only the element to which it has been applied, as you can see in Figure 4-2.

The impact of the two CSS properties used in the example can be seen in the figure. The backgroundcolor property sets the color of the background of the element, and the color property sets the color of the foreground. The other two content elements in the HTML document are unaffected by the style.

THE ISSUE OF CSS RELIGION

CSS is a topic that seems to attract zealots. If you start reading any online discussion about how to achieve a certain effect with CSS, you soon see an argument about which is the right way. I have no time for people who make such arguments—the only right way to solve any problem is to use the knowledge and tools you have available to support as many of your users as possible. Tying yourself in knots to achieve CSS perfection is foolish. My advice is to ignore these arguments and adapt and develop the tricks and techniques that suit you and that you find pleasing and effective.

Creating an Embedded Style

Applying styles to individual elements can be a useful technique, but it is an inefficient approach when applied to a complex document that might require dozens of different styles. Not only do you have to apply the correct style to each element, but you have to be careful to correctly apply updates, which is an error-prone process. Instead, you can use the style element (as opposed to the style attribute) to define an embedded style and direct the browser to apply the style using a CSS selector. Listing 4-3 shows how you can use the style element with a simple CSS selector.

Listing 4-3. Using the Style Element





