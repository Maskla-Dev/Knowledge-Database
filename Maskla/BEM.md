#BEM #CSS #Patterns
*Block Element Modifier*  is a metodology for naming CSS components, BEM attempts to avoid collisition class names.
* **Block:** is a block if it is a container, self meaningful and does not require another section style overload. Class name should be writen as the section name
```HTML
<div class="Client">
<!--> CLient section block <-->
</>
```
* **Elements**: is an element if it is embeded in a container and its meaning depends from the section container. Class name should be writen as the section name, double underscore and the meaning of the content tag.
```HTML
<p class="Client__Name">Rigoberto</p>
```
* **Modifier**: Is a modifier if the element is a class variant. Classname should be writen as the section name, double underscore, element name, double hyphen and the variant name.
```HTML
<p class="Client__Name--CEO"></p>
```
