All CSS Element as organized in the [[CSS Box Model]], which is a layout of nested boxes. ^4b2ab8

* **Padding** is the inner spacing of the element, which is placed inside the Border
* **Border** is the space between the Padding and the Margin, can be colored, added weight and style
* **Margin** is the empty space outside the element, which separates it from the other elements

![CSS Box Model Illustration|400](css_box_model.png)

Code example:
```css
.element{
	padding: 10px;
	border: 3px solid red;
	margin: 20px;
}
```

>[!TIP] if ``box-sizing: border-box`` is applied to an element, the padding and the border are calculated inside the limits of the element. 