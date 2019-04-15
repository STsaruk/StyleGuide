# Selector naming
При верстке мы используем методологию [BEM naming convention](https://ru.bem.info/methodology/naming-convention/).  
Мы не используем подход BEM полностью а берем только её часть "Соглашение по именованию".
Стиль именования - [Two Dashes](https://ru.bem.info/methodology/naming-convention/#Стиль-two-dashes)

На Frontend части мы используем Vue.js. В Vue.js компонентный подход к разработке. Если смешать это с BEM согласованием по именованию то сам компонент является блоком а все что внутри компонента его элементами. 
Пример

**файл some-block.vue**
```html
<div class="some-block">
  <h2 class="some-block__title">Some title</h2>
  <p class="some-block__text">Some text</p>
</div>
```

# CSS/SCSS styles

**Группировка css свойств**

Свойства должны быть определены в группы.     
Порядок расположения свойств:   
1. **Расположение элемента относительно других:** position, left/right/top/bottom, float, clear, z-index.  
2. **Размеры и отступы:** width, height, margin, padding…  
3. **Типографика:** font, color…  
4. **Цветовое и стилевое оформление:** background, border  
5. **Общее оформление содержимого:** list-style-type, overflow  
6. **Миксины:** @apply --box-styles, @apply --clear 

```css
.some-block { 
  /* Позиционирование */
  position: absolute; 
  left: 0;
  top: 0;
  
  /* Размеры и отступы */
  width: 100px;
  height: 100px;
  margin: 10px;
  padding: 0 0 6px 0; 
  
  /* Типографика */
  color: red;       
  font-size: 16px;
  font-style: italic;  
  font-weight: bold;
  
  /* Цветовое и стилевое оформление */
  background: #fff;
  border: 1px solid #fff;
  
  /* Общее оформление содержимого */
  overflow: hidden;
  transition: color .2s ease;
  
  /* Миксины */ 
  @apply --box-styles;
}

```

**Вложенность селекторов**

В этой части верстки я бы предложил придерживаться правила: ‘не более 2 уровней вложенности ’. За исключением тех ситуаций когда мы работаем с псевдо классами. 

**Плохой пример**
```scss
.game__bonus {
   &-img {
       &:after {}
       &--center {
        }
   }
}
```
**Хороший пример**
```scss
.game__bonus {}
.game__bonus-img {}
.game__bonus-img {
     &:after {
      }
}
.game__bonus-img--center {}
```

**Сокращение CSS свойств**

1) Если вы назначаете только одно свойство из 4, например padding-left: 10px, не нужно переопределять сразу все четыре свойства padding: 0 10px 0 0; кроме случаев, когда мы определяем 3 и больше свойства
2) Это относится и к цвету. Если нам нужно назначить только цвет фона элемента - не стоит писать сокращенно background: red; Нужно назначить background-color: red. В этом случае переопределяется только цвет, а не все остальные значение, которые доступны свойству background
3) Если нам нужно определить плавность анимации через transition - не стоит задавать через свойство all, нужно задать только то свойство, которое мы анимируем 

**Плохой пример**
```scss
.element {
    color: red;
    transition: all .2s ease
}

```
**Хороший пример**
```scss
.element {
    color: red;
    transition: color .2s ease
}

```
